# Title of RFC

| Status        | draft                                                                                  |
| :------------ | :------------------------------------------------------------------------------------- |
| **PR #**      | [NNN](https://github.com/blindnet-io/PROJECT/pull/NNN) (update when you have PR #)     |
| **Author(s)** | milstan (milstan@blindnet.io), Clémentine VINCENT (clementine@blindnet.io)             |
| **Sponsor**   | Filip (filip@blindnet.io)                                                              |
| **Updated**   | 2022-05-19                                                                             |

## Objective

We propose a simple, structured data format for representing [Rights Requests](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization#data-capture--rights-requests).

## Motivation

Different systems, and different compontents of a single system, including different comnponents of blindnet devkit are likely to exchange information about Rights Requests.
Therefore, a common format is needed to facilitate exchange of information without loss of semantics.

## Benefit

**TBD** How will users (or other contributors) benefit from this work? What would be the
headline in documentation, release notes or blog post?

## Proposal

**TBD - Clémentine: you can imput your lists of request types, tratment types etc here.**This is the meat of the document, where you explain your proposal. If you have
multiple alternatives, be sure to use sub-sections for better separation of the
idea, and list pros/cons to each approach. If there are alternatives that you
have eliminated, you should also list those here, and explain why you believe
your chosen approach is superior.

Make sure you’ve thought through and addressed the following sections. If a section is not relevant to your specific proposal, please explain why, e.g. your RFC addresses a convention or process, not an API.

### Alternatives Considered

**TBD**- Make sure to discuss the relative merits of alternatives to your proposal.

### User Impact

**TBD**- What are the user-facing changes? How will this feature be rolled out?

## Detailed Design

The proposed desing comes in two forms that are to be considered together:
(1) This reference document, definining key concepts, terms and relationships in a human-readable format
(2) A JSON Schema document (link soon), for machine-readable interpretation of Rights Requests compliant with [v4 (or ideally lower) of IETF specification](https://datatracker.ietf.org/doc/html/draft-zyp-json-schema-04#:~:text=JSON%20Schema%20is%20a%20JSON,interaction%20control%20of%20JSON%20data.)

The key requirements of the desing are to enable:
- Unambiguous expression of Rights Requests in a machine-readable form
- Integrity of Rights Requests semantics when exchanged between components and systems. 
I.e. A system that has not directly collected the Rights Requests from the user, but has received in in JSON format from another system, can make the exact same interpretation of the request as if it had collected the request directly.
- A way of uniquely identifying one and the same Rights Request across systems and components concerned by it.

## Questions and Discussion Topics

**TBD** Seed this with open questions you require feedback on from the RFC process.
