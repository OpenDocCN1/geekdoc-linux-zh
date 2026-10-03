NOTE
This installation is for a Sun system.
To begin the installation on an Intel-based PC, insert the Device Configuration Assistant floppy, and boot to the floppy disk. You'll be instructed to install the Solaris media after the devices are configured.

# STEP BY STEP

# 3.1 Shutting Down and Starting a Solaris 8 Installation

+   1. Become root.
2. Issue the shutdown command. This command brings the system to a single-user state by halting the window system and leaving you with a single root prompt on the console. It takes about a minute.
3. Issue the halt command. This command puts you into the PROM. You'll know you're in the PROM when you receive either an ok or a > prompt.
4. Put the Solaris 8 Software CD 1 of 2 into the CD player and boot from the CD.
5. At the ok prompt, type boot cdrom.

The system boots from the CD-ROM. The process is slow, but the flashing light on the CD player shows activity. Eventually, the system starts the GUI and presents you with the Solaris Installation program. Follow the instructions onscreen to install the software on the system. Have the following information available because the installation tool will ask for it:

+   ♦ Hostname. The name for the system. Hostnames should be short, easy to spell, and lowercase; and they should have no more than 64 characters. If the system is on a network, the hostname should be unique.
♦ IP address. This information must come from your site IP coordinator. 192.9.200.1 is one example of an IP address. IP addresses must be unique for every system on your network. For a large site or a site that has a presence on the Internet, you should apply for a unique IP address from the NIC to ensure that no other network shares your address. On workstations, some sites use DHCP, described in Chapter 18, “Name Services,” to automatically set the IP address.