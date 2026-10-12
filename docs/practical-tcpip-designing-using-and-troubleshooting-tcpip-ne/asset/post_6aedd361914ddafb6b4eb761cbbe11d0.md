
Name resolution takes account of that as follows:

- NetBIOS programs will use the TCP/IP resolution methods (hosts file and DNS) if:
  - a. the name obviously can’t be a NetBIOS name, e.g. if it has more than 16 characters. Or if
  - b. NetBIOS fails to resolve the name using the NetBIOS methods (cache, broadcast, WINS, LMHOSTS)
- Microsoft’s own TCP/IP programs use the NetBIOS methods if a name can’t be resolved using hosts or DNS. (C.f. Module 18.3, NetBIOS programs, “real” TCP/IP programs, and hybrid programs.)

The resolution order for different configurations and name types is shown in Figure A22.2, e.g. if you **telnet bob**, because this is a TCP/IP program “**bob**” could be a DNS name, so **hosts** is checked before anything else. However, if you **net view bob**, “**bob**” is now treated as a NetBIOS name, and **hosts** is tried only *after* the NetBIOS resolution methods have failed, and then only if **Enable DNS for Windows Resolution** = **YES**.

![](img/a2132b646d336d5f9a21102d6320e537_848_0.png)

| | H-node | P-node | M-node | B-node |
| :--- | :---: | :---: | :---: | :---: |
| DNS names only | **DNS names only** | | | |
| | hosts file | | | |
| | DNS$^1$ | | | |
| both NetBIOS and DNS names | **both NetBIOS and DNS names** | | | |
| | NetBIOS name cache$^2$ | | | |
| | WINS | WINS | broadcast | broadcast |
| | broadcast | | WINS | |
| | LMHOSTS file$^3$ | | | |
| NetBIOS names only | **NetBIOS names only** | | | |
| | hosts file$^4$ | | | |
| | DNS$^5$ | | | |

Notes:

