# Salesforce to Salesforce

🔗Source: [Salesforce Help](https://help.salesforce.com/s/articleView?id=sales.business_network_intro.htm&type=5)

## Key Takeaways 🧠

- Salesforce Features:

	- **Salesforce to Salesforce**
		
		Allows organizations to share records and update record information.

		- Legality and Governance:
			- Ensure appropriate contractual or other legal arrangements are in place prior to sharing data
			- You agree to allow Salesforce to process update to information that is shared with other organizations
		- Only available in Salesforce Classic (UI)
			- Setup > Customize > Salesforce to Salesforce > Salesforce to Salesforce Configuration
				- Enable (Salesforce to Salesforce)
				- Email Settings
					- Name
					- Address
				- Email Templates
			- Connections (Tab)
				- Manage Connections
				- Manage Invitations
				- Manage Templates
		- Once enabled for the *Org*, it cannot be disabled
		- Use *permission sets* to:
			- Control which users can:
				- Manage connections
				- Share data
			- Control to which *Orgs* data can be shared
		- Uses email surveys to "discover connections"
			- *Connection Finder* values depend on partner's reponse (API value in parenthesis):
				- No (`No`)
				- No Response (`NoResponse`)
				- Not Sure (`NotSure`)
				- Yes, admin user (`YesAdmin`)
				- Yes, not admin user (`YesNotAdmin`)
		- Invitiations can be sent individually or in batch
		- When enabled:
			- Adds user '`Connection User`'
				- Cannot be managed/edited
				- Doesn't count toward license limits
				- Appears in the '`Last Modified By`' fields when a partner updates a record
			- Adds '`Partner Network`' profile
				- Cannot be managed/edited
			- Provides data to objects' *related lists* (requires adding columns)
		- 


## 1. Set Up Salesforce to Salesforce

### 1. 1. Enable Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

Available in:
- Salesforce Classic (UI)
- Editions:
	- Contact Manager
	- Group
	- Professional
	- Enterprise
	- Performance
	- Unlimited

Requires Permissions:
- `Modify All Data` permission

&nbsp;

Salesforce to Salesforce is a permanent feature that allows controlled data sharing between organizations. Permanent means that cannot be disabled once activated.



When enabling Salesforce to Salesforce:

- You are responsible for legal agreements and governance

	Prior to sharing data, consider the following legal stuff:

	- You are responsible for ensuring that appropriate contractual or other legal arrangements are in place between you and your connected organizations.
	
	- You legally agree to allow Salesforce to process information that is being shared with other organizations when enabling Salesforce to Salesforce.
- Creates user '`Connection User`'
	- User does not count towards any license usage
	- User does not show up in any user management view
	- '`Connection User`' is added to the '`Partner Network`' profile
		- Profile can't be modified and does not show up in any profile management view 
- When a business partner updates a shared record:
	- '`Connection User`' is used for the 'Last Modified By' field of the record

#### Prerequisites
- "Modify All Data" user permission
- Must use Salesforce Classic (switch from Lightning Experience if needed)

#### Setup Steps
1. Navigate to Setup > Quick Find > **Salesforce to Salesforce Settings**
0. Click **Edit**
0. Select **Enable**
0. Click **Save**

#### Key Points
- Creates a "Connection User" that doesn't count toward license limits
- Connection User tracks partner-made changes via Last Modified By field
- Requires appropriate legal arrangements between connected organizations
- Cannot be disabled once enabled
- Allows granular control over shared data and recipient organizations

### 1. 2. Configure Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

Available in:
- Salesforce Classic (UI)
- Editions:
	- Contact Manager
	- Group
	- Professional
	- Enterprise
	- Performance
	- Unlimited

Requires Permissions:
- `Modify All Data` permission

&nbsp;

Overview:

1. **Create Permission Set**

	Ensures secure cross-organization data sharing and delegates managing connections without needing assistance from an administrator.

	- Create new *permission set*
	- In Permission Set &gt; Enable '`Manage Connections`' permission
	- Set **Connection tab** to Visible
	- Enable '`Manage Queues`' permission for users with '`Manage Connections`'


0. **Update Page Layouts**

	Provides access to view and accept shared records to users (even those without the '`Manage Connections`' permissions).

	- Add the '`External Sharing`' *related list* to the appropriate profiles
	- Add columns '`Received Connection Name`' and '`Sent Connection Name`' columns to the *related lists* of the desired objects
	- Create custom list views on the '`External Sharing`' *related list* on the page layouts of desired objects

0. **Configure Communication Templates**

	Provides consistent communication templates.

	In '`Setup`', find '`Salesforce to Salesforce Settings`' in the *Quick Find* box:
	- Click on **Salesforce to Salesforce Settings** in the sidebar
	- Set sender's email address in the **From Email Address** field
	- Set sender's name in the **Name** field
	- You can configure the following email templates:
		- **Invitation Template**
		- **Deactivation Template**
		- **Accept Invitation Template**
		- **Reject Invitation Template**
		- **Update COnnection Profile Template**
	- Click **Save**

### 1. 3. Connect with Your Business Partners using Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

&nbsp;

#### 1. 3. 1. Enable Connection Finder

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;


1. In Setup, find **Salesforce to Salesforce Connection Finder** in the *Quick Find box*
0. Click **Edit**
0. Select **Enabled**
0. Click **Save**
	- Default email template and required related fields are created
	- Note: Disabling *Connection Finder* deactivates outstanding surveys and removes the Connection Finder button
0. Configure email template (must contain survey URL `{!Contact.PartnerSurveyURL}` merge field)
0. Optional: Add branded logo from Documents (must be marked Externally Available Image)
0. Add Connection Finder button to:
	- Contacts list view via search layout
	- Contact detail page via page layout
0. Add required fields:
	- "Uses Salesforce" to contacts page layout
	- "Salesforce Customer" to account page layout

#### 1. 3. 2. Find Out if Your Businesses Partners Use Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;


After enabling Salesforce to Salesforce, you can email a survey to partners that asks them if they use Salesforce. Requires user permissions: Send Email (single recipient) or Mass Email (multiple recipients).

1. In the Contact list view:
	1. Select partners
	0. Click **Find Connections** (does not appear when record has invalid email address or isn't associated with an account)
0. Select a template
	- Message body can be edited for single recipients, but must include the survey URL)
0. Send email

[Emailed] Survey:
- Expires after 90 days
- Response:
	- Recorded on:
		- recipient's contact record
		- recipient's account record
	- Adds a closed activity to the contact record
- Recipient:
	- Survey asks if recipient is an admin when the recipient's organization uses Salesforce
		- When not an admin:
			- Recipient can optionally provide their administrator's contact information (new contact record is created unless it already exists)
		- When admin:
			- Connection Finder field is set to `Yes, admin user` (Not updated if already set to `No`)

#### 1. 3. 3. Invite Business Partners to Connect

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;


**Invite One Business Partner**

1. Click the **Connections** tab
0. Click **New**
0. Enter a contact name or use the *lookup icon* to select one

**Invite Multiple Business Partners to Connnect**

1. Click the *Contacts* tab
0. Select a list view
0. Click **Go!**
0. Click **Invite to Connect**
0. Choose a user to manage the connection
0. (Optional) Choose a template
0. Click **Save &amp; Send Invite**


#### 1. 3. 4. Accept an Invitation for Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;

1. In the invitation email, click the link
0. Log in as either:

	- System administrator
	- User with '`Manage Connections`' permissions

0. Review invitation
0. Click on **Accept**, **Decline** or **Decide Later**

Your response notifies the sender's *Org*, using the following templates:
- Accept Invitation Template
- Reject Invitation Template
- Update COnnection Profile Template


#### 1. 3. 5. Create and Apply Connection Templates

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;

Connection templates let you define objects and fields that can be published to connected *Orgs*.

Consider the following prior to creating a *Connection Template*:

- Conflicting 'publish' or 'unpublish' statutes are changed to the status defined in the *Connection Template*
- Matching 'publish' or 'unpublish' statuses won't be changed

**Create a Connection Template**

1. Select the **Connections** tab
0. Select the **Templates** subtab
0. Click **New**
0. Type a name and an optional description
0. Selct the **Active** checkbox to assign the template to standard connections.
0. Click **Save** or **Save &amp; Add Objects**

**Assigning Objects to a Connection Template**
1. In the template detail page, click **Add/Remove Objects**
0. Click **Edit** next to an object you added to the 'Published Objects' *related list*
0. Select the fields you want to publish for the object
0. Click **Save**
0. Repeat as needed for each object you would like to add

**Deactivate a Connection Template**
1. Select the **Connections** tab
0. Select the **Templates** subtab
0. Click **Edit** next to the template to be deactivated
0. Deselect the **Active** checkbox
0. Click **Save**

**Assign a Connection Template to a Connection**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection you want to assign the template to
0. Click **Edit**
0. Type the name of the template you in the **Template** field, or use the *lookup icon* to select a template
0. Click **Save**


#### 1. 3. 6. Manage Salesforce to Salesforce Connections

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce) :
[Connect with Your Business Partners...](#1-3-connect-with-your-business-partners-using-salesforce-to-salesforce)

&nbsp;

**Accept an Invitation**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
0. Click **Accept**, next to the page heading "Connection Detail"

**Cancel an Invitation**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
0. Click **Cancel Invitation**

**Deactivate Connections**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
0. Click **Deactivate**, next to the page heading "Connection Detail"

**Edit Connections**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
	- To change **Connection Details**:
		1. At the *Connection Detail* page, click **Edit** (next to the page heading "Connection Detail")
			- At the Connection Edit page you can:
				- Select a *Connection Template*
				- Select an *Account* for the connected business partner
				- Select a *Connection Owner* for the connection
	- To change the objects published to a connection, click **Publish/Unpublish** (alternatively, you can add or replace the *Connection Template*)
		1. At the *Connnection Detail* page, click **Publish/Unpublish**
		0. Check the objects that you would like to publish, or uncheck the objects you would like to unpublish
		0. Click **Save**
	- To edit **published fields** on an object:
		1. At the *Connnection Detail* page, under *Published Objects* click on **Edit** next to the object's name
		0. Check the fields that you would like to publish and uncheck the fields that you would like to unpublish.
		0. Click **Save**

**View Connection History**
1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
0. You can find the **Connection History** at the bottom of the *Connection Detail* page
0. Optionally, you can download the connection history by clicking **Download connection history (csv)**

*Connection History* includes:
- Connection status changes
- Changes to which contact is associated with the connection
- Connection owner changes
- Changes to published fields
- Email communications sent to business partners
- Errors related to validation rules and Apex triggers with validation rules resulting from:
	- Records manually accepted
	- Records automatically accepted
	- Records updated by Connection User

System errors are not logged into the *Connection History*


### 1. 4. Publish Objects with Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

&nbsp;

Objects can be publish and unpublish from the *Connections* Tab. Follow the steps in [Manage Salesforce to Salesforce Connections](#1-3-6-manage-salesforce-to-salesforce-connections) > Edit Connections, to Publish/Unpublish objects.

- Only objects with edit permission can be published
- Only deployed custom objects can be published
- Only the following standard objects can be published:
	- Account
	- Attachment (unencrypted)
	- Case
	- Case Comment
	- Contact
	- Lead
	- Opportunity
	- Opportunity Product
	- Product
	- Task

**Updating published objects**
- Salesforce sends an email notification to connected partners upon updating published objects
- Partner is automatically unsubscribed from objects upon unpublishing objects
- All *public* case comments will be shared when sharing the *Case Comment* object.
	- To keep case comments private, make sure to select **Make Private** in the corresponding case comments
- Only unencrypted files are supported


### 1. 5. Publish Fields in Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

&nbsp;

Once objects are published, individual fields can be selected or unselected. Follow the steps in [Manage Salesforce to Salesforce Connections](#1-3-6-manage-salesforce-to-salesforce-connections) > Edit Connections, to Publish/Unpublish fields.

- Only fields with edit permissions can be published
- Takes up to 15 minutes for Salesforce to refresh the cache
- Rich text area (RTA) fields cannot be published
- Geolocation fields on standard addresses aren't supported

**Default Published Fields**
- Account
	- Account Name
- Account (Person)
	- Account Name
	- Last Name
- Attachment
	- Body
	- Content Type
	- File Name
- Case
	- Subject
- Case Comment
	- Body
	- Published
- Contact
	- Last Name
- Custom Object
	- Name
- Lead
	- Last Name
	- Company
- Opportunity
	- Name
	- Closed Date
	- Stage
- Product
	- Product Name
- Task
	- Subject
- Opportunity Product
	- Quantity
	- Sales Price

**Updating Published Fields**
- Salesforce sends an email notification to connected partners upon updating published fields
- Partner is is automatically unsubscribed from fields upon:
	- Unpublishing a field
	- Changing the type of a field
	- Changing size or precision of:
		- A long text area field
		- A text field
		- A percent field
		- A number field
		- A currency field


### 1. 6. Subscribe to Objects with Salesforce to Salesforce

&uarr; [Set Up Salesforce to Salesforce](#1-set-up-salesforce-to-salesforce)

&nbsp;

1. Select the **Connections** tab
0. Select the **Connections** subtab
0. Click the name of the connection to open the *connection detail page*
0. You can find **Subscribed Objects** *related list* almost at the bottom of the *Connection Detail* page
0. Click **Subscribe/Unsubscribe**


### Subscribe to Fields in Salesforce to Salesforce

### Automate Updates with Workflow Rules in Salesforce to Salesforce

## Share Records Using Salesforce to Salesforce

## Report on Salesforce to Salesforce Activity

## Guidelines for Using Salesforce to Salesforce

## Statuses for Records Shared with Salesforce to Salesforce

## Best Practices for Mapping Fields in Salesforce to Salesforce