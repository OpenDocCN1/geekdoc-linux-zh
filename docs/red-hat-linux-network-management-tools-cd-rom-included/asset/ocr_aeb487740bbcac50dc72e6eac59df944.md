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