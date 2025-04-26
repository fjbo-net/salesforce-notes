# Apex & .NET Basics

🔗Source: [Apex & .NET Basics Trailhead module](https://trailhead.salesforce.com/content/learn/modules/apex_basics_dotnet?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)

Discover the basics of Apex and its similarities to programming with .NET.


## Objectives

- Understand which key features make up the Lightning Platform and the Apex programming language
- Identify similarities and differences between .NET and the Lightning Platform
- Use Developer Console to create your first Apex class
- Use Anonymous Apex to invoke a method from an Apex class
- Know which methods to use to invoke Apex
- Write a trigger for a Salesforce object
- Observe how execution context works by executing code in Developer Console
- Understand how governor limits impact design patterns
- Understand the importance of working with bulk operations

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

	- [What Is Execution Context?](#2-1-what-is-execution-context)
		- Time between when code is executed and when it ends
		- Apex code isn't always the only code executing

		- [Methods of Invoking Apex](#2-1-1-methods-of-invoking-apex)
			- Database Trigger
			- Anonymous Apex
			- Asynchronous Apex
			- Web Services
			- Email Services
			- Visualforce or Lightning Pages

		- [Important Considerations](#2-1-2-important-considerations)
			- Declarative features can trigger actions within execution context
			- Apex executes in system context by default
				- Has access to all objects and fields
				- Ignores: Object permissions, field-level security and sharing rules
			- Keyword `with sharing` takes current user's rules into account

	- [Trigger Essentials](#2-2-trigger-essentials)
		- Execute programming logic before or after events to records
		- Trigger Events:
			- Insert: `before insert` and `after insert`
			- Update: `before update` and `after update`
			- Delete: `before delete` and `after delete`
			- Undelete: `after delete` only

		- [Best Practices](#2-2-2-best-practices)
			- Only use triggers when point-and-click automation tools cannot accomplish the task
			- Use Flow Builder for managing business logic without writing code when possible
			- Use only one trigger per object
			- Use context-specific handler methods within triggers to create logic-less triggers
	
	- [Examining the Execution Log](#2-4-examining-the-execution-log)
		- Everything between `EXECUTION_STARTED` and `EXECUTION_STARTED` is execution context
		- CODE_UNIT_STARTED events mark the start of specific code units
		- All code operates under the same execution context
		- Subject to the same set of governor limits

	- [Working with Limits](#2-5-working-with-limits)
		- Current Limits:
			- 100 SOQL queries (sync)
			- 150 DML statements (sync)
		- Limits tend to change with each major release

	- [Working in Bulk](#2-6-working-in-bulk)
		- Apex triggers can receive up to 200 records at once
		- If a trigger performs SOQL query or DML statement inside a loop, it can hit limits
		- "Bulkify" your code from the start

	- [Tell Me More](#2-7-tell-me-more)
		- Apex uses try-catch-finally block for exception handling
		- No application or session variables in Lightning Platform
		- Static variables only persist information within a single execution context
		- Working with limits involves many tradeoffs, especially for managed packages

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

Follow Along with *Trail Together*
- Video available at: https://play.vidyard.com/oWWzy6KQ8LEKfbGMskyhhR?second=998

### 2. 1. What Is Execution Context?

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Similar to application domain in ASP.NET
- Represents the time between when code is executed and when it ends
- Your Apex code isn't always the only code executing

#### 2. 1. 1. Methods of Invoking Apex

&uarr; [Understand Execution Context](#2-understand-execution-context): [What Is Execution Context](#2-1-what-is-execution-context)

- Database Trigger
	- Invoked for a specific event on a custom or standard object
- Anonymous Apex
	- Code snippets executed on the fly in Dev Console & other tools
- Asynchronous Apex
	- Occurs when executing a future or queueable Apex
	- Running a batch job
	- Scheduling Apex to run at a specified interval
- Web Services
	- Code exposed via SOAP or REST inbound or outbound web services
- Email Services
	- Code set up to process inbound or outbound email
- Visualforce or Lightning Pages
	- Controllers and components can execute Apex code
	- Can be triggered automatically or by user actions
	- Can be executed by Lightning processes and flows

#### 2. 1. 2. Important Considerations

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Declarative platform features can trigger actions within execution context
- Apex executes in system context by default
	- Has access to all objects and fields
	- Object permissions, field-level security, and sharing rules aren't applied
- You can use `with sharing` keyword to take current user's sharing rules into account

### 2. 2. Trigger Essentials

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Similar to SQL Server triggers
- Execute programming logic before or after events to records
- Trigger events:
	- before insert
	- before update
	- before delete
	- after insert
	- after update
	- after delete
	- after undelete

#### 2. 2. 1. Trigger Syntax

&uarr; [Understand Execution Context](#2-understand-execution-context): [Trigger Essentials](#2-2-trigger-essentials)

```
trigger TriggerName on ObjectName (trigger_events) {
	 // code_block
}
```

#### 2. 2. 2. Best Practices

&uarr; [Understand Execution Context](#2-understand-execution-context): [Trigger Essentials](#2-2-trigger-essentials)

- Only use triggers when point-and-click automation tools cannot accomplish the task
- Use Flow Builder for managing business logic without writing code when possible
- Use only one trigger per object
- Use context-specific handler methods within triggers to create logic-less triggers

### 2. 3. Mark Execution Context

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Walkthrough creating an Apex database trigger that creates an opportunity when a new account is entered

	1. Create an Apex Class

		1. From *Setup*, in User Menu, click on **Developer Console**

		2. In the *Developer Console*:
			1. At the top bar menu, click on **File**
			2. Click on **New**
			3. Click on **Apex Class**
		3. Name the new class, for example: `AccountHandler`

		4. Write class definition
			
			Sample Apex Class:

			``` apex
			public with sharing class AccountHandler {
				public static void CreateNewOpportunity(List<Account> accts) {
					for (Account a : accts) {
						Opportunity opp = new Opportunity();
						opp.Name = a.Name + ' Opportunity';
						opp.AccountId = a.Id;
						opp.StageName = 'Prospecting';
						opp.CloseDate = System.Today().addMonths(1);
						insert opp;
					}
				}
			}
			```
		5. Save the Apex code using the keyboard shortcut **Ctrl** + **S**

	2. Create a trigger

		1. From *Setup*, in User Menu, click on **Developer Console**

		2. In the *Developer Console*:
			1. At the top bar menu, click on **File**
			2. Click on **New**
			3. Click on **Apex Trigger**
		3. Name the new class, for example: `AccountTrigger`

		4. Write the trigger definition

			For example:

			``` apex
			trigger AccountTrigger on Account (before insert, before update, before delete, after insert, after update, after delete,  after undelete) {
				if (Trigger.isAfter && Trigger.isInsert) {
					AccountHandler.CreateNewOpportunity(Trigger.New);
				}
			}
			```

		5. Save the Apex code using the keyboard shortcut **Ctrl** + **S**

	3. Run the trigger

		1. From *Setup*, in User Menu, click on **Developer Console**

		2. In the *Developer Console*:
			1. At the top bar menu, click on **File**
			2. Click on **New**
			3. Click on **Apex Trigger**

		3. Name the new class, for example: `AccountTrigger`

	4. Write the trigger definition


### 2. 4. Examining the Execution Log

&uarr; [Understand Execution Context](#2-understand-execution-context)

- First line marks EXECUTION_STARTED event
- Last line is EXECUTION_FINISHED event
- Everything between is the execution context
- CODE_UNIT_STARTED events mark the start of specific code units
- All code operates under the same execution context
- Subject to the same set of governor limits

### 2. 5. Working with Limits

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Governor limits keep each instance from consuming too many resources
- Most common limits involve:
	- Number of SOQL queries
	- Number of DML statements
- Current limits:
	- 100 SOQL queries (synchronous)
	- 150 DML statements (synchronous)
- Limits tend to change with each major release

### 2. 6. Working in Bulk

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Common trap: designing code to work with a single record
- Apex triggers can receive up to 200 records at once
- If a trigger performs SOQL query or DML statement inside a loop, it can hit limits
- "Bulkify" your code from the start
- Example of bad code: DML operation inside a for loop
- Fixed code: write to a list variable inside loop, insert contents in one step

### 2. 6. 1. Testing Bulk Code

&uarr; [Understand Execution Context](#2-understand-execution-context): [Working in Bulk](#2-6-working-in-bulk)

- Write unit tests to ensure code works
- Test class example includes:
	- Creation of 200 test accounts
	- Verification that 200 new accounts were inserted
	- Verification that 200 new opportunities were created

### 2. 7. Tell Me More

&uarr; [Understand Execution Context](#2-understand-execution-context)

- Apex uses try-catch-finally block for exception handling
- No application or session variables in Lightning Platform
- Static variables only persist information within a single execution context
- Working with limits involves many tradeoffs, especially for managed packages

### 2. 8. Resources

&uarr; [Understand Execution Context](#2-understand-execution-context)

- [Invoking Apex](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_invoking.htm) in the Apex Code Developer's Guide
- [Getting Started with Apex Triggers](https://developer.salesforce.com/trailhead/apex_triggers/apex_triggers_intro) in the Developer Beginner trail
- [Executing Governors and Limits](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_gov_limits.htm)
- [Testing Triggers](https://developer.salesforce.com/trailhead/apex_testing/apex_testing_triggers) in the Developer Beginner Trail

## 3. Use Asynchronous Apex


## 4. Debug and Run Diagnostics