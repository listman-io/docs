# Documentation

##### Table of Contents  
[Getting Started](#gettingStarted)

[Download the App](#download)  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[System Requirements](#sysReq)  

[Support](#support) 

<a name="gettingStarted"/>

## Getting Started
**Listman.io** is a simple yet powerfully Windows Service/console application that helps organizations archive or export data and attachments from any Sharepoint lists of any size without infamous 5000 view limitation.

In short, Listman.io will allow your company run business more efficiently and:

1. Save money on custom SharePoint development (around one-two months of a developer salary), application support and maintenance 
2. Avoid 5000 view and search limitation threshold for the large lists in SharePoint by removing historical data
3. Reduce hosting costs by offloading unused attachments into the file system or any cloud storage
4. Improve overall system speed and responsiveness 
5. Comply and implement organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Back up old data for the peace of mind
8. And finally, configure and run archiving or exporting procedures in no time (around 30 mins after simple configuration)

<a name="download"/>

## Download the App
It's easy to start using Listman.io application and run your first archiving procedure. For that:

1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft Account. After succesfull Sign IN you'll redirected to your [Dashboard](https://www.listman.io/dashboard)
3. Click on Download the Listman.io

Alternatively you could download the previous versions of the Listman.io application using that [link](https://github.com/listman-io/docs/packages). 

**Note:** even if the app is downloaded from the Github you still will need to Sign In with your Microsoft account on [www.listman.io](https://www.listman.io) to run the app to obtain your licence information.

Congratulations! Now you are ready to configure your first archiving or export procedure.

<a name="sysReq"/>

### System Requirements And Prerequisites
Before processing to the next step make sure your system complies with following system requirements:

1. You have Windows 7/8/10/Server machine. For simplicity we will referencing to that machine as the **application server**.
2. You have .NET Framework 4.5 installed on the application server
3. Your application server is connected to internet. It's a very important point. Without the internet connection the Listman.io app wouldn't be able to ferity your application licence and fill fail to run.
4. You have some knowledge of JSON files as well as usage Windows Command Line and Windows Services.

### Get Your FREE Licence Details



## Free vs Enterprise Version

| Feature  | Free Version | Enterprise Version |
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

#### What is SharePoint Instance?

### How to Register Enterprise Version

## Create SharePoint app (app-only principal)

## Configuration

### Licence configuration

### Connect configuration

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
