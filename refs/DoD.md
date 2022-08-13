# Definition of Done

This document delivers a list of criteria that has to be met before any development on a blindnet project can be considered done.

Any task, issue or pull request updating our code base will NOT be considered to be complete until all these items can be checked off.

> **Note**
>
> Some development (i.e. merging a PR or, in the worst case scenario, directly pushing some commits to a `main` or `develop` branch) CAN still occur without checking all the following items.
>
> YET, we won't consider such development "done" (and therefor to solve any actual problems) until these items as been checked off.
>
> **NO** issue should be closed until we made sure the following criteria are met.

## Issue tracking

- [ ] All related new features, enhancements and bugs fixes can be associated with a GitHub issue(s).
  - [ ] Each issue has a clear description of the associate problem we intend to solve.
  - [ ] Issue number is included in the commit messages or PR description for traceability, using if possible the `close` keyword to automatically close the issue once the change is merged.

## Commits and Pull Requests

- [ ] All commits message correctly follow the project Commit Message Guidelines.
- [ ] A Pull Request has been created.
  - [ ] The Pull Request description is clear and descriptive.
    - [ ] It describes (or refer to the issue describing) the problems the PR intent to solve.
    - [ ] It describes the reasons behind any unobvious implementation choice.

## Tests

- [ ] sufficient test coverage (above 80% - goal: 100%)
  - [ ] Each modified code and behavior is covered by a passing unit test with a clear and meaningful description.
- [ ] All tests pass.
  - [ ] All pre-existing unit tests have been updated to reflect the changes and pass.

## Documentation

- [ ] The developer documentation has been completed as necessary.
  - [ ] All public APIs additions and changes are documented using the documentation generator(s) associated with the project (e.g. jsdoc, javadoc, storybook)
  - [ ] Moderately complex internal APIs or implementation details are documented using comments close to the related code.
  - [ ] Highly complex and structuring implementations details or architectural choices have been discussed and recorded in an Architectural Decision Record in accordance with the [blindnet decision framework](https://github.com/blindnet-io/openness-framework/tree/main/DecisionFramework)
- [ ] Documentation is up-to-date.
  - [ ] _IF the PR changes any dev tools, code structure or convention THEN_ the CONTRIBUTING guides have been updated.
  - [ ] _IF the PR changes any information in the README file THEN_ the README file has been updated.
  - [ ] _IF the PR changes the public API or any related description THEN_ any associated tutorial or guide has been updated.
  - [ ] Changes and additions follows the associated specifications and reference documents.
    - [ ] _IF a discussion leaded to a decision in contradiction with pre-existing specifications or reference documents THEN_ any associated specification or reference documents has been updated in accordance with the [blindnet decision framework](https://github.com/blindnet-io/openness-framework/tree/main/DecisionFramework) and [specification policy](https://github.com/blindnet-io/product-management/blob/main/specifications/README.md).
