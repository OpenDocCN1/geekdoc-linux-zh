# # ProFTPD

ProFTPD does not come with the Red Hat installation CD-ROM, but it is a very popular FTP server, and for that reason it would be a mistake not to discuss it here. It can be obtained from http://proftpd.linux.co.uk/.

The most commonly used server is WU-FTPD. However, the designers of ProFTPD thought that, while WU-FTPD provides excellent performance and is generally a good product, it lacked certain features found in newer Win32 FTP. With this in mind, they set out to create an FTP server for Unix and Linux systems that had the features they felt should be there.

Installing ProFTPD is relatively simple. After you have downloaded the package from a Web site (the one previously mentioned would be a good place to start), you can go to a shell, change to the directory where the package is located, and type in `rpm -install proftpd-{version}.rpm`.

This will place the configuration file for ProFTPD in either `/usr/local/etc/ proftpd.conf` or `/etc/proftpd.conf`. With this and any other software that does not come with Red Hat, your best place to look for more information is the documentation of that vendor. We are listing FTP servers here that are not included in the Red Hat installation to give you an idea of what alternatives are available.