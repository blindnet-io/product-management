# Privacy Request capture service User Stories

<!-- prettier-ignore -->
| User Stories | 07 |
| ---------- | ---- |
| **Status** | Draft |
| **Design** | [Figma activity diagram (draft)](https://www.figma.com/file/miUd9PEmLrjut53rwrQViX/Data-rights-request-capture-service?node-id=0%3A1) |
| **Previous discussions** | blindnet-io/product-ideas/issues/22 |
| **Other documents** | [Privacy Request Interchange Vocabulary](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md), [Examples of Privacy Requests](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md), [Scenarios](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/scenarios.md), [Expected Behavior of Systems](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/expected-behavior.md) |

## Introduction

Privacy Request Capture Service is a component of the [High Level Architecture](https://github.com/blindnet-io/product-management/tree/main/refs/high-level-architecture). The user stories listed here illustrate its behavior, but are not to be considered exhaustive with regards to all the functionalities this component SHOULD offer.

When this component is installed by a System and used to interact with the Internet Users of that System, we call that **Local** Privacy Request Capture Service.

However, Systems may declare Data Captures that they are responsible for to a centralised Global service, where any Internet User can make a Privacy Request. We call this service **Global** Privacy Request Capture Service.

## 07-1 Common US for Local and Global Privacy Request Capture Service

### US-07-1-01

**As an** Internet User (a Submitter or a Data Subject)

**I want to** send Privacy Request to the Organization I gave my data to

**because** I want to exercise my rights

### US-07-1-02

**As an** Internet User (a Submitter or a Data Subject)

**I want to** understand how to make a Privacy Request

**because** it is unclear to me and it seems complicated

### US-07-1-03

**As an** Internet User (a Submitter or a Data Subject),

**I want** be able to make any of the requests mentioned in the [list of request examples this document](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md)

**because** all my different privacy needs need to be covered

### US-07-1-04

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request with several [Demands](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#demands) (i.e. possibility of having several demands per request)

**because** I want to exercise several privacy rights at the same time, on the data an Organization has on me

### US-07-1-05

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want** be able to make any of the demands mentioned in this [list of action](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/actions/en.actions.json)

**because** thoses actions cover my possible privacy needs

### US-07-1-06

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want** be able to define a demand for a particular type of data among this [list of data categories](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/data-categories/en.data-categories.json), and/or for a particular type of processing among this this [list of processing categories](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/processing-categories/en.processing-categories.json), and/or for a particular purpose of processing among this [list of purposes](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/purposes/en.purposes.json), and/or restrict the action requested by my demand based on any combination of [Privacy Scope](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#privacy-scope), [Consent Restriction](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#consent-restriction), [Capture Restriction](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#capture-restriction), [Date Range](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#date-range), [Provenance Restriction](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#provenance-restriction), [Data Reference Restriction](https://github.com/blindnet-io/product-management/edit/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#data-reference-restriction), or [target](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#targets).

**because** my demand doesn't concern all of the data the Organization has on me, nor all the processing for all the purposes, but just a part of it

### US-07-1-07

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request to modify my address and to modify a field from an allergy record

**because** because I just moved and also discovered I have a new allergy

### US-07-1-08

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request to access some specific data : the data that are derived from me and my behavior

**because** I want to know what data a system has one me that I did not input myself

### US-07-1-09

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submint a Privacy Request to know the [provenance](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/provenance/en.provenance.json) of the data a system has on me

**because** I suspect someone might have shared my data without my authorization

### US-07-1-10

**As an** Internet User (a Submitter or a Data Subject), submitting a Privacy Request to an Organization

**I want** my request to be taken into account by some or all possible targets from this [targets list](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/targets/en.targets.json)

**because** I want my Privacy Request to be fully completed

### US-07-1-11

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** be guided in making my Privacy Request as precise and as correct as possible

**because** I want or avoid making a Privacy Request that is likely to be rejected (imprecise, or wrongly formulated)

### US-07-1-12

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** be guided towards making a Privacy Request in a way that makes it automatically processable

**because** I want or avoid making a Privacy Request that takes too much time (and human intervention) to process

### US-07-1-13

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** remain anonymous or at least not prove my identity

**because** My Privacy Request only concerns TRANSPARENCY about data usage (under Art. 13 and 14. of GDPR)

### US-07-1-14

*(see [a priori](../refs/schemas/priv/scenarios.md#a-priori-authentication) and [a posteriori](../refs/schemas/priv/scenarios.md#a-posteriori-authentication) authentication)*

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** authenticate

**because** I am requesting something that requires proof of identity

### US-07-1-15

**As an** Internet User (a Submitter or a Data Subject), after creating a Privacy Request

**I want to** know the status of my Privacy Request

**because** I have been waiting for a while and have got no response yet

### US-07-1-16

**As an** Internet User (a Submitter or a Data Subject), after creating a Privacy Request

**I want to** know the see/download the data concerning me

**because** the Privacy Request I made included an `ACCESS` demand.

### US-07-1-17

**As an** Internet User (a Submitter or a Data Subject), creating a Privacy Request

**I want to** be able to specifiy a specific demand and/or a specific elements of the demand

**because** I can't find what I want to request in the proposed elements

## 07-2 US specific to Local Privacy Request capture service

### US-07-2-01

**As an** Internet User (a Submitter or a Data Subject), while creating a Privacy Request

**I want to** be guided about all data fields the Organization collects

**because** I want to select particular data field to modify (such as a delivery address)

### US-07-2-02

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** have an entry point for the Privacy Request service embedded on the GDPR section of my website

**because** my customers might directly go to my website to make their Privacy Request, and it is easier for my customers and for me to use this service

### US-07-2-03

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** receive the Privacy Requests in a format that is compatible with my system

**because** otherwise I cannot use blindnet devkit for Privacy Request capture

### US-07-2-04

**As an** Organization, using blindnet devkit

**I want to** only use some of the components, a subset of the scope of blindnet devkit for things I don't have yet

**because** I want to continue using my existing system that already covers some of my compliance needs (e.g my system already allows users to log in and modify data adresses, preferences etc - on Amazon, Facebook, etc)

### US-07-2-05

**As an** Internet User (a Submitter or a Data Subject), after submitting my data in a Data Capture to an Organization using blindnet devkit

**I want to** make a Privacy Request in relation to one of the two particular consents I gave when submitting that particular Data Capture

**because** I only want the Organization to continue using my data to deliver a service to me, but I no longer consent to having my data shared with any other Organization.

### US-07-2-06

**As an** Internet User (a Submitter or a Data Subject), after submitting my data in a Data Capture to an Organization using blindnet devkit

**I want to** make a Privacy Request in relation to that particular Data Capture

**because** I only want the Organization to delete that particular Data Capture, that I submitted by mistake

### US-07-2-07

**As an** Organization, using blindnet devkit

**I want to** set up the data catgory, processing category and purpose category elements to the ones that are applicable in my case (ie only keeping the applicable elements)

**because** limiting the choice to only applicable elements will help the Internet user (a Submitter or a Data Subject) save timle by offering him the choice among only applicable demands and limit the submission of non applicable demands that will be automatically rejected

### US-07-2-08

**As an** Organization, using blindnet devkit

**I want to** offer a list of recommended/most frequent requests made to the Internet user (a Submitter or a Data Subject) who wants to create a request

**because** it can help them save time by quickly choose a pre-defined request among the list of recommened recommended/most frequent requests made

### US-07-2-09

**As an** Organization, using blindnet devkit

**I want to** to be able set the [target](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/dictionary/targets/en.targets.json) elements (SYSTEM, ORGANISATION, PARTNERS) to make them applicable to my case (ie only keeping the applicable elements and/or changing the wording on the interface to make it more understable for the user)

**because** I may be a big company with different systems offering different services (e.g organization = meta, system= instagram, a user might want to delete his data only from instragram) or I may be a small company and my organisation only have one system

## 07-3 US specific to Global Privacy Request Capture Service

### US-07-3-01

**As an** Internet User (a Submitter or a Data Subject)

**I want to** easily find the address (email or postal) I need to send my Privacy Request to

**because** it takes time and it is annoying to look for the right address

### US-07-3-02

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** have a proposition of addresses related to the Organization I want to address my Privacy Request to, if the address is known

**because** it saves me time and it is convenient

### US-07-3-03

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** add the address of the Organization I am sending my request to, that doesn't yet use blindnet devkit, and be able to easily access it next time

**because** I or other Internet Users might need the address of that Organization to send Privacy Requests in the future

### US-07-3-04

**As an** Internet User (a Submitter or a Data Subject)

**I want to** make one Privacy Request to all Organizations having my private phone number

**because** I am getting too many calls and I don't know which Organization is responsible for them.

### US-07-3-05

**As an** Organization (not using blindnet devkit) receiving Privacy Request

**I want to** know the request I received has been sent by blindnet's Privacy Request Capture Service and be informed about blindnet devkit

**because** I might be interested in the service blindnet devkit offers

### US-07-3-06

**As an** Organization (not using blindnet devkit) receiving Privacy Request

**I want to** be able to recognize the user who made the request in my system

**because** it will allow me to easily identify their data

### US-07-3-07

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** receive the request in the Privacy Request section of my system

**because** it is more convenient for me to have all my Privacy Requests centralized

### US-07-3-08

**As an** Organization (using or not using blindnet devkit) receiving Privacy Request

**I want to** transfer the request to another Organization if the request concerns data I transferred to another Organization or data I got from another Organization

**because** I need to be compliant, if a user wants their data deleted, I have to inform the other company I transferred the user's data to or I got the user's data from, to also delete the data

## 07-4 Other

### US-07-4-01

**As an** Internet User (a Submitter or a Data Subject), when the request I made is rejected

**I want to** know the motive of the rejection

**because** otherwise I might get frustrated not understanding why me request has been rejected

### US-07-4-02

**As a** developper from an Organization, using blindnet devkit

**I want to** use only the capture interface component (from the HLA) to generate a json file for a request

**because** this is all I need, as I want to handle the file and import it to some other system

### US-07-4-03

**As an** Organization, using blindnet devkit

**I want to** be able to keep track of Data Subject's data transfers between one system and another

**because** I need to know the provenance and/or where has been transfered Data Subject's data to, in order to complete some Privacy Requests
