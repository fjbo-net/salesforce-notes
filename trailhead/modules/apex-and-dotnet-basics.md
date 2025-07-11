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
- Know when to use Asynchronous Apex
- Use future methods to handle a web callout
- Work with the batchable interface to process a large number of records
- Understand the advantages of using the queueable interface when you need to meet in the middle

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
	- [When To Go Asynchronous](#3-1-when-to-go-asynchronous)
		- Processing large volumes of records
		- Making external web service callouts
		- Improving user experience by offloading processing to async calls
	- [Future Methods](#3-2-future-methods)
		- [Implementation](#3-2-1-future-methods-implementation):
			- Add `@future` annotation to make a static method asynchronous
			- Use `@future(callout=true)` for web service callouts
		- [Limitations](#3-2-2-future-methods-limitations):
			- No execution tracking
			- Parameter restrictions
			- No chaining
	- [Batchable Interface](#3-3-1-batchable-interface)
		- Process up to 150 million records
		- Clean up or archive large datasets
		- Can utilize Bulk API 2.0
		- Schedulable for specific times
		- [Implementation](#3-3-1-1-batchable-interface-implementation):
			- Implement `Database.Batchable<sObject>` interface
			- Define three methods: `start()`, `execute()`, and `finish()`
			- Invoke using `Database.executeBatch()`
			- Default batch size: 200 records
		- [Limitations](#3-3-1-2-batchable-limitations):
			- Troubleshooting can be difficult
			- Jobs are queued and subject to server availability
			- Still subject to various platform limits
	- [Queueable Apex](#3-3-3-and-then-there-was-queueable-apex)
		- Best of both worlds
			- Accepts non-primitive types
			- Progress can be tracked
			- Job chaining
		- Implementation:
	- [Tell Me More](#3-4-tell-me-more)
		- Apex Flex Queue
		- Scheduled Apex
		- Use **Future Methods** for simple async processing and web callouts
		- Use **Batch Apex** for processing large data volumes (millions of records)
		- Use **Queueable Apex** when you need the middle ground - more features than future methods but simpler than batch
		- Consider platform limits even in asynchronous context
		- Choose the right tool based on your specific requirements


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
Follow Along with *Trail Together*
- Video available at: https://play.vidyard.com/oWWzy6KQ8LEKfbGMskyhhR?second=1932
	- Clip starts at 32:07

### 3. 1. When to Go Asynchronous

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex)

Main reasons for choosing asynchronous programming on the Lightning Platform:
	- **Processing a very large number of records**
		- Limits associated with asynchronous processes are higher than synchronous processes
		- Best bet for processing thousands or millions of records
	- **Making callouts to external web services**
		- Callouts can take a long time to process
		- In the Lightning Platform, triggers can't make callouts directly
	- **Creating a better and faster user experience**
		- Offload some processing to asynchronous calls

### 3. 2. Future Methods

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex)

- Future Methods are the async methods in Apex
- Used when you need to make a callout to a web service or want to offload simple processing to an asynchronous task
- Changing a method from synchronous to asynchronous processing is amazingly easy
- Just add the `@future` annotation to your method
- Requirements:
	- Method must be static
	- Method must return only a void type
- Called like any other static methods

#### 3. 2. 1. Future Methods Implementation

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Future Methods](#3-2-future-methods)

- Add `@future` annotation to make a *static* method asynchronous
- Use `@future(callout=true)` for web service callouts

Example for performing a web service callout:
``` java
public class MyFutureClass {
	// Include callout=true when making callouts
	@future(callout=true)
	static void myFutureMethod(Set<Id> ids) {
		// Get the list of contacts in the future method since
		// you cannot pass objects as arguments to future methods
		List<Contact> contacts = [SELECT Id, LastName, FirstName, Email
			FROM Contact WHERE Id IN :ids];
		// Loop through the results and call a method
		// which contains the code to do the actual callout
		for(Contact con: contacts) {
			String response = anotherClass.calloutMethod(con.Id,
				con.FirstName,
				con.LastName,
				con.Email);
			// May want to add some code here to log
			// the response to a custom object
		}
	}
}
```

#### 3. 2. 2. Future Methods Limitations

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Future Methods](#3-2-future-methods)


Limitations to consider before using a future method:
	- **No execution tracking**
		- Can't track execution because no Apex job ID is returned
	- **Parameter restrictions**
		- Parameters must be primitive data types, or collections of primitive data types
		- Future methods can't take sObjects as arguments as they might change in the time before the @future method executes
	- **No chaining**
		- You can't chain future methods and have one call another
		- Use Queueable apex if you need execution in a certain order
- Although asynchronous calls are sometimes done to avoid limits, you still need to consider limits

### 3. 3. Batch or Scheduled Apex

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex)

#### 3. 3. 1. Batchable Interface

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Batch or Scheduled Apex](#3-3-batch-or-scheduled-apex)

- Another long-used asynchronous tool is the batchable interface
- Use cases:
	- Clean up or archive up to 150 million records
	- Can utilize the Bulk API 2.0 in your Apex code
	- Can schedule your batches to run at a particular time

##### 3. 3. 1. 1. Batchable Interface Implementation

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Batch or Scheduled Apex](#3-3-batch-or-scheduled-apex): [Batchable Interface](#3-3-1-batchable-interface)

- Your class implements the Database.Batchable interface
- Define start(), execute(), and finish() methods
- Invoke a batch class using the Database.executeBatch method

Example batchable class that processes all accounts in an org and sends an email when done:

``` java
global class MyBatchableClass implements
			Database.Batchable<sObject>,
			Database.Stateful {
	// Used to record the total number of Accounts processed
	global Integer numOfRecs = 0;
	// Used to gather the records that will be passed to the interface method
	// This method will only be called once and will return either a
	// Database.QueryLocator object or an Iterable that contains the records
	// or objects passed to the job.
	global Database.QueryLocator start(Database.BatchableContext bc) {
		return Database.getQueryLocator('SELECT Id, Name FROM Account');
	}
	// This is where the actual processing occurs as data is chunked into
	// batches and the default batch size is 200.
	global void execute(Database.BatchableContext bc, List<Account> scope) {
		for(Account acc : scope) {
			// Do some processing here
			// and then increment the counter variable
			numOfRecs = numOfRecs + 1;
		}
	}
	// Used to execute any post-processing that may need to happen. This
	// is called only once and after all the batches have finished.
	global void finish(Database.BatchableContext bc) {
		EmailManager.sendMail('someAddress@somewhere.com',
							numOfRecs + ' Accounts were processed!',
							'Meet me at the bar for drinks to celebrate');
	}
}
```

Invoke the batch class using anonymous code:

``` java
MyBatchableClass myBatchObject = new MyBatchableClass();
Database.executeBatch(myBatchObject);
```

##### 3. 3. 1. 2. Batchable Limitations

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Batch or Scheduled Apex](#3-3-batch-or-scheduled-apex): [Batchable Interface](#3-3-1-batchable-interface)


Limitations to consider:
- **Troubleshooting can be troublesome**
- **Jobs are queued and subject to server availability**
	- Can sometimes take longer than anticipated
- **Limits**
	- Still subject to various limits

#### 3. 3. 2. Scheduled Apex

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Batch or Scheduled Apex](#3-3-batch-or-scheduled-apex)

Scheduled Apex not covered in this unit. 😶‍🌫️

**Note**: Scheduled Apex is similar to the batchable interface

- Implements the schedulable interface
- Can be used to invoke Apex at specific times
- Learn more in the [Asynchronous Apex](https://trailhead.salesforce.com/content/learn/modules/asynchronous_apex) module

#### 3. 3. 3. And Then There Was Queueable Apex

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex): [Batch or Scheduled Apex](#3-3-batch-or-scheduled-apex)

Best of Both Worlds

- **Non-primitive types**
	- Accepts sObjects and custom Apex types as parameters
- **Job monitoring**
	- Returns jobId for tracking progress
- **Job chaining**
	- Can chain one job to another for sequential processing

##### 3. 3. 3. 1. Queueable Apex Implementation
- Implement `Queueable` interface
- Define `execute(QueueableContext context)` method
- Invoke using `System.enqueueJob()`
- Much easier to implement than Batch Apex

Example converting the future method web callout to Queueable Apex:

```apex
public class MyQueueableClass implements Queueable {
	private List<Contact> contacts;
	// Constructor for the class, where we pass
	// in the list of contacts that we want to process
	public MyQueueableClass(List<Contact> myContacts) {
		contacts = myContacts;
	}
	public void execute(QueueableContext context) {
		// Loop through the contacts passed in through
		// the constructor and call a method
		// which contains the code to do the actual callout
		for(Contact con: contacts) {
			String response = anotherClass.calloutMethod(con.Id,
					con.FirstName,
					con.LastName,
					con.Email);
			// May still want to add some code here to log
			// the response to a custom object
		}
	}
}
```

To invoke Queueable Apex:

```apex
List<Contact> contacts = [SELECT Id, LastName, FirstName, Email
	FROM Contact WHERE Is_Active__c = true];
Id jobId = System.enqueueJob(new MyQueueableClass(contacts));
```

### 3. 4. Tell Me More

&uarr; [Use Asynchronous Apex](#3-use-asynchronous-apex)

- **Apex Flex Queue**
	- Eliminates the 5 concurrent batch limit and allows job order management
- **Scheduled Apex**
	- Uses schedulable interface to invoke Apex at specific times

Best Practices:
- Use **Future Methods** for simple async processing and web callouts
- Use **Batch Apex** for processing large data volumes (millions of records)
- Use **Queueable Apex** when you need the middle ground
	- More features than future methods but simpler than batch
- Consider platform limits even in asynchronous context
- Choose the right tool based on your specific requirements

## 4. Debug and Run Diagnostics