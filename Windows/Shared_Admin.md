/*
Title: Shared Local Windows Admin Password
Description: Search engine meta data about the finding
*/

- LAST UPDATED DATE: 2015/11/25
- LAST UPDATED BY: @mubix

## Summary

Pass the Hash is 

## Capabilities and Risk

- Lateral code execution and access to all systems with same local admin password

## Detection

?? Other than dumping hashes and trying it out yourself, I'm lost on this one

## Remediation

- Disable the local Administrator (RID 500) account. Or simply do not enable the account as it has been disabled by default since Windows Vista 
- Enable LocalAccountTokenFilterPolicy registry key as detailed in the references
- Use Microsoft's LAPS or alternative local account randomization tool to randomize the local account passwords.

## References

- Pass the Hash: https://en.wikipedia.org/wiki/Pass_the_hash
- Microsoft LAPS: https://www.microsoft.com/en-us/download/details.aspx?id=46899

## Exploitation


### Dumping hashes from exploited machine then using the hash to access other machines on the network

```
```