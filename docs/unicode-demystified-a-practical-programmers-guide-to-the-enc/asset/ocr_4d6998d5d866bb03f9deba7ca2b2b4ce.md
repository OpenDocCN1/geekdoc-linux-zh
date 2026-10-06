# Host Security

Your host must be secure. Simple security steps include preventing remote logins and leaving the /etc/hosts.equiv and individual users ~/.hosts empty (or not having them at all). Complex security steps include installing IPSec for VPNs between hosts. Many common security measures are between these two extremes. A few of these follow. See Table C-1 on page 1421 for URLs.

+   - All potentially tricky to implement and manage, Intrusion Detection Systems (IDS) are an excellent way to keep an eye on the integrity of a device. An IDS can warn of possible attacks at subverting the host on which it runs. The great-grandsaddy of intrusion detection systems is tripwire. This host-based system checks modification times and integrity of files by using strong algorithms (cryptographic checksums and signatures) that can detect the most minor modification. There is also a commercial version of tripwire. Another commercial IDS is DragonSquire. Other free, popular, and flexible IDS include samhain and AIDE. These last two even more features and means of remaining invisible to users than tripwire. Commercial IDS that are popular in enterprise environments include Cisco IDS (formerly NetRanger), Enterasys Dragon, and IISSecure.

+   - The redhat-watch-list mailing list (note the s following in this URL: https://listman.redhat.com/pipermail/redhat-watch-list), can keep you up-to-date on security and bugfix announcements. Go to https://listman.redhat.com/mailman/listinfo/redhat-watch-list to subscribe to this list.

+   - Red Hat Network (RHN) can automatically or semiautomatically keep one or more systems up-to-date (page 936), preventing your system from becoming prey to fixed security bugs.

+   - Complementing host-based intrusion detection systems are network-based intrusion detection systems. These programs monitor the network and nodes and report suspicious occurrences (attack signatures) via user-defined alerts. These signatures can be matches on known worms, overflow attacks against programs, or unauthorized scans of network ports. Such programs as sport, klaxon, and NFR are used in this capacity. Commercial programs, such as DragonCentury, also fill this role.

+   - Provided with Red Hat Linux is PAM, which allows you to set up different methods and levels of authentication in many ways (page 1043).

+   - Process accounting, a good supplement to system security, can provide a continuous record of user actions on your system. See the acton man page for more information.