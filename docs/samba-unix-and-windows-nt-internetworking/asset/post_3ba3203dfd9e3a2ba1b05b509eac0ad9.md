
![](img/7684008b1d7775727df27d44aed5b3f0_190_0.png)

Figure 14.4: SMB2WWW network neighborhood

## Smbconfool

Smbconfool is another smb.conf editing tool. Unlike SWAT, smbconfool will preserve comments in smb.conf. However, you cannot enter comments. That capability will come in a future release. You can do most general configuration tasks like creating, updating, and removing share sections.

Smbconfool is Java-based, so will require Java support in the browser. You can obtain a copy of smbconfool from: http://www.eatonweb.com/samba/

## Windows Tools

### bbSAT

The HP 3000 Channel Partner B+B Unternehmensberatung built a Windows-based GUI tool called bbSAT (Figure 14.5) for maintaining Samba configuration. This was done as part of the Samba port MPE/iX. bbSAT is freely available and will work with other Samba platforms. Like smbconfool, bbSAT will preserve smb.conf comments. There is also an enhanced version of bbSAT called "bbSAT (GE) Gold Edition" that provides additional functionality. For more information visit the bbSAT Web site: http://jazz.external.hp.com/src/samba/bbsat_index.html.

![](img/7684008b1d7775727df27d44aed5b3f0_191_0.png)

Figure 14.5: bbSAT

### smbedit

smbedit is another free Win32 application for editing smb.conf from a Windows client (Figure 14.6). Along with general Samba configuration editing, you can also invoke Samba services like testparm and smbstatus. For more information see the smbedit Web page: http://us3.samba.org/samba/smbedit/readme.htm.

![](img/7684008b1d7775727df27d44aed5b3f0_192_0.png)

Figure 14.6: smbedit

## Other Tools

### smb-mode.el

For you Emacs aficionados, there is an Emacs major mode available for editing smb.conf called smb-mode.el. With smb-mode.el you can edit individual smb.conf sections, look up parameter information from the Samba man pages, perform parameter completion, and run a buffer through the Samba testparm command. To get a copy of smb-mode.el, look at the following Web site: http://users.gtn.net/fraserm/smbmode.html.

### GSMB

Departing a bit from our focus on smb.conf editing tools, we note a Gtk tool for administering Samba smbpasswd encrypted password support called gsmb (Figure 14.7). It was created by Laurent Foucher. gsmb uses the Gtk 1.2.0 library. For more information visit the gsmb Web site: http://savage.iut-blagnac.fr/projets/developpement/gsmb/.

![](img/7684008b1d7775727df27d44aed5b3f0_193_0.png)

Figure 14.7: gsmb

## Summary

- Useful Samba administration command line tools include: `testparm`, `smbclient`, `smbstatus`, and `testprns`.
- Useful Samba GUI administration tools include:
  - **Web Tools:** SWAT, Webmin, SMB2WWW, and smbconfool.
  - **Windows Tools:** bbSAT and smbedit.
  - **Other Tools:** smb-mode.el and gsmb.

## Chapter 15: Troubleshooting

### Overview

> "Politics is the art of looking for trouble, finding it, misdiagnosing it, and then misapplying the wrong remedies."

**Groucho Marx**

Computers are somewhat like politics. Sooner or later trouble always shows up. It usually happens when you're making one small late-night change to a production service. You know the kind. It's always some preventative service patch for a problem you've never seen; one the vendor advises needs to be applied, assuring that it is only a benign software update. You apply the patch and dream of sleeping in late the following morning. Just as you're ready to call it a night, problem symptoms start showing up from multiple subsystems. SNMP monitor alerts are popping up everywhere announcing server failures all across the network. In a nervous adrenalin rush you rapidly try to back out the patch before it's too late. Halfway through, the uninstall task fails, your screen goes blank, and the phone begins to ring off the hook.

Gruesome isn't it? You can't avoid computer and network problems, but you can limit the scope of disaster. The trick is to always have a good selection of diagnostic tools at hand, and to have a sound fallback plan. When installing a new system, try it out first in an isolated test environment. When problems emerge in production systems, address them as a series of validation stages. Begin with the lowest-level subsystems. In turn, examine each higher-level service eliminating possibilities as you proceed. This process will assist in diagnosing events rooted in complex subsystem interrelationships.

### Sleuthing Samba

