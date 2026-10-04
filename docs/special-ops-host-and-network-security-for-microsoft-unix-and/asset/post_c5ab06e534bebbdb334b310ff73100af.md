
## Chapter 15 • Wireless LANs: Discovery and Defense

way to remotely query the system to obtain its NetBIOS name table and MAC address. Entering `nbtstat -A IP Address` from the command line will return this information. You can then check the MAC to see if it matches a known wireless manufacturer. Since NBTStat requires no privileges to the target host other than UDP port 137 being accessible, it will work across the widest range of hosts. To better automate this process, you can use the NBTScan tool (located at http://www.inetcat.org/software/nbtscan.html). NBTScan will perform the same tasks as NBTstat, but lets you input network ranges of a single address or host-name. Figure 15.14 shows NBTScan results from an example. The host at 172.16.0.25 has a MAC prefix of 00-40-96 (a prefix known to be used by Cisco Aironet products), which immediately identifies it as a wireless device. 172.16.0.52 could be a wireless device if your network is not supposed to contain any NetGear devices.

### Figure 15.14 NBTScan results 172.16.0.1-254

| IP address | Name | Server | User | MAC address |
| :--- | :--- | :--- | :--- | :--- |
| 172.16.0.25 | OHGR | <server> | OHGR | 00-40-96-b1-ff-8c |
| 172.16.0.52 | NIVEK | <server> | NIVEK | 00-30-ab-85-53-95 |
| 172.16.0.37 | CHEMLAB | <server> | CHEMLAB | 00-b0-d0-62-0f-47 |

### Finding Wireless Clients with the GetMac

GetMac is a Windows 2000 resource kit utility (by default with XP) that uses the Win32 NetTransportEnum API to list out the current network interfaces on a target system. GetMac requires at least an established null session to execute in terms of privileges, so if null session is disabled on the target host it will not work. GetMac is useful for seeing network interfaces that are not directly accessible from the network. For example, a user is connected to the network via Ethernet, but also has a wireless NIC installed and active. With GetMac, you would be able to see this second interface. Example usage of GetMac (Windows XP version) follows:

```cmd
C:\>getmac /s 10.0.2.127
```

| Physical Address | Transport Name |
| :--- | :--- |
| 00-08-74-4B-BA-FE | \Device\(DC590387-DAFB-4469-8080-41DA5A835A08) |
| 00-09-E8-B4-CB-E8 | Media disconnected |

The first adapter in the list was reachable from our source network, and the second is a wireless card that has not associated with an access point (indicated by the “Media disconnected” message).

### Finding Wireless Clients with the Windows Registry

The Windows Registry stores information about the adapters registered with the system. This useful info is descriptive enough to determine the maker of the device. In Windows 2000, this information is stored in a few places. One is HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards, which will list entries from the following:

```registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards\10]
"ServiceName"="B25B1B3-C4AD-4F55-BD8A-B2E4D56C4398"
"Description"="D-Link DWL-650 11Mbps WLAN Card"
```

```registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards\11]
"ServiceName"="C2A919F1-D7C7-45E8-81D9-DC627B3793EE"
"Description"="Cisco Systems 350 PCMCIA Wireless LAN Adapter"
```

```registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkCards\9]
"ServiceName"="B39BFE7E-D7C1-4774-9E96-08E597A65514"
"Description"="ORINOCO PC Card (5 volt) *"
```

From this, it’s easy to identify the wireless NICs that have been installed on this system. Most wireless client cards come with management software to handle basic configuration. Figure 15.15 shows the HKLM\Software entry for the Cisco Aironet Client.

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients via SNMP

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clientss: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the Windows Registry

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### LANs: Discovery and Defense • Chapter 15

### Finding Wireless Clients with the LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clientss: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Wireless LANs: Discovery and Defense

If you have SNMP access to a target system, you should be able to identify its network adapters enough to determine if it is a wireless NIC or not. SNMP access to host is helpful for non-Windows systems, because SNMP is

![](img/729efc56f204a2ebff)

### Finding Wireless Clients with the LANs: Discovery and Defense

