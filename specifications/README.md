# Specification

The first step of building products at blindnet always includes specification writing. It helps not only us to rapidly build better products, but we hope it also helps others better understand how our products work.

<br />

> **Please report any issues or errors you find in the specification in this repository .**

There are two categories of specification, _product specification_ and _technical specification_.

## Product specification

Product specification defines the product from the end-user point of view, focusing on the problems it solves for the end-users. Two main parts of the product specification are user stories and interaction diagrams.

### User stories

User stories describe, in natural/informal language, atomic parts of a product (or feature) from the end-user perspective. They define end-users' expectations from the product, and the end-users' needs a product aims to fulfil. See [here](./user-stories/) for more details about user stories at blindnet.

### Interaction diagrams

Interaction diagrams capture different forms of interaction between a product and the users. These include:
- Activity diagrams, defining the product through user actions and activities.
- State machine diagrams, defining how the product behaves in relation to different user inputs.
- User interface sketches, defining the look of user-facing parts of the product.

## Technical specification

Technical specification defines the product from the implementational point of view. The main parts of technical specification are functional requirements, architecture, and design.

### Functional requirements

Functional requirements define functional aspects of the product and are captured in the functional requirements document (FRD). Each functional requirement defines one particular function a product needs to deliver, and is assigned a unique code identifier (e.g., FRD-BE01, FR-SDK14). 

### Architecture

Product architecture defines different components of the product structure and how they interact together in order to deliver specified functions. For example, the architecture document defines different SDKs, APIs and databases that, when put together, deliver promised functional aspects. 

### Design

Product design defines in detail the technical aspects of each architectural component of the product. It includes, for example, database models, or expected inputs/outputs of SDK functions and REST API routes. In some cases, like for example for REST API routes, the design is described together with the corresponding functional requirement. 


