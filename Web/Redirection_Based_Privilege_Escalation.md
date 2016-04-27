/*
Title: Redirection Based Privilege Escalation
Description: Leverage of XSS on one page to escalation control over application flow.
*/

- LAST UPDATED DATE: 2015/12/1
- LAST UPDATED BY: @zaeyx

## Summary

Redirection Based Privilege Escalation describes a situation in which a web application is split into at least two parts.  One highly secure section (such as a payment system) and one less secured section (an index page perhaps).  When an attacker gains access to the less secure portion of the site, he may leverage this capability to gain access to the application flow and in effect escalate his privileges to exploit the more secure section.

## Capabilities and Risk

An attacker may utilize this technique to turn access to a less secured section of a site into full application flow control. 

More work is spent securing the highly sensitive section of the site.  But a vulnerability is a less sensitive section of the site is potentially just as dangerous under this model.

## Detection

Detection relies on the application defense team being able to detect the underlying XSS in the less sensitive portion of the application.  

Additional detection methods include writing hidden javascript routines into the code of the site which send an alert home if they are hosted somewhere other than the original site.

## Remediation

Do not keep the security of one portion of the site your highest priority.  Control over application flow can be achieved with an injection to any section for the subset of users which visit that section.

## Exploitation

An attacker may in effect escalate their privileges to gain access to application flow by first finding an injectable field in any one portion of the site.  The attacker then injects into that field a script that performs a redirection to a site that they have control over.  The attacker clones the insecure application and redeploys a copy on their malicious site.  

When a user visits the page containing the injection they are redirected to the attacker's malicious copy of the vulnerable application.  This happens transparently, and unless the user is exceptionally privy they are unlikely to notice the redirection.  They will then continue to use the application as before.  Potentially accessing the highly secure sections (such as the payment system) on the attacker's malicous site.
