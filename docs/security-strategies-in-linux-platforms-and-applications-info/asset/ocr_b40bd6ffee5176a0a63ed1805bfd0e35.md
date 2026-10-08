# CHAPTER 1 | Security Threats to Linux

# Definitions Phase

The definitions phase start with a Visibility Audit module. This module is focused on clients, servers, routers, and more. If it specifies the systems to be tested. This module is split into three areas:

+   - Network surveying—This defines the perimeter of the network, checks DNS databases, reviews broadcasts, routing protocols, Internet Control Message Protocol (ICMP) routing and responses, Simple Network Management Protocol (SNMP) names, certain parts of the Transmission Control Protocol (TCP/IP) suite, and more.

+   - Enumeration—Enumeration examines webs, e-mail headers, network responses, and more to measure how the network is seen internally and externally.

+   - Identification—This matches the characteristics of a network with responses from system and service identification tools.

The Access Verification module includes the full range of access requests, from logins to packet-service banners to responses to known Trojan services. This module is divided into three areas:

+   - Access—Access audits relate to connection protocols, Internet Protocol Security (IPSec), along with attempted connections through the Transmission Control Protocol (TCP), User Datagram Protocol (UDP), and ICMP protocols.

+   - Services—Services audits relate to open TCP/IP ports, virtual Web site configuration. Voice over IP (VoIP) communication, and more.

+   - Authentication—These audits list all methods that provide some level of access, including potentially cracked services that may not be locked down.

The Trust Verification module relates to services or systems that allow any form of user without credentials. This module is divided into three areas:

+   - Spoofing—These audits check whether a network is susceptible to spoofed addresses, as those from within a local network. It also checks for possible DNS cache poisoning.

+   - Phishing—These audits look for external copies of your Web site, domain records for similar names, and verifies control of mail targets.

+   - Resource abuse—These audits review for how a cracker can get into your system, including any variances between multiple servers with the same functionality.

The Controls Verification module is designed to measure how your security efforts make a difference. This module is divided into four areas:

+   - Nonrepudiation—In this context, nonrepudiation is a measure of integrity for issues such as login access or system verification.

+   - Confidentiality—In this context, confidentiality reviews options for secure encrypted communication. Related audits may verify the extent and availability of protected communication.