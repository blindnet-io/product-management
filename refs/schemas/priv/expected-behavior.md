# Privacy Request Interchange Vocabulary : Expected Behavior of Implementing Systems

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io)         |
| **Updated**   | 2022-06-07                                                                             |

## Introduction

This document specifies the expected behaviour of Systems implementing [Privacy Request Interchange Vocabulary](./RFC-PRIV.md). It defines actions that the systems MAY undertake with regards to particular Privacy Requests and particular situations.

It is a first step towards the specification of the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler), formerly known as Data Rights Compiler in the [High Level Architecture](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture).


## Motivation

While this document is a first step in the definition of the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler), it is not intended to be its formal specification nor to influence the design choices related to formalisation of rules and configurations.

The purpose of the document is primarily illustrate a possible behaviour Systems (And their Privacy Compilers) MAY implement in response to Privacy Requests, in order to test the completeness of the [Privacy Request Interchange Vocabulary](./RFC-PRIV.md).

## Terminology


- We use all the terms of the  [Privacy Request Interchange Vocabulary](./RFC-PRIV.md) as defined there
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
- **Intended Privacy Scope**: A set of **Privacy Scope Triple**s that describe the usage the System is likely to make with data. Each triple consists of:
    - a `selector` (or Data Category implying every `selector` used within that Data Category)
    - a Processing Category that the System is likely to perform on that data
    - a Purpose
