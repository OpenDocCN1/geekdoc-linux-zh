# Attacking and Defending Oracle • Chapter 13

by using a default user login and password such as SYS, SYSTEM, or CTSYS. At the very least, they could deny service by altering passwords and yielding the accounts unusable. Requesting http://<oracleserver>/pls/<hostname>/admin_/ will show whether the site is vulnerable. If the administration page is returned, then of course it is. To secure this, several steps are required. Edit the wdbsvr.app file located in the $ORACLE_HOME\Apache\modplsql cfg directory; modify the "adminPath" entry to something difficult to guess or brute force; add a password.

# PL/SQL Authorization Denial of Service

A denial of service exists with the PL/SQL module. When a request is received by the module with a malformed Authorization HTTP client header with no authorization type set, such as Basic, Apache will access violate or core dump. The resolution to this is install the patch provided by Oracle. This is available from the Metalink Web site. The patch number for this vulnerability is 2209455.

# The OWA_UTIL PL/SQL Package

The OWA_UTIL package exists to provide Web-related services, along with packages such as hypertext procedures (htp), for creating HTML content (htf), which functions that produce HTML tags. These and others are all installed as part of the PL/SQL Toolkit. OWA_UTIL exposes many procedures that can be called directly from the Web—this section looks at signature, showsource, cellprint, listprint, and show_query_columns.

owa_util.signature

Signature does nothing but returns a message. It can be used to verify that access can be gained to owa_util. It doesn't require any parameters (then it can take some):

```
http://oracleserver/pls/dna/owa_util.signature
```

If a message is returned along the lines of, "This page was produced by the PL/SQL Cartridge on December 21, 2001 04:50A AM," then access can be gained to owa_util. If it doesn't return this and the Web server returns a 500 or 403 response, it may be that the package is protected. Often not than, depending on how it has been protected, this protection can be bypassed by inserting a space, tab or new line character before:

![](bbox=[0.712, 0.943, 0.929, 0.966])