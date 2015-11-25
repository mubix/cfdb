# WDigest Clear-Text Password Storage Enabled

- LAST UPDATED DATE: 2015/11/25
- LAST UPDATED BY: @mubix

## Summary

Mimikatz

## Capabilities and Risk

- Lateral code execution and access to all systems that require only password authentication

## Detection

- Host level by detecting Mimikatz usage
- Network level by mass usage of credentials. Attackers need to find where the credentials dumped can be used and the usual way to do this is to test them out and see where access is granted


## Remediation

- Disable the local Administrator (RID 500) account. Or simply do not enable the account as it has been disabled by default since Windows Vista 
- Enable LocalAccountTokenFilterPolicy registry key as detailed in the references
- Use Microsoft's LAPS or alternative local account randomization tool to randomize the local account passwords.

## References

- Patch for Wdigest storage: http://blogs.technet.com/b/kfalde/archive/2014/11/01/kb2871997-and-wdigest-part-1.aspx

## Exploitation


### Dumping hashes from exploited machine then using the hash to access other machines on the network

```
```
