The easiest way to detect TFN2000 possibly running on a system is to detect that the network interface is in Promiscuous mode. Although this is as easy as invoking *iconfig*, this important check rarely is done. It is time to do it. This technique is discussed in “Detecting Promiscuous Network Interface Cards” on page 393 and in “Finding Promiscuous Processes” on page 397, which cover ways to detect this problem automatically and alert you, including paging you.

> On Red Hat systems (and possibly some other versions of Linux), the *iconfig* program fails to indicate that a network interface is in Promiscuous mode. The chapters referenced here give more details and reference a program that will detect processes that have an interface in Promiscuous mode, even on Linux systems with this bug.

# B.25 Stealth Trojan Horses

**DANGER LEVEL** ☠☠☠☠

More SysAdmins are scanning their own systems now for Trojans that might be listening on particular ports awaiting instructions. The default port numbers for some popular Trojans are well known; the *ports* program discussed in “Turn Off Unneeded Services” on page 80 will recognize some of these and generate an alert. Of course, it is a simple matter for the cracker to alter the port listened on. The *ports* program will help detect this by flagging *any* high numbered port in a listen state because the listen state is for servers. Legitimate servers almost always are on well-known ports and almost always on ones below 1024.

Note that the issue here is an illicit program running on *your system* listening for messages from other systems (or outbound messages from your system). See “Captain, We’re Being Scanned! (Stealth Scans)” on page 570 regarding programs on other systems scanning your system.

The TFN2000 (Tribe Flood Network 2000) Trojan, explained in the previous section, is an example of a Stealth Trojan horse. Normally an Ethernet network card’s hardware is configured to “capture” only packets on the Ethernet with the destination address of the system that the card is in. This greatly reduces the load on the system by having the card not generate an interrupt and force the kernel to process the 80–99 percent of network traffic that is not destined for the local system.