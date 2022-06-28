# Privacy Request Interchange Vocabulary : Expected Behavior of Implementing Systems

| Status        | NA / supporting document                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **Author(s)** | milstan (milstan@blindnet.io)         |
| **Updated**   | 2022-06-14                                                                             |

## Introduction

This document specifies the expected behavior of Systems implementing [Privacy Request Interchange Vocabulary](./RFC-PRIV.md). It defines actions that the systems MAY undertake with regards to particular Privacy Requests and particular situations.

It is a first step towards the specification of the [Privacy Compiler](../../high-level-architecture#data-rights-compiler), formerly known as Data Rights Compiler in the [High Level Architecture](../../high-level-architecture).


## Motivation

While this document is a first step in the definition of the [Privacy Compiler](../../high-level-architecture#data-rights-compiler), it is not intended to be its formal specification nor to influence the design choices related to formalization of rules and configurations.

The purpose of the document is primarily illustrate a possible behavior Systems (And their Privacy Compilers) MAY implement in response to Privacy Requests, in order to test the completeness of the [Privacy Request Interchange Vocabulary](./RFC-PRIV.md).

## Terminology

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119)
- The key word "CAN" denotes ability of someone or something, and is interpreted as "MUST be able to"
- The key words "blindnet devkit", "CCPA", "CPRA", "Capture Fragment", "Component", "Data Capture", "Data Capture Fragment", "Data Consumer", "Data Subject", "DPO", "Fragment", "GDPR", "HIPPA", "Internet User", "Organization", "Privateform", "Privacy Request", "System", "Submitter", "User" are to be interpreted as described in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md)
- Any additional precision about the key words defined in [RFC-Lexicon-2](../lexicon/RFC-Lexicon-2.md), as well as additional key words such as "Consent" and "Legal Base", provided in [High Level Conceptualization](../high-level-conceptualization/) is to be considered normative
- All key words denoting components of [blindnet devkit](../lexicon/RFC-Lexicon-2.md#blindnet-devkit), such as "Capture Component", "Encryption and Access Management Engine", "Privacy Computation Engine", "Privacy Compiler", "Privacy Request Capture Interface", "Customization API", "Data Consumer Interface", "Schemas" and "Storage Component" are to be interpreted as defined in [High Level Architecture](../high-level-conceptualization/)
- Privacy Compiler was formerly known as Data Rights Compiler
- Privacy Request was formerly known as Data Rights Request
- All the concepts, properties and [Terms](./RFC-PRIV.md#terms) listed in the [Proposal](./RFC-PRIV.md#proposal) section of PRIV(Privacy Request Interchange Vocabulary are to be interpreted as defined in [Privacy Request Interchange Vocabulary](./RFC-PRIV.md#proposal)

## Scope of automation

Privacy Requests can be resolved more or less automatically.
Privacy Requests that are expressed in unambiguous [Terms](./RFC-PRIV.md#terms), may be fully processed automatically.
Those that include any [Terms](./RFC-PRIV.md#terms) containing the string "OTHER" or a textual message with more details about the request likely require human intervention.
Cf. [different automation scenarios](./scenarios.md#automation)

Systems MAY be configured to treat Privacy Requests eligible for automation with or without human validation. In any case, the role of the [Privacy Compiler](../high-level-architecture#data-rights-compiler) is to calculate the appropriate action, given particular Privacy Request in a particular situation.

Systems CAN also direct certain requests (such as `MODIFY`) to dedicated interfaces that they may already have for Data Subjects to provide and modify their data.

Because of this Systems MUST be able to configure their particular ways of automating the processing of Privacy Requests.

## Configuration and Prerequisites

A [Privacy Compiler](../high-level-architecture#data-rights-compiler) serving a particular System MUST have the knowledge of the following key parameters and data structures:

- **Parameters**: a set of parameters defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV) needed to resolve `TRANSPARENCY` requests. Those MAY be received using UROPA format (see [UROPA section of PRIV](./RFC-PRIV.md#uropa)).

- **Known Selectors** : exhaustive list of [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) `selector` know by the System, including for every data field that the System is likely to store (either a field of a data collection form, or simply a field in its database) the [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) `selector` corresponding to it

- **Configuration Maps**, defined at configuration time:
    - *Retention Policies*: For each **Known Selector** (or Data Category implying every `selector` used within that Data Category) a data [Retention Policy](./RFC-PRIV.md#retention-policy),

    - *Provenance*: For every **Known Selector** keep track of one or more [Provenance](./RFC-PRIV.md#provenance) objects.

    - **Intended Privacy Scope** : A set of **[Privacy Scope Triples](#privacy-scope-triples)** that describe the usage the System is likely to make with data.

    Each **Known Selector** MUST be included in the The Intended Privacy Scope.

    > **Note**
    >
    > In addition to `selectors` that are a native mechanism for extending Data Categories with System-specific subcategories, it is necessary to allow Systems to also extend Processing Categories and Purposes, with potentially System-specific terms following PRIV's [Term Dot Notation](./RFC-PRIV.md#term-dot-notation).
    >
    > This is necessary for interoperability with the specific Processing Categories of the [HL7 Standards](./RFC-PRIV.md#hl7-standards)
    >

    - *Legal Bases*: For each [Privacy Scope Triple](#privacy-scope-triples) from the **Intended Privacy Scope**, one or more [Legal Bases](./RFC-PRIV.md#legal-bases)

    - *Corresponding Systems*: A map of Other Systems with which data is being exchanged. For each System The Privacy Compiler MUST know if they are an `ORGANIZATION` or `PARTNERS` System, and have a way to uniquely identify and address them (see [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV), [Working with Provenance](#working-with-provenance))

- **Privacy Metadata Store**, updated at runtime:
   - *All Captures*: a list of all the [Data Capture](./RFC-PRIV.md#data-capture) objects that the Privacy Compiler is aware of.


   > Data Captures are not only generated on user input, but may result from user tracking, or from data transfers.
   > All such Data Captures objects are of interest to the Privacy Compiler.

   - *All Requests*: a list of all the [Privacy Request](./RFC-PRIV.md#privacy-request) objects that the Privacy Compiler is aware of
   - *All Responses*: a list of all the [Privacy Request Response](./RFC-PRIV.md#privacy-request-response) objects that the Privacy Compiler is aware of
   - Legal Bases:
       - *All Consents*: a list of all the [Consent](./RFC-PRIV.md#consent) objects that the Privacy Compiler is aware of
       - *All Contracts*: establishing a correspondence between a Data Subject and a `contract-id` being an identifier of a particular relationship that the Data Subject has with the system (e.g. a user account open with the system, employment contract, a court case treated by a lawfirm, etc.) with a `start` date and (optionally, if ended) a `end` date.
       - *All Legitimate Interests*: establishing a correspondence between a Data Subject and each [Privacy Scope Triples](#privacy-scope-triples) included in the **Intended Privacy Scope** under `LEGITIMATE-INTEREST`
       - *Necessary*: establishing a correspondence between a Data Subject and each [Privacy Scope Triple](#privacy-scope-triples) included in the **Intended Privacy Scope** under `NECESSARY` Legal Base

- **Runtime Maps**, updated at runtime:
    - Active Legal Bases:
        - *Active Consents*: a list of `consent-id`s that is modified when Consent is collected and within [Operations over consents](#operations-over-consents)
        - *Active Contracts*: a list of `contract-id`s of all active contracts that have not been subject to a `RELATIONSHIP-END` event
        - *Active Legitimate Interests*: a subset of *All Legitimate Interests*
    - Events, for [Resolving Retention Policies](#resolving-retention-policies):
        - `SERVICE-END` events for contracts that end (e.g. user closes the account, or stops a service agreement), that directly impact *Active Contracts* the [Privacy Scope Triples](#privacy-scope-triples) of which have not been in the scope of any `DELETE`, `OBJECT`, or `RESTRICT` Privacy Request by the data Subject concerned
        - `RELATIONSHIP-END` events the Data Subject ended all contracts and ended the relationship with the System/Organization
        - `CAPTURE-DATE` when a Data Capture is made or updated
    - Transfers:
        - All the data exchanges with other Systems, as described in [Remembering Transfers](./RFC-PRIV.md#remembering-transfers).
    - Privacy Scope:
        - For each Data Subject, an **Eligible Privacy Scope**, according to [Privacy Algebra](#privacy-algebra).
        This **Eligible Privacy Scope** is easily resolved at the level of each [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) (or its `selector`)

## Privacy Scope Triples

A **<a name="triple"></a>Privacy Scope Triple** is a unit of [Privacy Scope](RFC-PRIV.md#privacy-scope)
and it consists of (in that order):
    - one [Data Category Term](./RFC-PRIV.md#data-categories) or `*`
    - one [Processing Category Term](./RFC-PRIV.md#processing-categories) or `*`
    - one [Purpose Term](./RFC-PRIV.md#purpose) or `*`

When `*` is indicated at one of the places of the triple, it is interpreted as all [Data Categores](./RFC-PRIV.md#data-categories), all [Processing Categories](./RFC-PRIV.md#processing-categories) or all [Purposes](./RFC-PRIV.md#purpose) depending on its place in the triple.

Each [Privacy Scope Triple](#privacy-scope-triples) that includes a `*` or a [Term](./RFC-PRIV.md#terms) of which subcategory terms are known (including [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) `selectors` for [Data Category Terms](./RFC-PRIV.md#data-categories)) is equivalent to the set of Privacy Scope Triples including all combinations of such known subcategories (or all categories in case of `*`).

E.g. `FINANCIAL` x `SHARING` x `SERVICES` is equivalent to the following set:

`FINANCIAL` x `SHARING` x `SERVICES`
`FINANCIAL` x `SHARING` x `SERVICES.ADDITIONAL-SERVICES`
`FINANCIAL` x `SHARING` x `SERVICES.BASIC-SERVICE`
`FINANCIAL.BANK-ACCOUNT` x `SHARING` x `SERVICES`
`FINANCIAL.BANK-ACCOUNT` x `SHARING` x `SERVICES.ADDITIONAL-SERVICES`
`FINANCIAL.BANK-ACCOUNT` x `SHARING` x `SERVICES.BASIC-SERVICE`

If the System also knows of a `selector` `FINANCIAL.BANK-ACCOUNT.PRIMARY`, then the equivalent set also includes:

`FINANCIAL.BANK-ACCOUNT.PRIMARY` x `SHARING` x `SERVICES`
`FINANCIAL.BANK-ACCOUNT.PRIMARY` x `SHARING` x `SERVICES.ADDITIONAL-SERVICES`
`FINANCIAL.BANK-ACCOUNT.PRIMARY` x `SHARING` x `SERVICES.BASIC-SERVICE`

Systems MUST apply any operation concerning a Privacy Scope Triple to all of the Privacy Scope Triples equivalent to it.


## Privacy Algebra

For each Data Subject, at all times, the [Privacy Compiler](../high-level-architecture#data-rights-compiler) maintains an **Eligible Privacy Scope**.

For each Data Capture Fragment `selector`, the Privacy Compiler knows the **Intended Privacy Scope**.
At the same time the Privacy Compiler knows about a set of [Privacy Scope Triples](#privacy-scope-triples) that are associated with an active Legal Base (in the **Runtime Maps**)

The **Eligible Privacy Scope**, is a set of [Privacy Scope Triples](#privacy-scope-triples), that is the INTERSECTION of:
- set of [Privacy Scope Triples](#privacy-scope-triples) in the **Intended Privacy Scope**,
- AND the set of [Privacy Scope Triples](#privacy-scope-triples) for which at least one of the following statements is true:
    - They are associated with `CONSENT` legal base, and there is an active Consent such that the [Privacy Scope Triple](#privacy-scope-triples) is contained in the Privacy Scope of that Consent
    - They are associated with `CONTRACT` legal base, and there is an active relationship (`contract-id` in *Active Contracts*) with the Data Subject in question for which no `RELATIONSHIP-END` event has been registered
    - They are associated with `LEGITIMATE-INTEREST` legal base, and
        - IF the Data Subject made any `OBJECT` Demand, they are not part of Privacy Scope of any such Demand
        - IF the Data Subject made any `RESTRICT` Demand, they are a part of the intersection of Privacy Scopes of all such Demands
    - They are associated with `NECESSARY` legal base

The Privacy Compilers can be configured to evaluate Eligible Privacy Scopes in the context of particular regulations.
In this case, Privacy Compilers maintain a list of [Privacy Scope Triples](#privacy-scope-triples) prohibited by that regulation and they exclude them from the Eligible Privacy Scope.
E.g. under GDPR, it is prohibited to process gender and genetic data under any Legal Base other than Consent.

For convenience, Privacy Compilers MAY also keep track of a set of **Prohibited (Privacy Scope)-(Legal Base) Pairs**, in which they SHOULD include [Privacy Scope Triples](#privacy-scope-triples) made illegal by the legislation that they want to support. It might also be convenient, when Data Subject's `OBJECT` or `RESTRICT` Demands are granted over a particular Privacy Scope, to list that scope under `LEGITIMATE-INTEREST` in the **Prohibited (Privacy Scope)-(Legal Base) Pairs** for making sure not to re-include them in the **Eligible Privacy Scope** unless the user gives explicit consent, signs a contract or becomes subject to mandatory data keeping.

> E.g. under GDPR, as processing of RACE data is only allowed under 'CONSENT' for medical research purposes, examples of **[Prohibited (Privacy Scope)-(Legal Base) Pairs](./prohibiter-scope-gdpr.md)** include
>
> (`data-category`=`DEMOGRAPHIC.RACE`, `purpose`=`ADVERTISING`) - CONSENT
>
> (`data-category`=`DEMOGRAPHIC.RACE`) - CONTRACT
>
> (`data-category`=`DEMOGRAPHIC.RACE`) - LEGITIMATE-INTEREST

The **Eligible Privacy Scope** is recalculated with every Data Capture, or whenever a Privacy Request Demand (other than `ACCESS` and `TRANSPARENCY`) is granted.

Yet, the **Eligible Privacy Scope** is independent to [Retention Policy](./RFC-PRIV.md#retention-policy). A particular Data Capture Fragment MAY be associated with a non-empty Eligible Privacy Scope yet [be evaluated as expired under its Retention Policy](#resolving-retention-policies) and as such may need to be deleted anyway.

### Set Operations over Privacy Scope

#### Set-Theoretic Operations over Privacy Scope

A Privacy Scope consists of a set of [Privacy Scope Triples](#privacy-scope-triples).
All set operations (union, intersection, inclusion, etc.) are performed over Privacy Scopes taking into account the [Privacy Scope Triples](#privacy-scope-triples) equivalence.

Privacy Scopes MAY first be resolved to all of their equivalent [Privacy Scope Triples](#privacy-scope-triples), over which simple set-theoretic operations MAY be applied.


#### <a name="updateConsent"></a>Operations over consents

The scope of Consents can be modified by Privacy Request that include `OBJECT`, `RESTRICT`, and `REVOKE-CONSENT` actions.

The System SHOULD, at all times, keep track of *Active Consents*. We call a Consent active if its scope has not been modified or the Consent totally revoked. When the scope of a Consent is modified, a new Consent (that is now active) is made that replaces the old Consent (no longer active).

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
      "purposes":["PERSONALIZATION", "MARKETING", "ADVERTISING"]
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

The [Privacy Compiler](../high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
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
      "purposes":["PERSONALIZATION"]
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

The System MAY continue to use the Data Subjects' data for personalizing their experience but no longer has consent to use the data for marketing and advertising.

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
At the time of receiving this request, the System has consent for `STORING` and `SHARING` all `CONTACT` data for `PERSONALIZATION` purposes.
When the System gets this request, the scope of the consent MUST change. The remaining scope of the consent will only include:
- `SHARING` of all `CONTACT` data other then `CONTACT.EMAIL`, for `PERSONALIZATION` purposes, and
- `STORING` of all `CONTACT` for `PERSONALIZATION` purposes

The [Privacy Compiler](../high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
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
      "purposes":["PERSONALIZATION"]
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
      "purposes":["PERSONALIZATION"]
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
  "request-id": "e848d0e0-41ab-492c-ae90-ca891b70abc1",TRANSPARENCY.ORGANIZATION
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

At the time of receiving this request, the System has consent for `STORING` of all `CONTACT` for `PERSONALIZATION` purposes, and for `SHARING` of all `CONTACT` data other then `CONTACT.EMAIL`, for `PERSONALIZATION` purposes.

After processing the `RESTRICT` request, only the consent for `STORING` of all `CONTACT` for `PERSONALIZATION` purposes remains valid.

The [Privacy Compiler](../high-level-architecture#data-rights-compiler) SHOULD resolve this request by:
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

The System SHOULD be able to deliver a timeline of Consents, Privacy Requests and Privacy Request Responses, that may serve as a proof of compliance and good faith.

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
- They don't affect [Privacy Scope Triples](#privacy-scope-triples) that are included in the Eligible Privacy Scope under `CONTRACT` or `NECESSARY` legal bases,

- with regards to Consents, they affect only existing Consents, not the future ones.
    - Let us imagine for example that the Data Subject gave consent for processing of their data for any purpose.
    - Then later, the Data Subject makes an `OBJECT` Demand related to `SALE` purposes.
    At this point all [Privacy Scope Triples](#privacy-scope-triples) having `SALE` as purpose exit the Eligible Privacy Scope.
    - This same Data Subject MAY again give consent for processing of their data for any purpose in which case the [Privacy Scope Triples](#privacy-scope-triples) having `SALE` as purpose re-enter the Eligible Privacy Scope.

- with regards to [Privacy Scope Triples](#privacy-scope-triples) that are integrated in the Eligible Privacy Scope under `LEGITIMATE-INTEREST`, once `OBJECT` or `RESTRICT` Demands are made, they affect present and future Eligible Privacy Scope. In other words, the [Privacy Scope Triples](#privacy-scope-triples) that have exited the Eligible Privacy Scope due to `OBJECT` or `RESTRICT` Demands, can't re-enter Eligible Privacy Scope under `LEGITIMATE-INTEREST`. When several `OBJECT` or `RESTRICT` Demands are made over time, a particular [Privacy Scope Triple](#privacy-scope-triples) that entered the Eligible Privacy Scope under `LEGITIMATE-INTEREST`, can remain in the Eligible Privacy Scope if and only if:
    - It is not a part of union of Privacy Scopes of all `OBJECT` Demands, AND if
    - It is a part of the intersection of Privacy Scopes of all `RESTRICT` Demands

Let us take an example to illustrate updating of Eligible Privacy Scope. At the beginning the System holds the Data Subjects e-mail address for prospecting purposes, under `LEGITIMATE-INTEREST` Legal Base.
```
Eligible Privacy Scope:
CONTACT.EMAIL x * x MARKETING (LEGITIMATE-INTEREST)
```

The Data Subject, after receiving a marketing e-mail, decides to open an account and start using the service. They provide their postal address for billing. While creating an account, they also give consent for their postal address to be used for advertising purposes.

```
Eligible Privacy Scope:
CONTACT.EMAIL x * x MARKETING (LEGITIMATE-INTEREST)
CONTACT.EMAIL x * x SERVICES (CONTRACT)
CONTACT.ADDRESS x * x SERVICES (CONTRACT)
CONTACT.ADDRESS x * x ADVERTISING (CONSENT)
```

The Data Subject realizes that they are receiving too much advertising material and they formulate a Privacy Request with one `REVOKE-CONSENT` demand targeting particular consent that they gave.

```
Eligible Privacy Scope:
CONTACT.EMAIL x * x MARKETING (LEGITIMATE-INTEREST)
CONTACT.EMAIL x * x SERVICES (CONTRACT)
CONTACT.ADDRESS x * x SERVICES (CONTRACT)
```

The Data Subject realizes that they are still receiving marketing e-mail and they formulate a Privacy Request with one `OBJECT` demand with `CONTACT.EMAIL` being defined as its Privacy Scope. Yet, this Demand only affects the [Privacy Scope Triples](#privacy-scope-triples) held under `LEGITIMATE-INTEREST`. The System can still, continue to keep the `CONTACT.EMAIL` and `CONTACT.ADDRESS` for the same of the ongoing contractual relationship with the user.

```
Eligible Privacy Scope:
CONTACT.EMAIL x * x SERVICES (CONTRACT)
CONTACT.ADDRESS x * x SERVICES (CONTRACT)
```
However, the remaining purpose (`SERVICES`) now only allows the System to send e-mail related to the services being provided, and no longer supports sending marketing e-mail to this Data Subject.

### Calculating Permissions

Since the [Privacy Compiler](../high-level-architecture#data-rights-compiler) maintains the Eligible Privacy Scope at any time, it can (given a Data Capture ID, or a Data Capture Fragment ID) answer whether at that time, a particular data processing operation is permitted.

For example, the System can inquire whether a particular data fragment, corresponding to `CONTACT.EMAIL` data category, can be used to invoice the user (processing = `USING`; purpose = `SERVICES`), or whether it can be shared with some other partner system for user profiling (processing = `SHARING`; purpose = `AUTOMATED-INFERENCE`).


## Resolving requests

The [Privacy Compiler](../high-level-architecture#data-rights-compiler) evaluates Privacy Request Demands and issues recommendations to the System. The Systems can then be configured to respond to Privacy Requests automatically, blindly following those recommendations (whenever possible), or to await human input just in case. Cf. [different automation scenarios](./scenarios.md#automation)

Privacy Requests MAY need to be processed in the context of different [authentication scenarios](./scenarios.md#authentication) and different [response scenarios](./scenarios.md#response).

Here is how the Privacy Request Response recommendations are calculated:

When no Data Subject ID is provided in the Privacy Request:
- `TRANSPARENCY` Demands: recommend status = `GRANTED`. Provide requested information: Data Categories, Processing Categories, Purposes, and Legal Bases from Intended Privacy Scope, as well as other information from general settings as defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV) and under [Configuration and Prerequisites](#configuration-and-prerequisites). The `data` values of Privacy Request Responses MAY be formatted using UROPA format (see [UROPA section of PRIV](./RFC-PRIV.md#uropa)).
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- For any other action : recommend status = `DENIED`, motive=`IDENTITY-UNCONFIRMED`

When Data Subject ID is provided, Data Subject is authenticated but is unknown by the System:
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- For any other action : recommend status = `DENIED`, motive=`USER-UNKNOWN`

When Data Subject ID is provided, the Data Subject is known by the System but failed to authenticate:
- `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
- `TRANSPARENCY.KNOWN` Demands: recommend status = `GRANTED`, and data = `NO`.
- For any other action : recommend status = `DENIED`, motive=`IDENTITY-UNCONFIRMED`

When Data Subject ID is provided, the Data Subject is known by the System and authenticated:
- Regardless of restrictions
    - `OTHER` Demands: recommend human review and status = `UNDER-REVIEW`
    - `TRANSPARENCY.KNOWN` Demands: recommend status = `GRANTED`, and data = `YES`.
    - `TRANSPARENCY.DATA-CATEGORIES` Demands: recommend status = `GRANTED`, and data = list of Data Categories that are included in any of the [Privacy Scope Triples](#privacy-scope-triples) included in the Eligible Privacy Scope.
    - `TRANSPARENCY.PROVENANCE`, see [Resolving provenance in requests](#resolving-provenance-in-requests)
    - `TRANSPARENCY.ORGANIZATION`, `TRANSPARENCY.POLICY`, `TRANSPARENCY.RETENTION`, `TRANSPARENCY.DPO`, `TRANSPARENCY.WHERE`, `TRANSPARENCY.WHO`, Demands: recommend status = `GRANTED`, and data = information corresponding to the request taken from configuration settings as defined under [Implications for Systems](./RFC-PRIV.md#design-implications-for-systems-implementing-PRIV) and under [Configuration and Prerequisites](#configuration-and-prerequisites).

- With regards to Demand restrictions (if any) limiting the scope of the Demand:
    - first, check for presence of incompatible restrictions (and if incompatible recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED`):
        - [Consent Restriction](./RFC-PRIV.md#consent-restriction) with any other type of Restriction,
        - [Consent Restriction](./RFC-PRIV.md#consent-restriction) within a Demand other than `REVOKE-CONSENT`,
        - More than one [Capture Restriction](./RFC-PRIV.md#capture-restriction),
        - More than one [Data Reference Restriction](./RFC-PRIV.md#data-reference-restriction)
        - A Capture Restriction and any other restriction that is not a Privacy Scope Restriction, or a Data Reference Restriction,
        - More than one [Date Range](./RFC-PRIV.md#date-range) Restriction.

    - second, Calculate **Restriction Scope** and **Concerned Fragments**. This is done by processing every Restriction according to the following approach:
        - at the beginning set **Restriction Scope** to be equal to the Eligible Privacy Scope of the Data Subject
        **Concerned Fragments** is set to all Data Capture Fragments the `scope`s of which are included in the **Restriction Scope**.

        - when processing a [Privacy Scope](./RFC-PRIV.md#privacy-scope) Restriction, set the new **Restriction Scope** to be the intersection of the previous **Restriction Scope** with the Privacy Scope of the Restriction.
        **Concerned Fragments** is set to all Data Capture Fragments the `scope`s of which are included in the **Restriction Scope**.

        - when processing a [Capture Restriction](./RFC-PRIV.md#capture-restriction) set the new **Restriction Scope** to be the intersection of the previous **Restriction Scope** with union of the [Privacy Scope](./RFC-PRIV.md#privacy-scope)s of each Data Capture Fragment of each Data Capture the `capture-id` of which is listed under `capture-ids` of that Capture Restriction
        **Concerned Fragments** is set to all Data Capture Fragments that satisfy both of the criteria:
            - their `scope` is included in the **Restriction Scope**, AND
            - they are part of one of the Data Captures the `capture-id` of which is listed under `capture-ids` of that Capture Restriction

        - when processing a [Data Reference Restriction](./RFC-PRIV.md#data-reference-restriction) look for all the Data Capture the `data-reference` of which matches the `data-reference`  of the Restriction. Then for each such Data Capture `capture-id` proceed as if when processing when processing a [Capture Restriction](./RFC-PRIV.md#capture-restriction).

        - when processing a [Date Range](./RFC-PRIV.md#date-range), look for all the Data Capture Fragments the dates of which are within the given Date Range, and set the new **Restriction Scope** to be the intersection of the previous **Restriction Scope** with union of the [Privacy Scope](./RFC-PRIV.md#privacy-scope)s of each of those Data Capture fragments
        **Concerned Fragments** is set to all Data Capture Fragments that satisfy both of the criteria:
            - their `scope` is included in the **Restriction Scope**, AND
            - their `date` falls within the Date Range of the Restriction

        - when processing a [Provenance Restriction](./RFC-PRIV.md#provenance-restriction) look for all the Data Capture Fragments that match the Provenance Restriction criteria (as seen in [Resolving provenance in requests](#resolving-provenance-in-requests)) and set the new **Restriction Scope** to be the intersection of the previous **Restriction Scope** with union of the [Privacy Scope](./RFC-PRIV.md#privacy-scope)s of each of those Data Capture fragments
        **Concerned Fragments** is set to all Data Capture Fragments that satisfy both of the criteria:
            - their `scope` is included in the **Restriction Scope**, AND
            - they match the Provenance Restriction criteria (as seen in [Resolving provenance in requests](#resolving-provenance-in-requests))


        > **Note**
        >
        > Data Capture Fragments the scopes of which fall under the **Restriction Scope** are not the same as (but are a superset of) the Data Capture Fragments included in the **Concerned Fragments** scope.
        >
        > This is due to [Date Range](./RFC-PRIV.md#date-range), [Capture Restriction](./RFC-PRIV.md#capture-restriction) and [Provenance Restriction](./RFC-PRIV.md#provenance-restriction), all of which might be used to select particular Data Capture Fragments out of many thay may be captured with the same Data Capture Fragment `selector`.
        >

    - third, with regards to the `action` of the Demand:     
     - `TRANSPARENCY.LEGAL-BASES` Demands, recommend status = `GRANTED`, and data = list of Legal Bases under which any of the [Privacy Scope Triples](#privacy-scope-triples) are included in the **Restriction Scope**
     - `TRANSPARENCY.PROCESSING-CATEGORIES` Demands: recommend status = `GRANTED`, and data = list of Processing Categories that are included in any of the [Privacy Scope Triples](#privacy-scope-triples) included in the **Restriction Scope**.
     - `TRANSPARENCY.PURPOSE` Demands: recommend status = `GRANTED`, and data = list of Purposes that are included in any of the [Privacy Scope Triples](#privacy-scope-triples) included in the **Restriction Scope**
     - `REVOKE-CONSENT` Demands:
         - If restricted to concrete consent IDs with a [Consent Restriction](./RFC-PRIV.md#consent-restriction), recommend status = `GRANTED` and recalculate Eligible Privacy Scope to drop any [Privacy Scope Triples](#privacy-scope-triples) that have been included as a result of Consents being revoked.
         - If Demand is restricted by a Privacy Scope, recommend status = `GRANTED` and [update consents](#updateConsent)
         - If no Restriction is given in the Demand, revoke all consents given by this Data Subject
         - If only a Date Range restriction is present, recommend status = `GRANTED` and revoke all consents that have been collected in the given Date Range
         - In other combinations of Restrictions, take the resulting **Restriction Scope**, recommend status = `GRANTED` and [update consents](#updateConsent) as if an `OBJECT` Demand has been made with the **Restriction Scope**

     - `OBJECT`, `RESTRICT` Demands:
         - Recommend status = `GRANTED`, and then, upon granting [update consents](#updateConsent), [recalculate Eligible Privacy Scope](#updateScope) by excluding **Restriction Scope** or limiting to the **Restriction Scope**
         - Recommend deletion of the **Concerned Fragments**.

     - `DELETE` Demands:
         - If restricted to a Privacy Scope Restriction having a `processing-category` or a `purpose`, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED` (A DELETE request can only be relative to a category of data, not to a category of processing or a particular purpose.)
         - If the **Concerned Fragments** set is empty, recommend status = `DENIED`, motive = `NO-SUCH-DATA`
         - If it is non-empty:
             - recommend for deletion the Data Capture Fragments from that set, the `scope` of which only includes [Privacy Scope Triples](#privacy-scope-triples) that are introduced in the Eligible Privacy Scope under Legal Bases belonging to {`LEGITIMATE-INTEREST`, `CONSENT`}
             - if the set of Data Capture Fragments recommended for deletion is *the same as* the **Concerned Fragments** set, recommend status = `ACCEPT`,
             - else, if the set of Data Capture Fragments recommended for deletion is *included in* the **Concerned Fragments** set, recommend status = `PARTIALLY-GRANTED`,
             - else, recommend status = `DENIED`,
             - when status is one of {`PARTIALLY-GRANTED`, `DENIED`} add one or more motives = `VALID-REASONS` or `IMPOSSIBLE` when **Concerned Fragments** that are not recommended for deletion, have in their `scope` Privacy Scope Triples included in the Eligible Privacy Scope under `CONTRACT` or `NECESSARY` Legal Bases, respectively.

     - `MODIFY` Demands:
         - If restricted to a Privacy Scope Restriction having a `processing-category` or a `purpose`, recommend status = `DENIED`, motive = `REQUEST-UNSUPPORTED` (A MODIFY request can only be relative to a category of data, not to a category of processing or a particular purpose.)
         - If the **Concerned Fragments** set is empty, recommend status = `DENIED`, motive = `NO-SUCH-DATA`
         - If it is non-empty, recommend status = `ACCEPT` (potentially upon human validation)

     - `ACCESS` Demands:
         - If the **Concerned Fragments** set is empty, recommend status = `DENIED`, motive = `NO-SUCH-DATA`
         - If it is non-empty, recommend status = `ACCEPT`, and data = data corresponding to the Privacy Scope of the Demand

         (NB. contrary to MODIFY and DELETE, the Data Subject SHOULD be able to request access to data being used for particular `purpose` or being subject to particular `processing-category`)

     - `PORTABILITY` Demands:
         - If the **Concerned Fragments** set is empty, recommend status = `DENIED`, motive = `NO-SUCH-DATA`
         - If it is non-empty, recommend status = `ACCEPT` and data = data corresponding to the Privacy Scope of the Demand


## Resolving Retention Policies

[Privacy Compilers](../high-level-architecture#data-rights-compiler) SHOULD store and resolve [Retention Policies](./RFC-PRIV.md#retention-policy), as well as to them associated *Events* in **Runtime Maps**.

Systems SHOULD define Retention Policies at the time of configuration, and SHOULD cover all Data Categories and Data Capture Fragment `selector`s from the Intended Privacy Scope with at least one Retention Policy.

Retention Policies are resolved upon concrete instances of Data Capture Fragments. A particular instance of data, given the Data Capture Fragment `selector` to which it corresponds, is considered `EXPIRED` if all of the following is true:
- There is a Retention Policy the `data-categories` of which is a Privacy Scope that includes Data Capture Fragment `selector` of the particular Data Capture Fragment, that is of type `NO-LONGER-THAN`, such that the date of the event defined under `after` has passed for a more then the time defined under `duration`
- AND `selector` of the Data Capture Fragment is NOT a part of a Privacy Scope of any of the Data Categories defined under `data-categories` property of the Retention Policy, whose type is `NO-LESS-THAN` and the difference between the current date and the date of the event defined under `after` is less than the value of `duration`, or has already occurred 

Privacy Compilers SHOULD be able to:
- provide lists of active policies, in the context of answering to the `TRANSPARENCY.RETENTION` requests
- resolve policies and generate `EXPIRED` alerts, upon which the Systems MAY chose to implement automatic data deletion, or other protocols for data archiving or similar
- resolve policies for Systems configured not to automatically delete data, but to automatically grant `DELETE` requests only when data is `EXPIRED`

Optionally, for systems wanting to automatically deny `DELETE` requests when data MUST be kept, Privacy Compilers MAY be able resolve policies giving `HOLD` status, when there is at least one Retention Policy the `data-categories` of which is a Privacy Scope that includes Data Capture Fragment `selector` of the particular data, that is of type `NO-LESS-THAN`, such that the event defined under `after` is yet to happen or has happened before a period of time inferior to `duration`.

## Working with Provenance

### Remembering provenance
In order to correctly process `TRANSPARENCY.PROVENANCE` requests as well as requests that are intended to be transferred (`target` = `ORGANIZATION`, `PARTNERS`), the Privacy Compiler MUST:
- Keep track of transfers, as described in [Implications for Systems](./RFC-PRIV.md#remembering-transfers)
- Keep track of System IDs that correspond to particular targets values, i.e. know which Systems are in `ORGANIZATION`, and which are in `PARTNERS`
- For every **Known Selector** keep track of one or more [Provenance](./RFC-PRIV.md#provenance) objects.

> When a System generates data about the Data Subject, it creates a Data Capture and associates its Fragments with a [Provenance](./RFC-PRIV.md#provenance) object having `provenance-category`: `DERIVED`
>
> When a System A receives a Data Capture from another System B, they associate to all of its Fragments an additional [Provenance](./RFC-PRIV.md#provenance) object having `provenance-category`: `TRANSFERRED`
>
> A Data Capture Fragment may end up having multiple [Provenance](./RFC-PRIV.md#provenance) objects to indicate that it has been given by a human user to one System (System B), then transferred to another System (System A).


### Resolving provenance in requests

In response to `TRANSPARENCY.PROVENANCE` Demands, the Privacy Compiler can:
- look for [Data Capture Fragment](./RFC-PRIV.md#data-capture-fragments) related to particular Data Subject,
- specifically, when the `TRANSPARENCY.PROVENANCE` Demand is constrained to a particular Privacy Scope, look for only Data Capture Fragments corresponding to this particular Privacy Scope, and
- retrieve the [Provenance](./RFC-PRIV.md#provenance) objects provided in `provenance` of such Data Capture Fragments

When a Demand is restricted by a [Provenance Restriction](./RFC-PRIV.md#provenance-restriction), the Privacy Compiler is tasked with a more complex interpretation:
- The [Provenance Restriction](./RFC-PRIV.md#provenance-restriction) either includes an explicit `target`, one of {`ORGANIZATION`, `PARTNERS`, `SYSTEM`}, or `SYSTEM` is assumed.
- The Privacy Compiler MUST resolve this information in the context of the particular System that it serves.
    - `SYSTEM` is understood as the System that the Privacy Compiler serves.
    - To resolve `ORGANIZATION` and `PARTNERS` The Privacy Compiler looks into the correspondence table it keeps, to know which System IDs are `ORGANIZATION` and `PARTNERS` Systems to the System it serves.

After having resolved the `target` value to concrete Systems IDs, the Privacy Compiler looks for Data Capture Fragments, the `provenance` of which matches both:
- the `provenance-category` of the Demand's [Provenance Restriction](./RFC-PRIV.md#provenance-restriction), AND
- the one of the System IDs to which the `target` value has been resolved.

> A Data Capture Fragment has been given by a human user to one System (System B), then transferred to another System (System A).
>
> A Data Subject may address a Demand to DELETE all Data Capture Fragments that have been `TRANSFERRED`. In the case of the above-mentioned Data Capture Fragment such Demand is interpreted differently by the System A (that should respond `GRANTED`) and by the System B (that should respond `DENIED`).
>
> The Systems A and B behave the same way when each of them receives this Demand directly from the Data Subject, and when the Data Subject formulates their Demand to only one System and marks it with the `target`: `PARTNERS` so that the Demand is transmitted from one System to another.

## References

### Normative References

- **[RFC8259]**  Bray, T., ["The JavaScript Object Notation (JSON) Data Interchange Format"](https://datatracker.ietf.org/doc/html/rfc8259), STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017.
- **[RFC3986]**  Berners-Lee, T., Fielding, R., and L. Masinter, ["Uniform Resource Identifier (URI): Generic Syntax"](https://www.rfc-editor.org/rfc/rfc3986), STD 66, RFC 3986, January 2005.
- **[RFC2119]**  Bradner, S., ["Key words for use in RFCs to Indicate Requirement Levels"](https://datatracker.ietf.org/doc/html/rfc2119), BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,


### Supported Legislation

- [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [CCPA](https://leginfo.legislature.ca.gov/faces/codes_displayText.xhtml?division=3.&part=4.&lawCode=CIV&title=1.81.5)

### Yet to be Supported Legilsation

- CPRA
- HIPPA
