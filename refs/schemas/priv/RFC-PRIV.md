# Privacy Request Interchange Vocabulary (PRIV)

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [659](https://github.com/blindnet-io/product-management/pull/659)                      |
| **Author(s)** | [milstan](https://github.com/milstan) (milstan@blindnet.io)                                                          |
| **Updated**   | 2022-06-14                                                                             |



## Introduction

We propose a simple vocabulary for representing [Privacy Requests](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization#data-capture--rights-requests).

The vocabulary introduces a finite set of `concepts`, `properties` and `terms`. `Concepts` define the objects of exchange, `properties` define their characteristics, and `terms` define commonly understood values of properties.

This vocabulary corresponds to the [Schemas](../high-level-architecture#schemas) component of the [High-Level Architecture](../high-level-architecture).

Additional documents: [Examples of use](./examples.md), [Scenarios](./scenarios.md) and [Expected Behavior of Implementing Systems](./expected-behavior.md), complement this document.


## Motivation

An individual is in connection with software Systems (and Organizations operating them) that process the individual's data.
In order to [regulate the relationship](../notion-of-privacy/notion-of-privacy.md) with those Systems (and Organizations), the individual makes requests related to their privacy.

With a Privacy Request the individual aims to gain a degree of transparency about data processing and a degree of control over the data and over the data processing. Allowing individuals to make Privacy Requests is becoming more and more a legal obligation.

Different Systems, and different components of a single System, including different components of blindnet devkit are likely to exchange information about Privacy Requests. Therefore, a common format is needed to facilitate exchange of information without loss of semantics. The goal of Privacy Request Interchange Vocabulary is to establish a shared conceptualization and format of Privacy Request so that their processing can be, as much as possible, automatized by the Systems.


## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-architecture/)

## Version

This document defines the version `1.0` of the Privacy Request Interchange Vocabulary.

## Design Considerations

### Design Inspiration

- **Smart data structures and dumb code works a lot better than the other way around.** lesson No 9 from Raymond, Eric Steven. ["The Cathedral and the Bazaar"](https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar). We want PRIF to embody a smart way of thinking about privacy, solving common challenges through the data structure itself.

- **Often, the most striking and innovative solutions come from realizing that your concept of the problem was wrong.** lesson No 12 from Raymond, Eric Steven. ["The Cathedral and the Bazaar"](https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar). We indeed now have novel understanding of the [problem of Privacy in Software Systems](../notion-of-privacy/notion-of-privacy.md).

### Design Goals

With this design we seek:
- Consistent unambiguous interpretation of Privacy Requests (including shared understanding of their meaning and ways to uniquely identify them) across different Systems, independently of programming languages and components they use
- Minimal exposure of Data Subject and their data during the processing of a Privacy Request,
- Making processing of Privacy Requests as automatic as possible,
- Compatibility with the use of different protocols and tools for user identity management, authentication, and encryption,
- Allowing developers to fully comply with [supported legislation](#supported-legislation) related to Privacy Requests quickly and easily
- Exhaustivity with regards to situations we need to support in response to [supported legislation](#supported-legislation) yet Extensibility in case new situations arise in the future.
- Highly normative minimal specification, using as much as possible the [Plain Language](https://www.plainlanguage.gov/media/FederalPLGuidelines.pdf) while at the same time making clear references to the (often misfortunate) language of the [supported legislations](#supported-legislation)
- Limit, as much as possible, the possibility of representing the same meaning in more than one way
- Decentralized design compatible with both the Internet's Client-Server Architecture and Metaverse/Web3 Architecture

### Design Choices

We have made the following choices:
- **Language Independence**. The Privacy Request Interchange Vocabulary is independent from any programming language, or any format or language for expressing structured data, and can be materialized in different forms such as json, xml, or other. A [json schema](./json-schema/priv.schema.json) is provided for convenience.

- **Rich Semantics**. The Privacy Request Interchange Vocabulary includes `terms` - reserved words to describe common types of Privacy Requests, categories of data, categories of data processing and other key notions. This choice is made to facilitate their uniform interpretation by the implementing systems. Their [human-readable titles and descriptions](dictionary) are provided in json format for convenience.

- **Multiple User Identities**. The Privacy Request Interchange Vocabulary  allows for a Data Subject to be identified using more than one user identity. This choice is made to enable the Privacy Request to be easily exchanged across Systems that use different user identifiers.

- **Systems resolve Privacy Requests**. The Privacy Requests are interpreted at the level of a particular System. If an Organization operates several Systems, and if the Data Subject wants to have the Privacy Request transmitted to all of them, each System may respond differently. While a Privacy Request can target a group of Systems, the most atomic target of a Privacy Request is thus the System exposing an API for Privacy Requests, and it is only at this level that a Privacy Request can be resolved.

- **Decentralized IDs**. The Privacy Request Interchange Vocabulary uses decentralized ways to uniquely identify Data Subjects, Systems, Requests and their elements. The exchange of Privacy Requests can happen without a centralized entity to control identity disambiguation.

## Proposal

The Privacy Request Interchange Vocabulary includes the following:

- **Concepts**:
[Consent](#consent),
[Data Capture](#data-capture),
[Data Capture Fragment](#data-capture-fragments),
[Data Subject Identity](#decentralized-identity-of-data-subjects),
[Demand](#demands),
[Demand Restriction](#demand-restrictions) (including [Privacy Scope Restriction](#privacy-scope),[Consent Restriction](#consent-restriction), [Capture Restriction](#capture-restriction), [Date Range](#date-range), [Provenance Restriction](#provenance-restriction), [Data Reference Restriction](#data-reference-restriction)),
[Privacy Request](#privacy-request),
[Privacy Request Response](#privacy-request-response),
[Privacy Scope](#privacy-scope)(and its dimensions: *Data Category*, *Processing Category* and *Purpose*), [Provenance](#provenance),
[Retention Policy](#retention-policy),
[Data Subject Identity](#decentralized-identity-of-data-subjects)

- **Properties**: `action`, `after`, `answers`, `capture-id`, `capture-ids`, `consent-id`,`consent-ids`, `data-subject`,`data`, `data-categories`, `data-reference`, `data-subject`, `date`,`demand-id`, `demands`, `dsid`, `dsid-schema`, `duration`, `expires`,`fragment-id`, `fragments`, `from`, `includes`, `in-response-to`,`lang`, `legal-base`, `message`, `motive`, `policy-type`, `processing-categories`, `provenance, `provenance-category`, `purposes`, `replaces`, `response-id`, `restrictions`, `request-id`, `replaced-by`, `retention`, `requested-action`, `scope`, `selector`, `status`, `system`, `target`, `to`, `vocab`

- **<a name="terms"></a>Terms**: all terms included in the [dictionary](./dictionary), and particularly:

    - **<a name="actions"></a>Action Terms**: {`ACCESS`, `DELETE`, `MODIFY`, `OBJECT`, `PORTABILITY`, `RESTRICT`, `REVOKE-CONSENT`, `TRANSPARENCY`, `TRANSPARENCY.DATA-CATEGORIES`, `TRANSPARENCY.DPO`, `TRANSPARENCY.KNOWN`, `TRANSPARENCY.LEGAL-BASES`, `TRANSPARENCY.ORGANIZATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.PROCESSING-CATEGORIES`, `TRANSPARENCY.PROVENANCE`, `TRANSPARENCY.PURPOSE`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO`, `OTHER-DEMAND`} or any of their subcategories defined using the [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/actions](./dictionary/actions).*

    - **<a name="data-categories"></a>Data Category Terms**: {`AFFILIATION`, `AFFILIATION.MEMBERSHIP`, `AFFILIATION.SCHOOL`, `AFFILIATION.WORKPLACE`, `BEHAVIOR`, `BEHAVIOR.ACTIVITY`, `BEHAVIOR.CONNECTION`, `BEHAVIOR.PREFERENCE`, `BEHAVIOR.TELEMETRY`, `BIOMETRIC`, `CONTACT`, `CONTACT.EMAIL`, `CONTACT.ADDRESS`, `CONTACT.PHONE`, `DEMOGRAPHIC`, `DEMOGRAPHIC.AGE`, `DEMOGRAPHIC.BELIEFS`, `DEMOGRAPHIC.GENDER`, `DEMOGRAPHIC.ORIGIN`, `DEMOGRAPHIC.RACE`, `DEMOGRAPHIC.SEXUAL-ORIENTATION`, `DEVICE`, `FINANCIAL`, `FINANCIAL.BANK-ACCOUNT`, `GENETIC`, `HEALTH`, `IMAGE`, `LOCATION`, `NAME`, `PROFILING`, `RELATIONSHIPS`, `UID`, `UID.ID`, `UID.IP`, `UID.USER-ACCOUNT` , `UID.SOCIAL-MEDIA` , `OTHER-DATA`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation) including any [Data Capture Fragment](#data-capture-fragments) `selector`s. *See definitions in the [dictionary/data-categories](./dictionary/data-categories).*

    - **<a name="processing-categories"></a>Processing Category Terms**: {`ANONYMIZATION`, `AUTOMATED-INFERENCE`, `AUTOMATED-DECISION-MAKING`, `COLLECTION`, `GENERATING`, `PUBLISHING`, `STORING`, `SHARING`, `USING`, `OTHER-PROCESSING`}  or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/processing-categories](./dictionary/processing-categories).*

    - **<a name="purposes"></a>Purposes Terms**: {`ADVERTISING`, `COMPLIANCE`, `EMPLOYMENT`, `JUSTICE`, `MARKETING`, `MEDICAL`, `PERSONALIZATION`, `PUBLIC-INTERESTS`, `RESEARCH`, `SALE`, `SECURITY`, `SERVICES`, `SERVICES.ADDITIONAL-SERVICES`, `SERVICES.BASIC-SERVICE`, `SOCIAL-PROTECTION`, `TRACKING`, `VITAL-INTERESTS`, `OTHER-PURPOSE`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/purposes](./dictionary/purposes).*

    -  **<a name="provenance-categories"></a>Provenance Terms**: {`DERIVED`, `TRANSFERRED`, `USER`, `USER.DATA-SUBJECT`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/provenance](./dictionary/provenance).*

    -  **<a name="targets"></a>Target Terms**: {`ORGANIZATION`, `PARTNERS`, `SYSTEM`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/targets](./dictionary/targets).*

    -  **<a name="target-directions"></a>Target Direction Terms**: {`PARTNERS.DOWNWARD`, `PARTNERS.UPWARD`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/targets](./dictionary/targets).*

    - **<a name="statuses"></a>Status Terms**: {`GRANTED`, `DENIED`, `PARTIALLY-GRANTED`, `UNDER-REVIEW`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/statuses](./dictionary/statuses).*

    - **<a name="motives"></a>Motive Terms**: {`IDENTITY-UNCONFIRMED`, `LANGUAGE-UNSUPPORTED`, `VALID-REASONS`, `IMPOSSIBLE`, `NO-SUCH-DATA`, `REQUEST-UNSUPPORTED`, `USER-UNKNOWN`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/motives](./dictionary/motives).*

    - **<a name="boolean"></a>Boolean Terms**: {`YES`, `NO`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/boolean](./dictionary/boolean).*

    - **<a name="legal-bases"></a>Legal Base Terms**: {`CONTRACT`, `CONSENT`, `LEGITIMATE-INTEREST`, `NECESSARY`, `OTHER-LEGAL-BASE`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/legal-bases](./dictionary/legal-bases).*

    - **<a name="retentions"></a>Retention Terms**: {NO-LONGER-THAN, "NO-LESS-THAN"} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/retentions](./dictionary/retentions).*

    - **<a name="events"></a>Event Terms**: {`CAPTURE-DATE`,`RELATIONSHIP-END`, `SERVICE-END`} or any of their subcategories defined according to [Term Dot Notation](#term-dot-notation). *See definitions in the [dictionary/events](./dictionary/events).*

### Privacy Request

Data Subject is the author of a Privacy Request.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-subject` |  1-* | [Data Subject Identities](#decentralized-identity-of-data-subjects) each containing one `dsid` and one `dsid-schema`|

A Privacy Request is made by one and only one Data Subject.

A System MAY have multiple ways to identify the Data Subject, especially when data about them came from some other System that uses different identifiers.

The System capturing the Privacy Request MAY associate multiple Data Subject Identities to the Privacy Request, especially if the Privacy Request is likely to be transmitted to other systems.

An array of one or more [Data Subject Identities](#decentralized-identity-of-data-subjects) MUST be provided in order to match the Data Subject with the data concerning them.

In addition, the Privacy Request has other meta-data:

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `request-id` | 1 | Unique ID for referring to this request in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | 1 | Date and Time when Privacy Request was created in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `demands` | 1-* | [Demands](#demands) |

The Data Subject can request several things (e.g. see the data the System has on me, know the source from where you have got it, and have my data deleted). We call those 'Demands'.

A Privacy Request includes an array of one or more Demands.

#### Demands

A Demand is a concrete action that the user requests.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `demand-id` | 1 | Unique ID for referring to this demand in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `action` | 1 | Unique value. One of the [Action Terms](#actions) |
| `message` | 0-1 | Optional string comment, motivation or explanation of Demand |
| `lang` | 0-1 | Optional string Language of textual message associated with demands in the format of [FRC5646](https://datatracker.ietf.org/doc/rfc5646/) |
| `data` | 0-* | Optionally concrete data |


The key element that defines the nature of the Demand is the `action`. A Demand MUST have one and only one `action`.

Actions are hierarchical, and defined using the [Term Dot Notation](#term-dot-notation).

E.g. when `TRANSPARENCY` is demanded, Systems MUST interpret the demand as if all the subcategories of `TRANSPARENCY` were demanded.

Certain Demands MAY include data, such as a `MODIFY` Demand where new data MAY be provided by the Data Subject.

##### Demand Restrictions

The `action` that the Data Subject requests with a particular Demand MUST be interpreted in the context of restrictions.

A Demand MAY refer to only certain Privacy Scope (Data Categories, certain Processing Categories, certain Purposes of processing) or may only refer to particular Consents (e.g. those that the Data Subject wants to revoke) or to particular Data Captures (e.g. those that the Data Subject want to delete).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `restrictions` |  0-* | An optional array of restriction objects, each being one of [Privacy Scope](#privacy-scope), [Consent Restriction](#consent-restriction), [Capture Restriction](#capture-restriction), [Date Range](#date-range), [Provenance Restriction](#provenance-restriction), [Data Reference Restriction](#data-reference-restriction)|

When more than one restriction is specified, the System MUST interpret the Demand as referring to the **intersection of restrictions**.
For example let us consider a `DELETE` demand having two restrictions: `data-category`:`LOCATION` as Privacy Scope, and from 11th to 15th of June 2022 as Date Range.
The System SHOULD understand that the Data Subject wants the System to delete only their location data processed in this precise period.

A demand with multiple restrictions MUST NOT have more than one restriction of the same type.

###### Privacy Scope

A Privacy Scope is be defined by three dimensions: Data Categories, Categories of Processing, and Purposes of Processing.

A Data Subject can formulate a Demand or give Consent within a particular Privacy Scope, e.g. only referring to `COLLECTING` (Category of Processing) `CONTACT` data (Category of Data) for `PERSONALIZATION` (Purpose of Processing).

Privacy Scope can be understood as a vector space defined by those three dimensions.

```

Privacy Scope = (Data Categories) x (Processing Category) x (Purposes of Processing)

```

It is possible to specify a Privacy Scope by referring to only one or two, or none (out of those tree) dimensions.
An unspecified dimension MUST be interpreted as designating the totality of Terms that are eligible as one of its Expected values.

E.g. A Privacy Scope defined only by `data-categories`: `CONTACT` is interpreted as any [Processing](#processing-categories), for any [Purpose](#purpose) or any data marked with `CONTACT` or any of its subcategories including `CONTACT.EMAIL`, `CONTACT.ADDRESS`, `CONTACT.PHONE`.
This Privacy Scope includes Privacy Scope Triples that are all possible combinations of those known subcategories (including [Data Capture Fragment](#data-capture-fragments) `selectors`) of `CONTACT` with all known [Processing](#processing-categories) and with all known [Purpose Terms](#purpose).

*Data Categories*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-categories` |  0-* | [Data Category Terms](#data-categories)|

When several values are given, Systems MUST interpret the `data-categories` dimension as a **union** of all the categories indicated.

E.g. if `GENETIC` and `FINANCIAL` are specified, the `data-categories` dimension includes all known subcategories of those two [Data Category Terms](#data-categories), including `FINANCIAL.BANK-ACCOUNT`. If the the System knows of a system-specific subcategory `GENERIC.GENOME`, then the `data-categories` dimension includes that as well.

In the absence of indication of any `data-categories` dimension, Systems MUST interpret the Privacy Scope as being related to all and any known [Data Category](#data-categories).


*Processing Categories*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `processing-categories` | 0-* | [Processing Category Terms](#processing-categories) |

When several values are given, Systems MUST interpret the `processing-categories` dimension as a **union** of all the processing categories indicated.

E.g. if `STORING` and `GENERATING` are specified, the `processing-categories` dimension includes all known subcategories of those two [Processing Category Terms](#processing-categories). If the the System knows of a system-specific subcategory `GENERATING.TRANSLATING`, then the `processing-categories` dimension includes that as well.

In the absence of indication of any `processing-categories` dimension, Systems MUST interpret the Demand as being related to all and any known [Processing Category](#processing-categories).


*Purposes of Processing*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `purposes` | 0-* | [Purposes Terms](#purposes) |

When several values are given, Systems MUST interpret the `purposes` restriction as a **union** of all the purposes indicated.

E.g. if `RESEARCH` and `SERVICES` are specified, the `purposes` dimension includes all known subcategories of those two [Purposes Terms](#purposes) including `SERVICES.BASIC-SERVICE` and `SERVICES.ADDITIONAL-SERVICES`. If the the System knows of a system-specific subcategory `RESEARCH.MEDICAL-RESEARCH`, then the `purposes` dimension includes that as well.

In the absence of indication of any `purpose` restriction, Systems MUST interpret the Demand as being related to all and any known [Purpose](#purposes).

###### Consent Restriction

A Demand can be restricted to particular Consent ID(s). For example, a Data Subject revokes a particular consent only (the one related to his data being shared with 3rd parties) but maintains other consents they may have given.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `consent-ids` | 0-* | Optional array of consent ids to indicate that the Demand (e.g. a `REVOKE-CONSENT` Demand) is restricted to particular consents. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `consent-ids` are indicated, Systems MUST interpret the Demand as related to all Consents related to indicated `consent-ids`.

###### Capture Restriction

A Demand can be restricted to particular Capture ID(s). For example, a Data Subject to delete a particular data, they indicate the [Data Capture](#data-capture) concerned by their Demand.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `capture-ids` | 0-* | Optional array of [Data Capture](#data-capture) IDs to indicate that the Demand (e.g. a `DELETE` Demand) is restricted to data captured within particular Data Captures. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `capture-ids` are indicated, Systems MUST interpret the demand all related to (the **union** of) all the data captured as part of those Data Captures.

###### Date Range

A Demand can be restricted to particular Date Range, for example the Data Subject may `OBJECT` to data collection in a particular time period, or they might want to `DELETE` only data collected at certain dates.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `from` | 0-* | Date and Time when the Date Range starts in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `to` | 0-* | Date and Time when the Date Range ends in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |

A Date Range defined by only one of the {`from`, `to`} properties indicates a period of time after or before a certain date, unbounded on the other end.

###### Provenance Restriction

A Demand can be restricted to particular `provenance-category`, for example the Data Subject may `OBJECT` to data that is `DERIVED` about them being shared (`processing-category`:`SHARING`), or they may want to `RESTRICT` the `SHARING` of their data only to the data that came from themselves `USER`.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `provenance-category` | 1 | [Provenance Terms](#provenance-categories) |
| `target` | 0-1 | [Target Terms](#targets). In absence of indication `SYSTEM` is assumed |

Optionally the Provenance Restriction may also include a particular [Target](#targets).

E.g. the Data Subject might demand to have `ACCESS` to data that was `TRANSFERRED` by partner Systems (`target`:`PARTNERS`).

Not to be confused with [Provenance](#provenance).

###### Data Reference Restriction

A Demand can be restricted to particular `data-reference` to precisely identify particular data to which the Data Subject wants to refer in their Demand. E.g., a Data Subject can request from a law-firm to `DELETE` data from a particular file and provide the reference of that file. A Data Subject may request from a website to `DELETE` their photo from a particular web URL.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-reference` | 1-* | one or more references that uniquely identify the data that the Demand concerns (e.g. URLs, file IDs, etc.)|

#### Targets

It is common for Internet Systems to be distributed (organised in a set of connected websites and applications) and to exchange data among themselves.

It is therefore convenient for a Data Subject to be able to formulate Privacy Requests (but also give Consents) targeting well-defined Systems.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `target` | 0-1 | [Target Terms](#targets) or [Target Direction Terms](#target-directions)
 In absence of indication `SYSTEM` is assumed |

`SYSTEM` refers to the particular System with which the Data Subject is in direct interaction while making the Privacy Request (or giving the Consent).

`ORGANIZATION` includes, in addition to the `SYSTEM`, all other Systems belonging to the same Organization. In the context of Systems that are essentially wbesites, the `ORGANIZATION` Term SHOULD be understood as all Systems being a part of the same [First-Party Set](https://github.com/WICG/first-party-sets).

`PARTNERS.DOWNWARD` includes, in addition to the `SYSTEM`, and to all other Systems belonging to the same Organization, all other Systems belonging to Organizations with which the data about the Data Subject has been shared.

`PARTNERS.UPWARD` includes, in addition to the `SYSTEM`, and to all other Systems belonging to the same Organization,  all other Systems belonging to Organizations from which the data about the Data Subject has been obtained.

`PARTNERS` includes, in addition to the `SYSTEM`, and to all other Systems belonging to the same Organization, all other Systems belonging to Organizations with which any sort of exchange of data concerning the Data Subject has been performed.

Different values of the `target` Property imply different obligations for the System receiving a Privacy Request to transfer that request to other Systems.

Let us imagine the following situation: System A gave information about the Data Subject to System B, and System B gave information about the Data Subject to System C. The same Organization that operates System B, also operates System D.

When System B receives a Privacy Request having `target` value:
- `SYSTEM`, it SHOULD NOT transfer it to any other system.
- `ORGANIZATION` for a `target`, it MUST transfer it to all other systems operated by the same Organization (System D in our example).
- `PARTNERS.DOWNWARD` it MUST also send it to all systems to which it transferred data about the Data Subject (System C).
- `PARTNERS.UPWARD` it MUST also send it to all systems from which it obtained data about the Data Subject (System A).
- `PARTNERS`, it MUST also send it to all systems from which it obtained data about the Data Subject or to which it gave information about the Data Subject (System A and System C).

Systems should interpret the target of Privacy Request regardless of the Privacy Request being received directly from the Data Subject or from a corresponding System.
This means that the same `target` value of the same Privacy Request transferred across several Systems may end-up being interpreted differently by those Systems (e.g. in every System `PARTNERS.DOWNWARD` is likely to be resolved to different Systems)


### Privacy Request Response

Systems SHOULD respond to [Privacy Requests](#privacy-request).
Regardless of the [scenario (Responding to the Data Subject directly or to the System)](./scenarios.md#response) Systems SHOULD generate a response using the Privacy Request Interchange Vocabulary.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `response-id` | 1 | Unique ID for referring to this request in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `in-response-to` | 1 | `request-id` of the Privacy Request to which response is made or `demand-id` of the particular Demand to which response is made, in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | 1 | Date and Time when Privacy Request Response was created in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `system` | 1 | System ID of the System having generated the response (**Format TBD**) |
| `requested-action` | 0-1 | Optional information about the action that was demanded, and to which the response is made. [Action](#actions)|
| `data-subject` |  0-* | Optional indication of the [Data Subject Identities](#decentralized-identity-of-data-subjects) to which the response refers to |
| `status` | 1 | [Status Terms](#statuses) |
| `motive` | 0-* | [Motive Terms](#motives) |
| `answers` | 0-* | [Terms](#terms) |
| `message` | 0-1 | Optional string comment, motivation or explanation of Demand |
| `lang` | 0-1 | Optional string Language of textual message associated with demands in the format of [FRC5646](https://datatracker.ietf.org/doc/rfc5646/) |
| `includes` | 0-* | Optionally an array of one or more [Privacy Request Response](#privacy-request-response)s |
| `data` | 0-* | Optionally concrete data to which access is being given|

A Privacy Request Response MUST have:
- a unique ID,
- a clear indication of the particular Privacy Request or the particular Demand to which its content refers,
- a date,
- a status.

Privacy Request Responses CAN be nested. One can imagine a Privacy Request Response to a particular Privacy Request, that `includes` Privacy Request Responses to the particular Demands made in that Privacy Request. Several Systems MAY respond to the same Privacy Request or Demand, and one System MAY nest them in order to gather them and send them back to the Data Subject (in the [Coordinated Response secenario](./scenarios.md#coordinated-response)).

When a Demand is being denied, the Privacy Request Response MUST provide a `motive`.

>To illustrate the `answers` value, we can imagine a `TRANSPARENCY.DATA-CATEGORIES` Demand, to which a response may include `answers`: `CONTACT`, `IMAGE`. Or a `TRANSPARENCY.KNOWN` Demand to which the answer may include `answers`: `YES` from [Boolean Terms](#boolean).

### Consent

A Consent is given by one Data Subject which can be identified by one or more [Data Subject Identities](#decentralized-identity-of-data-subjects).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-subject` |  1-* | [Data Subject Identities](#decentralized-identity-of-data-subjects) each containing one `dsid` and one `dsid-schema`|
| `consent-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | 1 | Date and Time when Consent was given in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `expires` | 0-1 | Date and Time when Consent expires in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `target` | 0-1 | [Target Terms](#targets) to indicate the category of Systems to which consent for processing is given. In absence of indication `SYSTEM` is assumed. |
| `scope` |  0-1 | a [Privacy Scope](#privacy-scope) in absence of which the Consent SHOULD be interpreted as unlimited |
| `replaces` |  0-* | Optionally one or more 'consent-id's of previous [Consents](#consent) that have became void when this consent was made |
| `replaced-by` |  0-* | Optionally one or more 'consent-id's of previous [Consents](#consent) that have became void when this consent was made |

### Data Capture

A Data Capture is given by one Data Subject which can be identified by one or more [Data Subject Identities](#decentralized-identity-of-data-subjects).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-subject` |  1-* | [Data Subject Identities](#decentralized-identity-of-data-subjects) each containing one `dsid` and one `dsid-schema`|
| `capture-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `data-reference` | 1-* | one or more references that uniquely identify the data that the capture concerns (e.g. a legal case file reference, account ID, contract ID, a URL)|
| `target` | 0-1 | [Target Terms](#targets). In absence of indication `SYSTEM` is assumed |
| `fragments` | 1-* | One or more [Data Capture Fragments](#data-capture-fragments) |

A Data Capture concerns one and only one Data Subject who CAN be identified by multiple Data Subject Identities.

#### Data Capture Fragments

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `fragment-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `selector` | 1 | a string used to uniquely identify a data field (in the System's data model) to which the fragment corresponds. MUST be a subcategory of a [Data Category](#data-categories) and MUST be defined according to [Term Dot Notation](#term-dot-notation) |
| `date` | 1 | Date and Time when data was Captured was given in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `scope` |  0-1 | a [Privacy Scope](#privacy-scope) in absence of which the fragment SHOULD be interpreted as unlimited, including all categories of all dimensions |
| `target` | 0-1 | [Target Terms](#targets). In absence of indication `SYSTEM` is assumed |
| `retention` | 1-* | one or more [Retention Policies](#retention-policy) |
| `provenance` | 1-* | one or more [Provenance](#provenance) |
| `data` | 0-* | Optionally concrete data (Format **TBD**) |
| `legal-base` | 0-* | [Legal Bases](#legal-bases) |

A `selector` MUST include, at the beginning of its string, one of the [Data Category Terms](#data-categories).
Its syntax MUST follow the [Term Dot Notation](#term-dot-notation).
A `selector` is considered a subcategory (in the sense of the [Term Dot Notation](#term-dot-notation)) of the most granular [Data Category Term](#data-categories) that it includes at at the beginning of its string.

For example selectors 'CONTACT.ADDRESS.SHIPPING' and 'CONTACT.ADDRESS.BILLING' indicate that the data being captured by a particular fragment belonging to the `CONTACT.ADDRESS` [Data Category](#data-categories) of which they are considered to be a subcategory.

While the Data Categories are globally defined by PRIV and interpreted the same way by all implementing Systems, the selectors are defined by the Systems.
A `selector` uniquely identifies a particular data field that the Systems works with.
When several Systems exchange data among them, they SHOULD align on using the same `selectors` in the same way, in order to be able to correctly interoperate.

Processing MAY be legitimate according to one or more [Legal Bases](#legal-bases) for processing.
For example, a Data Subject can give explicit `CONSENT` when creating an account with a particular online service, and at the time, the System providing a service to the Data Subject might need to process their data in order to deliver a service or honor a `CONTRACT` (e.g. deliver the purchased goods to the Data Subjects address and issue an invoice).

Certain processing is made legitimate (`LEGITIMATE-INTEREST`) or mandatory (`NECESSARY`) by law, e.g. [Article 6 og GDPR](https://gdpr-info.eu/art-6-gdpr/).

##### Provenance

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `provenance-category` | 1 | [Provenance Terms](#provenance-categories) |
| `system` | 1 | System ID (**Format TBD**) |

Data provenance is interpreted in relation to a particular System.

The same Data Capture Fragment might be:
- data collected from the `USER` for one System (the one being in direct interaction with the Data Subject), and be
- data `TRANSFERRED` in the eyes of another System that obtained it through transfer from the user-facing System.

Not to be confused with [Provenance Restriction](#provenance-restriction).

##### Retention Policy

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-categories` | 1-* | Any of the any [Data Category Terms](#data-categories) or concrete [Data Capture Fragment](#data-capture-fragments) `selector`s within those categories |
| `policy-type` | 1 | [Retention](#retentions) |
| `duration` | 1 | Duration in JSON Schema [duration](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `after` | 1 | Event to which the retention duration is relative to. [Events](#events) |

When several `data-categories` values are given, they are interpreted as a **union**.

## Detailed Design

A separate document gives a list of [examples](examples.md) on how to represent real-life Privacy Requests, as defined in [supported legislation](#supported-legislation), or as modeled in existing systems with which we seek interoperability.

### JSON format

We provide a [JSON Schema document](./priv.schema.json) for machine-readable interpretation of Privacy Requests compliant with [v4 (or ideally lower) of IETF specification](https://datatracker.ietf.org/doc/html/draft-zyp-json-schema-04#:~:text=JSON%20Schema%20is%20a%20JSON,interaction%20control%20of%20JSON%20data.)

### Authenticated exchanges

Systems exchanging Privacy Requests MUST be able to do so in a way allowing them to verify the integrity of their content, and the identity of the system having emitted the Privacy Request. Ideally, Privacy Requests MAY be signed by Data Subjects themselves.

For this purposes Privacy Requests MAY be embedded as 'Claims' in [JWTs (RFC7519)](https://datatracker.ietf.org/doc/html/rfc7519).

### Decentralized Identity of Data Subjects

The Systems are only able to provide control to Data Subjects if they can identify them. On the other hand, there is no central authority to manage Data Subject identity globally.

Therefore, we use a set of attributes to uniquely identify one Data Subject. One and the same Data Subject can have multiple such identities.

#### Globally Unique Data Subject Identities

The identifiers used to refer to Data Subjects MUST be globally unique. One Data Subject identity corresponds to one Data Subject. One Data Subject can have several Data Subject Identities.

When refering to a Data Subject, Systems MUST use both of the following attributes:
- `dsid` - Data Subject ID
- `dsid-schema` - A scheme allowing to dereference the Data Subject ID

The (`dsid`,`dsid-schema`) pair denotes a globally unique reference to always the same Data Subject.

We refer to (`dsid`,`dsid-schema`) pairs as Data Subject Identities.

A Privacy Request MAY include several (`dsid`,`dsid-schema`) pairs that refer to the same user, in order to facilitate the interoperability of Privacy Requests across systems.

#### Data Subject ID Schemas

Systems using RRIF MUST implement at least the following `dsid-schema`:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`uuid`| Indicates that the value of the corresponding `dsid` attribute is a Universally Unique ID in the sens of [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) |

Systems using RRIF SHOULD implement at the following `dsid-schema`:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`email-sha-256`| Indicates that the value of the corresponding `dsid` attribute is the result of the SHA-256 hashing function taking the e-mail of the Data Subject as argument |

Additional Data Subject ID Schemes MAY be defined by convention. For example the following MAY be used:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`global-id`| Indicates that the value of the corresponding `dsid` attribute is the `gid_name` - User's GlobaliD name - used to identify the Data Subject in [GlobalId](https://developer.global.id/documentation/api%2Fidentity.html)|

#### Data Subject SHOULD be Authenticated

In some cases, valid reasons MAY exist for Systems to respond to Privacy Requests even from anonymous Data Subjects. This is the case, for example, with request relative to general data treatment practices practiced by the system.

However, in most cases, Systems MUST require the Data Subject to be authenticated as being indeed the person corresponding to the (`dsid`,`dsid-schema`) pair.

When processing Privacy Request, Systems MAY automatically disregard the (`dsid`,`dsid-schema`) paris for which they have not been able to establish Data Subject authentication.

However, the authentication does not necessarily have to be performed during the collection of the Privacy Request. It can be done separately. The design of PRIV aims to support [several authentication workflows](./scenarios.md#authentication), as many as possible authentication methods (i.e. be as much as possible agnostic from the authentication method).


#### Matching Multiple Data Subject Identities

Systems MAY keep track of Data Subject Identities that refer to the same Data Subject. In some cases, valid reasons MAY exist for Systems to ignore such information.

When Systems do know that one Data Subject Identity corresponds to the same user as another Data Subject Identity, then Systems SHOULD offer the Data Subject a possibility for their Privacy Requests, expressed in relation to one Data Subject Identity to be automatically extended to include other equivalent Data Subject Identities.

Systems SHOULD NOT imply Data Subject Identity equivalence from Privacy Requests, especially when granting Privacy Requests that require authentication.

### IDs are Globally Unique

All of the following identifiers `capture-id`, `fragment-id`, `consent-id`, `request-id`, `demand-id`, `response-id` MUST be globally unique and be generated according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) in order for the corresponding objects to be easily identifiable across systems.
The reason for using UUDIs is to allow Systems to independently generate globally unique identifiers while being autonomous from a central entity that would ensure identifier uniqueness.

Having a public ledger for UUDIs MAY be considered for Consents and Data Captures, but serious implications to Data Subject exposure MUST also be considered.
However, the design MUST be compatible with building a public decentralized ledger.

### Term Dot Notation

The vocabulary defines [Terms](#terms) to express different aspects of Privacy Request, Data Captures, Consents etc.

[Terms](#terms) follow Term Dot Notation (TDN), defined using the following ABNF (cf. [FRC5234](https://www.rfc-editor.org/info/rfc5234)):
```
term = category *subcategory

subcategory =  "." category

category = *(%x41–5A) *((%x2D) 1*(%x41–5A))

```
A category includes the union of all of its subcategories.
Terms can be specified at different levels of granularity.
E.g. the following statements are equivalent:
- `A.B`, `A`
- `A`

PRIV includes a set of [Terms](#terms), provided in the [dictionary](./dictionary).

This list is designed with the aim to be:
- **Unambiguous** : The developer using the schema knows without ambiguity which one (or which ones) to use in any given situation, AND
- **Complete** : They allow to express the totality of possible needs in the context of a user wanting to [regulate their privacy/connectedness](https://github.com/blindnet-io/product-management/blob/dogma/refs/notion-of-privacy/notion-of-privacy.md), as well as the totality of requests defined by the [supported legislation](#supported-legislation).

Implementing Systems SHOULD be able to interpret and operate with all the [Terms](#terms).

#### Interpreting subcategories

A term (`A.B`) is a subcategory of another term (`A`) if an only if the subcategory term's string includes at its beginning the totality of this other (supercategory) term's string.

E.g. `TRANSPARENCY.ORGANIZATION` is a subcategory if `TRANSPARENCY`.
`TRANSPARENCY.ORGANIZATION` is not a subcategory of `ORGANIZATION`

E.g. `CONTACT.ADDRESS.SHIPPING` is a subcategory of `CONTACT.ADDRESS`.
`CONTACT.ADDRESS.SHIPPING` is a subcategory of `CONTACT`


#### Extending Terms

When needed, Systems MAY include support for additional terms, not included in the [dictionary](./dictionary).
Such additional terms MUST be subcategories of one of the [Terms](#terms), and they MUST follow the same syntax of the [Term Dot Notation](#term-dot-notation).

Such Systems MAY manifest specific behavior in reaction to those additional terms, yet they may end-up communicating them with other Systems that only support the [Terms](#terms) from the [dictionary](./dictionary).

Systems processing Privacy Requests (or other Concepts) containing a term unknown to them, SHOULD deploy behavior they are programmed to deploy in response to the first known supercategory of such term.

In that way, interoperability CAN always be expected at the level of [Terms](#terms).

### Extending the vocabulary

Systems MAY specify the vocabulary used to express data being exchanged. The value indicating this version of this vocabulary is `priv.1.0`.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `vocab` | 0-1 | The name of the vocabulary used to describe data. In absence of indication `priv.1.0` is assumed. |

When [addition additional terms](#extending-terms) is not sufficient, and additional Concepts or Properties are needed, it is possible to extend the vocabulary.

This vocabulary is extended by defining a new identifier for the new vocabulary.
New vocabularies MAY include other vocabularies as long as their sets of concepts, properties and terms are disjoint.  

## Examples

A [JSON schema of the PRIV](./priv.schema.json) is provided for convenience. To illustrate a request, let us take the example of a data subject wanting to know if a an Organization (and any of its partners if applicable) have any data on them, and if so, have their contact data deleted.

This request can be represented with the following json data:
```
{
  "$schema":"https://blindnet.io/schemas/priv.schema.json",
  "request-id": "8f9066c6-1c6c-42a0-9993-e88c98d0e84d",
  "date": "2022-06-02T14:40:39+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "demands":[{
    "demand-id":"496294eb-5293-47dd-aaf8-494a0cb09134",
    "action":"TRANSPARENCY.KNOWN"
  },{
    "demand-id":"86bbb28a-eee6-45e6-81d6-7101de32374b",
    "action":"DELETE",
    "restrictions":[{
      "data-categories":["CONTACT"]
    }]
  }],
  "target":"PARTNERS"

}

```
In [here](./examples.md) we provide an overview of various Privacy Requests that a Data Subject might want to formulate according to [supported legislation](#supported-legislation) and we give indications on how each of those can be modeled with the Privacy Request Interchange Vocabulary.

## Design Implications for Systems Implementing PRIV

### Remembering Transfers

When data about Data Subjects is transmitted from one system to another, in order to be able to process the [Targets property](#targets), and in order to reply to `TRANSPARENCY.WHO` and `TRANSPARENCY.PROVENANCE` demands, Systems MUST keep track of:
- System of destination/origin and addresses where their APIs can be reached
- Categories of data being transferred
- Identifiers (`data-capture-id`s,`fragment-id`s) associated to the data being transferred
- Consents (`consent-id`) associated to the data being transferred
- Data Subject Identities (`dsid`,`dsid-schema`) pairs associated to the data being transferred

> **Note**
>
> Systems that exchange Data Subject information with other Systems MUST:
> - expose an API for communicating with other systems about Privacy Requests:
>     - receiving Privacy Requests from those other Systems,
>     - receiving Privacy Request Responses from other Systems in the case of [Nested Responses Scenario](https://github.com/blindnet-io/product-management/tree/devkit-schemas/refs/high-level-architecture#different-rights-request-response-scenrarios).

### Storing General Information

In order to automatically respond to `TRANSPARENCY` demands, Systems should store general information about:
- Countries where data servers are located (`TRANSPARENCY.WHERE`)
- The identity of the Organization controlling them, and the Organization's representative(s) (`TRANSPARENCY.WHO`)
- The categories of Data Consumers, and access policies (`TRANSPARENCY.WHO`)
- Identity and contact of a Data Protection Officer (`TRANSPARENCY.DPO`)
- A link to their Privacy Policy (`TRANSPARENCY.POLICY`)
> **Note**
>
> To be compliant with GDPR.{13,14,15} and use this schema, the Systems MUST ensure to include the following information in their Privacy Policy:
> - the existence of the right to request from the controller access to and rectification or erasure of personal data or restriction of processing concerning the data subject or to object to processing as well as the right to data portability
> - where the processing is based on point (a) of Article 6(1) or point (a) of Article 9(2), the existence of the right to withdraw consent at any time, without affecting the lawfulness of processing based on consent before its withdrawal
> - the right to lodge a complaint with a supervisory authority;
> - whether the provision of personal data is a statutory or contractual requirement, or a requirement necessary to enter into a contract, as well as whether the data subject is obliged to provide the personal data and of the possible consequences of failure to provide such data
> - the existence of automated decision-making, including profiling, referred to in Article 22(1) and (4) and, at least in those cases, meaningful information about the logic involved, as well as the significance and the envisaged consequences of such processing for the data subject.
> - Where personal data are transferred to a third country or to an international Organization, the data subject shall have the right to be informed of the appropriate safeguards pursuant to Article 46 relating to the transfer.

### Storing Capture-related Information

In order to automatically respond to data-specific demands, Systems should store particular information about every Data Capture (and make sure to implement ways of configuring how this information is applied to Data Captures):
- Legal Basis for processing particular data - can be different per Data Capture Fragment (`TRANSPARENCY.LEGAL-BASES`, but also for automatically evaluating the legality of keeping data upon `REVOKE-CONSENT`, `OBJECT`, `RESTRICT`, `DELETE` requests)
- Purposes of data processing - can be different per Data Capture Fragment (`TRANSPARENCY.PURPOSES`, but also for automatically evaluating  `OBJECT` and `RESTRICT` requests related to particular Purposes)
- Duration of mandatory data keeping, as well as period after which the data is automatically deleted - Can be different per Data Capture Fragment, and relative to en event such as Data Capture, End of Contract, Account Deletion (`TRANSPARENCY.RETENTION`, but also for automatically evaluating the legality of keeping data at a certain time and upon `REVOKE-CONSENT`, `OBJECT`, `RESTRICT`, `DELETE` requests)
- Data Categories - can be different per Data Capture Fragment (`TRANSPARENCY.DATA-CATEGORIES`)
- Data Processing Categories - can be different per Data Capture Fragment (`TRANSPARENCY.PROCESSING-CATEGORIES`)
- Purposes of Data Processing  - can be different per Data Capture Fragment (`TRANSPARENCY.PURPOSE`)

>**Note**
>
> To automatically calculate legality of keeping a particular data, Systems MUST track events such as Data Capture, End of Contract / Account Deletion

### Exposing Privacy Request API

The Systems that implementing the Privacy Request Interchange Vocabulary SHOULD expose an API to:
- Receive Privacy Requests from other Systems and acknowledge their reception
- Receive Privacy Request Responses from other Systems and acknowledge their reception

A System MAY be made only to collect Privacy Requests and send them to other Systems implementing the above-mentioned APIs.

It SHOULD be possible for systems to expose Privacy Request APIs in such a way that browsers can detect them while a Data Subject is on their website. The browser SHOULD be able to make (at least a simple `TRANSPARENCY.KNOW` or `TRANSPARENCY.POLICY`) requests and get instant answers to show to the user.


### Compliance History

Systems SHOULD keep a log of received [Privacy Requests](#privacy-request), generated [responses](#privacy-request-response), and as much as possible proofs of response delivery and visualization.


## Questions and Discussion Topics

### Use UUID for identifying Data Subjects

We could imagine an alternative design, where we would force systems to use an [UUID]([uuid](https://en.wikipedia.org/wiki/Universally_unique_identifier)) (according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html)), to identify the users. That would require us to provide some way for systems to match UUIDs with their local IDs (usernames, or e-mails), and would potentially limit the ability of 3rd party systems to interpret Privacy Request made at another system. This goal of proposed design is to allow for flexibility. However it is a very important aspect of the proposal, that deserves further debate.

### Zero-knowledge proof Data Subject authentication

PRIV MUST be agnostic of the authentication method, and as such MUST be compatible with Zero-knowledge proof authentication, biometric methods, password-based authentication and any other method. We should check whether this is the case with the current design.

### Mandatory properties and value constrains

Should we include restrictions in the schema according to the [JSON-schema-validation vocabulary](https://datatracker.ietf.org/doc/html/draft-bhutton-json-schema-validation-00#page-4) in order to make certain properties mandatory and ensure to limit string values to the values we support?

In the current proposal, this is the case for target, but not for request types, data categories, and user identity schemas. We might want to include more forma constraints there, or deliberately leave flexibility. This is a discussion we need to have.

### Dot-notation for Terms

Hierarchies of categories are represented using the "supercategory.subcategory" notation. The idea behind this is to allow developers to use the level of granularity that is adapted to them, yet be able to easily situate the subcategory in supercategory when dealing with more generic requests.

E.g. We have a data capture associated to "CONTACT.ADDRESS" data category. The Data Subject makes a DELETE request related to all of their data falling under "CONTACT" data category. The developer can easily identify "CONTACT.ADDRESS" as being a subcategory of ""CONTACT.ADDRESS" (either in SQL or in jquery).

The advantages are:
- It is human-readable
- It is easy to filter and get what you need

The disadvantages:
- Takes a lot of bites to store (as it is text) and the search operations in it a string operations (also taking time). Those disadvantages can be easily managed on the level of the storage used for the data, and do not have to be managed on the level of this interoperability format,
- this notation (although intuitive) is to the best of my knowledge, non-standard.

Maybe there are reasons for it (although similar notations are used for packages in programming languages, which are also hierarchical structures).

*Is there a standard (better) notation we can adopt?*

A candidate for a standard notation is the [URN](https://datatracker.ietf.org/doc/html/rfc8141). It is - less pretty (still human-readable), + standard, = equally searchable, = equally bad for storage and time. However we would still need to specify our own notation of the part of the URN that we want to customise. So the advantages are limited (if any).

Disadvantage: using a non-standard notation we expose ourselves to unpredictable risks.

### Schema elegance and modularity

We need a way to make enums different categories and types more elegant, and reusable in the perspective of using them to also represent Data Captures, Consents and responses to Privacy Requests.

### Addressability of System Endpoints

Is there a standard way for representing peer-to-peer System's API endpoints (compatible with our [implications for systems](#exposing-privacy-request-api)) that we can reuse here for representing systems?

### Anonymous Privacy Requests

In the current design, a Privacy Request must have at least one Data Subject Identity associated to it. However it might be useful to allow change the Expected cardinality from `1-*` to `0-*` so that a request can be made about general practices (`TRANSPARENCY`) without reference to any user.

This would make sense if the Systems would be responsible for finding a way to respond to such, unidentified user.

### General vs Specific Interpretation of `TRANSPARENCY` Privacy Requests

A Data Subject can formulate a request to know about processing generally practiced by the System, or to know about processing being done on Data Subejct's particular data. Those can be different. Yet we have only one category 'TRANSPARENCY.PROCESSING-CATEGORIES'. Same goes for other `TRANSPARENCY` requests.

Currently we don't offer any way to distinguish between those two kinds of demands. We offer instructions for Systems, under [Expected Behavior](expected-behavior.md), on how to interpret them based on context (whether the request is made during capture, or prior to capture where request scope SHOULD be interpreted as general, or in some other context where the request scope SHOULD be interpreted as related to user's particular data).

This design choice MAY be a bad idea.

### Inform-as-you-capture

To better explain Inform-as-you-capture, we introduce to the concept of a theoretical superprivate System, in which the Data Subject's ability of control is absolute.

This absolute control involves also the ability to acquire absolute transparency about future processing at the time of capture.

As the user provides the data to the superprivate system, the system is able to dynamically show, for each field (Data Capture Fragment) the intended usage (including purposes and categories of processing, duration of retention, legal grounds and other privacy-related parameters). As they enter data, the Data Subject, if they wish so, is able to dynamically restrict this intended usage and impose their own terms.

A consent scope (including purposes and categories of processing, duration of retention etc.) can be dynamically defined and negotiated with the Data Subject at the time of Data Capture. Instead of a predefined consent, the Data Subject is offered to give a personalised consent.

The superprivate system can dynamically inform the Data Subject of consequences of certain consent restrictions (such as inability to provide certain functionalities).

To achieve this ability, the superprivate system uses a data structure describing all the data fields (Data Capture Fragments) and to them associated:
- objective information (data categories; legal bases),
- general intentions (default values of: categories of processing, retention, purposes)
- minimal viable consent settings allowing the System to offer certain functionalities.

After negotiation with the Data Subject during Data Capture, the superprivate System applies metadata to the Data Capture to indicate concrete consents and limitations that it wants to respect in run-time of data processing.

Even if a less than superprivate System does not want to dynamically negotiate consent, it can still benefit from this data structure in order to show (fragment by fragment) the policies in place. The information obligation during capture (as defined by GDPR.13 and GDPR.14) is currently mostly achieved by Privacy Policies (that nobody ever reads). The inform-as-you-capture paradigm works as tooltip (or equivalent interface element), more adapted to the actual demonstration of transparency.

### A Way for Systems to Sign Responses

Should we include a way for systems to sign responses and allow to confirm their authenticity. Maybe it can be a set of optional variables for signatures and keys in the [Privacy Request Response](#privacy-request-response)) so that they can be easily nested as they only sign the body of the response? Or is there (certainly is, but should we use it) some standard way to handle this separately from the format of the requests and responses?

### Expect Language

Should we implement the Accept-Language logic from HTTP? Or can we assume that the 'lang' of request is the language in which the response is expected?


### Extending the vocabulary

Is the mechanism for extending the vocabulary appropriate?

### Format and encryption of the `data` values

We need a way for Systems to encrypt the data (that compatible also with encryption libraries other then our own).

### Motivation or explanation of Demand

When a Demand is motivated by a `message`, then it can't be processed automatically.
To the best of our knowledge, motivating a Demand is optional under [supported legislation](#supported-legislation).
The `message` is thus optional.

If PRIV is ever to support a legislation under which a message might be mandatory, this design SHOULD be reconsidered.

## Alternatives

### Ethyca

Ethyca has their (also open-soruce) [FIDES language](https://ethyca.github.io/fideslang/). Their language is less modular. Data provenance and data category are mixed together, which means that terms are long, and each has quite particular, complicated meaning.

We aim here for a simpler way to express requests and rights, and for a more automated Privacy Request resolution algebra.

Their support for purposes, and per-purpose consents is limited.

Yet, we want to be compatible with them.

We examine, in [examples.md](./examples.md#ethyca-data-categories) how users of Ethyca can map their matadata PRIV terms.

### ISO 19944

There is an ISO standard for data categories and processing categories. They are mostly very broad, many overlap, and they are of almost no use for resolving Privacy Requests in the context of GDPR.

However, we might want to allow developers to use our format (properties and concepts) with ISO 19944 categories instead of our terms.

### HL7 Standards

The [HL7 Version 3 Standard: Role-based Access Control Healthcare Permission Catalog](http://www.hl7.org/documentcenter/private/standards/v3/V3_HACC_R3_2016_R2021.pdf) offers terms for describing a variety of:
- Operations: OPERATE, CREATE, READ, UPDATE, APPEND, ANNOTATE, DELETE, PURGE, EXECUTE, REPRODUCE, COPY, BACKUP, RESTORE, EXPORT, PRINT, DERIVE, CONVERT, EXCERPT, TRANSLATE, MOVE, ARCHIVE, REPLACE, FORWARD, TRANSFER, SIGN, VERIFY, NOTARIZE, ALARM
- Permissions (associating those Processing Categories with different types of information objects.)

Users of this standard SHOULD be able to easily associate those Operations with PRIV Processing Categories, and treat them as subcategories according to the DOT NOTATION.

### HIPAA Identifiers

[HIPPA](https://www.hhs.gov/hipaa) regulation introduces 18 categories of Protected Health Information:
Name, Address (all geographic subdivisions smaller than state, including street address, city county, and zip code), All elements (except years) of dates related to an individual (including birthdate, admission date, discharge date, date of death, and exact age if over 89), Telephone numbers, Fax number, Email address, Social Security Number, Medical record number, Health plan beneficiary number, Account number, Certificate or license number, Vehicle identifiers and serial numbers, including license plate numbers, Device identifiers and serial numbers, Web URL, Internet, Protocol (IP) Address, Finger or voice print, Photographic image - Photographic images are not limited to images of the face, Any other characteristic that could uniquely identify the individual.

We examine, in [examples.md](./examples.md#hippa) how those categories can be mapped to PRIV's Data Categories.




## See also

This document comes with the following support documents:
- [Examples of use](./examples.md)
- [Expected Behavior of Implementing Systems](./expected-behavior.md)
- [Scenarios](./scenarios.md)

## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.
- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,
- **[RFC5234]**  Crocker, D., Ed. and P. Overell, ["Augmented BNF for Syntax Specifications: ABNF"](https://www.rfc-editor.org/info/rfc5234), STD 68, RFC 5234, DOI 10.17487/RFC5234, January 2008,



### Initiative with which PRIV seeks to be compatible

- [Privacy Model for the Web](https://github.com/michaelkleber/privacy-model/blob/main/README.md)
- [First Party Sets](https://github.com/privacycg/first-party-sets)


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legislation

- CPRA
- HIPPA
