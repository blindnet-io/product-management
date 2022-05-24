# Rights Request Interoperability Format (RRIF)

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [NNN](https://github.com/blindnet-io/PROJECT/pull/NNN) (update when you have PR #)     |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Sponsor**   | milstan (milstan@blindnet.io)                                                          |
| **Updated**   | 2022-05-19                                                                             |

## Objective

We propose a simple, structured data format for representing [Rights Requests](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization#data-capture--rights-requests).

Rights Requests exist within the relationship between an individual and software systems (and organisations operating them) treating data that concerns that individual. 

Systems MAY process and respond to Rights Request by legal obligation, or as a simple courtesy in the pursuit of gaining and maintaining the individual's trust.

## Motivation

Different systems, and different compontents of a single system, including different comnponents of blindnet devkit are likely to exchange information about Rights Requests.

Therefore, a common format is needed to facilitate exchange of information without loss of semantics. 

Our goal is to establish a shared semantics of Rights Request so that their processing can be, as much as possible, automatised by the Systems.

## Design Considerations

The design also aimes to maximise:
- Consistent Interpretation of Rights Request accorss different Systems
- Automatisation of Rights Request Processing
- Confidentialty of data
- Compatibility with the use of different protocols and tools for:
    - user identity management and authentication,
    - encryption.



## Terminology

>**TO BE Updated** once Lexicon and High Level Conceptualization are synchronised

- We use the terms Rights Request, Data Subject, System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Rights Request and Data Rights Request interchangeably
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)
- We use all the terms from the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv) as defined there.


## Proposal

### Rights Request

Data Subjects is the author of a Rights Request.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `data-subject` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1-* | An array of objects, each containing a (`dsid`,`dsid-schema`) pair |

