(IOS) running on the system. The IOS is the Cisco system software that provides all the routing and processing functions for a large array of Cisco hardware devices. In this example, the system model is a 3000 series router running version 11.0 that has been up for the last 1.5 days.

Please note that sometimes when accessing objects from certain devices, we may encounter error messages that lead us to believe that the device in question does not support the objects specified with the SNMP command. For example, consider the following command that is executed against a Linux system called \(monet\):

```
# snmpget monet private-write system.sysDescr.0
```

The command produces the following:

```
system.sysDescr.0 = "Linux monet 2.2.5-15 #5 Mon Aug 2\n 21:07:04 EDT 1999 i586"
```

However, running the same command against the same system but using a different community string, as shown:

```
# snmpget monet bad-password system.sysDescr.0
```

displays the following message:

```
Error in packet\nReason: (noSuchName) There is no such variable name in this MIB.\nThis name doesn't exist: system.sysDescr.0
```

In the preceding example, the error message isn't clear about what is going on; the message suggests that the object being requested does not exist within the agent. Obviously, from the first example, the object \(system.sysDescr.0\) does exist and has an associated value. The reason for the disparity lies in the fact that the Linux agent supports different views of the MIB tree. In the last command, it simply attempted to search for the \(system.sysDescr.0\) object within the view that was associated with the \(bad-password\) community string. MIB views were introduced with SNMPv2, and the Linux agent supports these protocols. In actuality, since the \(bad-password\) command string is invalid, the agent issued the most appropriate response for the situation.