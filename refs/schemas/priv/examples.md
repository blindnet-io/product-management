# Privacy Request Interchange Vocabulary : Examples

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Updated**   | 2022-05-25                                                                             |

## Introduction

This document examines how the [Privacy Request Interchange Vocabulary](./RFC-PRIV.md) can be used to represent Privacy Requests:
- introduced by the [supported legislation](#supported-legislation),
- illustrated by tutorials and request templates from regulatory bodies (e.g. [CNIL](https://www.cnil.fr/)),
- or made possible by existing software solutions with which interoperability SHOULD be achieved (e.g. Transcend, Alias.dev)  


## Motivation

Elaborating the examples in detail should allow us to test the Privacy Request Interchange Vocabulary for exhaustivity.

## Terminology

>**TBD**

- We use the term Privacy Request interchangeably with the (deprecated) terms Rights Request and Data Rights Request as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Individual, Person, You, and Data Subject as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv)
- We use the term System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)
- We use the terms Organization, Submitter, Data Consumer as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv) as defined there.


## Examples

In the following examples we show how, requests introduced by different regulations and systems can be modeled using the Privacy Request Interchange Vocabulary.

### BASIC GDPR REQUESTS

#### Articles 13 and 14

*...the controller shall, ..., provide the data subject with all of the following information:*

| Law | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.13.1.a`, `GDPR.14.1.a` | the identity and the contact details of the controller and, where applicable, of the controller’s representative | action:`TRANSPARENCY.ORGANISATION` |
| `GDPR.13.1.b`, `GDPR.14.1.b` | the contact details of the data protection officer, where applicable; | action:`TRANSPARENCY.DPO` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | the purposes of the processing for which the personal data are intended  | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | ... legal basis for the processing | action:`TRANSPARENCY.LEGAL-BASES` |
| `GDPR.13.1.d`, `GDPR.14.1.d` | where the processing is based on point (f) of Article 6(1), the legitimate interests pursued by the controller or by a third party | action:`TRANSPARENCY.LEGAL-BASES` |
| `GDPR.13.1.e`, `GDPR.14.1.e` | the recipients or categories of recipients of the personal data, if any; | action:`TRANSPARENCY.WHO` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | where applicable, the fact that the controller intends to transfer personal data to a third country or international organisation | action:`TRANSPARENCY.WHERE` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | the existence or absence of an adequacy decision by the Commission, or in the case of transfers referred to in Article 46 or 47, or the second subparagraph of Article 49(1), reference to the appropriate or suitable safeguards and the means by which to obtain a copy of them or where they have been made available. | action:`OTHER-DEMAND` |
| `GDPR.13.2.a`, `GDPR.14.2.a` | the period for which the personal data will be stored, or if that is not possible, the criteria used to determine that period | action:`TRANSPARENCY.RETENTION` |
| `GDPR.13.2.b`, `GDPR.14.2.b` | the existence of the right to request from the controller access to and rectification or erasure of personal data or restriction of processing concerning the data subject or to object to processing as well as the right to data portability | action:`TRANSPARENCY.POLICY` |
| `GDPR.13.2.c`, `GDPR.14.2.c` | where the processing is based on point (a) of Article 6(1) or point (a) of Article 9(2), the existence of the right to withdraw consent at any time, without affecting the lawfulness of processing based on consent before its withdrawal | action:`TRANSPARENCY.POLICY` |
| `GDPR.13.2.d`, `GDPR.14.2.d` | the right to lodge a complaint with a supervisory authority | action:`TRANSPARENCY.POLICY` |
| `GDPR.13.2.e`, `GDPR.14.2.e` | whether the provision of personal data is a statutory or contractual requirement, or a requirement necessary to enter into a contract, as well as whether the data subject is obliged to provide the personal data  | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.13.2.e`, `GDPR.14.2.e` | ... and of the possible consequences of failure to provide such data | action:`TRANSPARENCY.POLICY` |
| `GDPR.13.2.f`, `GDPR.14.2.f` | the existence of automated decision-making, including profiling | action:`TRANSPARENCY.PROCESSING` |
| `GDPR.13.2.f`, `GDPR.14.2.g` | the existence of automated decision-making, including profiling, referred to in Article 22(1) and (4) and, at least in those cases, meaningful information about the logic involved, as well as the significance and the envisaged consequences of such processing for the data subject. | action:`TRANSPARENCY.POLICY` |
| `GDPR.14.2.f` | from which source the personal data originate, and if applicable, whether it came from publicly accessible sources; | action:`TRANSPARENCY.PROVENANCE` |

