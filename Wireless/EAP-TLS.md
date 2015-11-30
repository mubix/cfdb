/*
Title: WPA EAP-TLS Mode Certificate Only
Description: Finding when EAP-TLS is in a mode that only requires a client certificate be present.
*/

- LAST UPDATED DATE: 2015/11/25
- LAST UPDATED BY: @mubix

## Summary

EAP-TLS based authentication is the best form of Wireless security currently available because of the need for a client certificate to authenticate to the wireless. However, without additional authentication it is difficult to detect misuse or theft of the client certificate.

## Capabilities and Risk

- Theft / Creation of valid certificate used for continued access wireless network

## Detection

1. Use of of client certificates on multiple IP addresses
2. Reissuance of certificates with export flag enabled

## Remediation

1. Revoke certiicate effected and start investigation into the user(s) effected. Unless re-issued in order to be exportable, administrative access to the machine it was installed on is needed in order to extract the certificate.

## References

- Setting up EAP-TLS with Cisco WLC: https://networklessons.com/wireless/peap-and-eap-tls-on-server-2008-and-cisco-wlc/
- Stealing User certificates with Mimikatz:
  - http://carnal0wnage.attackresearch.com/2012/10/more-with-mimikatz-crypto-module.html
  - http://www.darkoperator.com/blog/2013/6/11/stealing-user-certificates-with-meterpreter-mimikatz-extensi.html
- KeyRaider malware steals certificates from iPhone: http://researchcenter.paloaltonetworks.com/2015/08/keyraider-ios-malware-steals-over-225000-apple-accounts-to-create-free-app-utopia/


## Exploitation

### Scenario 1 - Exporting Certificate via Mimikatz

```
Test
```
