+   1. Become root if you are not already.
+   2. Change your current working directory to that of the anonymous FTP server account. This is normally /home/ftp.
+   3. Issue following commands to create the incoming directory and set its permissions:
+      # mkdir incoming
+      # chmod 333 incoming

Caution should be taken with any site that hosts a writable incoming directory to ensure that illegal activity does not occur. More information on strategies for preventing such activity is given in the “Dealing with Warez D00dz” section of this chapter.

# Alternative FTP Servers

Professional FTP Daemon, otherwise known as ProFTPD, is another popular FTP server that is publicly available. ProFTPD is based on an entirely new code-base, not using legacy code from any existing daemons such as wu-ftpd.

It was written in an attempt to create a highly configurable FTP server offering customization capabilities similar to that of the Apache Web server. ProFTPD is based entirely on free code, and is licensed under the GPL (GNU Public License).

The ProFTPD software package offers several advanced features that are not seen in many other FTP servers. These include the ability to use per-directory .ftpaccess configuration files and the option of using any desirable directory structure for anonymous FTP servers. ProFTPD also has several security advantages over other FTP daemons in that it can run as a non-privileged user to prevent possible root compromises, and the fact that it does not rely on any external software binaries for execution.

To install the ProFTPD software package on your system, you must do the following:

+   1. Download the ProFTPD RPM from the following location:
+      ftp://rhcn.redhat.com/pub/rhcn/RPMS/1386/proftpd-rhcn-1.2.0pre3-1.i386.rpm
+   2. Install the RPM with the following command:
+      # rpm -Uvh proftpd-rhcn-1.2.0pre3-1.i386.rpm
+   3. To install the ProFTPD RPM, you must first remove the wu-ftpd and anonftp packages.
+   4. Edit the ProFTPD configuration file to match the desired FTP server configuration. The ProFTPD configuration file is located in the following directory:
+      /etc/proftpd.conf