---
layout: article
title: "Vermail: the Sync Engine"
date: 2026-11-02
categories: [ vermail ]
tags: [ vermail, imap, sync, qresync, uidvalidity, java ]
author: Joseph
description: >
  The local store is a rebuildable projection of IMAP, and sync is three conversations: full
  snapshot, flag delta (CONDSTORE), and state diff (QRESYNC). The interesting part is reconciliation.
---

The first decision in Vermail was that the local store is a rebuildable
projection of the server, not a second source of truth. Once that's settled,
sync is just a question of asking the server for changes as cheaply as possible.

There are three ways to do that. The sync plan picks the strongest one the
server supports.

- **Full snapshot.** Fetch everything. Always works, always expensive.
- **Flag delta (CONDSTORE, RFC 7162).** The server tells you which flags changed
  since your last look. Only flags travel here; the delta engine can't see
  expunges, and doesn't pretend it can.
- **State diff (QRESYNC).** The server names the expunged UIDs (`vanishedUids`),
  so an expunge costs a diff instead of a rediscovery.

Each delta path is its own class, `FlagChanges` for CONDSTORE and `StateDiff`
for QRESYNC. Neither pretends to see what the other sees.

UIDVALIDITY is handled in one place, `UidValidityChange`. An announced change is
`FIRST_CONTACT`, `UNCHANGED`, or `REKEYED`, and only `REKEYED` invalidates the
projection. The rest of the engine asks this kernel instead of reasoning about
epochs itself.

Push is one `IdleHolder` per push-capable account, re-armed at 24 minutes with a
1-second to 5-minute backoff.

The part I keep returning to is reconciliation. It runs on the first sync, on
every tenth, and on any failure, and it fail-open. It doesn't try to repair a
broken projection by guessing; it asks the server for the truth and lets the
diff be the answer.

The honest reason is that I don't trust my cache to stay valid. UIDs are only
stable until the server rekeys them, and a user can delete a message from their
web app while my local copy still thinks it exists. No concrete failure has hit
me yet, the project is too young. But that's exactly when I want the question
answered, before I'm debugging someone's vanished inbox.
