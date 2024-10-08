# Signals
[Definitions](#dictionary-definitions) |
[Why signals](#why-signals-general-problems-we-are-solving) |
[Specification](#specification) |
[Interop examples](#other-interop-examples)

## What are Signals?

### Dictionary definitions

> Noun: 'anything agreed upon or understood as the occasion for concerted action'

> Adjective: 'unusual; notable; outstanding'

> Verb: 'to communicate or make known by a signal'

> 'The fundamental quantity of representing some information'.

### Signal definition

Signals are simple messages that can be exchanged between organisations to indicate that an action has been taken or that something has been decided or agreeed upon.

With signals insight is moved (the result of deploying expertise over raw data) not the raw data itself. This has many benefits.

## Why Signals? (General problems we are solving)

* Signals are light-weight, with simple payloads and a straightforward version control system. This means it will be less expensive to experiment with new types of information exchange and that signals can be revised, or new signals added, without disrupting existing implementations 
* Signals can be delivered as soon as a corresponding event occurs in the originating business process.  We believe this will allow new workflows to be created based on actual business timings rather than an arbitrary schedule set by any specific actors in an information sharing network
* Signals can move in any direction, creating the potential for feedback loops that are difficult to create with the traditional declaration-based approaches

## What are the features of a well designed signal?
- Signals permit organisations to minimise information share volume while maximising the sharing of expertise
- Signals are typically self contained - they usually do not require additional out of band information to be made available
- Signals reduce the need for complex ontologies and reduce semantics leaking over boundaries due to their more precise/targetted deisgn and footprint
- Signals may be anonymous/opaque - identity of the producer/provider and detail of the due diligence behind any insight may be omitted
- Signals permit consuming parties to make their own minds up on whether and how to use them for example whether aggregation or corroboration are necessary
- Signals may move bi-directionally between any number of actors participating in a network
- A signal is typically not a large footprint of raw information

## What data should be contained in a signal?
- A signal is typically:
  - An attribute of an event or information element
  - A verified attribute of an event or information element
  - An opinion based on observation of information or events
  - A claim based on analysis of information or events
  - Insight generated by the deployment of expertise over data or events
  - An attestation from an organisation that a signal produced or provided by another organisation is accurate or true

## Specification

**V0.2.0**

### Example 1 - The simplest possible signal

N.B. we are using Extensible Data Notation to outline signal structure here to simplify signal presentation - implementations of the protocol will present signals in a number of formats including JSON.

```clojure
{
  :provider "sample-isn.my-example.xyz" [1]
  :published "2023-03-16T22:51:51.379072Z" [2]
  :signalId "704e851a-9ab4-40d6-b995-765f64104072" [3]
  :correlationId "734713bc04" [4]
  :category #{"isn-membership-participant-update" "isn@sample-isn.my-example.xyz"} [5]
  :object "organisation-a.my-example.xyz" [6]
  :predicate "joins ISN sample-isn.my-example.xyz" [7]
}
```

- 1: **System provided usually** The signal provider (all signals are contributed into an [Information Sharing Network (ISN)](https://github.com/information-sharing-networks/.github/blob/main/glossary.md#information-sharing-network-isn) information exchange infrastructure by a site on behalf of an organisation)
- 2: **System provided** The instant in time a signal is published into an ISN
- 3: **System provided** A unique identifier which makes this signal distinct
- 4: **System provided** A unique identifier which lets all actors using and adding to a signal understand they are operating on the same signal (traces through workflows)
- 5: **Required - user provided** Category used to indicate both which ISN the signal pertains to (ISN category) and what kind of signal is being transmitted (domain signal or signals) - both are required
- 6: **Required - user provided** A simple name to represent the signal where it is placed adjacent to others (human readable and meaningful)
- 7: **Required - user provided** A more meaningful and full explanation of the signal's purpose (when combined with the object creates a single sentence much like those that are part of an event log describing what is happening over time e.g. Git messages)

This is a simple and encapsulated signal - but not very useful.

### Example 2 - A more detailed (useful) example

```clojure
{
  :provider "sample-isn.my-example.xyz"
  :start "2023-03-17T22:51:51.379676Z" [1]
  :end "2023-03-18T18:00:00Z" [2]
  :published "2023-03-16T22:51:51.379072Z"
  :signalId "704e851a-9ab4-40d6-b995-765f64104072"
  :correlationId "734713bc04"
  :category #{"isn-membership-participant-update" "isn@sample-isn.my-example.xyz"}
  :object "organisation-a.my-example.xyz"
  :predicate "joins ISN sample-isn.my-example.xyz"
  :providerMapping {
    :id "804e851b-9ab4-40d6-b995-765f64104072"
    :uri "https://uri-to-system-which-provided.io/xyz/"
  } [3]
}
```
- 1: **System provided** (TBC) we are thinking on this one - could be e.g. an ETA or could be the moment in time the signal is valid from
- 2: **System provided** the instant in time a signal expires and will no longer be surfaced in operational contexts
- 3: **Optional - upstream system or user provided** a mapping construct that lets us associate a signal with information in an upstream system (which has directly provided it) through a number of identity related fields

This is a slightly more involved example. It is based on an actual signal indicating membership change within an ISN but is contrived as it demonstrates how we might link to an underlying system which provides the signal (which is irrelevant for this type of signal).

### Example 3 - A signal and its metadata which is associated to a payload of information in a given domain

```clojure
{
  :provider "sample-isn.my-example.xyz"
  :start "2024-01-10T16:51:51.379676Z"
  :end "2024-01-20T18:00:00Z"
  :published "2024-01-08T12:51:51.379072Z"
  :signalId "704e851a-9ab4-40d6-b995-765f64104072"
  :correlationId "734713bc04"
  :category #{"isn-membership-participant-update" "isn@sample-isn.my-example.xyz"}
  :object "organisation-a.my-example.xyz"
  :predicate "joins ISN sample-isn.my-example.xyz"
  :payload {
    :dueDiligenceChecked true
    :participantMembershipAgreementLevel :majority
  } [1]
}
```
- 1: **Optional - upstream system or user provided** a map of key value pairs capturing any required domain related information. E.G. associating the metadata in a signal to moving goods in the supply chain. Note it is a combination of the isn category (isn@sample-isn.my-example.xyz) and the domain category which determines what the payload will be. It is important that the payload honours the contract for this combination of categories by being backwards compatible (e.g. fields may be added to it but not removed or renamed, this may result in the need to use new key/value pairs withi the payload while continuing to pass old unused key/value pairs).

*How might these signals look when sufaced e.g. on a dashboard?*

- organisation-a.my-example.xyz joins ISN XYZ
- organisation-b.my-example.xyz joins ISN XYZ
- ...

Again this is a slightly more involved example. In the same way as example 2 above it is based on a real signal. This example it contrived as it includes a payload which represents domain specific information. Here we include sample payload information indicating whether due diligence was undertaken for the process of onboarding the new participant into the ISN and the level of agreement reached by existing ISN participants.


## Further links
A  proof of concept implementation of these ideas can be found [here](https://github.com/information-sharing-networks/isn-ref-impl)
