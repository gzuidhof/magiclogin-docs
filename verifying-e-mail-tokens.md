# Verifying e-mail tokens

In the previous guide we sent an e-mail to **tabby@ilovecats.com** which contained a link to **`https://airbnbforcats.com/magic?mtoken=9nwTWNkNDG1TgwaNzVAt3t`**

When Tabby clicks the link she will open that page in her browser. Your server's handler for that endpoint retrieves the value of the **mtoken** query parameter and verifies it using the **verifyEmailToken** endpoint.

{% hint style="info" %}
If you are using a client-side framework such as React or Next.js you can use **fetch** or **XMLHttpRequest** to pass the token to your server.

Alternatively you can use some Javascript to embed the token into a form.
{% endhint %}

## Verifying the token

We will make a HTTP **POST** request to**`https://api.magiclogin.net/<YOUR-APP-ID>/v1/verifyEmailToken`**.

Here's the request we will make and its response:

```javascript
// Request
{
    token: "9nwTWNkNDG1TgwaNzVAt3t",
    purpose: "signup"
 }
 
 // Response
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

```

The **success** value indicated whether the verification could be performed successfully. The **data.valid** field is what indicates whether this is a valid token.

That's it, we have succesfully authenticated **tabby@ilovecats.com** and can allow her to sign up. This is all you need to know to use Magic Login to authenticate users through e-mail and to use it for e-mail verification.

In some cases however you will want to _**consume**_ the token, which marks the token so it can not be used again. You should do this when you use Magic Login for logging in users. We'll cover that next.

## Consuming the token \(optional\)

{% hint style="success" %}
### Tip: _****_don't immediately consume the token on page load

First check validity, passing**`consume: false`**_**.**_ If the token is valid show the user a page that allows them to perform the action using a button, instead of doing so automatically.

For a login action this could be a big button that says: **"Sign in to AirBnB for Cats"**. For signup this could be a form where the user has to fill additional details for account creation \(e.g. their name, address, etc\). You can embed the token in the form using a hidden field.

When the user clicks the button or submits the form, verify the token again - this time with **`consume: true`**.

**Why?**

It allows users that accidentally open the link in the wrong browser to copy paste the URL to a different one \(perhaps even on a different device\). 

Also some poorly configured e-mail providers will fetch all URLs as part of their virus scans.
{% endhint %}

When we actually sign Tabby in, we can verify the token again, but this time with `consume: true`

The `consume`  field allows you to mark the token as "used" after this verification, which means it can never be used again.

```javascript
 { // Request
    "token": "9nwTWNkNDG1TgwaNzVAt3t",
    "purpose": "signup",
    "consume": true
 }
```

```javascript
{ // Response
  success: true,
  data: {
    valid: true,
    token_id: 'GdyU4bHKeRDYxjrn7y4Fk576HHDpCLyaoNYRUgAtKKGf',        
    email: 'tabby@ilovecats.com',
    user_data: '',
    purpose: 'signup',
    consumed: true,
    expires_at: '2021-02-16T03:51:34.511Z',
    created_at: '2021-02-16T03:21:34.511Z'
  }
```

The token can now no longer be used.

 ****and marked the token as **consumed**. Depending on your application you may never consume the tokens. 

Check out the **API** section in the sidebar for more details on these two endpoints.

{% page-ref page="api/verifying-tokens.md" %}

## **Extra Credits**

 For completeness and as a sanity check let's try verifying the token one more time:

```javascript
 { // Request
    "token": "9nwTWNkNDG1TgwaNzVAt3t",
    "purpose": "signup",
    "consume": true
 }
```

```javascript
{ // Response
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

Note that now the token is `valid: false`



