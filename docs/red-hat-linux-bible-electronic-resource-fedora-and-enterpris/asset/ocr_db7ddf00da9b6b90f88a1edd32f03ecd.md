As an administrator of an FTP server, it is your responsibility to make sure that you share your files in a way that gives people access to the information that you want them to have without compromising the security of your system. This means implementing a strong security policy and relentlessly monitoring the system to prevent abuse.

> **CROSS-REFERENCE:** See Chapter 14 for information on computer security issues.

# ## FTP user types

Several different types of users can log in to and use an FTP server. *Real users* represent the category of users who have login accounts to the Red Hat Linux system that contains your FTP server (that is, you know them and have given them permission for other uses besides FTP). A guest user is similar to a real user account, except that guest user access to the computer’s file system is more restricted. The user name *anonymous* is the most common for providing public access. Procedures for setting up these different kinds of users for each of the two FTP servers described here are outlined later in this chapter.

At this point, you must decide if you want to run the vsFTpd server on your Red Hat Linux system or download WU-FTPD (wu-ftpd package) and install it instead. The one you choose will, by default, take over the full functions of FTP service on your computer.

# ## Using the Very Secure FTP Server (vsFTPd)

The Very Secure FTP Server (vsFTPd) is the only FTP server software included in the Red Hat Linux distribution. Although it hasn’t been around as long as WU-FTPD, vsFTPd is becoming the FTP server of choice for sites that need to support thousands of concurrent downloads. It was also designed to secure your systems against most common attacks.

Red Hat, Inc. itself uses vsFTPd on its own FTP servers (ftp.redhat.com). Other organizations in the Linux/GNU world have also made the switch to vsFTPd, including Debian Linux (ftp.debian.org) and the GNU Project (ftp.gnu.org).

Besides security and scalability, vsFTPd was designed for simplicity. Therefore, fewer options exist for configuring vsFTPd than you find in WU-FTPD, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with vsFTPd, or using it to replace WU-FTPD, is fairly straightforward.

# ### Quick-starting vsFTPd

By enabling the vsFTPd service, you can almost instantly have an FTP service running with the default values (set in the `/etc/vsftpd/vsftpd.conf` file). The following is a quick procedure for getting your vsFTPd server up and running.