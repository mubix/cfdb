/*
Title: Default Credential (Printers)
Description: Default Credentials in printers are often over looked because of a misunderstood level of security risk.
Access to printers can give details used for data loss, network discovery, and firmware loading, which can allow for
additional functionalities to be loaded.
*/

- LAST UPDATED DATE: 12/16/2015
- LAST UPDATED BY: Joey M. (l0stkn0wledge)

## Summary

Most enterprise printers and many SOHO devices ship with an interface allowing for remote configuration of the devices that
are located on the network.  In many cases, the security of these systems will be overlooked due to a lack of security
understanding about the capabilities of these devices.  This can allow printers to act as a means to gain network details
and to potentially gain access to sensitive information being printed.

## Capabilities and Risk

Many of the capabilities and risks depend on the features of the printer. More advanced devices will often provide details
of the documents printers, including potential username information. Some printers may have "advanced functions" that can
provide additional network information. 

- Gain access to printer files and configuration
- Execute programs from the printer by loading custom firmware images
- Read files on the printer and potentially intercept printed files

## Detection

Printers with Web UIs will most often standard http/https ports (80/443).  Additional functionality may also be exposed
through the printer ports (e.g. HP JetDirect port 9100).  

## Remediation

Printers should have all web interface passwords changed to strong passwords. Additionally, it is important to ensure that
only SSL is available for login when the option is available.

## References

- IronGeek page on Printer Hacking (http://www.irongeek.com/i.php?page=security/networkprinterhacking)
- Deral Heiland: From Printer to Pwned (https://www.youtube.com/watch?v=PH4pTCmKgOg)
- Extensive Default Password List (http://www.defaultpassword.com/)

## Exploitation

Standard web interface used for accessing UI and entering passwords.
