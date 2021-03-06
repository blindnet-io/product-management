# User Stories

## What is a User Story

A User Story is a general explanation of a feature from the user's perspective in natural/informal language (not in a technical perspective).

A user story describes in one sentence:

- the user type
- what this user wants
- and why.

The objective of crafting User stories is to be able to rely on it to plan and implement new features and design.

## How to craft User Stories

### Personas

<span style="text-decoration:underline;">Amélie</span>, the client of our system (e.g. the dentist).

<span style="text-decoration:underline;">Jean-Pierre</span>, the user filling the form (e.g. the patient).

### Good Practices

- Put yourself in Amélie and Jean-Pierre shoes and imagine the goals they would like to achieve in PrivateForm for Amélie, while filling the forms for Jean-Pierre.
- Think of what would need Amélie while using PrivateForm and what would need Jean-Pierre while/after filling the form.
- Make sure no similar user story has been written already.
- Use the following structure : _<span style="text-decoration:underline;">As a</span>_ **[type of user]**, _<span style="text-decoration:underline;">I want to</span>_ **[the goal]** _<span style="text-decoration:underline;">because</span>_ **[the benefit, the reason]**
- Each User Story has a unique ID, in the following structure "US-XX-YY" where XX is the number of the section and YY is the number of the user story within that section
- Each User Story are consistent level 2 titles (e.g. ## US-01-01) as this will allow us to refer to them using an anchor link (automatically added by Github)

### New feature context

Follow the steps above when creating a group of user stories for a new feature context:

1. copy the [`US-NN-template.md`](./US-NN-template.md) template file in this directory 
2. give it a unique two-digits id and short title describing a clear context (e.g. `US-19-sign-in.md`)
3. indicate the status of the document for the group of US : 
    - `Draft`: unfinished group of US redaction (US doc "in progress")
    - `Proposed`: finished group of US redaction
    - `Accepted`: group of US doc reviewed and validated with @blindnet-io/engineering (therefore To Be Developed)
    - `In Development`: @blindnet-io/engineering started working on group of US
    - `Released`: group of US released in production environment
4. indicate the status of specific US :
    - `In Development`: @blindnet-io/engineering started working on the US
    - `Integrated`: US development merged and released in staging environment
    - `Tested`: US validated in staging environment
    - `Released`: US released in production environment
5. (optional) add links to the draft PRs integrating this US in the codebase
6.  write new user stories following the [good practices](#good-practices)

## Related documents

* [Privatefrom User Stories (google doc)](https://docs.google.com/document/d/1-_iVgamjIm0aH-txl2aVDIfSNRuwS-agKf74G1q1KRk/edit)
* [Product feature and planning for 2022 (google doc)](https://docs.google.com/document/d/1UJhyVTOyjICTlG5wFVYIlmJQ1s-1DWPsBbvq2kvLb8A/edit#heading=h.4qvql0srrn4)
* [Figma activity diagrams, state-machine diagrams and sketches (figma)](https://www.figma.com/files/project/44665172/PrivateFrom?fuid=1025053302751681674)
* [PF messages & e-mail wording (google doc)](https://docs.google.com/document/d/1fK0Pw-OkN1YLQ5rD1STdRzFk1mPNyTLjcYBKBLhirCc/edit#heading=h.9yvxtjspa6zs)
