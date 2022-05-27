# Data rights request capture service

<!-- prettier-ignore -->
| User Stories | 07 |
| ---------- | ---- |
| **Status** | Draft |
| **Design** | [Figma activity diagram (draft)](https://www.figma.com/file/miUd9PEmLrjut53rwrQViX/Data-rights-request-capture-service?node-id=0%3A1)
| **Previous discussions** | https://github.com/blindnet-io/product-ideas/issues/22
| **Other documents** | [Requests list](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/RFC-rights-request-interoperability-format.md)

## 07-1 Internet user (a submitter or a data subejct)

### US-07-1-01

**As an** internet user (a submitter or a data subejct)

**I want to** send Data rights request to the organization I gave my data to

**because** I want to exercise my rights 

### US-07-1-02

**As an** internet user (a submitter or a data subejct)

**I want to** understand how to make a Data rights request

**because** it is unclear to me and it seems complicated

### US-07-1-03

**As an** internet user (a submitter or a data subejct) (Global data rights request capture service)

**I want to** easily find the address (email or postal) I need to send my Data rights request to 

**because** it takes time and it is annoying to look for the right address 

### US-07-1-04

**As an** internet user (a submitter or a data subejct), when creating a Data rights request (Global data rights request capture service)

**I want to** have a proposition of addresses related to the organization I want to address my Data rights request to, if the address is known

**because** it saves me time and it is convenient

### US-07-1-05

**As an** internet user (a submitter or a data subejct), when creating a Data rights request (Global data rights request capture service)

**I want to** add the address of the organization I am sending my request to, that doesn't use blindnet devkit/Privaform, and be able to easily access it next time

**because** I or other users might need the address of that organization to send Data rights request in the future

### US-07-1-06

**As an** internet user (a submitter or a data subejct), when creating a Data rights request

**I want** be able to make any of the requests mentionned in the [requests list of this document](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/RFC-rights-request-interoperability-format.md)

**because** this list of requests covers my data rights needs

### US-07-1-07

**As an** internet user (a submitter or a data subejct), when creating a Data rights request

**I want to** send several demands per request

**because** I want to exercise several data rights at the same time, on the data an organization has on me

### US-07-1-08

**As an** internet user (a submitter or a data subejct), when creating a Data rights request

**I want to** modify my address and to modify a field from an allergy record 

**because** because I just moved and also dicovered I have a new allergy

## 07-2 Organization receiving Data rights request (Global data rights request capture service)

### US-07-2-01

**As an** organization (not using blindnet devkit) receiving Data rights request 

**I want to** know the request I received has been sent by blindnet Data rights request capture service and be informed about Privateform

**because** I might be interested in the service Privateform offers

### US-07-2-02

**As an** organization (not using blindnet devkit) receiving Data rights request 

**I want to** be able to recognize the user who made the request in my system

**because** so I can easily identify their data

### US-07-2-03

**As an** organization, using blindnet devkit, receiving Data rights request 

**I want to** receive the request in the Data rights request section of my system/my Privatefrom account

**because** it is more convenient for me to have all my Data rights requests centralised

### US-07-2-04

**As an** organization (using or not using blindnet devkit) receiving Data rights request

**I want to** transfer the request to another organization if the request concerns data I transfered to another organization

**because** I need to be compliant, if a user wants their data deleted, I have to inform the other company I transfered the user's data to to also delete the data

## 07-3 Organization using Local data rights request capture service

### US-07-3-01

**As an** organization, using blindnet devkit, receiving Data rights request

**I want to** have an entry point for the Data rights request service embedded on the GDPR section of my website

**because** my customers might direclty go to my website to make their Data rights request, and it is easier for my cutomers and for me to use this service

### US-07-3-02

**As an** organization, using blindnet devkit, receiving Data rights request

**I want to** receive the Data rights requests in a format that is compatible with my system

**because** otherwise I cannot use blindnet devkit to for data rights request capture 


### US-07-3-03
**As an** organization, using blindnet devkit

**I want to** only use some of the components, a subset of the scope of blindnet devkit for things I don't have yet

**because** I want to continue using my existing interface that already covers some of my compliance needs

### US-07-3-04
**As an** organization, using blindnet devkit

**I want to** only use some of the components, a subset of the scope of blindnet devkit for things I don't have yet

**because** I want to continue using my existing system that already covers some of my compliance needs (e.g my system already allows users to log in and modify data adresses, preferences etc - on Amazon, Facebook, etc)

### US-07-3-05
**As an** organization, using blindnet devkit

**I want to** use the whole blindnet devkit to automate the processing of requests

**because** I don't have any system that covers my compliance needs, I do everything manually

### US-07-3-06
**As an** organization, using blindnet devkit

**I want to** use blindnet devkit to automate the processing of requests except for "other" type of request

**because** I need to process "other" type of request manually 
