
# Chapter 20

# Setting Up an FTP Server

In This Chapter

- Understanding FTP servers
- Using the vsFTPpd FTP server
- Getting more information about FTP servers

File Transfer Protocol (FTP) has been the standard method for sharing files over the Internet for many years. Even with the popularity of the Web, which made document database services such as Gopher and WAIS obsolete, FTP servers are still the most common way to make directories of documents and software available to the public over the Internet.

File-sharing applications, such as NFS and Samba, are excellent tools for sharing files and directories over a private network. For organizations that need to share large numbers of files over public networks, however, FTP software provides more robust tools for sharing files and protecting your computer systems. Also, FTP client software (for accessing FTP servers) is available for any type of computer that can access a network.

This chapter describes how to set up and maintain an FTP server using the Very Secure FTP package (vsFTPpd).

Configuring your FTP server to allow users to upload files to your server involves more risk than just allowing downloads. Anyone could upload a malicious file, overwrite other files, or depending on the configuration, place file in an undesired location. To mitigate this risk, you can set your server in a chrooted environment to limit access to the filesystem.

Also, keep in mind that authentication information and file transfers are still in plain text across the network. If this traffic carries sensitive information, you might want to configure encryption. FTP (also sometimes called FTP/SSL) is FTP over a secure sockets layer connection. Space permits me only to cover a basic installation in this chapter. You can visit http://chrootssh.sourceforge.net/docs/chrootedsftp.html for more on setting up sftp in a chrooted environment.

# Part IV: Fedora RHEL Network and Server Setup

NOTE: In discussing secure file transfer options you may come across both SFTP and FTPS, FTPS is a newer protocol designed by the Internet Engineering Task Force (IETF) and offers more features than traditional FTP, including secure transfers. FTPS is transacted over an encrypted SSL connection, while SFTP is SSH File Transfer Protocol.

## Understanding FTP Servers

The first implementations of FTP date back to 1971, predating the Web by almost two decades. FTP was created at a time when most computing was done on large mainframe computers and minicomputers. The predominant platforms using FTP were UNIX systems.

FTP set out to solve the need to publish documents and software so that people could get them easily from other computer systems. On the FTP server, files were organized in a directory structure. Users could connect to the server over the network (originally Paypal and now the Internet), move up and down the directory structure to find the files they interested them, and download from (possibly upload) to the server. 

Originally, one drawback with FTP servers was when people looked for a file or document on the Internet, they had to know which FTP server had the file they were looking for. Tools such as Gopher and Wiley helped search. With the advent of the Web, however, users can now rely on a variety of search engines and links from Web pages to identify FTP servers that have the files they want. In fact, most modern web browsers have integrated multiple protocols to access content, when you download files by clicking a link from a Web page, you may not even aware that the file is being downloaded from an FTP server.

## Attributes of FTP servers

That FTP was implemented on large, multiuser UNIX systems accounts for most of the design decisions that remain a part of FTP today. FTP servers in Linux draw on FTP features that have resulted from years of testing and experience from other UNIX systems. Some attributes of FTP servers:

- FTP was originally used on multiuser systems, only limited parts of the file system in Fedora and RHEL are devoted to public FTP access. Those who access FTP from a public user (by default, the `anonymous` user) are automatically given an FTP directory (/var/ftp) as their root directory. From there, the `anonymous` user can access only files and directories below that point in the system.

- Access to the FTP server relies on a login process that uses UNIX login names (that is, those user names found in /etc/passwd). Although strangers to the system could log in using `anonymous` as a user name, users with their own accounts on the system could log in with their own names through FTP and likely have access to a greater part of the file system (in particular, their own private files and directories).

- The ftp command and other FTP client programs let you log in and operate from a command interpreter (similar to a very simple shell). Many of the commands that you use from command interpreter are UNIX commands. You change directions with cd, list permissions with ls, change permissions your location with pwd (to name a file). When you find where you want to be, you use the get to download a file or the put to upload one.

As an administrator of an FTP server, it is your responsibility to make sure that you share your files in a way that give people access to the information you want them to have without compromising the security of your system. This means implementing a strong security policy and relentlessly monitoring your system to prevent abuse.

> CROSS-REFERENCE: See Chapter 14 for information on computer security issues.

## FTP user types

Different types of users can log in and use an FTP server. Real users represent the category of users who have login accounts to the Fedora or RHEL system that contains your FTP server (that is, you know them and given them permission for other uses besides FTP). With vsFTPd (described in the following section), you can configure settings for each real user.

As an administrator of an FTP server, it is your responsibility to make sure that you share your files in a way that give people access to the information you want them to have without compromising the security of your system. This means implementing a strong security policy and relentlessly monitoring your system to prevent abuse.

> CROSS-REFERENCE: See Chapter 14 for information on computer security issues.

## Using the FTP Server

The Secure FTP server (vsFTPd) is the recommended FTP software in Fedora and RHEL.
