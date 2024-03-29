# Compatibility with other Protocols, Vocabularies and Formats

| Status        | NA / supporting document                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io)         |
| **Updated**   | 2022-07-25                                                                             |

## Introduction

There are other initiatives, partially overlapping with the goals of the [Privacy Request Interchange Vocabulary](./priv/RFC-PRIV.md) and the [Privacy Request Multicast Protocol](./protocols/RFC-PRMP.md).

This document addresses the question of their differences and compatibility.

## Compatibility

### Vocabularies

| Alternative Vocabulary | Status | Implications |
| :-----: | :----: | :------ |
| [Fides by Ethica](https://ethyca.github.io/fides/1.7.0/) | [Full mapping](#fides-by-ethica) | Systems using Fides can use the Fides-to-PRIV mapping to export their (meta)data to systems using PRIV. On import from other systems, they will not be able to process all (meta)data as Fides only covers a subset of PRIV's scope |
| [Trasncend](https://transcend.io/) | [Full mapping](#transcend) | same as above |
| [Data Rights Protocol Data Schemas](https://github.com/consumer-reports-digital-lab/data-rights-protocol#30-data-schemas) | [Full mapping](#drp-data-schemas)| same as above |

## Data Exchange Formats

| Format | Status | Implications |
| :-----: | :----: | :------ |
| [UROPA](https://gdpr.stoplight.io/docs/uropa/) | Compatible | Can be used natively with PRIV terms as values of textual properties for Data Categoties. For properties where UROPA imposes the use of their enums, those must be converted to PRIV terms using the [available mapping](#uropa). |


## Protocols

| Format | Status | Implications |
| :-----: | :----: | :------ |
| [Data Rights Protocol Endpoint Specification](https://github.com/consumer-reports-digital-lab/data-rights-protocol#20-http-endpoint-specification) | [Can be made compatible with PRIV](#drp-endpoint-specification) | The protocol can be used in conjunction with PRIV objects, if the keyword MUST is dropped from all statements related to the use of DRP Data Schemas, and instead the use of PRIV object is allowed. |


## Mappings

### Fides by Ethyca

#### Account Contact Data

| Ethyca Parent key | **Ethyca Label** | Ethyca Description |Representation |
|  ------------ | -------------------------------------- | ------------ | ------------ |
| **account** | **Contact**  | Contact data related to a system account | `data-categories`:`CONTACT` |
| **account.contact** | **email**  | Account's email address | `data-categories`:`CONTACT.EMAIL` |
| **account.contact** | **phone_number**  | Account's phone number | `data-categories`:`CONTACT.PHONE` |
| **account.contact** | **City**  | Account's city level address data | `data-categories`:`CONTACT.ADDRESS` |
| **account.contact** | **Country**  | Account's country level address data | `data-categories`:`CONTACT.ADDRESS` |
| **account.contact** | **postal_code**  | Account's postal code  | `data-categories`:`CONTACT.ADDRESS` |
| **account.contact** | **state**  | Account's state level address data  | `data-categories`:`CONTACT.ADDRESS` |
| **account.contact** | **street**  | Account's street level address | `data-categories`:`CONTACT.ADDRESS` |

#### Account Payment Data

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **account** | **payment**  | Payment data related to system account | `data-categories`:`FINANCIAL` |
| **account.payment** | **financial_account_number**  | Payment data related to system account | `data-categories`:`FINANCIAL.BANK-ACCOUNT` |

#### System Data Categories

> Data unique to, and under control of the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **system** | **authentication**  | Data used to manage access to the system | `data-categories`:`OTHER-DATA` |
| **system** | **operations**  | Data used for system operations | `data-categories`:`**Any/all**`, `processing-categories`:`**Any/all**` |

#### User Data Categories

> Data related to the user of the system
> The "User" data category has two important subcategories for derived and provided data
> In turn, derived and provided both have subcategories for identifiable and nonidentifiable data, to make it clear what data is considered identifiable in your systems

#### User Derived Data

> Data derived from user provided data or as a result of user actions in the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **user.derived** | **identifiable**  | Derived data that is linked to, or identifies a user | `data-categories`:`**Any/all**`, provenance:`DERIVED` |
| **user.derived.identifable** | **biometric_health**  | Encoded characteristic collected about a user | `data-categories`:`BIOMETRIC`,`HEALTH`, provenance:`DERIVED` |
| **user.derived.identifable** | **browsing_history**  | Content browsing history of a user | `data-categories`:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **contact**  | Contact data collected about a user | `data-categories`:`CONTACT`,provenance:`DERIVED` |
| **user.derived.identifable** | **demographic**  | Demographic data about a user | `data-categories`:`DEMOGRAPHIC`, provenance:`DERIVED` |
| **user.derived.identifable** | **gender**  | Gender of an individual | `data-categories`:`DEMOGRAPHIC.GENDER`, provenance:`DERIVED` |
| **user.derived.identifable** | **location**  | Records of the location of a user | `data-categories`:`LOCATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **media_consumption**  | Media type consumption data of a user | `data-categories`:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **non_specific_age**  | Age range data | `data-categories`:`DEMOGRAPHIC.AGE`, provenance:`DERIVED` |
| **user.derived.identifable** | **observed**  | Data collected through observation of use of the system | `data-categories`:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **organization**  | Derived data that is linked to, or identifies an organization | `data-categories`:`AFFILIATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **profiling**  | Preference and interest data about a user | `data-categories`:`BEHAVIOR.PREFERENCE` (/!\ not same meaning for our PROFILING cat), provenance:`DERIVED`  |
| **user.derived.identifable** | **race**  | Racial or ethnic origin data | `data-categories`:`DEMOGRAPHIC.RACE`, provenance:`DERIVED` |
| **user.derived.identifable** | **religious_belief**  | Religion or religious belief | `data-categories`:`DEMOGRAPHIC.BELIEFS`, provenance:`DERIVED` |
| **user.derived.identifable** | **search_history**  | Records of search history and queries of a user | `data-categories`:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **sexual_orientation**  | Personal sex life or sexual data | `data-categories`:`DEMOGRAPHIC.SEXUAL-ORIENTATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **social**  | Social activity and interaction data | `data-categories`:`RELATIONSHIPS`, provenance:`DERIVED` |
| **user.derived.identifable** | **telemetry**  | User identifiable measurement data from system sensors and monitoring | `data-categories`:`BEHAVIOR.TELEMETRY`, provenance:`DERIVED` |
| **user.derived.identifable** | **unique_id**  | Unique identifier for a user assigned through system use | `data-categories`:`UID`, provenance:`DERIVED` |
| **user.derived.identifable** | **user_sensor**  | Measurement data derived about a user's environment through system use | `data-categories`:`BEHAVIOR`,`COLLECTION`, provenance:`DERIVED` |
| **user.derived.identifable** | **workplace**  | Organization of employment | `data-categories`:`AFFILIATION.WORK`, provenance:`DERIVED` |
| **user.derived.identifable** | **device**  | Data related to a user's device, configuration and setting | `data-categories`:`DEVICE`, provenance:`DERIVED` |
| **user.derived.identifable** | **cookie_id**  | Cookie unique identification number | `data-categories`:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **device_id**  | Device unique identification number | `data-categories`:`DEVICE`, provenance:`DERIVED` |
| **user.derived.identifable** | **ip_address**  | Unique identifier related to device connection | `data-categories`:`DEVICE`, provenance:`DERIVED` |
| **user.derived** | **nonidentifiable**  | Non-user identifiable data derived related to a user as a result of user actions in the system | `data-categories`:`OTHER-DATA`, provenance:`DERIVED` |
| **user.derived.nonidentifiable** | **nonsensor**  | Non-user identifiable measurement data derived from sensors and monitoring systems | `data-categories`:`OTHER-DATA`, provenance:`DERIVED` |

#### User Provided Data

> Data provided or created directly by a user of the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **user.provided** | **identifiable**  | Data provided or created directly by a user that is linked to or identifies a user | `data-categories`:`**any/all**`, provenance:`USER` |
| **user.provided.identifiable** | **identifiable**  | Encoded characteristics provided by a user | data-categories :`**any/all**`, provenance:`USER`|
| **user.provided.identifiable** | **children**  | Data relating to children | `data-categories` :`**any/all**`, provenance:`USER` @milstan: I don't think the fact someone is a child makes it a separate Data Category. The same person can turn 18 and no longer be a child - and data category can't change due to that. So this should be the responsibility of the System to use AGE to determine if special child-related policies must apply. |
| **user.provided.identifiable** | **health_and_medical**  | Health records or individual's personal medical information | `data-categories` :`HEALTH` provenance:`USER` |
| **user.provided.identifiable** | **job_title**  | Professional data | `data-categories` :`CONTACT`, provenance:`USER` |
| **user.provided.identifiable** | **name**  | User's real name | `data-categories` :`NAME`, provenance:`USER` |
| **user.provided.identifiable** | **non_specific_age**  | Age range data | `data-categories` :`DEMOGRAPHIC.AGE`, provenance:`USER` |
| **user.provided.identifiable** | **political_opinion**  | Data related to the individual's political opinions | `data-categories` :`DEMOGRAPHIC.BELIEFS`, provenance:`USER` |
| **user.provided.identifiable** | **race**  | Racial or ethnic origin data | `data-categories` :`DEMOGRAPHIC.RACE`, provenance:`USER` |
| **user.provided.identifiable** | **religious_belief**  | Religion or religious belief | `data-categories` :`DEMOGRAPHIC.BELIEFS`, provenance:`USER` |
| **user.provided.identifiable** | **sexual_orientation**  | Personal sex life or sexual data | `data-categories` :`DEMOGRAPHIC.SEXUAL-ORIENTATION`, provenance:`USER` |
| **user.provided.identifiable** | **workplace**  | Organization of employment | `data-categories` :`AFFILIATION.WORK`, provenance:`USER` |
| **user.provided.identifiable** | **date_of_birth**  | User's date of birth | `data-categories` :`DEMOGRAPHIC.AGE`, provenance:`USER` |
| **user.provided.identifiable** | **gender**  | Gender of an individual | `data-categories` :`DEMOGRAPHIC.GENDER`, provenance:`USER` |
| **user.provided.identifiable** | **genetic**  | Data about the genetic makeup provided by a user | `data-categories` :`GENETIC`, provenance:`USER` |
| **user.provided.identifiable** | **contact**  | User provided contact data for purposes other than account management | `data-categories` :`CONTACT`, provenance:`USER` |
| **user.provided.identifiable** | **city**  | User's city level address data | `data-categories` :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **country**  | User's country level address data | `data-categories` :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **email**  | User's provided email address | `data-categories` :`CONTACT.EMAIL`, provenance:`USER` |
| **user.provided.identifiable** | **phone_number**  | User's phone number | `data-categories` :`CONTACT.PHONE`, provenance:`USER` |
| **user.provided.identifiable** | **postal_code**  | User's postal code | `data-categories` :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **state**  | User's state level address data | `data-categories` :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **street**  | User's street level address data | `data-categories` :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **credentials**  | User provided authentication data | `data-categories` :`UID.USER-ACCOUNT`, provenance:`USER` |
| **user.provided.identifiable** | **biometric_credentials**  | User provided authentication data | `data-categories` :`UID.USER-ACCOUNT`,`BIOMETRIC`, provenance:`USER` |
| **user.provided.identifiable** | **password**  | Password for system authentication | `data-categories` :`UID.USER-ACCOUNT`, provenance:`USER` |
| **user.provided.identifiable** | **financial**  | Payment data and financial history | `data-categories` :`FINANCIAL`, provenance:`USER` |
| **user.provided.identifiable** | **account_number**  | User's account number for a payment card, bank account, or other financial system | `data-categories` :`FINANCIAL.BANK-ACCOUNT`, provenance:`USER` |
| **user.provided.identifiable** | **government_id**  | State provided identification data | `data-categories` :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **drivers_license_number**  | State issued driving identification number | `data-categories` :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **national_identification_number**  | State issued personal identification number |`data-categories` :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **passport_number**  | State issued passport data | `data-categories` :`UID.ID`, provenance:`USER` |
| **user.provided** | **nonidentifiable**  | Data provided or created directly by a user that is not identifiable | `data-categories` :`OTHER-DATA`, provenance:`USER` |

### Transcend

Transcend proposes the following [action (demand) types](https://github.com/transcend-io/privacy-types/blob/main/src/actions.ts):
| Transcend Demand Type | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| ACCESS | Data Download request | action:`ACCESS` |
| ERASURE | Erase the file completely | action:`DELETE`, other properties:`Data-identifier` |
| ACCOUNT_DELETION | Run an account deletion instead of a fully compliant deletion | action:`DELETE`, other properties: `Data-identifier` |
| AUTOMATED_DECISION_MAKING_OPT_OUT | Opt out of automated decision making | action:`RESTRICT`, processing-categories:`AUTOMATED-DECISION-MAKING`|
| CONTACT_OPT_OUT | A contact opt out request | action:`RESTRICT`, `data-categories`:`CONTACT`, `processing-categories`:`USING`, purpose:`MARKETING`|
| SALE_OPT_OUT | Opt-out of the sale of personal data | action:`RESTRICT`, `processing-categories`:`SHARE`, purpose:`SALE` |
| TRACKING_OPT_OUT | A tracking opt out request | action:`RESTRICT`, `processing-categories`:`COLLECTION`, purpose:`TRACKING` |
| RECTIFICATION | Make an update to an inaccurate record | action:`MODIFY`, other properties: `Selector.to-modify`,`Data.rectified` |
| RESTRICTION | A restriction of processing request | action:`RESTRICT` |

All of those can be modeled using our Demand Types.

Transcend proposes the following [treatment types](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Transcend Treatment Type | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| ESSENTIAL | Provide a service that the user explicitly requests and that is part of the product's basic service or functionality| `processing-categories`:`**any/all**`, purpose:`SERVICES.BASIC-SERVICE` |
| ADDITIONAL_FUNCTIONALITY | Provide a service that the user explicitly requests but that is not a necessary part of the product's basic service | `processing-categories`:`**any/all**`, purpose:`SERVICES.ADDITIONAL-SERVICE` |
| ADVERTISING | To show ads that are either targeted to the specific user or not targeted | `processing-categories`:`**any/all**`, purpose:`ADVERTISING` |
| MARKETING | To contact the user to offer products, services, or other promotions | `processing-categories`:`**any/all**`, purpose:`MARKETING` |
| ANALYTICS | For understanding the product’s audience, improving the product, inform company strategy, or general research | `processing-categories`:`**any/all**`, purpose:`RESEARCH` |
| PERSONALIZATION | For providing user with a personalized experience | `processing-categories`:`**any/all**`, purpose:`PERSONALIZATION` |
| OPERATION_SECURITY | For product operation and security, enforcement of terms of service, fraud prevention, protecting users and property, etc. | `processing-categories`:`**any/all**`, purpose:`SECURITY` |
| LEGAL | For compliance with legal obligations | `processing-categories`:`**any/all**`, purpose:`COMPLIANCE` |
| TRANSFER | For data that was transferred as part of a change in circumstance (e.g. a merger or acquisition) | `processing-categories`:`COLLECTION`, provenance:`TRANSFERRED` |
| SALE | For selling the data to third parties | `processing-categories`:`**any/all**`, purpose:`SALE` |
| HR | For personnel training, recruitment, payroll, management, etc. | `processing-categories`:`**any/all**`, purpose:`EMPLOYMENT` |
| OTHER | Other specific purpose not covered above | `processing-categories`:`**any/all**`, purpose:`OTHER-PURPOSE` use `message` to specify|
| UNSPECIFIED | The purpose is not explicitly stated or is unclear | `processing-categories`:`**any/all**`, purpose:`OTHER-PURPOSE` use `message` to specify|

All of those SHOULD be modeled using our Treatment Types.

Transcend proposes the following [data categories](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Transcend Data Category | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| FINANCIAL | Financial information | `data-categories`:`FINANCIAL` |
| HEALTH | Health information | `data-categories`:`HEALTH` |
| CONTACT | Contact information | `data-categories`:`CONTACT` |
| LOCATION |  Geo-location information | `data-categories`:`LOCATION` |
| DEMOGRAPHIC | Demographic Information | `data-categories`:`DEMOGRAPHIC` |
| ID | Identifiers that uniquely identify a person | `data-categories`:`UID` |
| ONLINE_ACTIVITY | The user's online activities on the first party website/app or other websites/apps | `data-categories`:`BEHAVIOR.ACTIVITY` |
| USER_PROFILE | he user’s profile on the first-party website/app and its contents | `data-categories`:`UID.USER-ACCOUNT` |
| SOCIAL_MEDIA | User profile and data from a social media website/app or other third party service | `data-categories`:`UID.SOCIAL-MEDIA` |
| CONNECTION | Connection information for the current browsing session, e.g. device IDs, MAC addresses, IP addresses, etc. | `data-categories`:`DEVICE`,`BEHAVIOR.CONNECTION` |
| TRACKING | Cookies and tracking elements | `data-categories`:`BEHAVIOR`, purpose:`TRACKING` |
| DEVICE | Computer or device information | `data-categories`:`DEVICE` |
| SURVEY | Any data that is collected through surveys | `data-categories`:`OTHER-DATA` |
| OTHER | A specific type of information not covered by the above categories | `data-categories`:`OTHER-DATA` use `message` to specify|
| UNSPECIFIED | The type of information is not explicitly stated or unclear| `data-categories`:`OTHER-DATA` use `message` to specify|

### UROPA

[UROPA](https://github.com/uropa-project/uropa) defines the following JSON enum values that can be mapped to PRIV Terms:

| UROPA [collectionMean](https://gdpr.stoplight.io/docs/uropa/922d9e36659fd-data-type) | PRIV [Provenance Terms](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#provenance-categories) |
| -------------- | ------------------ |
| `generated` | `DERIVED` |
| `computed` | `DERIVED`|
| `submitted` | `USER` |
| *not supported* | `TRANSFERRED` |

It is possible to model subcategory terms `DERIVED.GENERATED` and `DERIVED.COMPUTED` for the purposes of interoperability with UROPA.

| UROPA [Legal Bases](https://github.com/uropa-project/uropa/blob/main/src/LegalBasis.json) | PRIV [Legal Base Terms](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#legal-bases) |
| -------------- | ------------------ |
| `contract` | `CONTRACT` |
| `consent` | `CONSENT`|
| `legitimate interest` | `LEGITIMATE-INTEREST` |
| `legal obligation` | `NECESSARY.LEGAL-OBLIGATION` |
| `vital interest` | `NECESSARY.VITAL-INTEREST` |
| `public interest task` | `NECESSARY.PUBLIC-INTEREST` |
| *not supported* | `OTHER-LEGAL-BASE` |

### Data Rights Protocol

[Data Rights Protocol](https://github.com/consumer-reports-digital-lab/data-rights-protocol#303-schema-status-of-a-data-subject-exercise-request) defines behavior of endpoints working with privacy metadata.
It can be used in conjunction with PRIV.

DRP is principally focused on CCPA and its vocabulary is not rich enough to support the needs of other legislations such as GDPR.
Its semantics is also not rich enough to support the level of automation that PRIV can deliver.

It contains two components, a Protocol (Endpoint Specification) and a Vocabulary (Data Schemas).

#### DRP Endpoint Specification

The [Endpoint Specification](https://github.com/consumer-reports-digital-lab/data-rights-protocol#20-http-endpoint-specification) part of DRP is compatible with PRIV, because both use UUIDs to identify Privacy Requests.
Endpoints using PRIV can implement this Protocol to exchange PRIV objects instead of DRP Data Schema Objects.
This may turn out handy for Systems that operate in a client-server setting.

For a more peer-to-peer architecture, and full support for the exchange of the whole variety of PRIV events, Systems can opt to implement the [Privacy Request Multicast Protocol](./protocols/RFC-PRMP.md).


#### DRP Data Schemas

The [Data Schemas](https://github.com/consumer-reports-digital-lab/data-rights-protocol#30-data-schemas) part of DRP is focused on CCPA and only covers a fraction of the scope covered by PRIV.
Systems using DRP can export their data in PRIV and communicate with Systems using PRIV by using the following mapping.

##### Actions for CCPA

| DRP Data Schemas Action | PRIV Representation |
| :---: | :--- |
| sale:opt_out | priv:`action`: `OBJECT` |
| sale:opt_in | priv:[Cosent](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#consent) |
| deletion | priv:`action`: `DELETE` |
| access | priv:`action`: `ACCESS` |
| access:categories | priv:`action`: `ACCESS`, `restrictions`:[Privacy Scope Restriction](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#privacy-scope) |
| access:specific | priv:`action`: `ACCESS`, `restrictions`:[Demand Restrictions](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#demand-restrictions)|

##### Statuses

| DRP Data Schemas State | PRIV [Status](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#statuses) |
| :---: | :--- |
| open | `UNDER-REVIEW` |
| in_progress | `UNDER-REVIEW` |
| fulfilled | `GRANTED` |
| revoked | `CANCELED` |
| denied | `DENIED` |
| expired | `UNDER-REVIEW`, passed due date |


##### Motives

| DRP Data Schemas Reason | PRIV [Motives](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#motives) |
| :---: | :--- |
| need_user_verification | - |
| suspected_fraud | `IDENTITY-UNCONFIRMED` |
| insuf_verification | `IDENTITY-UNCONFIRMED` |
| no_match | `USER-UNKNOWN` |
| claim_not_covered | `VALID-REASON` |
| outside_jurisdiction | `VALID-REASON` |
| too_many_requests | `OTHER-MOTIVE` |
| other | `OTHER-MOTIVE` |
