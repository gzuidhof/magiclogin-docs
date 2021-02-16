---
description: The format of errors our API returns
---

# API Errors

Things can go wrong, sometimes it's you, and sometimes it's us.

## API Errors

Our errors should always follow this format \(based on [JSON API](https://jsonapi.org/examples/#error-objects)\):

```javascript
{
  "success": false,
  "errors": [
    {
      "code": "authentication_error",
      "message": "API token invalid or not found",
      "detail": "Check the api token you provided or create a new one."
    }
  ]
}
```

`success` will always be **false** in case of an error, `mesage` and `code`will always be present, `detail` may not be present.

The possible values for `code` are

* `authentication_error:` Failure to properly authenticate yourself in the request. Status **401** or **403**.
* `invalid_request_error:` Your request is invalid for the given endpoint. Status **400**, **402** or **404**.
* `api_error:` API errors cover any other type of problem \(e.g., a temporary problem with Magic Login's service\). Of course we do our best to make sure these never happen. Status **500**, **502**, **503** or **504**
* `rate_limit_error:` You made too many requests in a short period of time. Status **429**

{% hint style="info" %}
The `errors`array will always contain at least one value, it may contain multiple values \(but it's OK to only handle first error in your code.
{% endhint %}

It is possible that in the future more error codes will be added.

### **A word of caution**

The status code and `success` field returned by API endpoints indicate whether the request was succesful or not.

If you make a request to verify a token and it returns `success: true` with HTTP status code **200**, the token may still be invalid! Check the corresponding field in the data field.

