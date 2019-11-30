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

1. Save money on development (around one month of developer cost), application support and maintenance 
2. Avoid 5000 view and search limitation for large lists in Sharepoint by removing historical data
3. Reduce hosting costs by offloading attachments to filesystem or cloud storage
4. Improve overall system speed and responsiveness 
5. Comply and implement organization’s data retention policies
6. Meet regulatory compliance without shortcuts
7. Back up old data
8. Run archiving in no time (around 30 mins after simple configuration)

<a name="download"/>

## Download the App

<a name="sysReq"/>

### System Requirements

### Register Your Copy

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
