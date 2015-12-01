/*
Title: SQL Injection
Description: Injection of SQL commands directly into databse
*/

- LAST UPDATED DATE: 2015/12/1
- LAST UPDATED BY: @zaeyx

## Summary

SQL Injection occurs when a unsanitized field takes content from an untrusted source and passes it directly into an SQL query.

## Capabilities and Risk

SQL Injection allows an attacker to execute arbitrary SQL in the context of the web application.  Potentially gaining the ability to read, write, and modify database contents.

## Detection

Detection can be accomplished by whitelisting known database lookups performed by the web application, and alerting if any commands other than the whitelisted ones are executed against the database in the context of the web application.

## Remediation

Correctly sanitize input into the database from any and all untrusted sources.

This resource provides instructions for proper sanitization in a number of languages: http://bobby-tables.com/

## References

https://www.owasp.org/index.php/SQL_Injection

## Exploitation

An attacker can exploit this vulnerability by simply injecting arbitrary SQL into an unsanitized input field.  The attacker is usually required to properly guess the format of the query into which his input in injected.  He can then reverse engineer the format, causing his data to in effect "break out" of the query and create it's own.

For example.  If a query performs a lookup of username by first name in a users table it might look something like this, 'SELECT username FROM users WHERE firstname="user_supplied_firstname"'.  In this scenario, the attacker would be able to "break out" of the query by setting his input like so user_supplied_firstname = jimmy"; SELECT passwd FROM users;--

The final query would look like this: SELECT username FROM users WHERE firstname="jimmy"; SELECT passwd FROM users;--"

This would select and (potentially, based on the application) display all the passwords in the database.
