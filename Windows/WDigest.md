/*
Title: WDigest Enabled
Description: WDigest Clear-Text Password Storage Enabled
*/ 

- LAST UPDATED DATE: 2015/11/25
- LAST UPDATED BY: @mubix

## Summary

WDigest is an authentication funtion that is built into Windows. It is used to allow automatic authentication against web applications that require Digest authentcation (MD5). In order to provide the MD5 hash automatically, Windows stores the clear text version of that the user's password. Tools like Mimikatz and WCE provide a way to dump these passwords out of memory with the use of administrative access to a system. Mimikatz even has the ability to do this offline with a memory dump of a system's LSASS process.

## Capabilities and Risk

- Lateral code execution and access to all systems that require only password authentication. Due to the fact that Pass-the-Hash is non-trivial with RDP and usually requires specific settings to be set, a clear text credential is much more damaging to an organization.

## Detection

- Host level by detecting Mimikatz or WCE usage
- Network level by mass usage of credentials. Attackers need to find where the credentials dumped can be used and the usual way to do this is to test them out and see where access is granted


## Remediation

- Disable WDigest storage by applying the patch KB2871997 to all applicable systems

## References

- Patch for Wdigest storage: http://blogs.technet.com/b/kfalde/archive/2014/11/01/kb2871997-and-wdigest-part-1.aspx

## Exploitation

### Using Mimikatz to dump clear text credentials

```
```
