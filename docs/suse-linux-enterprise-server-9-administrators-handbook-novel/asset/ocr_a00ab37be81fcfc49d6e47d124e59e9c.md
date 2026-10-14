One of the most common routes for (software) virus “distribution” is via email. Included with SLES 9 are AMaViS (A Mail Virus Scanner, http://amavis.sourceforge.net) and AMaViGate (http://www.nbedv.com) to help you protect your system. The packages are called amavisd-new and amavigate, respectively, on the SLES media and are automatically installed when you install Postfix. Note that AMaViS requires you to have a virus scanner already installed; refer to /usr/share/doc/packages/amavisd-new for more details.

The following are some examples of commercial antivirus solutions that may meet your requirements:

+   - BitDefender for Postfix (http://www.bitdefender.com)
+   - Sophos Anti-Virus for Linux (http://www.sophos.com)
+   - Kaspersky Anti-Virus Business Optimal (http://www.kaspersky.com)
+   - F-Prot Antivirus for Linux (http://www.f-prot.com)

# # File Transfer Services

The File Transfer Protocol (FTP) is probably the most common means of copying files between servers over the Internet. Most web-based download sites use the built-in FTP capabilities of web browsers, and consequently, most server-oriented operating systems usually include an FTP server application as part of the software suite. Linux is no exception. There are a large number of different commercial and free FTP servers available for Linux/Unix. The following are some examples:

+   - NcFTP Server (http://www.ncftp.com/ncftpd); commercial
+   - ProFTPD (http://www.proftpd.org); free, GPL-licensed
+   - Pure-FTPd (http://www.pureftpd.org); free, BSD-licensed
+   - glFTPd (http://www.glftpd.com); free
+   - vsftpd (http://vsftpd.beasts.org); free, GPL-licensed
+   - wu-ftpd (http://www.wu-ftpd.org); free

The Trivial File Transfer Protocol (TFTP) also is often used to supply boot images on the network to facilitate remote booting of diskless workstations. TFTP servers are also used to provide images for network devices (such as routers and switches) to obtain firmware updates. You can save device configuration data to a TFTP server as well. Similar to FTP servers, a number of TFTP