# Listman.io Docs

**Listman.io** is a simple yet powerfully Windows Console Application that helps organizations auto archive or export data and documents from SharePoint Lists and Document Libraries of any size without annoying [5000 list view threshold](https://docs.microsoft.com/en-us/sharepoint/support/lists-and-libraries/items-exceeds-list-view-threshold) based of certain criteria.

![](https://user-images.githubusercontent.com/13550565/70306479-e872cd00-1841-11ea-9a44-26255be30a13.png)

#### Table of Contents  

* [Why Your Business May Need Listman.io](#why-your-business-may-need-listmanio)
  + [Why Archive/Export to CSV](#why-archive-export-to-csv)
* [System Requirements And Prerequisites](#system-requirements-and-prerequisites)
* [Download the App](#download-the-app)
* [Understanding the Free vs Enterprise License](#understanding-the-free-vs-enterprise-license)
  + [Note on Sharepoint Instance](#note-on-sharepoint-instance)
  + [Get Your Free License Details](#get-your-free-license-details)
  + [How to Subscribe to Enterprise License](#how-to-subscribe-to-enterprise-license)
  + [**`siteUrl` vs `host`**](#---siteurl--vs--host---)
* [Create SharePoint Application (App-Only/Application Context)](#create-sharepoint-application--app-only-application-context-)
* [Quick Start Guide](#quick-start-guide)
  + [I got an error, what to do?](#i-got-an-error--what-to-do)
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
  + [`useLicense` section](#-uselicense--section)
  + [`connectTo` section](#-connectto--section)
  + [`logTo` section](#-logto--section)
  + [`archiveJobs` section](#-archivejobs--section)
    - [`exportColumns` field](#-exportcolumns--field)
    - [`filterBy` subsection](#-filterby--subsection)
      * [`filterBy` with SharePoint Conditional Columns](#-filterby--with-sharepoint-conditional-columns)
    - [`recordAction` subsection](#-recordaction--subsection)
    - [`archiveTo` subsection](#-archiveto--subsection)
    - [`schedule` section](#-schedule--section)
* [Command Line Parameters](#command-line-parameters)
* [How to Get Help](#how-to-get-help)

## Why Your Business May Need Listman.io

In short, Listman.io will allow your company to run business more efficiently and:

1. Save money on custom SharePoint development (around one-two months of a developer salary), application support and maintenance 
2. Avoid 5000 view and search limitation threshold for the large lists and document libraries in SharePoint by removing historical data, files and attachments
3. Reduce hosting costs by offloading unused attachments or documents into the file system or any cloud storage including OneDrive, Dropbox, Google Drive or Azure Storage
4. Improve overall system speed and responsiveness 
5. Comply and implement custom organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Automatically back up old data and documents based on certain criteria
8. Transfer or export lists data from SharePoint into any DB including MS SQL Server or Azure Database
8. And finally, configure and run archiving or exporting procedures in no time without any custom development (around 30 mins after simple configuration)

And if you are a SharePoint Consulting Microsoft Partner Listman.io will help you to implement client-side projects with better profit margin by saving money on custom archiving/export/migration requirements development.

### Why Archive/Export to CSV
... and not to MS SQL for example? 

So, Listman.io is built upon the principles of Unix philosophy and designed to *do one thing very well*, namely to archive and export SharePoint lists and document libraries data into the CSV format files (comma delimited). We use CSV files as a final data destination because:

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
4. Your application server must be connected to the Internet. Without the internet connection Listman.io app wouldn't be able to verify your *license* and will fail to run archiving or export jobs.
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

## Understanding the Free vs Enterprise License
Listman.io is a **commercial software** but purposely designed to be run in a free mode for better learning and evaluation experience. There is **no trial** so you have unlimited time to make sure Listman.io fits all your organization archiving or exporting needs. 

We recommend you to start run Listman.io using a Free License and first learn how to archive/export data from your Development or Staging SharePoint servers. Once confident with app configuration you could easily [subscribe to the Enterprise License]() and make the most from your archiving or exporting procedures.

> Free License is limited to archive or export only 50 records from one SharePoint Instance per run. You could have just one Free License for your account. If you want to archive or export more than 50 records monthly we recommend you to upgrade to Enterprise License. Enterprise License also includes priority support.

Look at the table below to choose between Free or Enterprise Licenses.

| Listman.io Feature  | Free License | Enterprise License |
| ------------- | ------------- | -----------------|
| Unlimited sites |  ✅ |  ✅ |
| Unlimited lists |  ✅ |  ✅ |
| Unlimited document libraries |  ✅ |  ✅ |
| Unlimited jobs |  ✅ |  ✅ |
| Support large lists/libraries archiving/exporting (over 5000 threshold)   |  ✅ |  ✅ |
| Modify list/library items after archiving/export |  ✅ |  ✅ |
| Delete list/library items after archiving/export |  ✅ |  ✅ |
| Download list attachments |  ✅ |  ✅ |
| Download library documents |  ✅ |  ✅ |
| Run as CLI |  ✅ |  ✅ |
| Run as Windows Service |  ✅ |  ✅ |
| Cron Scheduler |  ✅ |  ✅ |
| Email Support |  ✅ |  ✅ |
| Priority Support |  ❌ |  ✅ |
| Records/documents archiving/export per run |  50 |  ♾️, No Limit |
| Cost |  Free |  $69 / per month / per SharePoint Instance |

### Note on Sharepoint Instance
So what is SharePoint Instance? Let's assume that your root SharePoint site is accessible by the URL address (also known as `siteUrl`): 

```sh
https://listman.sharepoint.com/
```

We will call that unique installation of SharePoint Server as **SharePoint Instance**. Your SharePoint Instance could have multiple sites and lists. So one Enterprise License lets you to archive or export data from any site/list on one SharePoint Instance.

### Get Your Free License Details

To run the Listman.io application for the first time you have to know your *license* details. We define **license** as a set of:

* SignIn email (like `peter.pan@gmail.com`)
* SharePoint host (like `demo`, `listman.sharepoint.com` or `localhost`)
* AppKey (like `listman-*****-io`)

To get your Free License details:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). 

![image](https://user-images.githubusercontent.com/13550565/70402399-2fdda100-1a6e-11ea-8356-60f742cb3e6c.png)

3. Note your Microsoft Account email on the top of the page near your name. You'll need it on the configuration step later.

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70385182-cb1b3b80-19c6-11ea-87f4-549562458d8a.png" alt="drawing" width="300"/>

4. Go to "Licenses" section and note the following details for the `demo` license:
 * Host name: `demo`
 * AppKey: `listman-*****-io`

![image](https://user-images.githubusercontent.com/13550565/70397377-ad90b500-1a4c-11ea-9d55-40d091bc19dd.png)

Now we ready to create your first SharePoint Application (also known as Application Context or App-Only) that will be used to authorize Listman.io app against your Sharepoint Instance. 

### How to Subscribe to Enterprise License

If you are a new user of Listman.io you could skip this section and circle back to it later after trying Listman.io app by using a Free License.

If you want to run archiving procedure on a full scale **without 50 records per run limitation** you have to subscribe to an Enterprise License:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). Note your Microsoft Account email. You'll need it on the configuration step.
<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70385182-cb1b3b80-19c6-11ea-87f4-549562458d8a.png" alt="drawing" width="300"/>
3. Go to Billing details section and add details of your credit or debit card. 
4.  Make sure there is no errors and click **Update** twice. Once your billing details is saved you'll see a green label `Provided`.

![image](https://user-images.githubusercontent.com/13550565/70397403-d749dc00-1a4c-11ea-9d03-8e3076d19a21.png)


5. You could always change your billing details in the future. Just type a new card details and click on **Update** twice.
> **Note:** we never store your billing detail on our servers. All the billing information and payments processed by Stripe. 
3. Once billing details are added, go to Licenses section
4. Click on **Add license** button near `licenses` section (big plus icon)

<img style="display: block; margin: 0 auto;" src="https://user-images.githubusercontent.com/13550565/70407048-c9607f00-1a7d-11ea-8912-b8aba0c5228e.png" alt="drawing" width="200"/>

5. Type name of the new SharePoint `host` you want to archive or export data from like `listman.sharepoint.com` or `localhost`. If you host is accessible only by IP address or localhost type them as they are. **Do not type port**. 

![image](https://user-images.githubusercontent.com/13550565/70407093-f745c380-1a7d-11ea-82c9-97ce333366bd.png)


7. Check your license details, note generated `AppKey` and click on **Activate** button **twice** to confirm activation.

![image](https://user-images.githubusercontent.com/13550565/70397587-89ce6e80-1a4e-11ea-90c9-e86c6d2a34f6.png)

> **Note**: you can't change the **Host** after your license is activated so make sure to thoroughly check your details.
8. You could **Unsubscribe** from active license at any time. For that click on **Unsubscribe** button **twice**. Once unsubscribe your licence will be deactivated immediately and any archiving or export run will fail on license validation step. 

![image](https://user-images.githubusercontent.com/13550565/70397601-a9659700-1a4e-11ea-94e9-c7bee237fdc5.png)

> **Note**: Listman.io doesn't support *Pausing* for a license.

9. If you need to archive or export lists from multiple SharePoint Instances available on different **hosts** you have to create a new license for each host.

> Once license is activated your card will be billed immediately. Make sure you have sufficient funds available on your card each month so your subscription will stay active.

### **`siteUrl` vs `host`** 
Your SharePoint Instance is usually available via urls like:
 * `https://listman.sharepoint.com`, 
 * `https://localhost:4545` or even 
 * `https://192.123.23.12`. 
 
 That url is also known as `siteUrl` and used by Listman.io to establish connection with SharePoint Instance (using CSOM). We define `host` for `siteUrl`s as 
 * `listman.sharepoint.com`, or
 * `localhost`, or
 * `192.123.23.12` (note the absence of a port number). 
 
 When Listman.io app is running we match the `siteUrl` with the `host` from the license details provided in the config file and throwing an error if there is any difference.
 
 > **Note**: `demo` is a special type of host used for the Free License so the Listman.io app could be run in demo mode for any `siteUrl` but with **50 records per run limitation**.

## Create SharePoint Application (App-Only/Application Context)

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

## Quick Start Guide
Now let's quickly validate that we could run Listman.io app using a Free License and `clientId` and `clientSecret` created above against your Sharepoint Instance. For that:

1. Download the Listman.io application from your Dashboard or from Github if you haven't done it before.
2. Unpack the archive into a folder from which you want to run the application on your application server. We will reference to this folder as the **app folder** for simplicity.
3. Navigate to **app folder** using Windows Explorer
4. Open the `config.json` file in any text editor of your choice
5. Make sure your know:
 * your sign in email
 * `appKey` for Free License from your dashboard
 * `clientId` for the SharePoint app from step 4, section [Create SharePoint Application](#create-sharepoint-application-app-onlyapplication-context)
 * `clientSecret` for the SharePoint app from step 4, section [Create SharePoint Application](#create-sharepoint-application-app-onlyapplication-context)
5. Edit the `config.json` file. Change the fields to your specific values and **Save** the file:

```js
uselicense: {
  email: "your_sign@in_email.com",
  host: "demo",
  appKey: "appKey_from_dashboard"
},
connectTo: {
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
> listman-cli.exe -p -l -s
``` 
Where:
* `-p` - parameter used to validate config file
* `-l` - parameter used to validate user license
* `-s` - parameter used to test the connection to Sharepoint using `siteUrl` and App-Only credentials
9. Check the results. Note that:
 * you Free License details are valid, for that make sure you see the message
 ```
 license successfully validated: demo
 ```
 * the app could connect to the SharePoint instance, for that make sure you see the message
 ```
 Successfully connected to: https://yourcompany.sharepoint.com/
 ```

Good job! Now let's learn what are some different ways to run the Listman.io app. 

### I got an error, what to do
If you can't see the two successful messages above check:
1. Validate all your details in the config file
2. Make sure your application server is connected to Internet and there is no Firewall rules block any outcomming/incomming https requests 
3. Look at the `app folder\trobleshooting.log` file for verbose exception details
4. If nothing helped contact us on `support@listman.io`, we will schedule a call with you help you personally 

## Run as Console Application

Before running Listman.io app against your production SharePoint Instance we recommend you to *always* run the app in a test mode.

### Run in Test Mode
Test mode allows you to start Listman.io app, validate config file, connect to SharePoint Instance and *iterate through the list items without actual archiving, deletion, modification and attachments downloading*. 

The Test Mode is designed to battle test your configuration as close as possible to the actual production run including logs creation to verify all the expected records were correctly marked for archiving.

To run application in Test Mode run the app with the  `-p` and `-t` parameter:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -p -t
```

You could combine `-p`, `-t` and `-v` parameters for detailed logging:
```sh
> listman-cli.exe -c "Configs\comsco.sharepoint.com.json" -p -t -v
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

The config file has some other additional parameters including logging, what list columns to archive, **filtering condition** to decide which list items to archive and post action that has to be invoked against already archived record (like remove record or modify some of it's fields).

```js
{
  uselicense: {
    email: "listman.io@gmail.com",
    host: "demo",
    appKey: "listman-123123-io"
  },
  connectTo: {
    siteUrl:"https://listman.sharepoint.com/",
    clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
    clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
  },
  logTo:{
    csvLogFile: "C:\\Work\\listman-cli\\log.csv"
  },
  archiveJobs: [
    {
      name: "Job 1",
      list: "list2",
      filterRecordsBy: {
        columnName: "Archived",
        equalBool: false
      },
      exportColumns: ["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
      exportAttachments: true,
      recordAction:{
        remove: true
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

### How To Verify and Validate Config File
You could always validate your configuration by running the app with the following command parameters:

```sh
> listman-cli.exe -c "\path\to\config.json" -v -p -s
```

That command will:
1. `-p` - Parse and validate config file syntax
2. `-v` - validate your license details
3. `-s` - connect to to Sharepoint using `siteUrl` and App-Only credentials

We recommend you to run this command every time you make significant changes to your config file to catch and debug any unexpected configuration and syntax errors.

Now let's look on the all configuration sections in details.

### `useLicense` section
`uselicense` section is used to provide details about your free or Enterprise License:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `email` | Your Microsoft Account email used to sign in on www.listman.io  | aershov24@gmail.com |
| `host` | Sharepoint Instance host (domain) name or `demo` for Free License | `demo` for Free License or `yourcompany.sharepoint.com` for Enterprise License |
| `appKey` | Application Key generation on your Dashboard for particular host (including `demo`)  | 123123123123123123123 |

**Example**:
```js
uselicense: {
  email: "aershov24@gmail.com",
  host: "demo",
  appKey: "123"
}
```
**Errors**:
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `license validation failed: No user found` |  |
| `license validation failed: No host found` |  |
| `license validation failed: AppKey is invalid` |  |
| `license validation failed: License is not active` |  |

### `connectTo` section

`connectTo` section is used to define siteUrl of the Sharepoint Instance as well as app-only authorization details:

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `siteUrl` | Url of your Sharepoint Instance  | https://listman.sharepoint.com |
| `clientId` | Client Id generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `fe26fe8a-60b9-4523-996e-3e5ac2596e9f` |
| `clientSecret` | Client Secret generated for the Sharepoint application, created in the [Create SharePoint Application (App-Only/Application Context)]() section | `mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI=` |

**Example**:
```js
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

### `logTo` section
Listman.io has several layers of logging:
1. Console logging. You usee it only when Listman.io is run as a console app.
2. Logging into `troubleshooting.log` file in the application folder. That logging is used only for troubleshooting and debuging.
3. Logging into a custom CSV file. That is the log you should prefer for everyday use.

The `logTo` section is used to configure the logging into the CSV file and fairly simple to understand:
```js
logTo:{
 csvLogFile: "C:\\Work\\listman.cli\\listman-cli\\log.csv"
}
```

> **Why Listman.io use CSV files for logging and not the simple txt format?** The answer is the Asyncronical execution of Archiving Jobs doesn't play well with text logs. 

Let's say you run archiving for two large list nearly in the same time. When log into a simple txt file logging messages from diffrent Archiving Jobs can't be easily grouped and analised. On the other hand CSV file could be opened in Microsoft Excel and filtered to display the log messages just from a particular Job or Action (download, delete, edit). It's especially usefull if you have multiple archiving jobs running at the same day.

### `archiveJobs` section
Listman.io supports running multiple archiving jobs at the same time or by schedule. You have to add all the job configurations into the `archiveJobs` section (that is an array of JSON objects) of the config file:
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
| `listName` | The title of a SharePoint list or document library to archive | `customers` |
| `libraryName` | The title of document library to archive | `customers` |
| `exportColumns` | List of column titles for archiving or export as JSON array of strings. Note: `ID` and `GUID` columns are mandatory and have to be in the list. | `["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"]` |
| `exportFiles` | Do we need to download list attachments or library documents? Default is `true`. | `true` or `false` |
| `batchSize` | When Listman.io gets list data from Sharepoint lists it iterates through the list's data in batches or pages. The default `batchSize` value is `500`. We recommend to keep this value as 500 or lower if you have slow or unstable Internet connection | `500` |
| `filterBy` | This subsection is used to filter specific list or library records for archiving or export. You could specify what list records or library documents to archive or export using a criteria. Don't use that field or set it's value to `null` if you want to archive/export **all list items or library documents**. Default is `null`. | See [Filter By configuration]() for details |
| `recordAction` | You may want to delete or modify some fields of a record from the list after archiving. This subsection is used to configure post archive action for the record. | See [Record Action configuration]() for details |
| `archiveTo` | This section is used to specify properties of the archiving or export output files like file path, adding header and file write modes like `append` or `rewrite` | See [Archive To configuration]() for details |
| `schedule` | This section is used to specify job run schedule. Basically you could run jon immediately after application launch or by schedule using cron syntax. | See [Schedule configuration]() for details |

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Can't find the list with the Title`| Check your list title |
| `Export Columns list should contain at least ID and GUID columns`| Check your export columns list |

#### `exportColumns` field
`exportColumns` field should contain a list of column titles for archiving or export as JSON array of strings. Note that `ID` and `GUID` are mandatory columns and have to be presented in the `exportColumns` list.

> SharePoint list columns have three different names: Column Name (or Title), InternalName and StaticName. In the `exportColumns` list you have to provide list of  **Column Names**. The Listman.io automatically will find InternalNames of the columns for CSOM operations. You could find all column names for the list on a view list settings page.

**Example:**
```js
exportColumns: ["ID", "GUID", "Title","col1", "col2", "Published", "Bool", "Archived", "ArchivedDate"],
```

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `No ID column found`| Check that list contains "ID" column name |
| `No GUID column found`| Check that list contains "GUID" column name |
| `No "Column Name" found`| Check that list contains "Column Name" |

#### `filterBy` subsection

`filterBy` subsection is used to specify a simple equality condition under which record from the SharePoint list or library will be marked for archiving or export. Condition could be specified just for one column that has `number`, `string`, `bool`, `currency` or `datetime` type. For documents library you could also specify an extension of the files to download.

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


Or if you want to archive all the `docx` documents that contains `_Alex_` in the `FileName`:
```js
filterBy: {
  documentExt: "pdf",
  columnName: "FileName",
  containStr: "_Alex_",
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
| `documentExt` | Document file extension. Applicable only for document libraries. `null` by default | "docx" |
| `columnName` | Column to apply condition to. Column has to have either `string` or `bool` or `DateTime` types  | "Published" |
| `equalDouble` | Conditional value to match current value of the `currency` type column to. The record will be marked for archiving if values are equal. Note absence of any currency sign. | `98.99` |
| `equalInt` | Conditional value to match current value of the `number` type column to. The record will be marked for archiving if values are equal. | `12` |
| `equalStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if values are equal. | "Processed Successfully" |
| `containStr` | Conditional value to match current value of the `text` or `note` type column to. The record will be marked for archiving if field contains conditional value. | "_London" |
| `equalBool` | Conditional value to match current value of the `bool` type column to. The record will be marked for archiving if values are equal. | `true` or `false` |
| `olderThanDays` | Conditional value to match current value of the `datetime` type column to. The record will be marked for archiving if column value are older than `olderThanDays` days. | `30` |

**Errors:**
There are some errors that may be generated by the app if that section is filled up with incorrect information:

| Error Message  | How to solve | 
| ------------- | ------------- | 
| `Column value and conditional value have different types`| Check that `columnName` has `string`, `bool` or `datetime` type and the right condition column is chosen |

#### `recordAction` subsection

Once list or library record/document is archived or exported you may want to delete it or modify some of its fields. The `recordAction` subsection is designed to configure post archive action applied to the archived record.

| Field  | Description | Example |
| ------------- | ------------- | -----------------|
| `remove` | remove list item or library file after archiving, `false` by default  | `true` |
| `modify` | List of modifications (JSON array) for one or more list/library item fields after archiving, `null` by default | `true` |

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
| `filesFolder` | The output folder for downloaded attachments or library documents. For list each attachment will be downloaded into a separate subfolder named by Item ID. For libraries the Item ID will be added as a postfix into the file name to prevent files with similar names from overwriting. Only latest version of each document will be downloaded. Look at the `keepFoldersStructure` setting below if you want to keep documents library folder structure  | `C:\\Work\\listman.cli\\listman-cli\\attachments` |
| `addHeaderToCSV` | Add columns header to the CSV file. `true` by default. | `true` |
| `appendRecordsToCSV` | Overwrite or append archived records into the CSV file if it exists. `true` by default. | `true` |
| `keepLibraryFoldersStructure` | Set to `true` if you want to keep folders structure from the documents library, `false` if all the files could be copied in the one folder. `true` by default. | `true` |

**Example**:
```js
archiveTo: {
  csvFile: "C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv",
  filesFolder: "C:\\Work\\listman.cli\\listman-cli\\attachments",
  addHeaderToCSV: true,
  appendRecordsToCSV: false
}
```

#### `schedule` section
Listman.io could run archiving jobs by schedule. Basically you could run job immediately after application launch or by schedule using `cron` syntax. 

> If you not familiar with `cron expressions` read this [article](https://www.quartz-scheduler.net/documentation/quartz-3.x/tutorial/crontriggers.html). You could also use this `cron expression` [builder](http://www.cronmaker.com/). 

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
| `-l`| `--license` | `false` | Validate user license without jobs run  |
| `-s`| `--server` | `false` | Test connection to SharePoint Server|
| `-n`| `--cron` | `false` | Validate Cron Expressions for jobs |
| `-t`| `--test` | `false` | Run archive/export jobs in testing mode (without actual data transfer and items modification) |

## How to Get Help
If you have any troubles with running or configuring Listman.io there is several channels where you could get help:
1. Read This (F*cking) Manual
3. In case of any runtime errors (exceptions) look at the `app_folder\troubleshooting.log` file for detailed `Exception Stack Trace` and try to fix your config file or environment
2. Browse [All The Issues](https://github.com/listman-io/docs/issues?utf8=%E2%9C%93&q=) that have been already asked and closed
5. [Create a new Issue](https://github.com/listman-io/docs/issues) using this Github repo
6. Send us a support request to [support@listman.io](mailto:support@listman.io)
