# The atalkd Daemon

The atalkd daemon provides much of the basics of AppleTalk networking, so configuring and running it is the first order of business when you've got a kernel running with DDP support.

# atalkd Configuration

To configure atalkd, you need to edit the /etc/atalk/atalkd.conf file. Configuring atalkd is unusual because, in many cases, the atalkd.conf file can be completely empty and the system will still work! Aside from comment lines that start with pound signs (#), atalkd.conf contains configuration information on a one-line-per-interface basis. Information on each line may include the following:

+   - Ethernet device—This is generally eth0, although if you have more than one Ethernet board, the device may be eth1 or above. If you specify any options at all, the Ethernet device must be the first option on the line. If atalkd.conf is empty, atalkd probes all available interfaces looking for AppleTalk computers.
+   - -seed—If this option is present, you must specify all the additional information. Normally you don't have to use the -seed option because it's used only if you want your Linux computer to serve as a bridge between two AppleTalk networks and as the provider of configuration rules for one of them.
+   - -phase number—This is essentially the revision number of EtherTalk to which Netatalk conforms. The default is 2, but you can set up Phase 1 if you prefer.
+   - -net netrange—You can specify a range of numbers within which your computer will attempt to obtain a network address. You specify netrange as a pair of numbers separated by a hyphen, as in 4000-4100. Legal values range from 1 to 65279. Values higher than this are used in automatic configurations.
+   - -addr address—You can request a specific address using this parameter. address is a two-part number separated by a period (.). The first part is a network number (legal values range from 1 to 65279), and the second part is a node number (1 to 255). Examples of valid addresses include 1.1, 60321.200, and 5.254.

# NOTE

With Phase 2 EtherTalk, the network and node values of Ethernet addresses can both vary on a single network. For instance, you could have a network with computers taking addresses of 60321.200, 3243.78, and 231.231, and all three computers could talk to one another. If your Macintoshes still use Phase 1 EtherTalk or LocalTalk, you might need to give your Linux server the same network number that's used by the Macintoshes.