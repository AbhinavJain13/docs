---



copyright:

  years: 2016, 2017
lastupdated: "2017-02-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# IBM {{site.data.keyword.Bluemix_notm}} Standard Account Beta 
{: #betaintro}

The {{site.data.keyword.Bluemix}} Standard Account Beta introduces a new free account, which offers a new way to work in the {{site.data.keyword.Bluemix_notm}} Public Cloud. The Standard Account never expires, unlike the 30-day {{site.data.keyword.Bluemix_notm}} Trial. You can continue to work on your {{site.data.keyword.Bluemix_notm}} applications without any concerns about time restrictions. 
{:shortdesc}

Participation in the Standard Account Beta is by invitation only. After you accept the invitation and create your Standard Account, you can invite friends and colleagues to participate in the Beta.  

## Introducing the {{site.data.keyword.Bluemix_notm}} Standard Account
{: #standardaccount}

You might be wondering what is different in the Standard Account as compared to the Trial Account. The following tables summarize the key details about the {{site.data.keyword.Bluemix_notm}} Standard Account. 

|What's new in a Standard Account? |    
|-----------------|
| The account never expires. |
| Cloud Foundry applications can access up to 256 MB of free, instantaneous runtime memory. |
| You can access free Lite Plans for Cloudant NoSQL DB, Internet of Things Platform, and Internet of Things Real Time Insights with more services coming soon. |
| Your applications will sleep if there is no development activity for 10 days. |
| Your service instances are deleted after 30 days of inactivity. |
{:caption="Table 1. What's new in a Standard Account" caption-side="top"}

|What's not changing when a Trial Account is converted? | 
|-----------------|
|The account is free -- you don't need a credit card. |
|Any Lite instances of Cloudant NoSQL DB, Internet of Things Platform, and Internet of Things Real Time Insights. One Lite instance for each of these services can be transferred to your new account. |
|Your organization, spaces, and associated team member access settings stay the same. One organization can be transferred to your new account. |
|The level of {{site.data.keyword.Bluemix_notm}} Support stays the same. |
{:caption="Table 2. What's not changing" caption-side="top"}

**Note** If your Trial Account doesn't convert, you will see a message that explains why. You might have more than one organization in your existing Trial Account or apps that cannot be transferred. You can take the appropriate action and then try to convert the account again.

When you are signed up for a Standard Account, you can invite team members to collaborate in your organization and spaces, view your usage, create spaces, update your account profile, and manage your organization. For more 
information, see [Setting up your account](/docs/admin/adminpublic.html#account).

### Lite Plans
{: #liteplans}
   
Lite Plans, which are also available in a Pay-As-You-Go Account, are structured as a free quota. You can work on your projects worry free, without the risk of generating an accidental bill. The quota might operate for a specific time period, for example, a month, or on a one-off usage basis. Here are some examples of Lite Plan quotas:

<ul>
<li>Maximum number of registered devices.</li>
<li>Maximum number of application bindings.</li>
<li>Encrypted data storage limit, for example, 1 GB.</li>
<li>Provisioned throughput capacity.</li>
</ul> 

In a Standard Account, you can use anything in the {{site.data.keyword.Bluemix_notm}} Catalog that has a Lite Plan. Lite plans are easy to find. By default, when you open the Catalog, all services with a Lite Plan are displayed and identified with a Lite tag ![Lite tag](../icons/Lite.svg). Select a service to view the quota details for the associated Lite Plan.

### What’s available in the Standard Account?
{: #whatsavailable}

In a Standard Account, Cloud Foundry applications can access up to a maximum of 256 MB of instantaneous runtime memory. If you exceed your allocated quota, you can stop some of your apps to free up runtime memory. 

During the Standard Account Beta, the following services offer a Lite Plan:

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
<li>Internet of Things Real Time Insights</li>
</ul>

We’ll be adding to this list of services, so stay tuned!

When quota limits are reached, your application is stopped or your service is disabled. If the Lite Plan specifies that the quota is provided on a monthly basis, the resource usage is reset on the 1st of every month when you can resume working with the service. When you are approaching a quota limit, or are at the quota limit, you will receive a notification email. 

You can provision 1 instance per Lite Plan. 

**Note**: These limitations apply to the Standard Account only. At any time, you can upgrade to a Pay-As-You-Go or a Subscription billing account. You pay only for what you use beyond the free allowances. For more information about Pay-As-You-Go and Subscription 
accounts, see [How you are billed](/docs/pricing/index.html#pay-accounts).

### Development activity
{: #devactivity}

To help Standard Account users best manage their resources, we have built a couple of efficiency features that are based on development activity and usage:

 * Your apps will go to sleep after 10 days of development inactivity. This helps when you want to work on a new app, because you won’t find yourself hitting the 256 MB memory quota limit. To wake up your apps, start working on them again in the Cloud Foundry command line or the {{site.data.keyword.Bluemix_notm}} console. 
 
 Here’s a list of all commands that’ll wake up your app:
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Note** If your app is already ssh enabled, the `cf enable-ssh` and `cf disable-sh` commands will not wake up your app. 

 * Your Lite Plan services will be deleted if there isn’t any activity on them for 30 days. Then, you don’t have to delete inactive instances when you want to create a new instance. Right now only the Internet of Things Platform service is using this feature. 
 
 Keep your Internet of Things Platform Lite instance active by logging in to the Internet of Things Platform service instance dashboard.
 
### Participating in the Standard Account Beta
{: #betainvitation}

If you are selected to participate in the Beta, an invite is sent to the email address associated with your {{site.data.keyword.Bluemix_notm}} Trial Account. When you receive the invite, complete the instructions in the email to register for the Standard Account. 

Interested in participating in the Standard Account Beta offering? Ask your friends and colleagues. If they have been invited to join the Beta and created their Standard Account, they can invite you too. 
