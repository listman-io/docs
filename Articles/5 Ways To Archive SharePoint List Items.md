5 Ways To Archive SharePoint List Items

The Problem with SharePoint Content Archive

Probably you are running out of storage space on this list. Or probably yo want to reduce the bloat of SharePoint Online 
cost of hosting in Office365 by automatically archiving sites, lists or libraries to remote storage? Or probably you have policies enforced by company and archiving is necessary especially when you have users storing documents in a library or a list that exceed the 5000 threshold view limit. Or may be your company collecting online forms as a list items and pictures are often attached to each "item" of this list so you just want to offload these images to a file or cloud storage?

SharePoint Archiving/Exporting Solutions

* Simply export data into Excel from SharePoint list view (no attachments, only metadata, doesn't work for large lists)
* Apply information management policies to a list (not available by default for SharePoint Online, limited destination optionality)
* Use Export-SPWeb SharePointServer cmdlet (only for Sharepoint Server, wouldn't work for SharePoint online)
* Create workflow which can move the items from the List to a chosen destination (5000 search limit and other)
* Write PowerShell script (using SharePoint PnP PowerShell cmdlets for Sharepoint Online) and run is by Task Scheduler (time consuming and costly)
* Create a custom .NET Application using CSOM (.NET Framework required) and run it as a Windows Service (costly)
* Create custom WEB application using SharePoint JavaScript Client Object Model or 3-rd party libraries like SharepointPlus
* If you have MS SQL Server you could create SQL Server Integration Services (SSIS) package, read list items as a OData source and run it as a job
* Use 3-rd party tools like Listman.io to automate lists data archiving and export by schedule with attachment (all options ticked)