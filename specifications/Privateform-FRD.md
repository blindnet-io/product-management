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
