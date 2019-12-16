# Listman.io is a SharePoint Lists Auto Archive and Export Tool

## Documentation

**Listman.io** is a simple yet powerfully Windows Console Application that helps organizations auto archive and export data and attachments from SharePoint Lists of any size without annoying [5000 list view threshold](https://docs.microsoft.com/en-us/sharepoint/support/lists-and-libraries/items-exceeds-list-view-threshold) based of certain criteria.

![](https://user-images.githubusercontent.com/13550565/70306479-e872cd00-1841-11ea-9a44-26255be30a13.png)

## Table of Contents
* [What Listman.io App Is For](#what-is-listmanio-app-for)
* [What Listman.io Is Not For](#what-is-listmanio-not-for)
* [Why Your Business May Need Listman.io](#why-your-business-may-need-listmanio)
  + [Why Archive/Export SharePoint Lists to CSV](#why-archive-export-sharepoint-lists-to-csv)
* [System Requirements And Prerequisites](#system-requirements-and-prerequisites)
* [Download the App](#download-the-app)
* [Understanding the Free vs Business Plan](#understanding-the-free-vs-business-plan)
  + [How to Subscribe to Business Version](#how-to-subscribe-to-business-version)
* [Create SharePoint Application (App-Only or Application Context principal)](#create-sharepoint-application--app-only-or-application-context-principal-)
* [Quick Start Guide](#quick-start-guide)
* [Run as Console Application](#run-as-console-application)
  + [Run in Test Mode](#run-in-test-mode)
  + [Run in Production Mode](#run-in-production-mode)
* [Run as Windows Service](#run-as-windows-service)
  + [Install Service](#install-service)
  + [Start Service](#start-service)
  + [Stop Service](#stop-service)
  + [Delete Service](#delete-service)
* [Configure Listman.io](#configure-listmanio)
  + [How To Verify and Validate Config File](#how-to-verify-and-validate-config-file)
  + [`connectTo` section](#-connectto--section)
  + [`archiveJobs` section](#-archivejobs--section)
    - [`exportColumns` field](#-exportcolumns--field)
    - [`filterBy` subsection](#-filterby--subsection)
      * [`filterBy` with SharePoint Conditional Columns](#-filterby--with-sharepoint-conditional-columns)
    - [`recordAction` subsection](#-recordaction--subsection)
    - [`archiveTo` subsection](#-archiveto--subsection)
    - [`schedule` section](#-schedule--section)
* [Note on Logging](#note-on-logging)
* [Command Line Parameters](#command-line-parameters)
* [How to Get Help](#how-to-get-help)

## What Listman.io Is For

There are three main business cases when you could find Listman.io app helpful for your business:

1. You need to archive SharePoint Lists Items with attachments based on some searching criteria into an external file or cloud storage. You want to run that task periodically using CRON schedule as a Windows Service. You want to delete or modify archived list item afterwards.

2. You need to export large (more than 5000) SharePoint lists data (optionally with attachments) but can't do that using PowerShell, Excel, MS Access or Flow by some reason or just probably want to save your time. 

3. You may just want to download all lists items from SharePoint lists, probably to back up them or move over (offload) from SharePoint.

## What Listman.io Is Not For

1. Listman.io is not a SharePoint Migration tool. You could try to use it for simple migration tasks but once exported you shall import the lists data using your own approach.
2. Listman.io is not a SharePoint Back Up tool. It means once archived you can't easily restore and convert the lists data and attachment back to SharePoint.
3. And obviously, Listman.io is not a SharePoint Reporting tool.

## Why Your Business May Need Listman.io

In short, Listman.io will allow your company to run business more efficiently and:

1. Save money on custom SharePoint development (around one-two months of a developer salary), application support and maintenance 
2. Avoid 5000 view and search limitation threshold for the large lists in SharePoint by removing historical data and attachments
3. Reduce hosting costs by offloading unused attachments or documents into the file system or any cloud storage including OneDrive, Dropbox, Google Drive or Azure Storage
4. Improve overall system speed and responsiveness 
5. Comply and implement custom organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Automatically back up old data and documents based on certain criteria
8. Transfer or export lists data from SharePoint into any DB including MS SQL Server or Azure Database
9. And finally, configure and run archiving or exporting procedures in no time without any custom development (around 30 mins after simple configuration)
10. Development and other 3-rd party tools are costly for a small company. You could find Listman.io a perfect fit for a small organization or your consulting/freelancing business.

And if you are a SharePoint Consulting Microsoft Partner Listman.io will help you to implement client-side projects with better profit margin by saving money on custom archiving/export/migration requirements development.

### Why Archive/Export SharePoint Lists to CSV
... and not to MS SQL for example? 

So, Listman.io is built upon the principles of Unix philosophy and designed to *do one thing very well*, namely to archive and export SharePoint lists data into the CSV format files (comma delimited). We use CSV files as a final data destination because:

* CSV is understood by almost every piece of software on the planet (past and present)
* CSV is more human-readable than XML, JSON formats 
* CSV natively supported by Microsoft Excel
* CSV could be used as a source of import for almost any relational, document and graph DB including MS SQL Server and Microsoft Azure Database

So if you are looking to archive, export or migrate your SharePoint data into Microsoft SQL Server Database you could use Listman.io in conjunction with other ETL tools (for example custom SSIS packages or SQL Server Import and Export Wizard) to easily accomplish your goal delegating exporting data from SharePoint to the Listman.io.

## System Requirements And Prerequisites
Before start let's make sure your system complies with the following system requirements:

1. You have an instance of SharePoint 2013/2016/2019 or SharePoint Online
2. You should have a Microsoft Account to Sign In for the service
2. To run Listman.io as command line application or Windows Service you must have Windows 7/8/10/Server 2008/2012/2016 system installed on one of your local machines or cloud VM. For simplicity we will reference to the machine as the **application server**.
3. You have .NET Framework 4.7.1 installed on the application server. **Note:** .NET Core is not yet supported*.
4. Your application server must be connected to the Internet. Without the internet connection Listman.io app wouldn't be able to verify your *sign in email*.
5. Ideally you should to have some knowledge of JSON files, usage of Windows Command Line and Windows Services, and specifically `sc` command but it's all optional.

> **\* What about .NET Core?** Unfortunately by the time of application implementation Microsoft didn't yet release .NET Standart CSOM libraries compatible with .NET Core runtime environment. We will keep our eye on that matter and plan to implement .NET version of the Listman.io app as soon as CSOM will be available for .NET Core.

## Download the App
Listman.io app distributed as `zip` archive and don't need any additional installation except unzipping. It's very easy to download a copy of the Listman.io application:

1. Go to [www.listman.io](https://www.listman.io)

![image](https://user-images.githubusercontent.com/13550565/70397333-57bc0d00-1a4c-11ea-87d2-0079a10f3844.png)

2. Click on **Sign In with Microsoft**. After successfully Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard)

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70385120-e6397b80-19c5-11ea-9291-36aebedfb3cd.png" alt="drawing" width="200"/>

3. Click on **Download Listman.io App** button and save the archive somewhere on your application server

Alternatively you could download the latest and all the previous versions of the Listman.io application using that [link](https://github.com/listman-io/docs/packages) from the Github. 

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70385126-01a48680-19c6-11ea-8859-b83cf2f5992a.png" alt="drawing" width="400"/>

> **Note:** Even if the app is downloaded from the Github you still need to Sign In with your Microsoft account on [www.listman.io](https://www.listman.io) to obtain your Free License details.

Congratulations! Now you are ready to run and configure the Listman.io app. But first let's understand different Listman.io Licenses.

## Understanding Free vs Business Plan
Listman.io is a **commercial software** but purposely designed to have Free Plan for better evaluation experience. There is **no trial/expiration for a Free Plan** so you have unlimited time to make sure Listman.io fits all your organization archiving or exporting needs. 

We recommend you to start run Listman.io using a Free Plan and first learn how to archive/export data from small lists on your Development or Staging SharePoint servers. Once confident with the app configuration you could easily subscribe to a Business Plan and start archive or export data from larger lists.

> Free Plan is limited to archive or export data from the lists with to 500 items. If you want to archive or export data from the lists larger than 500 items we recommend you upgrade to a Business Plan. Note, Business Plan also includes priority support.

Look at the table below to choose between Free or Business Plan.

| Listman.io Feature  | Free Plan | Business Plan |
| ------------- | ------------- | -----------------|
| Unlimited sites |  ✅ |  ✅ |
| Unlimited lists |  ✅ |  ✅ |
| Unlimited jobs |  ✅ |  ✅ |
| Delete list items after archiving/export |  ✅ |  ✅ |
| Download list attachments |  ✅ |  ✅ |
| Run as CLI |  ✅ |  ✅ |
| Run as Windows Service |  ✅ |  ✅ |
| Cron Scheduler |  ✅ |  ✅ |
| Email Support |  ✅ |  ✅ |
| Large lists archiving/exporting | ❌, only lists up to 500 items |  ✅ |
| Priority Support |  ❌ |  ✅ |
| Cost |  Free |  $69 / per month |

### How to Subscribe to Business Plan

If you want to run archiving or exporting procedures for large lists **without 500 items limitation** you have to subscribe to a Business Plan. For that:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email.
3. Go to Billing details section and add details of your credit or debit card. 
4.  Make sure there is no errors and click **Update** twice. Once your billing details is saved you'll see a green label `Business Plan is Active`. Once billing details are provided for the first time your card will be billed immediately. Make sure you have sufficient funds available on your card each month so your subscription will stay active.

![image](https://user-images.githubusercontent.com/13550565/70397403-d749dc00-1a4c-11ea-9d03-8e3076d19a21.png)

> **Note:** We never store your billing detail on our servers. All the billing information and payments processed by Stripe.

5. You could always change your billing details. Just type a new card details and click on **Update** twice.

5. To unsubscribe from the Business Plan click twice on the **Unsubscribe** button. Note, once unsubscribed your Business Plan will be downgraded to the Free Plan *immediately* with 500 items limitation in place.

## Create SharePoint Application (App-Only aka Application Context Principal)

Now let's create your first SharePoint Application (also known as Application Context or App) that will be used to authorize Listman.io app against your Sharepoint Instance. 

In order for the Listman.io app to have an access to all the lists and lists attachments we have to create an Application Context (or App-Only) and grant it the `fullcontroll` **right** for the chosen **scope**. You could [read](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azureacs) about that procedure in more details on Microsoft Documentation Portal.

For this example let's assume that your SharePoint Instance is available on `https://listman.sharepoint.com` url. To create Application Context for the Listman.io app:

1. Make sure you have an admin access (like primary site collection administrator) to your Sharepoint Instance

> When you purchase a Microsoft 365 or Office 365 subscription, a team site is automatically created, and the global admin is set as the primary site collection administrator. For info about assigning a user the SharePoint administrator role, see [Assign admin roles in Office 365 for business](https://docs.microsoft.com/en-us/office365/admin/add-users/assign-admin-roles?view=o365-worldwide).

2. Go to url: `https://listman.sharepoint.com/_layouts/15/appregnew.aspx` or to `https://yourcompany.sharepoint.com/_layouts/15/appregnew.aspx`. You will see the new app registration form:

![image](https://user-images.githubusercontent.com/13550565/70397741-c5b60380-1a4f-11ea-92b8-788a0db71504.png)

3. Type the new application details in the form:
 * Client Id: click on **Generate**
 * Client Secret: click on **Generate**
 * Title: listman.io
 * App Domain: www.listman.io
 * Redirect Url: https://www.listman.io
 * Click **Create** button

![image](https://user-images.githubusercontent.com/13550565/70397765-f7c76580-1a4f-11ea-84bf-a0959f49c108.png)


4. You'll see the message:

```
The app identifier has been successfully created.
Client Id:  	b74101eb-cbec-4096-ac08-b61bdbcfdb58
Client Secret:  qhl9N9GCgJ11+Phh6WNhm39l+64ZlJRRm06wcQ2iJF4=
Title:  	listman.io
App Domain:  	www.listman.io
Redirect URI:  	https://www.listman.io
```

![image](https://user-images.githubusercontent.com/13550565/70397778-19285180-1a50-11ea-816c-8f2d390c60be.png)

5. Note the `Client Id` and `Client Secret` and write them down somewhere
6. Now go to `https://listman-admin.sharepoint.com/_layouts/15/appinv.aspx` or `https://yourcompany-admin.sharepoint.com/_layouts/15/appinv.aspx` . You will see another app form but on the admin site (don't ask, it's Microsoft 🤦🤦🤦 designed this UI).

> Note the `-admin` in the URL! It's very important!

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70397812-512f9480-1a50-11ea-84f4-867c147b3d3a.png" alt="drawing" width="400"/>

7. Copy `Client Id` from the step 5 into the "App Id and Title" field
8. Click on **Lookup**
9. Note the app details from the step 3 will appear in the form
10. Fill up the field `App's Permission Request XML` with the following XML:
```xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70397855-b5eaef00-1a50-11ea-9a2a-0f5790caff90.png" alt="drawing" width="400"/>

> In that example we specify scope as `Tenancy` so the `FullControl` right will be applied to all children (sites, lists) of this scope. Based on your requirements you could change that scope to Site Collection, Website or individual Lists. Reference to [Microsoft Documentation](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/add-in-permissions-in-sharepoint) for more details on that topic.

11. Click **Create**
12. You'll see the following Page:

![image](https://user-images.githubusercontent.com/13550565/70397861-d450ea80-1a50-11ea-88ea-9465dbd40e05.png)

13. Click on **Trust It**.

Great! Now we are ready to run Listman.io for the first time and make sure we could connect to your SharePoint Instance.

## Test Connection To SharePoint
Now let's quickly validate that we could connect Listman.io app to your SharePoint site using `clientId` and `clientSecret` created on the previous step. For that:

1. Download the Listman.io application from your Dashboard or from Github if you haven't done it before.
2. Unpack the archive into a folder from which you want to run the application on your application server. We will reference to this folder as the **app folder** for simplicity.
3. Navigate to **app folder** using Windows Explorer
4. Open the `config.json` file in any text editor of your choice
5. Make sure your know:
 * your `sign in email`
 * `clientId` for the SharePoint app from step 4, section [Create SharePoint Application](#create-sharepoint-application-app-onlyapplication-context)
 * `clientSecret` for the SharePoint app from step 4, section [Create SharePoint Application](#create-sharepoint-application-app-onlyapplication-context)
5. Edit the `config.json` file. Change the fields to your specific values and **Save** the file:

```js
connectTo: {
  email: "your_sign@in_email.com",
  siteUrl:"https://yourcompany.sharepoint.com/",
  clientId: "clientId_for_sharepoint_app",
  clientSecret: "clientSecret_for_sharepoint_app"
},
```
6. Open Windows Command Line
7. Navigate into the **app folder**, for that use the command:
```sh
> cd /d app_folder
``` 
8. Run the Listman.io app with the following command line parameters:
```sh
> listman-cli.exe -s
``` 
Where:
* `-p` - parameter used to validate config file
* `-s` - parameter used to test the connection to Sharepoint using `siteUrl` and App-Only credentials
9. Check the application output. Note that the app could connect to the SharePoint instance, for that make sure you see the message
 ```
 Successfully connected to: https://yourcompany.sharepoint.com/
 ```

Good job! Now let's learn what are some different ways to run the Listman.io app. 

## Run as Console Application

Before running Listman.io app against your production SharePoint Instance we recommend you to *always* run the app in a test mode.

### Run in Test Mode
Test mode allows you to start Listman.io app, validate config file, connect to SharePoint Instance and *iterate through the list items without actual archiving, deletion, modification and attachments downloading*. 

The Test Mode is designed to battle test your configuration as close as possible to the actual production run including logs creation to verify all the expected records were correctly marked for archiving.

To run application in Test Mode run the app with the  `-p` and `-t` parameter:
```sh
> listman-cli.exe -p -t
```

You could combine `-p`, `-t` and `-v` parameters for detailed logging:
```sh
> listman-cli.exe -p -t -v
```

### Run in Production Mode
To run Listman.io in a production mode as a console app  go to (`cd`) to **Application Folder** and run:
```sh
> listman-cli.exe
```
By default application fill try to read a config file from the `app_folder/config.json` path.

You can specify a path to the custom config file using `-c` parameter:
```sh
> listman-cli.exe -c "Configs\yourcompany.sharepoint.com.json"
```
The `-c` parameter is useful if you have several config files for several SharePoint Instances.

To produce detailed logging run the application with the `-v` (verbose) parameter:
```sh
> listman-cli.exe -c "Configs\yourcompany.sharepoint.com.json" -v
```

## Run as Windows Service
When you ready to move your archiving or export automation to a new level you may want to run Listman.io as a Windows Service. 

### Install Service
Assuming the installation path to listman.cli is `C:\Work\listman.cli.release\` use that command to install listman-cli as a Windows Service with name `ListmanService`:
```sh
sc create ListmanService binPath= "C:\Work\listman.cli.release\listman-cli.exe"
```

> Note the white space after `=`. It's there for purpose. 

### Start Service
1. Go to Services
2. Right click on ListmanService -> Properties
3. Type
```sh
-c C:\Work\listman.cli.release\Config\listman.sharepoint.json -v
```
 into the `Start Parameters` field
4. Click Start

Alternatively use the `sc.exe` command:
```sh
sc start ListmanService -v -c C:\Work\listman.cli.release\Config\listman.sharepoint.json
```
### Stop Service
To stop the service use

```sh
sc stop ListmanService
```

### Delete Service
To delete the service use

```sh
sc delete ListmanService
```

## Configure Listman.io
Now after we learned how to run the Listman.io let's have a look at the simple Listman.io config file. 

In that example will run one archiving job immediately after the application start and archive all the items from the "list2" on the https://listman.sharepoint.com/ SharePoint instance into the `list1_archive.csv` file. All the attachment will be downloaded into the `attachments` folder. 

The config file has some other additional parameters like what columns to archive, **filtering condition** to decide which list items to archive/export and post action that has to be invoked against already archived/exported records (like remove record or modify some of its fields).

```js
{
  connectTo: {
    email: "listman.io@gmail.com",
    siteUrl:"https://listman.sharepoint.com/",
    clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
    clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
  },
  archiveJobs: [
    {
      jobName: "Job 1",
      listName: "list2",
      filterRecordsBy: {
        columnName: "Archived",
        equalBool: false
      },
      exportColumns: ["Title", "col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
      exportAttachments: true,
      recordAction:{
        remove: true
      },
      archiveTo: {
        csvFile: "C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv",
        attachmentsFolder: "C:\\Work\\listman.cli\\listman-cli\\attachments",
        addHeaderToCSV: true,
        appendRecordsToCSV: false
      },
      schedule: {
        runImmidiate: false,
        runUsingCron: "0 0/2 * * * ?"
      },
      batchSize: 200
    }
  ]
}
```

Don't panic and bear with us, we will explain all the sections and corresponding options below.

### How To Verify and Validate Config File
You could always validate your configuration by running the app with the following command parameters:

```sh
> listman-cli.exe -v -p -s
```
or for config file in a custom location:
```sh
> listman-cli.exe -c "\path\to\config.json" -v -p -s
```

That command will:
1. `-p` - Parse and validate config file syntax
2. `-v` - validate your license details
3. `-s` - connect to to Sharepoint using `siteUrl` and App-Only credentials

We recommend to run this command every time you make significant changes to your config file to catch and debug any unexpected configuration and syntax errors.

Now let's look on the all configuration sections in details.

### `connectTo` section

`connectTo` section is used to provide your sign in email, siteUrl and app-only authorization details:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `email` | Your Microsoft Account email used to sign in on www.listman.io  | aershov24@gmail.com |
| `siteUrl` | Url of your Sharepoint Instance  | https://listman.sharepoint.com |
| `clientId` | Client Id generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `fe26fe8a-60b9-4523-996e-3e5ac2596e9f` |
| `clientSecret` | Client Secret generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI=` |

**Example**:
```js
connectTo: {
  email: "listman.io@gmail.com",
  siteUrl:"https://listman.sharepoint.com/",
  clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
  clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
}
```

### `archiveJobs` section
Listman.io supports running multiple archiving jobs at the same time or by CRON schedule. You have to add all the job configurations into the `archiveJobs` section (that is an array of JSON objects) of the config file:
```js
archiveJobs: [
 {
  ...Job #1 config
 }, {
  ...Job #2 config
 }
]
```

An `archiveJobs` object may contain the following properties and subsections:

| Field/Subsection  | Description | Example |
| ------------- | ------------- | -----------------|
| `jobName` | Name of the job. Used for logging.  | Customers Archiving - May 2019 |
| `listName` | The title of a SharePoint list to archive/export | `customers` |
| `exportColumns` | List of column titles for archiving or export as JSON array of strings. | `["Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"]` |
| `exportAttachments` | Download list attachments. Default is `true`. | `true` or `false` |
| `batchSize` | When Listman.io gets list data from Sharepoint lists it iterates through the list's data in batches or pages. The default `batchSize` value is `500`. We recommend to keep this value as 500 or lower if you have slow or unstable Internet connection | `500` |
| `filterBy` | This subsection is used to filter specific list records for archiving or export. You could specify what list records to archive or export using a criteria. Don't use that field or set it's value to `null` if you want to archive/export **all list items**. Default is `null`. | See [Filter By configuration]() for details |
| `recordAction` | You may want to delete or modify some fields of a record from the list after archiving. This subsection is used to configure post archive action for the record. | See [Record Action configuration]() for details |
| `archiveTo` | This section is used to specify properties of the archiving or export output files like file path, adding header and file write modes like `append` or `rewrite` | See [Archive To configuration]() for details |
| `schedule` | This section is used to specify job run schedule. Basically you could run jon immediately after application launch or by schedule using cron syntax. | See [Schedule configuration]() for details |

#### `exportColumns` field
`exportColumns` field should contain a list of column titles for archiving or export as JSON array of strings. Note that `ID` and `GUID` of the item will be always presented in the output CSV file. To export all columns you could use special `*` shortcut (see example below).

> SharePoint list columns have three different names: Column Name (or Title), InternalName and StaticName. In the `exportColumns` list you have to provide list of  **Column Names**. The Listman.io automatically will find InternalNames of the columns for CSOM operations. You could find all column names for the list on a view list settings page.

**Example:**
```js
exportColumns: ["Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
```
or to export **all** columns:
```js
exportColumns: ["*"],
```

#### `filterBy` subsection

`filterBy` subsection is used to specify a simple equality condition under which record from the SharePoint list will be marked for archiving or export. Condition could be specified just for one column that has `number`, `string`, `bool`, `currency` or `datetime` type.

> If you want to archive/export all list items without filtering just **don't** provide `filterBy` in your config file.

For example let's say you have a list of `Articles` with columns `State (string)`, `Published (boolean)`, `Published Date (datetime)` and `Price (currency)`. 

If you want to archive all the records that were `Published` use that condition (note `null` values):
```js
filterBy: {
  columnName: "Published",
  equalBool: true
}
```

Or if you want to archive all the records that have `Published Date` older than 30 days:
```js
filterBy: {
  columnName: "PublishedDate",
  olderThanDays: 30
}
```

Or if you want to archive all the records that have `State` is equal `Processed Successfully` :
```js
filterBy: {
  columnName: "PublishedNote",
  equalStr: "Processed Successfully",
}
```

Or if you want to archive all the records that have `Price` is equal `$100.99` :
```js
filterBy: {
  columnName: "Price",
  equalDouble: 100.99,
}
```

##### `filterBy` with SharePoint Conditional Columns
Currently Listman.io doesn't support complex logical conditions (like `and` or `or`) on multiple set of fields. In case if you list has multiple archiving condition you could either 

1. run multiple jobs to archive records based on different conditions (that will be equal the `or` logical operator)

2. create a new calculated column using SharePoint formulas (read more about conditional columns [here](https://support.office.com/en-us/article/examples-of-common-formulas-in-sharepoint-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3))

If you decided to create a new conditional columns for `filterBy` we recommend you to use the following formula syntax:
```sh
=IF([Column1]<=[Column2], "ARCHIVE", "DON'T ARCHIVE")
```
or in case of ranges:
```sh
=IF(AND([Column1]> 50, [Columns1] < 100), "ARCHIVE", "DON'T ARCHIVE")
```

In that case you could just use string equality condition, aka `equalStr`:
```js
filterBy: {
  columnName: "ConditionalColumn",
  equalStr: "ARCHIVE",
}
```


| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `columnName` | Column to apply condition to. Column has to have either `string` or `bool` or `DateTime` types  | "Published" |
| `equalDouble` | Conditional value to match current value of the `currency` type column to. The record will be marked for archiving if values are equal. Note absence of any currency sign. | `98.99` |
| `equalInt` | Conditional value to match current value of the `number` type column to. The record will be marked for archiving if values are equal. | `12` |
| `equalStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if values are equal. | "Processed Successfully" |
| `containStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if field contains conditional value. | "_London" |
| `equalBool` | Conditional value to match current value of the `bool` type column to. The record will be marked for archiving if values are equal. | `true` or `false` |
| `olderThanDays` | Conditional value to match current value of the `datetime` type column to. The record will be marked for archiving if column value are older than `olderThanDays` days. | `30` |

#### `recordAction` subsection

Once list record is archived or exported you may want to delete it or modify some of its fields. The `recordAction` subsection is designed to configure post archive action applied to the archived record.

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `remove` | remove list item after archiving, `false` by default  | `true` |
| `modify` | List of modifications (JSON array) for one or more list item fields after archiving, `null` by default | `true` |

`modify` is a JSON array that contains configuration for one or more list fields to edit:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `columnName` | Column to modify. Make sure you also have this column specified in `exportColumns` array  | `true` |
| `setIntValue` | set number value, `null` by default | `-1` |
| `setDoubleValue` | set currency value, `null` by default | `99.89` |
| `setStrValue` | set string or choice value, `null` by default | `Choice 2` |
| `setBoolValue` | set boolean value, `true` or `false`, `null` by default | `true` |
| `setCurrentDateValue` | set current datetime value for DateTime type column, `null` by default | `true` |

> You could specify multiple modifications for one list record (see an example below). Make sure you use the right `set*Value` property for and set all others to `null`.

**Example**:
In this example archived record would not be removed from the list. After archiving two of its fields will be modified:
* `Choice` field will be set to `Choice 2`
* `Archived` field will be set to `true`
* `ArchiveDate` field will be set to the current date 

```js
recordAction:{
  remove: false,
  modify: [
     {
      columnName: "Choice",
      setStrValue: "Choice 2",
    },
    {
      columnName: "Archived",
      setBoolValue: true,
    },
    {
      columnName: "ArchivedDate",
      setCurrentDateValue: true
    }
  ]
},
```

#### `archiveTo` subsection

 `archiveTo` section is used to specify properties of archive or export output files and folders. 

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `csvFile` | The output CSV file  | `C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv` |
| `attachmentsFolder` | The output folder for downloaded attachments. For list each attachment will be downloaded into a separate subfolder named by Item ID. Only latest version of each document will be downloaded. | `C:\\Work\\listman.cli\\listman-cli\\attachments` |
| `addHeaderToCSV` | Add columns header to the CSV file. `true` by default. | `true` |
| `appendRecordsToCSV` | Overwrite or append archived records into the CSV file if it exists. `true` by default. | `true` |

**Example**:
```js
archiveTo: {
  csvFile: "C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv",
  attachmentsFolder: "C:\\Work\\listman.cli\\listman-cli\\attachments",
  addHeaderToCSV: true,
  appendRecordsToCSV: false
}
```

#### `schedule` section
Listman.io could run archiving jobs by schedule. Basically you could run job immediately after application launch or by schedule using `cron` syntax. 

> If you not familiar with `cron expressions` read this [article](https://www.quartz-scheduler.net/documentation/quartz-3.x/tutorial/crontriggers.html). You could also use this `cron expression` [builder](http://www.cronmaker.com/) for expressions construction and validation.

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `runImmediate` | Run the job immediate after application start. Default is `true`  | `true` |
| `runUsingCron` | Run the job using cron expression. For example, run the job every 1 hour starting at 12 am every day or run the job each first day of each month at 12 am | `0 0 0/1 1/1 * ? *` or `0 0 12 1 1/1 ? *` |

**Example:**
Run the job **immediately** after start:
```js
schedule: {
  runImmediate: true,
  runUsingCron: null
}
```
or
run the job **each first day of each month at 12 am**:
```js
schedule: {
  runImmediate: false,
  runUsingCron: "0 0 12 1 1/1 ? *"
}
```

## Note on Logging
Listman.io has several layers of logging:
1. Console logging. You usee it only when Listman.io is run as a console app.
2. Logging into `troubleshooting.log` file in the application folder. That logging is used only for troubleshooting and debuging.
3. Logging into a `log.csv` file. That is the log you should prefer to analyze first.

> **Why Listman.io use CSV files for logging and not the simple txt format?** The answer is the Asyncronical execution of Archiving Jobs doesn't play well with text logs. 

Let's say you run archiving for two large list nearly in the same time. When log into a simple txt file logging messages from different Archiving Jobs can't be easily grouped and analysed. On the other hand CSV file could be opened in Microsoft Excel and filtered to display the log messages just from a particular Job or Action (download, delete, edit). It's especially usefully if you have multiple archiving jobs running at the same day.

## Command Line Parameters
Listman.io app could be run with the following parameters:

| Short Parameter  | Long Parameter | Default Value | Description |
| ------------- | ------------- |  --| -- |
| `-c path\to\config\file`| `--config path\to\config\file` | `./config.json` | Path to config file |
| `-v`| `--verbose` | `false` | Activate detailed (verbose) logging |
| `-p`| `--parse` | `false` | Parse and validate config file without jobs run |
| `-l`| `--license` | `false` | Validate user license without jobs run  |
| `-s`| `--server` | `false` | Test connection to SharePoint Server|
| `-n`| `--cron` | `false` | Validate Cron Expressions for jobs |
| `-t`| `--test` | `false` | Run archive/export jobs in testing mode (without actual data transfer and items modification) |

## How to Get Help
If you have any troubles with running or configuring Listman.io there is several channels where you could get help:
1. Read this manual (again)
3. In case of any runtime errors (exceptions) look at the `app folder\troubleshooting.log` file for detailed `Exception Stack Trace` and try to fix your config file or environment
2. Browse [All The Issues](https://github.com/listman-io/docs/issues?utf8=%E2%9C%93&q=) that have been already asked and closed
5. [Create a new Issue](https://github.com/listman-io/docs/issues) using this Github repo
6. Send us a support request to [support@listman.io](mailto:support@listman.io)
