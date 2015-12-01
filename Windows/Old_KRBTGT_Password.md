/*
Title: Old KRBTGT Password
Description: Search engine meta data about the finding
*/

- LAST UPDATED DATE: 2015/11/25
- LAST UPDATED BY: @mubix

## Summary

Commonly referred to as the "Golden Ticket", this vulnerability stems from the fact that the KRBTGT user account that Microsoft uses to "sign" tickets isn't forced to change and is often discounted due to the fact that it expires soon after the domain is created. If an attacker is able to gain access to the password hash of this account (usually by dumping the domain hashes), they will be able to create kerberos ticket to log in to any Windows domain service or share as any user they wish, even fake ones, with any group membership they wish.

## Capabilities and Risk

- Anyone with access to the KRBTGT user account's password hash can effectively authenticate as any user in the domain until the account's password has been changed twice.

## Detection

- TODO add detection mechanisms, there are a few

## Remediation

Set up a script to change the password of the KRBTGT account password once a day. This limits the possible abuse window to 48 hours (because of the requirement to change the password twice to be effective). With a 48 hour window, it is less likely that an abuse of the Golen Ticket will be beneficial to an attacker or insider who has gotten to the point where they can dump the KRBTGT's account password hash.

## References

- Kerberos & KRBTGT: Active Directory’s Domain Kerberos Service Account: https://adsecurity.org/?p=483

## Exploitation

A write up on how this vulnerability can be exploited with demo code or screen shots

