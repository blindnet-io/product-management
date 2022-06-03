# blindnet - Functionnal Requirements Document

## Implementation - Functional requirements

### blindnet BE

_**FR-G01.** The system must verify all user requests with JWT. The signing algorithm is EdDSA._

For authenticated users, JTW contains (FR-BE01, 02, 03, 07, 08, 09, 10):
* type: “jwt”
* app_id
* user_id 
* user_group_id
* expiry

For unauthenticated users, JWT contains (FR-BE04, 05, 06):
* type: “stjwt” (short for short-term jwt)
* app_id
* request_id (randomly generated)
* user_group_id
* list of user_id (optional)
* expiry

For client’s backend, JWT contains (FR-BE11, 12, 13):
* type: “cl” (short for client)
* app_id
* request_id (randomly generated)
* expiry

_**FR-BE01.** The system must be able to register a new user's identity. Each user must be associated with a particular blindnet client._

Input:
* JWT
* Signed JWT
* public_encryption_key
* public signing key
* key_derivation_salt
* encrypted_private_encryption_key
* encrypted_private_signing_key
* signed_public_encryption_key

Output:
* OK

The system must verify the signed JWT and signed public encryption key with the user's public signing key. The signing algorithm used in this signature is Ed25519.

The system extracts the user_id from the JWT, creates a user with that id and associates it with the user_group_id (extracted from the JWT), and all provided keys.

Usage: 1c

Blindnet ref: same as FR-UM01

_**FR-BE02.** The system must be able to retrieve user’s public keys and encrypted private keys_

Input:
* JWT

Output:
* user_id
* public_encryption_key
* encrypted_private_encryption_key
* key_derivation_salt
* public_signing_key
* encrypted_private_signing_key
* signed_public_encryption_key

The system extracts the user_id from the JWT, and retrieves the user's public key and encrypted private key.

Usage: 1d

_**FR-BE03.** The system must deliver the users PKs upon request._

Input:
* JWT
* user_id

Output:
* user_id
* public_encryption_key
* public_signing_key
* signed_public_encryption_key

The system validates the JWT, and retrieves the public key associated with the user_id.

Usage: 8c

Blindnet ref: similar to FR-UM03, but with a list of user ids

_**FR-BE04.** The system must deliver the users PKs upon request. (convert to POST)_

Input:
* One time JWT (contains group_id ) or regular JWT
* group_id or a list of user ids

Output:
* a list of
    * user_id
    * public_encryption_key
    * public_signing_key
    * signed_public_encryption_key

If otJWT, the system extracts the user group_id from the JWT, checks that it is the same as the one in body (if given), and retrieves public keys of each user_id that is associated with that user group_id. 

If instead of group_id the body contains a list of user ids, verify that all user ids from the body belong to the group_id from the token, and if yes return the public keys of all user ids given in the body.

If regular JWT, just return the response by using the group id from the body

Usage: 2a

_**FR-BE05.** The system must deliver the users PKs upon request. (convert to POST)_

Input:
* One time JWT (contains list of user ids) or regular JWT
* a list of user ids

Output:
* a list of
    * user_id
    * public_encryption_key
    * public_signing_key
    * signed_public_encryption_key

If otJWT, the system extracts the list of user ids from the JWT, checks that all user ids from the req body are present in the JWT, and retrieves public keys of each user id from the body. 

If regular JWT, just return the response by using the list of users from the body.

_**FR-BE06.** The system must accept and store encrypted symmetric keys from users and associate them with a document._

Input:
* one_time_JWT or JWT
* a list of:
    * encrypted_symmetric_key
    * user_id

Output:
* document id

If otJWT, check that the group id from the JWT is related to all user ids in the request, or that the JWT contains the specified user ids, if regular JWT then the check is not necessary.  

The backend randomly creates a document id and for each user_id stores a triple _{user_id, encrypted symmetric key, document id}_.

Usage: 2d, 2e, 2f

Blindnet ref: similar as FR-M13

_**FR-BE07.** The system must be able to return the encrypted symmetric key_

Input:
* JWT
* document_id

Output:
* encrypted_symmetric_key

