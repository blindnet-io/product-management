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

#### FR-PRCI-002

The component MUST allow a Data Subject to create a rights request with the properties described in [PRIV][PRIV], or they may enter their own properties.

#### FR-PRCI-003

The component MAY produce a JSON file for a created request.

#### FR-PRCI-004

The component MUST inform the user of the status of their previously created requests.

#### FR-PRCI-005

The component SHOULD guide the user in creating a privacy request in order to aid their understanding, as well as to make the request as precise, correct, and automatically processable as possible.

#### FR-PRCI-006

The component MAY be configured to display only a subset of the values for certain request properties, based on applicability to the organization. The component MAY also recommend values for certain properties, based on frequent occurrence in previous requests.

### Data Consumer Interface
> The scope covered by this document only concerns the Q3 2022 milestone (does not include data view)

#### FR-DCI-001

The Component MUST authenticate (and log in) any Data Consumer prior to exposing other functionalities to them.

#### FR-DCI-002

The Component MUST allow a logged-in Data Consumer to log out.

#### FR-DCI-003

The component MUST allow a Data Consumer to view a list of all new and processed privacy requests. This list MAY be sorted in ascending or descending order by date received.

### Privacy Request Computation Engine

**TBD: handling real data access for certaing types of Privacy Requests**
**TBD: handling Provenance**
**TBD: handling Retention Policies**

#### FR-PRCE-001

The Component MUST receive Privacy Requests from other components (or other Systems) expressed in a machine-readable format using [PRIV][PRIV].

Depending on the type of a Privacy Request, the requesting party migh need to authenticate.

#### FR-PRCE-

The Component MUST authenticate incoming requests.

Authentication is done through blindnet tokens.
Two types of tokens exist:
- user tokens
- system token

Following roles are observed in a user token:
- data subject
- data consumer
- DPO

#### FR-PRCE-

The Component MUST automatically resolve TRANSPARENCY demands.

The Component SHOULD automatically resolve other types of demands if applicable.

#### FR-PRCE-

The Component MUST return the list of requests to a requesting component.

#### FR-PRCE-

The Component MUST receive Privacy Request resolution from other components and create a Privacy Response.

#### FR-PRCE-

The Component MUST notify a Data Subject when the Privacy Response is finished.

#### FR-PRCE-

The Component MUST receive configuration for a particular system, according to [PRIV][PRIV] and [Expected behavior of systems implementing PRIV][[expected-behavior].

Configuration can be submitted by either a specialized user (e.g. with the DPO role) through specialized UI or directly from the system.

Configuration includes:
- general info
- list of selectors
- for each selector
  - privacy scope
  - retention policy
  - target provenance
- list of legal bases (necessary, contracts, legitimate interests)
- privacy scope for each legal base
- consent templates and associated privacy scopes
- active regulations (e.g. GDPR)

#### FR-PRCE-

The Component MUST recive consents from a user of the implementing system.
Consent is received as an ID of a configured consent template, and is used for calculation of Eligible privacy scope of a user.

#### FR-PRCE-

The Component MUST return information about it's configuration.
- list of legal bases
- list of regulations
- list of selectors
- required consents for each selector to be compliant with the regulation
- list of consents a user has submitted
- selectors (types of data) that can be processed for a user, in terms of user's consents
- etc.

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
- **Expected behavior** [Privacy Request Interchange Vocabulary : Expected Behavior of Implementing Systems][expected-behavior]

[Lexicon]: ../../refs/lexicon/RFC-Lexicon-2.md "RFC-Lexicon-2"
[HLA]: ../../refs/high-level-architecture/ "High Level Architecture"
[HLC]: ../../refs/high-level-conceptualization/ "High Level Conceptualization"
[PRIV]: ../../refs/schemas/priv/RFC-PRIV.md "Privacy Request Interchange Vocabulary"
[RFC 2119]: https://datatracker.ietf.org/doc/html/rfc2119 "Key words for use in RFCs to Indicate Requirement Levels"
[expected-behavior]: ../../refs/schemas/priv/expected-behavior.md "Privacy Request Interchange Vocabulary : Expected Behavior of Implementing Systems"