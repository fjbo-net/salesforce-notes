# Apex & .NET Basics

🔗Source: [Apex & .NET Basics Trailhead module](https://trailhead.salesforce.com/content/learn/modules/apex_basics_dotnet?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)

Discover the basics of Apex and its similarities to programming with .NET.


## Objectives

- Understand which key features make up the Lightning Platform and the Apex programming language
- Identify similarities and differences between .NET and the Lightning Platform
- Use Developer Console to create your first Apex class
- Use Anonymous Apex to invoke a method from an Apex class

## Key Takeaways 🧠

- [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

	- [Platform Basics](#1-1-platform-basics)
		- Everything is defined as metadata
		- Tightly integrated with the database	
			- Database define objects and properties
			- Built-in security and reporting
		- Platform-as-a-Service cloud model

	- [Apex Basics](#1-2-apex-basics)
		- Mostly declarative development
		- Code is not always needed

	- [What is Similar?](#1-3-what-is-similar)
		- [Object-oriented design](#1-3-1-object-oriented-design)
		- [Data Types](#1-3-2-data-types)
		- ASP.NET to Visualforce
			- Separation between markup and code
			- Property mapping
			- MVC paradigm

	- [What is Different?](#1-4-what-is-different)
		- Apex is case insensitive
		- Database objects are automatically represented in code
		- Design patterns are different
		- 75% test coverage is required for production deployment
		- No solution, project or config files
		- Less capable out-of-the-box class library
		- Lightning Platform is component-based

	- [Development Tools](#1-5-development-tools)
		- Developer Console (Salesforce web UI)
		- Visual Studio Code Extensions
		- Salesforce CLI

	- [Handling Security](#1-6-handling-security)
		- Identity is handled by the platform
		- Access is granular
		- Security is declarative

	- [What About Integration?](#1-6-handling-security)
		- SOAP and REST integration in both directions
		- Uses Apex for both exposing and consuming data

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
- Enums
	- Apex support enums, but you can't define the ordinal (number) values
- Familiar collections
	- List
		- An ordered collection of elements
		
		- Syntax:
			 
			``` apex
			List<String> myStrings =  new List<String> {'String1', 'String2', 'String3' };
			```
	- Set
		- An unordered collection of elements that does not contain duplicates.
		- Syntax:
			
			``` apex
			Set<ID> accountIds = new Set<ID>{'001d000000BOaHSAA1','001d000000BOaHTAA1'};
			List<Account> accounts = [SELECT Name FROM Account WHERE Id IN :accountIds];
			```
	- Map
		- Collection of key-value pairs.
		
		- Syntax:

			``` apex
			Map<Id, Account> accountMap = new Map<Id, Account>([SELECT Id, Name FROM Account]);
			```


#### 1. 3. 3. ASP.NET to Visualforce

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform): [What is Similar?](#1-3-what-is-similar)

Visualforce is similar to ASP.NET Web Forms

- Clear separation between markup and code
- Mapping code to properties defined in the controller
- Both use the Model-View-Controller paradigm
- State view is just as painful due to the stateless nature of HTTP

### 1. 4. What is Different?

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

Despite similarities with .NET, they are different.

- Apex is NOT case sensitive
- Apex and database are tightly coupled
	- All database tables automatically create a code representation
	- Changes to the database automatically update object definitions (and properties)
- Different design patterns
- Unit tests are required
	- 75% test coverage is required for deploying Apex code to a production org
- No solution, project, or config files
	- All code resides and executes in the cloud
	- The closest concept to a solution or project file is a Lightning Platform application (a loose collection of components and pages)
	- No need for connection strings or connections to a database
	- No route configuration
	- No config file
- A much smaller class library
- Lightning is component-based

### 1. 5. Development Tools

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

- Developer Console
	- Used for:
		- Edit source code
		- Navigate source code
		- Debugging code
		- Troubleshooting
		- Executing SOQL queries
		- View (SOQL) query plans
- Visual Studio Code
	- Has extensions for custom development
- Salesforce CLI


### 1. 6. Handling Security

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

- Identity is handled by the platform
	- No need for authentication procedures
	- No need for storing passwords
	- No need for connection strings
- Access is granular
	- Different permission levels
		- Object-level
		- Record-level
		- Field-level
- Security is declarative
	- Usually defined and configured by a *Saleseforce Administrator*

### 1. 7. What About Integration?

&uarr; [Map .NET Concepts to the Lightning Platform](#1-map-net-concepts-to-the-lightning-platform)

- SOAP and REST integration in both directions
- Create/expose web services in Apex
- Invoke external web services from Apex
- React to incoming emails, send outbound messages
- SOAP and REST APIs for direct data access
- API toolkits for various languages:
	- .NET, Java, PHP, Objective C, Ruby, JavaScript
- Third-party integration via AppExchange


## 2. Understand Execution Context


## 3. Use Asynchronous Apex


## 4. Debug and Run Diagnostics