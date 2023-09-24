# Microservices
## 1. History of Microservices
This is result of problem with 2 architrcture paradiagms `Monolith` and `SOA`
### 1.1 `Monolith`
 - original art where all sw component are exected in single process
 - No distribution of any kind
 - Strong coupling between all classes
 - Implemented as Silo

 Example: We have 2 app `HR App` and `Purchasing App`. It works good but one day they need comunication each others to know some more inforation as what HR for that Purchasing. Monolith doesn't support for that, do not expose ways to share data functionality. It can be done but it's not easy

 `Pros`
 - Easier to design
 - Performance if we develop correcly (No network, no seriablization, no deserialization layers, all core in process) about theory it should faster than distributed systems

 `Problem`
 - All components must be developed using same development flatform
 - Future upgrade is a problem - need to upgrade the whole app
 - Inflexing Deployment - Always deploy for whole app -> cost and risk a lot
 - Infficient Compute Resources - accross all components - no ways to know the specific component need more resources.
 - Large and Complex code base - hard to maintain, a little change requires long process because impact to whole application so develop will try the best not to change anything and lead to system obsolete quite q2uickly


 ### 1.2 `Service Oriented Architecture (SOA)`

 SOA is about sharing and giving, sharing capabilities using a well-defined API
 - Fist cointed in 1998
 - Apps are services exposing functionality to outside world
 - Services expose metadata to declare their functionality
 - Usually implemented using SOAP and WSDL
 - Usually implemented with `ESB` - Enterprise Service Bus that were design to mediate between the client and services and between the services themselves - so ESB provides all the cross-cutting concerns as authentication, routing, validation, monitoring and more - look good on paper but turned out to be a huge problem

 Example - 2 App HR services and Purchase Services. 
 Thoese expose SOAP apis. Using that endpoint the services can comnunicate with each others. Client interacts `ESB` which comunicates with the services, `ESB` know the real target services and routers the request to appropriated services => `Client have no ideas about real services just know how to talk with ESB and it lead to some problems` 

`Pros`
- Sharing data & functionality
- Polyglot between Services

`Problems`
- ESB is one of main components and it can become bloated and expensive - It was built by IBM or Oracle - It's extremely expensive, complex from start
- ESB do anything, when a single piece of code tries to do everything it usally doesn't end well
- Difficuylt to maintain
- Lack of tooling - testing and deployment were manly manual processes and take a lot of time
- Take longer time to build a monolith

## 2. `Microservices Architecture`
- Has to be modular with simple API
- Term first appreared in 2011

`Characteristics of Microservices`
- Componentization via Services
- Organized Around Bussiness Capabilities
- Products not Projects
- Smart endpoints and Dump Pipes
- Decentralized Governance
- Decentralized Data Management
- Infastructure Automation
- Design for Failure
- Evolutionary Design

### 2.1 `Componentization via Services`
- Modular is always a good idea
- Components are the parts that together compose the software
- Modularity can be achieved using:
  - liberies - called directly within the process with pros is good performance -  there are no mediators bw our components
  - services - called by out-of-process mechanism (WebAPI, RCP)

In microservices we prefer using Services for componentization and not liberies
Just use liberties in the case that is a part of service and that is service itself

- Motivation
  - Independent deployment
  - Well defined interface

### 2.2. `Organized Around Business Capabilities`
- Every sevice is handled by a single team. responsible for all aspects -from UI -> DB so team have same goal, has holistic view of serices that is better in develop the app
(monolith can share responsible by horizontal from UI is a team to DB is another team)

Motivation
 - Quick development
 - Well-defined boundaries

### 2.3 `Products not Projects`

- In traditional projects, the goal is deliver a working code
- With microservices, the goal is deliver a working product
"You build it, you run it"

Motivation
- Increase customer's satisfaction
- Change developer's mindset

### 2.4 `Smart Endpoints and Dump Pipes`
- Microservice systems use "dumb pipes"- simple protocols
- Strive to use what the web already offers

Important notes:
 - Direct conenctions between services is not a good idea because when one of them change the endpoint all of them have to update
 - Better use discovery services or a gateway

Motivation
- Accelerate develop
- Make app easiser to maintain

### 2.5 `Decentralized Governance`
- Each team is fully responsible for it's service
- Enabled the loosely coupled nature of Microservices
- polyot flatform

### 2.6 `Decentralized Data Management`
- It service own database

Important notes
- This is most controversial atrribute of Miicroservices
- Raises problems such as distributed transaction, data duplication and more

Motivation
- Right tool for right task - having the right database is important
- Encourages isolation

### 2.7 `Infrastructure Automation`
Tooling greatly helps in deployment using
 - Automated Testing
 - Automated Deployment

### 2.8 `Infrastructure Automation`
- For Microservices automation is essential
- Short deployment cycles are a must
- Can't be done manually
- There are a lot of automation tools - Gitlab, Jenkins

Motivation
- Short deployment cycles

### 2.9 `Design for Failure`
- Microservices have lot of processes and a lot of network traffic.
- A lot can go wrong

=> The code must assume failure can happen and hanle it greacefully
=> Extensive logging and monitoring should be in place to catch the errors and raise alerts when they happen

### 2.10 `Evolutionary Design`
- The move to Microservives should be gradual
- No need to break everything apart
- Start small and upgrade each part separately

## 3. `Problems solbved`
- Single technology Platform
- Inflexible Deployment
- Inefficient Compute Resource
- Large and Complex in codebase
- Complicated and Expensive ESB
- Lack of tooling


## 4. `Designing Microservices Architechture`
- Designing should be methodical
- Do not rush into development - "plan more, code less"
- Critical to the success of system

The Architecture Process
- Understand the System's Requirements
- Understand the Non-Functional Requirements
- Map to Components
  - Mapping
  - Communication Patterns
- Select the Technology Stack
- Design the Architecture
- Write Architecture Document
- Support the team


`Dive deeper on Mapping the Components - most imprtant step in whole process`
- Determines how the system will look like in long run
- Once set - not easy to change => taken very seriously

=> This step will literally shape the system

What is it ?
- Defining the various componenets of the system
- Remembers: Components =  Services

Mapping should be based on
- `Bussiness requirements`
  - The collection of requiments arround a specific bussiness capability
- `Functional autonomy`
  - The maximun functionality that does not involve other bussiness requirements
- `Data Entities`
  - Services is designed around well specified data entities
- `Data autonomy`
  - Underlying data is an atomic unit
  - Service does not depend on data from other serices to function properly
  `Example`: Employee service that relies on Addresses service to return employee's data => this is a major sign that our architecture is not optimized, righ thing is to include the Addresses data in the Employees service => make service litle bit larger but alternative is much worse, we really need our services to be autonomous 

  We still have the relationship bw services - `one services can realate to data in other services as long as this relationship is done using ID of the entity and not the entity itseft`

![Example](images/mapping_component_example.png)








