/*
Title: PowerShell
Description: PowerShell is a power scripting environment that is built-in to all modern Windows systems. When not locked
down and properly configured this can give an attacker a great deal of access and the ability to perform functions which
otherwise might not be possible without having the ability to install other tools.
*/

- LAST UPDATED DATE: 12/16/2015
- LAST UPDATED BY: Joey M. (@l0stkn0wledge)

## Summary

PowerShell scripting provides a lot of power to IT Administrators, but it can also be a powerful tool for an attacker who
gains access to a system running PowerShell.  The scripting can allow an attacker to perform many functions that may
normally require them install other applications/tools to perform those functions. 

## Capabilities and Risk

PowerShell can prove to be useful to attackers for a variety of reasons. There are examples where systems which had access
to the cmd.exe blocked did not have the same access to powershell.exe blocked, allowing essentially the same level of 
access as with the cmd.exe.  

Additionally, the vast scripting capabilities mean that many tools and exploits can potentially be run from a system on 
which a standard user account may not have privilege to install tools.  These tools could be used to perform functions 
to elevate privileges on the local system, perform network reconaissance, perform attacks against other remote systems, 
etc.

## Detection

Execution of powershell.exe on a Windows system is a sign of its availabilty. To check the execution policy, you can run:
```
Get-ExecutionPolicy
```

## Remediation

The best policy is to disable script execution within PowerShell.  The Set-ExecutionPolicy allows a Restricted option that
will prevent the execution of scripts. While some security guides may recommend setting a policy that only allows signed
scripts, this is a trivial barrier for an attacker to bypass. An attacker can bypass this by loading their own user-level
certificate (and if necessary CA) and sign scripts that way.  These scripts would then still validate as signed.

## References

- Wikipedia link on PowerShell (https://en.wikipedia.org/wiki/Windows_PowerShell)
- Microsoft Technet on Scripting in PowerShell (https://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx)
- Powersploit post exploitation with PowerShell (https://github.com/PowerShellMafia/PowerSploit)

## Exploitation

A write up on how this finding can be exploited with demo code or screen shots
