# WPAD Enabled

- LAST UPDATED DATE: 11/25/2015
- LAST UPDATED BY: @mubix

## Summary

WPAD (Web Proxy Auto Discovery Protocol) affects any system that has "Auto Discovery Proxy Settings" turned on but it is on by default in Windows. This 

## Capabilities and Risk

- Steal credentials while on the same network as the user affected
- SMB or HTTP relay of credentials to NTLM based services
- Code execution when used in conjuntion with PSEXEC

## Detection

Wireshark looking for WPAD requests on the wire. 

## Remediation

Windows has per-user and per-system proxy settings making this a very difficult setting to fix enterprise wide. 

## References

- Link to blog post
- Link to CVE
- Link to Metasploit module
- Link to Nessus/NeXpose/Qualys write up

## Exploitation

### Scenario 1: Credential Stealing

```
Code and screen shots of this happening
```

### Scenario 2: SMB Relay to PSEXEC for code execution

```
Code and screen shots of this happening
```
