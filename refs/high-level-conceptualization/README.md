# HIGH-LEVEL CONCEPT MODEL

## INTRODUCTION

> **The promise: blindnet devkit is the simplest solution for implementing [privacy-enabled connectedness](../notion-of-privacy/notion-of-privacy.md#privacy-enabled-connectedness). It enables confidentiality, control and compliance with regulation**
>
> It is foundation stone of a new software paradigm - it allows to build new kind of software, with privacy embedded in its design and architecture.

_This high-level concept model describes the conceptualization behind blidnet’s software, in terms of the information it deals with and the reality it enables.

This conceptualization does not directly translate to any database structure, workflow, or code. It aims to inform software designers’ thinking, guide design choices, and reduce confusion._

## TERMINOLOGY

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- All terms defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md) are to be interpreted as described there

### THE MAIN CONCEPT - DATA CAPTURE

<img width="900" alt="organisation" src="./img/organization.png">

A [Data Capture](../lexicon/RFC-Lexicon-2.md#data-capture) is the most central concept of interest in [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit).

It corresponds to a particular data exchange need, and can be composed of files and other data fields of different types.
A Data Capture can be captured at once or over the course of multiple interactions. One or more [Submitters](../lexicon/RFC-Lexicon-2.md#submitter) can complete a Data Capture.

Examples of a need include: medical history of a new patient (doctor); candidate CV (company hiring); a set of legal proofs in a lawsuit provided by a client (lawyer); identity documents of founders in the investment KYC process (VC fund).

### FORM FOLLOWS FUNCTION

A [Privateform](../lexicon/RFC-Lexicon-2.md#privateform) includes the interface, the data structures and to them associated settings and logic allowing to capture [Data Captures](../lexicon/RFC-Lexicon-2.md#data-capture).

Settings MAY include configurations related to delays of conservation and expiry of Data Captures, confidentiality and access rights to captured data, Consent collection options, view/decrypt rights and similar.

When a [Submitter](../lexicon/RFC-Lexicon-2.md#submitter) interacts with an instance of Privateform, a Data Capture is created.

<img width="350" alt="Data capture creation" src="./img/data-capture-creation.png">

>
> **Note**
> A Data Capture MAY also be created by generating/inferring data about the Data Subject, or by transfer from another [System](../lexicon/RFC-Lexicon-2.md#system)
>

### DATA CAPTURE - FRAGMENTS

A Data Capture has one or many [Capture Fragments](../lexicon/RFC-Lexicon-2.md#data-capture-fragment).

Examples of Fragments include: a file and a comment explaining it; a set of fields composing an address; a set of questions related to the same topic;

<img width="350" alt="Capture fragments" src="./img/capture-fragments.png">

The data structure of Data Capture Fragments allows to have interface elements such as granular progress bars, or checklists to present to the user the state of complement of the submission.

Data Capture Fragments have names, that exist in a multitude of languages and allow for easy reference by [Data Submitters](../lexicon/RFC-Lexicon-2.md#submitter) and Data Consumers.

The granularity can also allow, when needed, to the data consumers to accept or reject certain fragments for reasons of readability/conformity, and make the submitter submit them again.

It also favors incremental data submission (submit part of the form today, and another part some other day when the submitter collects more data), as well as partial modification and data update focused only on particular fragments.

<img width="300" alt="Checklist" src="./img/checklist.png">

Capture Fragments can be subject to validations:
- **a priori** using automatic validators (like checking the format of an e-mail adress, or extension of a file)
- **a posteriori** using human input to validate the conformity of submitted data with what is expected

### DATA CAPTURE – LEGAL BASE

Depending on the relationship between the [Submitter](../lexicon/RFC-Lexicon-2.md#submitter) and the [Organization](../lexicon/RFC-Lexicon-2.md#organziation), as well as the context of data capture and use, a [Data Capture](../lexicon/RFC-Lexicon-2.md#data-capture) can be associated with different Legal Bases for collecting, keeping and treating data.
Legal Bases impact the following properties of a particular Data Capture that our systems allows to compute:

- Data **CAN** be kept at a given time
- Data **MUST** be kept at a given time

**See more about legal bases** [here](https://www.cnil.fr/fr/les-bases-legales).
More than one legal base can exist for the same data at the same time.
E.g.:

- A user can give explicit Consent, and at the same time keeping the data might be mandatory; When the user revokes Consent, the data must still continue to be kept.
- A service contract can exist between the user and the organization making the organization legitimate to keep the data, and at the same time the user might give Consent. After contract has ended, the data can be kept until the user revokes Consent and withing the maximal conservation time allowed by law.

The CAN/MUST-be-kept of the data at a given time is also constrained by [maximal conservation times defined by law](https://www.cnil.fr/fr/les-durees-de-conservation-des-donnees) or by minimal legally mandatory conservation time in certain domains (finance).

Such times are often relative to some event (e.g. data collection date, or a date when the submitter-organization relationship or contract has ended).

> _Managing Legal bases SHOULD be a value-added service allowing to trigger automatic Data Capture deletion, or its protection from user-initiated deletion_

<img width="450" alt="Legal ground" src="./img/legal-ground.png">

### DATA CAPTURE – CONSENT

Consent is a particular form of Legal Base for data collection and keeping. When it is the only Legal Base, Consent MUST be explicitly collected while capturing data (even partial Data Capture without all fragments completed). When Consent is collected then, a possibility must be given to the submitter to revoke it.

Consents have states (e.g., valid, expired, revoked).

One Consent corresponds to [one and only one purpose](https://www.cnil.fr/fr/les-bases-legales/consentement) (e.g., facilitate future purchases, ongoing contract, promotions, 3rd party communication). Thus, a Data Capture can be associated to more then one Consent, that can be given and revoked separately.

<img width="225" alt="Consent" src="./img/consent.png">

### DATA CAPTURE – PRIVACY REQUESTS

A [Data Subject](../lexicon/RFC-Lexicon-2.md#data-subject) has the right to demand different things related to their privacy, their data and their rights. We call those, [Privacy Requests](../lexicon/RFC-Lexicon-2.md#privacy-request). They refer to:

- **General information** about policies, storage locations, practices, and purposes of data treatment (unrelated to any particular Data Capture)
- **Particular information** about Data Capture date, origin of data, etc.
- Data access and manipulation rights **related to a particular Data Capture or Data Capture Fragment**.
- Opposition to treatment (can be denied if unreasonable i.e. if other legal ground
  exists)

The [System](../lexicon/RFC-Lexicon-2.md#system) SHOULD allow to capture such requests, keep track of them, and on what is done to act upon them, and provide proof that the action upon the requests was compliant (rights given/denied according to law and in time).

Capturing requests related to a particular [Data Capture](../lexicon/RFC-Lexicon-2.md#data-capture) or [Data Capture Fragment](../lexicon/RFC-Lexicon-2.md#data-capture-fragment) requires user authentication.

<img width="275" alt="rights requests" src="./img/rights-requests.png">


### DATA CAPTURE - STATES

[Data Captures](../lexicon/RFC-Lexicon-2.md#data-capture) have states. States can be observed on the Data Capture level, or on the level of a [Data Capture Fragment](../lexicon/RFC-Lexicon-2.md#data-capture-fragment).

States concern different qualities, such as (not limited to):

- **Submission** (captured or missing)
- **Consumption** (viewed or new)
- **Acceptance** (accepted, rejected, under review)
- **Expiry** (In mandatory keeping, possible keeping, possible conservation expired, mandatory update pending)

Legal grounds also have states indicating if the data MUST or CAN be kept/deleted.

Rights Requests also have states with regards to:

- **Their treatment** by the [Data Consumers](../lexicon/RFC-Lexicon-2.md#data-consumers) / [Organization](../lexicon/RFC-Lexicon-2.md#organization) (received, viewed/under review, treated)
- **Acceptance** (accepted, partially accepted, rejected)
- **Fulfillment** of the [Data Subject's](../lexicon/RFC-Lexicon-2.md#data-subject) need (data accessed, data modified, data deleted)

The [System](../lexicon/RFC-Lexicon-2.md#system) keeps a record of every status change and the corresponding timestamp allowing to build a timeline.

Also, rights have states, meaning that in a particular state, a particular type of [Privacy Request](../lexicon/RFC-Lexicon-2.md#privacy-request) MUST be rejected. For example, during mandatory keeping a DELETE request from the user MUST be rejected.

> _The information provided here is just for illustrative purposes and does not imply any definitive naming or semantics of actual states._

### DATA CAPTURE – VERSIONING

[Data Capture Fragments](../lexicon/RFC-Lexicon-2.md#data-capture-fragment) are subject to versioning. A particular data fragment can evolve as a result of:
- **Submission and Changes** by [Data Subject](../lexicon/RFC-Lexicon-2.md#data-subject) or another [User](../lexicon/RFC-Lexicon-2.md#user) during submission or through interaction with a user-interface
- **Collection and Transfer** when data is derived/inferred by a [System](../lexicon/RFC-Lexicon-2.md#system) or transferred from System to System
- **[Privacy Requests](../lexicon/RFC-Lexicon-2.md#privacy-request)** by Data Subject asking to modify or delete the data or restrict its storing
- **Modifications** by Data Consumers (e.g., within modification requests, or through common features for user profile modification, or any other way) and DPOs (when the new data is collected offline from the Data Subject)

The format of Privacy Requests to modify data must be compatible with the versioning of Data Capture Fragments and allow for automatic update upon Privacy Request acceptance.

### DATA CAPTURE – INTEROPERABILITY

<img width="900" alt="interoperability" src="./img/interoperability.png">

More than one [System](../lexicon/RFC-Lexicon-2.md#system) can use [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit) to collect, store, and exploit data.
In other words, a [Data Capture](../lexicon/RFC-Lexicon-2.md#data-capture) MAY be generated by a [Submitter](../lexicon/RFC-Lexicon-2.md#submitter) within one system, but the [Data Consumers](../lexicon/RFC-Lexicon-2.md#data-consumer) MAY be consuming the data using multiple different systems.

Systems can exchange Data Captures without compromising the encryption of the data. In addition, they can use blindnet devkit to pass any change of state, Legal Bases, Consents, or data modifications, [Privacy Requests](../lexicon/RFC-Lexicon-2.md#privacy-request), etc., between Systems.

Blindnet serves as a _lingua franca_ for both confidentiality (encryption) and control (Legal Base/Consent/Privacy Request processing). While encryption de-facto constrains access to the data, the control part is not enforceable upon the systems but is rather enabling them to stay compliant and demonstrate compliance.

### SUBMITTER / DATA CONSUMER / DPO

**[Submitters](../lexicon/RFC-Lexicon-2.md#submitter)** provide the data. In many situations, it is safe to assume that the [Data Subjects](../lexicon/RFC-Lexicon-2.md#data-subject) is the Submitter (that the Submitter is providing data about himself). However those two are fundamentally different concepts. Thus, in order to be compliant, the [System](../lexicon/RFC-Lexicon-2.md#system) MUST also allow to capture [Privacy Requests](../lexicon/RFC-Lexicon-2.md#privacy-request) from a Data Subject regardless of the fact whether they are the Submitter or not. Submitter can be anonymous, Data Subject can’t.

**[Data Consumers](../lexicon/RFC-Lexicon-2.md#data-consumer)** can decrypt and view (and, if appropriate, modify and delete) the data.

**[DPOs](../lexicon/RFC-Lexicon-2.md#dpo)** are a special type of Users that use the System to respond to Privacy Requests. They MAY have limited access to the data itself (and in some case MUST NOT be able to see the data) but leverage the System as a proof of having acted legally and respected data subjects’ rights.

### CONFIDENTIALITY – CONTROL BRIDGE

<img width="1200" alt="confidentiality" src="./img/confidentiality.png">

[Privacy](../notion-of-privacy/notion-of-privacy.md#definition), in a psychological sense, equals the freedom of an individual to engage/disengage from certain relationships (and identities such relationships project upon them). This freedom to engage/disengage in the context of internet interactions, relies on two main pillars:

- **confidentiality** (the information being kept confidential from unintended data consumers or purposes)
- **control** (gain transparency and impose actions over data to the data consumers by the data subject)

However, there must be a separation between the two allowing a developer to use [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit) only for one of these two purposes, and use an alternative solution for the other. E.g., a developer can use a non-encrypted web form to capture data, manage his own access to it, and still use blindnet devkit for managing Consent, and [Privacy Requests](../lexicon/RFC-Lexicon-2.md#privacy-request).
Composition of the components of blindnet devkit is inspired by the bridge design pattern.
See [Bridge Pattern, Gang of Four](https://refactoring.guru/design-patterns/bridge).
