# Documentation

##### Table of Contents  
[Getting Started](#gettingStarted)

[Download the App](#download)  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[System Requirements](#sysReq)  

[Support](#support) 

<a name="gettingStarted"/>

## Getting Started

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
Install listman-cli as Windows Service:
```
sc create ListmanService binPath= "C:\Work\listman.cli.release\listman-cli.exe -c 'C:\Work\listman.cli.release\Config\listman.sharepoint.json'"
```

### Start Service
Start the service:
```
sc start ListmanService
```

### Delete Service
Delete the service

```
sc delete ListmanService
```

## Troubleshooting

<a name="support"/>

## Support
