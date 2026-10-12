The RAM Disk Support option allows the kernel to use a portion of your system's memory as a disk capable of storing a file system. Typically, a RAM disk functions only during system startup when the hard drive may not be available yet. The RAM disk is essential if you're booting a SCSI disk and you haven't compiled the SCSI drivers into the kernel.

# Networking options

This set of options (shown in Figure 6-10) deals with networking. How you set these options depends on how you want to use your Red Hat Linux system in a network. Always enable the TCP/IP Networking option because the X Window System uses TCP/IP networking (even if your PC isn't on any network).

Figure 6-10:
Configure the networking options from this configuration window.

![](bbox=[0.22, 0.4, 0.77, 0.72])

Set the Network Packet Filtering (Replaces ipchains) option to Yes if you want to use your Red Hat Linux system as a firewall — an intermediary system that controls information flowing between a local area network (LAN) and the Internet.

# Telephony support

With the right hardware and software, the telephony support options enable you to use the Red Hat Linux system for making phone calls over the Internet (also known as voiceover IP or VoIP). You can choose to build driver modules for telephony support if you have a telephony card, such as the Internet