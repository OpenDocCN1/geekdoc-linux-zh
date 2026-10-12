To retrieve the value of a variable, we use **snmpget** (Linux – Figure 17.20) or **snmputil get** (NT – Figure 17.21), followed by the name of the host we’re interrogating, the community string, and the ID of the object whose value you want. (Note that an OID must begin with a dot, or you get an error.) We also set a value using **snmpset** (Linux only – the NT tools don’t let you set variables).

![](bbox=[0.16, 0.18, 0.74, 0.38])

# **Figure 17.21** snmputil get on Windows-NT

Note that when we specify a variable, we append an *instance* value to its OID. For example, the OID of the sysName variable is 1.3.6.1.2.1.1.5, but when getting it we specified 1.3.6.1.2.1.1.5.0. The instance here is zero because this is a simple scalar variable and not an array. Instances are necessary to allow tables of values to be referenced. The Notes give more information on arrays and instances; for now, just remember that each simple variable must have an instance of zero appended – otherwise you’ll get an error message when you try to reference it.

Looking at a trace for a couple of these commands, using “**tcpdump -s200 port snmp**” (“-s200” to capture enough bytes to show all the detail) we see that the protocol is very simple indeed, and what happens on the wire reflects very closely the commands we issued:

```
```text
alice 2214 > bob.161:	GetRequest(32)	1.3.6.1.2.1.1.6.0
bob.161 > alice.2214:	GetResponse(44)	.1.3.6.1.2.1.1.6.0="Server rack no. 3"
alice 2214 > bob.161:	SetRequest(48)	.1.3.6.1.2.1.1.6.0="Server rack no. 4"
bob.161 > alice.2214:	GetResponse(44)	1.3.6.1.2.1.1.6.0="Server rack no 4" ```
```

Using **ethereal** on the same commands, we can see exactly what the packets contain, in the figure shown below.

The Notes at the end of the chapter give you pointers on how to explore SNMP in more depth.

![](bbox=[0.18, 0.73, 0.75, 0.95])