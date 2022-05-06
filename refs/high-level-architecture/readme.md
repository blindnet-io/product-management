# HIGH-LEVEL ARCHITECTURE
| Version | Date      | Authors | Status      | Improvements welcome until |
|---------|-----------|---------|-------------|----------------------------|
| 0.0.1   | 2022-05-6 |@milstan | First Draft | 2022-05-27                 |

> This documents describes the high-level view of the context in which our product requirments exists and suggests a high-level structure of components of the product that can meet those requirements.

## OVERVIEW
<img width="1400" alt="HIGH-LEVEL ARCHITECTURE" src="./img/hla.png">

## FUNCTIONS

The system supports secure capture of data and management of Data Subejcts' rights throughout the data lifecycle. As such is needs to support the following functions:
- Capture
- Access
- Transfer
- Rights Management

## BRIDGE AND INTEROPERABILITY

TBD


## COMPONENTS

### Encryption Engine

The Encryption Engine is composed of SDKs and APIs allowing to encrypt and decrypt the data in the context of Data Captures.

### Storage

The Storage component allows to store the Data Captures. It can inteface with systems that don't have their own storage, but integrate the whole secure data capturing as a fully external workflow, only integrated at front-end level with their website or app. 

### Data Consumer Interface

The Data Consumer Interface component allows to display the content of data captures for the eyes of Data Consumers. It allso allows to input (and register) parameters related to data rights management, necessary for the operation of the Data Rights Computation Engine.

### Access Management

The Access Management component can work with external user identity management solutions. The component allows to define and modify the intended Data Consumers of a particular Data Capture. This component also provides functions allowing to support Data Consumers in situations of lost access.

### Data Rights Computation Engine

Data Rights Computation Engine is a components that client systems can run in order to interpret their rights to hold and treat a particular Data Capture at a particular point of time, as well as in order to respond to Data Subjects' Data Rights Requests.

This component is composed of:
- A Data Rights Compiler : that takes into account data rights parameters of a particular system (e.g. storage location, mandatory duration of data keeping, etc.); Legal Grounds; history of transmissions to other systems as well as Data Rights Requests in order to compute one or more actions that need to be performed by the system in order to repsect the user's data rights. Such actions may include (not limited to): data deletion, acceptance/denial of a Data Rights Requests, transmission of a Data Rights Requests to another system.
- A Data Rights Request Capture Interface : a standardized end-user interface that systems can (optionally) run to capture Data Rights Requests. A global Data Rights Request Capture Interface can be hosted on a popular URL to capture Data Rights Requests in a standardized format (Data Rights Request Schema) on behlaf of other systems.
- Parametrable API - allowing to set and modify system-spectific parameters related to data rights and compliance (e.g. storage location, mandatory duration of data keeping, legal bases of treatment etc.)

This engine works in a way inspired by [Digital Rights Management](https://en.wikipedia.org/wiki/Digital_rights_management).

### Schemas

In order for the system to support interoperability with other systems and solutions, the following schemas should be made (and data export/import implemented using them):
 - **Data Rights Request Schema** : to represent Data Rights Requests made by users and allow their transfer from system to system and enforcement of Data Subject's Rights across systems holding his/her/their data.
 - **Data Capture Schema** : to represent data captures and allow transfer of encrypted captured data across systems while maintaining the integrity of data and its intended usage by intended data consumers

## RELATED DOCUMENTS
- [High Level Conceptualization](https://github.com/blindnet-io/product-management/tree/master/refs/high-level-conceptualization)
- [Lexicon](https://github.com/blindnet-io/product-management/blob/master/refs/privateform-lexicon.csv)
- [Digital Rights Management](https://en.wikipedia.org/wiki/Digital_rights_management)
