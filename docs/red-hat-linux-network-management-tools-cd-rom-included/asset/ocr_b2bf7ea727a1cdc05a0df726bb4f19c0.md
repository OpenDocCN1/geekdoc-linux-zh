Target [10.0.2.200.1]:1.3.6.1.2.1.2.2.1.14,141.3.6.1.2.1.2.2.1.20.1, \
public@10.0.2.200

This command retrieves both input and output error counts on the interface known as 1.

Notice the use of the & character in the preceding command. MRTG requires two variables when displaying data; this character is used as a separator. Alternatively, one could use the SNMP-abbreviated object names instead of the direct OID convention. Thus, the command

```
Target[10.0.2.200,1]:ifInErrors.1&ifOutErrors.1:public@10.0.2.200
```

is functionally equivalent to the previous **Target** command. MRTG knows a limited number of SNMP objects; the list of objects can be expanded by modifying and adding objects to the mibhelp.txt file. This file contains mappings between some SNMP MIB-II objects and fully qualified OID paths. The following is a sample of this file:

```
Descriptor:	ifInErrors
Identifier:	1.3.6.1.2.1.2.2.1.14
ASN.1 Syntax:	Counter32

The number of inbound packets that contained errors preventing them from being deliverable to a higher-layer protocol.
```

This file sample shows the ifInErrors object used in the preceding **Target** command and contains a descriptor, identifier, and ASN.1 syntax of the object. The descriptor names the object that MRTG will use and is associated with the identifier string; it can be any string name as long as it is unique within the mibhelp.txt file. The identifier is the fully qualified path name of the object, minus the instance. The ASN.1 syntax refers to the object type and should match the object definition found within the MIB that defines the object. Finally, the entry contains descriptive text that explains the object definition. Although this text isn't required, it is very useful, and its inclusion is recommended when additional objects are added to this file.

Table 9.6 lists SNMP objects that are predefined within the mibhelp.txt file. Consult Chapter 6, “Overview of MIB-II,” for additional information about these MIB-II objects.