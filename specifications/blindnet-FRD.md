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

_Input:_
* _one_time_JWT or JWT_

_Output:_
* _data_id_

_The system generates the data_id and stores it in the database._

_**FR-BEXX.** The system must accept and store the encrypted metadata._

_Input:_
* _one_time_JWT or JWT_
* _data_id_
* _metadata_

_Output:_
* _ok_

_The system verifies the data_id was created by the requesting user (uid or tid)._

_**FR-BEXX.** The system must be able to generate an upload link for a block for Azure blob storage._

_Input:_
* _one_time_JWT or JWT_
* _data_id_
* _block_size_

_Output:_
* _url_
* _authorization_header_
* _date_
* _block_id_

_The system checks if the block/total size is within the limit._

_The system generates and stores the block_id in the database (linked with data_id)._

_The system creates and signs the upload link and returns the parameters in the response._

_**FR-BEXX.** The system must be able to commit the file upload to Azure blob storage._

_Input:_
* _one_time_JWT or JWT_
* _data_id_
* _block_ids_

_Output:_ 
* _ok_

_The system checks if all the block_ids belong to the data_id, generates, signs and executes the request to the Azure blob storage._

_**FR-BEXX.** The system must be able to retrieve the encrypted metadata._

_storage._

_Input:_
* _JWT_
* _data_id_

_Output:_
* _encrypted_metadata_

_**FR-BEXX.$** The system must be able to create and sign the signed download link for GCP storage._

_Input:_
* _JWT_
* _data_id_

_Output:_ 
* _url_
* _authorization_header_
* _date_

_The system creates and signs the download link and returns the parameters in the response._

_**FR-BEXX.** The system must accept and store encrypted symmetric keys for data stored in the azure storage._

_Input:_
* _one_time_JWT or JWT_
* _data_id_
* _a list of:_
    * _encrypted_symmetric_key_
    * _user_id_

_Output:_
* _ok_

_Similar to BE06, only the document id is provided from the client side._

_The system checks if the data_id was created by the requesting user (uid or tid)._

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


