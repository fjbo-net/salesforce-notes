# Formulas and Validations

🔗 Source: [Formulas and Validations Trailhead module](https://trailhead.salesforce.com/content/learn/modules/point_click_business_logic?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)

Tailor your apps without writing code by using point-and-click logic.


## Objectives

- Create a custom formula field and use the formula editor
- Explain why formula fields are useful
- Outline at least one use case for formula fields
- Create simple formulas


## Key Takeaways 🧠

- [Use Formula Fields](#1-use-formula-fields)
	- Can be added to:
		- Page Layouts
		- Reports
		- List Views 
	- Cross-Object formulas allow displaying related object data
	- Date Calculations enable dynamic reporting capabilities
- [Implement Roll-Up Summary Fields](#2-implement-roll-up-summary-fields)
- [Create Validation Rules](#3-create-validatoin-rules)


## 1. Use Formula Fields

Use Case Applications:

- Page layouts for quick information access
- Reports for calculated columns
- List views for filtered data display
- Cross-object data relationships

### 1. 1. Introduction to Formula Fields

- Automatically calculate values that update dynamically
- Can be added to page layouts, reports, and list views for instant access
- Best practice: start with simple calculations and build to more complex scenarios


### 1. 2. Ready to Get Hands-on with Formulas?

- Create new Trailhead Playground for hands-on practice
- Must use brand-new playground to avoid challenge completion issues


### 1. 3. Find the Formula Editor

1. From *Setup*, open the **Object Manager** and click **Opportunity**.
0. In the left sidebar, click **Fields & Relationships**.
0. Click **New**.
0. Select **Formula**, and click **Next**.
0. In **Field Label**, type `My Formula Field`. Notice that **Field Name** populates atuomatically.
0. Select the type of data you expect your formula to return. Pick **Text**.
0. Click **Next**. You've arrived at the formula editor!


### 1. 4. Use the Formula Editor

- **Two editor types**: Simple and Advanced
	- Aalways use Advanced
- **Insert Field button**
	- Opens menu to select fields with correct syntax generation
- **Insert Operator** button
	- Provides dropdown of mathematical and logical operators
- **Functions** menu
	- Contains pre-implemented operations
	- Some functions work as-is (TODAY() returns current date)
	- Others require parameters (LEN(text) finds text length)
- Text area guidelines
	- Whitespace doesn't matter
	- Field and object names are case sensitive
	- Standard order of operations applies for numbers
- **Check Syntax** button
	- Validates formula before saving

#### 1. 4. 1. Example 1: Display an Account Field on the Contact Detail Page

**Cross-Object Formula Creation**
- Enables displaying related object data on current record
- Example: Show Account Number on Contact page

&nbsp;

1. Navigate to Contact object in Object Manager
0. Create new Formula field
0. Name: "Account Number", Type: Text
0. Use Insert Field: Contact | Account | Account Number
0. Formula result: `Account.AccountNumber`
0. Check syntax and save


#### 1. 4. 2. Example 2: Display the Number of Days Until an Opportunity Closes on a Report

Date Calculation Formula:
- Calculate dynamic date differences
- Example: Days remaining until opportunity close

&nbsp;

1. Navigate to Opportunity object
0. Create "Days to Close" field with Number type
0. Formula: `CloseDate - TODAY()`
0. Add field to reports for instant visibility
0. Can create reports showing calculated values


### 1. 5. Debug Formulas

Common Syntax Errors:

1. **Missing parentheses**
	 - Most common when opening/closing parentheses don't match
	 - Also occurs with missing commas between function parameters

2. **Incorrect parameter type**
	 - Providing wrong data type to functions
	 - Check documentation for expected parameter types

3. **Incorrect number of parameters**
	 - Too many or too few parameters for functions
	 - Reference help text for parameter requirements

4. **Formula result incompatible with return type**
	 - Selected data type doesn't match formula output
	 - Example: Number field returning date value

5. **Field does not exist**
	 - Misspelled or incorrectly capitalized field names
	 - Missing quotation marks around text literals

6. **Unknown function**
	 - Misspelled or unsupported functions
	 - Verify function exists in Salesforce

Debugging Best Practices

- Always use Check Syntax button
- Break complex formulas into multiple lines
- Use Insert Field menu to ensure correct syntax
- Verify function names and parameters in documentation

### 1. 6. Further Examples
1. **Hyperlink Formula**
	 - `HYPERLINK("http://www.VeryImportantWebsite.com", "Very Important Website")`
	 - Creates clickable links in page layouts

2. **Discount Calculation**
	 - `ROUND(Amount - (Amount * 0.12), 2)`
	 - Applies 12% discount with rounding to 2 decimal places

3. **Checkbox Logic**
	 - `AND(Account.NumberOfEmployees > 1000, Amount > 10000)`
	 - Returns true when both conditions met
	 - Displays as checked/unchecked box


## 2. Implement Roll-Up Summary Fields


## 3. Create Validatoin Rules