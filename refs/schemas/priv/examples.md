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

| CODENAME | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` |
| -------- | ----------------------------------------------------- | ------------ | ------------ | ------------ | ------------ |
| `GDPR.13.1.a`, `GDPR.14.1.a` | the identity and the contact details of the controller and, where applicable, of the controller’s representative | `TRANSPARENCY.ORGANISATION` | `null` | `null` | `null` |
| `GDPR.13.1.b`, `GDPR.14.1.b` | the contact details of the data protection officer, where applicable; | `TRANSPARENCY.DPO` | `null` | `null` | `null` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | the purposes of the processing for which the personal data are intended  | `TRANSPARENCY.PURPOSE` | `null` | `null` | `null` |
| `GDPR.13.1.c`, `GDPR.14.1.c` | ... legal basis for the processing |  `TRANSPARENCY.LEGAL-BASES` | `null` | `null` | `null` |
| `GDPR.13.1.d`, `GDPR.14.1.d` | where the processing is based on point (f) of Article 6(1), the legitimate interests pursued by the controller or by a third party | `TRANSPARENCY.LEGAL-BASES` | `null` | `null` | `null` |
| `GDPR.13.1.e`, `GDPR.14.1.e` | the recipients or categories of recipients of the personal data, if any; | `TRANSPARENCY.WHO` | `null` | `null` | `null` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | where applicable, the fact that the controller intends to transfer personal data to a third country or international organisation | `TRANSPARENCY.WHERE` | `null` | `null` | `null` |
| `GDPR.13.1.f`, `GDPR.14.1.f` | the existence or absence of an adequacy decision by the Commission, or in the case of transfers referred to in Article 46 or 47, or the second subparagraph of Article 49(1), reference to the appropriate or suitable safeguards and the means by which to obtain a copy of them or where they have been made available. | `OTHER` | `null` | `null` | `null` |
| `GDPR.13.2.a`, `GDPR.14.2.a` | the period for which the personal data will be stored, or if that is not possible, the criteria used to determine that period | `TRANSPARENCY.RETENTION` | `null` | `null` | `null` |
| `GDPR.13.2.b`, `GDPR.14.2.b` | the existence of the right to request from the controller access to and rectification or erasure of personal data or restriction of processing concerning the data subject or to object to processing as well as the right to data portability | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.13.2.c`, `GDPR.14.2.c` | where the processing is based on point (a) of Article 6(1) or point (a) of Article 9(2), the existence of the right to withdraw consent at any time, without affecting the lawfulness of processing based on consent before its withdrawal | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.13.2.d`, `GDPR.14.2.d` | the right to lodge a complaint with a supervisory authority | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.13.2.e`, `GDPR.14.2.e` | whether the provision of personal data is a statutory or contractual requirement, or a requirement necessary to enter into a contract, as well as whether the data subject is obliged to provide the personal data  |  `TRANSPARENCY.PURPOSE` | `null` | `null` | `null` |
| `GDPR.13.2.e`, `GDPR.14.2.e` | ... and of the possible consequences of failure to provide such data | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.13.2.f`, `GDPR.14.2.f` | the existence of automated decision-making, including profiling | `TRANSPARENCY.PROCESSING` | `null` | `null` | `null` |
| `GDPR.13.2.f`, `GDPR.14.2.g` | the existence of automated decision-making, including profiling, referred to in Article 22(1) and (4) and, at least in those cases, meaningful information about the logic involved, as well as the significance and the envisaged consequences of such processing for the data subject. | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.14.2.f` | from which source the personal data originate, and if applicable, whether it came from publicly accessible sources; | `TRANSPARENCY.PROVENANCE` | `null` | `null` | `null` |



#### Article 15.1

*The data subject shall have the right to obtain from the controller confirmation as to whether or not personal data concerning him or her are being processed*

