# OffSec

Penetration Testing with Kali Linux

The output of Listing.377 shows that we have command execution as user dave. Additionally, the output contains the hostname of the system, clientwk220. This hostname implies that our bind shell runs on a client system rather than on a server.

The hostname often can be used to infer the purpose and type of a machine. For example, if it is WEB01 for a web server or MSSQL0 for a SQL^743 server.

Next, we want to check groups which dave is. Display all groups our current user is a member of, we use whoami /groups.

```
C:\Users\dave> whoami /groups
whoami /groups

GROUP INFORMATION

Group Name              Type                        SID
Attributes
=====================================================
Everyone                 Well-known group S-1-1-0
Mandatory group, Enabled by default, Enabled group\CLIENTWRK220#helpdesk  Alias                       S-1-5-21-2309961351-4093626482-
222349231-1088 Mandatory Users, Enabled by default, Enabled group
BUILTIN\Remote Desktop Users Alias                       S-1-5-32-55
Mandatory group, Enabled by default, Enabled group
BUILTIN\Users           Alias                       S-1-5-32-545
Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\BATCH     Well-known group S-1-5-3
Mandatory group, Enabled by default, Enabled group
CONSOLE LOGON            Well-known group S-1-2-1
Mandatory group, Enabled by default, Enabled group
NT AUTHORITY\Authenticated Users Well-known group S-1-5-11
Mandatory group, Enabled by default, Enabled group
...
```

Listing 378 - Groups membership of the user dave

The output shows that dave is a member of the helpdesk group. Helpdesk staff often have additional permissions and access to standard users.

Additionally, the user is a member of BUILTIN\Remote Desktop Users. Membership of this group offers the possibility to connect to the system via RDP.

The other groups dave is a member of for non-privileged users such as Everyone and BUILTIN\Users.

The next piece of information we are interested in other users and groups on the system. We can use the net user^744 command or the Get-LocalUser^745 Cmdlet to obtain a list of all local users. Let's use the latter by running PowerShell and Get-LocalUser.

> ^743 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Microsoft,_SQL_Server

> ^744 (Microsoft Documentation, 2016), https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/server-2012-r2-and-2012/cc771865s-vs.11)

PWK - © 2023 OffSec Services. All rights reserved.

477