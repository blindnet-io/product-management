# Privacy Request Interchange Vocabulary (PRIV)

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [659](https://github.com/blindnet-io/product-management/pull/659)                      |
| **Author(s)** | [milstan](https://github.com/milstan) (milstan@blindnet.io)                                                          |
| **Updated**   | 2022-06-07                                                                             |



## Introduction

We propose a simple vocabulary for representing [Privacy Requests](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization#data-capture--rights-requests).

The vocabulary introduces a finite set of `concepts`, `properties` and `terms`. `Concepts` define the objects of exchange, `properties` define their characteristics, and `terms` define commonly understood values of properties.

This vocabulary corresponds to the [Schemas](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#schemas) component of the [High-Level Architecture](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture).

Two additional documents: [Examples of use](./examples.md) and [Expected Behavior of Implementing Systems](./expected-behavior.md), complement this document.


## Motivation

An individual is in connection with software Systems (and Organisations operating them) that process the individual's data.
In order to [regulate the relationship](https://github.com/blindnet-io/product-management/blob/main/refs/notion-of-privacy/notion-of-privacy.md) with those Systems (and Organisations), the individual makes requests related to their privacy.

With a Privacy Request the individual aims to gain a degree of transparency about data processing and a degree of control over the data and over the data processing. Allowing individuals to make Privacy Requests is becoming more and more a legal obligation.

Different Systems, and different components of a single System, including different components of blindnet devkit are likely to exchange information about Privacy Requests. Therefore, a common format is needed to facilitate exchange of information without loss of semantics. The goal of Privacy Request Interchange Vocabulary is to establish a shared conceptualisation and format of Privacy Request so that their processing can be, as much as possible, automatised by the Systems.


## Terminology

>**TO BE Updated** once Lexicon and High Level Conceptualization are synchronised

- We use the term Privacy Request interchangeably with the (deprecated) terms Rights Request and Data Rights Request as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Individual, Person, You, and Data Subject as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv)
- We use the term System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)
- We use the terms Organization, Submitter, Data Consumer as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv) as defined there.

## Version

This document defines the version `1.0` of the Privacy Request Interchange Vocabulary.

## Design Considerations

### Design Inspiration

- **Smart data structures and dumb code works a lot better than the other way around.** lesson No 9 from Raymond, Eric Steven. ["The Cathedral and the Bazaar"](https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar). We want PRIF to embody a smart way of thinking about privacy, solving common challenges through the data structure itself.

- **Often, the most striking and innovative solutions come from realizing that your concept of the problem was wrong.** lesson No 12 from Raymond, Eric Steven. ["The Cathedral and the Bazaar"](https://en.wikipedia.org/wiki/The_Cathedral_and_the_Bazaar). We indeed now have novel understanding of the [problem of Privacy in Software Systems](https://github.com/blindnet-io/product-management/blob/main/refs/notion-of-privacy/notion-of-privacy.md).

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
- Decentralised design compatible with both the Internet's Client-Server Architecture and Metaverse/Web3 Architecture

### Design Choices

We have made the following choices:
- **Language Independence**. The Privacy Request Interchange Vocabulary is independent from any programming language, or any format or language for expressing structured data, and can be materialised in different forms such as json, xml, or other. A [json schema](PRIV.schema.json) is provided for convenience.

- **Rich Semantics**. The Privacy Request Interchange Vocabulary includes `terms` - reserved words to describe common types of Privacy Requests, categories of data, categories of data processing and other key notions. This choice is made to facilitate their uniform interpretation by the implementing systems. Their [human-readable titles and descriptions](dictionary) are provided in json format for convenience.

- **Multiple User Identities**. The Privacy Request Interchange Vocabulary  allows for a Data Subject to be identified using more than one user identity. This choice is made to enable the Privacy Request to be easily exchanged across Systems that use different user identifiers.

- **Systems resolve Privacy Requests**. The Privacy Requests are interpreted at the level of a particular System. If an Organisation operates several Systems, and if the Data Subject wants to have the Privacy Request transmitted to all of them, each System may respond differently. While a Privacy Request can target a group of Systems, the most atomic target of a Privacy Request is thus the System exposing an API for Privacy Requests, and it is only at this level that a Privacy Request can be resolved.

- **Decentralised IDs**. The Privacy Request Interchange Vocabulary uses decentralised ways to uniquely identify Data Subjects, Systems, Requests and their elements. The exchange of Privacy Requests can happen without a centralised entity to control identity disambiguation.

## Proposal

The Privacy Request Interchange Vocabulary includes the following:
- Key Concepts: [Consent](#consent), [Data Capture](#data-capture), [Data Capture Fragment](#data-capture-fragments), [Demand](#demands), [Privacy Request](#privacy-request), [Privacy Scope](#privacy-scope)
- Properties: **TBD** full list of properties
- Terms: **TBD** full list of terms

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
| `action` | 1 | Unique value. One of {`ACCESS`, `DELETE`, `MODIFY`, `OBJECT`, `PORTABILITY`, `RESTRICT`, `REVOKE-CONSENT`, `TRANSPARENCY`, `TRANSPARENCY.DATA-CATEGORIES`, `TRANSPARENCY.DPO`, `TRANSPARENCY.KNOWN`, `TRANSPARENCY.LEGAL-BASES`, `TRANSPARENCY.ORGANISATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.PROCESSING-CATEGORIES`, `TRANSPARENCY.PROVENANCE`, `TRANSPARENCY.PURPOSE`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO`, `OTHER-DEMAND`} |
| `message` | 0-1 | Optional string comment, motivation or explanation of Demand |
| `lang` | 0-1 | Optional string Language of textual message associated with demands in the format of [FRC5646](https://datatracker.ietf.org/doc/rfc5646/) |
| `data` | 0-* | Optionally concrete data (Format **TBD**) |


The key element that defines the nature of the Demand is the `action`. A Demand MUST have one and only one `action`.

Actions are hierarchical.
Their relationships are denoted with a dot "." separating two actions, the more general one being written on the left.
`TRANSPARENCY` includes `TRANSPARENCY.WHERE`.
When `TRANSPARENCY` is demanded, Systems MUST interpret the demand as if all the subcategories of `TRANSPARENCY` were demanded.

Certain Demands MAY include data, such as a `MODIFY` Demand where new data MAY be provided by the Data Subject.

##### Demand Restrictions

The `action` that the Data Subject requests with a particular Demand MUST be interpreted in the context of restrictions.
A Demand MAY refer to only certain Privacy Scope (categories of data, certain types of processing, certain purposes of processing) or may only refer to particular Consents (e.g. those that the Data Subject wants to revoke) or to particular Data Captures (e.g. those that the Data Subject want to delete).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `restrictions` |  0-* | An optional array of restriction objects, each being one of [Privacy Scope](#privacy-scope), [Consent Restriction](#consent-restriction), [Capture Restriction](#capture-restriction), [Data Range](#data-range)|

When more than one restriction is specified, the System MUST interpret the Demand as referring to the intersection of restrictions. For example let us consider a `DELETE` demand having two restrictions: `LOCATION` `data-category` as Privacy Scope, and from 11th to 15th of June 2022 as Data Range. The System SHOULD understand that the Data Subject wants the System to delete only their location data processed in this precise period.

A demand with multiple restrictions MUST NOT have more than one restriction of the same type.

###### Privacy Scope

A Privacy Scope MAY be defined by three dimensions: Data Categories, Categories of Processing, and Purposes of Processing.
A Data Subject can formulate a Demand or give Consent within a particular Privacy Scope, e.g. only referring to `COLLECTING` (Category of Processing) `CONTACT` data (Category of Data) for `PERSONALISATION` (Purpose of Processing).

Privacy Scope can be understood as a vector space defined by those three dimensions.

```

Privacy Scope = (Data Categories) x (Categories of Processing) x (Purposes of Processing)

```

*Data Categories*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-categories` |  0-* | `AFFILIATION`, `AFFILIATION.MEMBERSHIP`, `AFFILIATION.SCHOOL`, `AFFILIATION.WORKPLACE`, `BEHAVIOR`, `BEHAVIOR.ACTIVITY`,  `BEHAVIOR.CONNECTION`, `BEHAVIOR.PREFERENCE`, `BEHAVIOR.TELEMETRY`, `BIOMETRIC`, `CONTACT`, `CONTACT.EMAIL`, `CONTACT.ADDRESS`, `CONTACT.PHONE`, `DEMOGRAPHIC`, `DEMOGRAPHIC.AGE`, `DEMOGRAPHIC.BELIEFS`, `DEMOGRAPHIC.GENDER`, `DEMOGRAPHIC.ORIGIN`, `DEMOGRAPHIC.RACE`, `DEMOGRAPHIC.SEXUAL-ORIENTATION`, `DEVICE`, `FINANCIAL`, `FINANCIAL.BANK-ACCOUNT`, `GENETIC`, `HEALTH`, `IMAGE`, `LOCATION`, `NAME`, `PROFILING`, `RELATIONSHIPS`, `UID`, UID.USER-ACCOUNT , UID.SOCIAL-MEDIA , `OTHER-DATA` or any [Data Capture Fragment](#data-capture-fragments) `selector`s within those categories |

When several values are given, Systems MUST interpret the `data-category` dimension as a union of all the categories indicated.

Categories are organised as a hierarchy, denoted with a dot ".", the more general category being written on the left.
E.g. the following two `data-category` restrictions are equivalent:
- `CONTACT`,`CONTACT.EMAIL`
- `CONTACT`

In the absence of indication of any `data-category` dimension, Systems MUST interpret the Privacy Scope as being related to all categories of data.
[A list of eligible `data-category` values with corresponding user-facing descriptions is provided](dictionary/data-categories/) for convenience.

*Categories of Processing*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `processing-categories` | 0-* | One of {`ANONYMIZATION`, `AUTOMATED-INFERENCE`, `AUTOMATED-DECISION-MAKING`, `COLLECTION`, `GENERATING`, `PUBLISHING`, `STORING`, `SHARING`, `USING`, `OTHER-PROCESSING`} |

When several values are given, Systems MUST interpret the `processing-categories` dimension as a union of all the processing categories indicated.

In the absence of indication of any `processing-categories` dimension, Systems MUST interpret the Demand as being related to all and any `processing-categories` of treatment.

[A list of eligible `processing-categories` values with corresponding user-facing descriptions is provided](dictionary/purposes) for convenience.

*Purposes of Processing*

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `purposes` | 0-* | `ADVERTISING`, `COMPLIANCE`, `EMPLOYMENT`, `JUSTICE`, `MARKETING`, `MEDICAL`, `PERSONALISATION`, `PUBLIC-INTERESTS`, `RESEARCH`, `SALE`, `SECURITY`, `SERVICES`, `SERVICES.ADDITIONAL-SERVICES`, `SERVICES.BASIC-SERVICE`, `SOCIAL-PROTECTION`, `TRACKING`, `VITAL-INTERESTS`, `OTHER-PURPOSE` |

When several values are given, Systems MUST interpret the `purposes` restriction as a union of all the purposes indicated.

Purposes are organised as a hierarchy, denoted with a dot ".", the more general purpose being written on the left. E.g. the following two `pruposes` restrictions are equivalent:
- `SERVICES`,`SERVICES.BASIC-SERVICE`
- `SERVICES`

In the absence of indication of any `purpose` restriction, Systems MUST interpret the Demand as being related to all and any purpose of treatment.

[A list of eligible `purposes` values with corresponding user-facing descriptions is provided](./dictionary/purposes/) for convenience.

###### Consent Restriction

A Demand can be restricted to particular Consent ID(s). For example, a Data Subject revokes a particular consent only (the one related to his data being shared with 3rd parties) but maintains other consents they may have given.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `consent-ids` | 0-* | Optional array of consent ids to indicate that the Demand (e.g. a `REVOKE-CONSENT` Demand) is restricted to particular consents. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `consent-ids` are indicated, Systems MUST interpret the Demand as related to all Consents related to indicated `consent-ids`.

###### Capture Restriction

A Demand can be restricted to particular Capture ID(s). For example, a Data Subject to delete a particular data, they indicate the data capture concerned by their Demand.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `capture-ids` | 0-* | Optional array of Data Capture IDs to indicate that the Demand (e.g. a `DELETE` Demand) is restricted to data captured within particular Data Captures. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `capture-ids` are indicated, Systems MUST interpret the demand all related to all the data captured as part of those Data Captures.

###### Data Range

A Demand can be restricted to particular Data Range, for example the Data Subject may `OBJECT` to data collection in a particular time period, or they might want to `DELETE` only data collected at certain dates.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `from` | 0-* | Date and Time when the Data Range starts in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `to` | 0-* | Date and Time when the Data Range ends in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |


A Data Range defined by only one of the {`from`, `to`} properties indicates a period of time after or before a certain date, unbounded on the other end.

###### Provenance Restriction

A Demand can be restricted to particular `provenance-category`, for example the Data Subject may `OBJECT` to data that is `DERIVED` about them being shared (`processing-category`:`SHARING`), or they may want to `RESTRICT` the `SHARING` of their data only to the data that came from themselves `USER`.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `provenance-category` | 1 | one of {`DERIVED`, `TRANSFERRED`, `USER`, `USER.DATA-SUBJECT`} |
| `target` | 0-1 | Optionally one of {`ORGANISATION`, `PARTNERS`, `SYSTEM`}. In absence of indication `SYSTEM` is assumed |

Optionally the Provenance Restriction may also include a particular [Target](#targets). E.g. the Data Subject might demand to have `ACCESS` to data that was `TRANSFERRED` by partner Systems (`target`:`PARTNERS`).

#### Targets

It is common for Internet Systems to be distributed (organised in a set of connected websites and applications) and to exchange data among themselves.

It is therefore convenient for a Data Subject to be able to formulate Privacy Requests (but also give Consents) targeting well-defined Systems.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `target` | 0-1 | Optionally one of {`ORGANISATION`, `PARTNERS`, `PARTNERS.DOWNWARD`, `PARTNERS.UPWARD`, `SYSTEM`}. In absence of indication `SYSTEM` is assumed |

`SYSTEM` refers to the particular System with witch the Data Subject is in direct interaction while making the Privacy Request (or giving the Consent).

`ORGANISATION` includes, in addition to the `SYSTEM`, all other Systems belonging to the same Organisation. Those are understood as being a part of the same First-Party Set (**TODO** ref and compatibility check)  

`PARTNERS.DOWNWARD` includes, in addition to the `SYSTEM`, all other Systems belonging to Organisations with which the data about the Data Subject has been shared.

`PARTNERS.UPWARD` includes, in addition to the `SYSTEM`, all other Systems belonging to Organisations from which the data about the Data Subject has been obtained.

`PARTNERS` includes, in addition to the `SYSTEM`, all other Systems belonging to Organisations with which any sort of exchange of data concerning the Data Subject has been performed.

Different values of the `target` Property imply different obligations for the System receiving a Privacy Request to transfer that request to other Systems.

Let us imagine the following situation: System A gave information about the Data Subject to System B, and System B gave information about the Data Subject to System C. The same Organisation that operates System B, also operates System D.

When System B receives a Privacy Request having `target` value:
- `SYSTEM`, it SHOULD NOT transfer it to any other system.
- `ORGANISATION` for a `target`, it MUST transfer it to all other systems operated by the same Organisation (System D in our example).
- `PARTNERS.DOWNWARD` it MUST also send it to all systems to which it transferred data about the Data Subject (System C).
- `PARTNERS.UPWARD` it MUST also send it to all systems from which it obtained data about the Data Subject (System A).
- `PARTNERS`, it MUST also send it to all systems from which it obtained data about the Data Subject or to which it gave information about the Data Subject (System A and System C).

Systems should interpret the target of Privacy Request the same way regardless of the Privacy Request being received directly from the Data Subject or from a corresponding System.

Convenient tables of `target` values and corresponding user-facing descriptions, in different languages, are provided [here](dictionary/targets).

### Privacy Request Response

Systems SHOULD respond to [Privacy Requests](#privacy-request).
Regardless of the [scenario (Responding to the Data Subject directly or to the System)](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#different-rights-request-response-scenrarios) that should be defined by a protocol (**TO BE WRITTEN** - the System SHOULD know when to wait for a response from another system), Systems SHOULD generate a response using the Privacy Request Interchange Vocabulary.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `response-id` | 1 | Unique ID for referring to this request in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `in-response-to` | 1 | `request-id` of the Privacy Request to which response is made or `demand-id` of the particular Demand to which response is made, in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | 1 | Date and Time when Privacy Request Response was created in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `by` | 1 | **TBD ID of the System having generated the response** |
| `requested-action` | 0-1 | Optional information about the action that was demanded, and to which the response is made. One of {`ACCESS`, `DELETE`, `MODIFY`, `OBJECT`, `PORTABILITY`, `RESTRICT`, `REVOKE-CONSENT`, `TRANSPARENCY`, `TRANSPARENCY.DATA-CATEGORIES`, `TRANSPARENCY.DPO`, `TRANSPARENCY.KNOWN`, `TRANSPARENCY.LEGAL-BASES`, `TRANSPARENCY.ORGANISATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.PROCESSING-CATEGORIES`, `TRANSPARENCY.PROVENANCE`, `TRANSPARENCY.PURPOSE`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO`, `OTHER-DEMAND`} |
| `data-subject` |  0-* | Optional indication of the [Data Subject Identities](#decentralized-identity-of-data-subjects) to which the response refers to |
| `status` | 1 | One of {`GRANTED`, `DENIED`, `PARTIALLY-GRANTED`, `UNDER-REVIEW`} |
| `motive` | 0-* | Optionally one of {`IDENTITY-UNCONFIRMED`, `LANGUAGE-UNSUPPORTED`, `VALID-REASONS`, `IMPOSSIBLE`, `NO-SUCH-DATA`, `REQUEST-UNSUPPORTED`, `USER-UNKNOWN`} |
| `answers` | 0-* | Any of the terms the meaning of which is defined by the present vocabulary |
| `message` | 0-1 | Optional string comment, motivation or explanation of Demand |
| `lang` | 0-1 | Optional string Language of textual message associated with demands in the format of [FRC5646](https://datatracker.ietf.org/doc/rfc5646/) |
| `includes` | 0-* | Optionally an array of one or more [Privacy Request Response](#privacy-request-response)s |
| `data` | 0-* | Optionally concrete data to which access is being given (Format **TBD**) |

A Privacy Request Response MUST have:
- a unique ID,
- a clear indication of the particular Privacy Request or the particular Demand to which its content refers,
- a date,
- a status.

Privacy Request Responses can be nested. One can imagine a Privacy Request Response to a particular Privacy Request, that `includes` Privacy Request Responses to the particular Demands made in that Privacy Request. Several Systems MAY respond to the same Privacy Request or Demand, and one System MAY nest them in order to gather them and send them back to the Data Subject.

When a Demand is being denied, the Privacy Request Response MUST provide a `motive`.

>To illustrate the `answers` value, we can imagine a `TRANSPARENCY.DATA-CATEGORIES` Demand, to which a response may include `answers`: `CONTACT`, `IMAGE`. Or a `TRANSPARENCY.KNOWN` Demand to which the answer may include `answers`: `YES`.

### Consent

A Consent is given by one Data Subject which can be identified by one or more [Data Subject Identities](#decentralized-identity-of-data-subjects).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-subject` |  1-* | [Data Subject Identities](#decentralized-identity-of-data-subjects) each containing one `dsid` and one `dsid-schema`|
| `consent-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | 1 | Date and Time when Consent was given in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `expires` | 0-1 | Date and Time when Consent expires in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `target` | 0-1 | Optionally one of {`ORGANISATION`, `PARTNERS`, `SYSTEM`} to indicate the category of Systems to which consent for processing is given. In absence of indication `SYSTEM` is assumed. |
| `scope` |  0-1 | a [Privacy Scope](#privacy-scope) in absence of which the Consent SHOULD be interpreted as unlimited |
| `replaces` |  0-* | Optionally one or more 'consent-id's of previous consents that have became void when this consent was made |
| `replaced-by` |  0-* | Optionally one or more 'consent-id's of previous consents that have became void when this consent was made |

### Data Capture

A Data Capture is given by one Data Subject which can be identified by one or more [Data Subject Identities](#decentralized-identity-of-data-subjects).

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-subject` |  1-* | [Data Subject Identities](#decentralized-identity-of-data-subjects) each containing one `dsid` and one `dsid-schema`|
| `capture-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `target` | 0-1 | Optionally one of {`ORGANISATION`, `PARTNERS`, `SYSTEM`}. In absence of indication `SYSTEM` is assumed |
| `fragments` | 1-* | One or more [Data Capture Fragments](#data-capture-fragments) |

A Data Capture concerns one and only one Data Subject who MAY be identified by multiple Data Subject Identities.

#### Data Capture Fragments

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `fragment-id` | 1 | a string in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `selector` | 1 | a string used to uniquely identify a data field (in the System's data model) to which the fragment corresponds |
| `date` | 1 | Date and Time when data was Captured was given in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `scope` |  0-1 | a [Privacy Scope](#privacy-scope) in absence of which the fragment SHOULD be interpreted as unlimited |
| `target` | 0-1 | Optionally one of {`ORGANISATION`, `PARTNERS`, `SYSTEM`}. In absence of indication `SYSTEM` is assumed |
| `retention` | 1-* | one or more [Retention Policies](#retention-policy) |
| `provenance` | 1-* | one or more [Provenance](#provenance) |
| `data` | 0-* | Optionally concrete data (Format **TBD**) |
| `legal-base` | 0-* | Optionally an array of values among `CONTRACT`, `CONSENT`, `LEGITIMATE-INTEREST`, `NECESSARY`, `OTHER-LEGAL-BASE` |

`selector`s MUST include the data category of the data. For example selectors 'CONTACT.ADDRESS.SHIPPING' and 'CONTACT.ADDRESS.BILLING' indicate that the data being captured by a particular fragment belong to the `CONTACT.ADDRESS` data category.

While the Data Categories are global, the selectors are defined by the Systems. A `selector` uniquely identifies a particular data field that the Systems works with. When several Systems exchange data among them, they SHOULD align on using the same `selectors` in the same way, in order to be able to correctly interoperate.

Processing MAY be legitimate according to several legal bases for processing. For example, a Data Subject can give explicit `CONSENT` when creating an account with a particular online service, and at the time, the System providing some service to the Data Subject might need to process their data in order to deliver a service or honour a `CONTRACT` (e.g. deliver the purchased goods to the Data Subjects address and issue an invoice).

Certain processing is made legitimate (`LEGITIMATE-INTEREST`) or mandatory (`NECESSARY`) by law, e.g. [Article 6 og GDPR](https://gdpr-info.eu/art-6-gdpr/).

##### Provenance

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `provenance-category` | 1 | one of {`DERIVED`, `TRANSFERRED`, `USER`, `USER.DATA-SUBJECT`} |
| `system` | 1 | System ID (**Format TBD**) |

Data provenance is interpreted in relation to a particular System.
The same Data Capture Fragment might be data collected from the `USER` for one System that is in direct interaction with the Data Subject, and be data `TRANSFERRED` in the eyes of another System that obtained in through transfer from the user-facing System.

##### Retention Policy

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-category` | 1-* | Any of the any Data Category terms or concrete Data Capture Fragment `selector`s within those categories |
| `policy-type` | 1 | one of {NO-LONGER-THAN, "NO-LESS-THAN"} |
| `duration` | 1 | Duration in JSON Schema [duration](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `after` | 1 | Event to which the retention duration is relative to. One of {`CAPTURE-DATE`,`RELATIONSHIP-END`, `SERVICE-END`}

When several `data-category` values are given, they are interpreted as a union.

## Detailed Design

A separate document gives a list of [examples](examples.md) on how to represent real-life Privacy Requests, as defined in [supported legislation](#supported-legislation), or as modelled in existing systems with which we seek interoperability.

### JSON format

We provide a [JSON Schema document](./priv.schema.json) for machine-readable interpretation of Privacy Requests compliant with [v4 (or ideally lower) of IETF specification](https://datatracker.ietf.org/doc/html/draft-zyp-json-schema-04#:~:text=JSON%20Schema%20is%20a%20JSON,interaction%20control%20of%20JSON%20data.)

### Authenticated exchanges

Systems exchanging Privacy Requests MUST be able to do so in a way allowing them to very the integrity of their content, and the identity of the system having emitted the Privacy Request.

For this purposes Privacy Requests MAY be embedded as 'Claims' in [JWTs (RFC7519)](https://datatracker.ietf.org/doc/html/rfc7519).

### Decentralised Identity of Data Subjects

The Systems are only able to provide control to Data Subjects if they can identify them. On the other hand, there is no central authority to manage Data Subject identity globally.

Therefore, we use a set of attributes to uniquely identify one Data Subject. One and the same Data Subject can have multiple such identities.

#### Globally Unique Data Subject Identities

The identifiers used to refer to Data Subjects MUST be globally unique. One Data Subject identity corresponds to one Data Subject. One Data Subject can have several Data Subject Identity.

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

However, the authentication does not necessarily have to be performed during the collection of the Privacy Request. It can be done separately. The design of PRIV aims to support several authentication workflows, as many as possible authentication methods (i.e. be as much as possible agnostic from the authentication method).


#### Matching Multiple Data Subject Identities

Systems MAY keep track of Data Subject Identities that refer to the same Data Subject. In some cases, valid reasons MAY exist for Systems to ignore such information.

When Systems do know that one Data Subject Identity corresponds to the same user as another Data Subject Identity, then Systems SHOULD offer the Data Subject a possibility for their Privacy Requests, expressed in relation to one Data Subject Identity to be automatically extended to include other equivalent Data Subject Identities.

Systems SHOULD NOT imply Data Subject Identity equivalence from Privacy Requests, especially when granting Privacy Requests that require authentication.

### Data Capture IDs, Data Capture Fragment IDs, Consent IDs, Privacy Request IDs, Demand IDs, Privacy Request Response IDs are Globally Unique

All of the following identifiers `data-capture-id`, `fragment-id`, `consent-id`, `rights-request-id`, `demand-id`, `rights-response-id` MUST be globally unique and be generated according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) in order for the corresponding objects to be easily identifiable across systems.
The reason for using UUDIs is to allow Systems to independently generate globally unique identifiers while being autonomous from a central entity that would ensure identifier uniqueness.

Having a public ledger for UUDIs MAY be considered for Consents and Data Captures, but serious implications to Data Subject exposure MUST also be considered.
However, the design MUST be compatible with building a public decentralised ledger.

### Data Categories, Treatment Types, Actions, and Purposes SHOULD be Unambiguous and Complete

The lists of Data Categories, Treatment Types, Actions, and Purposes SHOULD be designed in such a way to be:
- **Unambiguous** : The developer using the schema knows without ambiguity which one (of which ones) to use in any given situation, AND
- **Complete** : They allow to express the totality of possible needs in the context of a user wanting to [regulate their privacy/connectedness](https://github.com/blindnet-io/product-management/blob/dogma/refs/notion-of-privacy/notion-of-privacy.md), as well as the totality of requests defined by the [supported legilsation](#supported-legilsation).

### Extending the vocabulary

Systems MAY specify the vocabulary used to express data being exchanged. The value indicating this version of this vocabulary is `priv.1.0`.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `vocab` | 0-1 | The name of the vocabulary used to describe data. In absence of indication `priv.1.0` is assumed. |

This vocabulary can be extended by defining a new identifier for the new vocabulary. New vocabularies MAY include other vocabularies as long as their sets of concepts, properties and terms are disjoint.  

In addition, the Systems implementing PRIV can simply define their own subcategories of terms (not properties not concepts) defined by PRIV. This might be useful for their own internal operation, however the interoperability with other system can only be expected at the level of the particular, shared, version of the vocabulary.

## Examples

A [JSON schema of the PRIV](./priv.schema.json) is provided for convenience. To illustrate a request, let us take the example of a data subject wanting to know if a an organisation (and any of its partners if applicable) have any data on them, and if so, have their contact data deleted.

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
In [here](./examples.md) we provide an overview of various Privacy Requests that a Data Subject might want to formulate according to [supported legislation](#supported-legislation) and we give indications on how each of those can be modelled with the Privacy Request Interchange Vocabulary.

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
- The identity of the organisation controlling them, and the Organization's representative(s) (`TRANSPARENCY.WHO`)
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
> - Where personal data are transferred to a third country or to an international organisation, the data subject shall have the right to be informed of the appropriate safeguards pursuant to Article 46 relating to the transfer.

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

Systems SHOULD keep a log of received [Privacy Requests](#privacy-request), generated [responses](#privacy-request-response), and as much as possible proofs of response delivery and visualisation.




## Questions and Discussion Topics

### Use UUID for identifying Data Subjects

We could imagine an alternative design, where we would force systems to use an [UUID]([uuid](https://en.wikipedia.org/wiki/Universally_unique_identifier)) (according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html)), to identify the users. That would require us to provide some way for systems to match UUIDs with their local IDs (usernames, or e-mails), and would potentially limit the ability of 3rd party systems to interpret Privacy Request made at another system. This goal of proposed design is to allow for flexibility. However it is a very important aspect of the proposal, that deserves further debate.

### Zero-knowledge proof Data Subject authentication

PRIV MUST be agnostic of the authentication method, and as such MUST be compatible with Zero-knowledge proof authentication, biometric methods, password-based authentication and any other method. We should check whether this is the case with the current design.

### Mandatory properties and value constrains

Should we include restrictions in the schema according to the [JSON-schema-validation vocabulary](https://datatracker.ietf.org/doc/html/draft-bhutton-json-schema-validation-00#page-4) in order to make certain properties mandatory and ensure to limit string values to the values we support?

In the current proposal, this is the case for target, but not for request types, data categories, and user identity schemas. We might want to include more forma constraints there, or deliberately leave flexibility. This is a discussion we need to have.

### Dot-notation for category hierarchies

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

Or if none (which would be surprising) we could define our syntax using [Backus-Naur Form](https://datatracker.ietf.org/doc/html/rfc4234). Advantage: geeks will love us.
We would need to ensure: that any string used on any side of any dot, it is not contained in any other string not containing a dot.
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

Currently we don't offer any way to distinguish between those two kinds of demands. We will offer instructions for Systems (under [Expected Behavior](expected-behavior.md) - **TO BE WRITTEN**) on how to interpret them based on context (whether the request is made during capture, or prior to capture where request scope SHOULD be interpreted as general, or in some other context where the request scope SHOULD be interpreted as related to user's particular data).

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
>**Note**
>
> The motivation or explanation of Demand is modelled by a message, and the message is optional. If law regulations state that motivation or explanation of Demand is mandatory, it is not supported.

## Alternatives

### Ethyca

Ethyca has their (also open-soruce) [FIDES language](https://ethyca.github.io/fideslang/). Their language is less modular. Data provenance and data category are mixed together, which means that terms are long, and each has quite particular, complicated meaning.

We aim here for a simpler way to express requests and rights, and for a more automated Privacy Request resolution algebra.

Their support for purposes, and per-purpose consents is limited.

Yet, we want to be compatible with them.

Still the question remains, should we fully reuse what they have built (in terms of categories of data) and try to extend it? My view is that that would limit our ability to offer automation in many use-cases.

### ISO 19944

There is an ISO standard for data categories and processing categories. They are mostly very broad, many overlap, and they are of almost no use for resolving Privacy Requests in the context of GDPR.

However, we might want to allow developers to use our format (properties and concepts) with ISO 19944 categories instead of our terms.

## See also

This document comes with the following support documents:
- [Examples of use](./examples.md)
- [Expected Behavior of Implementing Systems](./expected-behavior.md)

## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.
- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,


### Initiative with which PRIV seeks to be compatible

- [Privacy Model for the Web](https://github.com/michaelkleber/privacy-model/blob/main/README.md)
- [First Party Sets](https://github.com/privacycg/first-party-sets)


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legislation

- CPRA
- HIPPA
