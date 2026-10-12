
**Object Name:** dot3ErrorInitError
**OID:** dot3Errors.1
**Object Type:** Counter
**Access Mode:** read-only
**Description:** Identifies errors related to the chipset that failed tests

**Object Name:** dot3StateIndex
**OID:** dot3StateEntry.1
**Object Type:** Counter
**Access Mode:** read-only
**Description:** Errors associated with running the loopback tests

## SNMP Group

The snmp group contains information related to the operation and implementation of SNMP. Some of the objects within this group are related to SNMP station management or agent functions. Hence, each SNMP implementation may use certain objects from the table. Those objects not supported by the agent contain a zero value.

With the exception of the snmpEnableAuthenTraps object, which is read-write, all the other objects are read-only. This object controls whether the agent is permitted to generate authentication-failure traps and is usually set by a network management application. Authentication failures are the result of a management entity attempting to execute some privileged function on the agent when it doesn’t have the correct security permission or credentials to do so. Figure 6.16 shows the tree view of the snmp table.

Notice that both positions 7 and 8 are not listed because the MIB doesn’t define any objects for these slots. As you can see in Figure 6.16, many of the SNMP objects are listed in gray, while a few are listed in black. This is because the original version of the table included all the gray objects plus some of the others as well. When the SNMPv2 specification was published, many of these objects were deprecated. However, since many agents continued to support SNMPv1, these objects are still in use. This is one example of when newer MIB specifications have little effect on what was implemented in the past. The older snmp group objects will be with us for a long time. The snmp table contains the following objects:

![](img/f265c9d1f2610aca197c430cbfcd51f5_346_0.png)

Figure 6.16 The snmp group view.

**Object Name:** snmpInPkts
**OID:** snmp.1
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP messages delivered to the agent

**Object Name:** snmpOutPkts **(Deprecated)**
**OID:** snmp.2
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP messages passed from the agent to the transport layer

**Object Name:** snmpInBadVersions
**OID:** snmp.3
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP messages passed to the agent that were unsupported

**Object Name:** snmpInBadCommunityNames
**OID:** snmp.4
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP messages passed to the agent that contained an unknown community name

**Object Name:** snmpInBadCommunityUses
**OID:** snmp.5
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP messages passed to the agent that contained an SNMP operation not allowed by the SNMP community name supplied

**Object Name:** snmpInASNParseErrs
**OID:** snmp.6
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of BER and ASN errors encountered when decoding incoming SNMP messages

**Object Name:** snmpInTooBig (Deprecated)
**OID:** snmp.8
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs delivered to the agent for which the tooBig error occurred

**Object Name:** snmpInNoSuchName (Deprecated)
**OID:** snmp.9
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs delivered to the agent for which the noSuchName error occurred

**Object Name:** snmpInBadValues (Deprecated)
**OID:** snmp.10
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs delivered to the agent for which the badValue error occurred

**Object Name:** snmpInReadOnlys (Deprecated)
**OID:** snmp.11
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs delivered to the agent for which the readOnly error occurred

**Object Name:** snmpInGenErrs (Deprecated)
**OID:** snmp.12
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs delivered to the agent for which the genErr error occurred

**Object Name:** snmpInTotalReqVars (Deprecated)
**OID:** snmp.13
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of MIB objects retrieved successfully by the agent as a result of a valid SNMP get-request and getnext-request

**Object Name:** snmpInTotalSetVars (Deprecated)
**OID:** snmp.14
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of MIB objects retrieved successfully by the agent as a result of a valid SNMP set-request

**Object Name:** snmpInGetRequests (Deprecated)
**OID:** snmp.15
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP get-requests accepted and processed by the agent

**Object Name:** snmpInGetNexts (Deprecated)
**OID:** snmp.16
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP getnext-requests accepted and processed by the agent

**Object Name:** snmpInSetRequests
**OID:** snmp.17
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP set-requests accepted and processed by the agent

**Object Name:** snmpInGetResponses (Deprecated)
**OID:** snmp.18
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP get-responses accepted and processed by the agent

**Object Name:** snmpInTraps (Deprecated)
**OID:** snmp.19
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP traps accepted and processed by the agent

**Object Name:** snmpOutTooBig
**OID:** snmp.20
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs generated by the agent for which the tooBig error occurred

**Object Name:** snmpOutNoSuchNames (Deprecated)
**OID:** snmp.21
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs generated by the agent for which the noSuchName error occurred

**Object Name:** snmpOutBadValues **(Deprecated)**
**OID:** snmp.22
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs generated by the agent for which the `badValue` error occurred

**Object Name:** snmpOutGenErrs **(Deprecated)**
**OID:** snmp.24
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP PDUs generated by the agent for which the `genErr` error occurred

**Object Name:** snmpOutGetRequests **(Deprecated)**
**OID:** snmp.25
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP `get-request` PDUs generated by the agent

**Object Name:** snmpOutGetNexts **(Deprecated)**
**OID:** snmp.26
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP `getNext-request` PDUs generated by the agent

**Object Name:** snmpOutSetRequests **(Deprecated)**
**OID:** snmp.27
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP set-request PDUs generated by the agent

**Object Name:** snmpOutGetResponses **(Deprecated)**
**OID:** snmp.28
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP get-responses PDUs generated by the agent

**Object Name:** snmpOutTraps **(Deprecated)**
**OID:** snmp.29
**Object Type:** Counter
**Access Mode:** read-only
**Description:** The number of SNMP traps generated by the agent

**Object Name:** snmpEnableAuthenTraps
**OID:** snmp.30
**Object Type:** Integer
**Access Mode:** read-write
**Description:** Whether authentication failure traps should be generated. Valid values are `enabled(1)` or `disabled(2)`. When an SNMP entity attempts to query the agent with an invalid community string or authentication token, the agent will emit an SNMP trap if enabled
