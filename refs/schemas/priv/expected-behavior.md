# Privacy Request Interchange Vocabulary : Expected Behavior of Implementing Systems

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [NNN](https://github.com/blindnet-io/PROJECT/pull/NNN) (update when you have PR #)     |
| **Author(s)** | milstan (milstan@blindnet.io)         |
| **Updated**   | 2022-05-25                                                                             |

## Introduction

This document specifies the expected behaviour of Systems implementing [Privacy Request Interchange Vocabulary](./RFC-PRIV.md). It defines actions that the systems SHOULD undertake with regards to particular Privacy Requests and particular situations.

It is a first step towards the specification of the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler), formerly known as Data Rights Compiler in the [High Level Architecture](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture).


## Motivation

**TBD**

## Terminology

>**TBD**

- We use the term Privacy Request interchangeably with the (deprecated) terms Rights Request and Data Rights Request as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use the terms Individual, Person, You, and Data Subject as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv)
- We use the term System as defined in [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/master/refs/high-level-conceptualization/README.md)
- We use MUST, MUST NOT and MAY, as defined in [IETF RFC2119](https://datatracker.ietf.org/doc/html/rfc2119)
- We use the terms Organization, Submitter, Data Consumer as defined in the [Lexicon](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/privateform-lexicon.csv) as defined there.


## Scope of automation

Privacy Requests can be resolved more or less automatically.
Privacy Requests that are expressed in unambiguous terms, may be fully processed automatically.
Those that include the term "OTHER" or a textual message with more details about the request likely require human intervention.

Systems MAY be configured to treat Privacy Requests eligible for automation with or without human validation. In any case, the role of the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) is to calculate the appropriate action, given particular Privacy Request in a particular situation.

## Configuration & Prerequisites

