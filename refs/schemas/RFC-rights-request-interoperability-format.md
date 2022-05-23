# Rights Request Interoperability Format (RRIF)

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [NNN](https://github.com/blindnet-io/PROJECT/pull/NNN) (update when you have PR #)     |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Sponsor**   | Filip (filip@blindnet.io)                                                              |
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

- We use the terms Rights Request, Data Subject, System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Rights Request and Data Rights Request interchangeably
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)


## Proposal

### Requests list
<!-- prettier-ignore -->
| Nb | Request | Description | Advised elements to provide| CNIL reference
| ---------- | ---- | ---- | ---- |---- |
| -- | ACCESS TYPE | ---- | ---- |---- |
| 01 | **Access** | Access to all data the organization has on me  | ID | https://www.cnil.fr/fr/modele/courrier/exercer-son-droit-dacces |
| 15 | **Access to my medical record** | Acces to my medical record | ID |  https://www.cnil.fr/fr/modele/courrier/acceder-son-dossier-medical |
| 16 | **Access to data "Preventel" has on me** | Access to data "Preventel" has on me | ID | https://www.cnil.fr/fr/modele/courrier/acceder-aux-informations-contenues-dans-preventel |
| 07 | **Access to data a financial organization has on me** *-> to delete and let user make access request + provenance request to the financial organization* | Access to all data the (financial) organization has on me, Provide with any available information on the origin of this data concerning me *(access+provenance info request)* | ID, Account number | https://www.cnil.fr/fr/modele/courrier/connaitre-les-informations-detenues-par-un-etablissement-financier |
| 09 | **Access to data "Fichier central des Chèques (FCC)" has on me** *-> to delete and let user make access request to the "Fichier central des Chèques (FCC)" ?*| Access to all data Fichier central des Chèques (FCC) has on me | ID, Birthdate | https://www.cnil.fr/fr/modele/courrier/acceder-au-fichier-central-des-cheques-fcc |
| 10 | **Access to data "Fichier national des Incidents de remboursement de Crédit (FICP)" has on me** *-> to delete and let user make access request to the "Fichier national des Incidents de remboursement de Crédit (FICP)" ?*| Access to all data "Fichier national des Incidents de remboursement de Crédit (FICP)" has on me | ID, Birthdate | https://www.cnil.fr/fr/modele/courrier/acceder-aux-donnees-du-fichier-national-des-incidents-de-remboursement-de-credit |
| 11 | **Access to geolocation data or an access control device an organization has on me** | Access to data organization has on me on a device on a specific period of time *access request to geolocation data and device data* | ID, Device type, Date and time | https://www.cnil.fr/fr/modele/courrier/acceder-des-donnees-de-geolocalisation-ou-un-dispositif-de-controle-dacces |
| 12 | **Access to video surveillance data** | Access to video data organization has on me on a specific period of time *access request to video surveillance data* | ID, Date and time | https://www.cnil.fr/fr/modele/courrier/acceder-des-images-video-vous-concernant |
| 34 | **Exerce my right to portability** | Receive the data that concerns me and reuse them, transmit them to another data controller *access request + donwnload?* | ID | https://www.cnil.fr/fr/professionnels-comment-repondre-une-demande-de-droit-la-portabilite |
| -- | MODIFICATION TYPE | ---- | ---- |---- |
| 02 | **Modification** | Rectify incorrect data organization has on me  | ID, Information to modify, Information rectified (PF Access request + diff) | https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-inexactes |
| 03 | **Rectification** *to merge in one modification?* | Rectify incomplete data organization has on me | ID, Information to modify, Information rectified | https://www.cnil.fr/fr/modele/courrier/rectifier-des-donnees-incompletes |
| -- | DELETION TYPE | ---- | ---- |---- |
| 04 | **Deletion** | Delete the data the organization has on me  | ID, Information to delete*, Reason of deletion | https://www.cnil.fr/fr/modele/courrier/supprimer-des-donnees-personnelles |
| 08 | **Stop receiving advertising from organization** | Deletion of my contact details from organization avdertising contact list | ID, Reason of deletion | https://www.cnil.fr/fr/modele/courrier/ne-plus-recevoir-de-publicites |
| 13 | **Closing an online account** | Closing online account, Deletion of all data the organization has on me | ID, Account name, Website name, URL of the pages with my data, Data to delete | https://www.cnil.fr/fr/modele/courrier/cloturer-un-compte-en-ligne |
| 14 | **Delete my data that are published on a webiste** | Delete my data a website has published, Pages where my data appears are no longer referenced by search engines | ID, URL of the pages with my data, Data to delete, Reason of deletion | https://www.cnil.fr/fr/modele/courrier/supprimer-des-informations-vous-concernant-dun-site-internet, https://www.cnil.fr/fr/webmaster-ou-responsables-de-sites-comment-repondre-aux-demandes-de-suppression-de-donnees |
| 32 | **Opt out of contact lists** | Delete my contact details from all contact lists an ornaginzation has with my contact details| ID |  |
| 33 | **Removal of my image online** | Remove photo or video of me that has been published without my consent| ID | https://www.cnil.fr/fr/demander-le-retrait-de-votre-image-en-ligne |
| -- | OPPOSITION TO TREATMENT TYPE | ---- | ---- |---- |
| 05 | **Opposition to commercial prospecting** | Opposition to treatment of all data the organization has on me for prospecting purpose, Deletion of my contact details from organization's prospecting files , Propagation of request | ID, Account number | https://www.cnil.fr/fr/modele/courrier/sopposer-la-prospection-commerciale-par-telephone-sms-mail-courriers |
| 06 | **Opposition to treatment of all data an organization has on me** | Opposition to treatment of all data the organization has on me, Deletion of all data the organization has on me, Propagation of request, Information on how long data will be kept on archive database if it is an organisation's legal obligation | ID, Reason of deletion | https://www.cnil.fr/fr/modele/courrier/sopposer-au-traitement-de-donnees |
| 24 | **Limit the treatment (oppose to particular type of treatment) organization does on the data it has on me** | I refuse the use of my data or of certain data but I don't want to delete my account or all my data | Type of treatment (to choose from possible type of treatment list) | https://www.cnil.fr/fr/le-droit-dopposition-refuser-lutilisation-de-vos-donnees |
| 29 | **Opt out of automated decision making** *-> to delete to include in 24. Limit treatment* | Opposition to automated decision making on the data organizatio has on me | ID |  |
| 30 | **Opt out of sale of my data** *-> to delete to include in 24. Limit treatment* | Opposition to sale of the data an organization has on me| ID |  |
| 31 | **Opt out of tracking on my data** *-> to delete to include in 24. Limit treatment* | Opposition to the tracking of my data from an organization | ID |  |
| 27 | **Revoke consent** | Revoke specific consent that I previously gave for a type of treatment on the data the organization has on me | Type of treatment (to choose from possible type of treatment list), ID  | https://www.cnil.fr/fr/les-bases-legales/consentement "Droit au retrait : la personne doit avoir la possibilité de retirer son consentement à tout moment, par le biais d’une modalité simple et équivalente à celle utilisée pour recueillir le consentement (par exemple, si le recueil s’est fait en ligne, il doit pouvoir être retiré en ligne également)." |
| -- | INFORMATIONNAL TYPE | ---- | ---- |---- |
| 17 | **Storage information** | Know where is stored the data organization has on me | ID |  |
| 18 | **Accessibility information** | Know who can access the data organization has on m | ID |  |
| 19 | **Provenance information** | Know the provenance of data organization has on me | ID |  |
| 20 | **Retention information** | Know for how long the data organization has on me will be kept | ID | https://www.cnil.fr/fr/les-durees-de-conservation-des-donnees |
| 21 | **Deletion information** | Know when my data will be deleted | ID |  |
| 22 | **Policy information** | Know what is the policy of the organization to keep data it has on me | ID |  |
| 23 | **Purpose of treatment information** | Know the purpose of the treatment organization does on the data it has on me | ID |  |
| 25 | **Treatment information** | Know what type(s) of treatment organization does on the data it has on me | ID |  |
| 26 | **Particular type(s) of treatment information** | Know if a particular type of treatment is done by organisation on the data it has on me | Type of treatment (to choose from possible type of treatment list), ID |  |
| -- | OTHER TYPE | ---- | ---- |---- |
| 28 | **Propagation of request** (can only be ask in addition of another request) | Send the request to other organizations the organization may have shared the data it has me with |  |  |

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

