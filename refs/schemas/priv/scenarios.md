# Privacy Request Interchange Vocabulary : Scenarios of Use

| Status        | NA / supporting document                                                               |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io)         |
| **Updated**   | 2022-06-10                                                                             |

## Introduction

This document illustrates different scenarios in which [Privacy Request Interchange Vocabulary](./RFC-PRIV.md) MAY be used.

The goal of this document is to explore the design implications for implementing systems, that might arise from different situations.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-conceptualization/)
- Privacy Compiler was formerly known as Data Rights Compiler
- Privacy Request was formerly known as Data Rights Request
- All the concepts, properties and terms listed in the [Proposal](./RFC-PRIV.md#proposal) section of PRIV(Privacy Request Interchange Vocabulary are to be interpreted as defined in [Privacy Request Interchange Vocabulary](./RFC-PRIV.md#proposal)

## Authentication
### Anonymous

Systems MAY process certain requests without asking the user for their identity. This is especially the case with some of the `TRANSPARENCY` requests, in response to which general information is given.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    subject->>system: Privacy Request TRANSPARENCY.WHERE
    system->>compiler: Privacy Request
    compiler->>system: recommend GRANTED
    note right of compiler: data: "France"
    system->>subject: Privacy Request GRANTED
    note left of system: Our servers are in France
```

In certain cases, such as with GDPR ([articles 13 and 14](./examples.md#articles-13-and-14)), Systems MAY find themselves in obligation to provide information prior to capturing any data. However, in such cases, Systems are expected to [respond differently to the same requests](./expected-behavior.md#resolving-requests), with regards to the Data Subject being authenticated or not. For example a `TRANSPARENCY.DATA-CATEGORIES` request for an anonymous Data Subject MAY trigger a response listing all the possible data categories that the System is configured to collect. The same request for the authenticated Data Subject MAY trigger a response listing only the categories of data that the System has on this particular Data Subject.

### A Priori Authentication

The Data Subject formulates a Privacy Request when their identity is already confirmed.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    subject->>system: authenticates
    subject->>system: Privacy Request DELETE CONTACT.PHONE
    system->>compiler: Privacy Request
    compiler->>system: recommend GRANTED
    system->>subject: Privacy Request GRANTED
    note left of system: Phone number deleted
```


### A Posteriori Authentication

The Data Subject formulates a Privacy Request before their identity is confirmed.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    subject->>system: Privacy Request DELETE CONTACT.PHONE
    system->>subject: please authenticate
    note left of system: We must verify your identity in order to process this kind of request
    subject->>system: authenticates
    system->>compiler: Privacy Request
    compiler->>system: recommend GRANTED
    system->>subject: Privacy Request GRANTED
    note left of system: Phone number deleted
```

### Signle Point Authentication for Corresponding Systems

In a context of multiple corresponding Systems, only one System confirms the identity of the user, and other Systems only process the Privacy Request.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant systemA as System A
    participant compilerA as Privacy Compiler A
    participant systemB as System B
    participant compilerB as Privacy Compiler B

    alt a priori authentication
    subject->>systemA: authenticates
    subject->>systemA: Privacy Request DELETE CONTACT.EMAIL target:PARTNERS

    else a posteriori authentication
    subject->>systemA: Privacy Request DELETE CONTACT.EMAIL target:PARTNERS
    systemA->>subject: please authenticate
    subject->>systemA: authenticates
    end

    systemA->>compilerA: Privacy Request

    systemA->>systemB: Privacy Request
    systemA->>systemB: Data Subject Identity Confirmed
    systemB->>compilerB: Privacy Request

    compilerA->>systemA: recommend GRANTED
    compilerB->>systemB: recommend GRANTED

    alt coordinated response
    systemB->>systemA: Privacy Request GRANTED
    systemA->>subject: Privacy Request GRANTED

    else direct response
    systemA->>subject: Privacy Request GRANTED
    systemB->>subject: Privacy Request GRANTED
    end

    note left of systemA: E-mail deleted
```

### Independent Authentication for Corresponding Systems

In a context of multiple corresponding Systems, every System confirms the identity of the Data Subject in their own way.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant systemA as System A
    participant compilerA as Privacy Compiler A
    participant systemB as System B
    participant compilerB as Privacy Compiler B

    alt a priori authentication
    subject->>systemA: authenticates
    subject->>systemA: Privacy Request DELETE CONTACT.EMAIL target:PARTNERS

    else a posteriori authentication
    subject->>systemA: Privacy Request DELETE CONTACT.EMAIL target:PARTNERS
    systemA->>subject: please authenticate
    subject->>systemA: authenticates
    end

    systemA->>compilerA: Privacy Request

    systemA->>systemB: Privacy Request
    systemB->>subject: please authenticate
    subject->>systemB: authenticates
    systemB->>compilerB: Privacy Request

    compilerA->>systemA: recommend GRANTED
    compilerB->>systemB: recommend GRANTED

    alt coordinated response
    systemB->>systemA: Privacy Request GRANTED
    systemA->>subject: Privacy Request GRANTED

    else direct response
    systemA->>subject: Privacy Request GRANTED
    systemB->>subject: Privacy Request GRANTED
    end

    note left of systemA: E-mail deleted
```

## Automation

### Automatic Processing

Systems MAY be configured to process certain Privacy Requests automatically.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    actor DPO

    note left of subject: New e-mail example@gmail.com

    alt a priori authentication
    subject->>system: authenticates
    subject->>system: Privacy Request MODIFY CONTACT.EMAIL

    else a posteriori authentication
    subject->>system: Privacy Request MODIFY CONTACT.EMAIL
    system->>subject: please authenticate
    subject->>system: authenticates

    end

    system->>compiler: Privacy Request
    compiler->>system: recommend GRANTED
    system->>subject: Privacy Request GRANTED
    note left of system: E-mail modified

    system->>DPO: Privacy Request GRANTED

```

### Semi-Automatic Processing

Systems MAY be configured to process certain Privacy Requests with human validation.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    actor DPO

    note left of subject: New e-mail example@gmail.com

    alt a priori authentication
    subject->>system: authenticates
    subject->>system: Privacy Request MODIFY CONTACT.EMAIL

    else a posteriori authentication
    subject->>system: Privacy Request MODIFY CONTACT.EMAIL
    system->>subject: please authenticate
    subject->>system: authenticates

    end

    system->>subject: Privacy Request UNDER-REVIEW

    system->>compiler: Privacy Request
    compiler->>system: recommend GRANTED

    system->>DPO: Privacy Request, recommend GRANTED

    DPO->>system: Privacy Request DENIED
    note right of DPO: We require a professional e-mail address

    system->>subject: Privacy Request DENIED

```

### Manual Processing

Certain Privacy Request can't be interpreted automatically and MUST be processed by a human.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant system as System
    participant compiler as Privacy Compiler
    actor DPO

    note left of subject: How much CO2 is spent on processing my data

    alt a priori authentication
    subject->>system: authenticates
    subject->>system: Privacy Request OTHER-DEMAND

    else a posteriori authentication
    subject->>system: Privacy Request OTHER-DEMAND
    system->>subject: please authenticate
    subject->>system: authenticates

    end

    system->>subject: Privacy Request UNDER-REVIEW

    system->>DPO: Privacy Request

    DPO->>system: Privacy Request GRANTED
    note right of DPO: 30g

    system->>subject: Privacy Request GRANTED, msg=30g

```
## Response

## Coordinated Response

When a Privacy Requests concerns corresponding Systems, they MAY be configured to respond to it in a coordinated way. The System having received the Privacy Requests gathers responses from corresponding Systems, and creates one single response to present to the user.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant systemA as System A
    participant compilerA as Privacy Compiler A
    participant systemB as System B
    participant compilerB as Privacy Compiler B


    subject->>systemA: Privacy Request TRANSPARENCY.WHERE

    systemA->>compilerA: Privacy Request

    systemA->>systemB: Privacy Request
    systemB->>compilerB: Privacy Request

    compilerA->>systemA: recommend GRANTED, France
    compilerB->>systemB: recommend GRANTED, USA

    systemB->>systemA: Privacy Request GRANTED, USA
    systemA->>subject: Privacy Request GRANTED, France and USA

```
## Direct Response

When a Privacy Requests concerns corresponding Systems, they MAY be configured to have each System reply to the Data Subject independently.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant systemA as System A
    participant compilerA as Privacy Compiler A
    participant systemB as System B
    participant compilerB as Privacy Compiler B


    subject->>systemA: Privacy Request TRANSPARENCY.WHERE, target:PARTNERS

    systemA->>systemB: Privacy Request

    systemA->>compilerA: Privacy Request
    compilerA->>systemA: recommend GRANTED, France
    systemA->>subject: Privacy Request GRANTED, France


    systemB->>compilerB: Privacy Request
    compilerB->>systemB: recommend GRANTED, USA
    systemB->>subject: Privacy Request GRANTED, USA

```

## Capture

## A Complex Journey of a Data Capture

A Data Capture MAY end up being shared among several Systems. We illustrate this on an example. System A and System B are a part of the same Organization, while System C is a part of a Partner Organization.

This complex scenario may take place under different [authentication](#authentication), [automation](#automation), and [response](#response) scenarios. For the sake of clarity of the diagram, we don't include all the possible options. We also abstract Privacy Compilers and interactions with them, as well as Data Consumers and DPOs.

```mermaid
sequenceDiagram
    actor subject as Data Subject
    participant systemA as System A
    participant systemB as System B
    participant systemC as System C

    subject->>systemA: name, e-mail
    subject->>systemA: phone number

    systemA->>systemA: Data Capture CONTACT, provenance:USER

    systemA->>systemA: Data Capture DEVICE (iPhone 13), provenance:DERIVED

    subject->>systemA: consent1 purpose: ADVERTISING, PERSONALIZATION, target: ORGANIZATION
    subject->>systemA: consent2 purpose: ADVERTISING, PERSONALIZATION, target: PARTNERS

    systemA->>systemB: Data Capture, Consent
    systemB->>systemC: Data Capture, Consent

    systemC->>subject: Advertising e-mail

    subject->>systemB: Privacy Request REVOKE-CONSENT consent2 target: PARTNERS.DOWNWARD
    systemB->>systemC: Privacy Request REVOKE-CONSENT consent2

    systemC->>systemB: Privacy Request GRANTED
    systemC->>systemC: Delete Data Subject's data, Delete consent2

    systemB->>subject: Privacy Request GRANTED

    systemA->>subject: Advertising e-mail

    subject->>systemA: Privacy Request OBJECT purpose:ADVERTISING, target: ORGANIZATION
    systemA->>systemB: Privacy Request OBJECT purpose:ADVERTISING

    systemA->>systemA: consent1->consent1.1 purpose: PERSONALIZATION, target: ORGANIZATION
    systemB->>systemB: consent1->consent1.1 purpose: PERSONALIZATION, target: ORGANIZATION

    systemB->>systemA: Privacy Request GRANTED
    systemA->>subject: Privacy Request GRANTED

    subject->>systemA: Privacy Request ACCESS provenance:TRANSFERRED,DERIVED target: ORGANIZATION

    systemA->>subject: Privacy Request GRANTED
    note left of systemA: DEVICE (iPhone 13)

    systemB->>subject: Privacy Request GRANTED
    note left of systemB: CONTACT (name, e-mail, phone) DEVICE (iPhone 13)

    subject->>systemA: Privacy Request RESTRICT provenance:USER target: ORGANIZATION
    systemA->>systemB: Privacy Request RESTRICT provenance:USER target: ORGANIZATION

    systemA->>systemA: Delete DEVICE (iPhone 13)
    systemB->>systemB: Delete DEVICE (iPhone 13)
    systemB->>systemA: Privacy Request PARTIALLY-GRANTED
    note right of systemB: VALID-REASONS not to delete CONTACT (name, e-mail, phone)

    systemA->>subject: Privacy Request PARTIALLY-GRANTED
    note right of systemA: DEVICE (iPhone 13) deleted from all Systems. Contact data kept.

```


## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- CPRA
- HIPPA
