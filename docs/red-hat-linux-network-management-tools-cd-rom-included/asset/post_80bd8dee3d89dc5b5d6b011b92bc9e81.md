
## Using SNMP Agents

This chapter provides a detailed overview of SNMP agents that are available specifically on Linux and Solaris systems. Red Hat Linux systems are shipped with the University of California at Davis (UCD) SNMP system agent that provides both MIB-II and UCD specific objects. The Sun agent, known as the Solstice Enterprise Agent (SEA), comes with the latest release of Solaris and includes Sun-specific MIB objects. The SEA package actually includes two agents: a master and a subagent. Because the term *Solstice* also refers to Sun's network management framework and mix of products, this book will use the terms *master agent* and *subagent* to describe these agents from Sun.

## Overview of Agents

All three of the agents listed above provide some of the same fundamental services: namely, the retrieval and setting of MIB objects. Each of the agents supports the standard SNMP basic operations, including get, set, and trap. Additionally, each of the agents provides some specialized functions such as support for disk or memory management. Which agent to use depends on the environment and the types of problems you attempt to solve. It might, for example, be necessary to use all three agents because each provides services that are required.

The functionality of each of the agents can be summarized into several categories:

- MIB-II Support: The agent supports either most of or the entire standard set of MIB-II objects. The MIB-II standard is described in the preceding chapter.
- Process Management: Additional MIB objects are available to manage UNIX processes. Basic operations include listing and controlling these processes via the agent.
- Remote Configuration: The agent can manipulate its own configuration file via the SNMP protocol. For example, the agent can be made to dynamically alter a predefined action when the monitored object reaches a critical threshold.
- Extended MIB Support: The agent supports additional MIB objects, which provide information beyond the MIB-II standard. This might include either proprietary vendor-specific MIBs or standard MIBs such as the Host Resource MIB.
- Flexible Configuration: The agent provides a flexible set of configuration options and keywords, which are primarily used to control the operating state and behavior of the agent.
- Performance Objects: The agent supports additional MIB objects that provide additional performance information or statistical data.
- Customizable Actions: The agent can execute external scripts or programs contained within the agent configuration file. These actions are usually the direct result of some specific condition or event that the agent has detected.
- Memory/Disk Management: The agent provides additional MIB objects that provide additional memory or disk information or statistical data.
- Master Agent Support: The agent provides the capability for subagents to register to receive SNMP messages. The master agent is responsible for handling outside communication on behalf of the subagents. The master agent uses SNMP port 161, while the subagents communicate with the master agent on another predefined port.
- Extensible: The agent can be extended to support additional functionality and provide new features such as executing external UNIX shell scripts or other commands. This might also mean that the agent provides a development environment that includes interfaces that facilitate adding new features by recompiling (or linking) various components of the package.
- SNMPv2/v3: The agent supports one or more elements of SNMPv2 and/or SNMPv3 protocol specifications.

Table 7.1 outlines the functionality of each agent and can be used as a quick reference when choosing an agent.

## Table 7.1 Functional overview of agents

| Category | Linux | Sun Master | Sun |
| :--- | :---: | :---: | :---: |
| MIB-II objects | | ✓ | ✓ |
| Process management objects | | ✓ | ✓ |
| Remote configuration | ✓ | | |
| Additional system objects | | | ✓ |
| Flexible configuration | ✓ | | ✓ |
| Additional performance objects | ✓ | | ✓ |
| Customizable actions | ✓ | | |
| Memory management objects | | ✓ | |
| Disk management objects | ✓ | | |
| Master agent | | ✓ | |
| Subagent management | | ✓ | |
| Extensible capabilities | ✓ | | |
| SNMP v2/v3 | ✓ | | |

## The Linux SNMP Agent

The Linux agent, known as snmpd, provides a comprehensive list of SNMP-related services. The Linux agent is actually the agent of the University of California at Davis known as the UCD-agent and is available on a large number of operating systems, including Linux. This agent supports SNMPv1, SNMPv2, and SNMPv3 network management protocols. This means it supports not only the basic SNMP operations, but also those associated with SNMPv2, such as `get-bulk`, `get-inform`, and several others.

Also, it supports the User Security Model (USM) that is described within the SNMPv3 specifications. It supports MIB-II, the UCD MIB, and several other MIBs as well. The agent provides the capability to remotely execute UNIX commands that have been configured based on certain events or conditions. The agent can be used to monitor both system memory and process information.

The advantages of using the UCD package are significant. First, the software provides a very complete set of tools and features that are available within the public domain. The package includes user SNMP tools, plus a fully functional SNMP agent. Many SNMP packages are available on the Internet, but most don't compare to the stability, robustness, and features found within the UCD package. Second, despite the fact that the UCD software is in the public domain, it seems to have a loyal following and has seen continuous improvement over the years, even surpassing some well-established commercial products in terms of SNMP protocol support and features. The UCD tools are supported on a large number of computer platforms and operating systems. The package is included in certain Linux distributions, such as Red Hat. Finally, the UCD package is free, which means it can be deployed across the network enterprise without concern for licensing issues. This makes the agent very attractive to budget-constrained institutions and other organizations.

### Sun's Master Agent

Sun provides a standard SNMP network management master agent that can be used as the basis for an enterprise management strategy. This agent, called snmpd, provides a master/subagent facility for one or more subagents. Recall from Chapter 2, “Simple Network Management Protocol,” that the main purpose and role of a master agent is to permit many SNMP agents to coexist. Because each SNMP agent must listen for requests on well-known SNMP port 161, a mechanism must be provided so that all agents can share this port without conflict. Without special arbitration, the first agent to use the port would obtain an exclusive lock on the port, and all other agents would be denied access. With the snmpdx agent, many subagents can be installed on the same system without the traditional port contention problem. Also, this master agent supports a collection of MIB objects that describe each of the sub-agents that have been configured with the master agent.

### Sun's SNMP Agent

Sun also provides a standard SNMP network management system and agent. This agent, known as *mib1sa*, supports SNMPv1 and provides read-write access to both MIB-II and Sun enterprise specific objects. This agent works under Sun's master/slave agent architecture, which means that it can operate in conjunction with a master agent or in stand alone mode. It provides the ability to manage Sun workstations and servers from an operational and performance standpoint. It supports the standard MIB-II object groups and some additional groups defined by Sun. Together, the features of this agent can monitor some of the more critical network management problems that face network and system managers alike.

The advantages of using the UCD agent include integration into the operating system and support by the vendor. Because the agent is shipped with Solaris, the agent component can very easily be loaded with the operating system software. On older versions of the operating system that don't already have the agent, it is possible to install the agent in a straightforward manner by using Sun's pkgadd utility. Additionally, because the agent was developed by Sun, it will be supported should problems arise that require technical assistance. Finally, vendor support ensures that users can expect enhancements and new functionality to be included in future releases of the agent. This is important because SNMP will continue to change to meet the growing requirements of network and system administrators.

## Agent MIBs

Each of the agents described in this section implements either standard or private (or both) MIBs. Because both the Sun and UCD agents use private MIBs, access to these objects is at the enterprise branch level. Figure 7.1 shows the path from root to each of the vendor's private branches.
