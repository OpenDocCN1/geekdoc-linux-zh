
## Table C.1 Terms and definitions (continued)

| Term | Definition |  |
| :--- | :--- | :--- |
| SNMPv2 | Enhancements to the SNMPv1 framework; includes new SMI, additional SNMP PDUs, and changes to MIB-II groups and objects | New SNMP version that provides a robust framework for security |
| SMI | Structure of Management Information; a general framework for the definition and construction of a MIB | A model that contains a fixed number of states and actions to transition from one state to another. TCP uses a state machine model for protocol operations |
| Subagent | An SNMP agent that has been configured to function with a master agent. All SNMP requests come from the master agent, and the subagent listens for SNMP requests on a different port | Transmission Control Protocol; OSI transport layer 4 protocol that is responsible for reliable data transport from one machine to another. TCP is used extensively throughout the Internet |
| Topology | A physical or logical layout of a network that consists of networking devices such as switches, routers, and individual workstations and servers | A network management package that provides a large number of management services. Services include software distribution, UNIX account administration, and remote system management |

## Table C.1 Terms and definitions (continued)

| Term | Definition |
| :--- | :--- |
| Trap | A message sent from an SNMP agent to a manager. Trap messages may include ColdStart, WarmStart, LinkDown, and LinkUp. Enterprise traps (<i>EnterpriseSpecific</i>) contain vendor-specific information |
| trapd | A UNIX program that listens for incoming traps from the network using port 162. Trap messages can be logged or deleted, or they can invoke additional actions if they fit a certain pattern or profile |
| UDP | User Datagram Protocol; a lightweight transport layer protocol that provides no guarantee of information delivery |
| Unicast | A datalink frame sent from one system to another. A unicast frame is directed to a specific device on a network |
| URL | Universal Resource Locator; a pathname that contains a host name plus a directory path to retrieve a particular Web page |
| Variable binding list | A field with an SNMP PDU containing specific MIB objects and associated values |
| Virtual LANs | Virtual Local Area Network (VLAN); a logical collection of networking devices (servers, workstations, etc.) that are contained within a single broadcast domain |
| WAN | Wide Area Network; a network that is spread out over a large geographic area or based on WAN technologies such as ATM, Frame Relay, PPP, and others. |
| WWW | World Wide Web; a collection of Web sites that span the globe |

## Index

### Symbols

- . (dot) 25
- accessing 25

### A

- abstract syntax notation (ASN.1)
- see ASN.1
- access control list (ACL) 19
- access mode 31, 297
- Accessing Objects 37
- ACK segment 75, 77, 80
- address primitives 163
- Address Resolution Protocol (ARP)
- see ARP 66
- agent 4, 23
  - architecture 55
  - determining functionality of 6
  - extensible 7, 8
  - external behavior 5
  - internal behavior 6
  - master agent 55
  - master and 54
  - master/subagent architecture 55
  - multiple 7
  - overview of 326
  - port contention problem 55
  - public domain 6
  - SNMP 5
  - subagent 54
- agent functional diagram 8
- AgentX 56
- alarms 15
- application data types
  - counter 29
  - displaystring 29
  - gauge 30
  - networkAddress 30
  - opaque 30
  - TimeTicks 30
- Application Layer 60
- Application Programming Interface (API) 13, 613
- ARCHIE 69
- architecture 13
- arithmetic operators 168
- arithmetic primitives 164
- ARP 66, 95, 96
  - --display option 110
  - -a option 110
  - -d option 112
  - -f option 114, 115
  - -n option 110
  - -s option 112
  - -v command example 107
  - Address field 108
  - advantages 97
  - C flag 109
  - cache 98, 99, 106
  - command character format 107
  - command-line options 107
  - datalink address format 100
  - deleting an ARP cache 112
  - description 106
  - Flag Mask field 108
  - Flag Mask field options 108
  - hardware type 98
  - hardware type field 98
  - hlen field 98
  - HWAddress field 108
  - HWType field 108
  - iface field 109
  - incomplete string 109
  - keyword format 107
  - loading ARP bindings using a file 113
  - M flag 113
  - message format 98
  - netmask option 114
  - operation field 98
  - P flag 109
  - packet fields 97
  - packet format 97
  - plen fields 98
  - protocol fields 98
  - proxy ARP 109, 114
  - pub keyword 114
  - refreshing cache bindings 99
  - remote dial-up access strategies 114
  - reply 97
  - request 96
  - sample 107
  - Sender HA 98
  - Sender IP 98
  - startup script 114
  - superuser privileges 107
  - target IP 98
  - temp keyword 114
