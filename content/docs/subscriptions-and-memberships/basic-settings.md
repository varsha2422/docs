---
path: "/docs/catalog/basic-settings"
updated: "2019-07-05"
title: "Basic Settings"
description: "basic settings"
author: "Varsha"
category: "subscriptions and memberships"
---


	For renewing subscriptions you should run cron job atleast every day.

The cron job must run once an hour. While setting cron job, choose Once Per Hour under the common settings.

There should be minimum 15 minutes interval between each cron job.


![subscription](https://raw.githubusercontent.com/j2store/doc-images/master/subscriptions-and-memberships/basic-settings/subscription-cron.png)


![subscription once hour](https://raw.githubusercontent.com/j2store/doc-images/master/subscriptions-and-memberships/basic-settings/subscription-cron-once-hour.png)


**Cron url**


<link-text url ="http://www.example.com/index.php?option=com_j2store&view=cron&command=appsubscriptionproduct&cron_secret=XXXXX" target = "_blank" rel = "noopener"> click here </link-text>

Replace the domain with your domain. 

Where XXXXX is your cron secret key which can be identified in your store settings (J2Store > Setup > Configuration > Store tab)

Don't know how to set cron job ?  <link-text url ="http://docs.j2store.org/general/how-to-set-cron-job-on-your-server" target = "_blank" rel = "noopener"> click here </link-text>

**Notify expire day before**

Enter the number of days to send the remember mail to customer for notifying that their subscription will be going to end. For example, 2. So the mail will be sent before 2nd day to expire.

**Display settings**

* Show Duration
This option allows you to show / hide duration displaying below the product price.

* Show recurring total
Setting NO to this option will hide displaying recurring total column from the cart total table.

* Show non recurring total
This option helps you to show / hide non recurring total displaying in cart page.

* Show renewal date
If you would like to not show the next renewal date to users, just set this option NO.

* Renewal date format
This is the text box allows you to change the format of renewal date displaying in  item table.

* Show renew button
This option is used to show / hide renew button on profile page > Subscription tab.

**Renewal settings**

* Renewal discount

If you would like to give customers a discount for renewing subscription, then enter your discount value in percent in this text box. The discount value applied in this text box will be applied to all subscription products.