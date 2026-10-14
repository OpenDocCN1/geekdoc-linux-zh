To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# Hosting an FTP Service

Although most of the time you’ll be a client to FTP sites, you might want to make some files available through FTP. To enable FTP access from other machines, you must enable the FTP service in /etc/inetd.conf. For information on how to enable these services, see the “Network Services” note.) After you enable the service in /etc/inetd.conf, you can use FTP to get to your machine and use your login and password.

To enable an FTP service, you need to ensure that the wu-ftpd package is installed. If you did a standard installation, it was installed.

The FTP service installed by default in Linux is called wu-ftpd. Wu-ftpd was originally developed at the Washington University in St. Louis. This robust FTP server software is used by sites that support thousands of users.

Providing anonymous FTP is enabled by default as your /etc/passwd contains an entry for the FTP user. Users who log in to the system as FTP login are put into the /home/ftp directory. This directory is treated differently by the FTP daemon (the software running the FTP service). As far as anonymous users are concerned, /home/ftp looks like a root file system. Users cannot change directories outside it and only have access to directories within it. The FTP daemon accomplishes this by changing the server’s root for the FTP process to the /home/ftp directory. This directory contains minimum/etc and /bin directories with just enough information and software to allow anonymous users access to the system. You should not modify the contents of the /home/ftp/etc and /home/ftp/bin directories unless you know what you are doing.