The system extracts user_id from the JWT, and returns the encrypted symmetric key associated with the user_id and document_id

Usage: 3a

Blindnet ref: same as FR-14-2

_**FR-BE08.** The system must return all encrypted symmetric keys of a user._

Input:
* JWT

Output:
* a list of
* document_id
* encrypted_symmetric_key

The system extracts user_id from the JWT, and returns all encrypted symmetric keys associated with the user_id.

Usage: 8a

_**FR-BE09.** The system must update user’s encrypted private keys and salt_

Input:
* JWT
* encrypted_private_encryption_key
* encrypted_private_signing_key
* key_derivation_salt

Output:
* Ok

Usage: 4c

_**FR-BE10.** The system must allow addition of encrypted symmetric keys to a given user._**

Input:
* JWT
* user_id
* a list of:
    * document_id
    * encrypted_document_key

Output:
* Ok

The system validates the JWT, and adds _{user_id, encrypted document key, document id} triples_. The user_id to use in these triples is the one from the request, not the one from the JWT.

Usage: 8e

_**FR-BE11.** The system must delete all references for a given document id._

Input:
* client JWT
* document_id

Output:
* Ok

The system validates the JWT signature, and for the given document_id deletes a tuple {_document_id, encrypted_key} _for every user in the system.

Usage: 5b

_If a document with a given id is stored on Azure, delete it from Azure storage._

_**FR-BE12.** The system must revoke access to documents for a given user._

Input:
* client JWT
* user_id

Output: 
* Ok

The system validates the JWT signature, and deletes all encrypted symmetric keys associated with the given user_id.

Usage: 6b

_**FR-BE13.** The system must delete a given user._

Input:
* client JWT
* user_id

Output: 
* Ok 

The system validates the JWT signature, and deletes all user data (all keys and all encrypted symmetric keys associated with the user_id).

Usage: 7b

_**FR-BE14.** The system must delete a given hotel._

Input:
* client JWT
* hotel_id

Output: 
* Ok 

The system validates the JWT signature, and deletes all users and their associated data and encrypted symmetric keys from the system.

Usage: 11b

_**FR-BEXX.** The system must initialize the parameters to upload a file to Azure blob storage._

Input:
* one_time_JWT or JWT

Output:
* data_id

The system generates the data_id and stores it in the database.

_**FR-BEXX.** The system must accept and store the encrypted metadata._

Input:
* one_time_JWT or JWT
* data_id
* metadata

Output:
* ok

The system verifies the data_id was created by the requesting user (uid or tid).

_**FR-BEXX.** The system must be able to generate an upload link for a block for Azure blob storage._

Input:
* one_time_JWT or JWT
* data_id
* block_size

Output:
* url
* authorization_header
* date
* block_id

The system checks if the block/total size is within the limit.

The system generates and stores the block_id in the database (linked with data_id).

The system creates and signs the upload link and returns the parameters in the response.

_**FR-BEXX.** The system must be able to commit the file upload to Azure blob storage._

Input:
* one_time_JWT or JWT
* data_id
* block_ids

Output:
* ok

The system checks if all the block_ids belong to the data_id, generates, signs and executes the request to the Azure blob storage.

_**FR-BEXX.** The system must be able to retrieve the encrypted metadata._

_storage._

Input:
* JWT
* data_id

Output:
* encrypted_metadata

_**FR-BEXX.$** The system must be able to create and sign the signed download link for GCP storage._

Input:
* JWT
* data_id

Output:
* url
* authorization_header
* date

The system creates and signs the download link and returns the parameters in the response.

_**FR-BEXX.** The system must accept and store encrypted symmetric keys for data stored in the azure storage._

Input:
* one_time_JWT or JWT
* data_id
* a list of:
    * encrypted_symmetric_key
    * user_id

Output:
* oK

Similar to BE06, only the document id is provided from the client side.

The system checks if the data_id was created by the requesting user (uid or tid).

_**FR-BE17.** The system must retrieve requested symmetric keys of a user._

Input:
* JWT
* list:
    * data id

Output:
* list
    * data id
    * symmetric key

