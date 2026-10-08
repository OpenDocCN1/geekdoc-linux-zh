# Chapter 4. The sysconfig Directory

+   - VNCSERVERS=<value>, where <value> is set to like "l:fred", to indicate that a VNC server should be set for user display on :1. User must have set a VNC password using vncpasswd before attempting to connect to the VNC server.
- When using a VNC server, communication with it is unencrypted, and so it should not be used on an untrusted network. For specific instructions concerning the use of SSH to secure the VNC communication, please read the information found at http://www.uk.research.ac.uk/vnhnc. To find out more about SSH, see Chapter 18 SSH Protocol or Red Hat Linux Customization Guide.

 4.1.3. /etc/sysconfig/xinetd
Theetc/sysconfig/xinetd file is used to pass arguments to the xinetd daemon at boot. The xinetd daemon starts providing Internet services when a request is received to the port for that service is received. For more information about the parameters available for this file, see the xinetd man page. For more information see Section 15.3 xinetd.

 4.2. Directories in the /etc/sysconfig/ Directory
The directories are normally found in /etc/sysconfig/.

+   - apm-scripts/ — This directory contains the Red APM suspend/resume script. Do not edit the files directly. If customization is necessary, create a file called /etc/sysconfig/apm-scripts/apmcontinue and it will be called at the end of the script. It is also possible to control the script by editing /etc/sysconfig/apmdd.
- cbq/ — This directory contains the configuration files needed to do Class Queuing for bandwidth management on network interfaces.
- networking/ — This directory is used by the Network Administration Tool (redhat-config-network), and its contents should not be edited manually. For more information about configuring network interfaces using the Network Administration Tool, see the chapter Network Configuration in the Red Hat Linux Customization Guide.
- network-scripts/ — This directory contains the following network-related configuration files:
- Network configuration files for each configured network interface, such as ifcfg-eth0 for the eth0 Ethernet interface.
- Scripts used to bring up and down network interfaces, such as ifup and ifdown.
- Scripts used to bring up and down ISDN interfaces, such as ifup-isdn and ifdown-isdn.
- Various shared network functions which should not be edited directly.
For more information on the network-scripts directory, see Chapter 8 Network Interfaces.
- rhn/ — This directory contains the configuration files and GPG keys for the Red Hat Network. No files in this directory should be edited by hand. For more information on the Red Hat Network, see the Red Hat website at the following URL: https://rhn.redhat.com.

#  4.3. Additional Resources

This chapter is only intended as an introduction to the files in /etc/sysconfig/ directory. The following sources contain more comprehensive information.