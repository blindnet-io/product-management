# RFC Lexicon 2

| Status        | proposed                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io)             |
| **PR**   | [694](https://github.com/blindnet-io/product-management/pull/694) |
| **Version**   | 2.0                                                                             |
| **Updated**   | 2022-06-14                                                                             |
| **Obsoletes** | [privateform-lexicon.csv](https://github.com/blindnet-io/product-management/blob/2b44581255fbe431cd056ebdb332c7f9067b0121/refs/privateform-lexicon.csv) |

## Introduction

>
> “The limits of language are the limits of my world.” - Ludwig Wittgenstein
>

Many product-related documents refer to terms of common interest, often written in [initial caps, or all caps](https://en.wikipedia.org/wiki/Letter_case#Stylistic_or_specialised_usage). This document defines the meaning of these terms as they should be interpreted in the context of blindnet products.

## Terms

### blindnet devkit

A set of software components for implementing [privacy-enabled connectedness](../notion-of-privacy/notion-of-privacy.md#privacy-enabled-connectedness).

### CCPA

California Consumer Privacy Act. A regulation in California (USA). See [official text](https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=201720180AB375).

### CPRA

California Privacy Rights Act. A regulation in California (USA). See [official text](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf).

### Capture Fragment

See [Data Capture Fragment](#data-capture-fragment).

### Component

A part of a [System](#system), interdependent with other Components of the same System.

### Data Capture

A compound unit of data, concerning a [Data Subject](#data-subject), made available to an [Organization](#organization) and processed by that Organization's [System(s)](#system).

It is composed of one or more [Data Capture Fragments](#data-capture-fragment).

It is obtained in any way, including: directly submitted by a [Submitter](#submitter)(who is the same as the Data Subject, or not), transferred from System to System, generated or inferred by a System.

### Data Capture Fragment

Part of a [Data Capture](#data-capture). A meaningful compound of atomic information units (e.g, data fields of different type, files, and to them associated labels) that are meaningfully captured together.

Examples of situations in which information units are meaningfully captured together include:
- splitting them would introduce an obstacle to making sense of the information that they carry. For example, elements of an address such as street number and street name,
- it doesn’t make sense to capture one of them today and the other tomorrow,
- they are not likely to be modified separately.

Also know as Capture Fragment, or Fragment.

### Data Consumer

A human, or a other entity consuming the data concerning [Data Subjects](#data-subject).

### Data Subject

A human, concerned by particular data that a [System](#system) is processing. Holder of rights over the data concerning them.

### DPO

A Data Protection Officer. An individual or a company charged with responding to [Privacy Requests](#privacy-request) in the name of an [Organization](#organization).

### Fragment

See [Data Capture Fragment](#data-capture-fragment).

### GDPR

General Data Protection Regulation. A regulation in the European Union. See [official text](https://eur-lex.europa.eu/eli/reg/2016/679/oj).

### HIPPA

Health Insurance Portability and Accountability Act. A regulation in the USA. See [official text](https://www.govinfo.gov/content/pkg/PLAW-104publ191/html/PLAW-104publ191.htm).

### Internet User

See [User](#user).

### Organization

A structure, commercial or not, processing [Data Subjects'](#data-subject) data as a part of its operations.
Also known as "controller", "data controller", and "processor" under [GDPR](#GDPR).
Also know as "business" under [CCPA](#CCPA) and [CPRA](#CPRA).

It operates one or more [Systems](#system).

### Privateform

[User](#user)-facing software that uses [blindnet devkit](#blindnet-devkit) to capture user data (and to it associated metadata) in a way that restitutes confidentiality and control to the [Data Subject](#data-subject).

### Privacy Request

A request made by a [Data Subject](#data-subject) in order to regulate privacy in the relationship they have with a [System](#system) or an [Organization](#organization).

Privacy Requests MAY concern any aspect of the [privacy-enabled connectedness](../notion-of-privacy/notion-of-privacy.md#privacy-enabled-connectedness), including transparency, confidentiality and control over data processing.

### System

A combination of hardware and software which forms a complete, working computer.
It is the unit of processing of [Data Subjects'](#data-subject) data.

A System may interoperate with other Systems while maintaining a certain level of autonomy.
It has one or more [Components](#components).

### Submitter

A human providing data.

### User

A human. Potentially one (or more) of [Data Consumer](#data-consumer), [Data Subject](#data-subject), [DPO](#dpo), [Submitter](#submitter).

## Extending the Lexicon

README.md file of [refs/lexicon](./README.md) point to the current version of the lexicon.

To make a new version, propose a new RFC, mention the current version is **Obsoletes**, and redirect the README.md to this new RFC.
