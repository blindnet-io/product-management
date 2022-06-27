# Privacy Request capture service

<!-- prettier-ignore -->
| User Stories | 07 |
| ---------- | ---- |
| **Status** | Draft |
| **Design** | [Figma activity diagram (draft)](https://www.figma.com/file/miUd9PEmLrjut53rwrQViX/Data-rights-request-capture-service?node-id=0%3A1)
| **Previous discussions** | https://github.com/blindnet-io/product-ideas/issues/22
| **Other documents** | [Privacy Request Interchange Vocabulary](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md), [Examples of Privacy Requests](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md), [Scenarios](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/scenarios.md), [Expected Behavior of Systems](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/expected-behavior.md)

## Introduction

Privacy Request Capture Service is a component of the [High Level Architecture](https://github.com/blindnet-io/product-management/tree/main/refs/high-level-architecture). The user stories listed here illustrate its behavior, but are not to be considered exhaustive with regards to all the functionalities this component SHOULD offer.

When this component is installed by a System and used to interact with the Internet Users of that System, we call that **Local** Privacy Request Capture Service.

However, Systems may declare Data Captures that they are responsible for to a centralised Global service, where any Internet User can make a Privacy Request. We call this service **Global** Privacy Request Capture Service.


## 07-1 Internet User (a Submitter or a Data Subject)

### US-07-1-01

**As an** Internet User (a Submitter or a Data Subject)

**I want to** send Privacy Request to the Organization I gave my data to

**because** I want to exercise my rights

### US-07-1-02

**As an** Internet User (a Submitter or a Data Subject)

**I want to** understand how to make a Privacy Request

**because** it is unclear to me and it seems complicated

### US-07-1-03

**As an** Internet User (a Submitter or a Data Subject) (Global Privacy Request Capture Service)

**I want to** easily find the address (email or postal) I need to send my Privacy Request to

**because** it takes time and it is annoying to look for the right address

### US-07-1-04

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request (Global Privacy Request Capture Service)

**I want to** have a proposition of addresses related to the Organization I want to address my Privacy Request to, if the address is known

**because** it saves me time and it is convenient

### US-07-1-05

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request (Global Privacy Request Capture Service)

**I want to** add the address of the Organization I am sending my request to, that doesn't yet use blindnet devkit, and be able to easily access it next time

**because** I or other Internet Users might need the address of that Organization to send Privacy Requests in the future

### US-07-1-06

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want** be able to make any of the requests mentioned in the [requests list of this document](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md)

**because** this list of requests covers my data rights needs

### US-07-1-07

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request with several [Demands](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#demands) (i.e. possibility of having several demands per request)

**because** I want to exercise several data rights at the same time, on the data an Organization has on me

### US-07-1-08

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request to modify my address and to modify a field from an allergy record

**because** because I just moved and also discovered I have a new allergy

### US-07-1-09

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submit a Privacy Request to access the data that are derived from me and my behavior  

**because** I want to know what data a system has one me that I did not input myself

### US-07-1-10

**As an** Internet User (a Submitter or a Data Subject), when the request I made is rejected

**I want to** know the motive of the rejection

**because** otherwise I might get frustrated not understanding why me request has been rejected

### US-07-1-11

**As an** Internet User (a Submitter or a Data Subject),

**I want to** submint a Privacy Request to know the provenance of the data a system has on me

**because** I suspect someone might have shared my data without my authorization

### US-07-1-12

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** be guided in making my Privacy Request as precise and as correct as possible

**because** I want or avoid making a Privacy Request that is likely to be rejected (imprecise, or wrongly formulated)

### US-07-1-13

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** be guided towards making a Privacy Request in a way that makes it automatically processable

**because** I want or avoid making a Privacy Request that takes too much time (and human intervention) to process

### US-07-1-14

**As an** Internet User (a Submitter or a Data Subject), while creating a Privacy Request

**I want to** be guided about all data fields the Organization collects

**because** I want to select particular data field to modify (such as a delivery address)

### US-07-1-15

**As an** Internet User (a Submitter or a Data Subject), after submitting my data in a Data Capture

**I want to** make a Privacy Request in relation to that particular Data Capture

**because** I only want the Organization to delete that particular Data Capture, that I submitted by mistake

### US-07-1-16

**As an** Internet User (a Submitter or a Data Subject), after submitting my data in a Data Capture

**I want to** make a Privacy Request in relation to one of the two particular consents I gave when submitting that particular Data Capture

**because** I only want the Organization to continue using my data to deliver a service to me, but I no longer consent to having my data shared with any other Organization.

### US-07-1-17

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** remain anonymous or at least not prove my identity

**because** My Privacy Request only concerns TRANSPARENCY about data usage (under Art. 13 and 14. of GDPR)

### US-07-1-18

*(see [a priori](../refs/schemas/priv/scenarios.md#a-priori-authentication) and [a posteriori](../refs/schemas/priv/scenarios.md#a-posteriori-authentication) authentication)*

**As an** Internet User (a Submitter or a Data Subject), when creating a Privacy Request

**I want to** authenticate

**because** I am requesting something that requires proof of identity


### US-07-1-19

**As an** Internet User (a Submitter or a Data Subject), after creating a Privacy Request

**I want to** know the status of my Privacy Request

**because** I have been waiting for a while and have got no response yet

### US-07-1-20

**As an** Internet User (a Submitter or a Data Subject) (Global Privacy Request Capture Service)

**I want to** make one Privacy Request to all Organizations having my private phone number

**because** I am getting too many calls and I don't know which Organization is responsible for them.

## 07-2 Organization receiving Privacy Request (Global Privacy Request Capture Service)

### US-07-2-01

**As an** Organization (not using blindnet devkit) receiving Privacy Request

**I want to** know the request I received has been sent by blindnet's Privacy Request Capture Service and be informed about blindnet devkit

**because** I might be interested in the service blindnet devkit offers

### US-07-2-02

**As an** Organization (not using blindnet devkit) receiving Privacy Request

**I want to** be able to recognize the user who made the request in my system

**because** like that I can easily identify their data

### US-07-2-03

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** receive the request in the Privacy Request section of my system

**because** it is more convenient for me to have all my Privacy Requests centralized

### US-07-2-04

**As an** Organization (using or not using blindnet devkit) receiving Privacy Request

**I want to** transfer the request to another Organization if the request concerns data I transferred to another Organization or data I got from another Organization

**because** I need to be compliant, if a user wants their data deleted, I have to inform the other company I transferred the user's data to or I got the user's data from, to also delete the data

## 07-3 Organization using Local Privacy Request capture service

### US-07-3-01

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** have an entry point for the Privacy Request service embedded on the GDPR section of my website

**because** my customers might directly go to my website to make their Privacy Request, and it is easier for my customers and for me to use this service

### US-07-3-02

**As an** Organization, using blindnet devkit, receiving Privacy Request

**I want to** receive the Privacy Requests in a format that is compatible with my system

**because** otherwise I cannot use blindnet devkit for Privacy Request capture

### US-07-3-03

**As an** Organization, using blindnet devkit

**I want to** only use some of the components, a subset of the scope of blindnet devkit for things I don't have yet

**because** I want to continue using my existing system that already covers some of my compliance needs (e.g my system already allows users to log in and modify data adresses, preferences etc - on Amazon, Facebook, etc)

### US-07-3-04

**As an** Organization, using blindnet devkit

**I want to** use the whole blindnet devkit to automate the processing of requests

**because** I don't have any system that covers my compliance needs, I do everything manually

### US-07-3-05

**As an** Organization, using blindnet devkit

**I want to** use blindnet devkit to automate the processing of requests except for "other" type of request

**because** I need to process "other" type of request manually

### US-07-3-06

**As a** developper from an Organization, using blindnet devkit

**I want to** use only the capture interface component (from the HLA) to generate a json file for a request

**because** this is all I need, as I want to handle the file and import it to some other system

### US-07-3-07

**As a** developper from an Organization, using blindnet devkit

**I want to** use the capture interface component and the data consumer interface component (from the HLA)

**because** I need to generate a JSON file for the requests and also to view the requests. From there I will treat the requests manually

### US-07-3-08

**As a** developper from an Organization, using blindnet devkit

**I want to** configure the data rights computation engine component (from the HLA) in my system with information about server locations, privacy policy, data types, organisation identity etc (cf. list of TRANSPARENCY actions from the [PRIV examples](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/examples.md))

**because** I want it to automatically compute the responses to (at least some) requests

### US-07-3-09

**As an** Organization, using blindnet devkit

**I want to** be able to keep track of Data Subject's data transfers between one system and another

**because** I need to know the provenance and/or where has been transfered Data Subject's data to, in order to complete some Privacy Requests
