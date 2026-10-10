# Chapter 19

# Setting Up an FTP Server

File Transfer Protocol (FTP) has been the standard method for sharing files over the Internet for many years. Even with the popularity of the Web, which made document database services such as Gopher and WAIS obsolete, FTP servers are still the most common way to make directories of documents and software available to the public over the Internet.

File-sharing applications, such as NFS and Samba, are excellent tools for sharing files and directories over a private network. For organizations that need to share large numbers of files over public networks, however, FTP server software provides more robust tools for sharing files and protecting your computer systems. Also, FTP client software for accessing FTP servers is available for any type of computer that can access a network.

This chapter describes how to set up and maintain an FTP server using the Very Secure FTP Server package (vsftpd).

Configuring your FTP server to allow users to upload files to your server involves more risk than just allowing downloads. Anyone could upload a malicious file, overwrite other files, or, depending on the configuration, place a file in an undesired location. To help mitigate this risk, you can set your server up in a chrooted environment to limit access to the file system.

Also, keep in mind that authentication information and file transfers are sent in plaintext across the network. If this traffic contains sensitive information, you might want to configure encryption. FTPS (also sometimes called *FTP/SSL*) is FTP over a Secure Sockets Layer connection. Space permits me only to cover a basic installation in this chapter. You can visit `http://chrootssh.sourceforge.net/docs/chrootedftpd.html` for more on setting up FTPS in a chrooted environment.

# IN THIS CHAPTER

+   - Understanding FTP servers
+   - Using the vsFTPd FTP server
+   - Getting more information about FTP servers