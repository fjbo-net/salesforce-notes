# Application Integration Patterns for Saleforce Ligthning Platform

🔗Source: [Salesforce Integration Patterns Modules](https://trailhead.salesforce.com/content/learn/modules/app-integration-patterns?trail_id=explore-integration-patterns-and-practices&trailmix_creator_id=strailhead&trailmix_slug=architect-integration-architecture)

## Objectives
- Describe what an integration pattern is
- Identify the different integration patterns
- Identify the three layers used to evaluate integration patterns
- Describe the two types of timing and why they are important

## Key Takeaways 🧠

- [Learn About Integration Patterns and Designs](#1-learn-about-integration-patterns-and-designs)
	- [Integration Patterns](#1-1-integration-patterns)
		- Systems as part of a solution
		- Proven way to solve integration problems
	- [Integration Types](#1-2-integration-types)
		- Application Integration
			- Extend functionality across systems
		- Data Integration
			- Data between two or more systems
		- Process Integration
			- Extends business processes
	- [Security Considerations](#1-3-security-considerations)
		- Solutions determine security requirements
	- [Salesforce Lightning Platform Integration Patterns](#1-4-salesforce-lightning-platform-integration-patterns)
		- Remote Process Invocation: Request and Reply
		- Remote Process Invocation: Fire and Forget
		- Batch Data Synchronization
		- Remote Call-In
		- Data Virtualization
		- High-Frequency Data Replication
		- Publish/Subscribe
- [Practice the Layer Approach](#2-practice-the-layer-approach)
	- []()


## 1. Learn About Integration Patterns and Designs

## 1. 1. Integration Patterns

&uarr; [Learn About Integration Patterns and Designs](#1-learn-about-integration-patterns-and-designs)

&nbsp;

**Integration Patterns**

- Identify how systems (including components and services) interact as part of an integration solution design
- Describe (or capture) a proven way to evaluate and solve integration problems without reinventing the wheel


## 1. 2. Integration Types

&uarr; [Learn About Integration Patterns and Designs](#1-learn-about-integration-patterns-and-designs)

&nbsp;

**Application Integration**
- Focuses on extending features and fucntionality across systems
- Including:
	- UI-triggered events
	- API integrations
	- Flows
	- Connectors

**Data Integration**
- Focuses on data integration between two or more systems
- Including:
	- Data Integrity
	- Data Governance
	- Data flow-design
	- Data migration

**Process Integration**
- Focuses on extending business processes and services across systems.
- Including:
	- Events that trigger activity from one system
	- Run transactions between two systems

## 1. 3. Security Considerations

&uarr; [Learn About Integration Patterns and Designs](#1-learn-about-integration-patterns-and-designs)

&nbsp;

- Security play an important role
- Every system design has security requirements
- Solutions determine the security requirements

## 1. 4. Salesforce Lightning Platform Integration Patterns

&uarr; [Learn About Integration Patterns and Designs](#1-learn-about-integration-patterns-and-designs)

&nbsp;

**Remote Process Invocation: Request and Reply**
- Salesforce invokes a process on a remote system
- Waits for a reply

**Remote Process Invocation: File and Forget**
- Salesforce invokes a process on a remote system
- Does not wait for a reply

**Batch Data Synchronization**
- When data is updated, updates are reflected in either systems
- Updates are applied in a batch manner

**Remote Call-In**
- Remote system creates, retrieves, updates or deletes data sotred in Lightning Platform

**Data Virtualization**
- Salesforce accesses external data in real time

**High-Frequency Data Replication**
- Source system asynchronously replicates data in near-real time at high scale

**Publish/Subscribe**
- Salesforce publishes an event (not specific to a consumer)
- Any number of subscribers (consumers) listen and process the events


## 2. Practice the Layer Approach

### 2. 1. The Layer Approach

&uarr; [Practice the Layer Approach](#2-practice-the-layer-approach)

#### 2. 1. 1. Dimensions

&uarr; [Practice the Layer Approach](#2-practice-the-layer-approach): [The Layer Approach](#2-1-the-layer-approach)

Each dimension represents criteria that helps understand which solution is best to solve an integration problem.

- **Layers**
	- Different types of tasks in a system
- **Volume**
	- Amount of data synched
	- Transformation activity between systems
- **Timing**
	- Either asynchro nous or synchronous
- **Direction**
	- Whether is:
		- From Salesforce (into another system)
		- (From another system) To Salesforce
		- Bidirectional

#### 2. 1. 2. Layers

&uarr; [Practice the Layer Approach](#2-practice-the-layer-approach): [The Layer Approach](#2-1-the-layer-approach)

**User Interface Layer**
- Focuses on user interactions with the system
- Layer interacts with the business process layer

**Business Process Layer**
- Includes data interaction, validation and processing data transactions
- Layer interacts with the data layer

**Data Layer**
- Maps and identifies the primary data source and connections to other segments of the system

#### 2. 1. 3. Layers in Salesforce Lightning Platform

&uarr; [Practice the Layer Approach](#2-practice-the-layer-approach): [The Layer Approach](#2-1-the-layer-approach)

| Lightning Platform Pattern | Layer |
|--|--|
| Remote Process Invocation-Request and Reply | Business logic |
| Remote Process Invocation-Fire and Forget | Business logic |
| Data Virtualization | Data |
| Remote Call-In | Business logic |
| Batch Data Synchronization | Data |
| High Frequency Data Replication | Data and UI |
| Publish/Subscribe | Data and Business Logic |

## 3. Evaluate an Integration Pattern
