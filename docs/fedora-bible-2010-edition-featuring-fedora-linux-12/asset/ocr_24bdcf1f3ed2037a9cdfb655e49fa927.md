# # Chapter 19
## Setting Up an FTP Server

# **In This Chapter**

+   *   Understanding FTP servers
+   *   Using the vsFTPd FTP server
+   *   Getting more information about FTP servers

File Transfer Protocol (FTP) has been the standard method for sharing files over the Internet for many years. Even with the popularity of the Web, which made document database services such as Gopher and WAIS obsolete, FTP servers are still the most common way to make directories of documents and software available to the public over the Internet.

File-sharing applications, such as NFS and Samba, are excellent tools for sharing files and directories over a private network. For organizations that need to share large numbers of files over public networks, however, FTP server software provides more robust tools for sharing files and protecting your computer systems. Also, FTP client software (for accessing FTP servers) is available for any type of computer that can access a network.

This chapter describes how to set up and maintain an FTP server using the Very Secure FTP Daemon package (vsFTPd).

Configuring your FTP server to allow users to upload files to your server involves more risk than just allowing downloads. Anyone could upload a malicious file, overwrite other files, or depending on the configuration, place a file in an undesired location. To help mitigate this risk, you can set up your server in a chrooted environment to limit access to the filesystem or allow only read-only access to anonymous users.

Also, keep in mind that authentication information and file transfers are sent in plain text across the network. If this traffic contains sensitive information, you might want to configure encryption. FTPS (also sometimes called FTP/SSL) is the use of the File Transfer Protocol (FTP) over a Secure Sockets Layer (SSL) connection.

> **NOTE:** In discussing secure file transfer options, you may come across both SFTP and FTPS. FTPS is a newer protocol designed by the Internet Engineering Task Force (IETF) and offers more features than traditional FTP, including secure transfers. FTPS is FTP transacted over an encrypted SSL connection, while SFTP is File Transfer Protocol over Secure Shell (SSH).