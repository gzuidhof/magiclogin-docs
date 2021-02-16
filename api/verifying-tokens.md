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
Check that the token had a specific purpose. If this value is not passed no check is performed.
{% endapi-method-parameter %}

{% api-method-parameter name="consume" type="string" required=true %}
Consumes this token after verification: the token can not be used again if you pass true here.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Verification successful  
  
⚠️ **Note that the token may still be invalid** ⚠️ **** Always check **data.valid**. See below for the possible values of **data.reason** in case of an invalid token.
{% endapi-method-response-example-description %}

```javascript
// Token found and it's valid
{
  success: true,
  data: {
    valid: true,
    token_id: 'GdyU4bHKeRDYxjrn7y4Fk576HHDpCLyaoNYRUgAtKKGf',        
    email: 'tabby@ilovecats.com',
    user_data: '',
    purpose: 'signup',
    consumed: false,
    expires_at: '2021-02-16T03:51:34.511Z',
    created_at: '2021-02-16T03:21:34.511Z'
}


// Token not found
// Maybe it's made up by your user, or it expired a long time ago.
{ success: true,
  data: {
    valid: false,
    reason: 'not_found'
}


// The token was already consumed (=used).
{
  success: true,
  data: {
    valid: false,
    token_id: '9bBgLz1x6qvQzbRLDn4hZcSySSDQzM5F22FvGEYnUve3',        
    reason: 'already_consumed',
    email: 'tabby@ilovecats.com',
    user_data: '',
    purpose: 'signup',
    consumed: true,
    expires_at: '2021-02-16T03:51:34.511Z',
    created_at: '2021-02-16T03:21:34.511Z'
  }
}

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Invalid token reasons

* `"not_found"`: Token not found, perhaps tried to make their own token or their token expired a long time ago and has since been cleaned up.
* `"expired"`: The token has expired.
* `"already_consumed"` : This token has already been marked as "consumed".
* `"invalid_purpose"` : The purpose of the token does not match the purpose passed in your request. 

In the case of `"expired"`, `"already_consumed"` and `"invalid_purpose"` the token's data will still be returned including any **user\_data** you may have passed. In case of `"not_found"` this is of course not possible.

