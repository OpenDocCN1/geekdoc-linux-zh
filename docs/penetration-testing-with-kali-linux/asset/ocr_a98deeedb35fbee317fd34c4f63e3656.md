# OffSec

Penetration Testing with Kali Linux

| Password required | Yes |
| User may change password | Yes |
| Workstations allowed | All |
| Logon script | |
| User profile | |
| Home directory | |
| Last logon | 9/20/2022 1:36:09 |

Logon hours allowed | All
Local Group Memberships | *Administrators
Global Group memberships | *Domain Users
The command completed successfully.
Listing 713 - Running 'net user' against a specific user

According to the output, jeffadmin is a part of the Domain Admin group, which is something we should take note of. If we manage to compromise this account, we will essentially elevate ourselves to domain administrator.

We can also use netex to enumerate groups in the domain with net group.1014

```
C:\Users\stephanie>net group /domain
The request will be processed at a domain controller for domain corp.com.
```

+   Group Accounts for DCI.corp.com

*Cloneable Domain Controllers
*Debug
*Development Department
*DnUpdateProxy
*Domain Admins
*Domain Computers
*Domain Controllers
*Domain Guests
*Domain Users
*Enterprise Admins
*Enterprise Key Admins
*Enterprise Read-only Domain Controllers
*Group Policy Creator Owners
*Key Admins
*Management Department
*Protected Users
*Read-only Domain Controllers
*Sales Department
*Schema Admins
The command completed successfully.
Listing 714 - Running 'net group' to display groups in the domain

1014 (Microsoft, 2012). https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754051(v=10)?redirectfrom=MSN

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

693