---
description: Sending e-mails is what Magic Login is all about.
---

# Sending Emails

{% api-method method="post" host="https://api.magiclogin.net" path="/v1/{app\_id}/sendTemplateEmail" %}
{% api-method-summary %}
Send Template Email
{% endapi-method-summary %}

{% api-method-description %}
This endpoint is for sending e-mails that look great without having to deal with any of the nitty gritty.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="app\_id" type="string" required=false %}
Your **Application ID** \(copy it from the Applications page\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
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
E-mail address that you want to send from. Note you will need to add your own domain as an **Identity** if you want to use it here. Check the _Identities_ page in the dashboard.
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

### TemplateEmailContent

```typescript
interface EmailTemplateContent {
    /**
     * OPTIONAL
     * The preheader is the summary text that follows a subject line when the email is viewed in an inbox.
     * In many cases, it's used to provide a short summary of the email, and is typically one sentence long.
     * 
     * NOTE: This content is not visible in the e-mail itself, only the inbox.
     */
    preheader?: string;

    /**
     * OPTIONAL
     * The URL and name of the product used in the link at the top of the e-mail.
     * You should point this at the homepage of your app/website.
     * 
     * Defaults to the Application name and URL.
     */
    product?: {
        url: string;
        name: string;
    }
    /**
     * OPTIONAL
     * The main text content of your e-mail that appears above the action button.
     * 
     * Markdown enabled.
     */
    main?: string;
    
    /**
     * OPTIONAL
     * Describes the main action button in the e-mail.
     * If you don't specify the action object, there will be no button in the e-mail.
     */
    action?: {
        /**
         * The URL of the action, for example https://airbnbforcats.com/magic/signup
         * The email auth token (mtoken) gets added automatically to this URL.
         */
        url: string;
        /**
         * The button text.
         */
        name: string;
        /**
         * OPTIONAL
         * The "purpose" of the action. Use a short value to describe what the token should be valid for,
         * such as "signup" or "login".
         * 
         * When you verify the token you can verify this expected purpose to ensure somebody isn't using a token
         * for an unintended purpose.
         * 
         * Default to an empty string.
         */
        purpose?: string;
        /**
         * You can specify some user data to associate with the email auth token that will be returned
         * when you verify this token. You could add information about the user here (e.g. their user ID).
         * 
         * Must be a string, up to 2KB in size, which should be large enough for a small JSON object.
         */
        user_data?: string;
        /**
         * OPTIONAL
         * How long the action's token should be valid for in seconds.
         * 
         * Defaults to 1800 seconds (=30 minutes), and can be at most 14 days.
         */
        expiry_in_seconds?: number;
    }
    /**
     * OPTIONAL
     * The content shown below the action.
     * 
     * Markdown enabled.
     */
    outro?: string;
    /**
     * OPTIONAL
     * Content that is shown just below the main e-mail content, usually here you would put extra help text for the user.
     * Such as: "If you don't want to log in, you can safely ignore this e-mail", or "You are receiving this e-mail because
     * someone ...".
     * 
     * Markdown enabled.
     */
    sub?: string;
    /**
     * OPTIONAL
     * Shown at the very bottom of the e-mail.
     * 
     * This is a good place to put your company name and address, as well as links to your terms of service and privacy policy.
     * 
     * Markdown enabled.
     */
    footer?: string;
}

```

### TemplateStyle

```typescript
interface EmailTemplateStyleOptions {
   /**
    * OPTIONAL
    * The CSS color of buttons in your e-mail.
    * For maximum compatability use a hex color such as "#FAEECC".
    * 
    * Defaults to a dark blue color.
    */
   button_color?: string,
   /**
    * OPTIONAL
    * Whether to use a custom font.
    * 
    * Custom fonts in e-mails have to be loaded from a third party (usually Google Fonts), which means they are not great for your user's privacy.
    * 
    * Defaults to `true`.
    */
   custom_font?: boolean,
   /**
    * OPTIONAL
    * Whether to offer dark mode support.
    * 
    * Defaults to `true`.
    */
   dark_mode?: boolean,
}
```

