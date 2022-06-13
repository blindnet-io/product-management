# Privateform - Functional Requirements Document

This document describes functional requirements for the [PrivateForm](https://form.blindnet.io/).

-------------------------------------------------------------------------------------------------

## Glossary

_Server_ - PrivateForm Light backend server.

_Data Consumer_ - Registered user of the Server.

_Submitter_ - Unregistered user who fills and submits the forms sent by a Data Consumers.

_Interface_ - PrivateForm Light frontend (UI).

_Form_ - A form on the web page on PrivateForm Light where Submitters fill their data and Metadata.

_Data_ - Data about data subject, filled by Submitter on the Form 

Metadata - Data related to Submitters and data
* id
* names
* email
* datetime when a form is filled
* type of the filled form

-------------------------------------------------------------------------------------------------

## Background

PrivateForm is a web application for Data Consumers. It allows Data Consumers to securely collect data from their Submitters in an end-to-end encrypted workflow. Submitters access online forms where they answer a set of questions, after which the form is encrypted and sent to PrivateForm. There are two possible forms for Submitters to fill (COVID-19 and general medical form). 

Data Consumers have accounts on PrivateForm Light, where they can login, see and update all their Submitters’ data. For more details see interaction and design documents.

-------------------------------------------------------------------------------------------------

## Functional Requirements

This section describes functional requirements for the backend (FR-BExx) and frontend (FR-FExx).

_**FR-FE01.** The System must allow users to set up 2FA._

-------------------------------------------------------------------------------------------------

### Account creation and logging in

_**FR-FE01.** The Interface must allow a Data Consumer to create an account._

Account is created on the Interface in the following workflow:
* Step 1: A Data Consumer inserts name, email and a password
* Step 2: The Interface sends request to the Server to create a new account (FR-BE01)

_**FR-BE01.** The Server must be able to create a new account for a Data Consumer._
* Any Data Consumer must be freely available to create an account and use PrivateForm Light, without intervention from blindnet staff.
* Accounts are created only with Data Consumer’s email as input. After receiving a request, the Server generates an id (UUID) for a Data Consumer, and sends a verification link to the given email.
* The Title of the account (see FR-FE03) is set to have the value of Data Consumer’s name as given when registering.

_**FR-FE02.** The Interface must allow a Data Consumer to verify account creation._

Account is verified on the Interface in the following workflow:
* Step 1: A Data Consumer clicks on verification link in her email and is redirected to the Interface
* Step 2: A Data Consumer sets up a password
* Step 3: The Interface sends a verification request to the Server (FR-BE02)
* Step 4: The Interface connects a Data Consumer to blindnet
* Step 5: The Interface logs a Data Consumer in automatically and redirects her to a page for setting up her information

_**FR-BE02.** The Server must be able to verify account creation._
* The Server verifies account creation after a Data Consumer clicks the verification link in the email.
* Upon account verification the Data Consumer does not have any forms assigned to her account.

_**FR-FE03.** The Interface must allow a Data Consumer to set up her information._

A Data Consumer sets up her information in the following workflow:
* Step 1: A Data Consumer inserts her name, title, subtitle, contact information, and selects a logo
* Step 2: The Interface sends Data Consumer’s information to the Server (FR-BE03)

_**FR-BE03.** The Server must be able to store Data Consumer’s information._

The Server accepts Data Consumer’s information in the request containing:
* name
* title
* subtitle
* contact information
* logo

_**FR-FE04.** The Interface must allow a Data Consumer to log in._

A Data Consumer is logged in with the following workflow:
* Step 1: A Data Consumer inserts email and password
* Step 2: The Interface sends a login request to the Server (FR-BE04) and, if successful, connects the Data Consumer to blindnet 

_**FR-BE04.** The Server must be able to log a Data Consumer in._
* A Data Consumer is logged in by providing a username and password. If successfully authenticated, the Server returns a response containing:
    * Data Consumer id
    * a list of form links

_**FR-FE05.** The Interface must allow a Data Consumer to log out._
* When a Data Consumer logs out, the Server disconnects her from blindnet.

_**FR-FE06.** The Interface must allow a Data Consumer to update her information._

Same workflow as FR-FE03.

-------------------------------------------------------------------------------------------------

### Sending Forms

_**FR-FE07.** The Interface must show the Form links and allow a Data Consumer to copy the link of any of the Forms_
* By clicking a copy button
* By selecting the Form link with a mouse

_**FR-FE08.** The Interface must allow a Data Consumer to send a Form to a Submitter_

A Data Consumer sends a Form to a Submitter in the following workflow:
* Step 1: A Data Consumer checks the checkbox of a Form she wishes to send. It is possible to select multiple Forms.
* Step 2: A Data Consumer inputs an email of a Submitter
* Step 3: A Data Consumer clicks the send button and a request for emailing a Submitter is sent to the Server (FR-BE05)

_**FR-BE05.** The Server must be able to send emails with Form link to Submitters_

Input request contains:
* Data Consumer id
* form link
* Submitter email

Upon receiving the request the Server sends an email to the Submitter. Emails must not be stored nor logged.

_**FR-BE06.** The Server must allow blindet to customize emails through configurable templates._

-------------------------------------------------------------------------------------------------

### Filling and uploading the data

_**FR-FE09.** The Form must allow a Submitter to fill out the data and to submit it encrypted to a Data Consumer._

Forms are sent in the following workflow:
* Step 1: The Interface uses blindnet to encrypt the Metadata
* Step 2: The Interface uses blindnet to encrypt data
* Step 3: The Interface uploads the encrypted data and the encrypted Metadata to the Server (FR-BE07)

The Form page must work on mobile browsers.

_**FR-BE07.** The Server must be able to accept encrypted data._

The Server accepts the data in a request containing:
* Data Consumer id
*data id
* encrypted data
* metadata id
* encrypted metadata
* hashed Submitter email

FR-BE07-2. If a form contains files, the Form must send file IDs to a Server for it to store them.

-------------------------------------------------------------------------------------------------

### Resubmitting the data

_**FR-BE08** The Server must be able to accept duplicates of encrypted data._

When a Submitter with the same email fills a Form for the second time for the same Data Consumer, new data will be saved in addition to the old data (a Data Consumer will have two form data for the same Submitter).

-------------------------------------------------------------------------------------------------

### Reading and managing the data (related to Search)

_**FR-FE10.** The Interface must allow a Data Consumer to see all Submitters and their information (excluding the data)._

The Interface shows a table with Submitter information in the following workflow:
* Step 1: The Interface retrieves metadata of the Submitters from the Server (FR-BE09)
* Step 2: The Interface uses blindnet to decrypt retrieved Metadata
* Step 3: The Interface shows Metadata of retrieved Submitters in a table (including possible duplicate entries)

_**FR-BE09.** The Server must be able to retrieve Metadata of Submitters for a given Data Consumer after a given date._

If the date is not provided, all metadate is returned. 

The Server retrieves Metadata in a request containing:
* Data Consumer id
* date: optional

Response:
* an array of
    * metadata id
    * encrypted metadata
    *data id

_**FR-FE11.** The Interface must allow a Data Consumer to retrieve the data for a given Submitter, and to display it._

Data is retrieved and displayed in the following workflow:
* Step 1: The Interface sends a request to the Server (FR-BE10)
* Step 2: The Interface uses blindnet to decrypt the data
* Step 3: The Interface displays data to a Data Consumer

_**FR-BE10.** The Server must be able to retrieve the encrypted data._

The Server retrieves the data in a request containing:
* Data Consumer id
* medical data id

Response:
* encrypted data

_**FR-BE10-2.** The Server must be able to retrieve all encrypted data for a Data Consumer._

The Server retrieves the data in a request containing:
* Data Consumer id

Response:
* an array of
    * encrypted medical data

_**FR-BE10-3.** The Server must be able to retrieve all encrypted data for given ids._

The Server retrieves the data in a request containing:
* Data Consumer id
* an array of
    * form id

Response:
* an array of
    * encrypted medical data

_**FR-BE10-4.** The Server must be able to return a list of file IDs for a given form._

Input:
* form id

Output:
* list of
    * IDs of files submitted in a given form

-------------------------------------------------------------------------------------------------

### Deleting the data

_**FR-FE12.** The Interface must allow a Data Consumer to delete the data of a given Submitter_

Data is deleted in the following workflow:
* Step 1: The Data Consumer clicks a button to delete the data
* Step 2: The Interface sends a request to the Server to delete the data (FR-BE11)

_**FR-BE11.** The Server must be able to delete the encrypted data._

The Server deletes data and metadata in a request containing medical_data_id.

If the data contained files, the server must delete all files from Azure.

-------------------------------------------------------------------------------------------------

### Updating the data

_**FR-FE13.** The Interface must allow a Data Consumer to update the data of a Submitter_

After data is shown to a Data Consumer (FR-FE11), she must be able to make some changes. Data is updated in the following workflow:
* Step 1: The Interface accepts the input from a Data Consumer for data that needs to be updated
* Step 2: The Interface uses blindnet to encrypt the data
* Step 3: The Interface sends an update request to the Server (FR-BE12)

_**FR-BE12.** The Server must be able to update the encrypted data._

The Server updates the data in a request containing:
* Data Consumer id
* old medical data id
* new encrypted medical data
* new medical data id 

Response:
* Status (OK/error)

The Server deletes all data related to _old_medical_data_id_, and stores new encrypted medical data. The _new_medical_data_id _must be inserted in the corresponding metadata record, and the metadata record must update the medical data id with the _new_medical_data_id._

-------------------------------------------------------------------------------------------------

### GDPR compliance

-**FR-GDPR-01.** After filling a form and before final submission, the System must inform a Submitter about his data and ask for consent for each specific usage._

Figma ref: [4-1.0](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=113%3A38)

_**FR-GDPR-02.** The System must collect the user's email in each filled form._

User’s email is hashed on the client side, and the hash is stored in the backend and is associated with the filled form. Emails must never reach the backend in plaintext, unless they are used for emailing users and are deleted right away.

Figma ref: [4-1.0](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=113%3A38)

_**FR-GDPR-03.** The System must create a unique GDPR rights link for each Data Consumer._

The link must lead to a GDPR page which is associated with the Data Consumer, where a Submitter can make a GDPR related request to exercise his rights.

Figma ref: [4-1.7](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=227%3A257)

_**FR-GDPR-04.** The System must present a GDPR link to a Data Consumer on her GDPR page._

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=163%3A82)

