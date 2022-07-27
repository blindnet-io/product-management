# Privacy Request Multicast Protocol (PRMP)

| Status        | working draft                                                                              |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [#727](https://github.com/blindnet-io/product-management/pull/727)                    |
| **Author(s)** | [milstan](https://github.com/milstan) (milstan@blindnet.io)              |
| **Updated**   | 2022-07-12                                                                             |



## Introduction

Systems exchanging data about a Data Subject might find themselves in a situation to also exchange Privacy Requests.
The purpose of Privacy Request Multicast Protocol (hereby the **Protocol**) is to define messaging and sequences of such exchanges.

The need to exchange Privacy Requests (or other [PRIV](../priv/RFC-PRIV.md) objects) might arise from contractual liabilities of Systems or from legal obligations such as in the case of Article 19 of [GDPR][GDPR] in European Union.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-architecture/)

## Requirements

- Systems exchange PRIV objects related to Data Subjects they both know of. The way they do it MUST be:
    - Asynchronous: A System may be unavailable and get a message when it becomes available again
    - Non-blocking: Systems may take action with regards to PRIV objects they know of without waiting for any input from other Systems
    - [Eventually Consistent](https://en.wikipedia.org/wiki/Eventual_consistency) with regards to PRIV objects [a System is concerned by](#priv-objects-that-concern-a-system)

- Systems SHOULD NOT have access to the content of PRIV objects not concerning them (e.g. Privacy Requests of users they do not know of, or Privacy Requests Responses from other Systems that may be confidential)

- Systems CAN implement only parts of the Protocol. E.g. a browser may only send Privacy Requests, Consents and retrieve nothing (or retrieve only Privacy Request Responses). We call such systems **Agent Systems**. We call Systems that perform actual data processing and that implement the full Protocol - **Processing Systems**.

- Systems are independent in their responses, i.e. a System MUST BE ABLE to respond to a Privacy Request addressed to it regardless of (the existence and the content of) the responses of other Systems.

- The Systems CAN apply the Protocol in the context of different [Scenarios][Scenarios].

- The Protocol can be used regardless of the Systems exchanging data in a one-off data dump, or through a continuous connection.

- The network of Systems exchanging data related to a Data Subject CAN be cyclical. It MUST not be assumed to be a complete graph. It CAN also be highly volatile i.e. Systems can participate on an ad-hoc basis, only once, disappear and reappear.

## Design Choices

- The Protocol is agnostic from any particular way to address Systems and transfer messages to and from them. Systems are responsible of knowing how to identify and address another System with which they exchange data or any object defined in PRIV.

- Systems process Privacy Requests and other PRIV objects (e.g. legal-base related events and consents) in order of their dates, and regardless of the order in which they have gain knowledge of them using the Protocol.

- The Protocol is agnostic of the level of inter-system trust. A System MAY be implemented to trust other Systems to authenticate the Data Subject, covey responses, tell the truth or not. The security implications of such choices are out of scope of the Protocol.

- The content of a message exchanged between two Systems is a PRIV object (e.g. [Privacy Request](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#privacy-request), [Privacy Request Response](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#privacy-request), [Consent](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#consent))

## Proposal

### Multicast APIs

To participate in exchange of PRIV objects, Systems expose an API. We call the System calling the API the **Calling System** and the System exposing the API the **Exposing System**. The API MAY have the following functions:

#### push

Updates the information of the Exposing System with novel information from the Calling System.

#### pull

Updates the information of the Calling System with novel information from the Exposing System.

#### merge

Equivalent to push and pull. Both Systems get updated with novel information from the other system.

#### compare

Tells the Calling System if the Exposing System has novel information with regards to what the Calling System already knows.

## Design Implications for Systems Implementing PRMP

### Underlying Data Structure

Systems have the interest to store PRIV objects in a data structure equivalent to a hash map or to a message queue, capable of easy comparison and efficient compare function.

### Callback Mechanism

Systems MUST implement, internally, a callback mechanism, with a message queue to account for asynchronous nature of the Protocol.

### Public ledger

It is possible to implement the protocol through a distributed data structure such as a public ledger. However, in order to comply with the [requirements](#requirements) and in particular with the requirement for the Systems only to be able to access the PRIV objects that they are concerned about, such implementation MUST involve encryption of messages such that only the concerned Systems can access their content.

### PRIV objects that concern a System

A System is (as soon as they become available or, in the case of Consents `revoked` value, modified) concerned by:
- Privacy Requests of which it is the `target`. Knowing if the system is the target of a Privacy Request depends on the `target` value of the Privacy Request and of the System's relationship with the System having received the request. See [more](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#targets),
- Privacy Request Responses made by other Systems, only in the case of:
    - a [Coordinated Response scenario](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/scenarios.md#coordinated-response) for Privacy Request Responses made to the same Privacy Request that the System is also a responding to within the Coordinated Response scenario
    - An Agent System charged with displaying the response to the Data Subject
- Consents, having for `data-subject` a Data Subject the System knows (has data on)
- Events related to a Data Subject the System knows (has data on)


## Questions and Discussion Topics

## Signing of PRIV objects

We still need to discuss and decide whether we impose the PRIV objects to be signed by Systems and/or Users.

## Blockchain

In addition to environmental concerns, there seams to be a fundamental incompatibility issue with blockchain, as Users MUST be able to formulate Privacy Requests in front of systems that are is a situation of incomplete knowledge of previous Privacy Requests (or PRIV objects) - a principle opposite of blockchain, where new information is added to the chain (knowing the chain).

## References

### Normative References

- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,
- **[RFC-PRIV]** Stankovic, M., ["Privacy Request Interchange Vocabulary"](../priv/RFC-PRIV.md)
- **[RFC-Lexicon-2]** Stankovic, M., ["Lexicon"](../lexicon/RFC-Lexicon-2.md)


### Informative References

- [Examples of use](../priv/examples.md)
- [Expected Behavior of Implementing Systems](../priv/expected-behavior.md)
- [Scenarios](../scenarios.md)
- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
