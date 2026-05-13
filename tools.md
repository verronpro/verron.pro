---
layout: page
title: Practices & Tools
aside:
  toc: true
---

Welcome to the toolbox I use as a **software craftsman, coach in software engineering best practices, and tech lead**. This catalogue intentionally steps beyond the ubiquitous corporate standards — Draw.io, Visio, Confluence, Jira — and instead explores tools and practices that are often simpler, more open, and in many cases more effective. My hope is that you’ll discover something unexpected that makes your daily work better.

---

## Documentation & Communication

These are the textual languages and tools I use to describe systems, draw diagrams, plot data, and publish documentation. All of them are plain‑text friendly, versionable, and designed to live alongside source code.

### Diagrams as code
Instead of dragging boxes, I describe diagrams in a simple language. The result is readable in a diff, reviewable in a pull request, and never out of sync.

- **Graphviz / Dot language** — Render graphs from a textual description of nodes and edges.  
  [https://graphviz.org/](https://graphviz.org/) | [Layout engines](https://www.graphviz.org/docs/layouts/) | [Repository](https://gitlab.com/graphviz/graphviz)

- **Mermaid** — JavaScript‑based diagrams from Markdown‑like syntax. Ideal for READMEs and wikis.  
  [https://mermaid.js.org/](https://mermaid.js.org/) | [CLI](https://github.com/mermaid-js/mermaid-cli)  
  Supported kinds: Flowchart, Sequence Diagram, Gantt, Pie, User Journey, Entity Relationship, State, Class.

- **PlantUML** — A Swiss‑army knife for software architecture and process diagrams.  
  [https://plantuml.com/](https://plantuml.com/) | [Themes](https://plantuml.com/skinparam)  
  Supported kinds: Sequence, Use Case, Class, Activity, Component, State, Network Time, JSON/YAML visualisation, SALT GUI prototyping, Gantt, Mindmap, Work Breakdown Structure, Entity Relationship.

- **Kroki** — A unified API to render all of the above, perfect for CI pipelines and tools without native diagram support.  
  [https://kroki.io/](https://kroki.io/)

### Other text‑to‑diagram DSLs
Smaller, specialised tools that turn ASCII art or concise text into clean graphics.

- **Mingram** — Experimental diagramming DSL for learning how visual thinking can be encoded.
- **Blockdiag / nwdiag / seqdiag / actdiag** — Simple Python tools for block, network, sequence, and activity diagrams.  
  [http://blockdiag.com/](http://blockdiag.com/)
- **svgBob** — Converts ASCII‑art diagrams into polished SVG.  
  [https://github.com/ivanceras/svgbob](https://github.com/ivanceras/svgbob)
- **ditaa** — Diagrams Through ASCII Art; renders ASCII drawings into bitmaps.  
  [https://ditaa.sourceforge.net/](https://ditaa.sourceforge.net/)
- **shaape** — ASCII‑art to SVG with stylistic flexibility.  
  [https://github.com/christiangoltz/shaape](https://github.com/christiangoltz/shaape)
- **ascii2svg** — Lightweight ASCII‑diagram to SVG converter.  
  [https://github.com/derhuerst/ascii2svg](https://github.com/derhuerst/ascii2svg)

### Plotting, charting and science
When raw numbers need visual form.

- **GnuPlot** — Command‑line 2D/3D plotting for scriptable, reproducible graphs.  
  [http://www.gnuplot.info/](http://www.gnuplot.info/) | [Introduction PDF](https://www.phys.uconn.edu/~rozman/Courses/P2200_16F/downloads/gnuplot-introduction-2016-10-25.pdf)

- **Chart.js** — Interactive, browser‑based charts (Line, Bar, Radar, Polar, Pie, Doughnut, Bubble).  
  [https://www.chartjs.org/](https://www.chartjs.org/)

- **MathJax** — Beautiful mathematical notation in web pages.  
  [https://www.mathjax.org/](https://www.mathjax.org/)

### Writing and publishing
- **Markdown** — The plain‑text markup language that powers almost all my writing.  
  [https://daringfireball.net/projects/markdown/](https://daringfireball.net/projects/markdown/)
- **Jekyll** — The static site generator behind this blog (Ruby‑powered).  
  [https://jekyllrb.com/](https://jekyllrb.com/)
- **AsciiDoc** — A more powerful markup language for technical documentation, with native support for admonitions, barcodes, memes, and Reveal.js slides.  
  [https://asciidoc.org/](https://asciidoc.org/) | [Reveal.js converter](https://docs.asciidoctor.org/reveal.js-converter/latest/) | [Syntax highlighting](https://docs.asciidoctor.org/reveal.js-converter/latest/converter/syntax/syntax-highlighting/) | [Barcode extension](https://docs.asciidoctor.org/diagram-extension/latest/diagram_types/barcode/) | [Admonitions](https://docs.asciidoctor.org/asciidoc/latest/syntax-quick-reference/#admonitions)

---

## Development Environment & Setup

A well‑tuned workspace that supports multiple identities, multiple language runtimes, and multiple operating systems.

- **Git** — Distributed version control, the backbone of my work. I also use self‑hosted Git servers (GitLab CE, Gitea) for full data sovereignty.  
  [https://git-scm.com/](https://git-scm.com/) | [GitLab CE](https://about.gitlab.com/install/) | [Gitea](https://gitea.io/)

- **Multi‑identity Git & SSH** — Configure different SSH keys and Git identities per repository.  
  [Specify different SSH keys for a domain](https://thucnc.medium.com/how-to-specify-different-ssh-keys-for-git-push-for-a-given-domain-bef56639dc02) | [Fixing wrong user on push](https://stackoverflow.com/questions/21615431/git-pushes-with-wrong-user-from-terminal) | [Fixing wrong SSH key](https://www.howtogeek.com/devops/how-to-fix-git-using-the-wrong-ssh-key-account/) | [SSH config not read](https://stackoverflow.com/questions/60786635/git-uses-the-wrong-identity-ssh-config-file-not-read)

- **Ubuntu & Java** — Switch the default JDK version on Ubuntu.  
  [https://attacomsian.com/blog/change-default-java-version-ubuntu](https://attacomsian.com/blog/change-default-java-version-ubuntu)

- **Spring Expression Language (SpEL)** — Dynamic expression power used carefully for template resolution and conditional logic.  
  [Spring SpEL reference](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#expressions) | [Spring Boot + H2 tutorial](https://www.baeldung.com/spring-boot-h2-database)

- **WSL (Windows Subsystem for Linux)** — Run a full Linux environment inside Windows for a consistent toolchain.  
  [https://github.com/microsoft/WSL](https://github.com/microsoft/WSL)

- **Web hosting** — [Gandi.net](https://www.gandi.net/) for simple, privacy‑respecting domain and hosting.

---

## Automation & AI

Automation frees developers for higher‑value work; AI, used carefully, can become a powerful pair partner. I treat both with curiosity and a sharp eye on security.

### Low‑code automation
- **n8n** — Low‑code workflow automation for gluing together internal tools, notifications, and data pipelines. I build integrations that call AI platform APIs.  
  [https://n8n.io/](https://n8n.io/)
- **Node‑RED** — Flow‑based programming for wiring together hardware devices, APIs, and online services. Often used in IoT and automation contexts.  
  [https://nodered.org/](https://nodered.org/)

### Local AI
- **Ollama** — Run large language models locally, privately, and without cloud dependency.  
  [https://ollama.com/](https://ollama.com/)

### Generative AI experiments
I actively experiment with both cloud‑based and local assistants, always applying strict cybersecurity rules: **no sensitive code leaves my machine, prompts are sanitised, local‑first when possible, and every AI suggestion is reviewed like an untrusted junior developer’s pull request**.

- **ChatGPT** — [https://chat.openai.com/](https://chat.openai.com/)
- **OpenAI API platform** — [https://platform.openai.com/](https://platform.openai.com/)
- **GitHub Copilot** — AI pair programmer embedded in the editor (also available as Copilot for Web and Microsoft 365).  
  [https://github.com/features/copilot](https://github.com/features/copilot)
- **Google Gemini** — Used for Android app experiments and exploring multimodal AI.  
  [https://gemini.google.com/](https://gemini.google.com/)
- **Junie AI, Kimi, DeepSeek, Liangma** — A set of cloud and local‑capable assistants I evaluate for real‑world programming tasks.

### AI‑assisted development in practice
I use the above tools while building **office‑stamper** (see Repositories). The goal is to improve my workflow — from scaffolding code to explaining unfamiliar libraries — while keeping the human firmly in control. It’s pair programming with a machine, not a replacement for craftsmanship.

---

## Collaborative Practices & Product Thinking

How teams organise, name their work, and split requirements has a bigger impact than any technology choice.

- **Conway’s law** — Organisations design systems that mirror their communication structures. I use this insight to reshape architectures and team boundaries together.
- **Commit naming rules (Conventional Commits)** — Machine‑readable commit history that generates changelogs and reduces release friction.  
  [https://www.conventionalcommits.org/](https://www.conventionalcommits.org/) | [Guide](https://developerexperience.io/articles/commit-naming-rules) | [Tag naming](https://github.com/naming-convention/naming-convention-guides/blob/master/git/tag-naming.md)
- **Team Topologies** — A model for designing teams around the flow of value, lowering cognitive load.  
  [https://teamtopologies.com/](https://teamtopologies.com/) | [Workbook](https://teamtopologies.com/workbook) | [Infographic](https://teamtopologies.com/infographic/team-topologies-in-a-nutshell-infographic) | [Team Shape Templates](https://github.com/TeamTopologies/Team-Shape-Templates)
- **Jugement Majoritaire (Majority Judgment)** — A voting method that yields nuanced group decisions; useful for retrospectives and prioritisation.  
  [https://app.mieuxvoter.fr/](https://app.mieuxvoter.fr/)
- **BDD (Behaviour‑Driven Development)** — Describe system behaviour in plain language that becomes executable tests.  
  [https://cucumber.io/docs/bdd/](https://cucumber.io/docs/bdd/)
- **User Story splitting** — Techniques that break large stories into valuable, independently deliverable increments.  
  [LinkedIn advice](https://www.linkedin.com/advice/3/what-best-tools-techniques-splitting) | [Practical guide](https://techbeacon.com/app-dev-testing/practical-guide-user-story-splitting-agile-teams) | [Medium article](https://ancaonuta.medium.com/how-to-split-user-stories-b55f20ea0a4e)
- **“It Depends”** — A reminder that every software decision is context‑dependent.  
  [https://blog.frankel.ch/it-depends/](https://blog.frankel.ch/it-depends/)

---

## Technical Disciplines & Craftsmanship

The day‑to‑day practices that turn code into well‑crafted software.

### Foundations
- **[Agile Manifesto Principles](https://agilemanifesto.org/principles.html)** — The compass I still navigate by.
- **Software Craftsmanship Manifesto** — An explicit commitment to well‑crafted software, continuous learning, and productive partnerships.  
  [http://manifesto.softwarecraftsmanship.org/](http://manifesto.softwarecraftsmanship.org/)
- **TDD (Test‑Driven Development)** — Writing the test first as a design technique, not just a testing technique.  
  [Kata 1](https://osherove.com/tdd-kata-1) | [TDD book by Kent Beck](https://www.amazon.com/Test-Driven-Development-Kent-Beck-ebook/dp/B095SQ9WP4)
- **Design patterns & refactorings** — Reusable solutions that improve communication and structure.  
  [Refactoring Guru](https://refactoring.guru/design-patterns) | [GoF tutorial](https://www.digitalocean.com/community/tutorials/gangs-of-four-gof-design-patterns) | [Patterns reference](https://www.gofpatterns.com/) | [PDF reference](http://w3sdesign.com/GoF_Design_Patterns_Reference0100.pdf) | [Refactoring to Patterns (Fowler)](https://www.martinfowler.com/books/r2p.html)
- **Clean Architecture** — Isolate business logic from frameworks so that the system is testable and adaptable.  
  [Beginner’s guide](https://betterprogramming.pub/the-clean-architecture-beginners-guide-e4b7058c1165) | [Uncle Bob’s original post](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

### Katas (deliberate practice)
Repetition of small exercises to internalise technique.
- [TDD Kata 1](https://osherove.com/tdd-kata-1) | [String Calculator](https://kata-log.rocks/string-calculator-kata) | [GitHub topic](https://github.com/topics/string-calculator-kata) | [Code Review example](https://codereview.stackexchange.com/questions/128361/tdd-kata-string-calculator)
- [Awesome Katas](https://github.com/gamontal/awesome-katas) | [Ultimate Code Kata (Jeff Atwood)](https://blog.codinghorror.com/the-ultimate-code-kata/) | [Don’t Code Katas (counterpoint)](https://simpleprogrammer.com/dont-code-katas/)
- [Software Craftsmanship KATA](https://github.com/HoucemNaffati/A-Software-Craftsmanship-KATA) | [Incremental Katas](https://github.com/Gianfrancoalongi/incremental_katas/tree/master)
- [Architecture katas](http://fundamentalsofsoftwarearchitecture.com/katas/) | [Craftsmanship katas site](https://katas.softwarecraftsmanship.org/)
- [The Diamond Kata in APL](https://www.dyalog.com/blog/2015/01/the-diamond-kata/) | [Trivia refactoring kata (Emily Bache)](https://github.com/emilybache/trivia)

### Code quality & security
- **Qodana** — Static analysis engine for CI by JetBrains.  
  [https://www.jetbrains.com/qodana/](https://www.jetbrains.com/qodana/)
- **SonarQube** — Dashboard of bugs, vulnerabilities, code smells, and duplications.  
  [https://www.sonarqube.org/](https://www.sonarqube.org/)
- **PIT (Mutation Testing)** — Audits test suite effectiveness by injecting faults.  
  [https://pitest.org/](https://pitest.org/)
- **Legacy code** — [8 tips for working with legacy code](https://www.perforce.com/blog/qac/8-tips-working-legacy-code)
- **Git mishap recovery** — [Oh Shit, Git!?!](https://dangitgit.com/)

### Accessibility
Inclusive design is a quality attribute, not an afterthought.
- **pa11y-ci** — Command‑line accessibility testing in CI.  
  [https://github.com/pa11y/pa11y-ci](https://github.com/pa11y/pa11y-ci)
- **Koa11y** — Desktop accessibility inspector.  
  [https://open-indy.github.io/Koa11y/](https://open-indy.github.io/Koa11y/)
- **Images for Everyone** — Guide for accessible visual content.  
  [https://github.com/ksylor/images-for-everyone](https://github.com/ksylor/images-for-everyone)

---

## Languages & Paradigms

I believe a polyglot approach sharpens thinking. Different languages force different mental models.

- **Ballerina** — Cloud‑native integration language where sequence diagrams are syntax.  
  [https://ballerina.io/](https://ballerina.io/)
- **Clojure** — Lisp on the JVM; functional, immutable‑by‑default.  
  [https://clojure.org/](https://clojure.org/)
- **J** — Terse, array‑oriented programming.  
  [https://www.jsoftware.com/](https://www.jsoftware.com/)
- **APL** — Symbolic mathematical notation descendant; experimented with via the Diamond Kata.  
  [https://www.dyalog.com/](https://www.dyalog.com/)
- **Java (with JEPs)** — My core enterprise language; I follow JDK Enhancement Proposals closely.  
  [https://openjdk.org/jeps](https://openjdk.org/jeps)
- **JavaScript** — The web’s language, used with [Node.js](https://nodejs.org/) and [nvm](https://github.com/nvm-sh/nvm) to manage multiple runtime versions.
- **Python** — My go‑to for prototyping, glue code, data wrangling, and interfacing with AI/ML ecosystems.  
  [https://www.python.org/](https://www.python.org/)
- **C#** — For Windows‑specific and Azure‑centric solutions where the .NET ecosystem shines.  
  [https://dotnet.microsoft.com/en-us/languages/csharp](https://dotnet.microsoft.com/en-us/languages/csharp)
- **C / C++** — When I need to hack closer to the metal, understand performance, or work with systems programming.  
  [C](https://en.cppreference.com/w/c) | [C++](https://isocpp.org/)
- **Bash / Batch / PowerShell** — Small scripts that run on any machine without extra installation; the glue of CI/CD and everyday automation.  
  [Bash](https://www.gnu.org/software/bash/) | [PowerShell](https://learn.microsoft.com/en-us/powershell/)
- **Ruby** — Cherished for its vibrant documentation‑focused community and tools like Jekyll, Asciidoctor, and more.  
  [https://www.ruby-lang.org/](https://www.ruby-lang.org/)

---

## Self‑Hosted Infrastructure & Services

I have a strong affinity for self‑hosted, open‑source alternatives that keep data under my control. These are some of the services I run, contribute to, or use regularly.

- **Nextcloud** — Self‑hosted file sync, calendar, contacts, and collaboration platform.  
  [https://nextcloud.com/](https://nextcloud.com/)
- **osTicket** — Open‑source ticket system for managing support inquiries.  
  [https://osticket.com/](https://osticket.com/)
- **Wiki.js** — Modern, extensible wiki engine powered by Node.js.  
  [https://js.wiki/](https://js.wiki/)
- **XWiki** — Enterprise wiki platform with structured data and powerful extensions.  
  [https://www.xwiki.org/](https://www.xwiki.org/)
- **Mastodon** — Decentralised social network; my presence in the fediverse.  
  [https://joinmastodon.org/](https://joinmastodon.org/)
- **WordPress** — The ubiquitous open‑source CMS, still useful for quick sites and blogging (though this blog is Jekyll‑powered).  
  [https://wordpress.org/](https://wordpress.org/)
- **Calibre‑Web** — Web interface for browsing, reading, and downloading eBooks from a Calibre database.  
  [https://github.com/janeczku/calibre-web](https://github.com/janeczku/calibre-web)
- **AnythingLLM** — Private, self‑hosted AI assistant that can ingest your documents.  
  [https://anythingllm.com/](https://anythingllm.com/)
- **Kodi** — Media centre for organising and playing local and streamed content.  
  [https://kodi.tv/](https://kodi.tv/)
- **CUPS** — The standard printing system for Unix‑like operating systems.  
  [https://www.cups.org/](https://www.cups.org/)
- **Habitica** — Gamified habit tracker (also self‑hostable).  
  [https://habitica.com/](https://habitica.com/)
- **Reveal.js** — HTML presentation framework; I often generate slides from AsciiDoc.  
  [https://revealjs.com/](https://revealjs.com/)
- **Bitwarden** — Self‑hosted password manager with official server images.  
  [https://bitwarden.com/](https://bitwarden.com/) (self‑host via [Vaultwarden](https://github.com/dani-garcia/vaultwarden))
- **Framadate** — Open‑source poll and scheduling tool (Doodle alternative).  
  [https://framadate.org/](https://framadate.org/)
- **Odoo** — Suite of business apps (CRM, accounting, project management).  
  [https://www.odoo.com/](https://www.odoo.com/)
- **Eclipse Che** — Kubernetes‑native IDE for cloud development workspaces.  
  [https://www.eclipse.org/che/](https://www.eclipse.org/che/)

---

## Repositories

A selection of my open‑source projects and deliberate practice playgrounds.

- [Blog](https://github.com/verronpro/blog) — Source of this site.
- [office‑stamper](https://github.com/verronpro/office-stamper) — The **office‑stamper** project: stamp or fill Word documents programmatically. This is where I actively pair with AI assistants while keeping a strict cybersecurity posture.
- [Vieilles Photos](https://github.com/verronpro/vieilles.photos) — Old‑photo processing/storytelling.
- [Hyrule ID Generator](https://github.com/josephverron/hyrule-id-generator) — Playful ID generation for TDD practice.
- [HTTP Workshop](https://github.com/josephverron/http-workshop) — Hands‑on HTTP protocol workshop materials.
- [Scrapy](https://github.com/josephverron/scrapy) — Web scraping experiments.
- [Workshop Secure Messenger](https://github.com/josephverron/workshop-secure-messenger) — Encryption and secure coding workshop.
- [Gource](https://github.com/josephverron/Gource) — Version control history visualisation.
- [GitHub Visualizer](https://github.com/josephverron/GitHubVisualizer) — Repository activity trends.
- [Advent of Code](https://github.com/josephverron/adventofcode) — Multi‑language puzzle solutions.
- [Orgnosis](https://github.com/josephverron/orgnosis) — Personal knowledge management exploration.
- [Trip Service Kata](https://github.com/josephverron/trip-service-kata) — Legacy‑code refactoring kata.
- [Dojo](https://github.com/josephverron/dojo) — Coding dojo setup for group practice.
- [gource-action](https://github.com/josephverron/gource-action) — GitHub Action to auto‑generate Gource videos.
- [Sonar Extractor](https://github.com/josephverron/sonar-extractor) — Pull metrics from SonarQube.
- [Talon](https://github.com/josephverron/talon) — Voice‑coding / automation experiment.
- [Presentations](https://github.com/josephverron/presentations) — Slide decks from talks.
- [Manga Library](https://github.com/josephverron/manga_library) — Full‑stack cataloguing project.
- [Graphical Sorter](https://github.com/josephverron/graphical-sorter) — Sorting algorithm visualisations.
- [Java Evolutions](https://github.com/josephverron/java-evolutions) — Feature showcases across Java versions.
- [Project Euler](https://github.com/josephverron/euler) — Mathematical programming challenges.
- [CodinGame](https://github.com/josephverron/codingame) — Puzzle solutions.
- [Disk Store](https://github.com/josephverron/disk-store) — Simple key‑value store exercise.
- [Notes](https://github.com/josephverron/notes) — Public digital garden.
- [Codeology](https://github.com/josephverron/codeology) — Code structure and aesthetics study.
- [Code Swarm](https://github.com/josephverron/code_swarm) — Developer activity visualisation.

---

## Inspirations & Tangents

Things that inform my work, make me smile, or remind me that technology is a human endeavour.

- **Webcomics** — [Geek and Poke](https://geek-and-poke.com/), [Glasbergen](https://www.glasbergen.com/), CommitStrip, XKCD.
- **NDC Oslo** — Rich archive of talks on craftsmanship and architecture.  
  [YouTube channel](https://www.youtube.com/@NDC/videos) | [Be a Compass (Nelly Sattari)](https://nelly-sattari.atlassian.net/wiki/spaces/4Cs/pages/21299251/Be+a+Compass)
- **Minitel experiments** — Vintage French pre‑internet tinkering; a reminder that constraint breeds creativity.
- **QR generation** — [QR.io](https://qr.io/) when a quick scannable link is needed.
