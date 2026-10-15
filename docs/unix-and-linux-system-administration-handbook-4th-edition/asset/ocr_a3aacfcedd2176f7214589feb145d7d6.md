# The NET-SNMP tools

Even if your system comes with its own SNMP server, you may still want to compile and install the client-side tools from the NET-SNMP package. Table 21.3 lists the most commonly used tools.

| Command | Function |
|---|---|
| `snmpdelta` | Monitors changes in SNMP variables over time |
| `snmpdf` | Monitors disk space on a remote host via SNMP |
| `snmpget` | Gets the value of an SNMP variable from an agent |
| `snmpgetnext` | Gets the next variable in sequence |
| `snmpset` | Sets an SNMP variable on an agent |
| `snmptable` | Gets a table of SNMP variables |
| `snmptranslate` | Searches for and describes OIDs in the MIB hierarchy |
| `snmptrap` | Generates a trap alert |
| `snmpwalk` | Traverses a MIB starting at a particular OID |

In addition to their value on the command line, these programs are tremendously handy in simple scripts. It is often helpful to have `snmpget` save interesting data values to a text file every few minutes. (Use `cron` to implement the scheduling; see Chapter 9, *Periodic Processes*.)

`snmpwalk` is another useful tool. Starting at a specified OID (or at the beginning of the MIB, by default), this command repeatedly makes “get next” calls to an agent. This behavior results in a complete list of available OIDs and their associated values. `snmpwalk` is particularly handy when you are trying to identify new OIDs to monitor from your fancy enterprise management tool.

Here’s a truncated sample `snmpwalk` of the host tuva. The community string is “secret813community”, and `-v1` specifies simple authentication.

```
```text
$ snmpwalk -c secret813community -v1 tuva
SNMPv2-MIB::sysDescr.0 = STRING: Linux tuva.atrust.com 2.6.9-11.ELsmp #1
SNMPv2-MIB::sysUpTime.0 = Timeticks: (1442) 0:00:14.42
SNMPv2-MIB::sysName.0 = STRING: tuva.atrust.com
IF-MIB::ifDescr.1 = STRING: lo
IF-MIB::ifDescr.2 = STRING: eth0
IF-MIB::ifDescr.3 = STRING: eth1
IF-MIB::ifType.1 = INTEGER: softwareLoopback(24)
IF-MIB::ifType.2 = INTEGER: ethernetCsmacd(6)
IF-MIB::ifType.3 = INTEGER: ethernetCsmacd(6)
IF-MIB::ifPhysAddress.1 = STRING:
IF-MIB::ifPhysAddress.2 = STRING: 0:11:43:9d:1e:f5
IF-MIB::ifPhysAddress.3 = STRING: 0:11:43:9d:1e:f6
```
```