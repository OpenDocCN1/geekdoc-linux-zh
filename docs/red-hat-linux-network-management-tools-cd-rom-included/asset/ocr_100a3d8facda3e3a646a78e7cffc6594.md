the field separator when displaying the same TCP table above, use the following command sequence(shown with output):

```
# snmp table 10.0.2.240 public -f : tcp.tcpConnTable

SNMP table: tcp.tcpConnTable

tcpConnLocalAddress:tcpConnLocalPort:tcpConnRemAddress:tcpConnRemPort

listen:0.0.0.0:23:0.0.0.0:0

listen:0.0.0.0:111:0.0.0.0:0

listen:0.0.0.0:513:0.0.0.0:0

established:10.0.2.240:23:10.0.2.75:33441
```

Each of the columns is now separated by the : character, making it very easy to parse this information as input into other programs. The -b option can be used to provide a more descriptive column label, as shown here. The at.atTable table contains the address translation mappings between IP addresses and physical addresses. In this case, three column labels are displayed: IfIndex, PhysAddress, and NetAddress. The ifIndex is the index in the interface table and shows from which interfaces these mappings originated. The PhysAddress is the datalink address (Ethernet in this case), and the NetAddress is the IP address associated with each device on the network. The command:

```
# snmp table cisco-gw5 public -b at.atTable
```

probes the MIB-II address translation group and provides the following sample output:

SNMP table: at.atTable

|IfIndex|PhysAddress|NetAddress|
|---|---|---|
|2|"08 00 20 8D 81 B2"|10.0.1.100|
|2|"00 60 47 1F 76 8A"|10.0.1.120|
|14|"00 60 88 91 4A 64"|10.0.2.110|
|14|"00 60 95 AD F2 1F"|10.0.2.111|
|14|"00 80 5F E2 88 3D"|10.0.2.117|
|14|"00 60 B8 94 37 FC"|10.0.2.200|
|14|"08 00 20 B6 2F C2"|10.0.2.221|
|14|"00 60 88 62 C7 C1"|10.0.2.226|
|14|"08 00 20 7A CA 49"|10.0.2.234|
|14|"08 00 20 25 70 E7"|10.0.2.250|
|14|"00 20 CA FA E6 99"|10.0.2.251|
|14|"00 60 88 10 D8 A5"|10.0.2.252|
|14|"00 80 A3 03 4E 98"|10.0.2.257|