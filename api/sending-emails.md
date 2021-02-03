---
description: Sending e-mails is what Magic Login is all about.
---

# Sending Emails

{% api-method method="post" host="https://api.magiclogin.net" path="/v1/sendTemplateEmail" %}
{% api-method-summary %}
Send Template Email
{% endapi-method-summary %}

{% api-method-description %}
This method is how you send e-mails that look good without having to deal with e-mail HTML yourself.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Your API Token, in the form of \`Bearer &lt;api-token&gt;\`  
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="subject" type="string" required=false %}
The subject for the e-mail, visible in the user's e-mail client before they open the e-mail.
{% endapi-method-parameter %}

{% api-method-parameter name="reply\_to" type="string" required=false %}
E-mail address you want users to reply to, this can be any e-mail address.
{% endapi-method-parameter %}

{% api-method-parameter name="from" type="string" required=false %}
E-mail address that you want to send from. Note you will need to add your own domain as an **Identity** if you want to use it here.
{% endapi-method-parameter %}

{% api-method-parameter name="to" type="string" required=true %}
E-mail address you want to send the e-mail to
{% endapi-method-parameter %}

{% api-method-parameter name="style" type="object" required=false %}
The **TemplateStyle** object for this e-mail, see below.
{% endapi-method-parameter %}

{% api-method-parameter name="content" type="object" required=true %}
The **TemplateEmailContent** object for this e-mail, see below.
{% endapi-method-parameter %}

{% api-method-parameter name="app\_id" type="string" required=true %}
Your application ID
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```
{"name": "Cake's name",    "recipe": "Cake's recipe name",    "cake": "Binary cake"}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```
{    "message": "Ain't no cake like that."}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