_**FR-GDPR-05.** The confirmation page for submitted forms must include information about the GDPR rights. _

GDPR rights details include: 
* A unique GDPR rights link that a Submitter is able to copy. The link will lead to a GDPR demand page specific to the Data Consumer.
* Action buttons for creating a GDPR demand.

Figma ref: [4-1.1](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=227%3A196)

_**FR-GDPR-06.** After submitting a form, the System must send an email to a Submitter, including a unique link to the GDPR rights page for the Data Consumer._

_**FR-GDPR-07.** The System must keep track of all GDPR requests, and show them to the Data Consumer in a separate tab on the Interface._

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=163%3A82)

_**FR-GDPR-08.** The System must allow a Data Consumer to specify the form min lifetime for each of her individual form types._

The min lifetime means how long a Data Consumer must keep the data for regulatory compliance.

Figma ref : [GDPR personnalisation 1](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=324%3A186), [GDPR perso 2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=443%3A442), [GDPR perso 3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=443%3A594), [GDPR perso 4](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=489%3A330)

_**FR-GDPR-09.** The System must allow a Data Consumer to specify delete duration and automatically delete a submitted form after that duration expires._

If a Data Consumer sets a duration of X days, every form must be automatically deleted on the Xth day after it has been submitted. 

-------------------------------------------------------------------------------------------------

