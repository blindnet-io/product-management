# Privateform - Functional Requirements Document

This document describes functional requirements for the [PrivateForm](https://form.blindnet.io/).

## Background

PrivateForm is a web application for doctors. It allows doctors to securely collect data from their patients in an end-to-end encrypted workflow. Patients access online forms where they answer a set of questions, after which the form is encrypted and sent to PrivateForm. There are two possible forms for patients to fill (COVID-19 and general medical form). 

Doctors have accounts on PrivateForm Light, where they can login, see and update all their patient’s data. For more details see interaction and design documents.

## Glossary

_Server_ - PrivateForm Light backend server.

_Doctor_ - Registered user of the Server.

_Patient_ - Unregistered user who fills and submits the forms sent by a Doctor.

_Interface_ - PrivateForm Light frontend (UI).

_Form_ - A form on the web page on PrivateForm Light where Patients fill their Medical data and Metadata.

Medical data - Healthcare related data about Patients, filled by Patients on the Form

Metadata - Data related to Patients and Medical data
* id
* names
* email
* datetime when a form is filled
* type of the filled form

## Functional Requirements

This section describes functional requirements for the backend (FR-BExx) and frontend (FR-FExx).

_**FR-FE01.** The System must allow users to set up 2FA._


### Account creation and logging in

_**FR-FE01.** The Interface must allow a Doctor to create an account._

Account is created on the Interface in the following workflow:
* Step 1: A Doctor inserts name, email and a password
* Step 2: The Interface sends request to the Server to create a new account (FR-BE01)

_**FR-BE01.** The Server must be able to create a new account for a Doctor._
* Any doctor must be freely available to create an account and use PrivateForm Light, without intervention from blindnet staff.
* Accounts are created only with Doctor’s email as input. After receiving a request, the Server generates an id (UUID) for a Doctor, and sends a verification link to the given email.
* The Title of the account (see FR-FE03) is set to have the value of Doctor’s name as given when registering.

_**FR-FE02.** The Interface must allow a Doctor to verify account creation._

Account is verified on the Interface in the following workflow:
* Step 1: A Doctor clicks on verification link in her email and is redirected to the Interface
* Step 2: A Doctor sets up a password
* Step 3: The Interface sends a verification request to the Server (FR-BE02)
* Step 4: The Interface connects a Doctor to blindnet
* Step 5: The Interface logs a Doctor in automatically and redirects her to a page for setting up her information

_**FR-BE02.** The Server must be able to verify account creation._
* The Server verifies account creation after a Doctor clicks the verification link in the email.
* Upon account verification the Doctor does not have any forms assigned to her account.

_**FR-FE03.** The Interface must allow a Doctor to set up her information._

A Doctor sets up her information in the following workflow:
* Step 1: A Doctor inserts her name, title, subtitle, contact information, and selects a logo
* Step 2: The Interface sends Doctor’s information to the Server (FR-BE03)

_**FR-BE03.** The Server must be able to store Doctor’s information._

The Server accepts Doctor’s information in the request containing:
* name
* title
* subtitle
* contact information
* logo

_**FR-FE04.** The Interface must allow a Doctor to log in._

A Doctor is logged in with the following workflow:
* Step 1: A doctor inserts email and password
* Step 2: The Interface sends a login request to the Server (FR-BE04) and, if successful, connects the Doctor to blindnet 

_**FR-BE04.** The Server must be able to log a Doctor in._
* A Doctor is logged in by providing a username and password. If successfully authenticated, the Server returns a response containing:
    * doctor id
    * a list of form links

_**FR-FE05.** The Interface must allow a Doctor to log out._
* When a Doctor logs out, the Server disconnects her from blindnet.

_**FR-FE06.** The Interface must allow a Doctor to update her information._

Same workflow as FR-FE03.

### Sending Forms

_**FR-FE07.** The Interface must show the Form links and allow a Doctor to copy the link of any of the Forms_
* By clicking a copy button
* By selecting the Form link with a mouse

_**FR-FE08.** The Interface must allow a Doctor to send a Form to a Patient_

A Doctor sends a Form to a Patient in the following workflow:
* Step 1: A Doctor checks the checkbox of a Form she wishes to send. It is possible to select multiple Forms.
* Step 2: A Doctor inputs an email of a Patient
* Step 3: A Doctor clicks the send button and a request for emailing a Patient is sent to the Server (FR-BE05)

_**FR-BE05.** The Server must be able to send emails with Form link to Patients_

Input request contains:
* doctor id
* form link
* patient email

Upon receiving the request the Server sends an email to the Patient. Emails must not be stored nor logged.

_**FR-BE06.** The Server must allow blindet to customize emails through configurable templates._

### Filling and uploading the data

_**FR-FE09.** The Form must allow a Patient to fill out the data and to submit it encrypted to a Doctor._

Forms are sent in the following workflow:
* Step 1: The Interface uses blindnet to encrypt the Metadata
* Step 2: The Interface uses blindnet to encrypt Medical data
* Step 3: The Interface uploads the encrypted Medical data and the encrypted Metadata to the Server (FR-BE07)

The Form page must work on mobile browsers.

_**FR-BE07.** The Server must be able to accept encrypted Medical data._

The Server accepts the Medical data in a request containing:
* doctor id
* medical data id
* encrypted medical data
* metadata id
* encrypted metadata
* hashed patient email

FR-BE07-2. If a form contains files, the Form must send file IDs to a Server for it to store them.

### Resubmitting the data

_**FR-BE08** The Server must be able to accept duplicates of encrypted Medical data._

When a Patient with the same email fills a Form for the second time for the same doctor, new data will be saved in addition to the old data (a Doctor will have two form data for the same patient).

### Reading and managing the data (related to Search)

_**FR-FE10.** The Interface must allow a Doctor to see all Patients and their information (excluding the Medical data)._

The Interface shows a table with patient information in the following workflow:
* Step 1: The Interface retrieves metadata of the Patients from the Server (FR-BE09)
* Step 2: The Interface uses blindnet to decrypt retrieved Metadata
* Step 3: The Interface shows Metadata of retrieved Patients in a table (including possible duplicate entries)

_**FR-BE09.** The Server must be able to retrieve Metadata of Patients for a given Doctor after a given date._

If the date is not provided, all metadate is returned. 

The Server retrieves Metadata in a request containing:
* doctor id
* date: optional

Response:
* an array of
    * metadata id
    * encrypted metadata
    * medical data id

_**FR-FE11.** The Interface must allow a Doctor to retrieve the Medical data for a given Patient, and to display it._

Medical data is retrieved and displayed in the following workflow:
* Step 1: The Interface sends a request to the Server (FR-BE10)
* Step 2: The Interface uses blindnet to decrypt the Medical data
* Step 3: The Interface displays Medical data to a Doctor

_**FR-BE10.** The Server must be able to retrieve the encrypted Medical data._

The Server retrieves the Medical data in a request containing:
* doctor id
* medical data id

Response:
* encrypted medical data

_**FR-BE10-2.** The Server must be able to retrieve all encrypted Medical data for a Doctor._

The Server retrieves the Medical data in a request containing:
* doctor id

Response:
* an array of
    * encrypted medical data

_**FR-BE10-3.** The Server must be able to retrieve all encrypted Medical data for given ids._

The Server retrieves the Medical data in a request containing:
* doctor id
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
    * IDs of files submitted in a given foformmr

### Deleting the data

_**FR-FE12.** The Interface must allow a Doctor to delete the Medical data of a given Patient_

Medical data is deleted in the following workflow:
* Step 1: The Doctor clicks a button to delete the data
* Step 2: The Interface sends a request to the Server to delete the data (FR-BE11)

_**FR-BE11.** The Server must be able to delete the encrypted Medical data._

The Server deletes Medical data and metadata in a request containing medical_data_id.

If the data contained files, the server must delete all files from Azure.


### Updating the data

_**FR-FE13.** The Interface must allow a Doctor to update the Medical data of a Patient_

After Medical data is shown to a Doctor (FR-FE11), she must be able to make some changes. Medical data is updated in the following workflow:
* Step 1: The Interface accepts the input from a Doctor for data that needs to be updated
* Step 2: The Interface uses blindnet to encrypt the Medical data
* Step 3: The Interface sends an update request to the Server (FR-BE12)

_**FR-BE12.** The Server must be able to update the encrypted Medical data._

The Server updates the Medical data in a request containing:
* doctor id
* old medical data id
* new encrypted medical data
* new medical data id 

Response:
* Status (OK/error)

The Server deletes all data related to _old_medical_data_id_, and stores new encrypted medical data. The _new_medical_data_id _must be inserted in the corresponding metadata record, and the metadata record must update the medical data id with the _new_medical_data_id._
