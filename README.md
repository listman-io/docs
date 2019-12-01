# Documentation

##### Table of Contents  
[Getting Started](#gettingStarted)

[Download the App](#download)  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[System Requirements](#sysReq)  

[Support](#support) 

<a name="gettingStarted"/>

## Getting Started
**Listman.io** is a simple yet powerfully Windows Service/console application that helps organizations archive or export data and attachments from any SharePoint lists of any size without annoying [5000 list view threshold](https://docs.microsoft.com/en-us/sharepoint/support/lists-and-libraries/items-exceeds-list-view-threshold).

In short, Listman.io will allow your company to run business more efficiently and:

1. Save money on custom SharePoint development (around one-two months of a developer salary), application support and maintenance 
2. Avoid 5000 view and search limitation threshold for the large lists in SharePoint by removing historical data
3. Reduce hosting costs by offloading unused attachments into the file system or any cloud storage
4. Improve overall system speed and responsiveness 
5. Comply and implement organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Back up old data for the peace of mind
8. And finally, configure and run archiving or exporting procedures in no time (around 30 mins after simple configuration)

<a name="download"/>

<a name="sysReq"/>

## System Requirements And Prerequisites
Before processing to the next step make sure your system complies with following system requirements:

1. Listman.io is a Windows application that could be run as command line application or Windows Service. To run it you must have Windows 7/8/10/Server system installed on one of your local machines or cloud. For simplicity we will referencing to that machine as the **application server**.
2. You have .NET Framework 4.5 installed on the application server
3. Your application server is connected to the Internet. It's a very important point. Without the internet connection the Listman.io app wouldn't be able to ferity your application licence and will fail to run archiving or export procedures.
4. You have some knowledge of JSON files as well as usage Windows Command Line and Windows Services.
5. You have SharePoint 2013/2016/2019 or SharePoint Online.

## Download the App
It's easy to start using Listman.io application and run your first archiving procedure. For that:

1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account. After succesfull Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard)
3. Click on Download the Listman.io

Alternatively you could download the latest and all the previous versions of the Listman.io application using that [link](https://github.com/listman-io/docs/packages). 

> Even if the app is downloaded from the Github you still will need to Sign In with your Microsoft account on [www.listman.io](https://www.listman.io) to run the app to obtain your licence information.

Congratulations! Now you are ready to configure your first archiving or export procedure.

### Free vs Enterprise Plans
Listman.io is a commercial software but purposely designed to be run in a free mode for better learning and assessment experience. There is no trial so you have unlimited time to make sure the Listman.io fits your organization needs. 

We recommend you to start your archiving experience by running Listman.io as a free version against your Development or Staging SharePoint servers to familiarize yourself with all application features. Once ready you could easily subscribe to Enterprise plan and make the most from your archiving or exporting procedures.

> Free version is limited to archive or export just 50 records from any list per application run. If you want to archive or export more than 50 records per run we recommend you to upgrade on Enterprise plan. Prioritized support is also available only for Enterprise customers.

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
| Records archiving/export limit per run |  50 |  ♾️, No Limit |
| Cost |  Free |  $69 per month / per SharePoint instance |

### How to Register Enterprise Version

## Get Your Free Licence Details

To get your free plan details:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account email. After Sign In you'll redirected to your [Dashboard](https://www.listman.io/dashboard). Note your Microsoft Account email. You'll need it on the configuration step.
3. Go to Subscriptions section and note the following details:
 * Your Microsoft Account `email`
 * Host name: `demo`
 * AppKey: `get it from subscription`

Now we ready to create your first SharePoint Application (also known as Application Context or App) that will be used to authorize Listman.io console application or Windows service against your Sharepoint instance. 

## Create SharePoint Application (App-Only/Application Context)

Let's assume that your SharePoint instance is accessible by address: https://listman.sharepoint.com/. We will call that site **SharePoint Instance**. Your SharePoint Instance could have multiple sites and lists. To make sure Listman.io app will have an access to any list on your SharePoint instance we have to create Application Context (or App-Only) and grant it the right permissions.

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
5. Note `Client Id` and `Client Secret` and write it down somewhere
6. Now go to `https://listman-admin.sharepoint.com/_layouts/15/appinv.aspx`, note the `-admin` in the URL
7. Copy `Client Id` from the step 5 into the "App Id and Title" field
8. Click on **Lookup**
9. Note the app details from step 3 will appear in the form
10. Fill up the field `App's Permission Request XML` with the following XML:
```
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```
11. Click **Create**
12. You'll see the following Page:

13. Click on **Trust It**.

Great! Now we are ready to run Listman.io for the first time and make sure we could connect to your SharePoint instance.

## Test Listman.io Connection
1. Download the Listman.io application from your Dashboard or from Github.
2. Unpack the archive into the folder from which you want to run the application. We will reference to this folder as **app folder** for simplicity.
3. Navigate to `{app folder}\Config\` using Windows Explorer or window Command Line
4. Open the `config.json` file in any text editor of your choice
5. Edit the config file. Change the fields to your specific values and **Save** the file:

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
6. Open Windows Command Line, for that ...
7. Navigate into the `app folder`, for that use the command:
```
> cd /d {path_to_app_folder}
``` 
8. Run the Listman.io app with the following command line parameters:
```
> listman-cli.exe -c '\Config\config.json' -l -s
``` 
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

In that example application will run one archiving job immediately after application start and archive all the items from the "list2" list on the https://listman.sharepoint.com/ SharePoint instance into the `C:\\Work\\listman.cli\\listman-cli\\list1_archive.csv` file in the file system including attachments. The config file has some other additional parameters including logging, desalination of what list columns to archive, **filtering condition** to decide which list items to archive and post action that has to be invoked against archived record (like remove record or modify some of it's fields).

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

Don't be scared if some of its options don't have any sense for now. We will explain all the sections and corresponding options below.

### How To Verify and Validate Config File
You could always validate your configuration by running the app with the following command parameters:

```
> listman-cli.exe -c \Config\config.json -v -p -s
```

That command will:
1. Parse and validate config file syntax
2. Check your plan details
3. Try to connect to the Sharepoint Instance

We recommend you to run this command every time you make significant changes to your config file.

Now let's look onto the all configuration sections in details.

### Licence configuration
`useLicence` section is used to provide details about your free or Enterprise plan:

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

`useLicence` section is used to provide details about your free or Enterprise plan:

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

### Logging configuration

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