#### View

_**FR-GDPR-FE-01.** The Interface must allow a Submitter to submit a request to view his data._

The request must contain:
* Submitter’s full name
* Submitter’s email
* Password set by a Submitter
* Submitter’s ID Document 

Workflow for sending the _view_ request to the server:
* The Interface uses blindnet SDK to encrypt Submitter’s name and ID document
* The Interface uses blindnet SDK to hash a Submitter's email. 
* The Interface uses blindnet SDK to derive a public key based on a password of the Submitter, and obtains the request id.
* The Interface sends a request to the Server (FR-GDPR-BE-01)
    The interface presents a Submitter with a GDPR request link (see next FR)

Figma ref: [4-1.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=227%3A313)

_**FR-GDPR-BE-01.** The Server must accept the Submitter's request to view the data._

The request contains:
* Submitter’s encrypted name and ID document
* Submitter’s email hash
* Request id (previously obtained by blindnet SDK)

Each request must be assigned a unique id (not to be confused with blindnet request id) and its status must be maintained (created/treated).

For each request, a link is created for a Submitter where he could see the request status (FR-GDPR-BE-02). A confirmation email is sent to a Submitter, containing the request status link.

Figma ref: [4-1.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=154%3A166), 

_**FR-GDPR-BE-02.** The Server must create a request status link._

When a new request is submitted to the Server, the Server must create a unique link for that request. The link must show a page with the request status (pending/treated)

_**FR-GDPR-BE-03.** The Server must send a notification to a Data Consumer when a new GDPR request is received._

Notifications include:
* Email
* A visual mark on the “GDPR” tab on the PrivateForm. This visual mark must be present as long as there are unanswered GDPR requests.

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=163%3A82)

_**FR-GDPR-FE-02.** The Interface must list all GDPR requests for a Data Consumer._

Requests are listed under the “GDPR” tab. 

Requests are divided according to pending/treated status.

Requests are ordered by dates they are created, most recent ones being on top.

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=163%3A82), [4-2.2(2)](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=329%3A197)

_**FR-GDPR-FE-03** The Interface must allow a Data Consumer to see each individual GDPR view request that is pending._

A Data Consumer must be able to click a pending request and observe the details including:
* Information about the deadline. It will show the days remaining for addressing the request, calculated as the number of days until the 30th day after request submission.
* Submitter’s name
* Request type (view/modify/delete/other)
* A button to open Submitter’s ID Document
* List of concerned forms
* A text field for Data Consumer’s response

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=4%3A162), 

