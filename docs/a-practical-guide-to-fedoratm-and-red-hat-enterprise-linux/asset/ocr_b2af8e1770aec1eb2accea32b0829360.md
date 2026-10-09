By default, SELinux will not allow you to share your home directory. Use `system-config-selinux` (page 475) to activate the `samba_enable_home_dirs` Boolean if you want to allow sharing. Any Windows or Mac user can access this share, which can be used to exchange files between users and among Linux, Mac, and Windows systems.

# # INTRODUCTION TO CACTI

Cacti (cacti.net) is a network monitoring tool that graphs system and network information over time (*time-series data*) and provides a comprehensive Web interface for browsing and examining the ongoing performance of the devices on a network.

For example, Cacti can monitor the network traffic passing through the network ports on local servers and the switch and router ports on the local network. Cacti graphs provide information on traffic levels on the various parts of the network. When the network is slow, for example, you can refer to the historical graphs and see if anything out of the ordinary has occurred. In addition to network traffic levels, Cacti can collect data on CPU usage, disk space usage, page views on a Web server, and almost any other data points available on the local network.

Cacti collects baseline (typical) data over time. You can use that information to gain insight into the ongoing behavior of a system and network, and to help resolve problems. The information can even predict what might happen in the future (e.g., when a disk is likely to become full).

Cacti periodically polls devices on a network for the data it needs, and stores the data in RRD files for use with RRDtool (round-robin database tool; oss.oetiker.ch/rrdtool). The Cacti Web interface allows you to browse a list of devices and graphs and see visual representations of device activity over time.

Cacti builds on the lessons learned from tools such as MRTG (oss.oetiker.ch/mrtg; page 975) and Cricket (sourceforge.net/projects/cricket). Each of these tools has the following characteristics:

+   * Periodically polls tracked devices for data. The tool most commonly used to collect this data is SNMP (Simple Network Management Protocol; www.net-snmp.org).
+   
+   * Stores the data in an RRD file.
+   
+   * Has a Web interface that allows you to examine graphs generated from the stored data. These graphs typically display daily, weekly, monthly, and yearly information.

Cacti’s configuration is performed through its Web interface, whereas MRTG and Cricket are configured by editing text files.

RRD files and RRDtool are the key to much of Cacti’s functionality. The Cacti Web site describes Cacti as “the complete RRDtool-based graphing solution.” RRD files store time-series data efficiently and, through the use of aggregation functions, make