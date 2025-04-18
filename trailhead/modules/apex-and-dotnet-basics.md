# Apex & .NET Basics

🔗Source: [Apex & .NET Basics Trailhead module](https://trailhead.salesforce.com/content/learn/modules/apex_basics_dotnet?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)

Discover the basics of Apex and its similarities to programming with .NET.


## Objectives

- Understand which key features make up the Lightning Platform and the Apex programming language
- Identify similarities and differences between .NET and the Lightning Platform
- Use Developer COnsole to create your first Apex class
- Use Anonymous Apex to invoke a method from an Apex class

## Key Takeaways 🧠

- [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)
- [Understand Execution Context](#2-understand-execution-context)
- [Use Asynchronous Apex](#3-use-asynchronous-apex)
- [Debug and Run Diagnostics](#4-debug-and-run-diagnostics)


## 1. Map .NET Concepts to the Lightning Platform

### 1. 1. Platform Basics

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

**Lightning Platform**

- Metadata-driven architecture
	- Code is metadata
	- Configuration is metadata
	- Apps are metadata
- Tightly integrated with the database
- User interface is built-in
- Security is built-in
- Reporting is built-in
- Platform-as-a-Service cloud model
	- No provisioning required
	- No infra/software maintenance required
	- Developer is only responsible for developing and deploying

### 1. 2. Apex Basics

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

- Declarative development (or "point-and-click" app building)
- Code is not always needed

[From article [Visual Development - When to Click Instead of Write Code](https://developer.salesforce.com/blogs/engineering/2014/12/forcedotcom-declarative-development)]

Things to consider prior to writing code:

- How much and how long would it take?
- Who's maintaing the code?
- Limits
	- Execution governor limits don't apply for declarative customizations
		- Total number of SOQL queries issued
	- Design limits apply for declarative customizations
		- Total number of workflow rules on an object
- Updating
	- Declarative features are updated automatically (by Salesforce releases)
	- Apex code requires revisions for adopting or fitting new features
- Usability and User Productivity
	- Using standard pages can keep usability more consistent
	- Custom pages lose changing the page layout with the Page Layout Editor
	- Custom pages lose inline editing capabilities in list views

Examples for Declarative Devlopment versus Code

- Instead of using triggers to update field values, automate Field Updates using Workflow
- Instead of calculating field values in a controller extension, use Formula Fields and Roll-Up Summary Fields for field calculations
- Instead of using triggers to enforce business rules, use Validation Rules
- Instead of implementing logic and process in Apex, use Approval Processes and Flows
- Instead of writing Custom Objects, search for Standard Objects first


### 1. 3. What is Similar?

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

Apex programming language
- Objected-oriented
- Saved in the Lightning Platform
- Compiled in the Lightning Platform
- Executed in the Lightning Platform

#### 1. 3. 1. Object Oriented Design

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform): [What is Similar?](#1-3-what-is-similar)

Apex is object-oriented.
- Supports object-oriented principles:
	- Encapsulation
	- Abstraction
	- Inheritance
	- Polymorphism
- Includes familiar language constructs:
	- Classes
	- Interfaces
	- Properties
	- Collections
- Uses familiar syntax when defining classes
	- Modifiers:
		- Access Modifiers
			- `private`
			- `protected`
			- `public`
			- `global`
		- Virtual Modifier:
			- `virtual`
		- Abstract Modifier:
			- `abstract`
	- Inheritance:
		- `extends ClassName`
	- Composition:
		- `implements InterfaceNameList`

#### 1. 3. 2. Data Types

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform): [What is Similar?](#1-3-what-is-similar)

Apex Data Types

- Primitive Types
	- Familiar primitive types
		- Integer
		- Double
		- Long
		- Date
		- DateTime
		- String
		- Boolean
	- New primitive types
		- ID
- Value and Reference Types
	- Work the same
	- In Apex, all variables are initilized to `null` by default


#### 1. 3. 3. ASP.NET to Visualforce

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform): [What is Similar?](#1-3-what-is-similar)


## 2. Understand Execution Context


## 3. Use Asynchronous Apex


## 4. Debug and Run Diagnostics