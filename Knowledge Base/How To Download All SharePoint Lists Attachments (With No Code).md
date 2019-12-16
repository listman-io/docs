# How To Download SharePoint Lists Attachments (Fast) With No Code or PowerShell in 5 Simple Steps

One of the most common tasks that occurs once your organization starts to use SharePoint Online/2013/2016/2019 Lists is to download all attachments from a particular list at once in order to store it somewhere outside SharePoint Farm. 

Unfortunately SharePoint does not provide a native way to extract all the attachments from a SharePoint list especially if you want to base that extraction on a particular search criteria. This is the reason why historically many SharePoint developers and administrators used to be creating their own home-made PowerShell scripts or custom .NET applications and export all attachments from SharePoint lists. While that option is still available for SharePoint Online in 2020 coding SharePoint automation using PowerShell and CSOM (that stands for client-side object model) has never been an easy task and may take a lot of your team's time (and money).

Luckily for all of SharePoint users there is a new non-programmatic way to extract all the attachments from SharePoint lists with absolutely no code (and no PowerShell) with a little help of the Listman.io application.

## What is a Listman.io App?

Listman.io is a simple yet powerfully Windows Console Application that helps organizations auto archive and export data and attachments from SharePoint Lists of any size without annoying 5000 list view threshold based of certain criteria with no code whatsoever.

There are three main use cases when you could find the Listman.io app helpful for your business:

1. You need to archive SharePoint Lists Items with attachments based on some searching criteria into an external file or cloud storage. You want to run that task periodically using CRON schedule as a Windows Service. You want to delete or modify archived list item afterwards.

2. You need to export large (more than 5000) SharePoint lists data (with attachments) but don't want to do that using PowerShell, Excel, MS Access or Flow for some reason.

3. You want to download all or particular attachments from SharePoint lists, in order to back up them or move over (offload) from SharePoint.

Let's focus on the 3-rd use case and look how we could use Listman.io app to download all the SharePoint lists items attachments for less that 20 minutes.

## How to Export SharePoint List With Attachments Using Listman.io App

To export all the attachments from SharePoint Online list follow these 5 simple steps or watch our interactive video explaining the process on Youtube:



### Step 1. Download Listman.io App - 3 mins

To download Listman.io app:
1. Go to [www.listman.io](https://www.listman.io)
2. Sign In with your Microsoft or Google Account
3. Download latest version of Listman.io app by clicking on the Download button
4. Unzip the downloaded archive somewhere on your machine. For that example we will use the `C:\Export\listman-cli` folder.

### Step 2. Get Your Licence Details - 1 min
1. Sign In with your Microsoft or Google Account on [www.listman.io](https://www.listman.io)
3. Once redirected to your dashboard note your Sign In email on the top of the page near your account name.
4. Look at the "Licenses" section and note the details for the `demo` license:
 * Host name: `demo`
 * AppKey: `listman-*****-io`

![image](https://user-images.githubusercontent.com/13550565/70397377-ad90b500-1a4c-11ea-9d55-40d091bc19dd.png)

Now in order to download all the attachments we need to authorize Listman.io app against your SharePoint Online site. For that we need to create a SharePoint Application (also known as Application Context or App-Only authorization). 

### Step 3. Create SharePoint Application for App-Only Authorization - 5 min

In order for the Listman.io app to have an access to all lists and lists attachments we have to create a new SharePoint Application to be able to use Application Context authorization (aka App-Only) and grant it the `fullcontroll` **right** for the chosen **scope**.

> Please reference to the Listman.io Documentation on how to accomplish this step in details.

As a result of this step you should get `clientId` and `clientSecret` of your newly created SharePoint Application.

### Step 4. Modify Config File - 3 min

Now the fun part begins! 

Let's imagine that you need to download all the attachments from the `Customers` list from the `https:\\listman.sharepoint.com` SharePoint Online site alongside with some list's metadata like Name, Email, Phone, Address. 

![image](https://user-images.githubusercontent.com/58321045/70859205-89e8d580-1f4a-11ea-97b3-ee7385630151.png)

To make that happen:

1. Navigate to the folder where you have unzipped the Listman.io app 
2. Open the `config.json` file in any text editor of your choice
3. Edit the `config.json` file. Change the fields to your specific values and *Save* the file:

```js
{
  useLicence: {
    email: "aershov24@gmail.com",
    host: "demo",
    appKey: "listman-k400ia6i-io"
  },
  connectTo: {
    siteUrl:"https://listman.sharepoint.com/",
    clientId: "fe26fe8a-60b9-4523-996e-3e5ac2596e9f",
    clientSecret: "mVhELni3mB5n5moBeav4e9sKpq+s1ylV+vU0MFyWjAI="
  },
  archiveJobs: [
    {
      list: "Customers",
      exportColumns: ["ID", "GUID", "Name", "Email", "Phone", "Address"],
      exportAttachments: true,
      archiveTo: {
        file: "C:\\Export\\Customers\\customers.csv",
        attachmentsFolder: "C:\\Export\\Customers\\attachments",
        addHeader: true,
        append: false
      },
      schedule: {
        runImmediate: true
      },
    }
  ]
}
```

#### 5. Run the Listman.io App - 1 min

1. Open Windows Command Line, for that type `cmd` in a windows search bar
2. Navigate into the application folder, for that use the `cd` command:
```sh
> cd C:\Export\listman-cli
``` 
3. Run the Listman.io app (`-v` makes the output more verbose but you can skip it):
```sh
> listman-cli.exe -v
``` 
4. Wait for the app to finish downloading for all the lists metadata and attachments and watch the output:

```
...
[12/15/2019 2:39:28 PM] - [Customers Attachments Download] - [Customers List]: Search, ItemId: 499, Item marked for archiving
[12/15/2019 2:39:28 PM] - [Customers Attachments Download] - [Customers List]: Search, ItemId: 500, Item marked for archiving
[12/15/2019 2:39:28 PM] - [Customers Attachments Download] Format and flush list items into the csv file...
[12/15/2019 2:39:28 PM] - [Customers Attachments Download] Downloading attachments...
[12/15/2019 2:39:32 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 1, Attachment found
[12/15/2019 2:39:32 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 1, Attachment downloaded: C:\Export\Customers\attachments\1
[12/15/2019 2:39:33 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 3, Attachment found
[12/15/2019 2:39:33 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 3, Attachment downloaded: C:\Export\Customers\attachments\3
[12/15/2019 2:39:33 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 3, Attachment found
[12/15/2019 2:39:33 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 3, Attachment downloaded: C:\Export\Customers\attachments\3
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment found
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment downloaded: C:\Export\Customers\attachments\6
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment found
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment downloaded: C:\Export\Customers\attachments\6
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment found
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] - [Customers List]: Download, ItemId: 6, Attachment downloaded: C:\Export\Customers\attachments\6
[12/15/2019 2:39:34 PM] - [Customers Attachments Download] "Customers" List archived...
```

5. Go at the`C:\\Export\\Customers\\attachments` folder. Yay! Each subfolder will have a name of the corresponding item ID with all the attachments stored inside! So Easy!

![image](https://user-images.githubusercontent.com/58321045/70859170-05965280-1f4a-11ea-872a-ce0d22b45fb5.png)

![image](https://user-images.githubusercontent.com/58321045/70859180-25c61180-1f4a-11ea-85ae-13906b484189.png)


That's it! Once configured you could run the Listman.io app as many times as you like and download all the SharePoint Online lists attachments in less than 20 minutes.

To know how to download SharePoint online lists attachments **based on certain search criteria** look at this article.