### Globaly Unique Data Subject IDs

The identifyers used to refer to Data Subjects MUST be globaly unique. One Data Subject ID corresponds to one Data Subject. One Data Subject can have several Data Subject IDs.

When refering to a Data Subject, Systems MUST use both of the following atributes:
- `dsid` - Data Subject ID
- `dsid-schema` - A scheme allowign to dereference the Data Subject ID

The (`dsid`,`dsid-schema`) pair denotes a globaly unique reference to always the same Data Subject.

A Rights Request MAY include several (`dsid`,`dsid-schema`) pairs that refer to the same user, in order to facilitate the interoperability of Rights Requests across systems.

### Data Subject ID Schemas

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

### Data Subject SHOULD be Authenticated

In some cases, valid reasons MAY exist for Systems to respond to Rights Requests even from anonymous Data Subjects. This is the case, for example, with request relative to general data treatment practices practiced by the system.

However, in most cases, Systems SHOULD require the Data Subject to be authenticated as being indeed the person corresponding to the (`dsid`,`dsid-schema`) pair.

When processing Rights Request, Systems MAY automatically disregard the (`dsid`,`dsid-schema`) paris for which they have not been able to establish Data Subject authentication.

However, the authentication does not necessairly have to be performed during the collection of the Rights Request. It can be done separately.

### Data Capture IDs, Data Capture Fragment IDs, Consent IDs, Rights Request IDs, Demand IDs, Rights Request Respons IDs are Globally Unique

All of the following identifiers `data-capture-id`, `fragment-id`, `consent-id`, `rights-request-id`, `demand-id`, `rights-response-id` MUST be globally unique and be generated according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html) in order for the corresponding objects to be easily identifiable across systems.


## Questions and Discussion Topics

### Use UUID for identifying Data Subjects

We chould immagine an alternative design, where we would force systems to use an [UUID]([uuid](https://en.wikipedia.org/wiki/Universally_unique_identifier)) (according to the [IETF RFC4122](https://www.rfc-editor.org/rfc/rfc4122.html)), to identify the users. That would require us to provide some way for systems to match UUIDs with their local IDs (usernames, or e-mails), and would ponteltially limit the ability of 3rd party systems to interprete Rights Request made at another system. This goal of proposed design is to allow for flexibility. However it is a very important aspect of the proposal, that deserves further debate.
