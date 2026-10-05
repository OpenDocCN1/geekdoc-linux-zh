# OffSec

Penetration Testing with Kali Linux

| SMB | 192.168.50.242 | 445 | MAILSRV1 | IPC$ | READ |
| Remote IPC | | | | |

Listing 897 - Listing SMB shares on MAILSRV1 with CrackMapExec

Listing 897 shows that CrackMapExec only the default shares on which we have actionable permissions.

At this point, we only have the second option left, preparing an email with a malicious attachment and sending it to daniela and marcus.

Let's summarize what we did in this section. We used the information we retrieved from the previous Learning Unit and leveraged it in a password attack against MAILSRV1. This password attack resulted in discovering one set of credentials. Then, we enumerated the SMB shares on MAILSRV1 as john without any actionable results.

# 24.3.2 Phishing for Access

In this section we perform a client-side attack by sending a phishing e-mail. Throughout this course, we've mainly discussed two client-side techniques: Microsoft Office documents containing Macros and Windows Library files in combination with shortcut files.

Because we don't have any information about the internal machines or infrastructure, we'll choose the second technique as Microsoft Office may not be installed on any of the target systems.

For this attack, we have to set up a WebDAV server, a Python 3 web server, a Netcat listener, and prepare the Windows Library and shortcut files.

Let's begin by setting the WebDAV share on our Kali machine on port 80 with wsgdav. In addition, we create the /home/kali///webdav as the WebDAV root directory.

```
kali@kali:~$ mkdir /home/kali/webdav
kali@kali:~$ /home/kali/local/bin/wsgdav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/binding/webdav/
Running without configuration file.
04:24:04.861 INFO - skipping.
04:04:04.861 WARNING - Wsgdav.my.cors.Core(None).is_disabled) returned True:
04:04:04.861 INFO - WsgDav/4.0.2 Python/3.10.7 Linux-5.18.0-kali-amd64-x86_64-with-glibc3
04:04:04.861 INFO - Loop manager: LockManager(LockStorageDirectory)
04:04:04.861 INFO - Property: None
04:04:04.861 INFO - Domain controller: SimpleHomeController
04:04:04.861 INFO - Registered DAV providers by route:
04:04:04.861 INFO - : Filesystem provider for path /home/kali/local/lib/python3/site-packages/wsgdav/dir_htdocs (Read-Only) (anonymous)
04:04:04.861 INFO - : Filesystem provider for path /home/kali/beyond/webdav (Read-Write) (anonymous)
04:04:04.861 INFO - Basic authentication is enabled: It is highly recommended to enable SSL.
04:04:04.861 WARNING - Share '' will allow anonymous write access.
04:04:04.861 WARNING - Share :/dir_browser will allow anonymous read access.
04:04:05.149 INFO - Running WsgDav/4.0.2 Cheroot/8.6.0 Python 3.10
04:04:05.149 INFO - Serving on http://0.0.0.0: 
```

PWK - 2023 OffSec Services Limited. All rights reserved.

827