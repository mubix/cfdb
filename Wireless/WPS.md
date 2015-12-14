/*
Title: Wifi Protected Setup (WPS)
Description: Pin-based WPS is susceptible to brute force attacks that could allow unauthorized access to WiFi networks. 
Devices relying on physical methods are vulnerable to physical attacks to allow network access.
*/

- LAST UPDATED DATE: 12/14/2015
- LAST UPDATED BY: Joey M. (@l0stkn0wledge)

## Summary

WPS is a feature most often found on home wireless routers; however, due to a large overlap in the home, small office, and
small business markets, the feature has crept into some smaller corporate environments where wireless networks are setup
using more commodity hardware.

WPS can pose a variety of risks for wireless network security. The PIN-based method can be vunerable to brute force attacks
over the air. Other types (e.g. push-button methods) would require physical access to the router.

## Capabilities and Risk

This would allow an attacker to gain unauthorized access to a wireless network, thereby allowing for additional access
into the network and systems attached to that connection.

## Detection

WPS settings can be confirmed by examining the configuration of your wireless router. Button-based WPS methods will have a
button located on the router.

## Remediation

Disable WPS on wireless access points. If a device cannot disable WPS, default PIN values should be changed. Physical 
access to the router should be limited and secured to prevent local, physical attacks using WPS.

## References

- WPS Wikipedia (https://en.wikipedia.org/wiki/Wi-Fi_Protected_Setup)
- Reaver on Google Code (https://code.google.com/p/reaver-wps/)
- Cert Write-up on WPS PIN Vulnerability (http://www.kb.cert.org/vuls/id/723755)

## Exploitation

```
reaver -i [monitor interface number] -b [ESSID] -v
```