_**FR-GDPR-FE-04** The Interface must allow a Data Consumer to see each individual GDPR view request that has already been responded to._

A Data Consumer must be able to click a solved request and observe the details including:
* Date when the request was received
* Date when the request was responded to
* Submitter’s name
* Request type (view/modify/delete/other)
* Data Consumer’s response (accepted/rejected)
* A text field for Data Consumer’s response
* Optional for view request: date the user accessed the data

Figma ref: [4-2.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=242%3A1014)

_**FR-GDPR-FE-05.** The Interface must allow a Data Consumer to approve the GDPR view request._

Once a Data Consumer approves the request, the workflow is the following:
* The Interface uses blindnet SDK to encrypt the Submitter’s form(s), using blindnet id obtained when a Submitter created the request (FR-GDPR-FE-01). 
* The Interface uploads the encrypted forms to the Server (FR-GDPR-BE-04). At this point the Interface has access to the user's email locally, and passes it to the Server as well so that the Server can email the Submitter.

The Data Consumer must also be able to add a textual note to the response. If this is the case, the response note is encrypted for a Data Consumer and sent to a Server.

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=242%3A1094)

_**FR-GDPR-BE-04.** The Server must accept the encrypted forms for the Submitters to view as a part of the accepted GDPR view request._

Once the Server receives the data, it must create a unique link for data access, and email that link to a Submitter. The link is valid for one week and a Submitter can’t access it after that.

_**FR-GDPR-FE-06.** The Interface must allow a Submitter to view his data once his view request has been approved by a Data Consumer._

To view the data, the Submitter visits a GDPR view link that has been created for his request. The workflow is the following:
* The Submitter inserts a password
* The Interface uses blindnet SDK and the password to decrypt all the forms
* The Interface shows the forms to a Submitter
* The Interface informs the Server that the Submitter has accessed the forms and stores the date.

Viewing data is not possible after the request expires.

Figma ref: [4-1.5](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=227%3A549)

_**FR-GDPR-FE-07.** The Interface must allow a Submitter to request data modification or data deletion directly from his view request while he is viewing the data._

Once a Submitter is viewing the data, the Interface must allow him also to:
* Directly modify any form and submit the modification. In this case, a new _modify_ request is created for the Data Consumer (FR-GDPR-FE-10).
* Request for his forms to be deleted. In this case, a new _delete_ request is created for the Data Consumer (FR-GDPR-FE-15). This delete request is marked as approved right away.

Figma ref: [4-1.8](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=258%3A165), [4-1.6](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=338%3A275)

_**FR-GDPR-BE-05.** The Server must keep track of the last date the Submitter has viewed his forms after being granted the GDPR view request._

_**FR-GDPR-FE-08.** The Interface must allow a Submitter to download a PDF with his data while he is viewing the data in browser after his GDPR view request has been granted._

Figma ref: [4-1.8](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=258%3A165)

_**FR-GDPR-FE-09.** The Interface must allow a Data Consumer to reject the GDPR view request._

The Data Consumer must also be able to add a textual message to the response, which must be encrypted for a Submitter in the same way with blindnet SDK as the forms when the request is accepted (FR-GDPR-FE-05). This text field is mandatory for a rejection, since the Data Consumer must provide a reason.

The rejection message is encrypted for a Data Consumer and sent to the Server for storage and processing (FR-GDPR-BE-06).

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=4%3A162), [4-2.4](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=290%3A390)

_**FR-GDPR-BE-06.** The Server must accept the rejection of the GDPR view request._

Once the Server receives the data, it must create a unique link for the request response, and email that link to a Submitter informing him about the rejection. Submitter consumes Data Consumer’s response in the same way as he would consume the forms if the request was accepted (workflow in FR-GDPR-FE-06)

-------------------------------------------------------------------------------------------------

#### Modify

_The GDPR modify request workflows are the same as those for the view request. The difference is in the possibility for a Submitter to modify his data, and the option for the Data Consumer to manage modifications, as described in the FRs below._

_**FR-GDPR-FE-10.** The Interface must allow a Submitter to submit a modification request for each of his forms._

When a Submitter is browsing his form data after submitting a _modify_ request (to allow a Submitter to browse the data the same workflow as in view request is applied), he must be able to modify the data and save the modifications. Form modification is treated as a submission of the new form (FR-FE09, FR-BE07) to a Server with the addition of versioning (next FR). 

If an unsolved modification request already exists for the same form, the new request must be rejected and the user informed about it.

With each modification request, a status link is created and emailed to a Submitter (FR-GDPR-BE-02)

Figma ref: [4-1.9](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=365%3A579)

_**FR-GDPR-BE-07.** The Server must be able to receive form modifications made by a Submitter._

