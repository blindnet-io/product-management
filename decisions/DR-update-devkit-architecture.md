# Update devkit architecture

| Status      | accepted |
| :---------- | :-------------------------------------------------------------------------------------- |
| **PR #**    | [761](https://github.com/blindnet-io/product-management/pull/761/) |
| **Author & Sponsor** | [Marko](https://github.com/m4rk055) (marko@blindnet.io) |
| **Reviewers** | [Milan](https://github.com/milstan), [Amaury](https://github.com/TheKinrar), [Justin](https://github.com/jboileau99) |
| **Assignee** | [Milan](https://github.com/milstan) |

## Context and Problem Statement

The model described in the [PRIV](https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md) document requires the [Privacy Compiler](https://github.com/blindnet-io/product-management/tree/main/refs/high-level-architecture#privacy-compiler) to be aware of every [Data Captures and Capture Fragments](https://github.com/blindnet-io/product-management/tree/main/refs/high-level-architecture#privacy-compiler) in the system.
That puts a burden on the implementing system to
- make sure every data point collected by the system is as well referenced (metadata) in the Privacy Computation Engine database
- collect or transform data to a particular format (capture and fragments)

This DR proposes removing the notion of Data Captures and Capture Fragments from Privacy Computation Engine.

## Proposal

The [Privacy computation engine](https://github.com/blindnet-io/product-management/tree/main/refs/high-level-architecture#privacy-computation-engine) (PCE) should have the following components:
- Privacy Compiler
- Privacy Request Capture Interface
- Data Consumer/DPO Interface
- Data access engine
- Data storage connectors (for e.g. Postgres, MongoDB, Azure Storage)

**Data access engine** is a component deployed by a client. It communicates with the **Privacy Compiler** and a **Data storage connector**.

A **Data storage connector** is a component that has mappings that queries the data storage. It can be implemented by blindnet or by a client for an unsupported storage or if the data model is not suitable.
It should containg a set of rules (mappings) on how to map a `selector` to a corresponding fetch query (`selector` to a e.g. table column in a relational database). 

PCE is [configurable](https://github.com/blindnet-io/product-management/blob/2645056f4477a93b5a6635129c77a3e7fe4d9a9b/refs/schemas/priv/expected-behavior.md#configuration-and-prerequisites) with the following:
- Parameters for `TRANSPARENCY` requests
- `selectors`
  - retention policies for every `selector`
  - `privacy scope` for every `selector`
- Legal bases with privacy scopes
  - necessary
  - contracts
  - legitimate interests
  - consent templates (default consents)
- Regulations

Regulation is defined as `(privacy scope)-(legal base)` which means data in `privacy scope` can only be processed if a user has the active `legal base` (e.g. has given consent).

A new user can be created in the PCE in the following ways:
- manually, with a request
- upon giving a consent
- upon making a privacy request

By default, the user's eligible privacy scope is composed of privacy scope triples from `necessary`, `contracts` and `legitimate interests` legal bases, with regards to all `Regulations`. Every subsequent consent or privacy request will change the user's eligible privacy scope.

### TBD Retention policy

Since metadata can't be accessed by a privacy compiler, handling retention policies becomes a tricky problem.
Data access engine can handle them by querying the storage on fixed intervals. That might put burden of additional development on a client.

### TBD Provenance

Privacy compiler should also be aware of data transfers between the systems, which includes knowing about the ids of the transferred data.

### 