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
* MindMap
* MOSCOW
* SWOT
* EventStorming
* Eisenhower box
* Pareto

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
* [Narzędzia pracy konsultanta](https://radekmaziarka.pl/2020/02/04/narzedzia-pracy-konsultanta-cz1/)
* [Greg Young - Versioning in an Event Sourced System](https://leanpub.com/esversioning)
* [A pattern language for microservices](https://microservices.io/patterns/index.html)
* [XUnit Test Patterns](http://xunitpatterns.com/)

## Useful books

* [Domain-Driven Design](http://domainlanguage.com/ddd/blue-book/)
* [Event storming](https://www.eventstorming.com/book/)
* [Software architecture for developers](https://softwarearchitecturefordevelopers.com/)
* [Just enough software architecture](https://www.georgefairbanks.com/e-book/)
* [Software systems architecture](https://www.viewpoints-and-perspectives.info/home/book/)

## Useful repositories

* [A comprehensive Domain-Driven Design example with problem space strategic analysis and various tactical patterns](https://github.com/ddd-by-examples/library)
* [Path to a Software Architect](https://github.com/justinamiller/SoftwareArchitect)