Form modification is in essence a new submitted form that is linked to the previous form. As a result, the Server now has the two different forms, and is able to connect them as one same form with different versions. This is done by using the same id for the two forms, while adding the _default_ flag to one of the forms:
* A Data Consumer browsing a modify request compares default version with the latest version
* If a Data Consumer accepts a modification, the last version becomes the default version
* If a Data Consumer is browsing a list with forms, he sees the default form in the list

With every modified form, add the id of the form parent, and the versioning date.

_**FR-GDPR-FE-11.** The Interface must allow a Data Consumer to see each individual GDPR modify request._

A Data Consumer must be able to click a pending request and observe the details including:
* Information about the deadline. It will show the days remaining for addressing the request, calculated as the number of days until the 30th day after request submission.
* Submitter’s name
* Request type (view/modify/delete/other)
* A button to open Submitter’s ID Document
* A button to observe the modifications. The Interface shows different versions of the forms to a Data Consumer so that the Data Consumer is able to compare the two forms.
* A text field for Data Consumer’s response

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A450)-1, [4-2.2-2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A604)

_**FR-GDPR-FE-12.** The Interface must allow a Data Consumer to accept the GDPR modify request._

Once a Data Consumer accepts the request, the workflow is the following:
* The form submitted as a modification is marked as the _default_ version of that form. As such, it is displayed in the Data Consumer’s forms under covid/history tab.
* The old version of the form is still stored for future references, but it is not listed under Data Consumer’s forms. It is available in the GDPR tab under treated requests.

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A696), [4-2.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=265%3A145)

_**FR-GDPR-FE-13.** The Interface must allow a Data Consumer to reject the GDPR modify request._

In this case, the old form is marked as the default one. The Submitter is informed about the decision, similarly as in the _view_ request (FR-GDPR-BE-06).

The Interface also provides a list of acceptable rejection motives to a Data Consumer.

Figma ref: [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A450) 1/4, [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A604) 2/4, [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A696) 3/4, [4-2.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=192%3A527) 4/4

_**FR-GDPR-FE-14.** The Interface must give a Data Consumer a note about an existing modification request if a Data Consumer wants to access a form that was modified but the request was not treated._

If a Data Consumer clicks on a form while browsing forms in the COVID/History tab, and if that form has been modified by the Submitter but the Data Consumer has not yet approved or rejected the modification, the Interface should show the old form together with a note that there is a new form and that the Data Consumer should take action.

-------------------------------------------------------------------------------------------------

#### Deletion

_**FR-GDPR-FE-15.** The Interface must allow a Submitter to submit a GDPR request for deleting his data._

The request must contain:
* Submitter’s full name
* Submitter’s email
* Submitter’s ID Document 
* Password set by a Submitter

The workflow is similar as in the _view_ request.

With each delete request, a status link is created and emailed to a Submitter (FR-GDPR-BE-02)

Figma ref: [4-1.2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=156%3A384)

_**FR-GDPR-BE-08.** The Server must accept the Submitter's request to delete his data._

The request contains:
* Submitter’s encrypted name and document ID
* Submitter’s email hash

Each request must be assigned a unique id and its status must be maintained (created/treated).

At this moment, the request is marked as _not-confirmed_ and the Data Consumer still can’t see anything.

An email with the confirmation link is sent to a Submitter.

_**FR-GDPR-BE-09.** The System must allow a Submitter to confirm the GDPR delete request._

Once a Submitter clicks the confirmation link in the email, the delete request is marked as _confirmed_. A link is created for a Submitter where he could see the request status. 

A confirmation email is sent to a Submitter, containing the request link.

Figma ref: [4-1.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=154%3A166)

_**FR-GDPR-FE-16.** The Interface must show to a Data Consumer only those delete requests that have been confirmed by a user (see previous FR, FR-GDPR-BE-09)._

_**FR-GDPR-FE-17.** The Interface must allow a Data Consumer to accept the GDPR delete request._

When viewing the request, the Data Consumer must be able to see the list of all Submitter’s forms. Each form must be clickable, and each list entry must contain: 
* Number of days since the form submission (x)
* Number of days until the date until which the form must be legally kept (y)(as configured by the Data Consumer, FR-GDPR-08). 
* A selection checkbox. By default the checkbox is selected if y = 0.

The page must also contain an action link for selecting all checkboxes.

The Data Consumer must be able to delete only the selected forms.

Figma ref:[ 4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=287%3A326) 1/6 , [4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=368%3A247) 2/6, [4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=460%3A195) 3/6, [4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=470%3A562) 4/6, [4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=462%3A217) 5/6, [4-2.2 DELETE](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=470%3A732) 6/6 

_**FR-GDPR-BE-10.** The System must delete selected Submitter’s forms once a Data Consumer approves the GDPR delete request._

When the Data Consumer accepts the deletion, Data Consumer’s textual response (if any) is encrypted for the Submitter (same as in other requests) and an email with a link is sent to a Submitter to inform him about the decision and provide him a way to see the Data Consumer’s response.