| LAW | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` |
| -------- | ----------------------------------------------------- | ------------ | ------------ | ------------ | ------------ |
| `GDPR.15.1` | confirmation as to whether or not personal data concerning him or her are being processed  | `TRANSPARENCY.KNOW` | `null` | `null` | `null` |

*and, where that is the case, access to the personal data and the following information:*

| LAW | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` |
| -------- | ----------------------------------------------------- | ------------ | ------------ | ------------ | ------------ |
| `GDPR.15.1.a` | the purposes of the processing  | `TRANSPARENCY.PURPOSE` | `null` | `null` | `null` |
| `GDPR.15.1.b` | the categories of personal data concerned | `TRANSPARENCY.DATA-CATEGORIES` | `null` | `null` | `null` |
| `GDPR.15.1.c` | the recipients or categories of recipient to whom the personal data have been or will be disclosed, in particular recipients in third countries or international organisations;  | `TRANSPARENCY.WHO` | `null` | `null` | `null` |
| `GDPR.15.1.d` | where possible, the envisaged period for which the personal data will be stored, or, if not possible, the criteria used to determine that period;  | `TRANSPARENCY.RETENTION` | `null` | `null` | `null` |
| `GDPR.15.1.e` | the existence of the right to request from the controller rectification or erasure of personal data or restriction of processing of personal data concerning the data subject or to object to such processing;  | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.15.1.f` | the right to lodge a complaint with a supervisory authority  | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.15.1.g` | where the personal data are not collected from the data subject, any available information as to their source  | `TRANSPARENCY.PROVENANCE` | `null` | `null` | `null` |
| `GDPR.15.1.h` | the existence of automated decision-making, including profiling  | `TRANSPARENCY.PROCESSING` | `null` | `null` | `null` |
| `GDPR.15.1.h` | the existence of automated decision-making, including profiling, referred to in Article 22(1) and (4) and, at least in those cases, meaningful information about the logic involved, as well as the significance and the envisaged consequences of such processing for the data subject  | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |

>**Note**
>
> To make a request to know if the System has data on them (`GDPR.15.1`) and know about the purposes of processing of that data, the Data Subject MUST make a request with two demands, one `TRANSPARENCY.KNOW` and one `TRANSPARENCY.PURPOSE`
#### Article 15.2 and 15.3

| LAW | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` |
| -------- | ----------------------------------------------------- | ------------ | ------------ | ------------ | ------------ |
| `GDPR.15.2` | Where personal data are transferred to a third country or to an international organisation, the data subject shall have the right to be informed of the appropriate safeguards pursuant to Article 46 relating to the transfer  | `TRANSPARENCY.POLICY` | `null` | `null` | `null` |
| `GDPR.15.3` | The controller shall provide a copy of the personal data undergoing processing.  | `ACCESS` | `null` | `null` | `null` |

#### Article 16-22

| LAW | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` |
| -------- | ----------------------------------------------------- | ------------ | ------------ | ------------ | ------------ |
| `GDPR.16` | The data subject shall have the right to obtain from the controller without undue delay the rectification of inaccurate personal data concerning him or her. 2Taking into account the purposes of the processing, the data subject shall have the right to have incomplete personal data completed, including by means of providing a supplementary statement.  | `MODIFY` | `null` | `null` | `null` |
| `GDPR.17` | The data subject shall have the right to obtain from the controller the erasure of personal data concerning him | `DELETE` | `null` | `null` | `null` |
| `GDPR.18` | The data subject shall have the right to obtain from the controller restriction of processing | `RESTRICT` | `null` | `null` | `null` |
| `GDPR.20` | **TBD** | `**TBD**` | `null` | `null` | `null` |
| `GDPR.21` | **TBD**  (note: 21.2 is not yet supported by the schema)| `**TBD**` | `null` | `null` | `null` |
| `GDPR.22` | **TBD** | `**TBD**` | `null` | `null` | `null` |



### GDPR REQUEST TEMPLATES FROM CNIL

