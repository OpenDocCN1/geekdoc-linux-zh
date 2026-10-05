# HP-UX configuration examples

503

# $ lscan

| Hardware Station Crd Hdw Net-Int NM MAC HP-DLPI DLPI |
| Path Address In# State PPA ID Type Support Mjr# |
| 8/02/0 0x01... 0 UP lan0 snapo 1 ETHER Yes 130 |

# $ configlnan

lan0: flags=843-UP,BROCAST,RUNNING,MULTICAST> inet 192.108.21.99
netmask fffff0 broadcast 192.108.21.255

# $ configsnap

ifsnap: no such interface

netstat -i shows network interface names, and netstat -nr displays routing tables:

# $ netstat -i

| Name Mtu Network Address Ipkts Opkits |
| lan0 1500 192.108.21.0 6047 3648 |
| lo0 4136 127.0.0.0 localhost.address.com 231 231 |

# $ netstat -nr

| Dest/Netmask Gateway Flags Refs Use Int Pmtu |
| 127.0.0.1 127.0.0.1 UH 0 231 lo0 4136 |
| 192.108.21.99 192.108.21.99 UH 8 0 lan0 4136 |
| 192.108.21.99 192.108.21.99 U 2 0 lan0 1500 |
| 127.0.0.0 127.0.0.1 U 0 0 lo0 4136 |
| default 192.108.21.254 UG 0 0 lan0 1500 |

The lanadmin command displays a summary of the network traffic that each interface. It can also manipulate and monitor interfaces. It's a menu-based program with useful help to lead you to the information you want. Here is an example that displays the statistics for the lan0 interface:

% lanadmin

LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
Copyright 1994 Hewlett Packard Company.
All rights are reserved.

Test selection mode:

```
lan = LAN Interface Administration
menu = Display this menu
quit = Terminate the Administration
ter = Do not display command menu
verbose = Display command menu
```

Enter command: lan

```
LAN Interface test mode. LAN Interface PPA Number = 0
clear = Clear statistics registers
display = Display LAN Interface status/statistics
 = End LAN Interface Admin., up level 1
menu = Display this menu\ppa = PPA Number of the LAN Interface
```