The Server deletes the form data and metadata (FR-BE11)

Figma ref: [4-1.10](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=376%3A516)

_**FR-GDPR-FE-18.** The Interface must allow a Data Consumer to reject the GDPR delete request._

The Interface must provide a list of acceptable rejection motives to a Data Consumer for her to be able to select them.

If a request is rejected, the Data Consumer’s response and relevant request data are sent to the Server for storage (encrypted for the Data Consumer). Also, the response is encrypted for the Submitter and the Submitter is informed by email.

Figma ref: [4-2.4](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=290%3A390)

_**FR-GDPR-FE-19.** The Interface must allow a Submitter to view Data Consumer’s response on the GDPR delete request once the request has been treated by the Data Consumer._

To view the response, the Submitter visits a GDPR link that has been created for his delete request. The workflow is the same as in the case of view (FR-GDPR-BE-06)

Figma ref: [4-1.10](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=376%3A516)

-------------------------------------------------------------------------------------------------

#### Other (GDPR)

_**FR-GDPR-FE-20.** The Interface must allow a Data Consumer to see already treated GDPR requests._**

The Interface will show to a Data Consumer for each individual request:
* Submitter’s name
* Request type (view/modify/delete/other)
* Submitter’s text (in the case of _other_ request type)
* Date the request has been made
* Request status (approved/rejected)
* Date the request has been responded
* Data Consumer’s message given when responding to the request, if any

Figma ref: [4-2.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=258%3A301)

_**FR-GDPR-FE-21.** The Interface must allow a Data Consumer to export a PDF with details of each GDPR request._

Details include request submission date, acceptance/rejected date, Submitter’s access date (if any), and a Data Consumer’s response (if any).

Figma ref: [4-2.3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=242%3A1014)

-------------------------------------------------------------------------------------------------

### Search

_**FR-SEARCH-FE-01.** The Interface must retrieve, decrypt, and store locally the metadata of all forms._

In order to perform the search over all forms, form metadata must first be decrypted and stored locally in the browser. 

_**FR-SEARCH-FE-02.** The interface must update the local copy of forms metadata everytime a forms page is opened by a Data Consumer._

In order to always have the latest data, every time a Data Consumer opens the forms page the Interface must check if there is any new metadata submitted after the timestamp of the last-submitted metadata in the local copy (see next FR).

_**FR-SEARCH-BE-01.** The Server must be able to retrieve all form metadata after a given datetime stamp._

_**FR-SEARCH-FE-03.** The Interface must allow a Data Consumer to filter all her forms._

The Interface must provide a user with a possibility to insert several different types of inputs in order to search for existing forms. These inputs include:
* Submitter full name (derived from the keyword-based search, see next FR)
* An email
* Time period (begin date and end date)
* Form type (a dropdown list of pre-filled values, see [Figma 3.5](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=27%3A562))

Figma ref: [3.1](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=44%3A43)

_**FR-SEARCH-FE-04.** The Interface must be able to search Submitter names/surnames based on the input keyword._