A [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) serving a particular system MUST have the knowledge of:
- The exhaustive list of [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) `selector`s that the System works with,
- For each `selector` (or Data Category implying every `selector` used within that Data Category) a data [Retention Policy](./RFC-PRIV.md#retention-policy),
- A set of Privacy Scope triples that describe the usage the System is likely to make with data. Each triple consists of:
    - a `selector` (or Data Category implying every `selector` used within that Data Category)
    - a Processing Category that the System is likely to perform on that data
    - a Purpose
- For each Privacy Scope triple, one or more [Legal Bases](./RFC-PRIV.md#legal-bases).

Legal Bases live a life of their own, regardless of the presence or absence of data, so Privacy Compilers MUST at all times, keep track of:
- All Legal Bases
- Active Legal Bases, which consist of:
    - active Consents, a list that is modified when Consent is collected and within [Operations over consents](#operations-over-consents),
    - other Legal Bases that have their validity conditions met at the given time

In addition, in order to resolve `TRANSPARENCY` requests, a Privacy Compiler MUST also know a set of parameters defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV).

## Privacy Algebra

### Set Operations over Privacy Scope

#### Operations over consents

The scope of Consents can be modified by Privacy Request that include `OBJECT`, `RESTRICT`, and `REVOKE-CONSENT` actions.

The System SHOULD, at all times, keep track of active Consents. We call a Consent active if its scope has not been modified or the Consent totally revoked. When the scope of a Consent is modified, a new Consent (that is now active) is made that replaces the old Consent (no longer active).

When the System has more then one active consent, the System considers the union of their scopes as being the Privacy Scope to which the Data Subject consents.

We illustrate this on the following example.

Let us imagine a System, processing data about a Data Subject, and having collected the following consent from the Data Subject:

```
{
  "consent-id": "6b3ad78c-2d4a-4575-8a9f-a69c2bfe0bd2",
  "date": "2022-06-01T14:40:39+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "scope": {
      "data-categories":["CONTACT"],
      "processing-categories": ["SHARING", "STORING"],
      "purposes":["PERSONALISATION", "MARKETING", "ADVERTISING"]
    }
}
```

Now this same Data Subject, makes a Privacy Request. In their request, they don't make a reference to the concrete `consent-id` but rather simply state that they no longer want their contact data processed in any way for marketing and advertising purposes.

```
{
  "request-id": "1a5c41f2-606f-4722-b852-4ba57cc9617c",
  "date": "2022-06-02T12:50:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "demands":[{
    "demand-id":"3173e329-ef64-4cb0-b87e-ba7d5d41fb8a",
    "action":"REVOKE-CONSENT",
    "restrictions":[{
      "data-categories":["CONTACT"],
      "purposes":["MARKETING", "ADVERTISING"]
    }]
  }],
}
```

The [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
- Generating a Privacy Request Response with the `GRANTED` Status,

```
{
  "response-id": "3b425097-3664-484c-95e1-015cbc126dff",
  "in-response-to": "3173e329-ef64-4cb0-b87e-ba7d5d41fb8a",
  "date": "2022-06-05T14:40:39+0000",
  "status": "GRANTED"
}
```

- Amending the consent to restrict its scope. For this purpose a new consent (that overrides the existing one) is produced:

```
{
  "consent-id": "4ec28dc8-8714-45a3-a710-c72cea6e6da4",
  "replaces": ["6b3ad78c-2d4a-4575-8a9f-a69c2bfe0bd2"],
  "date": "2022-06-05T14:40:39+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "scope": {
      "data-categories":["CONTACT"],
      "processing-categories": ["SHARING", "STORING"],
      "purposes":["PERSONALISATION"]
    }
}
```
- Keep track of the changes to the original consent by adding metadata about change to it:

```
{
  "consent-id": "6b3ad78c-2d4a-4575-8a9f-a69c2bfe0bd2",
  "replaced-by": ["4ec28dc8-8714-45a3-a710-c72cea6e6da4"],
}
```
- Consider active the new consent: `4ec28dc8-8714-45a3-a710-c72cea6e6da4`

The System MAY continue to use the Data Subjects' data for personalising their experience but no longer has consent to use the data for marketing and advertising.

Let us now imagine the Data Subject making another Privacy Request, this time to object to any sharing of their e-mail address. For this, the following Privacy Request is made:

```
{
  "request-id": "fe54a89f-99f8-4a8c-bc14-830bfd99d651",
  "date": "2022-06-07T16:20:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "demands":[{
    "demand-id":"64fec4cc-e879-4624-a3d7-df0c170fc862",
    "action":"OBJECT",
    "restrictions":[{
      "data-categories":["CONTACT.EMAIL"],
      "processing-categories": ["SHARING"],
    }]
  }],
}
```
At the time of receiving this request, the System has consent for `STORING` and `SHARING` all `CONTACT` data for `PERSONALISATION` purposes.
When the System gets this request, the scope of the consent MUST change. The remaining scope of the consent will only include:
- `SHARING` of all `CONTACT` data other then `CONTACT.EMAIL`, for `PERSONALISATION` purposes, and
- `STORING` of all `CONTACT` for `PERSONALISATION` purposes

The [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
- Generating a Privacy Request Response with the `GRANTED` Status,

```
{
  "response-id": "12f77337-0e06-4619-bfb7-8759a6c5e95a",
  "in-response-to": "64fec4cc-e879-4624-a3d7-df0c170fc862",
  "date": "2022-06-15T11:30:00+0000",
  "status": "GRANTED"
}
```

- Amending the consent to restrict its scope. For this purpose two new consents (that override the existing one) are produced:

```
{
  "consent-id": "6c8211c7-c152-4ef4-b264-098ee6533f75",
  "replaces": ["4ec28dc8-8714-45a3-a710-c72cea6e6da4"],
  "date": "2022-06-15T11:30:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "scope": {
      "data-categories":["CONTACT"],
      "processing-categories": ["STORING"],
      "purposes":["PERSONALISATION"]
    }
}

{
  "consent-id": "1f899305-235e-4fd4-b3c4-ff92dd67d769",
  "replaces": ["4ec28dc8-8714-45a3-a710-c72cea6e6da4"],
  "date": "2022-06-15T11:30:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "scope": {
      "data-categories":["CONTACT.ADDRESS", "CONTACT.PHONE"],
      "processing-categories": ["SHARING"],
      "purposes":["PERSONALISATION"]
    }
}
```
- Keep track of the changes to the amended consent by adding metadata about changes made to it:

```
{
  "consent-id": "4ec28dc8-8714-45a3-a710-c72cea6e6da4",
  "replaced-by": ["6c8211c7-c152-4ef4-b264-098ee6533f75","1f899305-235e-4fd4-b3c4-ff92dd67d769"],
}
```
- Consider active the new consents: `6c8211c7-c152-4ef4-b264-098ee6533f75`,`1f899305-235e-4fd4-b3c4-ff92dd67d769`

> **Note**
>
> When making derived consents, limited to certain data categories the Privacy Compiler MUST take into account the complete list of [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) `selector`s that the Systems works with.

Let us now imagine the Data Subject making another Privacy Request, this time to restrict data processing only to storing of their data. For this, the following Privacy Request is made:

```
{
  "request-id": "e848d0e0-41ab-492c-ae90-ca891b70abc1",
  "date": "2022-06-17T15:10:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "demands":[{
    "demand-id":"f3fb39df-9f25-44c9-8aaa-5ddac3833e6a",
    "action":"RESTRICT",
    "restrictions":[{
      "processing-categories": ["STORING"],
    }]
  }],
}
```

At the time of receiving this request, the System has consent for `STORING` of all `CONTACT` for `PERSONALISATION` purposes, and for `SHARING` of all `CONTACT` data other then `CONTACT.EMAIL`, for `PERSONALISATION` purposes.

Afther processing the `RESTRICT` request, only the consent for `STORING` of all `CONTACT` for `PERSONALISATION` purposes remains valid.

The [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
- Generating a Privacy Request Response with the `GRANTED` Status,

```
{
  "response-id": "82d27b4d-44f5-484c-9656-2e41fc2d9bf3",
  "in-response-to": "f3fb39df-9f25-44c9-8aaa-5ddac3833e6a",
  "date": "2022-06-18T14:30:00+0000",
  "status": "GRANTED"
}
```
- Consider active the only the consent: `6c8211c7-c152-4ef4-b264-098ee6533f75`

Finally, let us imagine the user now want to revoke the initial consent that they gave in the very beginning.
The system receives the following Privacy Request:

```
{
  "request-id": "e4585ec4-f566-45cd-9495-af622ff5e6fb",
  "date": "2022-06-17T15:10:00+0000",
  "data-subject":[{
    "dsid-schema": "email-sha-256",
    "dsid":"7cac89a56bbf998c996f33e0b2d3bad578e05f3af8d64793c0bcac46b8c260dc"
  }],
  "demands":[{
    "demand-id":"90303838-f134-4387-a59c-032b7b993ee6",
    "action":"REVOKE-CONSENT",
    "restrictions":[{
      "consent-id": "6b3ad78c-2d4a-4575-8a9f-a69c2bfe0bd2",
    }]
  }],
}
```
The System MUST no longer consider this Consent (nor any other consent derived from it) active. The list of active consents MUST now become empty, because the only active consent `6c8211c7-c152-4ef4-b264-098ee6533f75` is derived from `4ec28dc8-8714-45a3-a710-c72cea6e6da4` which is derived from
`6b3ad78c-2d4a-4575-8a9f-a69c2bfe0bd2` that the user now revokes.

The System SHOULD be able to deliver a timeline of Consents, Requests and Responses, that may serve as a proof of compliance and good faith.

> **Note**
>
> When Consent is used as one of legal bases for processing, it is not enough to only keep track of `RESTRICT` and `OBJECT` Privacy Requests to limit the eligible scope of data processing, but it is necessary to modify the Consents. This is due to the fact that Consents are not the only legal bases for data processing (i.e. Systems may have right to process data without consent). Different legal bases may evolve (be acquired and lost) independently.
>
>In other words, a `RESTRICT` Privacy Request may affect the scope of consent, but have no impact on actual processing being done. Another legal base for processing MAY make processing possible despite the `RESTRICT` request, yet the consent would still need to be amended in response to the `RESTRICT` Privacy Request.


## Alternatives Considered

**TBD**


## Questions and Discussion Topics

**TBD**


## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.

### Informative References

-

### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- [CPRA]([https://eur-lex.europa.eu/eli/reg/2016/679/oj](https://vig.cdn.sos.ca.gov/2020/general/pdf/topl-prop24.pdf))
- [HIPPA]([https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5](https://www.govinfo.gov/content/pkg/PLAW-104publ191/pdf/PLAW-104publ191.pdf))
