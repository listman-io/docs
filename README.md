# Documentation

##### Table of Contents  
[Getting Started](#gettingStarted)

[Download the App](#download)  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[System Requirements](#sysReq)  

[Support](#support) 

<a name="gettingStarted"/>

## Getting Started
**Listman.io** is a simple yet powerfully Windows Service/console application that helps organizations archive or export data and attachments from any SharePoint lists of any size without annoying [5000 list view threshold](https://docs.microsoft.com/en-us/sharepoint/support/lists-and-libraries/items-exceeds-list-view-threshold) into **CSV** files.

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

### Why CSV?
Listman.io is built upon the principles of Unix philosophy and designed to *do one thing very well*, namely to archive and export SharePoint lists data into the CSV format files (comma delimited). We use CSV files as a final data destination because:

* CSV is understood by almost every piece of software on the planet (past and present)
* CSV is more human-readable than XML, JSON formats 
* CSV natively supported by Microsoft Excel
* CSV could be used as a source of import for almost any relational, document and graph DB including MS SQL Server and Microsoft Azure Database

So if you are looking to archive, export or migrate your SharePoint data into Microsoft SQL Server Database you could use Listman.io in conjunction with other ETL tools (for example custom SSIS packages or SQL Server Import and Export Wizard) to easily accomplish your goal delegating exporting data from SharePoint to the Listman.io.

<a name="sysReq"/>

## System Requirements And Prerequisites
Before start let's make sure your system complies with the following system requirements:

1. Listman.io is a Windows application that could be run as command line application or Windows Service. To run it you must have Windows 7/8/10/Server system installed on one of your local machines or cloud VM. For simplicity we will reference to the machine when Listman.io is running as the **application server**.
2. You have .NET Framework 4.5 installed on the application server. **Note:** .NET Core is not yet supported*.
3. Your application server is connected to the Internet. Without the internet connection the Listman.io app wouldn't be able to verify your application licence and will fail to run archiving or export procedures.
4. Ideally you have to have some knowledge of JSON files as well as usage Windows Command Line and Windows Services.
5. You have SharePoint 2013/2016/2019 or SharePoint Online.

> **\*What about .NET Core?** Unfortunately by the time of application implementation Microsoft didn't yet release .NET Standart CSOM libraries compatible with .NET Core runtime environment. We will keep our eye on that matter and plan to implement .NET version of the Listman.io app as soon as CSOM will be available for .NET Core.

<a name="download"/>

## Download the App
It's easy to download a copy of the Listman.io application. For that:

1. Go to [www.listman.io](https://www.listman.io)
2. **Sign In** with your Microsoft Account. After succesfull Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard)
3. Click on Download the Listman.io

Alternatively you could download the latest and all the previous versions of the Listman.io application using that [link](https://github.com/listman-io/docs/packages) from the Github. 

> **Note:** Even if the app is downloaded from the Github you still need to Sign In with your Microsoft account on [www.listman.io](https://www.listman.io) to obtain your free plan licence details.

Congratulations! Now you are ready to configure your first archiving or export procedure. But first let's look at different Listman.io Plans.

### What is Sharepoint Instance?
Let's assume that your SharePoint instance is accessible by the URL address (also known as `siteUrl`): 

```
https://listman.sharepoint.com/
```

We will call that unique copy of SharePoint system **SharePoint Instance**. Your SharePoint Instance could have multiple sites and lists.

### Free vs Enterprise Plans
Listman.io is a **commercial software** but purposely designed to be run in a free mode for better learning and assessment experience. There is **no trial** so you have unlimited time to make sure Listman.io fits all your organization archiving or exporting needs. 

We recommend you to start by running Listman.io using a Free Plan and try archive/export data from your Development or Staging SharePoint servers in order to familiarize yourself with the all application features. Once ready you could easily [subscribe to the Enterprise Plan]() and make the most from your archiving or exporting procedures.

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

Now we ready to create your first SharePoint Application (also known as Application Context or App) that will be used to authorize Listman.io console application or Windows service against your Sharepoint instance. 

### How to Register Enterprise Version

If you are a new user of Listman.io you could skip this section and circle back to it later after testing Listman.io app by using a Free Plan.

If you want to run archiving procedure on a full scale **without 100 records per month** limitation you have to subscribe to an Enterprise plan:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). Note your Microsoft Account email. You'll need it on the configuration step.
3. Go to Billing details section and add details of your credit or debit card. 
4.  Click **Update**. Make sure there is no errors once billing details are updated. 
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

Once subscription is activated your card will be billed immediately. Make sure you have sufficient funds available on your card each month so your subscription will stay active.

### **`siteUrl` vs `host`?** 
Your SharePoint Instance is usually available via urls like:
 * `https://listman.sharepoint.com`, 
 * `https://localhost:4545` or even 
 * `https://192.123.23.12`. 
 
 That url is also known as `siteUrl` and used by Listman.io to establish connection with SharePoint Instance (using CSOM). We define `host` for `siteUrl`s as 
 * `listman.sharepoint.com`, or
 * `localhost`, or
 * `192.123.23.12` (note the absence of any port number). 
 
 When Listman.io is running we match your `siteUrl` from the config file with the `host` from the licence details and throwing an error if there is any difference. 
 
 > **Note**: `demo` is a special type of host used for the Free Plan licence details so the Listman.io app could be run in demo mode for any `siteUrl` but with **100 records per month limitation**.

## Create SharePoint Application (App-Only/Application Context)

Now let's create your first SharePoint Application (also known as Application Context or App) that will be used to authorize Listman.io console application or Windows service against your Sharepoint instance. 

To make sure Listman.io app will have an access to all the lists and lists attachments on your SharePoint Instance we have to create Application Context (or App-Only) and grant it with the `tenant` permissions. You could [read](https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-apponly-azureacs) about that procedure in more details on Microsoft Documentation.

For that:

1. Make sure you have an admin access to your Sharepoint instance
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
5. Note `Client Id` and `Client Secret` and write them down somewhere
6. Now go to `https://listman-admin.sharepoint.com/_layouts/15/appinv.aspx`
> Note the `-admin` in the URL!
7. Copy `Client Id` from the step 5 into the "App Id and Title" field
8. Click on **Lookup**
9. Note the app details from the step 3 will appear in the form
10. Fill up the field `App's Permission Request XML` with the following XML:
```
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```
In that example we specify scope as `Tenancy` so the `FullControl` right will be applied to all children (sites, lists) of this scope. Based on your requirements you could change that scope to Site Collection, Website or individual Lists. Reference to [Microsoft Documentation](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/add-in-permissions-in-sharepoint) for more information.

11. Click **Create**
12. You'll see the following Page:

13. Click on **Trust It**.

Great! Now we are ready to run Listman.io for the first time and make sure we could connect to your SharePoint instance.

## Test Listman.io Connection
1. Download the Listman.io application from your Dashboard or from Github if you haven't done it before.
2. Unpack the archive into a folder from which you want to run the application. We will reference to this folder as the **app folder** for simplicity.
3. Navigate to `{app folder}\Config\` using Windows Explorer or window Command Line
4. Open the sample `config.json` file in any text editor of your choice
5. Edit the `config.json` file. Change the fields to your specific values and **Save** the file:

```
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
```
> cd /d {path_to_app_folder}
``` 
8. Run the Listman.io app with the following command line parameters:
```
> listman-cli.exe -c '\Config\config.json' -l -s
``` 
Where:
* `-l` - parameter used to validate user licence
* `-s` - parameter used to test the connection to Sharepoint using `siteUrl` and App-Only credentials
9. Check the results. Note that:
 * you free plan details are valid, for that find the message
 ```
 Licence successfully validated: Free plan 
 ```
 * the app could connect to the SharePoint instance, for that find the message
  ```
 Successfully connected to: https://yourcompany.sharepoint.com/
 ```

Good job! Now we ready to configure our first archiving or export procedure.

## Configure Listman.io
Let's have a look at the simple Listman.io config file. 

In that example application will run one archiving job immediately after the application start and archive all the items from the "list2" on the https://listman.sharepoint.com/ SharePoint instance into the `list1_archive.csv` file. All the attachment will be downloaded into the `attachments` folder. 

The config file has some other additional parameters including logging, what list columns to archive, **filtering condition** to decide which list items to archive and post action that has to be invoked against already archived record (like remove record or modify some of it's fields).

```
{
  useLicence: {
    email: "aershov24@gmail.com",
    host: "demo",
    appKey: "123"
  },
  connectTo: {
    siteUrl:"https://listman.sharepoint.com/",
    appId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
    appSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
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

Don't panic now, we will explain all the sections and corresponding options below.

### How To Verify and Validate Config File
You could always validate your configuration by running the app with the following command parameters:

```
> listman-cli.exe -c \Config\config.json -v -p -s
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
```
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
```
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
```
logTo:{
 csvLogFile: "C:\\Work\\listman.cli\\listman-cli\\log.csv"
}
```

> **So why Listman.io use CSV files for logging and not the simple txt format?** The answer is the Asyncronical execution of Archiving Jobs doesn't play well with text logs. 

Let's say you run archiving for two large list nearly in the same time. When log into a simple txt file logging messages from diffrent Archiving Jobs can't be easily grouped and analised. On the other hand CSV file could be opened in Microsoft Excel and filtered to display the log messages just from a particular Job or Action (download, delete, edit). It's especially usefull if you have multiple archiving jobs running at the same day.

### Archive Jobs configuration

#### Export Columns configuration

#### Filter By configuration

#### Record Action configuration

#### Archive To configuration

#### Schedule configuration

## Run as Console App

To run application in production mode 
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json"
```

### Run in Verbose Mode
To produce detailed logging file during production run you shall run the application with the `-v` (verbose) parameter:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -v
```

### Run to Validate Config File
To validate a config file run the app with the `-p` parameter:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -p
```

### Run in Testing Mode
Testing mode allow you to run application, connect to the SharePoint instance and iterate throught the list items but without actuall archiving, deletion, modification and attachments download. It's designed to battle test your configuration as close as possible to the actual production run including logs creation where you could verify that all the expected records marked for archiuving.

To run application in testing mode run the app with the `-t` parameter:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -t
```

You could combine test mode `-t` and `-v` verbose parameters for detailed logging:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -t -v
```

## Run as Windows Service

### Install Service
Assuming the installation path to listman.cli is `C:\Work\listman.cli.release\` use that command to install listman-cli as a Windows Service with name `ListmanService`:
```
sc create ListmanService binPath= "C:\Work\listman.cli.release\listman-cli.exe"
```

### Start Service
1. Go to Services
2. Right click on ListmanService -> Properties
3. Type
```
-c C:\Work\listman.cli.release\Config\listman.sharepoint.json -v
```
into the `Start Parameters` field
4. Click Start

Alternatively use the `sc.exe` command:
```
sc start ListmanService -v -c C:\Work\listman.cli.release\Config\listman.sharepoint.json
```
### Stop Service
To stop the service use

```
sc stop ListmanService
```

### Delete Service
To delete the service use

```
sc delete ListmanService
```

## Troubleshooting

<a name="support"/>

## Support
