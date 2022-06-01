# Product Design Principles

|  Version | 0.1 |
| -------- | --- |
| **Update** | 2021-05-03

The purpose of this document is to ensure the efficiency of the design process while imposing product qualities compatible with the company’s values.
The document defines principles to be used when designing the product.
It should inform all decisions to be made in the design process.

For this document, we distinguish:

The CLIENT - the company implementing Blindnet software in its software solutions. Also the implementing solution;

From the USER - the end-user of the CLIENT

## 1. Minimal Friction Principle

Any decision related to the product should be taken in such a way to allow the product to deliver its intended functionality while generating minimal friction.

This implies that product design options are considered in the following order:

FIRST: Options that have no implications to the client’s nor to the user’s workflow. If such options exist, then no other options are taken into consideration.

SECOND: Options that have no implications to the user’s workflow, but do have implications to the client’s software design, architecture and therefore workflow. 

THIRD: if and only if no option exists of FIRST and SECOND type, can options having an implication to the users’ workflow be considered.

## 2. Minimal Decision Principle

The user should not have to make choices regarding options or functionalities that are of no use to him. Ideally, the existence of functionalities and options should come to the user’s attention when and only when the user needs them.

## 3. Privacy UX Enforcement Principle

Any developer oriented product should always help 3rd-party developers and companies to continuously improve the UX of their product.

This implies that all final user facing parts of the devkit and associated products are built in such a way that they:

1. **always** enforce Privacy UX patterns, [Privacy-by-Design principles](https://en.wikipedia.org/wiki/Privacy_by_design#Foundational_principles), and ["Privacy-Enabled Connectedness" principles](./notion-of-privacy/notion-of-privacy.md#privacy-enabled-connectedness)
2. **always** discourage Deceptive Design "dark patterns" and Privacy UX / Privacy-by-Design antipatterns

No "technical reason" can be considered to justify any infringement to this rule.
