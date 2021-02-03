---
description: >-
  Verifying that the clicked link in an e-mail is valid and retrieve its
  associated data.
---

# Verifying Tokens

{% api-method method="post" host="https://api.cakes.com" path="/v1/verifyEmailToken" %}
{% api-method-summary %}
Verify Email Token
{% endapi-method-summary %}

{% api-method-description %}
Verify that the token that was sent in an e-mail is valid, retrieve the associated **purpose** and **e-mail address**.  
  
Example:  
If I sent an e-mail to user **ilovecats@gmail.com** with an action to sign up for my service, the button in the e-mail may point to something like **https://airbnbforcats.com/magic?mtoken=2Nk3EwCaQKLmnT**. This endpoint allows you to verify that \`2Nk3EwCaQKLmnT\` is a valid token and that it was in fact **ilovecats@gmail.com** that clicked the link.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" %}
ID of the cake to get, for free of course.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
API token, in the form of \`Bearer &lt;api-token&gt;\`
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
The token that was in the URL \(with the \`mtoken\` key\).
{% endapi-method-parameter %}

{% api-method-parameter name="purpose" type="string" required=false %}
Check that the token had a specific purpose.
{% endapi-method-parameter %}

{% api-method-parameter name="app\_id" type="string" required=true %}
Your Application ID.
{% endapi-method-parameter %}

{% api-method-parameter name="consume" type="string" required=true %}
Consumes this token after verification: the token can not be used again if you pass true here.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```
{    "name": "Cake's name",    "recipe": "Cake's recipe name",    "cake": "Binary cake"}
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



