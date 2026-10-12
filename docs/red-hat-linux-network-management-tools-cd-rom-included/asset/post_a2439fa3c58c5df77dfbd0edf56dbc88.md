
**Description:** This file is used to contain subagent configuration information and is used by the master agent upon startup

**Object Name:** sunMasterAgentConfigurationDir  
**OID:** sunMasterAgent.3  
**Object Type:** Display String  
**Access Mode:** read-write  
**Description:** The directory that contains the configuration files for the master agent

**Object Name:** sunMasterAgentTrapPort  
**OID:** sunMasterAgent.4  
**Object Type:** INTEGER  
**Access Mode:** read-only  
**Description:** The port used by the master agent to receive SNMP traps from each of the subagents. These traps are then forwarded to one or more managers found in the master agent configuration file

**Object Name:** sunCheckSubAgentName  
**OID:** sunMasterAgent.5  
**Object Type:** Display String  
**Access Mode:** read-write  
**Description:** Used by the subagents to check that no duplicate subagent with the same name is running

| **Object Name:** | `sunMasterAgentPollInterval` |
| **OID:** | `sunMasterAgent.6` |
| **Object Type:** | `INTEGER` |
| **Access Mode:** | `read-only` |
| **Description:** | This variable contains the time interval when the agent will perform housekeeping activities, such as determining if the resource file has changed, rediscovering each subagent, and other related tasks |

| **Object Name:** | `sunMasterAgentMaxAgentTimeOut` |
| **OID:** | `sunMasterAgent.7` |
| **Object Type:** | `INTEGER` |
| **Access Mode:** | `read-only` |
| **Description:** | This object is used to signify the maximum allowed timeout that a subagent can set. This is used by the master agent to wait when sending requests to a subagent before the request is considered to have expired |

## Subagent Configuration Objects

Additional objects within the `snmpdx.mib` file provide information on each subagent operating under the master agent. This information is available via a table and using index objects. The table (`sunSubAgentTable`) lists all the subagents that have been registered with the master agent. Each entry in this table is described as a `sunSubAgentEntry` object. Access to the `sunSubAgentTable` table is via the `sunSubAgentEntry` object. Figure 7.8 shows the hierarchy of the `sunSubAgentTable` group from the standard `enterprises` branch.

![](img/f265c9d1f2610aca197c430cbfcd51f5_418_0.png)

Figure 7.8 The `sunSubAgentEntry` view.

The `sunSubAgentEntry` table consists of the following subagent-related objects:

|  |  |
| --- | --- |
| Object Name: | `sunSubAgentID` |
| OID: | `sunSubAgentEntry.1` |
| Object Type: | INTEGER |
| Access Mode: | read-only |
| Description: | This is the unique ID for each subagent running under the master agent |

Object Name: sunSubAgentStatus
OID: sunSubAgentEntry.2
Object Type: INTEGER
Access Mode: read-write
Description: Indicates the state of the subagent. Possible states include init(1), load(2), active(3), inactive(4), and destroy(5)

Object Name: sunSubAgentTimeout
OID: sunSubAgentEntry.3
Object Type: INTEGER
Access Mode: read-write
Description: The maximum amount of time that the master agent will wait for a subagent to complete a request, expressed in microseconds

Object Name: sunSubAgentPortNumber
OID: sunSubAgentEntry.4
Object Type: INTEGER
Access Mode: read-write
Description: The port number used by the subagent to listen for requests from the master agent

Object Name: sunSubAgentRegistrationFile
OID: sunSubAgentEntry.5
Object Type: Display String
Access Mode: read-write
Description: Specifies the registration file used by the subagent. Each subagent must have its own file and contain the subagent name, MIB tree information, preferred SNMP port, etc

**Object Name:** sunSubAgentAccessControlFile
**OID:** sunSubAgentEntry.6
**Object Type:** Display String
**Access Mode:** read-write
**Description:** Specifies the access control file used by the subagent to store SNMP community information

**Object Name:** sunSubAgentExecutable
**OID:** sunSubAgentEntry.7
**Object Type:** Display String
**Access Mode:** read-write
**Description:** Contains the executable subagent program

**Object Name:** sunSubAgentVersionNum
**OID:** sunSubAgentEntry.8
**Object Type:** Display String
**Access Mode:** read-write
**Description:** The version information for the subagent

Object Name: sunSubAgentProcessID
OID: sunSubAgentEntry.9
Object Type: Display String
Access Mode: read-write
Description: The process ID of the subagent

Object Name: sunSubAgentName
OID: sunSubAgentEntry.10
Object Type: Display String
Access Mode: read-write
Description: The name of the subagent specified in the registration file

Object Name: sunSubAgentSystemUpTime
OID: sunSubAgentEntry.11
Object Type: TimeTicks
Access Mode: read-write
Description: The system up time of the subagent

Object Name: sunSubAgentWatchDogTime
OID: sunSubAgentEntry.12
Object Type: INTEGER
Access Mode: read-write
Description: The amount of time that the master agent waits before polling the subagent to ensure that it is still operating correctly, expressed in seconds

## Sun SNMP Agent

The Sun agent can provide the following services:

- obtain network statistics
- obtain system process information
- obtain system memory information
- send traps to specified systems

This system and network information will be available by polling the agent's MIB. The agent supports both MIB-II and portions of Sun's private MIB. The Sun MIB is described below. The *trap definition*, which must be done in the agent configuration file, is also described below.

## Command-line Options

The `mib1isa` utility supports several command-line options, as outlined in Table 7.5. Perhaps one of the most important is the -r option, which can be used to disable write access to the agent's MIB. Because the `mib1isa` utility implements SNMPv1, the agent doesn't provide a very robust security model. It might be necessary to limit the access to the system objects supported by the agent. Using this option, all SNMP set-requests will be rejected, but read access will operate without being affected.

Any attempt to alter or set an MIB object after the -r option has been used will cause an error. More specifically, when using a MIB browser, for example, if an attempt is made to set MIB objects that are placed in read-only mode, the authentication trap message will be generated.

Table 7.5 *Master agent command options*

| Option | Description |
|:-----|:-----|
| -a | Disable authentication traps |
| -c | Specify path to search for the configuration file |
| -d | Enable debugging output |
| -p | Use specified port instead of 161 |
| -r | Place the MIB in read-only mode |

By default, the directory in which mib1isa searches for the required configuration file is /etc/snmp/conf. To specify an alternate directory, use the -c option followed by the directory name. This option can be used to help test new configuration files that might reside in other directory locations. The mib1isa agent requires a configuration file, and if it can't locate a valid configuration, it will exit with an error.

When an SNMP entity attempts to poll an agent with the incorrect community string, an authentication message is dispatched to the addresses configured in the mib1isa configuration file. If you would like to disable these trap messages, use the -a option.

To place the agent in debug mode, the -d option can be used when invoking the agent on the command line. Also, an optional debug level can be included that decreases levels of debugging from 3 (which is the highest) to 1 (which is the lowest).

Depending on the networking services presently running on the system, it might be necessary to use a different UDP port instead of the default of 161. This will be required if the mib1isa agent is running with a master agent. In this case, the agent will need to be started on a different port using the -p option. For example, to start the agent on port 32000, use the following command:

```
# /usr/lib/snmp/mib1isa -p 32000
```

## Configuring the Sun Agent

The mib1isa agent uses a configuration file called snmpd.conf and, by default, searches the /etc/snmp/conf directory for this file. This file contains configuration information that controls access to the agent's MIB and additional control information. Each entry contains a keyword followed by a string value, separated by one or more white spaces. Comments are also supported in this file by using the pound sign (#) and are ignored when processed by the
