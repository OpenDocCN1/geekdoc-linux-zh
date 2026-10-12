
## 14. When you are finished configuring the options, be sure to submit your changes.

![](img/b22364e57409c2481ba806e4e6b9309c_784_0.png)

At this point, you can allow users to join the list. Encourage them to explore and set their own user preferences.

If you encounter problems configuring mailman, refer to the INSTALL.REDHAT and README files in the `/usr/share/doc/mailman-*` directory.

### Summary

Fedora includes a full range of tools for configuring and managing mail servers. For mail transfer agents, Fedora includes the Sendmail and Postfix software packages. Both are considered to be excellent, professional quality mail servers.

To allow users to access their mailboxes from the server, Fedora includes the dovecot and cyrus-imapd packages. Those packages implement POP3 and IMAP protocols to allow e-mail to be downloaded or manipulated on the server. You can also configure SquirrelMail to allow users to access their mail through a Web-based interface.

To set up mailing lists in Fedora, you can use the mailman package. Besides including some very flexible configuration tools, mailman also provides simple Web-based access to mailing list preferences and archives.

## Chapter 20
Setting Up an FTP Server

### In This Chapter

- Understanding FTP servers
- Using the vsFTPd FTP server
- Getting more information about FTP servers

File Transfer Protocol (FTP) has been the standard method for sharing files over the Internet for many years. Even with the popularity of the Web, which made document database services such as Gopher and WAIS almost obsolete, FTP servers are still the most common way to make directories of documents and software available to the public over the Internet.

File-sharing applications, such as NFS and Samba, are excellent tools for sharing files and directories over a private network. For organizations that need to share large numbers of files over public networks, however, FTP server software provides more robust tools for sharing files and protecting your computer systems. Also, FTP client software (for accessing FTP servers) is available for any type of computer that can access a network.

This chapter describes how to set up and maintain an FTP server using the Very Secure FTP Server package (vsFTPd).

> **CAUTION:** Configuring your FTP server to share private files or to allow users to upload files to your server involves more risks than just allowing downloads. See the end of this chapter for references to documents from CERT that provide FTP security tips.

## Understanding FTP Servers

The first implementations of FTP date back to 1971, predating the Web by almost two decades. FTP was created at a time when most computing was done on large mainframe computers and minicomputers. The predominant platforms using FTP were UNIX systems.

FTP set out to solve the need to publish documents and software so that people could get them easily from other computer systems. On the FTP server, files were organized in a directory structure; users could connect to the server over the network (usually the Internet), move up and down the directory structure to find the files that interested them, and download files from (and possibly upload files to) the server.

Originally, one drawback with FTP servers was that when people looked for a file or a document on the Internet, they had to know which FTP server held the file they were looking for. Tools such as Gopher and WAIS helped in searches. With the advent of the Web, however, users can now rely on a variety of search engines and links from Web pages to help identify FTP servers that have the files they want. In fact, when you download files by clicking a link from a Web page, you may not even be aware that the file is being downloaded from an FTP server.

## Attributes of FTP servers

That FTP was implemented on large, multiuser UNIX systems accounts for many of the design decisions that remain a part of FTP today. FTP servers in Linux draw on FTP features that have resulted from years of testing and experience gained from other UNIX versions of FTP. Some attributes of FTP servers follow:

- Because FTP was originally used on multiuser systems, only limited parts of the file system in Fedora are devoted to public FTP access. Those who access FTP from a public user account (by default, the anonymous user name) are automatically given an FTP directory (often /var/ftp) as their root directory. From there, the anonymous user can access only files and directories below that point in the file system.
- Access to the FTP server relies on a login process that uses standard UNIX login names (that is, those user names found in /etc/passwd). Although strangers to the system could log in using anonymous as a user name, users with their own accounts on the system could log in with their own user names through FTP and most likely have access to a greater part of the file system (in particular, their own private files and directories).
- The ftp command and other FTP client programs let you log in and then operate from a command interpreter (similar to a very simple shell). Many of the commands that you use from that command interpreter are familiar UNIX commands. You change directories with cd, list files with ls, change permissions with chmod, and check your location with pwd (to name a few). When you find where you want to be, you use the get command to download a file or the put command to upload one.

As an administrator of an FTP server, it is your responsibility to make sure that you share your files in a way that gives people access to the information you want them to have without compromising the security of your system. This means implementing a strong security policy and relentlessly monitoring the system to prevent abuse.

> CROSS-REFERENCE: See Chapter 14 for information on computer security issues.

## FTP user types

Several different types of users can log in to and use an FTP server. Real users represent the category of users who have login accounts to the Fedora system that contains your FTP server (that is, you know them and have given them permission for other uses besides FTP). A guest user is similar to a real user account, except that guest user access to the computer’s file system is more restricted. The user name anonymous is the most common for providing public access.

The vsFTPd server also supports the concept of virtual users. The recommended method for creating virtual users for vsFTPd is to configure PAM (pluggable authentication modules) to point to per-user configuration files. A tutorial to configure vsFTPd to allow virtual users is available at www.debiansec.com/linux/services/ftp.html.

## Using the Very Secure FTP Server

The Very Secure FTP Server (vsFTPd) is the only FTP server software included in the Fedora distribution. vsFTPd is becoming the FTP server of choice for sites that need to support thousands of concurrent downloads. It is also designed to secure your systems against most common attacks.

Red Hat, Inc. itself uses vsFTPd on its own FTP servers (ftp.redhat.com). Other organizations in the Linux/GNU world have also made the switch to vsFTPd, including Debian Linux (ftp.debian.org) and the GNU Project (ftp.gnu.org).

Besides security and scalability, vsFTPd was designed for simplicity. Therefore, fewer options exist for configuring vsFTPd than you find in WU-FTPd, an older FTP server package which is still commonly used, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with vsFTPd, or using it to replace WU-FTPd, is fairly straightforward.

> NOTE: Although vsFTPd is the only full-blown FTP server software in Fedora, the WU-FTPd FTP server software, which was once part of Red Hat Linux, is still available on the Web. At this point, you must decide if you want to run the vsFTPd server on your Fedora system or download WU-FTPd (wu-ftp package) and install it instead. The one you choose will take over the full functions of FTP service on your computer. Descriptions for setting up WU-FTPd from a previous edition of the Red Hat Linux Bible are available online from the companion Web site to this book: www.wiley.com/go/fedora3bible.

## Quick-starting vsFTPd

By enabling the vsFTPd service, you can almost instantly have an FTP service running with the default values (set in the /etc/vsftpd/vsftpd.conf file). The following is a quick procedure for getting your vsFTPd server up and running.

> NOTE: If you have been using the WU-FTPd server on your computer and you are switching to vsFTPd, you need to turn off WU-FTPd. To do that, change disable=no to disable=yes in the /etc/xinetd.d/wu-ftpda file. Then, after you have completed the following procedure, vsFTPd will take control of the default FTP configuration, allowing access to the /var/ftp directory and listening on the default FTP port. Because the two packages have some different default settings, however, you may want to do additional tuning to get vsFTPd to perform as you would like it to.