#### Article 15.1

*The data subject shall have the right to obtain from the controller confirmation as to whether or not personal data concerning him or her are being processed*

| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.15.1` | confirmation as to whether or not personal data concerning him or her are being processed  | action:`TRANSPARENCY.KNOW` |

*and, where that is the case, access to the personal data and the following information:*

| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.15.1.a` | the purposes of the processing  | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.15.1.b` | the categories of personal data concerned | action:`TRANSPARENCY.DATA-CATEGORIES` |
| `GDPR.15.1.c` | the recipients or categories of recipient to whom the personal data have been or will be disclosed, in particular recipients in third countries or international organisations;  | action:`TRANSPARENCY.WHO` |
| `GDPR.15.1.d` | where possible, the envisaged period for which the personal data will be stored, or, if not possible, the criteria used to determine that period;  | action:`TRANSPARENCY.RETENTION` |
| `GDPR.15.1.e` | the existence of the right to request from the controller rectification or erasure of personal data or restriction of processing of personal data concerning the data subject or to object to such processing;  | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.1.f` | the right to lodge a complaint with a supervisory authority  | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.1.g` | where the personal data are not collected from the data subject, any available information as to their source  | action:`TRANSPARENCY.PROVENANCE` |
| `GDPR.15.1.h` | the existence of automated decision-making, including profiling  | action:`TRANSPARENCY.PROCESSING` |
| `GDPR.15.1.h` | the existence of automated decision-making, including profiling, referred to in Article 22(1) and (4) and, at least in those cases, meaningful information about the logic involved, as well as the significance and the envisaged consequences of such processing for the data subject  | action:`TRANSPARENCY.POLICY` |

>**Note**
>
> To make a request to know if the System has data on them (`GDPR.15.1`) and know about the purposes of processing of that data, the Data Subject MUST make a request with two demands, one `TRANSPARENCY.KNOW` and one `TRANSPARENCY.PURPOSE`
#### Article 15.2 and 15.3

| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.15.2` | Where personal data are transferred to a third country or to an international organisation, the data subject shall have the right to be informed of the appropriate safeguards pursuant to Article 46 relating to the transfer | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.3` | The controller shall provide a copy of the personal data undergoing processing | action:`ACCESS` |

#### Article 16-22

| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.16` | The data subject shall have the right to obtain from the controller without undue delay the rectification of inaccurate personal data concerning him or her. 2Taking into account the purposes of the processing, the data subject shall have the right to have incomplete personal data completed, including by means of providing a supplementary statement.  | action:`MODIFY` |
| `GDPR.17` | The data subject shall have the right to obtain from the controller the erasure of personal data concerning him | action:`DELETE` |
| `GDPR.18` | The data subject shall have the right to obtain from the controller restriction of processing | action:`RESTRICT` |
| `GDPR.20` | The data subject shall have the right to receive the personal data concerning him or her, which he or she has provided to a controller, in a structured, commonly used and machine-readable format and have the right to transmit those data to another controller without hindrance from the controller to which the personal data have been provided | action:`PORTABILITY` |
| `GDPR.21` | The data subject shall have the right to object, on grounds relating to his or her particular situation, at any time to processing of personal data concerning him or her which is based on point (e) or (f) of Article 6(1), including profiling based on those provisions.  *(note: 21.2 is not yet supported by the schema)*| action:`RESTRICT` |
| `GDPR.22` | The data subject shall have the right not to be subject to a decision based solely on automated processing, including profiling, which produces legal effects concerning him or her or similarly significantly affects him or her | action:`RESTRICT`, processing-category:`AUTOMATED-DECISION-MAKING` |



### GDPR REQUEST TEMPLATES FROM CNIL

| LAW | Demand | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.15` | [Acces](https://www.cnil.fr/fr/modele/courrier/exercer-son-droit-dacces) | action:`ACCESS` |
| `GDPR.15` | [Access to video surveillance data](https://www.cnil.fr/fr/modele/courrier/acceder-des-images-video-vous-concernant) from 01 Feb 2021 to 03 Feb 2021 | action:`ACCESS`, data-category:`IMAGE`, purpose:`SECURITY`, other-property:`from-to` |
| `Code de la santé publique art. L. 1111-7` | [Acces to my medical record](https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical) | action:`ACCESS`, data-category:`HEALTH` |
| `GDPR.15` | [Access to data "Preventel" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel) | action:`ACCESS` |
| `GDPR.15` | [Access to data a financial organization has on me](https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier): Access to all data the (financial)organization has on me, Provide with any available information on the origin of this data concerning me | action:`ACCESS`,`TRANSPARENCY.PROVENANCE` |
| `GDPR.15` | [Access to data "Fichier central des Chèques (FCC)" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-au-fichier-central-des-cheques-fcc) | action:`ACCESS` |
| `GDPR.15` | [Access to data "Fichier national des Incidents de remboursement de Crédit (FICP)](https://www.cnil.fr/fr/modele/courrier/acceder-aux-donnees-du-fichier-national-des-incidents-de-remboursement-de-credit) | action:`ACCESS` |
| `GDPR.15` | [Access to geolocation data or an access control device an organization has on me](https://www.cnil.fr/fr/modele/courrier/acceder-des-donnees-de-geolocalisation-ou-un-dispositif-de-controle-dacces) on a specific period of time | action:`ACCESS`, other-property:`from-to` |
| `GDPR.20` | [Exerce my right to portability](https://www.cnil.fr/fr/professionnels-comment-repondre-une-Demand-de-droit-la-portabilite) : Receive the data that concerns me to reuse them and transmit them to another data controller| action:`ACCESS`,`PORTABILITY` |
| `GDPR.16` | [Rectify incorrect data organization has on me](https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-inexactes)| action:`MODIFY`, other-property:`Selector.to-modify`,`data.rectified` |
| `GDPR.16` | [Rectify incomplete data organization has on me](https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-incompletes) | action:`MODIFY`, other-property:`Selector.to-modify`,`data.rectified` |
| `GDPR.17.1` | [Deletion](https://www.cnil.fr/fr/modele/courrier/supprimer-des-donnees-personnelles) | action:`DELETE`, message:`Reason of deletion`, other-property:`Data.identifier'(Information to delete-can be one or several data capture, or limited to a field , Data cat., Process cat. , Purpose, URL, ...)  |
| `GDPR.21.2` | [Stop receiving advertising from organization](https://www.cnil.fr/fr/modele/courrier/ne-plus-recevoir-de-publicites) | action:`DELETE`, data-category:`CONTACT`, purpose:`MARKETING` |
| `GDPR.17.1` | [Closing an online account](https://www.cnil.fr/fr/modele/courrier/cloturer-un-compte-en-ligne) | action:`OTHER-DATA` |
| `GDPR.21.1`,`GDPR.17.1.c` | [Delete my data that are published on a webiste](https://www.cnil.fr/fr/modele/courrier/supprimer-des-informations-vous-concernant-dun-site-internet) : Delete my data a website has published, Pages where my data appears are no longer referenced by search engines | action:`DELETE`, message:`Reason of deletion`, other-property:`Data.identifier`(data + URL) |
| `GDPR.21.1`,`GDPR.17.1.c` | [Removal of my image online](https://www.cnil.fr/fr/Demandr-le-retrait-de-votre-image-en-ligne) | action: `DELETE`, data-category:`IMAGE`, message:`Reason of deletion`, other-property:`Data.identifier`(data + URL) |
| `GDPR.21.2`,`GDPR.17.1`,`GDPR.19` | [Opposition to commercial prospecting](https://www.cnil.fr/fr/modele/courrier/sopposer-la-prospection-commerciale-par-telephone-sms-mail-courriers) : Opposition to treatment of all data the organization has on me for prospecting purpose, Deletion of my contact details from organization's prospecting files , Propagation of request | action:`RESTRICT`,`DELETE`, data-category:`CONTACT`, purpose:`MARKETING`, target: `ORGANISATION`,`PARTNERS`(propagation) |
| `GDPR.21.1`,`GDPR.17.1.c`,`GDPR.19` | [Opposition to treatment of all data an organization has on me](https://www.cnil.fr/fr/modele/courrier/sopposer-au-traitement-de-donnees) Opposition to treatment of all data the organization has on me, Deletion of all data the organization has on me, Propagation of request, Information on how long data will be kept on archive database if it is an organisation's legal obligation | action:`RESTRICT`,`DELETE`, message:`Reason of deletion`, other-property:`Data.identifier`,target:`ORGANISATION`,`PARTNERS`(propagation) |
| `GDPR.21`, GDPR.18.1 | [Limit the treatment (oppose to particular type of treatment) organization does on the data it has on me](https://www.cnil.fr/fr/le-droit-dopposition-refuser-lutilisation-de-vos-donnees) | action:`RESTRICT`, processing-category:`**any/all**` |
| `GDRP.4`,`GDRP.6`,`GDRP.7`, `GDPR.13.2.c`| [Revoke consent](https://www.cnil.fr/fr/les-bases-legales/consentement) : Revoke specific consent that I previously gave for a type of treatment on the data the organization has on me | action:`REVOKE-CONSENT`, processing-category:`**any/all**` |
| `GDPR.13.2.a`, `GDPR.14.2.a` | [For how long the data organization has on me will be kept](https://www.cnil.fr/fr/les-durees-de-conservation-des-donnees) | action:`TRANSPARENCY.RETENTION` |

>**Note**
>
>we need to add a schema field for providing data ranges (from date to date)

### OTHER EXAMPLES FROM DAILY LIFE

| LAW | Demand  | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.16` | Change my address, with new address being 1 blindnet street, 75000 blindcity, France, as of 01.01.2021  | action:`MODIFY`, data-category:`CONTACT.ADDRESS` |
| `GDPR.17` | Opt out of contact lists : Delete my contact details from all contact lists an ornaginzation has with my contact details | action:`DELETE`, data-category:`CONTACT`, purpose:`MARKETING` |
| `GDPR.21`,`GDPR.18.1` | Opt out of automated decision making | action:`RESTRICT`, processing-category:`AUTOMATED-DECISION-MAKING` |
| `GDPR.21`,`GDPR.18.1` | Opt out of sale of my data | action:`RESTRICT`, processing-category:`SHARING`, purpose`SALE` |
| `GDPR.21`,`GDPR.18.1` | Opt out of tracking on my data | action:`RESTRICT`, data-category:`BEHAVIOR`,`DEVICE`,`LOCATION`, processing-category:`COLLECTION`, purpose:`TRACKING` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | Storage information : know where is stored the data organization has on me | action:`TRANSPARENCY.WHERE` |
| `GDPR.14.1.e` | Accessibility information : know who can access the data organization has on me | action:`TRANSPARENCY.WHO` |
| `GDPR.14.2.f` | Provenance information : know the provenance of data organization has on me  | action:`TRANSPARENCY.PROVENANCE` | 
| `GDPR.13.2.a`, `GDPR.14.2.a` | Know when my data will be deleted | action:`TRANSPARENCY.RETENTION` |
| `**GDPR.13?**` | Know what is the policy of the organization to keep data it has on me | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.1.a` | Know the purpose of the processing organization does on the data it has on me | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.12.1` | Know what type(s) of treatment organization does on the data it has on me | action:`TRANSPARENCY.PROCESSING-CATEGORIES` |
| `GDPR.12.1` | Know if a particular type of treatment is done by organisation on the data it has on me | action:`TRANSPARENCY.PROCESSING-CATEGORIES`, processing-category:`**any/all**` |

>**Note**
>
>we need to add a schema field for providing new data, and date of validity of new data (not necessairly the date of trnasmission)

### CCPA REQUESTS
| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `CCPA.1798.100.1` | A consumer shall have the right to request that a business that collects a consumer’s personal information disclose to that consumer the categories and specific pieces of personal information the business has collected | action:`TRANSPARENCY.KNOWN`,`TRANSPARENCY.DATA-CATEGORIES` |
| `CCPA.1798.100.4` | A business that receives a verifiable consumer request from a consumer to access personal information shall promptly take steps to disclose and deliver, free of charge to the consumer, the personal information required by this section.  | action:`ACCESS` |
| `1798.105.1` | A consumer shall have the right to request that a business delete any personal information about the consumer which the business has collected from the consumer | action:`DELETE` |
| `1798.110.1.1` | A consumer shall have the right to request that a business that collects personal information about the consumer disclose to the consumer the following: The categories of personal information it has collected about that consumer | action:`TRANSPARENCY.DATA-CATEGORIES` | 
| `1798.110.1.2` | ...The categories of sources from which the personal information is collected | action:`TRANSPARENCY.PROVENANCE` |
| `1798.110.1.3` | ...The business or commercial purpose for collecting or selling personal information | action:`TRANSPARENCY.PURPOSE` |
| `1798.110.1.4` | ...The categories of third parties with whom the business shares personal information | action:`TRANSPARENCY.WHO` | `null` | processing-category:`SHARING`, `target`:`PARTNERS` |
| `1798.110.1.5` | ...The specific pieces of personal information it has collected about that consumer | action:`ACCESS` |
| `1798.115.1.1` | A consumer shall have the right to request that a business that sells the consumer’s personal information, or that discloses it for a business purpose, disclose to that consumer: The categories of personal information that the business collected about the consumer | action:`TRANSPARENCY.DATA-CATEGORIES`, processing-category:`SHARING`, purpose:`SALE` |
| `1798.115.1.2` | ...The categories of personal information that the business sold about the consumer and the categories of third parties to whom the personal information was sold, by category or categories of personal information for each category of third parties to whom the personal information was sold | action:`TRANSPARENCY.DATA-CATEGORIES`,`TRANSPARENCY.WHO`, processing-category:`SHARING`, purpose:`SALE` |
| `1798.115.1.3` | ...The categories of personal information that the business disclosed about the consumer for a business purpose | action:`TRANSPARENCY.DATA-CATEGORIES`, processing-category:`SHARING`, purpose:`SALE` |
| `1798.120.1` | A consumer shall have the right, at any time, to direct a business that sells personal information about the consumer to third parties not to sell the consumer’s personal information. This right may be referred to as the right to opt-out | action:`RESTRICT`, processing-category:`SHARING`, purpose:`SALE` |

### Alternatives Considered

#### Ethyca data categories

> [Ethyca data categories reference](https://ethyca.github.io/fideslang/data_categories/)

##### Account Data Categories
> Data related to an account on the system

###### Account Contact Data

| Ethyca Parent key | **Ethyca Label** | Ethyca Description |Representation |
|  ------------ | -------------------------------------- | ------------ | ------------ | 
| **account** | **Contact**  | Contact data related to a system account | data-category:`CONTACT` |
| **account.contact** | **email**  | Account's email address | data-category:`CONTACT.EMAIL` |
| **account.contact** | **phone_number**  | Account's phone number | data-category:`CONTACT.PHONE` |
| **account.contact** | **City**  | Account's city level address data | data-category:`CONTACT.ADDRESS` |
| **account.contact** | **Country**  | Account's country level address data | data-category:`CONTACT.ADDRESS` |
| **account.contact** | **postal_code**  | Account's postal code  | data-category:`CONTACT.ADDRESS` |
| **account.contact** | **state**  | Account's state level address data  | data-category:`CONTACT.ADDRESS` |
| **account.contact** | **street**  | Account's street level address | data-category:`CONTACT.ADDRESS` |
###### Account Payment Data
| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ | 
| **account** | **payment**  | Payment data related to system account | data-category:`FINANCIAL` | 
| **account.payment** | **financial_account_number**  | Payment data related to system account | data-category:`FINANCIAL.BANK-ACCOUNT` |

##### System Data Categories
> Data unique to, and under control of the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **system** | **authentication**  | Data used to manage access to the system | data-category:`OTHER-DATA` |
| **system** | **operations**  | Data used for system operations | data-category:`**Any/all**`, processing-category:`**Any/all**` |

##### User Data Categories
> Data related to the user of the system
> The "User" data category has two important subcategories for derived and provided data
> In turn, derived and provided both have subcategories for identifiable and nonidentifiable data, to make it clear what data is considered identifiable in your systems

###### User Derived Data
> Data derived from user provided data or as a result of user actions in the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ | 
| **user.derived** | **identifiable**  | Derived data that is linked to, or identifies a user | data-category:`**Any/all**`, provenance:`DERIVED` |
| **user.derived.identifable** | **biometric_health**  | Encoded characteristic collected about a user | data-category:`BIOMETRIC`,`HEALTH`, provenance:`DERIVED` |
| **user.derived.identifable** | **browsing_history**  | Content browsing history of a user | data-category:`BEHAVIOR`, provenance:`DERIVED` | 
| **user.derived.identifable** | **contact**  | Contact data collected about a user | data-category:`CONTACT`,provenance:`DERIVED` |
| **user.derived.identifable** | **demographic**  | Demographic data about a user | data-category:`DEMOGRAPHIC`, provenance:`DERIVED` |
| **user.derived.identifable** | **gender**  | Gender of an individual | data-category:`DEMOGRAPHIC.GENDER`, provenance:`DERIVED` |
| **user.derived.identifable** | **location**  | Records of the location of a user | data-category:`LOCATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **media_consumption**  | Media type consumption data of a user | data-category:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **non_specific_age**  | Age range data | data-category:`DEMOGRAPHIC.AGE`, provenance:`DERIVED` |
| **user.derived.identifable** | **observed**  | Data collected through observation of use of the system | data-category:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **organization**  | Derived data that is linked to, or identifies an organization | data-category:`AFFILIATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **profiling**  | Preference and interest data about a user | data-category:`BEHAVIOR.PREFERENCE` (/!\ not same meaning for our PROFILING cat), provenance:`DERIVED`  |
| **user.derived.identifable** | **race**  | Racial or ethnic origin data | data-category:`DEMOGRAPHIC.RACE`, provenance:`DERIVED` |
| **user.derived.identifable** | **religious_belief**  | Religion or religious belief | data-category:`DEMOGRAPHIC.BELIEFS`, provenance:`DERIVED` |
| **user.derived.identifable** | **search_history**  | Records of search history and queries of a user | data-category:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **sexual_orientation**  | Personal sex life or sexual data | data-category:`DEMOGRAPHIC.SEXUAL-ORIENTATION`, provenance:`DERIVED` |
| **user.derived.identifable** | **social**  | Social activity and interaction data | data-category:`BEHAVIOR.RELATIONSHIPS`, provenance:`DERIVED` |
| **user.derived.identifable** | **telemetry**  | User identifiable measurement data from system sensors and monitoring | data-category:`BEHAVIOR.TELEMETRY`, provenance:`DERIVED` |
| **user.derived.identifable** | **unique_id**  | Unique identifier for a user assigned through system use | data-category:`UID`, provenance:`DERIVED` |
| **user.derived.identifable** | **user_sensor**  | Measurement data derived about a user's environment through system use | data-category:`BEHAVIOR`,`COLLECTION`, provenance:`DERIVED` | 
| **user.derived.identifable** | **workplace**  | Organization of employment | data-category:`AFFILIATION.WORK`, provenance:`DERIVED` |
| **user.derived.identifable** | **device**  | Data related to a user's device, configuration and setting | data-category:`DEVICE`, provenance:`DERIVED` |
| **user.derived.identifable** | **cookie_id**  | Cookie unique identification number | data-category:`BEHAVIOR`, provenance:`DERIVED` |
| **user.derived.identifable** | **device_id**  | Device unique identification number | data-category:`DEVICE`, provenance:`DERIVED` |
| **user.derived.identifable** | **ip_address**  | Unique identifier related to device connection | data-category:`DEVICE`, provenance:`DERIVED` |
| **user.derived** | **nonidentifiable**  | Non-user identifiable data derived related to a user as a result of user actions in the system | `OTHER-DATA`, provenance:`DERIVED` |
| **user.derived.nonidentifiable** | **nonsensor**  | Non-user identifiable measurement data derived from sensors and monitoring systems | `OTHER-DATA`, provenance:`DERIVED` |

###### User Provided Data
> Data provided or created directly by a user of the system

| Ethyca Parent key | **Ethyca Label** | Ethyca Description | Representation |
| ------------ | -------------------------------------- | ------------ | ------------ |
| **user.provided** | **identifiable**  | Data provided or created directly by a user that is linked to or identifies a user | data-category :`**any/all**`, provenance:`USER` |
| **user.provided.identifiable** | **identifiable**  | Encoded characteristics provided by a user | data-category :`**any/all**`, provenance:`USER`|
| **user.provided.identifiable** | **children**  | Data relating to children | data-category :`**any/all**`, provenance:`USER` @milstan: I don't think the fact someone is a child makes it a separate Data Category. The same person can turn 18 and no longer be a child - and data category can't change due to that. So this should be the responsibility of the System to use AGE to determine if special child-related policies must apply. |
| **user.provided.identifiable** | **health_and_medical**  | Health records or individual's personal medical information | data-category :`HEALTH` provenance:`USER` |
| **user.provided.identifiable** | **job_title**  | Professional data | data-category :`CONTACT`, provenance:`USER` |
| **user.provided.identifiable** | **name**  | User's real name | data-category :`NAME`, provenance:`USER` | 
| **user.provided.identifiable** | **non_specific_age**  | Age range data | data-category :`DEMOGRAPHIC.AGE`, provenance:`USER` |
| **user.provided.identifiable** | **political_opinion**  | Data related to the individual's political opinions | data-category :`DEMOGRAPHIC.BELIEFS`, provenance:`USER` |
| **user.provided.identifiable** | **race**  | Racial or ethnic origin data | data-category :`DEMOGRAPHIC.RACE`, provenance:`USER` |
| **user.provided.identifiable** | **religious_belief**  | Religion or religious belief | data-category :`DEMOGRAPHIC.BELIEFS`, provenance:`USER` |
| **user.provided.identifiable** | **sexual_orientation**  | Personal sex life or sexual data | data-category :`DEMOGRAPHIC.SEXUAL-ORIENTATION`, provenance:`USER` | 
| **user.provided.identifiable** | **workplace**  | Organization of employment | data-category :`AFFILIATION.WORK`, provenance:`USER` |
| **user.provided.identifiable** | **date_of_birth**  | User's date of birth | data-category :`DEMOGRAPHIC.AGE`, provenance:`USER` | 
| **user.provided.identifiable** | **gender**  | Gender of an individual | data-category :`DEMOGRAPHIC.GENDER`, provenance:`USER` |
| **user.provided.identifiable** | **genetic**  | Data about the genetic makeup provided by a user | data-category :`GENETIC`, provenance:`USER` |
| **user.provided.identifiable** | **contact**  | User provided contact data for purposes other than account management | data-category :`CONTACT`, provenance:`USER` |
| **user.provided.identifiable** | **city**  | User's city level address data | data-category :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **country**  | User's country level address data | data-category :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **email**  | User's provided email address | data-category :`CONTACT.EMAIL`, provenance:`USER` |
| **user.provided.identifiable** | **phone_number**  | User's phone number | data-category :`CONTACT.PHONE`, provenance:`USER` |
| **user.provided.identifiable** | **postal_code**  | User's postal code | data-category :`CONTACT.ADDRESS`, provenance:`USER` | 
| **user.provided.identifiable** | **state**  | User's state level address data | data-category :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **street**  | User's street level address data | data-category :`CONTACT.ADDRESS`, provenance:`USER` |
| **user.provided.identifiable** | **credentials**  | User provided authentication data | data-category :`UID.USER-ACCOUNT`, provenance:`USER` | 
| **user.provided.identifiable** | **biometric_credentials**  | User provided authentication data | data-category :`UID.USER-ACCOUNT`,`BIOMETRIC`, provenance:`USER` |
| **user.provided.identifiable** | **password**  | Password for system authentication | data-category :`UID.USER-ACCOUNT`, provenance:`USER` |
| **user.provided.identifiable** | **financial**  | Payment data and financial history | data-category :`FINANCIAL`, provenance:`USER` |
| **user.provided.identifiable** | **account_number**  | User's account number for a payment card, bank account, or other financial system | data-category :`FINANCIAL.BANK-ACCOUNT`, provenance:`USER` |
| **user.provided.identifiable** | **government_id**  | State provided identification data | data-category :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **drivers_license_number**  | State issued driving identification number | data-category :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **national_identification_number**  | State issued personal identification number |data-category :`UID.ID`, provenance:`USER` |
| **user.provided.identifiable** | **passport_number**  | State issued passport data | data-category :`UID.ID`, provenance:`USER` |
| **user.provided** | **nonidentifiable**  | Data provided or created directly by a user that is not identifiable | data-category :`OTHER-DATA`, provenance:`USER` |

#### Transcend

Transcend proposes the following [action (demand) types](https://github.com/transcend-io/privacy-types/blob/main/src/actions.ts):
| Transcend Demand Type | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| ACCESS | Data Download request | action:`ACCESS` |
| ERASURE | Erase the file completely | action:`DELETE`, other properties:`Data-identifier` |
| ACCOUNT_DELETION | Run an account deletion instead of a fully compliant deletion | action:`DELETE`, other properties: `Data-identifier` |
| AUTOMATED_DECISION_MAKING_OPT_OUT | Opt out of automated decision making | action:`RESTRICT`, processing-categories:`AUTOMATED-DECISION-MAKING`|
| CONTACT_OPT_OUT | A contact opt out request | action:`RESTRICT`, data-category:`CONTACT`, processing-category:`USING`, purpose:`MARKETING`|
| SALE_OPT_OUT | Opt-out of the sale of personal data | action:`RESTRICT`, processing-category:`SHARE`, purpose:`SALE` |
| TRACKING_OPT_OUT | A tracking opt out request | action:`RESTRICT`, processing-category:`COLLECTION`, purpose:`TRACKING` |
| RECTIFICATION | Make an update to an inaccurate record | action:`MODIFY`, other properties: `Selector.to-modify`,`Data.rectified` |
| RESTRICTION | A restriction of processing request | action:`RESTRICT` |

All of those can be modeled using our Demand Types.

Transcend proposes the following [treatment types](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Transcend Treatment Type | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| ESSENTIAL | Provide a service that the user explicitly requests and that is part of the product's basic service or functionality| processing-category:`**any/all**`, purpose:`SERVICES.BASIC-SERVICE` |
| ADDITIONAL_FUNCTIONALITY | Provide a service that the user explicitly requests but that is not a necessary part of the product's basic service | processing-category:`**any/all**`, purpose:`SERVICES.ADDITIONAL-SERVICE` |
| ADVERTISING | To show ads that are either targeted to the specific user or not targeted | processing-category:`**any/all**`, purpose:`ADVERTISING` |
| MARKETING | To contact the user to offer products, services, or other promotions | processing-category:`**any/all**`, purpose:`MARKETING` |
| ANALYTICS | For understanding the product’s audience, improving the product, inform company strategy, or general research | processing-category:`**any/all**`, purpose:`RESEARCH` |
| PERSONALIZATION | For providing user with a personalized experience | processing-category:`**any/all**`, purpose:`PERSONALISATION` |
| OPERATION_SECURITY | For product operation and security, enforcement of terms of service, fraud prevention, protecting users and property, etc. | processing-category:`**any/all**`, purpose:`SECURITY` |
| LEGAL | For compliance with legal obligations | processing-category:`**any/all**`, purpose:`COMPLIANCE` |
| TRANSFER | For data that was transferred as part of a change in circumstance (e.g. a merger or acquisition) | processing-category:`COLLECTION`, provenance:`TRANSFERRED` |
| SALE | For selling the data to third parties | processing-category:`**any/all**`, purpose:`SALE` |
| HR | For personnel training, recruitment, payroll, management, etc. | processing-category:`**any/all**`, purpose:`EMPLOYMENT` |
| OTHER | Other specific purpose not covered above | processing-category:`**any/all**`, purpose:`OTHER-PURPOSE` |
| UNSPECIFIED | The purpose is not explicitly stated or is unclear | processing-category:`**any/all**`, purpose:`OTHER-PURPOSE` |

All of those SHOULD be modeled using our Treatment Types.

Transcend proposes the following [data categories](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Transcend Data Category | Transcend Description | Representation |
| -------------- | ----------------------------------------- | ------------------------ |
| FINANCIAL | Financial information | data-category:`FINANCIAL` |
| HEALTH | Health information | data-category:`HEALTH` |
| CONTACT | Contact information | data-category:`CONTACT` |
| LOCATION |  Geo-location information | data-category:`LOCATION` |
| DEMOGRAPHIC | Demographic Information | data-category:`DEMOGRAPHIC` |
| ID | Identifiers that uniquely identify a person | data-category:`UID` |
| ONLINE_ACTIVITY | The user's online activities on the first party website/app or other websites/apps | data-category:`BEHAVIOR.ACTIVITY` |
| USER_PROFILE | he user’s profile on the first-party website/app and its contents | data-category:`UID.USER-ACCOUNT` |
| SOCIAL_MEDIA | User profile and data from a social media website/app or other third party service | data-category:`UID.SOCIAL-MEDIA` |
| CONNECTION | Connection information for the current browsing session, e.g. device IDs, MAC addresses, IP addresses, etc. | data-category:`DEVICE`,`BEHAVIOR.CONNECTION` |
| TRACKING | Cookies and tracking elements | data-category:`BEHAVIOR`, purpose:`TRACKING` |
| DEVICE | Computer or device information | data-category:`DEVICE` |
| SURVEY | Any data that is collected through surveys | data-category:`OTHER-DATA` |
| OTHER | A specific type of information not covered by the above categories | data-category:`OTHER-DATA` |
| UNSPECIFIED | The type of information is not explicitly stated or unclear| data-category:`OTHER-DATA` |



## Questions and Discussion Topics



## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.

### Informative References

-

### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj), [CHAPTER III - Rights of the data subject](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre3#Article13)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5), [CCPA(more digestible format)](https://ccpa-info.com/california-consumer-privacy-act-full-text/)

### Yet to be Supported Legilsation

- [CPRA]([https://eur-lex.europa.eu/eli/reg/2016/679/oj](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf))
- [HIPPA]([https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5](https://www.govinfo.gov/content/pkg/PLAW-104publ191/pdf/PLAW-104publ191.pdf))
