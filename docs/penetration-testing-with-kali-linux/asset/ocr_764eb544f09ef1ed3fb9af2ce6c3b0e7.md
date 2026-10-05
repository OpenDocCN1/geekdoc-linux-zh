# OffSec
Penetration Testing with Kali Linux

Now that we have abused the GenericAll permission, let's use it to clean up after ourselves by
removing our user from the group:

```
PS C:\> net group "Management Department" stephanie /del /domain
The request will be processed at a domain controller for domain corp.com.
```

The command completed successfully.
Listing 775 - Using "net.exe" to remove ourselves from domain group

Once we can use PowerView to verify that jen is the sole member of the group:

```
PS C:\> Get-NetGroup "Management Department" | select member

member
-----
CN=jen,CN=Users,DC=corp,DC=com
Listing 776 - Running "Get-NetGroup" to verify that our user is removed from domain group
```

Great, the cleanup was successful.

From a system administrator perspective, managing permissions in Active Directory can be a
tough task, especially in complex environments. We permissions such as the one we saw
are often the go-to vectors for attackers since it can escalate our privileges within
the domain.

In this particular case, we enumerated the Management Group object specifically and leveraged
stephanie'sGenericAll to add our user to the group. Although it didn't grant us additional
d privileges, this exercise demonstrated the process of discovering and abusing the
ray of patterns that we can leverage in real-world environments.

# 21.3.5 Enumerating Domain Shares

To wrap up our manual enumeration, we'll shift our focus to domain shares. Domain
shares often contain critical information about the environment, which we can use to our
advantage.

We'll use PowerView's Find-DomainShare function to find the shares in the domain. We could
also add the -CheckShareAccess flag to display shares only available to us. However, we'll skip
this flag for a full list, including all shares we may target. Note that it may take a
moment for PowerView to find the shares and list them.

```
PS C:\> Find-DomainShare

Name      Type                ComputerName
----- --------------- -----------------
ADMIN$    217483648 Remote Admin    DC1.corp.com
C$       217483648 Default share   DC1.corp.com
IPC$     217483648 Remote IPC      DC1.corp.com
NETLOGON  0 Logon server share   DC1.corp.com
SYSVOL   0 Logon server share   DC1.corp.com
ADMIN$    217483648 Remote Admin    web04.corp.com
backup    0                               web04.corp.com
C$       217483648 Default share   web04.corp.com
IPC$     217483648 Remote IPC      web04.corp.com
ADMIN$    217483648 Remote Admin    FILES04.corp.com
```