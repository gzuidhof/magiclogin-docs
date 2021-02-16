---
description: >-
  Verifying that the clicked link in an e-mail is valid and retrieve its
  associated data.
---

# Verifying Tokens

{% api-method method="post" host="https://api.magiclogin.net" path="/v1/{app\_id}/verifyEmailToken" %}
{% api-method-summary %}
Verify Email Token
{% endapi-method-summary %}

{% api-method-description %}
Verify that the token that was sent in an e-mail is valid, retrieve the associated **purpose**, **user data** and **e-mail address**.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="app\_id" type="string" %}
Your **Application ID** \(copy it from the Applications page\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
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



