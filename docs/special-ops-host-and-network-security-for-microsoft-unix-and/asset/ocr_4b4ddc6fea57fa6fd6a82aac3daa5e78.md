# Chapter 15 • Wireless LANs: Discovery and Defense

way to remotely query the system to obtain its NetBIOS name table and MAC address. Entering nbtstat -A IP Address from the command line will return this information. You can then check the MAC to see if it matches a known wireless manufacturer. Since NBTStat requires no privileges to the target host other than UDP port 137 being accessible, it will work across the widest range of hosts. To better automate this process, you can use the NBTScan tool (located at http://www.inetcat.org/software/nbtscan.html). NBTScan will perform the same tasks as NBTstat, but lets you input network ranges of a single address or host-name. Figure 15.14 shows NBTScan results from an example. The host at 172.16.0.25 has a MAC prefix of 00-40-96 (a prefix known to be used by Cisco Aeron products), which immediately identifies it as a wireless device. 172.16.0.52 could be a wireless device if your network is not supposed to contain any NetGear devices.

# Figure 15.14 NBTScan results 172.16.0.1-254

```
E:\nbtscan 172.16.0.1-254
Doing NBT name scan for addresses from 172.16.0.1-254
IP address      Name            Server          User        MAC address
172.16.0.25     OHGR            <server> OHGR        00-40-96-b1-ff-8c
172.16.0.52     NIVEK           <server> NIVEK        00-30-ab-85-53-95
172.16.0.37     CHEMLAB         <server> CHEMLAB      00-b0-d0-62-0f-47
```

# Finding Wireless Clients with the GetMac

GetMac is a Windows 2000 resource kit utility (by default with XP) that uses the Win32 NetTransportEnum API to list out the current network interfaces on a target system. GetMac requires at least an established null session to execute in terms of privileges, so if null session is disabled on the target host it will not work. GetMac is useful for seeing network interfaces that are not directly accessible from the network. For example, a user is connected to the network via Ethernet, but also has a wireless NIC installed and active. With GetMac, you would be able to see this second interface. Example usage of GetMac (Windows XP version) follows:

```
C:\>getmac /s 10.0.2.127
```

Physical Address      Transport Name