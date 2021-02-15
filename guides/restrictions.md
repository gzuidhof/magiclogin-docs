---
description: 'Background, user requirements and tips on e-mail deliverability'
---

# Email deliverability and reputation

## E-mail reputation

It is important that you and our service as a whole retains a good **sender reputation** so that our e-mails get delivered reliably and fast.

Usually transactional e-mails don't require special care as the user usually initiates them, as opposed to a newsletter that they may mark as SPAM if they don't remember signing up for it.

For every e-mail consider: does the user actually want to receive this e-mail? If not: don't send it.

### Customer reputation quotas

To maintain a good reputation we enforce the following guidelines ****for all Magic Login accounts:

* **Your bounce rate must be under 5%**. Bounces happen when you send e-mail to an address that doesn't exist.
* **Your complaint rate must be under 0.1%**. A complaint happens when users click buttons like _Mark as Spam_ in their e-mail client.

Both of these limits should be attainable and reasonable for all users.

If you cross these quotas you will be warned and eventually your account's ability to send e-mails may be paused. At the end of this guide are some best practices that will help keep your reputation up.

## E-mail deliverability

Our e-mails should \(and do!\) arrive in inboxes in a matter of seconds. We take every step we can to make reliable transactional e-mails as easy, transparent and accessible as possible, but unfortunately with e-mails there are never any guarantees.

We enforce best practices in terms of DNS setup with **DKIM** and **SPF** and we use world class e-mail infrastructure \(Amazon SES\) which is also used by large tech companies such as Netflix and Reddit.

### Dedicated IPs

We can offer dedicated IPs to large customers on request against an additional payment. These put your sending reputation entirely in your hands.

Dedicated IPs only make sense if you are sending at least 500,000 e-mails per month \(despite what other e-mail providers want you to believe\). At smaller sending rates they will do more harm than good. 

## Tips for good e-mail deliverability

**E-mail content**

* Add a link to your privacy policy and terms of service in the footer of the e-mail.
* Explain to the user why they received the e-mail.
* Don't use a **noreply@example.com**-like address as the `from` or `reply_to` value. It's not customer friendly and can hurt deliverability too. Instead consider setting `reply_to` to your customer support e-mail address. It doesn't have to be on the same domain.

 **Domains**

* Send from your own subdomain. While every Magic Login user gets their own **email@magiclogin.email**, it is a good idea to switch away from that address at your earliest convenience. Here's the [**guide**](sending-from-your-own-domain.md).
* Always send from a subdomain of your main domain. If your domain is **airbnbforcats.com**, send from **ml.airbnbforcats.com** \(_ml_ is short for Magic Login, but you can use any name you want\).
* Send non-transactional e-mails \(e.g. newsletters, marketing\) from a different subdomain.

**Technical**

* Prevent abuse in your sign-up form and prevent bots from entering fake e-mail addresses. You can do this by adding a CAPTCHA or a honeypot. Also limiting by IP is a good idea.
* Program an upper limit to how often you will send the same e-mail to a user. It's ok to add a **re-send verification e-mail** button, but there is no need to send the same e-mail more than 5 times in an hour.