An array of one or more [Data Subject Identities](#decentralized-identity-of-data-subjects) MUST be provided in order to match the Data Subject with the data concerning them.

In addition, the Rights Request has other meta-data:

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `request-id` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | Unique ID for referening to this request in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `date` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1-* | Date and Time when Rights Request was created in JSON Schema [date-time](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `language` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | **TBD format** Language of textual message associated with demands |

The Data Subject can request several things (e.g. see the data the System has on me, know the source from where you have got it, and have my data deleted). We call those 'Demands'.

A Rights Request includes an array of one or more Demands.

#### Demands

A Demand is a concrete action that the user requests.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `demande-id` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | Unique ID for referening to this demande in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `action` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 1 | **TBD** |
| `data-categories` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of strings indicating particular categories of data to which the demand is limited to. See [Demand Restrictions](#demand-restrictions) for reserved values. |
| `treatment` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | **TBD**|
| `consent-ids` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of consent ids to indicate that the Demand (e.g. a `REVOQUE-CONSENT` Demand) is restricted to particular consents. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `capture-ids` | [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of Data Capture IDs to indicate that the Demand (e.g. a `DELETE` Demand) is restricted to data captured within particular Data Captures. Items of the array are strings in the [uuid](https://www.rfc-editor.org/rfc/rfc4122.html) format |
| `legal-grounds`| [array](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | Optional array of strings represented legal grounds that support the Demand. E.g. "GDPR.13" indicates Article 13 of GDPR, "CCPA.C" indicates Section C of CCPA |
| `message` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | Optional comment, motivation or explanation of Demand |

##### Demand Restrictions

A Demand MAY be restricted to one or more data categories. For example, a Data Subject can request to access to all data concerning his location.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `data-category` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-* | One of {`NAME`, `CONTACT`, `CONTACT.EMAIL`, `CONTACT.ADDRESS`, `CONTACT.PHONE`, `UID`, `FINANCIAL`, `HEALTH`, `IMAGE`, `LOCATION`, `DEVICE`, `BEHAVIOR`, `BEHAVIOR.CONNECTION`, `BEHAVIOR.ACTIVITY`,  `BEHAVIOR.PREFERENCE`, `PROFILING`, `OTHER`} |

When several values are given, Systems MUST interpret the `data-category` restriction as a union of all the categories indicated. 

Categories are organised as a hierarchy, denoted with a full-stop ".", the more general category being written on the left. E.g. the following two `data-category` restrictions are equivalent:
- `CONTACT`,`CONTACT.EMAIL`
- `CONTACT`

In the absence of indication of any `data-category` restriction, Systems MUST interpret the Demand as being related to all categories of data.


#### Transitive Rights Request

A Rights Request can be transitive.
Transitive Rights Requests are usefull in a distributed context where System A gave information about the Data Subject to System B, and System B gave information about the Data Subject to System C.

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

Convenient tables of Transitivity vlaues and corresponding user-facing descriptions, in different languages, are provided [here](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/dictionary/transitivity/).

#### Reply-to

In a distributed context, where one System transmits the Rights Request to another System, a `reply-to` field MAY be specified.

| Schema propery | JSON Type | Expected cardinality | Expected values |
| --------------- | ------------ | ------ | -------------------- |
| `reply-to` | [string](https://datatracker.ietf.org/doc/html/rfc8259#page-6) | 0-1 | One of {`SYSTEM`, `USER`} |

`SYSTEM` indicates that the [scenario of nested responses](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#scenario-1---nested-responses) is prefered. The System having registered the Rights Request from the Data Subject gathers responses and presents them to the Data Subject.

`USER` indicated the [scenario of direct responses](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#scenario-2---direct-responses) is prefered. Each System having received a Rights Request is expected to reply directly to the Data Subject, using contact information it has.

### Requests list
<!-- prettier-ignore -->
| Nb | Request | Description | Associated treatment | Associated data category | Advised elements to provide | Legal ground | CNIL reference
| ---------- | ---- | ---- | ---- | ---- | ---- | ---- |---- |
| -- | ACCESS TYPE | ---- | ---- | ---- | ---- | ---- | ---- |
| 01 | **Access** | Access to all data the organization has on me  | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/modele/courrier/exercer-son-droit-dacces |
| 15 | **Access to my medical record** | Acces to my medical record | ---- | ---- | ID | ---- |  https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical |
| 16 | **Access to data "Preventel" has on me** | Access to data "Preventel" has on me | ---- | ---- | ID | ---- | https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel |
| 07 | **Access to data a financial organization has on me** *-> to delete and let user make access request + provenance request to the financial organization* | Access to all data the (financial) organization has on me, Provide with any available information on the origin of this data concerning me *(access+provenance info request)* | ---- | ---- | ID, Account number | ---- | https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier |
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



### User Impact

**TBD**- What are the user-facing changes? How will this feature be rolled out?

## Detailed Design

### JSON format

In addition to this specification document we provide a JSON Schema document (link soon), for machine-readable interpretation of Rights Requests compliant with [v4 (or ideally lower) of IETF specification](https://datatracker.ietf.org/doc/html/draft-zyp-json-schema-04#:~:text=JSON%20Schema%20is%20a%20JSON,interaction%20control%20of%20JSON%20data.)

The key requirements of the design are to enable:
- Unambiguous expression of Rights Requests in a machine-readable form
- Integrity of Rights Requests semantics when exchanged between components and systems. 
I.e. A system that has not directly collected the Rights Requests from the user, but has received in in JSON format from another system, can make the exact same interpretation of the request as if it had collected the request directly.
- A way of uniquely identifying one and the same Rights Request across systems and components concerned by it.

### Authenticated exchanges

Systems exchanging Rignts Requests MUST be able to do so in a way allowing them to very the integrity of their content, and the identity of the system having emitted the Rignts Request.

For this purposes Rignts Requests MAY be embedded as 'Claims' in [JWTs (FRC7519)](https://datatracker.ietf.org/doc/html/rfc7519).

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

### Remembering Transfers

When data about Data Subjects is transmitted from one system to another, in order to be able to process [Transitive Rights Requests](#transitive-rights-request), Systems MUST keep track of:
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


## Questions and Discussion Topics

### Use UUID for identifying Data Subjects

We chould immagine an alternative design, where we would force systems to use an [UUID]([uuid](https://en.wikipedia.org/wiki/Universally_unique_identifier)) (according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html)), to identify the users. That would require us to provide some way for systems to match UUIDs with their local IDs (usernames, or e-mails), and would ponteltially limit the ability of 3rd party systems to interprete Rights Request made at another system. This goal of proposed design is to allow for flexibility. However it is a very important aspect of the proposal, that deserves further debate.

### Mandatory properties and value constrains

Should we include rescritions in the schema according to the [JSON-schema-validation vocabulary](https://datatracker.ietf.org/doc/html/draft-bhutton-json-schema-validation-00#page-4) in order to make certian properties mandatory and ensure to limit string values to the values we suppoort? 

In the curent proposal, this is the case for Transitivity, but not for request types, data categories, and user identity schemas. We might want to include more forma constraints there, or deliberately leave flexibility. This is a discussion we need to have.

## References

### Normative References


- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017. 

### Informative References
- 
