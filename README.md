# Signals

# What are Signals?

TBD


# Why Signals?
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


# other interop examples
other interop implemenations to use or borrow/learn from:

borders
* [DCSA event subscription](https://app.swaggerhub.com/apis/dcsaorg/DCSA_EBL/2.0.0-Beta-2#/Shipping%20Instructions/get_v2_shipping_instructions__shippingInstructionReference_) approach (webhook)  
* NOTN (discussion pending)
* Data Pipelines/waypoints:  [UNCEFACT Data Pipeline White Paper](https://unece.org/fileadmin/DAM/cefact/GuidanceMaterials/WhitePaperDataPipeline_Eng.pdf).  EU sponsored research: [Cassandra](https://cordis.europa.eu/project/id/261795) & [CORE](http://www.coreproject.eu/resources.aspx?filter=6073)

Finance
* FIX - electronic trading  - very simple, pre web, well adopted but possible challenges around multiple dialects
* PSD2 (c.f open banking exchange)  provision of payment services , interesting because (EU) legislation-lead

Industry led examples
* [OpenTravel](https://opentravel.org/) - does not appear to be a web based presence for the spec, but available on request.
* [OpenReferral](https://openreferraluk.org/about-standard) - local council data exchange 
* [GTFS](https://github.com/google/transit/tree/master/gtfs-realtime/spec/en) - public transportation (an example feed - from Connecticut Department of Transportation - is hosted on the [Ably hub](https://ably.com/hub/cttransit/gtfsr)
