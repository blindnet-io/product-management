# blindnet devkit Functional Requirements Document

| Status        | Accepted as normative draft                                                    |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | [milstan](https://github.com/milstan), [blindnet engineering](https://github.com/orgs/blindnet-io/teams/engineering)             |
| **PR**   | **TBD** |
| **Version**   | 1.0                                                                             |
| **Updated**   | 2022-07-04                                                                             |

This document specifies the technical requirements for the blindnet devkit.

## Terminology

- All terms defined in [RFC-Lexicon-2][Lexicon] are to be interpreted as described there
- Any additional precision about the terms defined in [RFC-Lexicon-2][Lexicon], as well as additional terms such as Consent and Legal Base, provided in [High Level Conceptualization][HLC] is to be considered normative
- We use the terms Capture Component, Encryption and Access Management Engine, Privacy Computation Engine, Privacy Compiler, Privacy Request Capture Interface, Schemas and Storage Component as defined in [High Level Architecture][HLA]
- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119][RFC 2119]
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"

## Functional Requirements

> We refer to **Privacy Manager** as to a bundle including [Privacy Request Capture Interface](#privacy-request-capture-interface) and [Data Consumer Interface](#data-consumer-interface)

In each sub-section, we understand by **Component** the component of blindnet devkit indicated in the subsection title.

### Privacy Request Capture Interface

#### FR-PRCI-001

The component MUST display the identity of the Organization, its representative, and its DPO, as well as the privacy policy (or link to it).



### Data Consumer Interface
> The scope covered by this document only concerns the Q3 2022 milestone (does not include data view)

#### FR-DCI-001

The Component MUST authenticate (and log in) any Data Consumer prior to exposing other functionalities to them.

#### FR-DCI-002

The Component MUST allow a logged-in Data Consumer to log out.


### Privacy Request Computation Engine

#### FR-PRCE-001

The Component MUST receive Privacy Requests from other components (or other Systems) expressed in a machine-readable format using [PRIV][PRIV].

The Component MUST confirm reception, or signal an error (messaging **TBD**).

### Capture Component (a.k.a. Metadata Engine)

#### FR-CC-001

The Component MUST generate metadata using [PRIV][PRIV], given:
- any actual data concerning a Data Subject, and
- a set of settings describing the data capture practices using [PRIV][PRIV] Terms (mapping form/database structure to [PRIV][PRIV] Terms).


## References
- **Lexicon** [RFC-Lexicon-2][Lexicon]
- **HLA** [High Level Architecture][HLA]
- **HLC** [High Level Conceptualization][HLC]
- **PRIV** [Privacy Request Interchange Vocabulary][PRIV]

[Lexicon]: ../../refs/lexicon/RFC-Lexicon-2.md "RFC-Lexicon-2"
[HLA]: ../../refs/high-level-architecture/ "High Level Architecture"
[HLC]: ../../refs/high-level-conceptualization/ "High Level Conceptualization"
[PRIV]: ../../refs/schemas/priv/RFC-PRIV.md "Privacy Request Interchange Vocabulary"
[RFC 2119]: https://datatracker.ietf.org/doc/html/rfc2119 "Key words for use in RFCs to Indicate Requirement Levels"