When a Data Consumer inputs a keyword related to name/surname, the Interface must return results in which:
* The input keyword is present in full or as part of either _nom_ or _prenom_ fields of the form, case insensitive. Example: searching for “Pierre” or “Pier” must return at least all forms that contain “Pierre” or “Jean-Pierre” in the _prenom_ field.
* The input keyword approximately matches either _nom_ or _prenom_ fields of the form, case insensitive. Example: searching “Clementine” or “Clementine” must return at least all forms that contain “Clémentine” in the _prenom_ field. For this task, a library such as [Fuse](https://github.com/krisk/fuse) can be used.

The results must consist only of Submitters’ full names (name + surname), and are presented in a drop down list for a Data Consumer to choose. Once chosen, the full name becomes an input in the form search.

Figma ref: [3.2](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=44%3A197)

_**FR-SEARCH-FE-05.** The Interface must be able to filter the forms_

Filtering is performed over all forms metadata that has previously been stored locally in the browser’s memory.

Depending on the input type, the results must be returned in the following way:
* Name: resulting forms must include all forms for which the full name on the form exactly matches the full name given in the query.
* Email: resulting forms must include all forms for which hashed email provided as input matches hashed email associated with the form.
* Time period: resulting forms must include all forms for which the submission date is later than _begin date_ (included) and earlier than _end date_ (included)
* Form type: resulting forms must include all forms for which the form type matches the type given as input. If multiple inputs are provided, the result is a union.

Figma ref: [3.3](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=27%3A136), [3.6](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=29%3A1379), [3.7](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=29%3A1189), [3.8](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=29%3A975)

_**FR-SEARCH-FE-06.** The Interface must allow a Data Consumer to freely add and remove filtering criteria._

After a filtering criterion is added/removed, the results must be updated.

Figma ref: [3.4](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=27%3A38), [3.5](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=27%3A562)

_**FR-SEARCH-FE-07.** The Interface must show the filtered forms to a Data Consumer._

The results is a list containing all the forms with:
* Submitter nom + Submitter Prenom
* Form type (e.g., covid, history)
* Form submission date
* A button for downloading the form to PDF

_**FR-SEARCH-FE-08.** The Interface must show a Data Consumer to order the results according to the form submission date._

Forms in the results must be orderable according to submission date, in ascending or descending order.

_**FR-SEARCH-FE-09.** The Interface must clear the form metadata from the browser after a Data Consumer logs out._

-------------------------------------------------------------------------------------------------

### Other

_**FR-FE19.** The Interface must allow a Data Consumer to download the data as a PDF file._

_**FR-FE20.** The Interface must be able to show both Data Consumer and Submitters the fingerprint of Data Consumer’s public key._

_**FF-FE21.** The Interface must support multiple languages._

The supported languages are currently French and English. A user must be able to change the UI language anytime.

Figma ref: [here](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=591%3A271)

_**FF-FE22.** The Interface must allow a Data Consumer to export all her data (i.e., forms) in a single action._

When a Data Consumer requests to export the data, all her forms are decrypted and downloaded to her local machine.

Figma ref: [3.1](https://www.figma.com/file/JT5Yq52CilZ7dVYchgGpJq/PF-SEARCH?node-id=44%3A43)

_**FF-FE23.** The Interface must allow a Data Consumer to delete her account._

Before deleting the count, the Data Consumer must confirm the deletion.

Figma ref: [1](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=567%3A221), [2](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=567%3A221), [3](https://www.figma.com/file/dkfknQnwNhCTGOMgIPjayx/PF-GDPR-Sketches?node-id=567%3A228)

_**FF-BE13.** The Server must be able to delete Data Consumer’s account._

Deleting an account implies deleting all Data Consumer’s data + all of her Submitters’ forms and medical data.

After an account is deleted, a confirmation email is sent to a Data Consumer.

-------------------------------------------------------------------------------------------------

## Password change workflow

Legend:
* Point of failure
* DB status

Prerequisite: Add another field in PF db, table User, column "NewPassword"

Change password workflow:
1. From the PF front-end, call the backend to change the password. If all validations pass on the backend, insert the new password into the "NewPassword" column, else do nothing. Send a response to the front.
2. Depending on the response from the backend:
    - a. If it’s 200, call blindnet SDK to change the password. At this point, the new password is in the "NewPassword'' field.
    - b. If other than 200, show the message that the password update failed. Do not continue further steps.
3. When (2a) is executed, depending on the result from blindnet SDK:
    - a. If it’s an exception, show the message that the password update failed. Do not continue further steps. At this point, the correct password is still in the “Password” field.
    - b. If it’s a success, show the message that password change was successful and asynchronously call the PF backend to copy the "NewPassword" value to the "Password" field and set "NewPassword" field to null. At this point, the password has been updated, the new password is either in the “Password” or “NewPassword” field (depending if the 3b backend call was successful).

User login workflow: call PF backend and try to regularly login a user by looking at the “Password” column (this is instructed by the front-end so that the front knows which pass field is checked; this is needed so that the front is able to distinguish between 1b and 2bii): 
1. If it’s a success, create a token and connect to blindnet at the front-end 
    - a. If the SDK fails, that means step 3b failed. Show the wrong password message.
    - b. If the SDK successfully connects, this means either step 2a failed or there wasn’t a change of password, or that there was a successful change of password. Log in the user.
2. If it’s a failure, return an error to the front-end and then call the server to log in the user by looking at the “NewPassword” field.
    - a. If it’s a failure or, it means that the password a user entered is completely wrong. Reject the login.
    - b. If it’s a success, create a token and connect to blindnet at the front-end
        - i. If the SDK throws an error, that means step 2a failed. Show an error about the wrong password and call the server to set the “NewPassword” to NULL. 
        - ii. If SDK successfully connects, that means step 3b failed. Log in the user. Asynchronously call the server to copy the “NewPassword” value into “Password” and set NewPassword to NULL.

-------------------------------------------------------------------------------------------------

## Privateform GDPR workflows

1. Submitter requests to exercise his GDPR rights
    - a. A token is created in the server SDK with a random request id ([user JWT](https://docs.google.com/document/d/1p4z2UE6Rk_3IEcz2xjQvqZXZacID-OLutkF17agHUVQ/edit#heading=h.mfn7thdg81vw)) and passed to FE. Request id is stored in a dedicated db table.
    - b. Submitter chooses the GDPR action
    - c. Submitter inserts password and other data on the FE
    - d. SDK:
        - i. Connects a user to the blindnet using request id as user id (FR-SDK03)
    - e. SDK encrypts the request for a Data Consumer (FR-SDK05, FR-SDK05-2)
    - f. FE sends the encrypted GDPR request and blindnet req id to the BE
    - g. User receives an email with a link https://form.blindnet.io/gdpr/request_id
2. Data Consumer approves the GDPR request to view or modify the data
    - a. FE retrieves the encrypted forms based on user’s email address, the encrypted GDPR req, and blindet req id from the BE 
    - b. SDK decrypts user forms for a Data Consumer
    - c. SDK decrypts the GDPR request for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - d. Data Consumer approves/rejects a req and gives an optional text (FR-SDK08, FR-SDK08-2)
    - e. If rejected:
        - i. SDK:
            - 1. Encrypts the answer for the Submitter (user id = request id) (FR-SDK05, FR-SDK05-2)
            - 2. Encrypts the answer for Data Consumer (FR-SDK05, FR-SDK05-2)
        - ii. FE stores answer ids, encrypted answers and rejection flag in dedicated db tables
    - f. If accepted:
        - i. SDK:
            - 1. Encrypts the forms for a Submitter (user id = request id). All forms are bundled and encrypted together. FE form id must be included with every form.
            - 2. Encrypts Data Consumer’s answer for a Submitter (FR-SDK05, FR-SDK05-2)
            - 3. Encrypts the answer for a Data Consumer (FR-SDK05, FR-SDK05-2)
        - ii. FE stores the encrypted form(s) for a Submitter and Data Consumer’s encrypted answers in dedicated db tables
3. Data Consumer approves the GDPR request to delete the data
    - a. FE retrieves the encrypted forms, the encrypted GDPR req, and blindet req id from the BE based on user’s email address
    - b. SDK decrypts user forms for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - c. SDK decrypts the GDPR request for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - d. Data Consumer approves/rejects a req and gives an optional text
    - e. When accepted/rejected:
        - i. SDK:
            - 1. Encrypts the answer for the Submitter (user id = request id) (FR-SDK05, FR-SDK05-2)
            - 2. Encrypts the answer for himself (FR-SDK05, FR-SDK05-2)
        - ii. FE stores answer ids, encrypted answers and rejection flag in dedicated db tables
    - f. FE stores the encrypted answers in dedicated db tables
4. Submitter receives a rejected/accepted response
    - a. Submitter receives an email and opens https://form.blindnet.io/gdpr/request_id
    - b. Submitter inserts a pass and connects to blindnet SDK (FR-SDK03-2)
    - c. FE gets encrypted Data Consumer’s answer
    - d. SDK decrypts the Data Consumer’s answer (FR-SDK08, FR-SDK08-2)
    - e. FE shows the Data Consumer’s answer to a Submitter
5. Submitter views the data
    - a. Submitter receives an email and opens https://form.blindnet.io/gdpr/request_id
    - b. Submitter inserts a pass and connects to blindnet SDK (FR-SDK03-2)
    - c. FE gets encrypted forms for a user and Data Consumer’s text
    - d. SDK:
        - i. Decrypts the forms (FR-SDK08, FR-SDK08-2)
        - ii. Decrypts the Data Consumer’s answer (FR-SDK08, FR-SDK08-2)
    - e. FE shows the form(s) and Data Consumer’s answer to a Submitter
6. Submitter modifies the data
    - a. Submitter views the data (same workflow as view)
    - b. Submitter inserts modifications
    - c. FE submits a new form (same workflow as currently on PrivateForm for form submissions) for each modified form, but must include the form id so the server can link it to the original form.
7. Data Consumer approves modifications
    - a. FE retrieves the encrypted modified forms, encrypted original forms, the encrypted GDPR req, and blindet req id from the BE based on user’s email address
    - b. SDK decrypts modified forms for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - c. SDK decrypts original forms for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - d. SDK decrypts the GDPR request for a Data Consumer (FR-SDK08, FR-SDK08-2)
    - e. Data Consumer is able to verify the modifications on every form
    - f. When accepted/rejected:
        - i. SDK:
            - 1. Encrypts the answer for the Submitter (user id = request id) (FR-SDK05, FR-SDK05-2)
            - 2. Encrypts the answer for himself (uses different token, Data Consumer’s token) (FR-SDK05, FR-SDK05-2)
    - g. Data Consumer approves or rejects the modifications
    - h. If approved, the modified forms will become default in the db
    - i. User receives an email
8. Submitter receives an email
    - a. When accepted/rejected:
        - i. Submitter opens [https://form.blindnet.io/gdpr/request_id](https://form.blindnet.io/gdpr/request_id)
        - ii. Submitter inserts a pass and connects to blindnet SDK
        - iii. FE gets encrypted Data Consumer’s answer
    - b. SDK:
        - i. Decrypts the Data Consumer’s answer (FR-SDK08, FR-SDK08-2)
    - c. FE shows the Data Consumer’s answer to a Submitter