- ARP cache 98
  - adding an entry 112
  - displaying 107
- arwatch
  - changed Ethernet address 186
  - command-line options 185
  - description 184
  - flip flop 187
  - new activity 188
  - new station 185
  - types of messages 185
- ASN.1 27, 41
  - application types 28
  - universal types 28
- at group 267
- authentication-failure traps
  - see also MIB-II
  - SNMP group 314
- B
- back-off 135
- backbone devices 466
- baud rate 547
- binding
  - standard address used to bind to local port 305
- Boolean operators 168
- broadcast 96
  - address 120
  - domain 19
- C
- Check Reachability 597
- Chesapeake Software
  - installing 634
- CMU Software Packages and snmpconf
  - installing 642
- collision 135
- common management Information protocol (CMIP) 13
- community name 40
- compress 159
- Configuration Control 414
- configurator tool 537
- connectionless protocol 54
- connections 72
- connectivity business 145
- control panel 119, 534
  - see Linux control panel 534
- Core Services 15
- D
- datalink address 106, 120
  - binding 106
  - mapping 106
  - table 106
- DataLink Address Format 100
- vendor list 101
- vendor OUI codes 101
- datalink frame sizes 192
- debugging 115, 125, 143
- network problems 177, 178
- network protocols 163
- default gateway 553
- developers
- agent 6
- devices 412
  - actual performance, determining 505
  - automated configuring with snmpconf tool 455
  - automatic discovery of interface 475
  - connection, observing state of 520
  - important information 412
  - interface, validate with cgmaker 475
  - performance problems 466
  - see also MRTG tool, target keyword
- di23r3cg 492
  - command-line options 494
- DHCP 66
- Directory Layout 641
- disk consumption monitoring 493
- disk space utilization 467
- DNS 67
- DNS information 539
- Domain Name Service (DNS)
  - see DNS
- dotted decimal notation 121
- dotted notation 25
  - see also MIB, dotted notation 25
- duplex session 73
- Dynamic Host Configuration Protocol (DHCP), see DHCP 66

### E

- edge router 466
- enterprise branch 461
- enterprise MIBs 38
  - assigned enterprise numbers 38, 39
  - development 38
- enterprise number
  - Sun's 383
- ethereal 453, 507, 530
  - TCP Display option 210
  - description 188
  - display options 190, 205
  - follow TCP stream menu item 205
  - functional options 190
  - installation 628
  - Match Selected option 209
  - network traffic, capturing 192
  - packet capture, optimizing 192
  - printing 203
  - saving captured data to UNIX file 201
  - setting preferences and options 202
  - Summary sub-menu 207
- ethereal Capture/Preferences window 193
- ethereal Capture/Playback window 193
- ethereal filter window 198
- ethereal packet summary window 208
- ethereal preferences window 203
- ethereal printing preferences 204
- ethereal time field display options window 205
- ethernet
  - capture packet types 194
  - display filter 197
  - examining packets 194
  - filtering network capture 199
  - packet
    - ARP portion 196
    - Ethernet II field 195
    - hexadecimal format 196
  - packet capture filter 197
  - permanent filters 197
  - standard message size 120
  - using filters 197
- events 16
- External Gateway Protocol (EGP)
  - see MIB-II, EGP group 306

### F

- fault detection 15
