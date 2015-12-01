/*
Title: Command Injection
Description: Injection of commands through web application onto host machine.
*/

- LAST UPDATED DATE: 2015/12/1
- LAST UPDATED BY: @zaeyx

## Summary

Command Injection occurs when an insecure application passes unsafe user supplied content to a system shell.  

## Capabilities and Risk

When Command Injection occurs, and attacker may be able to execute arbitrary commands as the web application's host machine.  This gives effective control over whatever portion of the host machine the web server's user is given access to.  

## Detection

Detection can be accomplished by searching for command line access by the web server's user that is not expected to have been given by the normal operations of the application.  For example, if an application uses command line operations to perform a ping.  If the web server's user is executing any command other than "ping" you might have a problem.

## Remediation

Sanitize input that is passed to the system shell from an untrusted source.

## References

https://www.owasp.org/index.php/Command_Injection

## Exploitation

To exploit this vulnerability, an attacker simply injects into a vulnerable field a command seperator for the system type (linux, windows) of the host machine in question.  Followed by the command to be executed.  

The command seperator is used to end the command that the application expects to execute, and everything that follows is added as commands appended to the application's usual request.

For example, if an application takes user input in the form of an IP address to "ping" from the command line; and the application does not correctly sanitize input:  A normal request might look like "ping user_supplied_ip".  The injection might look like "ping && cat /etc/passwd".