The system extracts user_id from the JWT, and returns only encrypted symmetric keys related to documents with provided ids.

Note: This is similar to FR-BE08 if an optional parameter is given. Unlike FR-BE08, this route should be POST and the data ids should be given in the request body (same as with FR-SYKEY02).

If a user does not have a key for some of the data id values, return “400 User does not have access to some of the provided data”.

_**FR-BE18.** The system must revoke access to a document for a given user._

Input:
* client JWT
* doc_id
* user_id

Output:
* Ok

The system validates the JWT signature, and deletes the encrypted symmetric key associated with the given doc_id and user_id.

### FE javascript SDK

_**FR-SDK01.** The SDK must be able to generate cryptographic keys._

Generation of cryptographic keys must include both random symmetric keys, random asymmetric key pairs, and symmetric keys based on a passphrase.

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 1a, 2b, 4b

Blindnet ref: similar as FR-SDK01, but with the passphrase

_**FR-SDK02.** The SDK must be able to locally store, locally retrieve, or delete cryptographic keys._

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 1a, 1e, 4a

Blindnet ref: same as FR-SDK02

_**FR-SDK03.** The SDK must be able to register the user's identity._

This is a functionality that must be directly exposed to developers that use the SDK.

Inputs, provided by developers that use the SDK:
* JWT

User registration workflow:
* SDK generates a random encryption key pair (FR-SDK01)
* SDK generates a random signing key pair (FR-SDK01)
* SDK generates a symmetric key based on a passphrase (FR-SDK01) (with salt)
* SDK encrypts the private encryption key with the symmetric key
* SDK encrypts the private signing key with the symmetric key
* SDK signs the JWT with the private signing key
* SDK signs the public encryption key with the private signing key
* SDK sends a request to blindnet with inputs (FR-BE01)
    * JWT
    * generated public encryption key
    * generated public signing key
    * key_derivation_salt
    * encrypted_private_encryption_key
    * encrypted_private_signing_key
    * signed_public_encryption_key
    * Signed JWT
* SDK receives registration confirmation from blindnet.

Usage: 1b

Blindnet ref: similar as FR-SDK03

_**FR-SDK03-2.** The SDK must be able to retrieve from blindnet the user's encrypted private keys and decrypt them_

This is a functionality that must be directly exposed to developers that use the SDK.

Inputs, provided by developers that use the SDK:
* JWT
* passphrase

User registration workflow:
* SDK generates a symmetric key based on a passphrase and salt (FR-SDK01)
* SDK fetches the encrypted private keys and the public keys from blindnet (FR-BE02)
* SDK decrypts the private keys with the symmetric key

Usage: every time employee logs in

Usage: 4a

_**FR-SDK04.** The SDK must be able to retrieve public keys from blindnet backend._

A request is sent to blindnet backend (FR-BE04/05) containing:

Input:
* JWT / one time JWT
* a list of user ids (must be inside one time JWT)

Output:
* A list of
    * user_id
    * public_encryption_key
    * public_signing_key
    * signed_public_encryption_key

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 8c (a single PK)

Blindned ref: similar as FR-SDK04, but with list of user ids

_**FR-SDK04-2.** The SDK must be able to retrieve public keys from blindnet backend._

A request is sent to blindnet backend (FR-BE04) containing:

Input:
* One time JWT (contains hotel id)

Output:
* A list of
    * user_id
    * public_encryption_key
    * public_signing_key
    * signed_public_encryption_key

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 2a

_**FR-SDK04-3.** The SDK must be able to retrieve a public key from blindnet backend._

A request is sent to blindnet backend (FR-BE03) containing:

Input:
* JWT / one time JWT
* user id

Output:
* user_id
* public_encryption_key
* public_signing_key
* signed_public_encryption_key

This is a functionality that must not be directly exposed to developers that use the SDK.

_**FR-SDK05.** The SDK must be able to encrypt messages._

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT / one time JWT
* optional list of user id (gdpr: for encrypting for a user with id other than the one in JWT)
* message data
* optional metadata

