# Simple Privacy Engineering Principles

| Status        | Accepted                                                                              |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [704](https://github.com/blindnet-io/product-management/pull/704)                    |
| **Author(s)** | [milstan](https://github.com/milstan) (milstan@blindnet.io)                           |
| **Updated**   | 2022-06-20                                                                             |


## Introduction

Privacy is a complex yet essential component of human socialization.
Ever since software Systems became tools for human connectedness, a need emerged to engineer privacy in them.

[Academic research](../notion-of-privacy.md) offers insight into the definition and function of privacy. Growing body of [regulation](#privacy-legislation) specifics how software Systems and Organizations operating them should behave in order to ensure privacy. Yet, it remains challenging for a software engineer to grasp all that information and translate it into design of a software System.

We propose simple engineering principles that embody key understandings of privacy in the context of software engineering.
While it is impossible to guarantee compliance with [regulation](#privacy-legislation) upfront, Systems engineered in the spirit of these principles are more likely than others to be compliant or easily made compliant with privacy regulations.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)


## Principles

### Transparency

> To let the user know.

Transparency means letting the user know what to expect (upfront transparency), and what is actually going on (ongoing transparency).

Transparency refers to different kinds of information that the user might want to know.
Particular [regulations](#privacy-legislation) define specific information.

Among the most common are:

- Who can access the data
- Where is the data stored
- What is done with the data
- Why is data being collected and used
- For how long is the data kept


### Confidentiality

> To keep the unintended parties away.

Data is handled in a way that ensures that only the intended parties can access it.
This might involve different approaches to security and access management.
The System (and its administrators and the Organization controlling it) may be an unintended party.
Particular [regulations](#privacy-legislation) impose specific techniques.

### Control

> To let the user negotiate the data usage.

Control means letting the users make requests related to data concerning them.
The usage of data is negotiated within the limits of what the System needs to fulfill its purpose.

Particular [regulations](#privacy-legislation) define specific requests the users must be able to make.


## References

### Normative References

- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,

### Informative References

- [Notion of Privacy](../notion-of-privacy/notion-of-privacy.md)
- [Privacy by design](https://en.wikipedia.org/wiki/Privacy_by_design)

### Privacy Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)
- [CPRA](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf)
- [HIPPA](https://www.govinfo.gov/content/pkg/PLAW-104publ191/html/PLAW-104publ191.htm)
- [New Zealand Privacy Act 2020](https://www.legislation.govt.nz/act/public/2020/0031/latest/LMS23333.html)
- [LFPDPPP](https://www.diputados.gob.mx/LeyesBiblio/pdf/LFPDPPP.pdf)
- [LGPD](https://gdpr.eu/gdpr-vs-lgpd/)
- [Canada Privacy Act](https://www.priv.gc.ca/en/privacy-topics/privacy-laws-in-canada/the-privacy-act/)
