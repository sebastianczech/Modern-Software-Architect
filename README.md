# Modern Software Architect

Notes and links useful for Modern Software Architect

## Architecture drivers

* business (goal, requirements)
* project (budget, deadline, knowledge)
* qualities (availability, security, reliability)

## 4 architecture types / styles

* big ball of mud (not distributed, not modular monolith)
* modular monolith (not distributed)
* microservices (distributed, modular)
* distrubted monoligth (not modular)

## Architecture patterns

* P&A (port & adapters) (hexagonal)
* CQRS (command query responsibility segregation)

# Data models

* anemic
* objective

## Coupling levels

|          | local method   | local instance   | external instance   | configurable instance   | notification |
| -------- | -------------- | ---------------- | ------------------- | ----------------------- | ------------ |
| *How?*   | +              | -                | -                   | -                       | -            |
| *Where?* | +              | +                | -                   | -                       | -            |
| *Who?*   | +              | +                | +                   | -                       | -            |
| *What?*  | +              | +                | +                   | +                       | -            |

*source: [Understanding coupling - Łukasz Szydło - wroc_love.rb 2018](https://www.youtube.com/watch?v=Jy6eS9QHJOM)*

## Communication in distributed system

* temporal coupling
* design for failure
* asynchronous over synchronous
* commans (queues) and events (topics)
* asynchronous principles: 
   * persistent
   * at least once delivery
   * exponential retries
* synchronous only when required   
* timeout ? retry !
* circuit breaker (fallback)
* load balancer is single point of failure
* if service discovery is not available, use cached information about service
* loose coupling over canonical model
* contracts between services
* monitoring is new testing
* percentiles (P99.95), not average
* automation as a code, pipeline as a code -> CI/CD
* infrastructure as a code, configuration as a code
* [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem):
   * **Consistency**: Every read receives the most recent write or an error
   * **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write
   * **Partition tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

*source: [Boiling Frogs 2019 - Jakub Kubryński - Kuloorporna komunikacja w systemtach rozproszonych](https://www.youtube.com/watch?v=zq71CKfiB0g)*

## General system architecture

```
---------------------- API GATEWAY ----------------------
------------------------ filters ------------------------
------------------------ routers ------------------------
---------------------------------------------------------
--- saga -----------------------------authorization------
--- process managager ----------------logging------------
--- workflow -------------------------notifications------
---------------------------------------------------------
---------------------- complex write --------------------
--- kafka ------------ CRUD ----------------- * MQ ------
---------------------- comple read ----------------------
---------------------------------------------------------
----------- hadoop -------- ML -------- spark -----------
---------------------------------------------------------
```

* communication between services is done by messages (*city metaphor*)
* database is private and under central elements for CRUD, read and write and duplication of data it prefered solution
* pyramid of tests:
   * for complex write: unit > integration-> e2e (unit the most important)
   * for complex read: e2e > integration > unit (e2e the most important)
   * for complex read: unit = integration = unit (all are important)
* construction elements:
   * for complex write: commands, events, aggregates, policies
   * for complex read: read models
* levels of designing from highest to lowest:
   * system
   * services
   * construction elements
   * objects
   * instructions
* saga - message handlers, which has state and it's long running process

*source: [Boiling Frogs 2018 - Łukasz Szydło - Modularity – the final frontier](https://www.youtube.com/watch?v=2oJrjyp7GHE)*

## Architecture decision record

* context:
   * stable / unstable
   * core / supporting / generic
   * time
   * known change vectors
   * complexity (rules, config, math, versioning, performance)
* decision
* cosequences

*source: [4Developers 2019: How does architect know? Łukasz Szydło](https://www.youtube.com/watch?v=Pm50mqO73YI)

## Aspects of product

* implementation: readability, reuse, expand
* delivery: tests, configuration
* use: availability, responsivness, security
* maintenance: stability, reliabilty

## Architect tools:

* ADR (Markdown)
* AsciiDoc
* C4
* plantUML
* [Diagram as a Code](https://diagrams.mingrammer.com/)
* [WebSequenceDiagrams](https://www.websequencediagrams.com/)
* [Lucidchart](https://app.lucidchart.com/)
* MindMap
* MOSCOW
* SWOT
* EventStorming
* Eisenhower box
* Pareto

## SOLID, KISS, DRY

* SOLID:
   * S – Single Responsibility
   * O – Open – Closed
   * L – Liskov Substitution
   * I – Interface Segregation
   * D – Dependency Inversion
* DRY – Don’t Repeat Yourself
* KISS – Keep It Simple Stupid

## 4 layers of domain model - reponsibility layers (chapter 16 from DDD - Eric Evans)

* CP - Capabilities
* OP - Operations
* P - Policies
* DM - Decision making

## EventStorming

* [Michał Bartyzel](https://www.michalbartyzel.pl/) - Biznes jest prosty
  * [Lean Canvas - introduction](https://medium.com/@steve_mullen/an-introduction-to-lean-canvas-5c17c469d3e0)
    * When to use event storming ? 
      * Unique value proposition
      * Unfair adventage
      * Anomalies
    * Domain model archetypes (the rest between IT and business)
  * [How to create your lean canvs](https://leanstack.com/LeanCanvas.pdf)
  * [Communicate your idea clearly and concisely to others so they can get behind it](https://leanstack.com/lean-canvas)
* Jakub Pilimon - O odkrywaniu granic - heurystyki ważnych decyzji
  * heuristics - methodology, logic, solution discovery
  * event storming - tool to achieve some goal
  * the cost of implementing a system is minimal when parts of the problem are:
    * manageably small
    * solveable separately
  * low coupling & high cohesion
    * logical cohesion is wrong
    * temporal cohesion
  * heuristics examples:
    1. removability - disposable modules - Royal Australian Air Force (if you can't find error in module in less than 15 minutes, remove this module)
    2. observable behaviours - pivotal events - events which are changing our current logic 
    3. be careful with systems storing status
    4. look out for logical cohesion
    5. look out for data placeholders
    6. look out for temporal cohesion
    7. data and rules stay together (what changes together, stays together)
    8. data used together (autonomy, minimalized coupling)
    9. anit-requirements 
    10. schizophrenia (many if)
    11. archetypes
* Mariusz Gil - EventStorming to tylko narzędzie, używaj go mądrze
  * f(hajs, time)
  * IT Depends Certified Developer

## Udi Dahan materials 

* [Webinar: Connect frontend to backend using SignalR and messaging](https://go.particular.net/e/27442/nd-using-signalr-and-messaging/8szlqs/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Blog post: Careful with Content-based routing](https://go.particular.net/e/27442/ul-with-content-based-routing-/8szlqv/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Documentation: Architectural Principles](https://go.particular.net/e/27442/icebus-architecture-principles/8szlqx/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Atomic increment using Riak counters](https://go.particular.net/e/27442/ing-data-types-counters-1-html/8szlqz/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Webinar: Finding your service boundaries: a practical guide](https://go.particular.net/e/27442/e-boundaries-a-practical-guide/8szlr2/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Webinar: All our aggregates are wrong](https://go.particular.net/e/27442/s-all-our-aggregates-are-wrong/8szlr4/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Blog post: Goodbye microservices, hello right sized services](https://go.particular.net/e/27442/ces-hello-right-sized-services/8szlr6/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Blog post: Break that big ball of mud](https://go.particular.net/e/27442/log-break-that-big-ball-of-mud/8szlr8/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Blog post: Microservices: the future or empty hype?](https://go.particular.net/e/27442/oservices-future-or-empty-hype/8szlrb/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)
* [Webinar: Making workflow implementation easy with CQRS](https://go.particular.net/e/27442/-implementation-easy-with-cqrs/8szlrd/1463215887?h=x6e3qKiv_DcfViVyyTqOa7TLrm379VScKwUyulYETjs)

## Useful articles

* [Modern Software Architecture](https://medium.com/modern-software-architecture/modern-software-architecture-1-domain-driven-design-f06fad8695f9)
* [The top 5 software architecture patterns: How to make the right choice](https://techbeacon.com/app-dev-testing/top-5-software-architecture-patterns-how-make-right-choice)
* [Mikroserwisy – czy to dla mnie?](https://kubrynski.blog/mikroserwisy-czy-to-dla-mnie/)
* [Software Architecture - The Difference Between Architecture and Design](https://codeburst.io/software-architecture-the-difference-between-architecture-and-design-7936abdd5830)
* [10 Common Software Architectural Patterns in a nutshell](https://towardsdatascience.com/10-common-software-architectural-patterns-in-a-nutshell-a0b47a1e9013)
* [Bottega IT Minds - Darmowe materiały dla programistów](https://bottega.com.pl/materialy.xhtm?cat=DDD)
* [GeeksforGeeks | Software Engineering | Coupling and Cohesion](https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/)
* [Software Design Basics](https://www.tutorialspoint.com/software_engineering/software_design_basics.htm)
* [Example of Hexagonal architecture with high cohesion modularization, CQRS and fast BDD tests in Java](https://github.com/jakubnabrdalik/hentai)
* [Martin Fowler - local DTO](https://martinfowler.com/bliki/LocalDTO.html)
* [Martin Fowler - architecture](https://martinfowler.com/architecture/)
* [Martin Fowler - monolith first](https://martinfowler.com/bliki/MonolithFirst.html)
* [Martin Fowler - Catalog of Patterns of Enterprise Application Architecture](https://martinfowler.com/eaaCatalog/index.html)
* [Enterprise Integration Patterns - Messaging Patterns](https://www.enterpriseintegrationpatterns.com/patterns/messaging/IdempotentReceiver.html)
* [Enterprise Integration Patterns - Process Manager](https://www.enterpriseintegrationpatterns.com/patterns/messaging/ProcessManager.html)
* [Narzędzia pracy konsultanta](https://radekmaziarka.pl/2020/02/04/narzedzia-pracy-konsultanta-cz1/)
* [Greg Young - Versioning in an Event Sourced System](https://leanpub.com/esversioning)
* [A pattern language for microservices](https://microservices.io/patterns/index.html)
* [Pattern: Saga](https://microservices.io/patterns/data/saga.html)
* [XUnit Test Patterns](http://xunitpatterns.com/)
* [Why Every Element of SOLID is Wrong](https://speakerdeck.com/tastapod/why-every-element-of-solid-is-wrong?slide=6)
* [Too much coding - Marcin Grzejszczak](https://toomuchcoding.com/publications/)
* [Miro - the best tool for Event Storming online](https://miro.com/)
* [Creating C4 models using plantUML](https://github.com/RicardoNiepel/C4-PlantUML)
* [draw.io plugin for C4 models](https://github.com/tobiashochguertel/c4-draw.io)
* [Loosely-Coupled Architecture – how to get rid of the domino effect](https://radekmaziarka.pl/2019/01/15/loosely-coupled-architecture/)
* [Mariusz Gil - awesome Event Storming](https://github.com/mariuszgil/awesome-eventstorming)
* [Modular-services in a NodeJs Monolith](https://slides.com/navalsaini/modular-nodejs#)
* [Wizualizacja architektury zgodnie z modelem C4. Podejście praktyczne](http://tomaszsokol.pl/wizualizacja-architektury-zgodnie-z-modelem-c4-podejscie-praktyczne/)
* [Uncovering Hidden Business Rules with DDD Aggregates](https://medium.com/@ntcoding/uncovering-hidden-business-rules-with-ddd-aggregates-67fb02abc4b)
* [Kamil Grzybek - Modular Monolith: A Primer](https://www.kamilgrzybek.com/design/modular-monolith-primer/)
* [DNA-Zadania-Wstęp](http://ismartdev.pl/dna-zadania/dna-zadania-wstep/)
* [Allegro REST API Design Guideline](https://github.com/allegro/restapi-guideline)
* [Łukasz Szydło - DDD - o jeden krok za daleko](https://speakerdeck.com/lszydlo/ddd-o-jeden-krok-za-dalego)
* [DevStyle.pl - O kohezji słów kilka](https://devstyle.pl/2020/03/09/o-kohezji-slow-kilka/)
* [Open API specification](https://github.com/OAI/OpenAPI-Specification)
* [Connascence is a software quality metric & a taxonomy for different types of coupling](https://connascence.io/)
* [Technology Radar - Thoughtworks](https://www.thoughtworks.com/radar)
* [Manifesto for Software Craftsmanship](http://manifesto.softwarecraftsmanship.org/#/en)
* [Software Craftsmanship](https://bulldogjob.pl/news/274-software-craftsmanship)
* [Azure Architecture Center Cloud Design Patterns](https://docs.microsoft.com/bs-latn-ba/azure/architecture/patterns/)
* [A Saga on Sagas](https://docs.microsoft.com/en-us/previous-versions/msp-n-p/jj591569(v=pandp.10))
* [Introduction to SOLID Design Principles for Java Developers](https://dzone.com/articles/a-gentle-and-easy-to-grasp-introduction-to-solid-p?edition=538293&utm_source=Weekly%20Digest&utm_medium=email&utm_campaign=Weekly%20Digest%202019-11-13)
* [Cloudflare - What Is Web Application Security?](https://www.cloudflare.com/learning/security/what-is-web-application-security/)
* [11 Ways to Improve Your Web Application Security](https://www.webarxsecurity.com/improve-web-application-security/)
* [Martin Fowler - The Basics of Web Application Security](https://martinfowler.com/articles/web-security-basics.html)
* [Top open source ESB (Enterprise Service Bus)](https://dzone.com/articles/top-open-source-esbs)
* [Securing REST APIs with Client Certificates](https://blog.pavelsklenar.com/securing-rest-api-with-client-certificate/)
* [Security tool - OWASP Threat Dragon](https://owasp.org/www-project-threat-dragon/)
* [Best practices for REST API design](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)
* [API BFF, API agregation](https://patoarchitekci.io/19/)
* [API Platform - REST and GraphQL framework to build modern API-driven projects](https://api-platform.com/)
* [Refaktoryzacja](https://refactoring.pl/pl/posty/)
* [Message Broker or Bus – what’s the difference?](https://neiljbrown.com/2017/05/13/message-broker-or-bus-whats-the-difference/)
* [Zasady projektowania obiektowego](https://devcave.pl/notatnik-juniora/zasady-projektowania-kodu)
* [SOLID, DRY, KISS](https://maciejjedrzejewski.pl/2016/12/17/solid-dry-kiss/)
* [SOLID](https://www.geeksforgeeks.org/dependecy-inversion-principle-solid/)
* [Design patterns for humans](https://github.com/kamranahmedse/design-patterns-for-humans)

## Useful books

* [Domain-Driven Design](http://domainlanguage.com/ddd/blue-book/)
* [Event storming](https://www.eventstorming.com/book/)
* [Software architecture for developers](https://softwarearchitecturefordevelopers.com/)
* [Just enough software architecture](https://www.georgefairbanks.com/e-book/)
* [Software systems architecture](https://www.viewpoints-and-perspectives.info/home/book/)
* [Book about Pythonic Application Architecture Patterns for Managing Complexity](https://github.com/cosmicpython/book)
* [Berkeley Packet Filter (BPF) Performance Tools](https://github.com/brendangregg/bpf-perf-tools-book)

## Useful courses

* [DevUpgrade](https://www.youtube.com/channel/UCvNne80z8XObPYIhDwnKDrg)

## Useful repositories

* [A comprehensive Domain-Driven Design example with problem space strategic analysis and various tactical patterns](https://github.com/ddd-by-examples/library)
* [Modular Monolith with DDD](https://github.com/kgrzybek/modular-monolith-with-ddd)
* [Aggregates by example](https://github.com/mariuszgil/aggregates-by-example)
* [Path to a Software Architect](https://github.com/justinamiller/SoftwareArchitect)
