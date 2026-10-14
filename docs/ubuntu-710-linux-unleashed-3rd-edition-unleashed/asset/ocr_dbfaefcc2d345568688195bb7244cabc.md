# CHAPTER 18

# Remote File Serving with FTP

# IN THIS CHAPTER

+   - Choosing an FTP Server
+   - Installing FTP Software
+   - The FTP User
+   - inetd Configuration for wu-ftpd
+   - Configuring the Very Secure FTP Server
+   - Configuring the Wu-FTPd Server
+   - Using Commands in the ftpaccess File to Configure wu-ftpd
+   - Configure FTP Server File-Conversion Actions
+   - Using ftphosts to Allow or Deny FTP Server Connection
+   - Using Commands for Server Administration
+   - Reference

File Transfer Protocol (FTP) was once considered the primary method used to transfer files over a network from computer to computer. FTP is still heavily used today, although many graphical FTP clients now supplement the original text-based interface command. As computers have evolved, so has FTP, and Ubuntu includes many ways with which to use a graphical interface to transfer files over FTP.

This chapter contains an overview of the available FTP software included with Ubuntu, along with some details concerning initial setup, configuration, and use of FTP-specific clients. Ubuntu also includes an FTP server software package named vsftpd, the Very Secure FTP Daemon, and a number of associated programs you can use to serve and transfer files with the FTP protocol.

# Choosing an FTP Server

FTP uses a client/server model. As a client, FTP accesses a server, and as a server, FTP provides access to files or storage. Just about every computer platform available has software written to enable a computer to act as an FTP server, but Ubuntu provides the average user with the capability to do this without paying hefty licensing fees and without regard for client usage limitations.

There are two types of FTP servers and access: anonymous and standard. A standard FTP server requires an account name and password from anyone trying to access the server. Anonymous servers allow anyone to connect to the server to retrieve files. Anonymous servers provide the most flexibility, but they can also present a security risk. Fortunately, as you will read in this chapter, Ubuntu is set