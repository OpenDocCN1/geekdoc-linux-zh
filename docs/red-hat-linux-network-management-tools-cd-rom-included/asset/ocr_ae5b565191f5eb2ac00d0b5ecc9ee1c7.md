Finally, the `-S` option requests that the MIB object be printed with both suffix and MIB name. Thus, the `-S` will display `.iso.org.dod.internet.mgmt.mib-2.system.sysUpTime.0` as shown:

```
SNMPv2-MIB::sysUpTime.0
```

Please note that, in this example, the `sysUpTime` object is found within the SNMPv2-MIB; this is true when you use the UCD tools. Traditionally, however, this object is found in the MIB-2 tree.

If you need to collect SNMP information from a `-q` device and use this information as input into another program, the `-q` option will come in handy. Normally, MIB object information is displayed as shown:

```
system.sysObjectID.0 = OID: enterprises.9.1.17
system.sysUpTime.0 = Timesticks: (139494644) 16 days, 3:29:06.44
system.sysContact.0 = Matthew Maxwell
system.sysName.0 = remote-gw5
system.sysLocation.0 = Remote Sales Office (San Jose)
system.sysServices.0 = 6
```

The `-q` option, which stands for *quick* format, causes the output above to be formatted differently. First, the equal sign (=) is removed; this makes it easier to parse because the data is now in column format. Second, notice that both the `sysObjectID` and `sysUpTime` formats have been altered. The information for these two objects in the preceding example is interpreted, while, in the following example, only the raw data is displayed.

```
system.sysObjectID.0 enterprises.9.1.17
system.sysUpTime.0 16:3:24:11.44
system.sysContact.0 Matthew Maxwell
system.sysName.0 remote-gw5
system.sysLocation.0 Remote Sales Office (San Jose)
system.sysServices.0 6
```

To display debugging information, use the `-d` option. This shows the packet information, including the size and destination, and also provides a hexadecimal and ASCII dump of the packet. The output shown here is the result of an SNMP *get* -request of the `system.sysContact` MIB object: