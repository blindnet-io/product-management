# Privacy Request Interchange Vocabulary : Examples

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Updated**   | 2022-06-13                                                                             |

## Introduction

This document examines how the [Privacy Request Interchange Vocabulary](./RFC-PRIV.md) can be used to represent Privacy Requests:
- introduced by the [supported legislation](#supported-legislation),
- illustrated by tutorials and request templates from regulatory bodies (e.g. [CNIL](https://www.cnil.fr/)),
- or made possible by existing software solutions with which interoperability SHOULD be achieved (e.g. Transcend, Alias.dev)  

The document is not normative, and often uses inconsistent language and format. It serves in the design process in order to test the Privacy Request Interchange Vocabulary for exhaustivity. It can be archived once design is finished and tutorials made.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-architecture/)
- Privacy Compiler was formerly known as Data Rights Compiler
- Privacy Request was formerly known as Data Rights Request
- All the concepts, properties and [Terms](./RFC-PRIV.md#terms) listed in the [Proposal](./RFC-PRIV.md#proposal) section of PRIV(Privacy Request Interchange Vocabulary are to be interpreted as defined in [Privacy Request Interchange Vocabulary](./RFC-PRIV.md#proposal)

## Examples

In the following examples we show how, requests introduced by different regulations and systems can be modeled using the Privacy Request Interchange Vocabulary.

### BASIC GDPR REQUESTS

#### Articles 13 and 14

*...the controller shall, ..., provide the data subject with all of the following information:*

| Law | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.13.1.a`, `GDPR.14.1.a` | the identity and the contact details of the controller and, where applicable, of the controller’s representative | action:`TRANSPARENCY.ORGANIZATION` |
| `GDPR.13.1.b`, `GDPR.14.1.b` | the contact details of the data protection officer, where applicable; | action:`TRANSPARENCY.DPO` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | the purposes of the processing for which the personal data are intended  | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | ... legal basis for the processing | action:`TRANSPARENCY.LEGAL-BASES` |
| `GDPR.13.1.d`, `GDPR.14.1.d` | where the processing is based on point (f) of Article 6(1), the legitimate interests pursued by the controller or by a third party | action:`TRANSPARENCY.LEGAL-BASES` |
| `GDPR.13.1.e`, `GDPR.14.1.e` | the recipients or categories of recipients of the personal data, if any; | action:`TRANSPARENCY.WHO` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | where applicable, the fact that the controller intends to transfer personal data to a third country or international Organization | action:`TRANSPARENCY.WHERE` |
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
| `GDPR.15.1.c` | the recipients or categories of recipient to whom the personal data have been or will be disclosed, in particular recipients in third countries or international Organizations;  | action:`TRANSPARENCY.WHO` |
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
| `GDPR.15.2` | Where personal data are transferred to a third country or to an international Organization, the data subject shall have the right to be informed of the appropriate safeguards pursuant to Article 46 relating to the transfer | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.3` | The controller shall provide a copy of the personal data undergoing processing | action:`ACCESS` |

#### Article 16-22

| LAW | Demand (as introduced by regulation) | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.16` | The data subject shall have the right to obtain from the controller without undue delay the rectification of inaccurate personal data concerning him or her. 2Taking into account the purposes of the processing, the data subject shall have the right to have incomplete personal data completed, including by means of providing a supplementary statement.  | action:`MODIFY` |
| `GDPR.17` | The data subject shall have the right to obtain from the controller the erasure of personal data concerning him | action:`DELETE` |
| `GDPR.18` | The data subject shall have the right to obtain from the controller restriction of processing | action:`RESTRICT` |
| `GDPR.20` | The data subject shall have the right to receive the personal data concerning him or her, which he or she has provided to a controller, in a structured, commonly used and machine-readable format and have the right to transmit those data to another controller without hindrance from the controller to which the personal data have been provided | action:`PORTABILITY` |
| `GDPR.21` | The data subject shall have the right to object, on grounds relating to his or her particular situation, at any time to processing of personal data concerning him or her which is based on point (e) or (f) of Article 6(1), including profiling based on those provisions.  *(note: 21.2 is not yet supported by the schema)*| action:`OBJECT` |
| `GDPR.22` | The data subject shall have the right not to be subject to a decision based solely on automated processing, including profiling, which produces legal effects concerning him or her or similarly significantly affects him or her | action:`OBJECT`, `processing-categories`:`AUTOMATED-DECISION-MAKING` |



### GDPR REQUEST TEMPLATES FROM CNIL

| LAW | Demand | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.15` | [Acces](https://www.cnil.fr/fr/modele/courrier/exercer-son-droit-dacces) | action:`ACCESS` |
| `GDPR.15` | [Access to video surveillance data](https://www.cnil.fr/fr/modele/courrier/acceder-des-images-video-vous-concernant) from 01 Feb 2021 to 03 Feb 2021 | action:`ACCESS`, `data-categories`:`IMAGE`, purpose:`SECURITY`, Date Range restriction `from:2021-02-01` `to:2021-02-03` |
| `Code de la santé publique art. L. 1111-7` | [Acces to my medical record](https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical) | action:`ACCESS`, `data-categories`:`HEALTH` |
| `GDPR.15` | [Access to data "Preventel" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel) | action:`ACCESS` |
| `GDPR.15` | [Access to data a financial organization has on me](https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier): Access to all data the (financial)organization has on me, Provide with any available information on the origin of this data concerning me | action:`ACCESS`,`TRANSPARENCY.PROVENANCE` |
| `GDPR.15` | [Access to data "Fichier central des Chèques (FCC)" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-au-fichier-central-des-cheques-fcc) | action:`ACCESS` |
| `GDPR.15` | [Access to data "Fichier national des Incidents de remboursement de Crédit (FICP)](https://www.cnil.fr/fr/modele/courrier/acceder-aux-donnees-du-fichier-national-des-incidents-de-remboursement-de-credit) | action:`ACCESS` |
| `GDPR.15` | [Access to geolocation data or an access control device an organization has on me](https://www.cnil.fr/fr/modele/courrier/acceder-des-donnees-de-geolocalisation-ou-un-dispositif-de-controle-dacces) on a specific period of time | action:`ACCESS`, Date Range Restriction `from`,`to` |
| `GDPR.20` | [Exerce my right to portability](https://www.cnil.fr/fr/professionnels-comment-repondre-une-Demand-de-droit-la-portabilite) : Receive the data that concerns me to reuse them and transmit them to another data controller| action:`ACCESS`,`PORTABILITY` |
| `GDPR.16` | [Rectify incorrect data organization has on me](https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-inexactes)| action:`MODIFY`, `data-categories`: particular `selector` to modify, `data`: new data |
| `GDPR.16` | [Rectify incomplete data organization has on me](https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-incompletes) | action:`MODIFY`, `data-categories`: particular `selector` to modify, `data`: new data  |
| `GDPR.17.1` | [Deletion](https://www.cnil.fr/fr/modele/courrier/supprimer-des-donnees-personnelles) | action:`DELETE`,`data-categories`: category or particular `selector` of the data to be deleted, or any Capture Restriction or Date Range Restriction, (optional) `message`:Reason of deletion   |
| `GDPR.21.2` | [Stop receiving advertising from organization](https://www.cnil.fr/fr/modele/courrier/ne-plus-recevoir-de-publicites) | action:`OBJECT`, `data-categories`:`CONTACT`, purpose:`ADVERTISING` |
| `GDPR.17.1` | [Closing an online account](https://www.cnil.fr/fr/modele/courrier/cloturer-un-compte-en-ligne) | `action`:`DELETE`,``data-categories``: `UID.USER-ACCOUNT` |
| `GDPR.21.1`,`GDPR.17.1.c` | [Delete my data that are published on a webiste](https://www.cnil.fr/fr/modele/courrier/supprimer-des-informations-vous-concernant-dun-site-internet) : Delete my data a website has published, Pages where my data appears are no longer referenced by search engines | action:`DELETE`, Data Reference Restriction (`data-reference`: concrete URLs), optional `message`:Reason of deletion, |
| `GDPR.21.1`,`GDPR.17.1.c` | [Removal of my image online](https://www.cnil.fr/fr/Demandr-le-retrait-de-votre-image-en-ligne) | action: `DELETE`, `data-categories`:`IMAGE`, Data Reference Restriction (`data-reference`: concrete URLs), (optional) message:`Reason of deletion` |
| `GDPR.21.2`,`GDPR.17.1`,`GDPR.19` | [Opposition to commercial prospecting](https://www.cnil.fr/fr/modele/courrier/sopposer-la-prospection-commerciale-par-telephone-sms-mail-courriers) : Opposition to treatment of all data the organization has on me for prospecting purpose, Deletion of my contact details from organization's prospecting files , Propagation of request | action:`OBJECT`(purpose:`MARKETING`), action:`DELETE`(`data-categories`:`CONTACT`), , target: `ORGANIZATION`,`PARTNERS`(propagation) |
| `GDPR.21.1`,`GDPR.17.1.c`,`GDPR.19` | [Opposition to treatment of all data an organization has on me](https://www.cnil.fr/fr/modele/courrier/sopposer-au-traitement-de-donnees) Opposition to treatment of all data the organization has on me, Deletion of all data the organization has on me, Propagation of request, Information on how long data will be kept on archive database if it is an Organization's legal obligation | action:`TRANSPARENCY.RETENTION`; action:`DELETE`, target:`ORGANIZATION`,`PARTNERS`(propagation); action:`OBJECT` |
| `GDPR.21`, GDPR.18.1 | [Limit the processing (oppose to particular type of processing) organization does on the data it has on me](https://www.cnil.fr/fr/le-droit-dopposition-refuser-lutilisation-de-vos-donnees) | action:`OBJECT` |
| `GDRP.4`,`GDRP.6`,`GDRP.7`, `GDPR.13.2.c`| [Revoke consent](https://www.cnil.fr/fr/les-bases-legales/consentement) : Revoke specific consent that I previously gave for a type of treatment on the data the organization has on me | action:`REVOKE-CONSENT`, Consent Restriction |
| `GDPR.13.2.a`, `GDPR.14.2.a` | [For how long the data organization has on me will be kept](https://www.cnil.fr/fr/les-durees-de-conservation-des-donnees) | action:`TRANSPARENCY.RETENTION` |

>**Note**
>
>we need to add a schema field for providing data ranges (from date to date)

### OTHER EXAMPLES FROM DAILY LIFE

| LAW | Demand  | Representation |
| -------- | ----------------------------------------------------- | ------------ |
| `GDPR.16` | Change my address, with new address being 1 blindnet street, 75000 blindcity, France, as of 01.01.2021  | action:`MODIFY`, `data-categories`:`CONTACT.ADDRESS`, `data`:1 blindnet street, 75000 blindcity, France , `message`: as of 01.01.2021 (*NB: can't be modeled as a Date Range as Data Ragnge MUST resolve to particular Data Capture Fragments*)|
| `GDPR.17` | Opt out of contact lists : Delete my contact details from all contact lists an ornaginzation has with my contact details | action:`DELETE`, `data-categories`:`CONTACT`; action:`OBJECT` (`purpose`:`MARKETING`, `ADVERTISING`) |
| `GDPR.21`,`GDPR.18.1` | Opt out of automated decision making | action:`OBJECT`, `processing-categories`:`AUTOMATED-DECISION-MAKING` |
| `GDPR.21`,`GDPR.18.1` | Opt out of sale of my data | action:`OBJECT`, purpose`SALE` |
| `GDPR.21`,`GDPR.18.1` | Opt out of tracking on my data | action:`OBJECT`, `data-categories`:`BEHAVIOR`,`DEVICE`,`LOCATION`, `processing-categories`:`COLLECTION`, purpose:`TRACKING` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | Storage information : know where is stored the data organization has on me | action:`TRANSPARENCY.WHERE` |
| `GDPR.14.1.e` | Accessibility information : know who can access the data organization has on me | action:`TRANSPARENCY.WHO` |
| `GDPR.14.2.f` | Provenance information : know the provenance of data organization has on me  | action:`TRANSPARENCY.PROVENANCE` |
| `GDPR.13.2.a`, `GDPR.14.2.a` | Know when my data will be deleted | action:`TRANSPARENCY.RETENTION` |
| `**GDPR.13?**` | Know what is the policy of the organization to keep data it has on me | action:`TRANSPARENCY.POLICY` |
| `GDPR.15.1.a` | Know the purpose of the processing organization does on the data it has on me | action:`TRANSPARENCY.PURPOSE` |
| `GDPR.12.1` | Know what type(s) of treatment organization does on the data it has on me | action:`TRANSPARENCY.PROCESSING-CATEGORIES` |
| `GDPR.12.1` | Know if a particular type of treatment is done by Organization on the data it has on me | action:`TRANSPARENCY.PROCESSING-CATEGORIES`, `processing-categories`:`**any/all**` |

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
| `1798.110.1.4` | ...The categories of third parties with whom the business shares personal information | action:`TRANSPARENCY.WHO` `processing-categories`:`SHARING`|
| `1798.110.1.5` | ...The specific pieces of personal information it has collected about that consumer | action:`ACCESS` |
| `1798.115.1.1` | A consumer shall have the right to request that a business that sells the consumer’s personal information, or that discloses it for a business purpose, disclose to that consumer: The categories of personal information that the business collected about the consumer | action:`TRANSPARENCY.DATA-CATEGORIES`, `processing-categories`:`SHARING`, purpose:`SALE` |
| `1798.115.1.2` | ...The categories of personal information that the business sold about the consumer and the categories of third parties to whom the personal information was sold, by category or categories of personal information for each category of third parties to whom the personal information was sold | action:`TRANSPARENCY.DATA-CATEGORIES`,`TRANSPARENCY.WHO`, `processing-categories`:`SHARING`, purpose:`SALE` |
| `1798.115.1.3` | ...The categories of personal information that the business disclosed about the consumer for a business purpose | action:`TRANSPARENCY.DATA-CATEGORIES`, `processing-categories`:`SHARING`, purpose:`SALE` |
| `1798.120.1` | A consumer shall have the right, at any time, to direct a business that sells personal information about the consumer to third parties not to sell the consumer’s personal information. This right may be referred to as the right to opt-out | action:`RESTRICT`, `processing-categories`:`SHARING`, purpose:`SALE` |


### HIPPA

The following correspondence of [data categories](https://www.luc.edu/its/aboutits/itspoliciesguidelines/hipaainformation/18hipaaidentifiers/) needed for [HIPPA](https://www.hhs.gov/hipaa) compliance can be used:

| HIPPA Category | PRIV Data Category |
| -------------- | ------------------ |
| Name | `NAME` |
| Address (all geographic subdivisions smaller than state, including street address, city county, and zip code) | `CONTACT.ADDRESS` |
| All elements (except years) of dates related to an individual (including birthdate, admission date, discharge date, date of death, and exact age if over 89) | `DEMOGRAPHIC.AGE` for birth date, death date, recommended `selector` for admission date `BEHAVIOR.ACTIVITY.ADMISSION`, discharge date  `BEHAVIOR.ACTIVITY.DISCHARGE`|
| Telephone numbers | `CONTACT.PHONE` |
| Fax number | recommended `selector` `CONTACT.FAX` |
| Email address | `CONTACT.EMAIL` |
| Social Security Number | `UID.ID` |
| Medical record number | recommended `selector` `HEALTH.RECORD`|
| Health plan beneficiary number | recommended `selector` `HEALTH.PLAN-BENEFICIARY-NUMBER` |
| Account number | `UID.USER-ACCOUNT` |
| Certificate or license number | recommended `selector` `UID.ID.LICENCE-NUMBER` |
| Vehicle identifiers and serial numbers, including license plate numbers | recommended `selector` `UID.ID.VEHICULE-ID` |
| Device identifiers and serial numbers | `DEVICE` |
| Web URL | `UID.USER-ACCOUNT` or `selector` `UID.WEB-URL` |
| Internet Protocol (IP) Address | `UID.IP` |
| Finger or voice print | `BIOMETRIC` |
| Photographic image - Photographic images are not limited to images of the face. | `IMAGE` |
| Any other characteristic that could uniquely identify the individual | `UID` |



## Questions and Discussion Topics



## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj), [CHAPTER III - Rights of the data subject](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre3#Article13)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5), [CCPA(more digestible format)](https://ccpa-info.com/california-consumer-privacy-act-full-text/)

### Yet to be Supported Legilsation

- CPRA
- HIPPA
