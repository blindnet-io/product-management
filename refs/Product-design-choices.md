# Product Design Choices

| Version    | 0.1        |
| ---------- | ---------- |
| **Update** | 2021-05-03 |

The purpose of this document (Product Design Choices) is to list particular UX choices made (according to the Design Principles) that should be generalized to all blindnet interfaces for consistency. While other solutions might still comply with the requirements of a suitable UX, those choices should be preferred and applied as solutions to typical interface situations, as a signature of blindnet experience.

## 1. Show Password rather than Repeat Password

There generally are two solutions to ensure that the user doesn't make a mistake while defining a password and unknowingly defines a (hidden) wrong password: (1) making the user type the password twice, or (2)  letting the user see the password.

Blindnet's interfaces let the user see the password and never ask to type the password again.

## 2. Avoid Modal Dialogs and Overlapping Forms

Modal dialogs (interface elements that block the user from using other interface controls until he/she/it has dealt with the modal dialog) are more and more commonly used to display GDPR consent forms or other alerts.

From a UX perspective, using modal dialogs is traditionally discouraged.
Modal dialogs are, in general, reserved for situations where stopping the user in his action is so crucial that it justifies interrupting him and forcing him to act upon the warning.

Traditionally, modal dialogues can be used with moderation (e.g. when the user closing an application risks losing all the work he made without saving a file). However, typical situations on a website (like displaying a cookie consent) are an example of situations where hiding a part of the interface with an overlapping warning is inappropriate.

Blindnet interfaces are made to avoid the use of overlapping interface elements whenever possible. The use of modal dialogs, and interface elements placed on top of each other, can be accepted, _if and only if the user is about to put himself or others in a vital danger, or is likely to suffer irreparable and highly damageable consequences of his intended actions._

In all other situations, no overlapping interface elements should be used.

## 3. Be Password Strength Policy Agnostic

A security system is only as secure as its secret. Yet, password strength can be achieved in many different ways. When blindnet’s software is used by other software systems, it can operate regardless of the particular password strength policies in place in those systems.

User-facing components of blindnet’s system prefer:
-	objective measures of Password Strength (such as Shannon entropy) over arbitrary constrains
-	length of passwords over complexity of passwords
-	to educate, inform and support various ways to reach password strength rather than impose a rigid set of constrains

## 4. Form fields validation should be done immediately after a field is filled

Form fields validation should be done immediately after a field is filled rather than after the form is submitted to reduce friction and user frustration.
The system should behave in the following way : 
- When a form is initialized, no field has an error
- After a field is focused for the first time, wait until a user finishes filling it in
- After the field is unfocused for the first time, validate it.
   - Validation passed: no decoration
   - Validation failed: error indicator*

*Error message should be under the field rather than in the right panel tooltip

- After the field is focused for the second time and onward, field validation runs on every value change so a user knows immediately when the value is acceptable
- Submitting the form validates all fields.
  - Validation passed: send a request to server
  - Validation failed: put an error indicator to every field with a bad value. From this point onward, all fields behave as if they were "focused" once
