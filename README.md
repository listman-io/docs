# Listman.io Docs

**Listman.io** is a simple yet powerfully Windows Service/console application that helps organizations archive or export data and attachments from any SharePoint lists of any size without annoying [5000 list view threshold](https://docs.microsoft.com/en-us/sharepoint/support/lists-and-libraries/items-exceeds-list-view-threshold) into **CSV** files.

#### Table of Contents  
[Getting Started](#Getting-Started)</br>
[System Requirements](#System-Requirements-And-Prerequisites)</br>
[Download the App](#Download-the-App)</br>
[Free vs Enterprise Plan](#Understanding-the-Free-vs-Enterprise-Plan)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Note on SharePoint Instance](#Note-on-Sharepoint-Instance)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Get Free Plan Licence Details](#Get-Your-Free-Licence-Details)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Subscribe to Enterprize Plan](#How-to-Register-Enterprise-Version)<br/>
[Create SharePoint Application (for App-Only/Application Context)](#create-sharepoint-application-app-onlyapplication-context)</br>
[Quick Start Guide](#Quick-Start-Guide)</br>
[Run as Console Application](#Run-as-Console-Application)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Run in Test Mode](#Run-in-Testing-Mode)</br>
[Run as Windows Service](#Run-as-Windows-Service)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Install Service](#Install-Service)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Start Service](#Start-Service)</br>
[Configure Listman.io](#Configure-Listmanio)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Config Files Samples](#Config-File-Samples)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Verify and Validate Config File](#How-To-Verify-and-Validate-Config-File)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Licence configuration](#Licence-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Connect configuration](#Connect-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Logging configuration](#Logging-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Archive Job Configuration](#Archive-Job-Configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Export Columns configuration](#Export-Columns-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Filter By configuration](#Filter-By-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Record Action configuration](#Record-Action-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Archive To configuration](#Archive-To-configuration)</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Schedule configuration](#Schedule-configuration)</br>
[Command Line Parameters](#Command-Line-Parameters)</br>
[How To Get Help](#How-to-Get-Help)</br>

## Why Your Business May Need Listman.io?

In short, Listman.io will allow your company to run business more efficiently and:

1. Save money on custom SharePoint development (around one-two months of a developer salary), application support and maintenance 
2. Avoid 5000 view and search limitation threshold for the large lists in SharePoint by removing historical data
3. Reduce hosting costs by offloading unused attachments into the file system or any cloud storage including OneDrive, Dropbox, Google Drive or Azure Storage
4. Improve overall system speed and responsiveness 
5. Comply and implement organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Back up old data for the peace of mind
8. Transfer or export lists data from SharePoint into any DB including MS SQL Server or Azure Database
8. And finally, configure and run archiving or exporting procedures in no time without any custom development (around 30 mins after simple configuration)

And if you are a SharePoint Consulting Microsoft Partner Listman.io will help you to implement client-side projects with better profit margin by saving money on custom archiving/export/migration requirements development.

### Why Archive/Export to CSV?
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
2. Listman.io is a Windows application that could be run as command line application or Windows Service. To run it you must have Windows 7/8/10/Server system installed on one of your local machines or cloud VM. For simplicity we will reference to the machine when Listman.io is running as the **application server**.
3. You have .NET Framework 4.5 installed on the application server. **Note:** .NET Core is not yet supported*.
4. Your application server is connected to the Internet. Without the internet connection the Listman.io app wouldn't be able to verify your *licence* and will fail to run archiving or export jobs.
5. Ideally you have to have some knowledge of JSON files, usage of Windows Command Line and Windows Services, and specifically `sc` command.

> **\* What about .NET Core?** Unfortunately by the time of application implementation Microsoft didn't yet release .NET Standart CSOM libraries compatible with .NET Core runtime environment. We will keep our eye on that matter and plan to implement .NET version of the Listman.io app as soon as CSOM will be available for .NET Core.

## Download the App
Listman.io app distributed as `zip` archive and don't need any additional installation except unzipping. It's very easy to download a copy of the Listman.io application:

1. Go to [www.listman.io](https://www.listman.io)
2. **Sign In** with your Microsoft Account. After successfully Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard)
3. Click on Download the Listman.io

Alternatively you could download the latest and all the previous versions of the Listman.io application using that [link](https://github.com/listman-io/docs/packages) from the Github. 

> **Note:** Even if the app is downloaded from the Github you still need to Sign In with your Microsoft account on [www.listman.io](https://www.listman.io) to obtain your free plan licence details.

Congratulations! Now you are ready to run and configure the Listman.io app. But first let's understand different Listman.io Plans.

## Understanding the Free vs Enterprise Plan
Listman.io is a **commercial software** but purposely designed to be run in a free mode for better learning and assessment experience. There is **no trial** so you have unlimited time to make sure Listman.io fits all your organization archiving or exporting needs. 

We recommend you to start run Listman.io using a Free Plan and first learn how to archive/export data from your Development or Staging SharePoint servers. Once confident with app configuration you could easily [subscribe to the Enterprise Plan]() and make the most from your archiving or exporting procedures.

> Free version is limited to archive or export only 100 records from one SharePoint Instance per month. You could have just one free plan for your account. If you want to archive or export more than 100 records monthly we recommend you to upgrade to Enterprise Plan. Enterprise Plan also includes 24/7 priority support.

Look at the table below to choose between Free or Enterprise plans.

| Listman.io Feature  | Free Plan | Enterprise Plan |
| ------------- | ------------- | -----------------|
| Unlimited sites |  ✅ |  ✅ |
| Unlimited jobs |  ✅ |  ✅ |
| Support large lists archiving/exporting (over 5000 threshold)   |  ✅ |  ✅ |
| Modify list items after archiving/export |  ✅ |  ✅ |
| Delete list items after archiving/export |  ✅ |  ✅ |
| Download attachments |  ✅ |  ✅ |
| Run as CLI |  ✅ |  ✅ |
| Run as Windows Service |  ✅ |  ✅ |
| Cron Scheduler |  ✅ |  ✅ |
| Email Support |  ✅ |  ✅ |
| Priority Support |  ❌ |  ✅ |
| Records archiving/export per month |  100 |  ♾️, No Limit |
| Cost |  Free |  $69 / per month / per SharePoint Instance |

### Note on Sharepoint Instance
Let's assume that your root SharePoint site is accessible by the URL address (also known as `siteUrl`): 

```sh
https://listman.sharepoint.com/
```

We will call that unique installation of SharePoint Server as **SharePoint Instance**. Your SharePoint Instance could have multiple sites and lists.

### Get Your Free Licence Details

To run the Listman.io application for the first time you have to know your *licence* details. We define **licence** as a set of:

* SignIn email (like `peter.pan@gmail.com`)
* SharePoint host (like `demo`, `listman.sharepoint.com` or `localhost`)
* AppKey (like `231231412`)

To get your Free Plan licence details:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). Note your Microsoft Account email. You'll need it on the configuration step.
3. Go to Subscriptions section and note the following details:
 * Your Microsoft Account `email`
 * Host name: `demo`
 * AppKey: `get it from subscription`

Now we ready to create your first SharePoint Application (also known as Application Context or App-Only) that will be used to authorize Listman.io app against your Sharepoint Instance. 

### How to Register Enterprise Version

If you are a new user of Listman.io you could skip this section and circle back to it later after trying Listman.io app by using a Free Plan.

If you want to run archiving procedure on a full scale **without 100 records per month limitation** you have to subscribe to an Enterprise plan:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). Note your Microsoft Account email. You'll need it on the configuration step.
3. Go to Billing details section and add details of your credit or debit card. 
4. Click **Update**. Make sure there is no errors once billing details are updated. 
5. You could always change your billing details in the future. Just type a new card details and click on **Update**.
> **Note:** we never store your billing detail on our servers. All the billing information and payments processed by Stripe. 
3. Once billing details are added, go to Subscriptions section
4. Click on **Add Subscription**
5. Type name of the new SharePoint `host` you want to archive or export data from like `listman.sharepoint.com` or `localhost`. If you host is accessible only by IP address or localhost type them as they are. **Do not type port**.
6. Click on **Save**. Now your Subscription is created but not yet activated.
7. Check your licence details, note generated `AppKey` and click on **Activate** button. Now your subscription and you could use `host` and `appKey` in your config file (see section...). 

> **Note**: you can't change the **host** after subscription is activated so make sure to thoroughly check your details.
8. You could delete an active subscription at any time. 

> **Note**: Listman.io doesn't support to *Pausing* a subscription.

9. If you need to archive or export lists from multiple SharePoint Instances available on different hosts you have to create a dedicated subscription for each host.

> Once subscription is activated your card will be billed immediately. Make sure you have sufficient funds available on your card each month so your subscription will stay active.

### **`siteUrl` vs `host`** 
Your SharePoint Instance is usually available via urls like:
 * `https://listman.sharepoint.com`, 
 * `https://localhost:4545` or even 
 * `https://192.123.23.12`. 
 
 That url is also known as `siteUrl` and used by Listman.io to establish connection with SharePoint Instance (using CSOM). We define `host` for `siteUrl`s as 
 * `listman.sharepoint.com`, or
 * `localhost`, or
 * `192.123.23.12` (note the absence of a port number). 
 
 When Listman.io app is running we match the `siteUrl` with the `host` from the licence details provided in the config file and throwing an error if there is any difference.
 
 > **Note**: `demo` is a special type of host used for the Free Plan licence details so the Listman.io app could be run in demo mode for any `siteUrl` but with **100 records per month limitation**.

## Create SharePoint Application (App-Only/Application Context)

Now let's create your first SharePoint Application (also known as Application Context or App) that will be used to authorize Listman.io app against your Sharepoint Instance. 

To make sure Listman.io app will have an access to all the lists and lists attachments we have to create an Application Context (or App-Only) and grant it the `tenant` permissions. You could [read](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azureacs) about that procedure in more details on Microsoft Documentation Portal.

To create Application Context for the Listman.io app:

1. Make sure you have an admin access to your Sharepoint Instance
2. Go to `https://listman.sharepoint.com/_layouts/15/appregnew.aspx`
3. Type the new application details in the form and click **Create**:
 * Client Id: click on **Generate**
 * Client Secret: click on **Generate**
 * Title: listman.io
 * App Domain: www.listman.io
 * Redirect Url: https://www.listman.io
 * Click Create
4. You'll see the message:

```
The app identifier has been successfully created.
Client Id:  	b74101eb-cbec-4096-ac08-b61bdbcfdb58
Client Secret:  qhl9N9GCgJ11+Phh6WNhm39l+64ZlJRRm06wcQ2iJF4=
Title:  	listman.io
App Domain:  	www.listman.io
Redirect URI:  	https://www.listman.io
```
5. Note the `Client Id` and `Client Secret` and write them down somewhere
6. Now go to `https://listman-admin.sharepoint.com/_layouts/15/appinv.aspx`
> Note the `-admin` in the URL! It' very important!
7. Copy `Client Id` from the step 5 into the "App Id and Title" field
8. Click on **Lookup**
9. Note the app details from the step 3 will appear in the form
10. Fill up the field `App's Permission Request XML` with the following XML:
```xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```
> In that example we specify scope as `Tenancy` so the `FullControl` right will be applied to all children (sites, lists) of this scope. Based on your requirements you could change that scope to Site Collection, Website or individual Lists. Reference to [Microsoft Documentation](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/add-in-permissions-in-sharepoint) for more details on that topic.

11. Click **Create**
12. You'll see the following Page:

13. Click on **Trust It**.

Great! Now we are ready to run Listman.io for the first time and make sure we could connect to your SharePoint Instance.

## Quick Start Guide
1. Download the Listman.io application from your Dashboard or from Github if you haven't done it before.
2. Unpack the archive into a folder from which you want to run the application. We will reference to this folder as the **app folder** for simplicity.
3. Navigate to **app folder** using Windows Explorer
4. Open the sample `config.json` file in any text editor of your choice
5. Edit the `config.json` file. Change the fields to your specific values and **Save** the file:

```json
useLicence: {
  email: "your_sign@in_email.com",
  host: "demo",
  appKey: "copy_from_dashboard"
},
connectTo: {
  siteUrl:"https://yourcompany.sharepoint.com/",
  appId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
  appSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
},
```
6. Open Windows Command Line
7. Navigate into the **app folder**, for that use the command:
```sh
> cd /d app_folder
``` 
8. Run the Listman.io app with the following command line parameters:
```sh
> listman-cli.exe -p -l -s
``` 
Where:
* `-p` - parameter used to validate config file
* `-l` - parameter used to validate user licence
* `-s` - parameter used to test the connection to Sharepoint using `siteUrl` and App-Only credentials
9. Check the results. Note that:
 * you free plan details are valid, for that make sure you see the message
 ```
 Licence successfully validated: Free plan 
 ```
 * the app could connect to the SharePoint instance, for that make sure you see the message
 ```
 Successfully connected to: https://yourcompany.sharepoint.com/
 ```

Good job! Now let's learn what are some different ways to run the Listman.io app. 

## Run as Console Application

Before running Listman.io app against your production SharePoint Instance we recommend you to *always* un the app in a test mode.

### Run in Test Mode
Test mode allows you to start Listman.io app, validate config file, connect to SharePoint Instance and iterate through the list items without actual archiving deletion, modification and attachments download. It's designed to battle test your configuration as close as possible to the actual production run including logs creation to verify all the expected records were correctly marked for archiving.

To run application in testing mode run the app with the  `-p` and `-t` parameter:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -p -t
```

You could combine `-p`, `-t` and `-v` parameters for detailed logging:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -p -t -v
```

### Run the App
To simply run Listman.io as a console app `cd` to **Application Folder** and run:
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
Now after we learned how to run the Listman.io application let's have a look at the simple Listman.io config file. 

In that example will run one archiving job immediately after the application start and archive all the items from the "list2" on the https://listman.sharepoint.com/ SharePoint instance into the `list1_archive.csv` file. All the attachment will be downloaded into the `attachments` folder. 

The config file has some other additional parameters including logging, what list columns to archive, **filtering condition** to decide which list items to archive and post action that has to be invoked against already archived record (like remove record or modify some of it's fields).

```json
{
  useLicence: {
    email: "aershov24@gmail.com",
    host: "demo",
    appKey: "123"
  },
  connectTo: {
    siteUrl:"https://listman.sharepoint.com/",
    clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
    clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
  },
  logTo:{
    csvLogFile: "C:\\Work\\listman.cli\\listman-cli\\log.csv"
  },
  archiveJobs: [
    {
      name: "Job 1",
      list: "list2",
      filterRecordsBy: {
        columnName: "Archived",
        equalStr: null,
        equalBool: false,
        olderThanDays: null
      },
      exportColumns: ["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
      exportAttachments: true,
      recordAction:{
        remove: true,
        modify: null
      },
      archiveTo: {
        file: "C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv",
        attachmentsFolder: "C:\\Work\\listman.cli\\listman-cli\\attachments",
        addHeader: true,
        append: false
      },
      schedule: {
        runImmidiate: false,
        runUsingCron: "0 0/2 * * * ?"
      },
      batchSize: 100
    }
  ]
}
```

Don't panic and bear with us, we will explain all the sections and corresponding options below.

### Config File Samples
If you like to learn based on examples you could find several predefined config files in the [Config File Examples]() folder. That config files will help you to learn how to:
* Run Multiple Archiving Jobs
* Use strings equality Filtering Criteria
* Use boolean equality Filtering Criteria
* Use "older that N days" Filtering Criteria
* Export All Items From The List (no Filtering criteria)
* Download All List Item Attachments
* Modify single or multiple list item columns after Archiving/Export
* Run app using different Cron Schedules:
 * run every day
 * run once per month
 * run every 6 hours
 * run every 3 months

### How To Verify and Validate Config File
You could always validate your configuration by running the app with the following command parameters:

```sh
> listman-cli.exe -c "config.json" -v -p -s
```

That command will:
1. `-p` - Parse and validate config file syntax
2. `-v` - validate your licence details
3. `-s` - connect to to Sharepoint using `siteUrl` and App-Only credentials

We recommend you to run this command every time you make significant changes to your config file to catch and debug any unexpected configuration and syntax errors.

Now let's look on the all configuration sections in details.

### Licence configuration
`useLicence` section is used to provide details about your free or Enterprise plan licence:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `email` | Your Microsoft Account email used to sign in on www.listman.io  | aershov24@gmail.com |
| `host` | Sharepoint Instance host (domain) name or `demo` for free plan | `demo` for free plan or `yourcompany.sharepoint.com` for Enterprise Plan |
| `appKey` | Application Key generation on your Dashboard for particular host (including `demo`)  | 123123123123123123123 |

**Example**:
```json
useLicence: {
  email: "aershov24@gmail.com",
  host: "demo",
  appKey: "123"
}
```
**Errors**:
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Licence validation failed: No user found` |  |
| `Licence validation failed: No host found` |  |
| `Licence validation failed: AppKey is invalid` |  |
| `Licence validation failed: Subscription is not active` |  |

### Connect configuration

`connectTo` section is used to define url of the Sharepoint INstance for connection as well as app-only authorization details:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `siteUrl` | Url of your Sharepoint Instance  | https://listman.sharepoint.com |
| `clientId` | Client Id generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `fe26fe8a-60b9-4523-996e-3e5ac2596e9f` |
| `clientSecret` | Client Secret generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI=` |

**Example**:
```json
connectTo: {
  siteUrl:"https://listman.sharepoint.com/",
  clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
  clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
}
```
**Errors**:
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Required property 'appSecret' not found in JSON. Path 'connectTo', line 10, position 2.`| Check that you provided `siteUrl`, `clientId` and `clientSecret` in the config file |
| `The remote name could not be resolved: 'accounts.accesscontrol.windows.net'`| Check your internet connection and make sure you could connect `siteUrl` from the applcaition server including firewall settings |
| `Token request failed. The remote server returned an error: (400) Bad Request.` | Check your `clientId` is valid |
| `Token request failed. The remote server returned an error: (401) Unauthorized.` | Check your `siteUrl` and `clientSecret` are valid |

### Logging configuration
Listman.io has several layers of logging:
1. Console logging. You usee it only when Listman.io is run as a console app.
2. Logging into `troubleshooting.log` file in the application folder. That logging is used only for troubleshooting and debuging.
3. Logging into a custom CSV file. That is the log you should prefer for everyday use.

The `logTo` section is used to configure the logging into the CSV file and fairly simple to understand:
```json
logTo:{
 csvLogFile: "C:\\Work\\listman.cli\\listman-cli\\log.csv"
}
```

> **So why Listman.io use CSV files for logging and not the simple txt format?** The answer is the Asyncronical execution of Archiving Jobs doesn't play well with text logs. 

Let's say you run archiving for two large list nearly in the same time. When log into a simple txt file logging messages from diffrent Archiving Jobs can't be easily grouped and analised. On the other hand CSV file could be opened in Microsoft Excel and filtered to display the log messages just from a particular Job or Action (download, delete, edit). It's especially usefull if you have multiple archiving jobs running at the same day.

### Archive Job Configuration
Listman.io supports running multiple archiving jobs at the same time or by schedule. You have to add all the job configurations into the `archiveJobs` section (that is an array of JSON objects) of the config file:
```json
archiveJobs: [
 {
  ...Job #1 config
 }, {
  ...Job #2 config
 }
]
```

An archive job configuration may contain the following properties and subsections:

| Field/Subsection  | Description | Example |
| ------------- | ------------- | -----------------|
| `name` | Name of the job. Used for logging.  | Customers Archiving - May 2019 |
| `list` | The title of a SharePoint list to archive | `customers` |
| `exportColumns` | List of column titles for archiving or export as JSON array of strings | `["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"]` |
| `exportAttachments` | Do we need to export attachments as well (true/false). Default is `false`. | `true` or `false` |
| `batchSize` | When Listman.io gets list data from Sharepoint lists it iterates through the list's data in batches or pages. The default `batchSize` value is `500`. We recommend to keep this value as 500 or lower if you have slow or unstable Internet connection | 500 |
| `filterRecordsBy` | You could specify what list records to archive or export using a simple equality criteria. This subsection is used to filter specific list records for archiving or export. | See [Filter By configuration]() |
| `recordAction` | You may want to delete or modify some fields of a record from the list after archiving. This subsection is used to configure post archive action for the record. | See [Record Action configuration]() |
| `archiveTo` | This section is used to specify properties of the archiving or export output files like file path, adding header and file write modes like `append` or `rewrite` | See [Archive To configuration]() |
| `schedule` | This section is used to specify job run schedule. Basically you could run jon immediately after application launch or by schedule using cron syntax. | See [Schedule configuration]() |

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Can't find the list with the Title`| Check your list title |
| `Export Columns list should contain at least ID and GUID columns`| Check your export columns list |

#### Export Columns configuration
`exportColumns` field should contain a list of column titles for archiving or export as JSON array of strings. Note that `ID` and `GUID` are mandatory columns and have to be presented in the `exportColumns` list.

> SharePoint list columns have three different names: Column Name (or Title), InternalName and StaticName. In the `exportColumns` list you have to provide list of  **Column Names**. The Listman.io automatically will find InternalNames of the columns for CSOM operations. You could find all column names for the list on a view list settings page.

**Example:**
```json
exportColumns: ["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
```

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `No ID column found`| Check that list contains "ID" column name |
| `No GUID column found`| Check that list contains "GUID" column name |
| `No "Column Name" found`| Check that list contains "Column Name" |

#### Filter By configuration

`filteredBy` subsection is used to specify a simple equality condition under which record from the SharePoint list will be marked for archiving or export. Condition could be specified just for one column that has `number`, `string`, `bool`, `currency` or `datetime` type. 

For example let's say you have a list of `Articles` with columns `State (string)`, `Published (boolean)`, `Published Date (datetime)` and `Price (currency)`. 

If you want to archive all the records that were `Published` use that condition (note `null` values):
```json
filterBy: {
  columnName: "Published",
  equalBool: true
}
```

Or if you want to archive all the records that have `Published Date` older than 30 days:
```json
filterBy: {
  columnName: "PublishedDate",
  olderThanDays: 30
}
```

Or if you want to archive all the records that have `State` is equal `Processed Successfully` :
```json
filterBy: {
  columnName: "PublishedNote",
  equalStr: "Processed Successfully",
}
```

Or if you want to archive all the records that have `Price` is equal `$100.99` :
```json
filterBy: {
  columnName: "Price",
  equalDouble: 100.99,
}
```

##### `filterBy` with Conditional Columns
Currently Listman.io doesn't support complex logical conditions (like `and` or `or`) on multiple set of fields. In case if you list has multiple archiving condition you could either 

1. run multiple jobs to archive records based on different conditions (that will be equal the `or` logical operator)

2. create a new calculated column using SharePoint formulas (read more about conditional columns [here](https://support.office.com/en-us/article/examples-of-common-formulas-in-sharepoint-lists-d81f5f21-2b4e-45ce-b170-bf7ebf6988b3))

If you decided to create a new conditional columns for `filterBy` we recommend you to use the following formula syntax:
```sh
=IF([Column1]<=[Column2], "ARCHIVE", "DON'T ARCHIVE")
```

In that case you could just use string equality condition, aka `equalStr`:
```json
filterBy: {
  columnName: "ConditionalColumn",
  equalStr: "ARCHIVE",
}
```


| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `columnName` | Column to apply condition to. Column has to have either `string` or `bool` or `DateTime` types  | Published |
| `equalDouble` | Conditional value to match current value of the `currency` type column to. The record will be marked for archiving if values are equal. Note absence of any currency sign. | `98.99` |
| `equalInt` | Conditional value to match current value of the `number` type column to. The record will be marked for archiving if values are equal. | `12` |
| `equalStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if values are equal. | "Processed Successfully" |
| `containStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if field contains conditional value. | ` London ` |
| `equalBool` | Conditional value to match current value of the `bool` type column to. The record will be marked for archiving if values are equal. | `true` or `false` |
| `olderThanDays` | Conditional value to match current value of the `datetime` type column to. The record will be marked for archiving if column value are older than `olderThanDays` days. | 30 |

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Column value and conditional value have different types`| Check that `columnName` has `string`, `bool` or `datetime` type and the right condition column is chosen |

#### Record Action configuration

Once list record is archived or exported you may want to delete it or modify some of its fields. The `recordAction` subsection is designed to configure post archive action applied to the archived record.

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `remove` | remove record after archiving, `false` by default  | `true` |
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

```json
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

##### Note on Field Types
Listman.io support **filterBy** and **modify** conditions for the following types of list fields:
1. Integer, using `equalInt` or `strIntValue`
2. Text, using `equalStr` or `strStrValue`
3. Note, using `equalStr` or `strStrValue`
4. DateTime, using `olderThanDays` or `setCurrentDateValue`
5. Counter, using `equalInt` or `strIntValue`
6. Choice, using `equalStr` or `strStrValue`

#### Archive To configuration

 `archiveTo` section is used to specify properties of archive or export output files and folders. 

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `file` | The output CSV file  | `C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv` |
| `attachmentsFolder` | The output folder for downloaded attachments. Each attachment will be downloaded into a separate subfolder by Item ID | `C:\\Work\\listman.cli\\listman-cli\\attachments` |
| `addHeader` | Add columns header to the CSV file. `true` by default. | `true` |
| `append` | Overwrite or append archived records into the CSV file if it exists. `true` by default. | `true` |

**Example**:
```json
archiveTo: {
  file: "C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv",
  attachmentsFolder: "C:\\Work\\listman.cli\\listman-cli\\attachments",
  addHeader: true,
  append: false
}
```

#### Schedule configuration
Listman.io could run archiving jobs by schedule. Basically you could run job immediately after application launch or by schedule using `cron` syntax. 

> If you not familiar with `cron expressions` read this [article](https://www.quartz-scheduler.net/documentation/quartz-3.x/tutorial/crontriggers.html). You could also use this `cron expression` [builder](http://www.cronmaker.com/). 

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `runImmediate` | Run the job immediate after application start. Default is `true`  | `true` |
| `runUsingCron` | Run the job using cron expression. For example, run the job every 1 hour starting at 12 am every day or run the job each first day of each month at 12 am | `0 0 0/1 1/1 * ? *` or `0 0 12 1 1/1 ? *` |

**Example:**
Run the job **immediately** after start:
```json
schedule: {
  runImmediate: true,
  runUsingCron: null
}
```
or
run the job **each first day of each month at 12 am**:
```json
schedule: {
  runImmediate: false,
  runUsingCron: "0 0 12 1 1/1 ? *"
}
```

**Errors:**

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Cron expression is invalid`| Check your cron expression syntax. Use that [link](http://www.cronmaker.com/) to verify your cron expression. |

## Command Line Parameters
Listman.io app could be run with the following parameters:

| Short Parameter  | Long Parameter | Default Value | Description |
| ------------- | ------------- |  --| -- |
| `-c path\to\config\file`| `--config path\to\config\file` | `./config.json` | Path to config file |
| `-v`| `--verbose` | `false` | Activate detailed (verbose) logging |
| `-p`| `--parse` | `false` | Parse and validate config file without jobs run |
| `-l`| `--licence` | `false` | Validate user licence without jobs run  |
| `-s`| `--server` | `false` | Test connection to SharePoint Server|
| `-n`| `--cron` | `false` | Validate Cron Expressions for jobs |
| `-t`| `--test` | `false` | Run archive/export jobs in testing mode (without actual data transfer and items modification) |

## How to Get Help?
If you have any troubles with running or configuring Listman.io there is several channels where you could get help:
1. Read This (F*cking) Documentation. Especially look for the **Errors** sections on how to fix the root problems
3. In case of any runtime errors (exceptions) look at the `app_folder\troubleshooting.log` file for detailed `Exception Stack Trace` and try to fix your config file or environment
2. Browse [All The Issues](https://github.com/listman-io/docs/issues?utf8=%E2%9C%93&q=) that have been already asked and closed
3. Look at the [Config Files Examples folder]() for diffident configuration file samples
4. Watch our explanatory videos on the [Listman.io Youtube Channel]()
5. [Create a new Issue](https://github.com/listman-io/docs/issues) using this Github repo
6. Send us a support request on [support@listman.io](mailto:support@listman.io) with all the available details about your use case or errors