- For each Privacy Scope triple, one or more [Legal Bases](./RFC-PRIV.md#legal-bases).


Legal Bases live a life of their own, regardless of the presence or absence of data, so Privacy Compilers MUST at all times, keep track of:
- All Legal Bases
- Active Legal Bases, which consist of:
    - active Consents, a list that is modified when Consent is collected and within [Operations over consents](#operations-over-consents),
    - other Legal Bases that have their validity conditions met at the given time.
        - For `CONTRACT` - Contracts/Services being provided, they constitute an active Legal base for as long as the user has not closed the account/ended commercial relationship `RELATIONSHIP-END`
        - When `LEGITIMATE-INTEREST` is used, it is active from the moment of data collection and for as long as the Data Subject has not made a `DELETE`, `OBJECT`, or `RESTRICT` Privacy Request

To keep track of active Legal Bases (but also in order to apply [Retention Policies](./RFC-PRIV.md#retention-policy) the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) MUST be able to register events related to the relationship with the data subject and save, for each Data Subject identity:
- One or more relationship IDs (e.g., this may be an ID of a user account on an e-commerce website, or an ID of a particular contract like a legal file for a lawfirm.), each having an activity status indicating if the relationship is ongoing or has been ended.

The Privacy Compiler MUST also keep track of every Privacy Request made to the System.

In addition, in order to resolve `TRANSPARENCY` requests, a Privacy Compiler MUST also know a set of parameters defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV).

## Privacy Algebra

For each Data Capture Fragment, at all times, the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) maintains an **Eligible Privacy Scope**.

For each Data Capture Fragment `selector`, the Privacy Compiler knows the **Intended Privacy Scope**.
At the same time the Privacy Compiler knows about a set of Privacy Scope triples that are associated with an active Legal Base.

The **Eligible Privacy Scope**, is a set of Privacy Scope triples, that is the INTERSECTION of:
- set of Privacy Scope triples in the **Intended Privacy Scope**,
- AND the set of Privacy Scope triples for which at least one of the following statements is true:
    - They are associated with `CONSENT` legal base, and there is an active Consent such that the Privacy Scope triple is contained in the Privacy Scope of that Consent
    - They are associated with `CONTRACT` legal base, and there is an active relationship with the Data Subject in question for which no `RELATIONSHIP-END` event has been registered
    - They are associated with `LEGITIMATE-INTEREST` legal base, and
        - IF the Data Subject made any `OBJECT` Demand, they are not part of Privacy Scope of any such Demand
        - IF the Data Subject made any `RESTRICT` Demand, they are a part of the intersection of Privacy Scopes of all such Demands
    - They are associated with `NECESSARY` legal base

The Privacy Compilers can be configured to evaluate Eligible Privacy Scopes in the context of particular regulations.
In this case, Privacy Compilers maintain a list of Privacy Scope triples prohibited by that regulation and they exclude them from the Eligible Privacy Scope.
E.g. under GDPR, it is prohibited to process gender and genetic data under any Legal Base other than Consent.

For convenience, Privacy Compilers MAY also keep track of a set of **Prohibited (Privacy Scope)-(Legal Base) Pairs**, in which they SHOULD include Privacy Scope triples made illegal by the legislation that they want to support. It might also be convenient, when Data Subject's `OBJECT` or `RESTRICT` Demands are granted over a particular Privacy Scope, to list that scope under `LEGITIMATE-INTEREST` in the **Prohibited (Privacy Scope)-(Legal Base) Pairs** for making sure not to re-include them in the **Eligible Privacy Scope** unless the user gives explicit consent, signs a contract or becomes subject to mandatory data keeping.

> E.g. under GDPR, as processing of RACE data is only allowed under 'CONSENT' for medical research purposes, examples of **Prohibited (Privacy Scope)-(Legal Base) Pairs** include
>
> (`data-category`=`DEMOGRAPHIC.RACE`, `purpose`=`ADVERTISING`) - CONSENT
>
> (`data-category`=`DEMOGRAPHIC.RACE`) - CONTRACT
>
> (`data-category`=`DEMOGRAPHIC.RACE`) - LEGITIMATE-INTEREST

The **Eligible Privacy Scope** is recalculated with every Data Capture, or whenever a Privacy Request Demand (other than `ACCESS` and `TRANSPARENCY`) is granted.

Yet, the **Eligible Privacy Scope** is independent to Retention Policy. A particular Data Capture Fragment MAY be associated with a non-empty Eligible Privacy Scope yet [be evaluated as expired under its Retention Policy](#resolving-retention-policies) and as such may need to be deleted anyway.

### Set Operations over Privacy Scope

#### <a name="updateConsent"></a>Operations over consents

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

### <a name="updateScope"></a>Updating the Eligible Privacy Scope upon `OBJECT` and `RESTRICT` Privacy Request Demands

Gained and lost consent modify the Eligible Privacy Scope.
Also, as [we have seen](#updateConsent), `OBJECT` and `RESTRICT` Privacy Request Demands SHOULD affect the scope of existing consents.
In addition, when such Demands are received, the Eligible Privacy Scope SHOULD be recalculated.

However, it is important to note that the `OBJECT` and `RESTRICT` Privacy Request Demands behave in very specific ways. Concretely:
- They don't affect Privacy Scope Triples that are included in the Eligible Privacy Scope under `CONTRACT` or `NECESSARY` legal bases,

- with regards to Consents, they affect only existing Consents, not the future ones.
    - Let us imagine for example that the Data Subject gave consent for processing of their data for any purpose.
    - Then later, the Data Subject makes an `OBJECT` Demand related to `SALE` purposes.
    At this point all Privacy Scope Triples having `SALE` as purpose exit the Eligible Privacy Scope.
    - This same Data Subject MAY again give consent for processing of their data for any purpose in which case the Privacy Scope Triples having `SALE` as purpose re-enter the Eligible Privacy Scope.

- with regards to Privacy Scope Triples that are integrated in the Eligible Privacy Scope under `LEGITIMATE-INTEREST`, once `OBJECT` or `RESTRICT` Demands are made, they affect present and future Eligible Privacy Scope. In other words, the Privacy Scope Triples that have exited the Eligible Privacy Scope due to `OBJECT` or `RESTRICT` Demands, can't re-enter Eligible Privacy Scope under `LEGITIMATE-INTEREST`. When several `OBJECT` or `RESTRICT` Demands are made over time, a particular Privacy Scope Triple that entered the Eligible Privacy Scope under `LEGITIMATE-INTEREST`, can remain in the Eligible Privacy Scope if and only if:
    - It is not a part of union of Privacy Scopes of all `OBJECT` Demands, AND if
    - It is a part of the intersection of Privacy Scopes of all `RESTRICT` Demands

Let us take an example to illustrate updating of Eligible Privacy Scope. At the beginning the System holds the Data Subjects e-mail address for prospecting purposes, under `LEGITIMATE-INTEREST` Legal Base.
```
Eligible Privacy Scope:
CONTACT.EMAIL x ALL x MARKETING (LEGITIMATE-INTEREST)
```

The Data Subject, after receiving a marketing e-mail, decides to open an account and start using the service. They provide their postal address for billing. While creating an account, they also give consent for their postal address to be used for advertising purposes.

```
Eligible Privacy Scope:
CONTACT.EMAIL x ALL x MARKETING (LEGITIMATE-INTEREST)
CONTACT.EMAIL x ALL x SERVICES (CONTRACT)
CONTACT.ADDRESS x ALL x SERVICES (CONTRACT)
CONTACT.ADDRESS x ALL x ADVERTISING (CONSENT)
```

The Data Subject realises that they are receiving too much advertising material and they formulate a Privacy Request with one `REVOKE-CONSENT` demand targeting particular consent that they gave.

```
Eligible Privacy Scope:
CONTACT.EMAIL x ALL x MARKETING (LEGITIMATE-INTEREST)
CONTACT.EMAIL x ALL x SERVICES (CONTRACT)
CONTACT.ADDRESS x ALL x SERVICES (CONTRACT)
```

The Data Subject realises that they are still receiving maketing e-mail and they formulate a Privacy Request with one `OBJECT` demand with `CONTACT.EMAIL` being defined as its Privacy Scope. Yet, this Demand only affects the Privacy Scope Triples held under `LEGITIMATE-INTEREST`. The System can still, continue to keep the `CONTACT.EMAIL` and `CONTACT.ADDRESS` for the same of the ongoing contractual relationship with the user.

```
Eligible Privacy Scope:
CONTACT.EMAIL x ALL x SERVICES (CONTRACT)
CONTACT.ADDRESS x ALL x SERVICES (CONTRACT)
```
However, the remaining purpose (`SERVICES`) now only allows the System to send e-mail related to the services being provided, and no longer supports sending marketing e-mail to this Data Subject.

### Calculating Permissions

Since the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) maintains the Eligible Privacy Scope at any time, it can (given a Data Capture ID, or a Data Capture Fragment ID) answer whether at that time, a particular data processing operation is permitted.

For example, the System can inquire whether a particular data fragment, corresponding to `CONTACT.EMAIL` data category, can be used to invoice the user (processing = `USING`; purpose = `SERVICES`), or whether it can be shared with some other partner system for user profiling (processing = `SHARING`; purpose = `AUTOMATED-INFERENCE`).


## Resolving requests

The [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) evaluates Privacy Request Demands and issues recommendations to the System. The Systems can then be configured to respond to Privacy Requests automatically, blindly following those recommendations (whenever possible), or to await human input just in case.

Here is how the Privacy Request Response recommendations are calculated:

When no Data Subject ID is provided in the Privacy Request:
- `TRANSPARENCY` Demands: recommend status = `GRANTED`. Provide requested information: Data Categories, Processing Categories, Purposes, and Legal Bases from Intended Privacy Scope, as well as other ifnromation from general settings as defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV).
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- For any other action : recommend status = `DENIED`, motive=`IDENTITY-UNCONFIRMED`

When Data Subject ID is provided, Data Subject is authenticated but is unknown by the System:
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- For any other action : recommend status = `DENIED`, motive=`USER-UNKNOWN`

When Data Subject ID is provided, the Data Subject is known by the System but filed to authenticate:
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- `TRANSPARENCY.KNOWN` Demands: recommend status = `GRANTED`, and data = `NO`.
- For any other action : recommend status = `DENIED`, motive=`IDENTITY-UNCONFIRMED`

When Data Subject ID is provided, the Data Subject is known by the System and authenticated:
- Regardless of restrictions
    - `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
    - `TRANSPARENCY.KNOWN` Demands: recommend status = `GRANTED`, and data = `YES`.
    - `TRANSPARENCY.DATA-CATEGORIES` Demands: recommend status = `GRANTED`, and data = list of Data Categories that are included in any of the Privacy Scope Triples included in the Eligible Privacy Scope.
    - `TRANSPARENCY.ORGANISATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.DPO`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO` Demands: recommend status = `GRANTED`, and data = information corresponding to the request taken from configuration settings as defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV).

- With regards to Demand restrictions (if any) limiting the scope of the Demand
    - `TRANSPARENCY.LEGAL-BASES` Demands: recommend status = `GRANTED`, and data = list of Legal Bases under which any of the Privacy Scope Triples are included in the Eligible Privacy Scope (or its intersection with the Privacy Scope of the Demand if restricted).
    - `TRANSPARENCY.PROCESSING-CATEGORIES` Demands: recommend status = `GRANTED`, and data = list of Processing Categories that are included in any of the Privacy Scope Triples included in the Eligible Privacy Scope (or its intersection with the Privacy Scope of the Demand if restricted).
    - `TRANSPARENCY.PURPOSE` Demands: recommend status = `GRANTED`, and data = list of Purposes that are included in any of the Privacy Scope Triples included in the Eligible Privacy Scope (or its intersection with the Privacy Scope of the Demand if restricted).
    - `REVOKE-CONSENT` Demands:
        - If restricted to concrete consent IDs, recommend status = `GRANTED` and recalculate Eligible Privacy Scope to drop any Privacy Scope Triples that have been included as a result of Consents being revoked.
        - If Demand is restricted by a Privacy Scope, recommend status = `GRANTED` and [update consents](#updateConsent)
        - If no Restriction is given in the Demand, revoke all consents given by this Data Subject
        - If only a Data Range restriction is present, recommend status = `GRANTED` and revoke all consents that have been collected in the given Data Range
        - If only a Data Capture Restriction is present, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED`
        - If several restrictions of the same type are present, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED`
        - If more restrictions (other than Data Capture Restriction) are present, interpret them as an intersection i.e. take only the consents collected within the from-to dates of the Data Range Restriction, then do an intersection of their Privacy Scopes with the scope of the Privacy Scope restriction. The resulting Privacy Scope can be used as if there were only one Privacy Scope demand. Recommend status = `GRANTED` and [update consents](#updateConsent)
    - `OBJECT`, `RESTRICT` Demands:
        - Recommend status = `GRANTED`, and then, upon granting [update consents](#updateConsent), [recalculate Eligible Privacy Scope](#updateScope)
        - Recommend deletion of Data Capture Fragments the categories of which are not longer included in the Eligible Privacy Scope.
    - `DELETE` Demands:
        - If restricted to concrete consent IDs, , recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED`
        - If restricted to a privacy scope having a `processing-category` or a `purpose`, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED` (A Delete request can only be relative to a category of data, not to a category of processing or a particular purpose.)
        - If restricted to a clearly identifiable data scope (such a Privacy Scope with a `processing-category`, or a concrete Data Capture Fragment `selector`, or to a Data Capture Fragment ID (or set of IDs), potentially limited to a Data Range):
            - if data corresponding to that scope does not exist, recommend status = `DENIED`, motive = `NO-SUCH-DATA`
            - if data corresponding to that scope does exist, AND:
                - the data is associated with Privacy Scope Triples that are introduced in the Eligible Privacy Scope under at least one Legal Base other than {`LEGITIMATE-INTEREST`, `CONSENT`}, recommend status = `ACCEPT`
                - the data is associated with Privacy Scope Triples that are introduced in the Eligible Privacy Scope under Legal Bases all of which belong to {`LEGITIMATE-INTEREST`, `CONSENT`}, recommend status = `DENIED`, and one or more motive = `LEGAL-BASES` when data is included in the Eligible Privacy Scope under `CONTRACT`, and `LEGAL-OBLIGATIONS` when data is included in the Eligible Privacy Scope under `NECESSARY`

    - `MODIFY` Demands:
        - If restricted to concrete consent IDs, , recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED`
        - If restricted to a privacy scope having a `processing-category` or a `purpose`, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED` (A Delete request can only be relative to a category of data, not to a category of processing or a particular purpose.)
        - If restricted to a clearly identifiable data scope (such a Privacy Scope with a `processing-category`, or a concrete Data Capture Fragment `selector`, or to a Data Capture Fragment ID (or set of IDs), potentially limited to a Data Range):
            - if data corresponding to that scope is not being collected by the System as is not part of the Intended Privacy Scope, status = `DENIED`, motive = `NO-SUCH-DATA`
            - if data corresponding to that scope is not being collected by the System (regardless of data being already collected or empty):
                - Recommend status = `ACCEPT` (potentially upon human validation)

    - `ACCESS` Demands:
        - Recommend status = `ACCEPT`, and data = data corresponding to the Privacy Scope of the Demand (NB. contrary to MODIFY and DELETE, the Data Subject SHOULD be able to request access to data being used for particular `purpose` or being subject to particular `processing-category`)

    - `PORTABILITY` Demands:
        - Recommend status = `ACCEPT`, and data = data corresponding to the Privacy Scope of the Demand


## Resolving Retention Policies

[Privacy Compilers](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-architecture#data-rights-compiler) SHOULD store and resolve Retention Policies.

| Property | Expected cardinality | Expected values |
| --------------- | ------ | -------------------- |
| `data-category` | 1-* | Any of the any Data Category terms or concrete Data Capture Fragment `selector`s within those categories |
| `policy-type` | 1 | one of {NO-LONGER-THAN, "NO-LESS-THAN"} |
| `duration` | 1 | Duration in JSON Schema [duration](https://json-schema.org/draft/2020-12/json-schema-validation.html#rfc.section.7.3.1) format |
| `after` | 1 | Event to which the retention duration is relative to. One of {`DATA-COLLECTION`,`RELATIONSHIP-END`}

When several `data-category` values are given, they are interpreted as a union.

Systems SHOULD define Retention Policies at the time of configuration, and SHOULD cover all Data Categories and Data Capture Fragment `selector`s from the Intended Privacy Scope with at least one Retention Policy.

Retention Policies are resolved upon concrete instances of data. A particular instance of data, given the Data Capture Fragment `selector` to which it corresponds, is considered `EXPIRED` if all of the following is true:
- There is a Retention Policy the `data-category` of which is a Privacy Scope that includes Data Capture Fragment `selector` of the particular data, that is of type `NO-LONGER-THAN`, such that the date of the event defined under `after` has passed for a more then the time defined under `duration`
- AND There is no Retention Policy the `data-category` of which is a Privacy Scope that includes Data Capture Fragment `selector` of the particular data, that is of type `NO-LESS-THAN`, such that the event defined under `after` is yet to happen or has happened before a period of time inferior to `duration`

Privacy Compilers SHOULD be able to:
- provide lists of active policies, in the context of answering to the `TRANSPARENCY.RETENTION` requests
- resolve policies and generate `EXPIRED` alerts, upon which the Systems MAY chose to implement automatic data deletion, or other protocols for data archiving or similar
- resolve policies for Systems configured not to automatically delete data, but to automatically grant `DELETE` requests only when data is `EXPIRED`

Optionally, for systems wanting to automatically deni `DELETE` requests when data MUST be kept, Privacy Compilers MAY be able deliver resolve policies giving `HOLD` status, when there is at least one Retention Policy the `data-category` of which is a Privacy Scope that includes Data Capture Fragment `selector` of the particular data, that is of type `NO-LESS-THAN`, such that the event defined under `after` is yet to happen or has happened before a period of time inferior to `duration`.

## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- CPRA
- HIPPA
