/*
Title: Cross Site Trust Exploitation
Description: Injection of static content to trick users.
*/

- LAST UPDATED DATE: 2015/12/1
- LAST UPDATED BY: @zaeyx

## Summary

Cross site trust exploitation occurs when an attacker is able to inject data into a web page for the purpose of making the site appear to say something it otherwise would not.
This results in the user's trust in the site being exploited.  No actual code execution is required.

## Capabilities and Risk

XSTE may allow an attacker to trick users into performing actions that they otherwise would not.  If the user trusts that the content of the site cannot be set by anyone other than the site itself the user is highly likely to trust any content appearing on the site.  

The attacker might use for example, an error field in a form which allows injecion of arbitraty (non-code) content to make the error field appear to read that the user must contact the "site admin" @ "malicious@email.com".  

## Detection

Detection may be accomplished by monitoring site content and potential injection points.  Your best hope is not detection, but rather remediation.

## Remediation

You must not allow injection into any portion of your application where injected content would appear to be coming from the site itself.  The user must not be able to in any way edit error fields for example.  (This commonly occurs when a web developer creates one error page which takes the error message as a parameter.)

## References

http://www.lanmaster53.com/2014/05/cross-site-trust-exploitation/

## Exploitation

The exploitation of this vulnerability is specific to the application in question.  It commonly requires nothing more than the attacker writing content into a sanitized field which does not properly format its output to clarify the origin of the content.

Pleae see the attached blog post for more information.
