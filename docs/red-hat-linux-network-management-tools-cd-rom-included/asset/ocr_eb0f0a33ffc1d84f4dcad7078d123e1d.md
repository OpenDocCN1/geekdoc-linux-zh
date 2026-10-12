```
snmpcmd protocol_version [additional_options] hostname community object [object]
```

The word *snmpcmd* is a placeholder and represents one of the UCD commands listed in the preceding table. All the UCD tools support this basic command syntax. The word *protocol_version* can be 1, 2c, or 3. This string identifier specifies which SNMP version should be used when sending queries to the agent. Option 1 represents the standard SNMPv1 format. The 2c option indicates differences within the supported SNMP protocol data units, but uses the same community-based approach as in SNMPv1. The 3 option indicates the use of the SNMPv3 security model.

The *additional_options* placeholder represents options that control both display attributes and operational behavior of the tools. The most commonly used command-line options are described below.

The word *hostname* can be replaced with the name of any host on the network that contains an SNMP agent that matches the *protocol_version* information specified on the command line. A valid IP address, expressed in dotted notation, may be used instead of a hostname.

The word *object* represents the MIB OID that should be retrieved (in the case of an SNMP *get-request*) or altered (in the case of an SNMP *set-requests*). It may be expressed in either dotted numeric or dotted named notation. In the case of an SNMP *set-request* operation, additional object information will be required, as discussed in the upcoming “SNMSet Tool” section. Note that one or more objects may be specified on the command line.

# Common Command-line Options

UCD tools share a number of common command-line arguments. Having a core set of options makes them easier to remember and use. The arguments supported by all the commands are divided into two categories: operational options and display options. The operational options control the behavior of each of the tools, while the display options control how the MIB objects, associated values, and other information are displayed.