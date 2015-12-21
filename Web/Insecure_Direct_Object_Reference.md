/*
Title: Insecure Direct Object Reference
Description: Directly access application objects (files, database records, messages, etc.) owned by other users
*/

- LAST UPDATED DATE: 12/14/2015
- LAST UPDATED BY: Mike S. (hardwaterhacker)

## Summary

Insecure Direct Object Reference results from using user-supplied input to directly reference objects.  Insecure 
Direct Object References allow attackers directly reference objects by manipulating the parameter value controlling
the object reference, allowing access to objects owned by other application users.

## Capabilities and Risk

Capabilities:
- Direct access to database records, messages, files, etc.

## Detection

To detect Insecure Direct Object Reference, the application must first be mapped to identify parameters which may 
control object references, such as ?invoice=12345 or ?msgId=654321.  After identifying potential testing points, attempt 
to enumerate other objects by manipulating the value associated with the identified parameter.  Insecure Direct Object 
Reference exists when the application returns objects belonging to other application users.

Typically, Insecure Direct Object Reference exists within the authentication boundary of the application.  However, in 
poorly designed authentication and authorization schemes, it may be possible to access objects for which authentication 
is normally required.  For example, if a company's support page offers only certain knowledgebase articles to 
unauthenticated users and requires authentication for all others, it may be possible to access articles which normally 
require authentication.  In this example, if kbarticle.php?article=12345 is viewable by unauthenticated users, but 
article=55555 is intended for only authenticated users, if article=55555 is accessible by an unauthenticated user then 
Insecure Direct Object Reference exists.

## Remediation

To prevent Insecure Directo Object References, the web application must assign ownership of each referenceable object to 
a given user, set of users, or group.  Whenever objects are referenced, the authorization record for the referened 
object must be compared against the requesting user.  Users lacking appropriate authorization should be denied access to 
the object.

## References

https://www.owasp.org/index.php/Top_10_2013-A4-Insecure_Direct_Object_References
https://cwe.mitre.org/data/definitions/639.html
https://cwe.mitre.org/data/definitions/22.html
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-8487
http://blog.attify.com/2015/05/26/offensive-security-oscp-student-control-panel-owned/

## Exploitation

1. Identify parameters which reference objects
2. Enumerate objects using BurpSuite Intruder or similar methods
3. Determine if objects are owned by another user or should be referenceable by requester

```
```
