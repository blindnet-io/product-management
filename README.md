# Product Feedback

At blindnet we expect every team member, regardless of their role and competence, to test the products and provide feedback ranging from bug reports to feature or product ideas. 

## WHY

The product team welcomes feedback, and will treat it in a constructive, polemic manner, meaning that:

- Team members are encouraged to review other team members' submissions and engage in discussions in order to consider different options, and make the best design decisions. They might disagree without judging one another. 
- Leads to justifiable design decisions
- Maximizes the chances that the design choices made are objectively superior to the available alternatives.

## WHERE
The team members should provide feedback in this repository by creating a new [Github Issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue) for each new feedback (check the **Issues** tab on top of the page).

## HOW
All feedback must follow certain guidelines in order to be considered in the feedback process. The design team will disregard any feedback that fails to meet these guidelines in any way. All feedback must be:

- **Contextualised**. It must be clear in which context (on which interface element, website, app screen, in which particular situation under which circumstances) can/should the system behavior that is the subject of the feedback be observed. 
- **Precise**. Please be clear in your feedback about what is observed and what is desired behaviour.
- **Unambiguously testable**. The feedback must include a clear way to test whether the suggestion being the subject of feedback has been implemented or not. If the feedback concerns a bug, it must be easy to answer in a binary yes/no way whether the bug has been fixed or not. If the feedback concerns an improvement suggestion (or feature request) it must be easy to answer in a binary yes/no way whether the suggestions has been implemented or not (there can't be any room left for "yes but…")
- **Justified**. Unless reasons for the suggestion are obvious, the feedback's author should give reasons why he/she/it thinks the suggestion is a good idea.

Examples:

| uncontextualised | contextualised 
| ----------- | -----------
| Design looks strange on some resolutions | On the *blindnet website (homepage), on width 991-1099px*, the blindnet logo is partially off screen. 
| “Save” button does not have a spinner when clicked | “Save” button *on the page for creating the apps currently* does not have a spinner when clicked. A spinner should be put in place in order to let the user know that something is going on.


| imprecise | precise
| ----------- | -----------
| Keys are updated when clicked on “I'll generate my own keys” | Currently, keys are updated when clicked on “I'll generate my own keys”. Instead, the click should open the page for inserting a new public key. 


| ambiguous, non-testable | unambiguously testable
| ----------- | -----------
| On mobile screens, the page is cut at the bottom | On the blindnet website (homepage), on mobile screens, the buttons on the bottom of the page are not visible (require the user to scroll down), *they should be in sight when the page loads whatever the screen size*.


| unjustified | justified
| ----------- | -----------
| In Private Form (covid questionnaire), the content scrolls vertically. Everything should fit on the screen. | In Private Form (covid questionnaire), the content scrolls vertically. Since we use back/next “horizontal” navigation, *having both “horizontal” and “vertical” navigation loads a higher cognitive charge on the user and might confuse the user*. Every panel should fit vertically on one the screen .
| “Save” button does not have a spinner when clicked | “Save” button on the page for creating the apps currently does not have a spinner when clicked. *A spinner should be put in place in order to let the user know that something is going on*.


When creating a new Issue, in the right panel you must choose the project related to this new Issue (e.g., Dashboard, Website) and choose one of the following labels:

- <span style="color: #d73a4a;">Bug</span>, if your feedback is about something that is not working correctly 
- <span style="color: #0E8A16;">Feature</span>, if your feedback is suggesting completely new feature 
- <span style="color: #FBCA04;">Question</span>, if your feedback is actually a question about something that needs clarification
- <span style="color: #0052CC;">Suggestion</span>, if your feedback is about improving existing feature or behaviour 

What not to do:
- Do not specify milestones. Milestones serve for managing versions and project boards, and are specified by the technical team.
- Do not specify assignees.
