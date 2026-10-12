/etc/rc5.d). You can check the /var/log/messages file to see if the Arpwatch services started successfully and watch for changes on your network.

# Simple Network Management Protocol (SNMP) server

The Simple Network Management Protocol (SNMP) server lets your Red Hat Linux system listen for SNMP requests from the network. With this server running, other computers using SNMP tools can monitor (based on configuration files you set up on your system) the activities of your computer.

By default, SNMP is turned off. To turn it on, change the kill script (K50snmpd) to a start-up script (S50snmpd). Do this by changing the files in the directories for run levels in which you want the service to run (probably /etc/rc3.d or /etc/rc5.d). SNMP configuration can be quite complex. Start by referring to the snmpd.conf man page (type man snmpd.conf) and going through the tutorial from the UCD-SNMP home page (http://ucd-snmp.ucdavis.edu).

# Information servers

By distributing such information as host names, user account information, and network addresses, an administrator can more easily manage groups of networked computers. Popular types of servers for managing network information include Network Information System (NIS), Dynamic Host Configuration Protocol (DHCP), and Lightweight Directory Access Protocol (LDAP).

# Network Information System servers

Network Information System (NIS) is a software feature that was developed by Sun Microsystems to manage information needed to configure a group of UNIX (and now Linux) computers on a network. Using NIS, a group of computers can share common passwd, groups, hosts, and other configuration files.

By default, NIS services are off. You can turn on NIS services for your Linux computer as either an NIS client (using shared information) or an NIS server (distributing shared information). NIS client computers need to start the /etc/init.d/ypbind script and identify the NIS servers in the /etc/yp.conf file.

If you want to use your Red Hat Linux system as an NIS server, you need to gather up the configuration files you need to share, then start the /etc/init.d/ypserv script. The script runs the /usr/sbin/ypserv daemon, which takes care of the distribution of information to the NIS client computers.

> **CROSS-REFERENCE:** Chapter 23 describes the NIS client and server software.