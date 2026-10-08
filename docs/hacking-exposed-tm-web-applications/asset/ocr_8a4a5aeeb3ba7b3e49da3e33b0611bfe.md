# Hacking Exposed Web Applications

NOTE Chapter 11 will discuss network management platforms that use HTTP as transport (for example, Compaq Insight Manger, or CIM).

# Novell GroupWise Arbitrary File Access

| Popularity: | 8 |
| Simplicity: | 8 |
| Impact: | 5 |
| Risk Rating: | 7 |

This is a good example of an insecure servlet that will retrieve arbitrary files from the server. Because a Java servlet can run on multiple operating systems and Web servers, this vulnerability can affect a wide range of servers from Windows 2000 to Novell Network. The basic premise is an input validation attack. A normal request for the login page uses the URL /servlet/webaccc?User.html=. Instead of using the "simple" template, an attacker can specify a filename anywhere on the system:

```
http://victim.com/servlet/webaccc?User.html=.../\../../novell/WebAccess/webaccc.cfg00
```

A byproduct of the exploit is that the full directory path of the Novell install will be revealed if the vendor's patch has been applied. Also check out the commrg.cfg and ldap.cfg files in the WebAccess directory for sensitive information. "%%00" at the end of the URL is the extra necessary for the exploit to succeed. We'll take a more detailed look at this in Chapter 8 when we discuss input validation.

# GroupWise Countermeasures

Ob the most recent GroupWise patches and make sure the GroupWise server (or other application) files are installed on a disk volume separate from the Windows system root.

# RealServer Administrator Password Can Be Retired

| Popularity: | 8 |
| Simplicity: | 8 |
| Impact: | 8 |
| Risk Rating: | 8 |

Whenever a port scan returns an unknown port, the first thing to check is if that port responds to HTTP requests. The RealNetworks' RealServer platform for streaming media has an insecure default configuration that can reveal the administrator's password. Requests to the /admin/ directory on the administration port require the user to