| LAW | Demande | `action`(s) | `data-categories` | `processing-categories` | `purposes` | `message` | Additional element |
| -------- | -------------------------------------- | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| `GDPR.15` | [Access to video surveillance data](https://www.cnil.fr/fr/modele/courrier/acceder-des-images-video-vous-concernant) from 01 Feb 2021 to 03 Feb 2021 | `ACCESS` | `IMAGE` | `null` | `SECURITY` | video surveillance data from 01 Feb 2021 to 03 Feb 2021 | `ID`,`date`,`time.begining`,`time.ending` |
| `Code de la santé publique art. L. 1111-7` | [Acces to my medical record](https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical) | `ACCESS` | `HEALTH` | `null` | `null` | `null` | `ID` |
| `GDPR.15` | [Access to data "Preventel" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel) | `ACCESS` | `null` | `null` | `null` | `null` | `ID` |
| `GDPR.15` | [Access to data a financial organization has on me](https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier) Access to all data the (financial)organization has on me, Provide with any available information on the origin of this data concerning me | `ACCESS`, `TRANSPARENCY.PROVENANCE` | `null` | `null` | `null` | `null` | `ID`,`account number` |
| `GDPR.15` | [Access to data "Fichier central des Chèques (FCC)" has on me](https://www.cnil.fr/fr/modele/courrier/acceder-au-fichier-central-des-cheques-fcc) | `ACCESS` | `null` | `null` | `null` | `null` | `ID`, (birthdate) |
| `GDPR.15` | [Access to data "Fichier national des Incidents de remboursement de Crédit (FICP)](https://www.cnil.fr/fr/modele/courrier/acceder-aux-donnees-du-fichier-national-des-incidents-de-remboursement-de-credit) | `ACCESS` | `null` | `null` | `null` | `null` | `ID`, (birthdate) |
| `GDPR.15` | [Access to geolocation data or an access control device an organization has on me](https://www.cnil.fr/fr/modele/courrier/acceder-des-donnees-de-geolocalisation-ou-un-dispositif-de-controle-dacces) on a specific period of time | `ACCESS` | `null` | `null` | `null` | `null` | `ID`,`date`,`time.begining`,`time.ending` |
| `GDPR.20` | [Exerce my right to portability](https://www.cnil.fr/fr/professionnels-comment-repondre-une-demande-de-droit-la-portabilite) Receive the data that concerns me to reuse them and transmit them to another data controller| `ACCESS` | `X` | `null` | `null` | `null` | `null` |

>**Note**
>
>we need to add a schema field for providing data ranges (from date to date)

### OTHER EXAMPLES FROM DAILY LIFE

*Change my address*

| LAW | Demande (as introduced by regulation) | `action`(s) | `data-categories` | `processing-categories` | `purposes` | `message` |
| -------- | -------------------------------------- | ------------ | ------------ | ------------ | ------------ | ------------ |
| `GDPR.16` | Change my address, with new address being 1 blindnet street, 75000 blindcity, France, as of 01.01.2021  | `MODIFY` | `CONTACT.ADDRESS` | `null` | `null` | `null` |

>**Note**
>
>we need to add a schema field for providing new data, and date of validity of new data (not necessairly the date of trnasmission)


### Requests list (**TO BE TRANSFORMED IN THE ABOVE FORMAT**)
<!-- prettier-ignore -->
| Nb | Request | Description | Associated treatment | Associated data category | Advised elements to provide | Legal ground | CNIL reference
| ---------- | ---- | ---- | ---- | ---- | ---- | ---- |---- |
| -- | ACCESS TYPE | ---- | ---- | ---- | ---- | ---- | ---- |
| OK | **Access** | Access to all data the organization has on me  | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/modele/courrier/exercer-son-droit-dacces |
| 15 | **Access to my medical record** | Acces to my medical record | ---- | ---- | ID | art. L. 1111-7 du code de la santé publique |  https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical |
| 16 | **Access to data "Preventel" has on me** | Access to data "Preventel" has on me | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel |
| 07 | **Access to data a financial organization has on me** *-> to delete and let user make access request + provenance request to the financial organization* | Access to all data the (financial)organization has on me, Provide with any available information on the origin of this data concerning me *(access+provenance info request)* | ---- | ---- | ID, Account number | ---- | https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier |
| 09 | **Access to data "Fichier central des Chèques (FCC)" has on me** *-> to delete and let user make access request to the "Fichier central des Chèques (FCC)" ?*| Access to all data Fichier central des Chèques (FCC) has on me | ---- | ---- | ID, Birthdate | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-au-fichier-central-des-cheques-fcc |
| 10 | **Access to data "Fichier national des Incidents de remboursement de Crédit (FICP)" has on me** *-> to delete and let user make access request to the "Fichier national des Incidents de remboursement de Crédit (FICP)" ?*| Access to all data "Fichier national des Incidents de remboursement de Crédit (FICP)" has on me | ---- | ---- | ID, Birthdate | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-aux-donnees-du-fichier-national-des-incidents-de-remboursement-de-credit |
| 11 | **Access to geolocation data or an access control device an organization has on me** | Access to data organization has on me on a device on a specific period of time *access request to geolocation data and device data* | ---- | ---- | ID, Device type, Date and time | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-des-donnees-de-geolocalisation-ou-un-dispositif-de-controle-dacces |
| 12 | **Access to video surveillance data** | Access to video data organization has on me on a specific period of time *access request to video surveillance data* | ---- | ---- | ID, Date and time | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-des-images-video-vous-concernant |
| 34 | **Exerce my right to portability** | Receive the data that concerns me and reuse them, transmit them to another data controller *access request + donwnload?* | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/professionnels-comment-repondre-une-demande-de-droit-la-portabilite |
| -- | MODIFICATION TYPE | ---- | ---- |---- |
| 02 | **Modification** | Rectify incorrect data organization has on me  | ---- | ---- | ID, Information to modify, Information rectified | ---- | https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-inexactes |
| 03 | **Rectification** *to merge in one modification?* | Rectify incomplete data organization has on me | ---- | ---- | ID, Information to modify, Information rectified | ---- | https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-incompletes |
| -- | DELETION TYPE | ---- | ---- |---- |
| 04 | **Deletion** | Delete the data the organization has on me  | ---- | ---- | ID, Information to delete*, Reason of deletion | ---- | https://www.cnil.fr/fr/modele/courrier/supprimer-des-donnees-personnelles |
| 08 | **Stop receiving advertising from organization** | Deletion of my contact details from organization avdertising contact list | ---- | ---- | ID, Reason of deletion | ---- | https://www.cnil.fr/fr/modele/courrier/ne-plus-recevoir-de-publicites |
| 13 | **Closing an online account** | Closing online account, Deletion of all data the organization has on me | ---- | ---- | ID, Account name, Website name, URL of the pages with my data, Data to delete | ---- | https://www.cnil.fr/fr/modele/courrier/cloturer-un-compte-en-ligne |
| 14 | **Delete my data that are published on a webiste** | Delete my data a website has published, Pages where my data appears are no longer referenced by search engines | ---- | ---- | ID, URL of the pages with my data, Data to delete, Reason of deletion | ---- | https://www.cnil.fr/fr/modele/courrier/supprimer-des-informations-vous-concernant-dun-site-internet, https://www.cnil.fr/fr/webmaster-ou-responsables-de-sites-comment-repondre-aux-demandes-de-suppression-de-donnees |
| 32 | **Opt out of contact lists** | Delete my contact details from all contact lists an ornaginzation has with my contact details| ---- | ---- | ID | ---- |  |
| 33 | **Removal of my image online** | Remove photo or video of me that has been published without my consent| ---- | ---- | ID | ---- | https://www.cnil.fr/fr/demander-le-retrait-de-votre-image-en-ligne |
| -- | OPPOSITION TO TREATMENT TYPE | ---- | ---- |---- |
| 05 | **Opposition to commercial prospecting** | Opposition to treatment of all data the organization has on me for prospecting purpose, Deletion of my contact details from organization's prospecting files , Propagation of request | ---- | ---- |ID, Account number | ---- | https://www.cnil.fr/fr/modele/courrier/sopposer-la-prospection-commerciale-par-telephone-sms-mail-courriers |
| 06 | **Opposition to treatment of all data an organization has on me** | Opposition to treatment of all data the organization has on me, Deletion of all data the organization has on me, Propagation of request, Information on how long data will be kept on archive database if it is an organisation's legal obligation | ---- | ---- | ID, Reason of deletion | ---- | https://www.cnil.fr/fr/modele/courrier/sopposer-au-traitement-de-donnees |
| 24 | **Limit the treatment (oppose to particular type of treatment) organization does on the data it has on me** | I refuse the use of my data or of certain data but I don't want to delete my account or all my data | *Type of treatment (to choose from possible type of treatment list)* | ---- |  | ---- | https://www.cnil.fr/fr/le-droit-dopposition-refuser-lutilisation-de-vos-donnees |
| 29 | **Opt out of automated decision making** *-> to delete to include in 24. Limit treatment* | Opposition to automated decision making on the data organizatio has on me | ---- | ---- | ID | ---- |  |
| 30 | **Opt out of sale of my data** *-> to delete to include in 24. Limit treatment* | Opposition to sale of the data an organization has on me| ---- | ---- | ID | ---- |  |
| 31 | **Opt out of tracking on my data** *-> to delete to include in 24. Limit treatment* | Opposition to the tracking of my data from an organization | ---- | ---- | ID | ---- |  |
| 27 | **Revoke consent** | Revoke specific consent that I previously gave for a type of treatment on the data the organization has on me | *Type of treatment (to choose from possible type of treatment list)* | ---- | ID | ---- | https://www.cnil.fr/fr/les-bases-legales/consentement "Droit au retrait : la personne doit avoir la possibilité de retirer son consentement à tout moment, par le biais d’une modalité simple et équivalente à celle utilisée pour recueillir le consentement (par exemple, si le recueil s’est fait en ligne, il doit pouvoir être retiré en ligne également)." |
| -- | INFORMATIONNAL TYPE | ---- | ---- |---- |
| 17 | **Storage information** | Know where is stored the data organization has on me | ---- | ---- | ID | ---- |  |
| 18 | **Accessibility information** | Know who can access the data organization has on me | ---- | ---- | ID | ---- |  |
| 19 | **Provenance information** | Know the provenance of data organization has on me | ---- | ---- | ID | ---- |  |
| 20 | **Retention information** | Know for how long the data organization has on me will be kept | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/les-durees-de-conservation-des-donnees |
| 21 | **Deletion information** | Know when my data will be deleted | ---- | ---- | ID | ---- |  |
| 22 | **Policy information** | Know what is the policy of the organization to keep data it has on me | ---- | ---- | ID | ---- |  |
| 23 | **Purpose of treatment information** | Know the purpose of the treatment organization does on the data it has on me | ---- | ---- | ID | ---- |  |
| 25 | **Treatment information** | Know what type(s) of treatment organization does on the data it has on me | ---- | ---- | ID | ---- |  |
| 26 | **Particular type(s) of treatment information** | Know if a particular type of treatment is done by organisation on the data it has on me | *Type of treatment (to choose from possible type of treatment list)* | ---- | ID | ---- |  |
| -- | OTHER TYPE | ---- | ---- |---- |
| 28 | **Propagation of request** (can only be ask in addition of another request) | Send the request to other organizations the organization may have shared the data it has me with | ---- | ---- |  | ---- |  |

### Types of treatment list
| Nb | Treatment | Description | CNIL reference
| ---------- | ---- | ---- | ---- |
| 01 | **Collection** | Data collection | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 02 | **Recording** | Data recording | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 03 | **Organisation** | Data organisation | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 04 | **Retention** | Data retention | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 05 | **Adapation** | Data adaptation | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 07 | **Modification** | Data modification | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 08 | **Extraction** | Data extraction | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 09 | **Consultation** | Data consultation| https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 10 | **Usage** | Data usage | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 11 | **Communication** | Data communication by transmission or broadcast or any other form of data communication | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 12| *FR: "Rapprochement" -> EN: "Matching" or "Reconciliation" ?* |  | https://www.cnil.fr/fr/definition/traitement-de-donnees-personnelles#:~:text=Exemples%20de%20traitements%20%3A%20tenue%20du,information%20(selon%20le%20cas |
| 13 | **Automatic Inference and Descisionmaking** | Any automatic inference made on the data | [GDPR chap3 art. 13 section 2. c)](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre3#Article13)|
| 14 | **Basic service** | Provide a service that the user explicitly requests and that is part of the product's basic service or functionality |  |
| 15 | **Additonal service** | Provide a service that the user explicitly requests but that is not a necessary part of the product's basic service |  |
| 16 | **Tracking** | Tracking information about user behavior and activity online |  |
| 17 | **Advertising** | To show ads that are either targeted to the specific user or not targeted |  |
| 18 | **Marketing** |  To contact the user to offer products, services, or other promotions |  |
| 19 | **Analytics** | For understanding the product’s audience, improving the product, inform company strategy, or general research |  |
| 20 | **Personnalisation** | For providing user with a personalized experience |  |
| 21 | **Operation security** | For product operation and security, enforcement of terms of service, fraud prevention, protecting users and property, etc. |  |
| 22 | **Legal** | For compliance with legal obligations |  |
| 23 | **Ongoing contract** | For ongoing contract purpose |  |
| 24 | **Data transfer** | For data that was transferred as part of a change in circumstance (e.g. a merger or acquisition) |  |
| 25 | **Sale** | Selling data to third parties |  |
| 26 | **OTHER** | Other specific purpose not covered above |  |
| 27 | **UNSPECIFIED** | The purpose is not explicitly stated or is unclear |  |
| 28 | **ALL** |  |  |

### Data categories list
| Nb | Data category | Description | CNIL reference
| ---------- | ---- | ---- | ---- |
| 01 | **Name** | Firstname, Surname |  |
| 02 | **Postal address** | *contact information* |  |
| 03 | **Email address** | *contact information* |  |
| 04 | **Phone number** | *contact information* |  |
| 04 | **ID data** | Identifiers that uniquely identify a person |  |
| 05 | **Financial data** | Financial information |  |
| 06 | **Connection data** | Information associated to connection |  |
| 07 | **Geoocation data** | Location information |  |
| 08 | **Health data** | Health information |  |
| 09 | **Tracking data** | Cookies and tracking information about user behavior and activity online|  |
| 10 | **User profile** | User’s profile on the first-party website/app and its contents |  |
| 11 | **Device data** | Device (desktop, tablet, mobile...) information |  |
| 12 | **Form data** | Information collected through forms  |  |
| 13 | **Image data** | Photo or video |  |
| 14 | **Video surveillance data** | Video from video surveillance |  |
| 15 | **OTHER** | A specific type of information not covered by the above categories | |
| 16 | **UNSPECIFIED** | The type of information is not explicitly stated or unclear|
| 17 | **ALL** |  |  |

### Alternatives Considered

#### Transcend

Transcend proposes the following [action (demand) types](https://github.com/transcend-io/privacy-types/blob/main/src/actions.ts):
| Demand Type | Description | Observation |
| -------------- | ----------------------------------------- | ------------------------ |
| ACCESS | Data Download request | |
| ERASURE | Erase the file completely | |
| ACCOUNT_DELETION | Run an account deletion instead of a fully compliant deletion | |
| AUTOMATED_DECISION_MAKING_OPT_OUT | Opt out of automated decision making | |
| CONTACT_OPT_OUT | A contact opt out request | |
| SALE_OPT_OUT | Opt-out of the sale of personal data | |
| TRACKING_OPT_OUT | A tracking opt out request | |
| RECTIFICATION | Make an update to an inaccurate record | |
| RESTRICTION | A restriction of processing request | |

All of those can be modeled using our Demand Types.

Transced proposes the following [treatment types](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Treatment Type | Description | Observation |
| -------------- | ----------------------------------------- | ------------------------ |
| ESSENTIAL | Provide a service that the user explicitly requests and that is part of the product's basic service or functionality| |
| ADDITIONAL_FUNCTIONALITY | Provide a service that the user explicitly requests but that is not a necessary part of the product's basic service | |
| ADVERTISING | To show ads that are either targeted to the specific user or not targeted | |
| MARKETING | To contact the user to offer products, services, or other promotions | |
| ANALYTICS | For understanding the product’s audience, improving the product, inform company strategy, or general research | |
| PERSONALIZATION | For providing user with a personalized experience | |
| OPERATION_SECURITY | For product operation and security, enforcement of terms of service, fraud prevention, protecting users and property, etc. | |
| LEGAL | For compliance with legal obligations | |
| TRANSFER | For data that was transferred as part of a change in circumstance (e.g. a merger or acquisition) | |
| SALE | For selling the data to third parties | |
| HR | For personnel training, recruitment, payroll, management, etc. | corresponds to ongoing contract in our terminology|
| OTHER | Other specific purpose not covered above | |
| UNSPECIFIED | The purpose is not explicitly stated or is unclear | |

All of those SHOULD be modeled using our Treatment Types.

Transced proposes the following [data categories](https://github.com/transcend-io/privacy-types/blob/main/src/objects.ts):
| Data Category | Description | Observation |
| -------------- | ----------------------------------------- | ------------------------ |
| FINANCIAL | Financial information | |
| HEALTH | Health information | |
| CONTACT | Contact information | |
| LOCATION |  Geo-location information | |
| DEMOGRAPHIC | Demographic Information | |
| ID | Identifiers that uniquely identify a person | |
| ONLINE_ACTIVITY | The user's online activities on the first party website/app or other websites/apps | |
| USER_PROFILE | he user’s profile on the first-party website/app and its contents | |
| SOCIAL_MEDIA | User profile and data from a social media website/app or other third party service | |
| CONNECTION | Connection information for the current browsing session, e.g. device IDs, MAC addresses, IP addresses, etc. | |
| TRACKING | Cookies and tracking elements | |
| DEVICE | Computer or device information | |
| SURVEY | Any data that is collected through surveys | |
| OTHER | A specific type of information not covered by the above categories | |
| UNSPECIFIED | The type of information is not explicitly stated or unclear| |



## Questions and Discussion Topics



## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.

### Informative References

-

### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- [CPRA]([https://eur-lex.europa.eu/eli/reg/2016/679/oj](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf))
- [HIPPA]([https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5](https://www.govinfo.gov/content/pkg/PLAW-104publ191/pdf/PLAW-104publ191.pdf))
