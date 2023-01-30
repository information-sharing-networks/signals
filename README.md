# Signals

## Definition

TBD


## Why Signals?
Signals are an attempt to resolve some of the limitations with the traditional declaration-based mechanism for exchanging information between trader and government:

*Declarations* 
* Declarations, licence applications notifications etc tend to be large, complex, documents that require complex software to generate and consume.  Changes to the data and associated systems are very disruptive and can take years to complete.
* Declarations are primarily organised for one-way communication (trade to government)
* Deadlines for delivering declarations are based on government needs rather than the business processes that generate the data, making it inconvenient to implement submission solutions.

*Signals*
* Signal messages are intended to be light-weight, simple documents with a straightforward version control system. This means it will be less expensive to experiment with new types of information exchange and that signals can be revised, or new signals added, without disrupting existing implementations 
* Signals can be delivered as soon as a corresponding event occurs in the originating business process.  We believe this will allow new workflows to be created based on actual business timings rather than the deadlines set by the government.
* Signals can go in any direction (including from government > trade and trade > trade), creating the potential for feedback loops that are difficult to create with the current declaration processes.

Signals are proposed as a complement to, rather than replacement for, the existing declaration systems.

## Implementations

- [Border signals protocol](https://github.com/information-sharing-networks/border-signals)
