the SSH server as an option. The main decision to make is whether to install an authenticated or anonymous server. Unless you have a very trivial setup and no Internet access, it is recommended that an authenticated server is used. Once installed, a user can connect to your server using the IP address, or DNS name using the command line or GUI. If the unsecured version has been installed, the user may be able to traverse across the server and upload and download files to/from many locations.

An FTP server can be set up to restrict the local usernames that can be used. For instance, you should typically stop remote users using the *root, bin, etc* username. This is achieved by putting the list of users in the */etc/ftpusers* file. This simple list of names must also appear in the */etc/passwd* file. The */etc/tftpchroot* file is in a similar format to the */etc/ftpusers* file and contains the list of users whose session root directory needs to be changed. This is usually to the directory listed in the */etc/tftpd.conf* configuration file. This is to ensure that the remote user is put in a safe directory and they cannot traverse into an area where there are sensitive files.

# EXERCISE 9.3: Transferring Files in ASCII or Binary

In this exercise, you will transfer an executable file from a server to a host with a command line *ftp* utility.

+   1. First, connect to the FTP server using *ftp servername*, where *servername* is the name or IP address of the server you wish to connect to.
+   2. When you are prompted for a username and password, enter the valid credentials.
+   3. When the */ftp>* (or similar) prompt is displayed, type *binary*. This will change the transfer mode to binary from ASCII (or text transfer).
+   4. Type *get filename* to retrieve the file you wish.
+   5. The file is now transferred to your computer in the correct format. If you had used the ASCII mode, the file would have been corrupted and unusable. ■

# Squid

Squid is a proxy server and Web caching service. There are a number of uses for it, and they are as follows:

+   - Caching Web lookups for the network
+   - Additional security for Web access
+   - Speeding up a Web server through caching of repeated requests.