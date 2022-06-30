# Architecture clarifications

| Status     | draft                                                             |
|:-----------|:------------------------------------------------------------------|
| **PR #**   | [748](https://github.com/blindnet-io/product-management/pull/748) |
| **Author** | Amaury Rousseau (amaury@blindnet.io)                              |

## Context and Problem Statement

The [High Level Conceptualization](https://github.com/blindnet-io/product-management/blob/d3dad802ce52fb1488cbda8302d3c36c94c3b47b/refs/high-level-conceptualization/README.md),
[High Level Architecture](https://github.com/blindnet-io/product-management/blob/d3dad802ce52fb1488cbda8302d3c36c94c3b47b/refs/high-level-architecture/readme.md),
and the [Architecture specification](https://github.com/blindnet-io/product-management/blob/ae344653217b03d3857fba63f5d716e43c72263b/specifications/architecture/README.md)
leave some free space for interpretation when implementing the devkit components.
To enable an efficient, coordinated and coherent development of all components, some choices have to be made.

## Considered Options

This record is the result of multiple meetings to discuss this matter between @filipblnt, @m4rk055 and @TheKinrar.

## Decision Outcome

### Interaction of Data Capture and Storage components

The Storage component only acts as an abstract interface to any backing storage implementation.
It is able to store data as byte streams, which might be short text representations, like Data Capture metadata,
or large files, like the actual data of a Capture Fragment.
File paths are used to designate data when reading and writing.
It is agnostic of the format of the data, and does not know either if the data is encrypted or not.

The Data Capture component is responsible for initiating data captures, but also for later retrieval of the data.
Therefore, it stores the minimal set of metadata needed for these operations, which includes IDs of captures, fragments
and users, fragment selectors and permissions.
When a client app is creating a Data Capture, the Data Capture Component is responsible for generating the ID of the
capture and of its fragments. It will return these to the app, alongside the necessary information for uploading the
actual data to the Storage Component. This includes a signed token authorizing the user for the upload process.
Fragment data never transits through the Data Capture Fragment.

### Encryption

Encryption being optional, the Data Capture and Storage components need to behave in the same way, whether
the data is encrypted or not. The Data Capture and Storage component do not need to communicate with the
Encryption Component, only the client app does.
The Encryption component is responsible for storage of all encryption keys, including user asymmetric keys and fragment
symmetric keys. Fragment data is the only data to be encrypted.

### Authentication and authorization

All components depend on the Identity Component for authentication purposes. The Identity Component will typically
take an Authorization header as input, and output a verified user ID, and some additional user info if needed.

Each component performs authorization of requests based on the output of the Identity Component.

### Versioning

Versioning is handled by the Data Capture component. Each version of a fragment has its own ID which is used to store
and retrieve the data in the Storage component. When a new version of a fragment is created, a new version ID is
generated and the new data can be uploaded to the storage.

This requires a change in the
[devkit Data Model](https://github.com/blindnet-io/product-management/tree/devkit-dbmodel/specifications/model):
Capture Fragment now has Versions, which have UUIDs too, and the Data value is moved from the fragment to the version.

<!-- markdownlint-disable-file MD013 -->
