# Big Pond Cable Linux Installation Notes. V 1.1 (12/03/98)

> **NOTE**  
> Change Note 1.1$^{12}$ /3/98 – Corrected spelling of *dhcpd* and *rrdhcpd*

Linux is not officially supported by Big Pond Cable. However, the TMM cable infrastructure does allow Linux to be used – with the appropriate login client. The following installation notes should allow you to install the Linux software without too many difficulties.

The full client distribution of rrclientd was obtained from ftp://ftp.vortech.net/pub/rllinux/rrclientd-1.3.tar.gz

I am running Red Hat version 5 of Linux, but the documentation indicates that it will work with other releases.

Note there is also more information in the rrclientd release than is documented here.

Here are the installation procedures:

+   1. Copy the distribution file `rrclientd-1.3.tar.gz` to your Linux PC.
+   2. Login as root for all of the following.
+   3. Expand the distribution (with gunzip) and then untar it.
+   4. In directory `rrclientd-1.3/bin` you will find all the executables that you need: fetchmail (not used), kdestroy, kinit, rdte, rrclientd, rrdhcpd, and rpasswd.
+   5. Rename `/sbin/dhcpd` to `/sbin/dhcpd.orig`. Copy and rename `rrdhcpd` to `/sbin/dhcpd`.
+   6. Copy kdestroy, kinit, rdte, rrclientd, rrdhcpd, and rpasswd to `/usr/local/bin`.
+   7. Set up your Ethernet card to use DHCP and restart the system. If the DHCP configuration is OK, an IP address will be assigned, with the details being placed in `/etc/dhcp/hostinfo-eth0` and `/etc/dhpc/resolv.conf`.