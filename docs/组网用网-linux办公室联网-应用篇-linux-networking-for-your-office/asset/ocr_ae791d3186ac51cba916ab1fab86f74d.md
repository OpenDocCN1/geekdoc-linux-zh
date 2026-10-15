# Configuring Dial-on-Demand Services

Assuming that you’ve compiled an appropriate kernel, you must configure diald to work for you. The first step is to install the package. It’s not part of the usual Red Hat Linux 6.0 stable of programs, but you’ll find a diald RPM file on the CD-ROM that accompanies this book, in the sams-extras/ppp directory. Install it as you would any RPM, using the rpm utility or a GUI tool such as gnorpm.

> Note
> diald has been changing rapidly recently, in part because of changes in the Linux kernel from 2.0 to 2.2. The version of diald included on the CD-ROM might be outdated by the time you read this book, so you might want to look for an updated file from the diald home page, at http://diald.unix.ch. If you obtain such a file, however, be aware that it might not contain the same configuration files that come with the RPM on this book’s CD-ROM. You might therefore want to install this RPM just to get the configuration files described here, and then upgrade the package.

Before proceeding further, check that you’ve configured DNS properly, as described earlier in this chapter (p. 198). Without DNS services, you need to specify an IP address, rather than a more reasonable host name, for every outside connection.

After you’ve installed the diald package, you need to edit two configuration files:

+   - /etc/diald.conf—Many of the options in this file are identical to those in the standard dialup script ppp-on, and their meanings should be obvious, such as the speed (115200) and device (/dev/modem). Change any of these that you need to change. If you’re using either the remote or the local IP address on your local network, you should change the addresses in this file to unused addresses on a private (192.168.x.x) network. What addresses you use is irrelevant, as long as they’re unused by any computer. One line you almost certainly have to change is the ISP username, which resides on a line reading pppd-name /errie in the default file. You must change ernie to your ISP username, as recorded in the pap-secrets or chap-secrets file.

+   - /etc/ppp/diald-dialer—This file is a slight modification of the ppp-on-dialer file presented earlier in this chapter. You should make the same changes to diald-dialer that you made to ppp-on-dialer. In addition, you must change the telephone number to be called (5551234 in the sample file) to one that’s appropriate for your ISP.