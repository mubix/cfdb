/*
Title: Directory Traversal / File Include
Description: Web server ACLs permit direct access to files outside the intended directory
*/

- LAST UPDATED DATE: 12/14/2015
- LAST UPDATED BY: Mike S. (hardwaterhacker) 

## Summary

Insufficient web server ACLs and/or input sanitization allow direct file access requests for files outside of the
intended directory or document root directory.

## Capabilities and Risk

- Information disclosure (reading files as web server user)
- Overwrite files (overwrite files as web server user)
- Denial of Service

## Detection

To detect directory traversal vulnerabilities, the application must first be mapped to identify parameters which
reference files on the server, such as /profile.php?user=bob.html or /display.asp?page=../main.html.  Once the target
pages and parameters have been identified, attempt to access files which would likely reside on the target system.
Identifying the operating system, web server software and version, and application version will assist in identifying
likely candidates.

If the server is vulnerable to directory traversal, it will be possible to "escape" from the
intended directory and/or document root by referencing a series of directories above the intended directory using
dot-dot-slash ("../") notation.  Depending on the starting directory, several dot-dot-slashes to reach the target
directory.

Example #1: Linux password file

http://www.example.com/profile.php?user=../../../../../etc/passwd

Example #2: Window.ini

http://www.example.com/display.asp?page=../../../../../Windows/system.ini

### Windows Web Servers

If the target web server is running on Windows, it may be necssary to use back slashes ("\") instead of forward slashes.

### Absolute Path Traversal

In some instances, it may be possible to specify the absolute path of the file.

Example #3: Linux password file via absolute path traversal

http://www.example.com/profile.php?user=/etc/passwd

### Encoding

During testing, it may appear that the web server ACLs and input sanitization are functioning properly.  Testing should
also include requests using character encoding to bypass input sanitization routines in the application.

Encoding Example #1:

http://www.example.com/profile.php?user=..%2f..%2f..%2f..%2f..%2fetc%2fpasswd

Encoding Example #2:

http://www.example.com/profile.php?user=%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd

### Overwriting files

If the web application uses client-supplied input to specify the target location or file name for file uploads, it may
be possible to overwrite existing files, provided the web server user has write permissions to the target file and
directory.  In some instances, this may result in a denial of service condition.  Testing for directory traversal file
overwrite vulnerabilities uses the same methods outlined above.

## Remediation

The developer should define the intended document root directory or directories that are valid for the file access
request.  All file access requests should be compared against this list of valid directories.  Additionally, whenever
client-supplied input (including cookies and headers) is used as part of a file access request, input sanitization
should be employed using a whitelist filter.

## References

https://www.owasp.org/index.php/Path_Traversal
https://www.owasp.org/index.php/Testing_Directory_traversal/file_include_(OTG-AUTHZ-001)
https://cwe.mitre.org/data/definitions/22.html
https://cwe.mitre.org/data/definitions/23.html
https://cwe.mitre.org/data/definitions/36.html

## Exploitation

See examples above.
```
```
