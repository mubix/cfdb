/*
Title: Weak SSL Configurations
Description: Availability of weak encryption (e.g. DES, RC4, NULL) and hash (e.g. MD4, MD2) algorithms can make SSL/TLS 
communications more suspectible to Decryption and Manipulation. In addition, vulnerabilities in old versions of SSL can
lead to information disclosure.
*/

- LAST UPDATED DATE: 12/14/2015
- LAST UPDATED BY: Joey M. (l0stkn0wledge)

## Summary

Many web servers still support out dated methods of securing connections with SSL/TLS.  These methods can make the 
communications between the server and clients more suspectible to both traditional man-in-the-middle attacks and to more
sophisticated attacks where the SSL Handshake is intercepted and modified to create weaker connections between the client
and the server.

## Capabilities and Risk

This can be used to lead to the exposure of encrypted communications, which are often used to transmit sensitive data,
which includes (but is not limited to):

- Usernames/Passwords
- Personally Identifiable Information
- Personal Health Information
- Financial Data

## Detection

Readily available tools like 'sslscan' can be used to determine the versions of SSL/TLS and cipher suites supported by a 
server. Servers can also be tested using 'openssl s_client', which has several configuration options for enabling different
versions of SSL/TLS and cipher suites.  This can allow for testing a server's connection and determining the supported 
cipher suites.

## Remediation

The best remedy for this solution is to ensure that web servers relying upon SSL/TLS are using up-to-date cipher suites
that offer appropriate levels of protection.  Modern cipher suites making use of algorithms like AES and SHA-256 are 
examples of the algorithms to consider for use.  Servers should be configured to a minimum SSL/TLS version of TLS v.1.0

## References

- TLS Wikipedia (https://en.wikipedia.org/wiki/Transport_Layer_Security)
- Mozilla Wiki on Server Hardening (https://wiki.mozilla.org/Security/Server_Side_TLS)
- OWASP TLS Cheat Sheet (https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet)
- CVE-2014-3566 "POODLE" (https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2014-3566)

## Exploitation

1. An attacker can use methods like ARP Spoofing or rogue wireless access points to intercept network communications
2. Use iptables to re-direct to your proxy listening port:
    iptables -t nat -A PREROUTING -p tcp --destination-port 443 -j REDIRECT --to-ports <$listenPort>
3. Use proxy tool (e.g. mitmproxy) to intercept the connection and alter SSL Handshake so client only requests weaker
versions of SSL and/or weaker ciphers (configuration will vary depending on the tool(s) used.
