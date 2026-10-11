# In Depth

Two simple but important services that most new system administrators only skim over when setting up a system are the File Transfer Protocol (FTP) and Telnet. Although certain aspects of these tools work by default with most Linux distributions, you need to know the security measures that are available and the risks that you are taking by allowing particular services to exist on your machines. This chapter discusses the issues involved with using FTP, anonymous FTP, and Telnet.

# FTP Issues

The FTP service is used to upload and download files from a remote machine. Over time, many distributions (including Red Hat) have separated this service into two parts. The first part enables users who have shell accounts on the system to access their own file system space and upload or download information. This use of FTP is generally no more or less secure than a shell login prompt. It is the second common use of FTP that opens the door to a wealth of security concerns. This use is anonymous FTP, which allows anyone to connect to a section of your file system space and upload or download information.

The concerns for system administrators setting up anonymous FTP are numerous. If the file system space and FTP user information for public access are not carefully created with the right permissions and ownerships, unknown guest users can break out of the public space and go into restricted parts of the file system. Another issue concerns people using your FTP upload space to share illegal materials or other items prohibited by your policies with other users.

If you do not intend to allow anyone to use FTP to access a particular machine, be sure to disable this service in /etc/inetd.conf, as discussed in Chapter 9.

# FTP Clients

The default FTP client under Linux—and most Unix flavors—is ftp. This is a relatively straightforward command-line tool. However, other FTP clients are available for those who have specific needs that are not met by ftp, or who simply like to experiment. These clients are listed in Table 15.1, and range from freely available clients designed to work under specific circumstances to complex clients with many features that you can test and purchase.

Many more FTP clients are available today, and more are certain to come. Table 15.1 represents a cross-section of some of the more interesting items. To find more