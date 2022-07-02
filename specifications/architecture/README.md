# blindnet devkit Architecture

This document specifies the architecture of the blindnet devkit.

> **Note**
>
> The current version of this document is based mainly on the [HLA][HLA]. It is expected for this document to evolve, especially once the [functional requirements document](../../specifications#functional-requirements) is available.

## Terminology

- All terms defined in [RFC-Lexicon-2][Lexicon] are to be interpreted as described there
- Any additional precision about the terms defined in [RFC-Lexicon-2][Lexicon], as well as additional terms such as Consent and Legal Base, provided in [High Level Conceptualization][HLC] is to be considered normative
- We use the terms Capture Component, Encryption and Access Management Engine, Privacy Computation Engine, Privacy Compiler, Privacy Request Capture Interface, Schemas and Storage Component as defined in [High Level Architecture][HLA]

## Responsibilities

Figure below presents the blindnet devkit architecture.

<img src="./img/devkit_architecture.png">
<br><br>

Each element within the architecture is responsible for a certain set of functions within the blindnet devkit.

**Privacy Request Capture Interface**, which is a part of **Privacy Request Manager** as described in [HLA][HLA], is an end-user interface allowing Data Subjects to submit Privacy Requests. For requests that require it, this component may also initiate Data Subject Authentication, deliver the Privacy Request Response (including the data that may be part of response) and show its status.

**Data Consumer Interface**, which is a part of **Privacy Request Manager** as described in [HLA][HLA], is an end-user interface for Data Consumers which allows them to:

*Q3 2022 Scope*:
- Set relevant configurations (e.g., Retention Policies, General Information for TRANSPARENCY requests, Transfers information, desired level of automation of Privacy Request Processing )
- Manage Privacy Requests (View Privacy Requests, Act upon Privacy Request Response recommendations - grant/deny/transfer requests)

*Autumn 2022 Scope*:
- View and manage Data Captures

**Web components** are front-end, look and feel agnostic components which allow integrations of different blindnet devkit functions into external systems and web sites. Currently, these include:
- Login component (System must be able to work with existing login engines of client Systems)
- Communication (emailing) component
- Custom data capture components
- Data consumption components, i.e., components that allow Data Consumers to view and manage data
- Privacy Request capture components, i.e., components that allow Data Subjects to submit Privacy requests
- Privacy settings component, i.e., component that allows Data Consumers to set desired configurations
- Privacy Request management components, i.e. components that allow Data Consumer to view and manage Privacy Request

**Blindnet common** is an entry point to blindnet devkit functions.
It is imagined as a single element used by developers, which further uses different parts of the blindnet devkit depending on developers' needs.

Different components from the [HLA][HLA] (Capture Component, Encryption and Access Management Engine, Privacy Computation Engine) are implemented through several architectural elements.

The [HLA][HLA]'s **Capture Component** consists of _Capture SDK_, _Capture API_, and _Capture DB_, and it:

*Q3 2022 Scope*:
- Generates metadata according to PRIV (whenever a data record is made - from user input or any other data-collection mode e.g. transfer, machine learning etc.), covering everything (including 3rd party consents) needed for Privacy Computation Engine to operate as automatically as possible.

*Autumn 2022 Scope*:
- Captures data and metadata for Data Consumers
- Protects confidentiality of Data Captures (encryption), by relying on Encryption Engine
- Obtains Legal Bases related to Data Captures
- Allows capturing Data Captures through Data Fragments
- Allows capturing Data Captures over multiple time instances
- Allows multiple Data Submitters to submit a Data Capture
- Allows managing Data Captures on the Data Fragment level

The [HLA][HLA]'s **Encryption and Access Management Engine** consists of _Encryption SDK_, _Encryption API_, and _Encryption DB_, and it:
- Encrypts and decrypts data
- Integrable with external OpenID tools
- Allows recovery after access is lost

The [HLA][HLA]'s **Privacy Computation Engine**, including **Privacy Compiler** and **Customization API**, consists of _Privacy SDK_, _Privacy API_, and _Privacy DB_, and it:
- Captures Privacy Requests from Data Subjects
- Captures privacy-related Settings (including mapping between PRIV terms and database schema of the client System)
- Interprets Data Capture metadata (based on Settings)
- Calculates (explainable) response to Privacy Requests
- Keeps traces of Privacy Requests decisions and actions
- Provides proofs of Privacy Requests decisions and actions
- Registers operations and transfers of Data Captures across Systems
- Allows Data Subjects to revoke Consents

**Storage** elements of the architecture (_Storage SDK_, _Storage API_, and _Cloud Storage_) are responsible for storing the data.

**Identity** elements of the architecture (_Identity SDK_, _Identity API_, and _Identity Storage_) are responsible for creating and managing Users of the blindnet devkit (e.g., Data Subjects, Data Consumers, etc.).

## References
- **Lexicon** [RFC-Lexicon-2][Lexicon]
- **HLA** [High Level Architecture][HLA]
- **HLC** [High Level Conceptualization][HLC]

[Lexicon]: ../../refs/lexicon/RFC-Lexicon-2.md "RFC-Lexicon-2"
[HLA]: ../../refs/high-level-architecture/ "High Level Architecture"
[HLC]: ../../refs/high-level-conceptualization/ "High Level Conceptualization"