Functionality workflow:
* SDK retrieves the public key of the recipients, by sending a request to blindnet backend (2a, FR-SDK04-2; FR-SDK04-3 if optional user id is provided)
* SDK verifies the public encryption key signature with the public signing key
* SDK generates a random symmetric encryption key (2b, FR-SDK01)
* SDK encrypts the generated symmetric key with each recipient public key and uploads all of them to blindnet (2c, 2d, FR-SDK06)
* SDK encrypts the data with the symmetric key (2b)

Outputs:
* encrypted data and metadata (one object)
* document id

Usage: 2

Blindnet ref: similar as FR-SDK07, but with list of user ids and a document id

_**FR-SDK05-02.** The SDK must be able to encrypt and store messages._

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT / one time JWT
* message data
* optional metadata

Functionality workflow:
* SDK retrieves the public key of the recipients, by sending a request to blindnet backend (2a, FR-SDK04-2)
* SDK verifies the public encryption key signature with the public signing key
* SDK generates a random symmetric encryption key (2b, FR-SDK01)
* SDK encrypts the generated symmetric key with each recipient public key and uploads all of them to blindnet (2c, 2d, FR-SDK06)
* SDK encrypts and transfers the metadata to blindnet server (FR-BEXX)
* SDK splits the data to fixed size chunks and for each chunk (can be done in parallel)
    * SDK encrypts the data with the symmetric key (2b)
    * SDK obtains the signed storage link from blindnet (FR-BEXX)
    * SDK directly stores the data to the Azure with the signed storage link
* SDK tells the blindnet to commit the file transfer (FR-BEXX)

Outputs:
* document id

Usage: /

_**FR-SDK06.** The SDK must be able to encrypt symmetric keys and post them to blindnet backend._

Symmetric encryption keys generated by the SDK must be encrypted with the user’s public keys. All encrypted keys are then sent to blindnet in a request containing (FR-BE06):
* JWT / one time JWT
* list of objects each containing
    * encrypted symmetric key
    * user_id

Output:
* document id

This is a functionality that must not be directly exposed to developers that use the SDK

Usage: 2c, 2d

Blindnet ref: similar as FR-SDK05

_**FR-SDK07.** The SDK must be able to retrieve encrypted symmetric keys from blindnet backend, and decrypt them._

Symmetric encryption keys encrypted with the public key must be retrieved from blindnet backend and decrypted with the associated private key.

Workflow:
* SDK retrieves the encrypted symmetric key from blindet with a request containing:
    * JWT
    * document id
    Response is an encrypted symmetric key
* SDK decrypts the encrypted symmetric key with the local private key.

This is a functionality that must not be directly exposed to developers that use the SDK

Usage: 3a, 3b, 8a, 8b

Blindnet ref: similar to FR-SDK06

_**FR-SDK08.** The SDK must be able to decrypt messages._

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT
* encrypted data and metadata (one object)

Functionality workflow:
* SDK retrieves and decrypts the encrypted symmetric key from blindnet backend (FR-SDK07).
* SDK decrypts the encrypted data with the decrypted symmetric key

Outputs:
* message data
* optional metadata

Usage: 3c

Blindnet ref: similar as FR-SDK09

_**FR-SDK08-02.** The SDK must be able to decrypt multiple messages._

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT
* list:
    * encrypted data and metadata (one object)

Functionality workflow:
* SDK retrieves and decrypts all the encrypted symmetric keys from blindnet backend (FR-SDK08).
* SDK decrypts all the encrypted data with the decrypted symmetric key

Outputs:
* list
    * data id
    * message data
    * optional metadata

Usage: /

_**FR-SDK08-03.** The SDK must be able to retrieve and decrypt messages._

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT
* document id

Functionality workflow:
* SDK retrieves and decrypts the encrypted symmetric key from blindnet backend (FR-SDK07).
* SDK retrieves the signed download link (FR-BEXX)
* SDK downloads the encrypted data directly from the Azure blob storage
* SDK decrypts the encrypted data with the decrypted symmetric key

Outputs:
* message data
* optional metadata

Usage: /

_**FR-SDK09.** The SDK must handle the passphrase update_

This is a functionality that must be directly exposed to developers that use the SDK. 