1. only if name being resolved is not a simple name
2. note that pre-loaded LHOSTS entries (**#PRE**) are resolved from the cache
3. only if **Enable LMHOSTS lookup** = **YES**
4. only if **Enable DNS for Windows Resolution** = **YES**
5. only if **Enable DNS for Windows Resolution** = **YES** and name is not a simple name

From Figure A22.2 you can see that in the resolution process taken as a whole, both types of names can use all the methods; what’s different is the order in which the different methods are attempted. Note also that for DNS names, the TCP/IP methods are always tried, but for NetBIOS names, the TCP/IP methods are only used if Enable DNS for Windows Resolution is set to YES.

## Example 1

```
ping name
```

ping is a TCP/IP program and expects DNS names, and therefore will initially try to resolve name using hosts or DNS. If these fail, ping will fall back and try to resolve name using the NetBIOS resolution methods.

## Example 2

```
net use x: \\name\datafiles
```

net use is very definitely a NetBIOS program, and assumes name is a NetBIOS name if at all possible:

- if name is 15 characters long or less, it’s taken as a NetBIOS name, even if it contains dots (e.g. b2.example.com)
- if name is 16 characters long, it’s still taken as a NetBIOS name, but NetBIOS resolution will almost inevitably fail because the last character of the name will be interpreted incorrectly as a NetBIOS type suffix.
- In both these cases (names less than or equal to 16 characters long), if the NetBIOS resolution fails, the system will then go on and try the TCP/IP resolution methods, but only if they are enabled; if they are not enabled, the resolution fails completely
- only if name is 17 characters long or more is it definitely not a NetBIOS name – it must be a DNS name instead. Accordingly, the system tries the TCP/IP resolution methods first, and if these fail it falls back to the NetBIOS methods. Note that in this case the resolution order is different to the above; here, the TCP/IP methods are tried first.

These examples illustrate that it is difficult to predict from first principles how a particular program is going to treat names for resolution. However, by observing what happens on the wire you can at least make sense of what actually occurs.

## Notes and further reading

- MS-KB-Q161431 Connecting to NetBIOS Resources Using DNS Names or IP Addresses explains the special computer name *\*SMBSERVER used when a client connects to a server using an IP number rather than a FQDN DNS-name or a NetBIOS name
- MS-KB-Q172218 Microsoft TCP/IP Host Name Resolution Order describes the difference between “hostname resolution” (i.e. DNS name resolution) and NetBIOS name resolution
- MS-KB-137565 System Error 53 When Connecting to a Fully Qualified Domain Name (FQDN)
- MS-KB-Q139270 *How to Change Name Resolution Order on Windows 95 and Windows NT*
- MS-KB-Q142309 *NetBIOS Name Resolution Using DNS and the HOSTS File*
- MS-KB-Q230744 *Windows NT 4.0 SP4 DNR Client Does Not Send Unqualified DNS Queries (“DNR” stands for “domain name resolver”)*
- MS-KB-Q198550 *SP4 Changes DNS Name Resolution*

## Appendix 23 Windows name resolution worksheet

- a. collect the details of the PC that is resolving the name, and enter them in Worksheet 1
- b. Figure A23.1 shows the expected name resolution order for the different node types and configurations. Copy the order for your node type into Worksheet 2
- c. from your etherreal or Network Monitor trace, enter the observed order in Worksheet 2.

### *Worksheet 1*

| Item | Value |
| :--- | :--- |
| Control Panel > Network > Identification | |
| 1. Computer Name | |
| Control Panel > Network > Protocols > TCP/IP > Properties | |
| 2. DNS > hostname | |
| 3. DNS > Domain | |
| 4. DNS > DNS Service Search Order | (list of DNS servers) |
| 5. DNS > Domain Suffix Search Order | |
| 6. WINS Address > Enable LMHOSTS Lookup | yes / no |
| Run ipconfig/all at the command prompt | |
| 7. hostname | |
| 8. Node Type | |
| 9. IP Address | |
| 10. Netmask (Sub-net Mask) | |
| 11. NetBIOS Scope ID | |
| 12. NetBIOS Resolution Uses DNS | |
| 13. Primary WINS Server | |
| 14. Secondary WINS Server | |
| 15. NetBIOS Resolution uses DNS | yes / no |

![](img/a2132b646d336d5f9a21102d6320e537_852_0.png)

**Notes:**

1. only if name being resolved is not a simple name
2. note that pre-loaded LHOSTS entries (#PRE) are resolved from the cache
3. only if Enable LMHOSTS lookup = YES
4. only if Enable DNS for Windows Resolution = YES
5. only if Enable DNS for Windows Resolution = YES and name is not a simple name

*Worksheet 2 – Name resolution order for this PC*

*Name to be resolved:*

| | Expected order (*copied from Figure A23.1*) | Observed order |
| :--- | :--- | :--- |
| 1. | | |
| 2. | | |
| 3. | | |
| 4. | | |
| 5. | | |
| 6. | | |
| 7. | | |
| 8. | | |

## Appendix 24 The BROWSTAT command

browstat.exe is included in the NT 4.0 Server Resource Kit. Browstat’s documentation in the Resource Kit lists only a few of the available commands. The following is a complete list for version "created 01 March 1996", 42,256 bytes.

Many of the commands take a *transport* argument. This is needed because if you’re running more than one networking system (e.g. NetBIOS over TCP/IP as well as NetBEUI), you can have different browse lists for each. The easiest way to find the value for transport is to run **browstat status**, which shows the default *transport*. In most commands you must explicitly specify *transport*, even if there is only one.

Instead of the full command name, you can use the abbreviation shown on the right after each command.

For most commands, if you give an invalid transport or an invalid domain name, no error message is printed but the command fails. For some domain-related operations you must be logged in as a user of that domain or the command fails.

- **ADDALTCOMP** *transport* *nbname*  
  *AAC*  
  Register *nbname* as an alternate NetBIOS computer name (<00>) for this machine, in addition to its existing name. Uses WINS or NetBIOS broadcasts as usual, depending on this PC’s configuration

- **GETNETBIOS** *transport*  
  *GN*  
  Get NetBIOS names for a transport

- **GETDOMAIN** *IPaddr*  
  *GWD*  
  Retrieve the domain list from the WINS server on the specified IP address

- **GETWINS** *transport*  
  *GW*  
  Retrieve the primary and backup WINS server

- **OTHERDOMAIN** \*pdc-addr*  
  *OTH*  
  Retrieve list of other domains that the PDC *pdc-addr* listens to

- **POPDOMAIN** *transport* *domain* *number*\[Domains\] \[*AnnouncementFrequency*\]  
  *PD*  
  Issue browser **announce** requests for the specified number of randomly generated domain names

- **POPSERVER** *transport* *domain* *numberOfMachines* \[*AnnouncementFrequency*\]  
  *PS*  
  Populate a workgroup with random PC names, by issuing browser **Announce** requests. The *AnnouncementFrequency* is in milliseconds but appears to be ignored. You will then see these names if you use **net view /domain:** domain or Windows Explorer

- **SD** ...
  Set debug info in the browser. Options are:
