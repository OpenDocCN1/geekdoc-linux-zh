# Chapter 3: Hacking Web Servers

[carriage return]
NT AUTHORITY\SYSTEM

We used the woami utility from the Windows 2000 Resource Kit to show this is running in the context of the all-powerful LocalSystem account from the remote machine.
Because the initial attack occurs via the Web application channel (port 80, typically) and because the shell is spawned outbound from the Web server on a port defined by the attacker, this attack often bypasses inadequate or firewall filtering.
A native Win32 version of jill called jill-win32 was released soon after the UNIX/Linux version. A hacker named CyrusTheGreat released his own version of this exploit, based on the shellcode of jill, all these tools work exactly the same way as previously demonstrated, including the need to be careful with closing the shelled.

![](bbox=[0.093, 0.345, 0.138, 0.403])

# ISAPI DLL Source Disclosure Vulnerabilities

| Popularity | 9 |
| Simplicity | 9 |
| Impact | 4 |
| Risk Rating | 8 |

Not all ISAPI DLL security flaws are as high as the printer buffer overflow. In this section, we will discuss an example of source disclosure vulnerability related to an ISAPI DLL bug. Source disclosure encompasses a large class of issues that allow remote clients to view information that would normally not be authorized to see.
The.+html is a classic example of source disclosure that works against IIS 4 and 5. By adding +html to an active file request, IIS 4 and 5 serve up fragments of the source data from the file rather than executing it. This is an example of a misinterpretation by an ISAPI DLL named ISM. The .dll extension maps files to DLL, which serves the file's source by mistake. Here's a sample file called htr.txt that you can pipe through network to exploit this vulnerability—note the +html appended to the request:

```
GET /site1/global.asa+.HTTP/1.0
[CRLF]
[CRLF]
C:\>nc -rv www.victim.com 80 < htr.txt
www.victim.com [10.0.0.10] 80 (open)
HTTP/1.1 200 OK
Server: Microsoft-IIS/5.0
Date: Thu, 25 Jan 2001 00:50:17 GMT
<-- filename = --> ("Profiles_ConnectString") \
  "DSN=profiles;UID=Company_user;Password=secret"
```

Piping through network connected to a vulnerable server produces the following results:

![](bbox=[0.093, 0.903, 0.138, 0.963])