# CHAPTER 13 | Testing and Reporting

TABLE 13-6 Virtual machine management commands at the vsh # prompt.

| COMMAND | DESCRIPTION |
| --- | --- |
| list | Lists active domains |
| attach-disk | Supports the inclusion of physical devices, virtual images as drives, and ISO files as CDs/DVDs |
| attach-interface | Connects a virtual machine to network interfaces |
| dominfo | Provides status information on a domain |
| domblstat | Notes read and write information of a hard-drive device on a domain |
| migrate | Moves a domain to a different host |
| reboot | Reboots a currently running domain |
| shutdown | Shuts down a currently running domain |
| start | Starts a currently inactive domain |
| vcpinfo | Lists current CPU information for a domain, including numbers of CPUs |
| vncdisplay | Uses the Virtual Network Computing (VNC) system to open a display |

As of writing, nine of the top 10 network security tools can be configured on Linux. Many are covered elsewhere in this chapter and this book. Wireshark was already covered in Chapter 8. The open top security tools that can be configured on Linux include the following:

+   * Wireshark—Supports analysis of network packets
* Snort—An intrusion detection system (IDS) with modes for packet analysis, logging, and interaction with iptables firewall rules; associated rules are updated on a regular basis
* Netcat—A utility that can read both TCP and UDP packets
* Metasploit Framework—A platform for testing for code to take advantage of known vulnerabilities
* Hping2—A command-line packet analyzer that sends TCP and UDP packets based on the features of the ping command

Take care if you use any of these tools on remote systems. Make sure you have the permission of responsible administrators before applying any of these tools. The warnings associated with the nmap command described earlier may apply.