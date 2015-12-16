/*
Title: Server-Side Request Forgery (SSRF)
Description: Server-Side Request Forgery, SSRF, CWE-918, CWE-441, A1-Injection
*/

- LAST UPDATED DATE: 12/7/2015
- LAST UPDATED BY: @sethsec

## Summary

The application takes a URL from the user and retrieves the contents of the URL on behalf of the user.  However, the application does not sufficiently validate the requested destination. (Paraphrased from CWE-918) 

## Capabilities and Risk

- By exploiting SSRF, an attacker can make requests from the application server.
- An attacker can interact with otherwise restricted IP addresses and services, either on the server itself (localhost), or on other IPs. This can give an external attacker visibility to an internal environment.  This includes using the vulnerable server to port scan other hosts (Cross Site Port Attacks (XSPA)). 
- If the vulnerable server can communicate with backend API's or services that do not require authentication, the external attacker can fully interact with those services.  
- If the vulnerable application is hosted in a cloud environment, such as Amazon EC2 and OpenStack, this may allow the attacker to gain access to metadata services, which can be used to gain access to sensitive information, sometimes including credentials or private keys.  

## Detection

1) Browse the target application using an intercepting proxy (Burp, Fiddler, ZAP, etc). Determine if the following conditions apply:
  - The target application is accepting a URL from you.  Ex: www.thirdpartysite.com
  - The target application is displaying part or all of the result back to you.

2) If both conditions apply, look at your proxy logs.  If you do not see the request to the resource (www.thirdpartysite.com) in your proxy logs, but you see the content on the page, this indicates that the content returned to you has been requested by the server itself on your behalf. This behavior indicates the application is vulnerable to SSRF.    

## Remediation

Rather than proxying requests on behalf of users, the application should have the user’s browser retrieve the desired information. If it is necessary to proxy the request, a whitelist should be used on the server side and the User-Agent information should be stripped or modified.        

## References

- [OWASP Top 10 2013-A1-Injection](https://www.owasp.org/index.php/Top_10_2013-A1-Injection)
- [CWE-918: Server-Side Request Forgery (SSRF)](http://cwe.mitre.org/data/definitions/918.html)
- [CWE-441: Unintended Proxy or Intermediary ('Confused Deputy')](http://cwe.mitre.org/data/definitions/441.html)
- [EC2 Instance Metadata Service Documentation](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
- [OpenStack Metadata Service Documentation](http://docs.openstack.org/admin-guide-cloud/content/section_metadata-service.html)
- [Compromising an unreachable Solr server with CVE-2013-6397](http://www.agarri.fr/kom/archives/2013/11/27/compromising_an_unreachable_solr_server_with_cve-2013-6397/index.html)
- [Bringing a Machete to the Amazon](https://www.youtube.com/watch?v=JTOWxi17k-w)
- [Prezi Got pwned - A tale of responsible disclosure](http://engineering.prezi.com/blog/2014/03/24/prezi-got-pwned-a-tale-of-responsible-disclosure/)

## Exploitation

Once you have determined that the application is vulnerable to SSRF, the vulnerability can be exploited in many different ways.
- Manually testing SSRF using a browser (GET Requests), or something like Burp Repeater (POST Requests)
  - The level of risk you can demonstrate depends on how much you know about the environment.  
  - Is the vulnerable application hosted on a service that uses a metadata service (ex: http://169.254.169.254)?
    - If so, pull up the reference documents above and make some requests to valid metadata service endpoints for your respective service. 
    - EC2: http://www.example.com/?url=169.254.169.254/latest/dynamic/instance-identity/document
- To discover services, exploit SSRF to perform a XSPA.  One simple way to do this is to use Burp Intruder. 
  - Send the initial Request to Burp Intruder
  - For the URL, use http://host:port format, and make the port the position
  - For the payload, enter the port numbers you want to test (only TCP works)
  - Start the attack. 
    - Pay attention to the response times for each requested port. You should be able to infer which ports are open and which ports are closed based on the response times. Quicker times are open ports, longer times are closed ports (they timed out before the client gave up). 
- Can you target other services via SSRF that are not directly accessible to you?
  - You could even run a tool like dirbuster or the http-enum NSE via SSRF. 


