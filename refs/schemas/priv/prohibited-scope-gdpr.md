# Privacy Request Interchange Vocabulary : Prohibited Privacy Scope under GDPR

| Status        | NA / supporting document                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | [milstan](https://github.com/milstan)        |
| **Updated**   | 2022-06-25                                                                             |

## Introduction

[Privacy Request Interchange Vocabulary](./RFC-PRIV.md) defines the notion of [Privacy Scope](./RFC-PRIV.md#privacy-scope). [Expected Behavior of Implementing Systems](./expected-behavior.md) document further specifies the Privacy Scope algebra.

However, [certain **(Privacy Scope)-(Legal Base) pairs** are simply prohibited by legislation](./expected-behavior.md#privacy-algebra) and Systems MAY be configured to reject them.

This document specifies such **(Privacy Scope)-(Legal Base) pairs** prohibited under GDPR. The list covers most general cases, under assumption that no particular country-specific regulation has specified particular rules.

Systems working under GDPR MAY be use those lists to facilitate compliance. Rejecting those prohibited scopes is not enough to ensure compliance. Not rejecting them is likely to put the System in a situation of non-compliance.

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-conceptualization/)
- Privacy Compiler was formerly known as Data Rights Compiler
- Privacy Request was formerly known as Data Rights Request
- All the concepts, properties and [Terms](./RFC-PRIV.md#terms) listed in the [Proposal](./RFC-PRIV.md#proposal) section of PRIV(Privacy Request Interchange Vocabulary are to be interpreted as defined in [Privacy Request Interchange Vocabulary](./RFC-PRIV.md#proposal)

## Prohibited Scopes

### Art. 9 of GDPR

Under `LEGITIMATE-INTEREST` or `CONTRACT` legal bases, (unless data are manifestly made public by the data subject) the following scopes are prohibited:
```
AFFILIATION.MEMBERSHIP.UNION x * x *
DEMOGRAPHIC.ORIGIN x * x *
DEMOGRAPHIC.RACE x * x *
DEMOGRAPHIC.BELIEFS x * x *
DEMOGRAPHIC.SEXUAL-ORIENTATION x * x *
GENETIC x * x *
HEALTH x * x *
BIOMETRIC x * x *
```

Such data categories MAY be processed under `CONSENT` or `NECESSARY` legal bases under certain conditions.

#### Special Organizations

##### Not-for-profit

`LEGITIMATE-INTEREST` can make processing of this data lawful according to Article 9. (d) of GDPR in the special case of not-for-profit body with a political, philosophical, religious or trade union aim and on condition that the processing relates solely to the members or to former members of the body or to persons who have regular contact with it in connection. However the data can't be shared.

Such Organizations are still subject to the following prohibited scopes when using `LEGITIMATE-INTEREST`:

```
DEMOGRAPHIC.ORIGIN x SHARING x *
DEMOGRAPHIC.RACE x SHARING x *
DEMOGRAPHIC.BELIEFS x SHARING x *
DEMOGRAPHIC.SEXUAL-ORIENTATION x SHARING x *
GENETIC x SHARING x *
HEALTH x SHARING x *
BIOMETRIC x SHARING x *
```

The following scopes remain prohibited, even for those Organizations, under `CONTRACT`:
```
AFFILIATION.MEMBERSHIP.UNION x * x *
DEMOGRAPHIC.ORIGIN x * x *
DEMOGRAPHIC.RACE x * x *
DEMOGRAPHIC.BELIEFS x * x *
DEMOGRAPHIC.SEXUAL-ORIENTATION x * x *
GENETIC x * x *
HEALTH x * x *
BIOMETRIC x * x *
```

##### Health professional

`CONTRACT` can make processing of this data lawful according to Article 9. (d) of GDPR in the special case of a health professional subject to the obligation of professional secrecy under Union or Member State law or rules established by national competent bodies or by another person also subject to an obligation of secrecy under Union or Member State law or rules established by national competent bodies.

The following scopes remain prohibited, even for those Organizations, under `LEGITIMATE-INTEREST`:
```
AFFILIATION.MEMBERSHIP.UNION x * x *
DEMOGRAPHIC.ORIGIN x * x *
DEMOGRAPHIC.RACE x * x *
DEMOGRAPHIC.BELIEFS x * x *
DEMOGRAPHIC.SEXUAL-ORIENTATION x * x *
GENETIC x * x *
HEALTH x * x *
BIOMETRIC x * x *
```
