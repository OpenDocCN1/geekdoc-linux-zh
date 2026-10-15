# SNMP Authentication

Because SNMP can be used to monitor and manage network nodes, some means of security is required to ensure that network nodes cannot easily be compromised.

SNMP defines two access levels of security: public and private. The public level is granted read-only access to the node, and the private is given full control of the node (read and write). Unfortunately, these levels are passed in clear text.

# SNMP Security

The SNMP Internet Engineering Task Force did seek to improve the security with version 2 of the protocol, but the members could not agree on the security requirements, which caused two spin-offs of version 2 with some of the security requirement left to be created: V2u and V2c. The version 3 working group is trying to fix this weakness with a standards track specification (see http://www.ietf.org/html.charters/snmpv3-charter.html).

# SNMP on Linux

SNMP for Linux was previously supported by two packages: ucd-snmp and the CMU SNMP project. Although both of these packages are still available on the Internet, SNMP development for Linux has moved to the NET-SNMP package.

# NET-SNMP

The NET-SNMP package available at http://net-snmp.sourceforge.net/ is the SNMP package known earlier as the ucd-snmp package. The current distribution, 4.2.1, is still referred to as the ucd-snmp package, but all future distributions will be named using the new name. The NET-SNMP package provides an SNMP agent for Linux, an SNMP library, and SNMP command-line tools for issuing SNMP commands and traps.

In addition to supporting the standard MIB-II, the NET-SNMP agent also directly supports monitoring disk usage, as well as provides support to ensure processes are running. The agent will send a trap to the management station when disk usage becomes low or a particular process has stopped executing. The agent also can make use of scripts to add further capabilities to the trap functionality.

The following section provides a brief overview of the installation of NET-SNMP.

# Installation

To install the NET-SNMP distribution, download the current version of the package as pointed to in the download section of http://net-snmp.sourceforge.net/. At the time of publication of this book, version 4.2.1 is the current version. Place the downloaded distribution in the appropriate place where source files are kept on your Linux system. For this example we use /usr/src/.

The installation should be performed as the root user.