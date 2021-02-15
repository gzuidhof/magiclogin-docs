---
description: Sending your first e-mail using the Magic Login API
---

# Setting Up

## Creating an Application

**Applications** are organizational units within your account that help you keep your different websites/apps separated. Think of them as projects: if you are building both _**AirBnB for Cats**_ and _**Netflix for Dogs**_ ****it would make sense to create two separate Applications for that.

All API requests you make are associated with a certain Application. You can create one from the [**Applications page**](https://magiclogin.net/dashboard/applications) in the dashboard.

After creating it an **Application ID** will be shown which we will need later, it looks like `app_aBcDeFg`. You can hardcode this value in your application code.

## Creating an API Token

When you talk to the Magic Login API we need to know who you are, that's what API Tokens are for. You can create as many as you would like.

You can create an API token on the [**API Tokens**](https://magiclogin.net/dashboard/apiTokens) page in the dashboard. It's a good idea to name them after where they are used \(e.g. _**AirBnB for Cats production webserver**_\).

Don't worry if you lose your API token, you can always generate a new one.

{% hint style="warning" %}
**API Tokens are secret**, treat them as a password! 

API Tokens are only visible after they have just been created and can not be recovered later.
{% endhint %}

## Ready for the launch

Now we have the two pieces of information, an **Application ID** and an **API Token**. That's all we need to start using the Magic Login API, let's go!

