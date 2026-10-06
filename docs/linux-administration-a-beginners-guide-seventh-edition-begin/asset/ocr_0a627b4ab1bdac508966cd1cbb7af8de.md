# CHAPTER 21 Voice over Internet Protocol (VoIP) 555

> **TIP** Asterisk can be fussy about its modules. To avoid the wrath of this fussiness, it's for newcomers to err on the side of being overly generous by autoloading all the modules in the modules directory.
As you get more familiar with Asterisk, you can then use the noload directive to instruct Asterisk not to load unneeded/unnecessary modules.

# Asterisk Network, Port, and Firewall Requirements

VoIP relies on your network being optimized for connectivity and good sound quality. Most of the sound quality that you will experience with the Asterisk system will be network related. If it is at all possible, VoIP-related traffic on the network should be segmented away from other day-to-day network traffic. This can be done through the use of a virtual area network (VLAN) and/or through the use of dedicated networking equipment. All relevant infrastructure equipment should be optimized to prioritize VoIP.

This section assumes that your Linux server has some default firewall rules in place to protect the system. To proceed with the Asterisk setup and make sure the relevant Asterisk components are reachable on the network, we need to ensure that the firewall subsystem on the server allows access to the necessary ports required by the Asterisk system to be functional. Please refer to the Linux firewall configuration primer in Chapter 13 if you need to know more about allowing port access.

Table 21-7 summarizes some default ports required by Asterisk. If needed, the ports can be changed in the various configuration files specific to the protocols and applications.

| Protocol | Port Number | Transport |
| SIP | 5060/5061 | TCP/UDP |
| RTP | 10000 to 20000 | UDP |
| IAX2 | 4569 | UDP |
| MGCP | 2727 | UDP |
| SCCP | 2000 | TCP |
| Asterisk Manager Interface (AMI) | 5038 | TCP |

**Table 21-7** List of Common VoIP Protocol Port Numbers