Samba is an excellent example of a network service comprised of tightly coupled subsystems. It is therefore often helpful to address Samba problems in the stepwise manner described in the previous paragraph. Begin by verifying network connectivity from both the server and client end of a circuit. Next confirm that the smbd and nmbd are running and listening for connection requests. Ensure that the configuration files correctly reflect the role Samba is playing in the workgroup or domain. When all else fails, make sure you know where to go for help.

In the following sections we'll look closely at validating Samba services at the network, daemon and configuration levels. Table 15.1 lists the set of tools we'll use as we analyze each component of the system.

### Table 15.1 Troubleshooting Tools

#### Samba Tools

```
smbclient
nmblookup
testparm
testprns
```

#### UNIX Tools

- `ifconfig`
- `netstat`
- `ping`
- `ps`
- `iostat`

#### Windows Client Tools

- `NET`
- `NBTSTAT`
- `WINIPCFG`

### Network Connectivity

Begin troubleshooting by examining network connectivity between clients and servers.

Can everybody talk to each other over the wire? Is everyone configured to support NetBIOS over TCP/IP? Are the assigned IP addresses and subnets correct? Use the `ifconfig` command on each UNIX client and server (Example 15.1) and the `winipcfg` command on Windows clients and servers (Figure 15.1) to verify network interface configuration. These commands will display network adapter status, assigned IP address and subnet mask, and the broadcast address.

### Example 15.1 ifconfig – UNIX Network Interface

```
# ifconfig en0
en0: flags=0x080863<UP,BROADCAST,NOTRAILERS,RUNNING,SIMPLEX,
    MULTICAST,GROUPRT>
inet 145.142.210.20 netmask 0xffffffff broadcast
    145.142.210.255
```

![](img/7684008b1d7775727df27d44aed5b3f0_196_0.png)

Figure 15.1: winipcfg – Windows network interface

Once you're certain that each systems network interface is operational, check reachability by using the ping command to send an ICMP echo request between problem systems (Example 15.2). Echo round-trip time and dropped-packet rate statistics are displayed, indicating the overall health of the communication path between the participating systems.

### Example 15.2 ping – Verify Communication Path

```
# ping foo.bar.com
PING foo.bar.com (130.111.58.1): 56 data bytes
64 bytes from 130.111.58.1: icmp_seq=0 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=1 ttl=252 time=3 ms
64 bytes from 130.111.58.1: icmp_seq=2 ttl=252 time=8 ms
64 bytes from 130.111.58.1: icmp_seq=3 ttl=252 time=5 ms
--- foo.bar.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 3/5/8 ms
```

In most cases reachability problems will be related to routing configuration or an incorrectly assigned subnet mask. Use the netstat command to display additional interface statistics (Table 15.2) including netmask and routing information (Example 15.3). An interval flag may be used with netstat to collect statistics snapshots over time.

### Table 15.2 Useful netstat Options

| Option | Description |
| -i | Interface state, packet rates and errors. |
| -a | Display socket connection status. |
| -R | Display routing table information. |
| -m | Display memory allocation and usage (mbufs). |

### Example 15.3 netstat – Display Routing

```
$ netstat -rn
Routing tables
Destination Gateway.Flags Refs Use If PMTU Exp Groups
Netmasks:
(0) 0 ff00
(0) 0 ffff ff00

Route Tree for Protocol Family 2:
default 145.142.210.100 UG 22 23884982 en0 - -
127 127.0.0.1 U 3 637989 lo0 - -
140.142.78 145.142.210.20 U 4 20262917 en0 - -
```

### Running Daemons

If you are confident that all network communication paths are functioning correctly, then the next step is to certify that the Samba smbd and nmbd daemons are running and listening for connections. Display the process status of smbd and nmbd with the ps command (Example 15.4).

Review inetd configuration (see "Configuration Files" section) to verify that the daemons will be spawned when SMB services are requested. Check the smb.log and nmb.log files in /usr/local/samba/var for diagnostic messages indicating any startup or communication anomalies.

### Example 15.4 'ps' Check Daemon Process Instance

```
# ps -ef | grep smbd
root 448 1 0 07:25 ? 00:00:00 /usr/local/samba/bin/smbd -D

# ps -ef | grep nmbd
root 446 1 0 07:25 ? 00:00:00 /usr/local/samba/bin/nmbd -D
```

Assuming that the smbd and nmbd daemons are up and running, next look to see if they are listening for incoming connection requests. Invoke netstat with the -a option to list the set of port listening services on the server. You can thin the list down to just the NetBIOS services by piping the command into grep (Example 15.5).

### Example 15.5 Samba Listing to NetBIOS Ports

```
$ netstat -a | grep netbios
```