Inputs given by developers that use the SDK:
* JWT
* new_passphrase (assumes that pass change on client’s frontend only requires new pass to be entered).

Functionality workflow:
* SDK locally retrieves the private key (FR-SDK02)
* SDK generates a new key based on the new_passphrase and salt (FR-SDK01)
* SDK encrypts user’s private encryption and signing key (FR-SDK12)
* SDK uploads the encrypted private keys and salt (FR-SDK12) \

Usage: 4

_**FR-SDK11.** The SDK must be able to decrypt all encrypted symmetric keys._

Input:
* a list of
    * document_id
    * encrypted_symmetric_key

Output:
* a list of
    * document_id
    * decrypted_symmetric_key

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 8b

_**FR-SDK12.** The SDK must be able to encrypt the user's private keys and upload it to blindnet._

Inputs:
* symmetric_key
* private_key
* key_derivation_salt

The SDK encrypts the private_key with a symmetric_key, and uploads the encrypted key and salt to blindnet in a request containing (FR-BE09):
* JWT
* encrypted_private_encryption_key
* encrypted_private_signing_key
* public key
* key_derivation_salt

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 4c

_**FR-SDK13.** The SDK must be able to give access to all documents to a new user._

This is a functionality that must be directly exposed to developers that use the SDK. 

Input:
* JWT
* a list of document_id - optional, omit if we want all the documents
* new_user_id

Functionality workflow:
* SDK fetches all encrypted symmetric keys of a user (admin, JWT)  for the provided documents (or all documents if not provided) (FR-SDK14) and decrypts them (FR-SDK11)
* SDK fetches from blindnet a user’s PK (FR-SDK04)
* SDK verifies the public encryption key signature with the public signing key
* SDK encrypts all symmetric keys with the user’s PK and uploads them to blindnet (FR-SDK15, FR-BE10)

Usage: 8,9

**_FR-SDK14._** _The SDK must fetch the user's encrypted symmetric keys._

Input:
* JWT
* optional list of
    * document_id

Output:
* a list of
    * document_id
    * encrypted_symmetric_key

A request is sent to blindnet backend to retrieve the keys (FR-BE08).

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 8a

**FR-SDK15.** The SDK must be able to encrypt a set of symmetric keys and upload them to blindnet backend for a given user._

Inputs:
* public_key
* a list of
    * document_id
    * symmetric_key

The SDK encrypts each symmetric_key with a public_key, and uploads them to blindnet in a request containing (FR-BE10):
* JWT
* user_id
* a list of
    * document_id
    * encrypted_symmetric_key

This is a functionality that must not be directly exposed to developers that use the SDK.

Usage: 8d, 8e

### Backend SDK

_**FR-BESDK01.** The backend SDK must be able to generate a JWT._

Used to authenticate a user.

Input:
* user_id
* user_role
* app_id
* user_group_id
* client SK

Output:
* JWT as described in FR-G01

_**FR-BESDK02.** The backend SDK must be able to generate a short term JWT._

Used to authenticate a single operation from unauthenticated users.

Input:
* app_id
* user_group_id
* list of user_id (optional)
* client SK

The function randomly creates request_id to put into JWT.

Output:
* JWT as described in FR-G01

Useage: 2

_**FR-BESDK03.** The backend SDK must be able to generate a backend JWT._

Used to authenticate an operation from the HiJiffy backend.

Input:
* app_id
* client SK

Output:
* JWT as described in FR-G01

Useage: 5, 6, 7, 11

_**FR-BESDK04.** The BE SDK must be able to delete a given document reference._

Input:
* client JWT
* document_id

Usage: 5a

_**FR-BESDK05.** The backend SDK must be able to revoke access for a given user._

Revokes access to all the documents.

Input:
* client JWT
* user_id

Usage: 6a

_**FR-BESDK06.** The backend SDK must be able to delete a given user from blindnet._

Input:
* client JWT
* user_id

Usage: 7a

_**FR-BESDK07.** The backend SDK must be able to delete a given hotel from blindnet._

Input:
* client JWT
* hotel_id

Usage: 11a
