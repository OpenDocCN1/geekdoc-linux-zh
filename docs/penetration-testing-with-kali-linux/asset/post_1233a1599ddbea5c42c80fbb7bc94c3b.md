
# OffSec

CN=stephanie,CN,DC=corp,DC=com
PS C:\Users\stephanie\Desktop>

Penetration Testing with Kali Linux

Listing 743 - Printing the member attribute on the Sales Department group object

The Development Department is indeed a member of the Sales Department group as indicated in Listing 743. This is something we missed earlier with net.exe.

This is a group within a group, known as a nested group. Nested groups are relatively common in AD and scales well, allowing flexibility and dynamic membership customization of even the largest AD deployments.

The net.exe tool used only lists user objects, not group objects.

In addition, net.exe does not display specific attributes. This emphasizes the benefit of custom tools.

Now that the Development Department is a member of the Sales Department, let's enumerate it:

```powershell
PS C:\Users\stephanie> $group = LDAPSearch -LDAPQuery "(&(objectCategory=$group) (cn=Development Department+))"
```

```powershell
PS C:\Users\stephanie> $group.properties.member
CN=Management Department,DC=corp,DC=com
CN=pete,CN=Users,DC=corp,DC=com
CN=dave,CN=Users,DC=corp,DC=com
```

Listing 744 - Printing the member attribute on the Development Department group object

Based on the above, we have another case of a nested group since Management Department is a member of Development Department. Let's check this group as well:

```powershell
PS C:\Users\stephanie> $group = LDAPSearch -LDAPQuery "(&(objectCategory=$group) (cn=Management Department+))"
```

```powershell
PS C:\Users\stephanie> $group.properties.member
CN=jen,CN=Users,DC=corp,DC=com
```

Listing 745 - Printing the member attribute on the Management Department group object

Finally, after searching through multiple groups, it appears we found the end. According to the output in Listing 745, we saw jen as a member of the Management Department group earlier in Listing 741, we obtained additional information about the group memberships in this by enumerating the groups one-one-one.

An additional thing to note is that while it appears that jen is only a part of the Sales Department and Development groups, which inherit each other, if misconfigured, users may end up with more privileges than they intended to have. This might allow attackers to take advantage of the misconfiguration to further expand their reach inside compromised domain.

This concludes the journey with our PowerShell script that invokes .NET classes to run queries against AD via LDAP. As we verified, this approach is much more powerful than running tools such as net.exe and provides a wealth of enumeration options.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

Penetration Testing with Kali Linux

While this script can surely be developed further adding additional options and functions, this may require more research on PowerShell scripting, which is outside the scope of this Module.

With a basic understanding of LDAP and how we can use it to communicate with AD using PowerShell, we'll shift our focus in the next section to a pre-developed script that will speed up our process.

## 21.2.4 Enumeration with PowerShell

So far we have only scratched the surface of Active Directory enumeration by mostly focusing on users and groups. The tools we use have given us a good start and an understanding of how we can communicate with AD and obtain information, other researchers have created more elaborate tools for the purpose.

One popular option is to use PowerShell script, which includes many functions to improve the effectiveness of our enumeration.

As a way of introducing PowerShell, let's walk through parts of our enumeration steps from the previous section. PowerShell is already installed in the C:\Tools folder on CLIENT75. To use it, we'll first import it to memory:

```powershell
PS C:\Tools> Import-Module \PowerShell.ps1
```

Listing 746 - Importing PowerShell to memory

With PowerShell, we can start exploring various commands that are available. For a list of available commands in PowerShell, please refer to the linked reference.

Let's start running Get-NetDomain, which will give us basic information about the domain (which we used GetCurrentDomain previously):

```powershell
PS C:\Tools> Get-NetDomain
```

```
Forest : corp.com
DomainControllers : (DC1.corp.com)
Children : {}
DomainMode : Unknown
DomainModeLevel : 7
Parent : 
PdcRoleOwner : DC1.corp.com
RidRoleOwner : DC1.corp.com
InfrastructureRoleOwner : DC1.corp.com
Name : corp.com
```

Listing 747 - Obtaining domain information

Like the script we created earlier, PowerShell is also using .NET classes to obtain the required LDAP data and it communicates with AD.

Now let's get a list of all users in the domain with Get-NetUser.

```powershell
PS C:\Tools> Get-NetUser
```

logoncount : 113
criticalsystemobject : Built-in account for administering the computer/domain
distinguishedname : CN=Administrator,CN=Users,DC=corp,DC=com
objectclass : (top, person, organizationalPerson, user)
lastlogontstamp : 9/13/2022 1:03:47 AM
name : Administrator
objectid : S-1-5-21-198730270-658905905-1788184369-500
samaccountname : Administrator
admincount : 1
codeppage : 0
samaccounttype : NEVER
cn : Administrator
whenchanged : 9/13/2022 08:03:47 AM
instancetype : 4
usercreated : 8196
objectguid : e5591000-088d-44c4-89c8-b0657a14d85
lastlogoff : 12/31/1606 4:01:00 PM
objectcategory : CN=Person,CN=Schema,CN=com
distinguishedname : CN=Administrator,CN=Users,DC=corp,DC...
objectguid : e5591000-088d-44c4-89c8-b0657a14d85
lastlogoff : 12/31/1606 4:01:00 PM
objectcategory : CN=Person,CN=Schema,CN=com

Listing 748 - Querying users

```powershell
PS C:\Tools> Get-NetUser | select cn
```

```powershell
PS C:\Tools> Get-NetUser | select cn
cn
Administrator
jen
dave
pete
stephanie
iis_service
```

Listing 749 - Querying groups using PowerShell

# Off

Penetration Testing with Kali Linux

While this script can surely be developed further adding additional options and functions, this may require more research on PowerShell scripting, which is outside the scope of this Module.

With a basic understanding of LDAP and how we can use it to communicate with AD using PowerShell, we'll shift our focus in the next section to a pre-developed script that will speed up our process.
