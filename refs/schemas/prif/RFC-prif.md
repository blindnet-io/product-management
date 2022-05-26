# Privacy Request Interoperability Format (PRIF)

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [NNN](https://github.com/blindnet-io/PROJECT/pull/NNN) (update when you have PR #)     |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Sponsor**   | milstan (milstan@blindnet.io)                                                          |
| **Updated**   | 2022-05-25                                                                             |

## Introduction

We propose a simple, structured data format for representing [Privacy Requests](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization#data-capture--rights-requests).
This format corresponds to the [Data Rights Request Schema](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#schemas) component of the [High- Level Architecture](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture).

## Motivation

An individual is in connection with software Systems (and Organisations operating them) that process the individual's data.
In order to [regulate the relationship](https://github.com/blindnet-io/product-management/blob/10bebeefc14f7db7bf7a491932d62a4a5d18ad70/refs/notion-of-privacy/notion-of-privacy.md) with those Systems (and Organisations), the individual makes requests related to their privacy.

With a Privacy Request the individual aims to gain a degree of transparency about data processing and a degree of control over the data and over the data processing. Allowing individuals to make Privacy Requests is becoming more and more a legal obligation.

Different Systems, and different compontents of a single System, including different comnponents of blindnet devkit are likely to exchange information about Privacy Requests. Therefore, a common format is needed to facilitate exchange of information without loss of semantics. The goal of Privacy Request Interoperability Format is to establish a shared conceptualisation and format of Privacy Request so that their processing can be, as much as possible, automatised by the Systems.



## Terminology

>**TO BE Updated** once Lexicon and High Level Conceptualization are synchronised

- We use the term Privacy Request interchangeably with the (deprecated) terms Rights Request and Data Rights Request as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Individual, Person, You, and Data Subject as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv)
- We use the term System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)
- We use the terms Organization, Submitter, Data Consumer as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv) as defined there.

## Design Considerations

### Design Goals

With this design we seek:
- Consistent unambiguous interpretation of Privacy Requests (including shared understanding of their meaning and ways to uniquely identify them) across different Systems, independently of programming languages and components they use
- Minimal exposure of Data Subject and their data during the processing of a Privacy Request,
- Making processing of Privacy Requests as automatic as possible,
- Compatibility with the use of different protocols and tools for user identity management, authentication, and encryption,
- Allowing developers to be fully comply with [supported legislation](#supported-legislation) related to Privacy Requests quickly and easily
- Exhaustivity with regards to situations we need to support in response to [supported legislation](#supported-legislation) yet Extensibility in case new situations arise in the future.
- Highly normative minimal specification, using as much as possible the [Plain Language](https://www.plainlanguage.gov/media/FederalPLGuidelines.pdf) while at the same time making clear references to the (often misfortunate) language of the [supported legislations](#supported-legislation)
- Decentralised design compatible with both the Internet's Client-Server Architecture and Metaverse/Web3 Architecture

### Design Choices

We have made the following choices:
- **Language Independence**. The Privacy Request Interoperability Format is independent from any language for expressing structured data, and can be materialised in different forms such as json, xml, or other. A [json schema](prif.schema.json) is provided for convenience.

- **Rich Semantics**. The Privacy Request Interoperability Format includes reserved words to describe common types of Privacy Requests, categories of data, categories of data processing and other key concepts. This choice is made to facilitate their uniform interpretation by the implementing systems. Their [human-readable titles and descriptions](dictionary) are provided in json format for convenience.

- **Multiple User Identities**. The Privacy Request Interoperability Format  allows for a Data Subject to be identified using more than one user identity. This choice is made to enable the Privacy Request to be easily exchanged across Systems that use different user identifiers.

- **System as a Target**. The Privacy Requests are interpreted at the level of a particular System. If an Organisation operates several systems, and if the Data Subject wants to have the Privacy Request transmitted to all of them, each System may respond differently. The target of a Privacy Request is thus the System exposing an API for Privacy Requests.

- **Decentralised IDs**. The Privacy Request Interoperability Format uses decentralised ways to uniquely identify Data Subjects, Systems, Requests and their elements. The exchange of Privacy Requests can happen without a centralised entity to control identity disambiguation.

## Proposal

### Privacy Request

Data Subject is the author of a Privacy Request.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `data-subject` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1-* | An array of objects, each containing a (`dsid`,`dsid-schema`) pair |

A System MAY have muptiple ways to identify the Data Subject, especially when data about them came from some other System that uses different identifiers.
The System capturing the Privacy Request MAY associate multiple Data Subject Identities to the Privacy Request, especially if the Privacy Request is likely to be transmitted to other systems.

An array of one or more [Data Subject Identities](#decentralized-identity-of-data-subjects) MUST be provided in order to match the Data Subject with the data concerning them.

In addition, the Privacy Request has other meta-data:

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `request-id` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | Unique ID for referening to this request in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1-* | Date and Time when Privacy Request was created in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `demands` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1-* | An array of [Demands](#demands) |

The Data Subject can request several things (e.g. see the data the System has on me, know the source from where you have got it, and have my data deleted). We call those 'Demands'.

A Privacy Request includes an array of one or more Demands.

#### Demands

A Demand is a concrete action that the user requests.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `demande-id` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | Unique ID for referening to this demande in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `action` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | Unique value. One of {`ACCESS`, `DELETE`, `MODIFY`, `OBJECT`, `PORTABILITY`, `RESTRICT`, `REVOKE-CONSENT`, `TRANSPARENCY`, `TRANSPARENCY.DATA-CATEGORIES`, `TRANSPARENCY.DPO`, `TRANSPARENCY.LEGAL-BASES`, `TRANSPARENCY.ORGANISATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.PROCESSING-CATEGORIES`, `TRANSPARENCY.PROVENANCE`, `TRANSPARENCY.PURPOSE`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO`, `OTHER`} |
| `legal-grounds`| [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of strings representing legal grounds that support the Demand. E.g. "GDPR.13" indicates Article 13 of GDPR, "CCPA.1798.105" indicates Section 1798.105 of CCPA |
| `message` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | Optional comment, motivation or explanation of Demand |
| `language` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | Language of textual message associated with demands in the format of [FRC5646](https://datatracker.ietf.org/doc/rfc5646/) |

The key element that defines the nature of the Demand is the `action`. A Demande MUST have one and only one `action`.

Actions are hierarchical.
Their relationships are dentoed with a dot "." separating two actions, the more general one being written on the left.
`TRANSPARENCY` includes `TRANSPARENCY.WHERE`.
When `TRANSPARENCY` is demanded, Systems MUST interpret the demand as if all the subcategories of `TRANSPARENCY` were demanded.

##### Demand Restrictions

The `action` that the Data Subject requests with a particular Demand MUST be interpreted in the context of restrictions.
A Demand MAY refer to only certain categories of data, or certain types of processing, certain purposes of processing etc.

###### Data Categories

A Demand MAY be restricted to one or more data categories. For example, a Data Subject can request to access to all data concerning his location.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `data-category` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | One of {`AFFILIATION`, `BEHAVIOR`, `BEHAVIOR.ACTIVITY`,  `BEHAVIOR.CONNECTION`,   `BEHAVIOR.PREFERENCE`, `BIOMETRIC`, `CONTACT`, `CONTACT.EMAIL`, `CONTACT.ADDRESS`, `CONTACT.PHONE`, `DEMOGRAPHIC`, `DEMOGRAPHIC.AGE`, `DEMOGRAPHIC.BELIEFS`, `DEMOGRAPHIC.GENDER`, `DEMOGRAPHIC.ORIGIN`, `DEMOGRAPHIC.RACE`, `DEVICE`, `FINANCIAL`, `FINANCIAL.BANK-ACCOUNT`, `GENETIC`, `HEALTH`, `IMAGE`, `LOCATION`, `NAME`,`RELATIONSHIPS`,  `PROFILING`, `UID`,  `OTHER`} |

When several values are given, Systems MUST interpret the `data-category` restriction as a union of all the categories indicated.

Categories are organised as a hierarchy, denoted with a dot ".", the more general category being written on the left.
E.g. the following two `data-category` restrictions are equivalent:
- `CONTACT`,`CONTACT.EMAIL`
- `CONTACT`

In the absence of indication of any `data-category` restriction, Systems MUST interpret the Demand as being related to all categories of data.
[A list of eligible `data-category` values with corresponding user-facing descriptions is provided](dictionary/data-categories/) for conveniance.

###### Categories of Processing

A Demand can be restricted to particular kinds of data processing.
For example, a Data Subject can oppose to automatic inference but continue to accept their data beeing collected and stored.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `processing-categories` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | One of {`ANONYMIZATION`, `AUTOMATED-INFERENCE`, `AUTOMATED-DECISION-MAKING`, `COLLECTION`, `GENERATING`, `PUBLISHING`, `STORING`, `SHARING`, `USING`, `OTHER`} |

When several values are given, Systems MUST interpret the `processing-categories` restriction as a union of all the processing categories indicated.

In the absence of indication of any `processing-categories` restriction, Systems MUST interpret the Demand as being related to all and any `processing-categories` of treatment.

[A list of eligible `processing-categories` values with corresponding user-facing descriptions is provided](dictionary/purposes) for conveniance.

###### Purposes of Processing

A Demand can be restricted to particular purpose of data processing. For example, a Data Subject can oppose to any data processing done for marketing purposes, but still accept their data being processed for the sake of personalisation of their experience.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `purposes` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | One of {`ADVERTISING`, `CONTRACT`, `CONTRACT.BASIC-SERVICE`, `CONTRACT.ADDITIONAL-SERVICES`, `NECESSARY`, `NECESSARY.JUSTICE`, `NECESSARY.LEGAL`, `NECESSARY.MEDICAL`, `NECESSARY.PUBLIC-INTERESTS`, `NECESSARY.VITAL-INTERESTS`, `NECESSARY.SOCIAL-PROTECTION`, `MARKETING`, `PERSONNALISATION`, `SALE`, `SECURITY`, `TRACKING`, `OTHER`, `ANY`} |

When several values are given, Systems MUST interpret the `purposes` restriction as a union of all the purposes indicated.

Purposes are organised as a hierarchy, denoted with a dot ".", the more general purpose being written on the left. E.g. the following two `pruposes` restrictions are equivalent:
- `NECESSARY`,`NECESSARY.LEGAL`
- `NECESSARY`

In the absence of indication of any `purpose` restriction, Systems MUST interpret the Demand as being related to all and any purpose of treatment.

[A list of eligible `purposes` values with corresponding user-facing descriptions is provided](./dictionary/purposes/) for conveniance.

###### Consent IDs

A Demand can be restricted to particular Consent ID(s). For example, a Data Subject revoques a particular consent only (the one related to his data being shared with 3rd parties) but maintains other consents they may have given.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `consent-ids` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of consent ids to indicate that the Demand (e.g. a `REVOKE-CONSENT` Demand) is restricted to particular consents. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `consent-ids` are idnicated, Systems MUST interpret the Demand as related to all Consents related to indicated `consent-ids`.

###### Capture IDs

A Demand can be restricted to particular Capture ID(s). For example, a Data Subject to delete a particular data, they indicate the data capture concerned by their Demand.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `capture-ids` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of Data Capture IDs to indicate that the Demand (e.g. a `DELETE` Demand) is restricted to data captured within particular Data Captures. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |

When one or more `capture-ids` are indicated, Systems MUST interpret the demande all related to all the data captured as part of those Data Captures.

#### Transitive Privacy Request

A Privacy Request can be transitive.
Transitive Privacy Requests are usefull in a distributed context where System A gave information about the Data Subject to System B, and System B gave information about the Data Subject to System C.

When a System receives a transitive Rights Request, it SHOULD not only respond to it, but also transfer it to corresponding Systems with which it exchnaged data about the Data Subject.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `transitivity` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | One of {`DOWNWARD`, `UPWARD`, `BIDIRECTIONAL`, `INTRANSITIVE`} |

Transitivity of Rights Requests can be `DOWNWARD` `UPWARD`, `BIDIRECTIONAL` or `INTRANSITIVE`. In the absence of any indication `INTRANSITIVE` SHOULD be assumed.

When System B receives a `DOWNWARD` transitive Rights Request, it MUST also send it to all systems to which it tranfered data about the Data Subject (System C).
When System B receives a `UPWARD` transitive Rights Request, it MUST also send it to all systems from which it obtained data about the Data Subject (System A).
When System B receives a `BIDIRECTIONAL` transitive Rights Request, it MUST also send it to all systems from which it obtained data about the Data Subject or to which it gave information about the Data Subject (System A and System C).
When System B receives an `INTRANSITIVE` Rights Request, it SHOULD NOT transfer it to any other system.

Systems should interpret the transitivity of Rights Request the same way regardless of the Rights Request being received directly from the Data Subject or from a corresponding System.

Convenient tables of `transitivity` values and corresponding user-facing descriptions, in different languages, are provided [here](dictionary/transitivity).

## Detailed Design

A separate document gives a list of [examples](examples.md) on how to represent real-life Privacy Requests, as defined in [supported legislation](#supported-legislation), or as modeled in existing systems with which we seek interoperability.

## Detailed Design

### JSON format

We provide a [JSON Schema document](./prif.schema.json) for machine-readable interpretation of Privacy Requests compliant with [v4 (or ideally lower) of IETF specification](https://datatracker.ietf.org/doc/html/draft-zyp-json-schema-04#:~:text=JSON%20Schema%20is%20a%20JSON,interaction%20control%20of%20JSON%20data.)

### Authenticated exchanges

Systems exchanging Privacy Requests MUST be able to do so in a way allowing them to very the integrity of their content, and the identity of the system having emitted the Rignts Request.

For this purposes Privacy Requests MAY be embedded as 'Claims' in [JWTs (RFC7519)](https://datatracker.ietf.org/doc/html/rfc7519).

### Decentralized Identity of Data Subjects

The Systems are only able to provide control to Data Subjects if they can identify them. On the other hand, there is no cetnral authority to manage Data Subject identity globally.

Therefore, we use a set of atributes to uniquely indenitfy one Data Subject. One and the same Data Subject can have multiple such identities.

#### Globaly Unique Data Subject Identities

The identifiers used to refer to Data Subjects MUST be globaly unique. One Data Subject identity corresponds to one Data Subject. One Data Subject can have several Data Subject Identity.

When refering to a Data Subject, Systems MUST use both of the following atributes:
- `dsid` - Data Subject ID
- `dsid-schema` - A scheme allowign to dereference the Data Subject ID

The (`dsid`,`dsid-schema`) pair denotes a globaly unique reference to always the same Data Subject.

We refer to (`dsid`,`dsid-schema`) pairs as Data Subject Identities.

A Rights Request MAY include several (`dsid`,`dsid-schema`) pairs that refer to the same user, in order to facilitate the interoperability of Rights Requests across systems.

#### Data Subject ID Schemas

Systems using RRIF MUST implement at least the following `dsid-schema`:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`uuid`| Indicates that the value of the corresponding `dsid` attribute is a Universaly Unique ID in the sens of [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) |

Systems using RRIF SHOULD implement at the following `dsid-schema`:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`email-sha-256`| Indicates that the value of the corresponding `dsid` attribute is the result of the SHA-256 hashing function taking the e-mail of the Data Subject as argument |

Additional Data Subject ID Schemes MAY be definied by convention. For example the following MAY be used:

|`dsid-schema` value | Interpretation of the corresponding `dsid` value |
| ------------------- | ---- |
|`global-id`| Indicates that the value of the corresponding `dsid` attribute is the `gid_name` - User's GlobaliD name - used to identify the Data Subject in [GlobalId](https://developer.global.id/documentation/api%2Fidentity.html)|

#### Data Subject SHOULD be Authenticated

In some cases, valid reasons MAY exist for Systems to respond to Rights Requests even from anonymous Data Subjects. This is the case, for example, with request relative to general data treatment practices practiced by the system.

However, in most cases, Systems MUST require the Data Subject to be authenticated as being indeed the person corresponding to the (`dsid`,`dsid-schema`) pair.

When processing Rights Request, Systems MAY automatically disregard the (`dsid`,`dsid-schema`) paris for which they have not been able to establish Data Subject authentication.

However, the authentication does not necessairly have to be performed during the collection of the Rights Request. It can be done separately.

#### Matching Multiple Data Subject Identities

Systems MAY keep track of Data Subject Identities that refer to the same Data Subject. In some cases, valid reasons MAY exist for Systems to ignore such information.

When Systems do know that one Data Subject Identity corresponds to the same user as another Data Subject Identity, then Systems SHOULD offer the Data Subject a possibility for their Rights Requests, expressed in relation to one Data Subject Identity to be automatically extended to include other equivalent Data Subject Identities.

Systems SHOULD NOT imply Data Subject Identity equivalence from Rights Requests, especially when granding Rights Requests that require authentication.

### Data Capture IDs, Data Capture Fragment IDs, Consent IDs, Rights Request IDs, Demand IDs, Rights Request Respons IDs are Globally Unique

All of the following identifiers `data-capture-id`, `fragment-id`, `consent-id`, `rights-request-id`, `demand-id`, `rights-response-id` MUST be globally unique and be generated according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) in order for the corresponding objects to be easily identifiable across systems.
The reason for using UUDIs is to allow Systems to independently generate globally unique identifiers while being autonomous from a central entity that would ensure identifier uniqueness.

Having a public ledger for UUDIs MAY be considered for Consents and Data Captures, but serious implications to Data Subject exposure MUST also be considered.
However, the design MUST be compatible with building a public decentralised ledger.

### Data Categories, Treatment Types, Actions, and Purposes SHOULD be Unambiguous and Complete

The lists of Data Categories, Treatment Types, Actions, and Purposes SHOULD be desiged in such a way to be:
- **Unambiguous** : The developer using the schema knows without ambiguity which one (of which ones) to use in any given situation, AND
- **Complete** : They allow to exress the totality of possible needs in the context of a user wanting to [regulate their privacy/connectedness](https://github.com/blindnet-io/product-management/blob/dogma/refs/notion-of-privacy/notion-of-privacy.md), as well as the totality of requests defined by the [supported legilsation](#supported-legilsation).

## Design Implications for Systems Implementing PRIF

### Remembering Transfers

When data about Data Subjects is transmitted from one system to another, in order to be able to process [Transitive Rights Requests](#transitive-rights-request), and in order to reply to `TRANSPARENCY.WHO` and `TRANSPARENCY.PROVENANCE` demands, Systems MUST keep track of:
- System of destination/origin and addresses where their APIs can be reached
- Categories of data being trasnfered
- Identifiers (`data-capture-id`s,`fragment-id`s) associated to the data being trasnfered
- Consents (`consent-id`) associated to the data being trasnfered
- Data Subject Identities (`dsid`,`dsid-schema`) pairs associated to the data being trasnfered

> **Note**
>
> Systems that exchange Data Subject information with other Systems MUST:
> - expose an API for communicating with other systems about Rights Requests:
>     - receiving Rights Requests from those other Systems,
>     - receiving Rights Request Responses from other Systems in the case of [Nested Responses Scenario](https://github.com/blindnet-io/product-management/tree/devkit-schemas/refs/high-level-architecture#different-rights-request-response-scenrarios).

### Storing General Information

In order to automatically respond to `TRANSPARENCY` demands, Systems should store general information about:
- Countries where data servers are located (`TRANSPARENCY.WHERE`)
- The identity of the organization controling them, and the Organization's representative(s) (`TRANSPARENCY.WHO`)
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
- Duration of mandatory data keeping, as well as period after which the data is automatically deleted - Can be difernt per Data Capture Fragment, and relative to en event such as Data Capture, End of Contract, Account Deletion (`TRANSPARENCY.RETENTION`, but also for automatically evaluating the legality of keeping data at a certain time and upon `REVOKE-CONSENT`, `OBJECT`, `RESTRICT`, `DELETE` requests)
- Data Categories - can be different per Data Capture Fragment (`TRANSPARENCY.DATA-CATEGORIES`)
- Data Processing Categories - can be different per Data Capture Fragment (`TRANSPARENCY.PROCESSING-CATEGORIES`)
- Purposes of Data Processing  - can be different per Data Capture Fragment (`TRANSPARENCY.PURPOSE`)

>**Note**
>
> To automatically calculate legality of keeping a particular data, Systems MUST track events such as Data Capture, End of Contract, Account Deletion




## Questions and Discussion Topics

### Use UUID for identifying Data Subjects

We chould immagine an alternative design, where we would force systems to use an [UUID]([uuid](https://en.wikipedia.org/wiki/Universally_unique_identifier)) (according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html)), to identify the users. That would require us to provide some way for systems to match UUIDs with their local IDs (usernames, or e-mails), and would ponteltially limit the ability of 3rd party systems to interprete Rights Request made at another system. This goal of proposed design is to allow for flexibility. However it is a very important aspect of the proposal, that deserves further debate.

### Mandatory properties and value constrains

Should we include rescritions in the schema according to the [JSON-schema-validation vocabulary](https://datatracker.ietf.org/doc/html/draft-bhutton-json-schema-validation-00#page-4) in order to make certian properties mandatory and ensure to limit string values to the values we suppoort?

In the curent proposal, this is the case for Transitivity, but not for request types, data categories, and user identity schemas. We might want to include more forma constraints there, or deliberately leave flexibility. This is a discussion we need to have.

### Dot-notation for category hierarchies

Hierarchies of categories are represented using the "supercategory.subcategory" notation. The idea behind this is to allow developers to use the level of granularity that is adapted to them, yet be able to easily situate the subcategory in supercategory when dealing with more generic requests.

E.g. We have a data capture associated to "CONTACT.ADDRESS" data category. The Data Subject makes a DELETE request related to all of their data falling under "CONTACT" data category. The developer can easily identify "CONTACT.ADDRESS" as being a subcategory of ""CONTACT.ADDRESS".

However, this notation (although intuitive) is to the best of my knoweldge, non-standard. Maybe there are reasons for it, or a standard (better) notation we can adopt?
Or if none (which would be surprising) we could define our syntax using [Backus-Naur Form](https://datatracker.ietf.org/doc/html/rfc4234). Advantage: geeks will love us.

### Representation of Legal Articles

Is there a better way to unambiguousely refer, in a machine-readable way, to parts of legislations?

### Schema elegance and modularity

We need a way to make enums different categories and types more elegant, and reusable in the perspective of using them to also represent Data Captures, Consents and responses to Privacy Requests.

### Addressability of System Endpoints

Is there a standard way for representing peer-to-peer System's API endpoints that we can reuse here for representing systems.


## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.
- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,

### Informative References

-

### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- [CPRA]([https://eur-lex.europa.eu/eli/reg/2016/679/oj](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf))
- [HIPPA]([https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5](https://www.govinfo.gov/content/pkg/PLAW-104publ191/pdf/PLAW-104publ191.pdf))
