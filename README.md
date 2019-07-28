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

## Coupling levels

|          | local method   | local instance   | external instance   | configurable instance   | notification |
| -------- | -------------- | ---------------- | ------------------- | ----------------------- | ------------ |
| *How?*   | +              | -                | -                   | -                       | -            |
| *Where?* | +              | +                | -                   | -                       | -            |
| *Who?*   | +              | +                | +                   | -                       | -            |
| *What?*  | +              | +                | +                   | +                       | -            |

*source: [Understanding coupling - Łukasz Szydło - wroc_love.rb 2018](https://www.youtube.com/watch?v=Jy6eS9QHJOM)*

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

## Useful articles

* [Modern Software Architecture](https://medium.com/modern-software-architecture/modern-software-architecture-1-domain-driven-design-f06fad8695f9)
* [The top 5 software architecture patterns: How to make the right choice](https://techbeacon.com/app-dev-testing/top-5-software-architecture-patterns-how-make-right-choice)
* [Mikroserwisy – czy to dla mnie?](https://kubrynski.blog/mikroserwisy-czy-to-dla-mnie/)
* [Software Architecture - The Difference Between Architecture and Design](https://codeburst.io/software-architecture-the-difference-between-architecture-and-design-7936abdd5830)
* [10 Common Software Architectural Patterns in a nutshell](https://towardsdatascience.com/10-common-software-architectural-patterns-in-a-nutshell-a0b47a1e9013)
* [Bottega IT Minds - Darmowe materiały dla programistów](https://bottega.com.pl/materialy.xhtm?cat=DDD)
* [GeeksforGeeks | Software Engineering | Coupling and Cohesion](https://www.geeksforgeeks.org/software-engineering-coupling-and-cohesion/)
* [Software Design Basics](https://www.tutorialspoint.com/software_engineering/software_design_basics.htm)

## Useful books

* [Domain-Driven Design](http://domainlanguage.com/ddd/blue-book/)
* [Event storming](https://www.eventstorming.com/book/)
* [Software architecture for developers](https://softwarearchitecturefordevelopers.com/)
* [Just enough software architecture](https://www.georgefairbanks.com/e-book/)
* [Software systems architecture](https://www.viewpoints-and-perspectives.info/home/book/)

## Useful repositories

* [A comprehensive Domain-Driven Design example with problem space strategic analysis and various tactical patterns](https://github.com/ddd-by-examples/library)
