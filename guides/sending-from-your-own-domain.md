---
description: Adding a domain name to send e-mails from
---

# Sending from your own domain

If you own a domain name \(for example **airbnbforcats.com\)** you can add it to your Magic Login account for sending. 

You should use a new subdomain for this purpose, such as **ml.airbnbforcats.com** or  **magiclogin.airbnbforcats.com**. This keeps your Magic Login usage and **sending reputation** from other mail sending services you may add in the future \(for example a newsletter service, or e-mails you send manually\).

Also if you want to one day switch away from Magic Login you will know exactly which DNS entries to remove \(but of course we hope you will never want to!\).

{% hint style="info" %}
It is not possible to add individual e-mail addresses through the UI: you will not be able to send e-mails from an address on a domain that you don't own \(such as an **@gmail** account\).

**Sending from a domain you don't own is bad for deliverability and we recommend always using a domain you own instead**. On special request we can add individual e-mail addresses for an extra $4 monthly cost, but please instead spend this money getting your own domain.
{% endhint %}

## Adding a domain identity

> You may not need to read through guide as the UI also shows instructions.  
> This page just contains more details in case you get stuck.

Navigate to the[ **Identities Dashboard page**](https://magiclogin.net/dashboard/identities), and click [**Add New Identity**](https://magiclogin.net/dashboard/identities/new). On the following page you add the domain \(including subdomain\) that you want to send e-mail from. Click **Create Identity.**

Next we will need to add some entries to the DNS of our domain. Usually you do this on the website where you registered your domain.

We will add four entries in total: 

* Three entries that prevent e-mails from being changed between your sending and arrival, these are called **DKIM** keys. 
* One entry that proves you own the domain name to us, and to link it to this specific Magic Login account.

Optionally \(but highly recommended\), we will also add a fifth entry:

* One entry that is used for **SPF** _\(**Sender Policy Framework\)**_ ****that prevents others from spoofing e-mails from this domain name, and helps us link the specific domain to your Magic Login account.

Both **DKIM** and **SPF** are important for ensuring your e-mails get delivered reliablity.

{% hint style="info" %}
After you have added the required entries it may take some hours to propagate your changes, we have no way to make this faster.

Refresh the domain's _Identity Management_ page to refresh the current status. 
{% endhint %}

After succesfully verifing your subdomain \(e.g. **ml.airbnbforcats.com**\) you can now send e-mails from any username on that domain, such as **robot@ml.airbnbforcats.com**.



