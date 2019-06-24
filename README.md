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

## Useful articles

* [Modern Software Architecture](https://medium.com/modern-software-architecture/modern-software-architecture-1-domain-driven-design-f06fad8695f9)
* [The top 5 software architecture patterns: How to make the right choice](https://techbeacon.com/app-dev-testing/top-5-software-architecture-patterns-how-make-right-choice)
* [Mikroserwisy – czy to dla mnie?](https://kubrynski.blog/mikroserwisy-czy-to-dla-mnie/)
* [Software Architecture - The Difference Between Architecture and Design](https://codeburst.io/software-architecture-the-difference-between-architecture-and-design-7936abdd5830)
* [10 Common Software Architectural Patterns in a nutshell](https://towardsdatascience.com/10-common-software-architectural-patterns-in-a-nutshell-a0b47a1e9013)
* [Bottega IT Minds - Darmowe materiały dla programistów](https://bottega.com.pl/materialy.xhtm?cat=DDD)

## Useful repositories

* [A comprehensive Domain-Driven Design example with problem space strategic analysis and various tactical patterns](https://github.com/ddd-by-examples/library)
