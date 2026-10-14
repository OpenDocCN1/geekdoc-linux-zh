![](bbox=[0.18, 0.12, 0.75, 0.48])

# Figure 15-10 The IPTraf network traffic analysis program

One of the best packet-sniffing tools is Ethereal, a graphical network traffic analysis tool. Though it's not installed by default on Red Hat Linux or Fedora, you can add it to your system by installing the following two packages from Fedora CD 3: ethereal and ethereal-gnome.

The first of these packages includes documentation; the second includes the actual Ethereal program and setup instructions for the GNOME graphical desktop. If you're running other versions of Linux, packaged binaries are also likely to be available for your system. Visit the Ethereal home page at www.ethereal.com or your favorite Linux download site (such as rpmfind.net or freshmeat.net). To start the program, execute the ethereal command from any graphical command-line window. Figure 15-11 shows the Ethereal window.

![](bbox=[0.13, 0.85, 0.2, 0.92])

The Ethereal packages also include a text-mode version called tethereal.

A special type of security software is called an intrusion detection system (IDS). An IDS watches the network for activity that may indicate that an attacker is looking for a way to enter your server. For example, when a person uses the nmap program to perform a port scan of your server, an intrusion detection program sees that certain network activity is coming from a port scanner, which indicates the presence of an attacker.

A freely available IDS is the Linux Intrusion Detection System (LIDS). LIDS is a challenge to use, but provides a level of protection that's hard to match with most other tools. LIDS adds a module to the Linux kernel that blocks access to resources for all users—including root—except as configured by LIDS. You can download LIDS from www.lids.org. Specific features of LIDS include: