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

Using the reference on [craig-tolley.co.uk](http://www.craig-tolley.co.uk/2011/08/30/disable-automatically-detect-settings-in-internet-explorer/) you can set a VB script to run as a Logon Script that will disable this setting.

## References

1. https://www.wikipedia.org/wiki/Web_Proxy_Autodiscovery_Protocol
2. http://www.netresec.com/?page=Blog&month=2012-07&post=WPAD-Man-in-the-Middle
3. http://www.craig-tolley.co.uk/2011/08/30/disable-automatically-detect-settings-in-internet-explorer/

## Exploitation

### Scenario 1: Credential Stealing

```
Code and screen shots of this happening
```

### Scenario 2: SMB Relay to PSEXEC for code execution

```
Code and screen shots of this happening
```
