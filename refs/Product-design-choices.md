# Product Design Choices

|  Version | 0.1 |
| -------- | --- |
| **Update** | 2021-07-13

The purpose of this document (Product Design Choices) is to list particular UX choices made (according to the Design Principles) that should be generalized to all blindnet interfaces for reasons of consistency. While other solutions might still comply with requirements of a suitable UX, those choices should be prefered, and applied as solutions to typical interface situations, as a signature of blindnet experience.

## 1. Show Password rather than Repeat Password

In order to ensure that the user, while defining a password, doesn't make a mistake and unknowingly defines a (hidden) wrong password, two major solutions have been generally used: making the user type the password twice, or letting the user see the password. blindnet interfaces let the user see the password and never ask to type the password again.

## 2. Avoid Modal Dialogs and Overlapping Forms

Modal dialogs (interface elements that block the user from using other interface controls until he/she/it has dealt with the modal dialog) are more and more commonly used to display GDPR consent forms or other alerts. However, their use, from a UX perspective, has traditionally been discouraged, and generally reserved to situations where stopping the user in his action is so crucial that it justifies interrupting him and forcing him to act upon the warning. 

Traditionally, modal dialogues can be used with moderation (e.g. when the user closing an application risks losing all the work he made without saving a file). However, typical situations on a website (like displaying a cookie consent) are an example of situations where hiding a part of the interface with an overlapping warning is inappropriate.

Blindnet interfaces are made to avoid the use of overlapping interface elements whenever possible. The use of modal dialogs, and interface elements placed on top of each other, can be accepted, _if and only if the user is about to put himself or others in a vital danger, or is likely to suffer irreparable and highly damageable consequences of his intended actions._

In all other situations, no overlapping interface elements should be used.
