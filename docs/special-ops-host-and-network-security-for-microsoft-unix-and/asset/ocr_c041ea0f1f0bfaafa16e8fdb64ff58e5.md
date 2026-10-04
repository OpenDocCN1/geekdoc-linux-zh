The banner strings from the HTTP header for 9iAS Release 2 is as follows:
Oracle9iAS/9.0.2 Oracle HTTP Server

This is actually not particularly helpful for determining what patches
have not been installed, which is good since you really don't want an attacker
nto be able to look up that information. The banner string from a 9iAS Release 1
was more typical as follows:

Oracle HTTP Server Powered By Apache/1.3.19

This did give an attacker some information, although it was somewhat
limited. The following is the banner string from an older version of Oracle
Application Server:

Apache/1.3.12 (Unix) mod_plsq/3.0.9.8b ApacheJServ/1.1 mod_ssl/2.6.4
OpenSSL

Notice that this banner string gave you some very detailed information that
could have helped an attack. It seems that Oracle has become a little
smarter in later versions in this regard.

# Vulnerabilities in Oracle 9iAS 2

Several of the vulnerabilities I address in this section were not patched at the time
of writing. Once again, Oracle Corporation was alerted to these security holes,
 they are working on a patch which is expected in early 2003. Once the
patch is available, more information about the vulnerability and the patch will
appear on http://otn.oracle.com/deploy/security/alerts.html.

# Buffer Overflow Vulnerability in iSQL*Plus

iSQL*Plus is a Web-based version of SQL*Plus. This URL will open a login
page for the iSQL*Plus application: http://oraclewebserver:7777/isqlplus. By
submitting an overly long username, a saved return address on the stack is over-
written, and an attacker can gain control over the Apache process' execution.
This is a classic buffer overflow vulnerability.

Oracle has provided a patch for a vulnerability. To download the patch
from Metalink, search for patches on the bug number 2581911. An advi-
sory for this vulnerability is available from Oracle at http://otn.oracle.com/
deploy/security/pdf/2002alert46rev1.pdf.