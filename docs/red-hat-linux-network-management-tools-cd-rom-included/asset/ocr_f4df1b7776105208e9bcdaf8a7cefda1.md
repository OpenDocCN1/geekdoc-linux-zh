address of any system that has been in communication with the agent, along with date and time information. This is useful for establishing that any configured ACLs are working properly. When an option is used, the agent will display messages like the following:

```
1999-11-21 16:04:17 Received SNMP packet(s) from 10.0.2.126
```

The -d option displays the UDP packets sent to and received from the agent and is used to help detect SNMP protocol-related problems or other operations issues. Also, this option can be used to examine the MIB object requested from SNMP client applications. A sample of the agent debugging output is shown here:

```
GET
  -- system.sysContact.0
   >> system.sysContact.0 = Steve Maxwell
sent 64 bytes to 10.0.2.126:
0000: 30 82 00 3c 02 01 00 04 6f 70 75 62 6c 69 63 34  0.<....public..
0016: 92 00 20 02 04 23 c1 e0 9f 02 01 00 02 01 00 30  ...*.......
0032: 82 00 10 30 82 00 19 06 08 28 60 01 02 01 01 04  ...
0048: 00 00 5d 74 65 76 65 20 4d 61 78 77 65 6c        ...Steve Maxwell
```

In this sample, the agent obtains an SNMP get request from the system with IP address 10.0.2.126. The agent displays the string “...” to indicate what the remote SNMP entity requests (in this case, the sysContact object) and the “>>” string shows what the agent returns. The hexadecimal output corresponds to the entire UDP packet, which includes the community string information and any returned object(s). If you want just the protocol transaction and not the UDP packet trace, use the -v option. This option will display

```
GET
  -- system.sysLocation.0
   >> system.sysLocation.0 = Graphics Lab 11-B
```

as a result of a request for the sysLocation MIB object from an SNMP client application.

The -q option, according to the documentation in the UCD package, displays simpler formatting that can be used, for example, to automate parsing of the agent output. Unfortunately, this option doesn’t seem to do anything in release 4 of the agent tested.