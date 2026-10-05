# # OffSec

Penetration Testing with Kali Linux

We produced a cleaned-up list of users in the domain.

When enumerating AD, there are many interesting attributes to search for. For example, if a user is dormant (they have not changed their password or logged in recently) we will cause less interference and draw less attention if we take over account during the engagement. In addition, if a user hasn't changed their password since a recent password policy change, their password may be weaker than the current policy. This might make it more vulnerable to password attacks.

This is something we can easily investigate. Let's run Get-NetUser again, this time piping the output into select and extracting these attributes.

```
PS C:\Tools> Get-NetUser | select cn,pwdlist,lastlogon
```

| cn | pwdlist | lastlogon |
|---|---|---|
| Administrator | 8/16/2022 5:27:22 PM | 9/14/2022 2:37:15 AM |
| Guest | 12/31/1600 4:00:00 PM | 12/31/1600 4:00:00 PM |
| krbtgt | 9/2/2022 4:27:20 PM | 12/31/1600 4:00:00 PM |
| dave | 9/14/2022 9:54:57 AM | 9/14/2022 2:57:28 AM |
| stephanie | 9/2/2022 4:23:38 PM | 9/14/2022 2:54:55 AM |
| jeff | 9/2/2022 4:27:20 PM | 9/14/2022 2:26:37 AM |
| jeffadmin | 9/14/2022 4:26:48 PM | 9/14/2022 2:35:55 AM |
| iis_service | 9/7/2022 12:41:54 PM | 9/13/2022 8:37:09 AM |
| pete | 9/6/2022 4:53:01 PM | 9/13/2022 8:36:55 AM |

> Listing 750 - Querying users displaying pwdlist and lastlogon

As indicated in Listing 750, we have a nice list shows us when the users last changed their password, as well as when last logged on to the domain.

Similarly, we use **Get-NetGroup** to enumerate groups:

```
PS C:\Tools> Get-NetGroup | select cn
cn
...
Key. Admins
Enterprise Key Admins
DnsAdmins
DnsUpdateProxy
sales Department
Management Department
Development Department
Debug
```

> Listing 751 - Querying groups in the domain using PowerView

Enumerating specific groups with PowerView is easy. Although not the process of unraveling nested groups in this case, let's investigate the **Sales Department** Get-NetGroup and pipe the output into select member:

```
PS C:\Tools> Get-NetGroup "Sales Department" | select member
member
```

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.