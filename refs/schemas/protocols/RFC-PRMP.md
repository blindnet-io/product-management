# Privacy Request Multicast Protocol (PRMP)

| Status        | proposed                                                                              |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [#727](https://github.com/blindnet-io/product-management/pull/727)                    |
| **Author(s)** | [milstan](https://github.com/milstan) (milstan@blindnet.io)              |
| **Updated**   | 2022-07-10                                                                             |



## Introduction

Systems exchanging data about a Data Subject might find themselves in a situation to also exchange Privacy Requests.
The purpose of Privacy Request Multicast Protocol (hereby the **Protocol**) is to define messaging and sequences of such exchanges.

Such a need might arise from contractual liabilities of Systems or from legal obligations such as in the case of Article 19 of [GDPR][GDPR] in European Union.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-architecture/)


## Design Choices

- The Protocol is agnostic from any particular way to address Systems and transfer messages to and from them. Systems are responsible of knowing how to identify and address another System with which they exchange data or any object defined in [PRIV][PRIV].

- Systems MAY be capable of sending Privacy Requests (and other PRIV concepts), receiving them, or both. E.g. a browser might be capable of sending Privacy Requests but not receiving them.

- Systems SHOULD know only of Privacy Requests (and other PRIV concepts) concerning them i.e. that require some action from them or are likely to have implications on them.

- Systems process Privacy Requests and other PRIV concepts (e.g. legal-base related events and consents) in order of their dates, and regardless fo the order in which they have gain knowledge of them using the Protocol.

- The Protocol is agnostic of inter-system trust. A System MAY be implemented to trust other Systems to authenticate the Data Subject, covey responses, tell the truth or not. The security implications of such choices are out of scope of the Protocol.

- The Systems CAN apply the Protocol in the context of different [Scenarios][Scenarios].

- The Protocol is asynchronous, i.e. it is possible for one System to be unavailable when the other System aims to communicate with it.

- Systems are independent in their responses, i.e. a System MUST BE ABLE to respond to a Privacy Request addressed to it regardless of (the existence and the content of) the responses of other Systems.

- The Protocol can be used regardless of the Systems exchanging data in a one-off data dump, or through a continuous connection. The Protocol specifies no means for Systems to actually exchange data, and is only concerned by the privacy aspects of the data being exchanges.

## Design Goals

- Achieve information consistency (equal information) among all Systems exchanging data about one Data Subject. This information includes Privacy Requests and every information likely to impact the validity of legal bases and retention policies (including events such as those related to `CONTRACT` legal bases, Consents and modifications of Consents).

- Efficiency : Systems reach information consistency with minimal effort.

- Support for situations where the graph of data flow among Systems is cyclical.

- Information consistency is evaluated regardless of order and route from which information is obtained i.e. two systems having obtained same elements of information from different sources and in different order are considered to have equal information. [Sequential Consistency](https://en.wikipedia.org/wiki/Sequential_consistency) is not expected.

- [Strong Eventual Consistency](https://en.wikipedia.org/wiki/Eventual_consistency#Strong_eventual_consistency)

- Fully support [PRIV][PRIV] and ints design choices

- Support highly volatile networks of Systems exchanging data about one Data Subject i.e. Systems can participate on an ad-hoc basis, only once, disappear and reappear.

## Proposal



## Design Implications for Systems Implementing PRMP

### Callback Mechanism

Systems MUST implement, internally, a callback mechanism, with a message queue to account for asynchronous nature of the Protocol.

### Using blockchain or hashgraph

Having in mind the multitude of risks associated with exchange of PRIV concepts across Systems (involving possible attacks), there is a clear case for implementing PRMP on top of an existing distributed ledger with its own safety mechanisms.

## Safety Considerations


## Questions and Discussion Topics

## Alternatives

## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.
- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,
- **[RFC3986]**  Berners-Lee, T., Fielding, R., and L. Masinter, ["Uniform Resource Identifier (URI): Generic Syntax"](https://www.rfc-editor.org/rfc/rfc3986), STD 66, RFC 3986, January 2005.
- **[RFC-PRIV]** Stankovic, M., ["Privacy Request Interchange Vocabulary"](../priv/RFC-PRIV.md)
- **[RFC-Lexicon-2]** Stankovic, M., ["Lexicon"](../lexicon/RFC-Lexicon-2.md)


### Informative References

- [Examples of use](../priv/examples.md)
- [Expected Behavior of Implementing Systems](../priv/expected-behavior.md)
- [Scenarios](./scenarios.md)
- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
