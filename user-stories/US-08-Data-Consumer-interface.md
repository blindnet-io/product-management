# Data Consumer Interface User Stories

<!-- prettier-ignore -->
| User Stories | 08 |
| ---------- | ---- |
| **Status** | Accepted |
| **Design** | [Figma diagrams and sketches document](https://www.figma.com/file/1hX1hlUrq0QTDjMmLJrDSK/Data-Consumer-Interface)
| **Related issues** | [#756 Make Data Consumer Interface](https://github.com/blindnet-io/product-management/issues/756), [#757 Make User Stories for Data Consumer Interface](https://github.com/blindnet-io/product-management/issues/757)
| **Other documents** | [Privacy Request Interchange Vocabulary](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md), [Examples of Privacy Requests](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md), [Scenarios](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/scenarios.md), [Expected Behavior of Systems](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/expected-behavior.md)

## US-08-01

**As a** Data Consumer,

**I want to** be able to see the list of all Privacy requests (new ones and processed one) I received

**because** I need to keep track of them for legal reason

## US-08-02

**As a** Data Consumer,

**I want to** be able to be informed with a notification on the tab label when I receive a new Privacy request, and that this notification mark stays until I have answered all requests

**because** I want to easily see I have new/pending Privacy requests so I don’t forget to answers them and stay in legality

## US-08-03

**As a** Data Consumer,

**I want to** be able to choose how I want to organize the order of my list of Privacy requests according to the date : either the most recent one top to first see the ones that I just received or the most old ones to first see the ones that require to be process first 

**because** I need to organize the list in way that it is easier for me to process all Privacy requests in legal due time

## US-08-04

**As a** Data Consumer,

**I want to** clearly see the deadline by which I have to legally reply to a Privacy request 

**because** I want to stay out of any legal trouble and process all the Privacy requests I receveice in the legal due time

## US-08-05

**As a** Data Consumer,

**I want to** view the details of each Privacy request I received (date of the request, Submitter identification, type of request and details of request (data category, processing catgory, target, provenance...), additional elements if there are any such as identification document, message, data range, data capture, data reference, selected data to delete, selected data to modify, new data modified, consent restriction...)

**because** I need to take notice of them to proccess the Privact request

## US-08-06

**As a** Data Consumer,

**I want to** be able to see, download and print the details of old Privacy Requests, a proof of compliance for treated Privacy Requests, with the following information : (date of the request, Submitter identification, type of request and details of request (data category, processing catgory, target, provenance...), additional elements if there are any such as identification document, message, data range, data capture, data reference, selected data to delete, selected data to modify, new data modified, consent restriction...), type of answer (approved/partially approvec/denied), date of the answer, date of the action associated with the type of request (e.g user has accessed data)

**because** I need to keep track of them for legal reason or I might need to give to my boss or colleague

## US-08-07

**As a** Data Consumer,

**I want to** process the Privacy requests, that can't be automatically processed, directly from the interface

**because** it is not convenient for me to manually write all an email and manually fetch all elements to answer the Privacy request

## US-08-08

**As a** Data Consumer,

**I want to** be able to track the Privacy requests that are automatically processed

**because** I need to be aware of them and to keep track of them for legal reason

## US-08-09

**As a** Data Consumer,

**I want to** be able to reply to a Privacy request by also adding a message

**because** I might have to deny a Privacy request and in that case I must give a specific reason to the submitter

## US-08-10

**As a** Data Consumer,

**I want to** be guided if I need to add a message to specifiy why I must deny a Privacy Request

**because** I want to save time and I might not know what are the valid reasons to deny a Privacy request

## US-08-11 

**As a** Data Consumer,

**I want to** be able to easily access and send a Privacy request capture link 

**because** a submitter might directly ask me where they can submit a Privacy Request 

## US-08-12 

**As a** Data Consumer, receiving a Privacy request containing mulitple demands

**I want to** be able to answer to some demand today, and to some other another day

**because** I might need more time to answer some demand, for example if I need to get information I don't have at the moment

## US-08-13

**As a** Data Consumer, receiving a Privacy request containing multiple demands

**I want** the demands that I configured as to be processed automatically, to be answered right away and then receive the request with the status of each demands

**because** I need to know which demands have already been processed automatically and which demands stil need to be answered manually so that I can answer them

## US-08-14

**As a** Data Consumer,

**I want** to able to answer several times to the same Privacy request I already responded to

**because** I might need to add something more that is not in my previous answer

## US-08-15

**As a** Data Consumer,

**I want** to be informed when an [Event](https://github.com/blindnet-io/product-management/blob/priv-event/refs/schemas/priv/RFC-PRIV.md#event) can happen, or a [Retention Policy](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/RFC-PRIV.md#retention-policy) might expire, or the user may Revoke Consent (processed automatically) and as a result the Privacy Compiler might emit a recommendation for me to delete particular Fragments

**because** I want to know of such recommendations and react to them

## US-08-16

**As a** Data Consumer,

**I want** to search for a particular Data Subject among my Privacy requests history and filter only their Privacy requests 

**because** I have a long Privacy request history and it is not convenient to try to spot the name of the Data Subject I am looking for by scrolling among my Privacy request history

## US-08-17

**As a** Data Consumer, receiving a Privacy Request that I need to share with a Partner organization

**I want** to be able to easily forward the Privacy request to that Partner organization, by configuring a setting to automatically forward such request with contact of all my Partner organizations and/or being able to explicitely forward it on the interface with the possibility of configuring sugesstion to whom forward the request with contact of all my Partner organizations

**because** I want to save time and effort regarding Privacy request transfer

## US-08-18

**As a** Data Consumer, receiving a Privacy Request transmitted from a Partner organization

**I want** to know and see on the Privacy request the detail that the request is not direclty coming from the Data Subject but from a transfer by a Partner organization

**because** in that case I might want to reply to the Partner organization and not directly to the Data Subject

## US-08-19

**As a** Data Consumer, receiving a Privacy Request transmitted from a Partner organization

**I want** to be able to either answer directly to the Data Subject or to answer to the Partner organization that will transmit my answer to the Data Subject

**because** in that case I want to chose to reply to the Partner organization or to the Data Subject

## US-08-20 - other (not part of interface per se)

**As an** Organization, using blindnet devkit to automate the processing of requests

**I want to** automate a maximum of requests except the "other" type of request that I need to process manually

**because** I want to save time and effort

## US-08-21 - other (not part of interface per se)

**As a** developper from an Organization, using blindnet devkit

**I want to** I want it to automatically compute the responses to (at least some) requests such as information about server locations, privacy policy, data types, organisation identity etc (cf. list of TRANSPARENCY actions from the [PRIV examples](https://github.com/blindnet-io/product-management/blob/main/refs/schemas/priv/dictionary/actions/en.actions.json))

**because** I want to save time and effort

## US-08-22 - other (not part of interface per se)

**As a** developper from an Organization, using blindnet devkit

**I want to** be able to configure which requests / which demands (inside a request containing multiple demands) are processed automatically, and which are processed using human validation (Privacy Computation Engine gives a recommendation but a human - Data Consumer/DPO accepts or rjects it)

**because** some of the requests can be processed automatically, some others cannot and need human validation 
