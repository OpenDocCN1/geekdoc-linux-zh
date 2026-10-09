# ## Setting up an FTP Server

If you want to enable other users to download files from a location on your server’s hard disk, and/or to upload files to that location, then one solution is to install an **FTP server**. You can think of an FTP server essentially as an area of disk space that is used for storing files, plus the software and configuration required to allow other users to upload and download files. When users want to upload or download from your FTP server, they use a program called an **FTP client**.

These communications between FTP server and FTP client take place using the **File Transfer Protocol (FTP)**. FTP is a TCP protocol that is designed specifically for the transfer of files over a network, and it’s one of the oldest Internet protocols still in widespread use. The availability of so many different FTP client programs, and the fact that many operating systems come with FTP software pre-installed, are indications of how relevant FTP still is today.

FTP is not considered a secure protocol, because communication between the FTP client and server are unencrypted. Consequently, **Secure FTP (SFTP)** is also becoming popular (and, indeed, is part of the **openssh** package that comes with Red Hat Linux 9), and it’s also possible to configure your FTP server in other ways, for example by forcing users to log in, or by using access control lists (ACLs) to allow different rights to different groups of users.

> *You need to take careful security precautions if you plan to expose your FTP server on the Internet. We’ll talk about how to minimize the security implications of supporting an FTP server in Chapter 12. There’s also information on this subject, and on the FTP protocol in general, at RFCs 959 and 2577 (http://ftp.rfc-editor.org/in-notes/rfc959.txt and http://ftp.rfc-editor.org/in-notes/rfc2577.txt).*

In fact, many FTP servers still allow **anonymous FTP access**, which means that the FTP server allows any user to access its disk space and download its files. Anonymous FTP access is used mostly to enable users to access freely available documents and files via the Internet without access control.

In spite of the security issues, FTP remains popular – it’s fast and easy to use, and it is the Internet standard protocol for file transfer.

# ### FTP Servers in the Red Hat Linux Distribution

There are a number of FTP servers available for Red Hat Linux 9 For example:

+   ❑ **vsftpd** is a simplified FTP server implementation. It is designed to be a very secure FTP server, and can also be configured to allow anonymous access. We’ll explore vsftpd in this section.

+   ❑ **TUX** is a kernel-based, threaded, extremely high performance HTTP server, which also has FTP capabilities. TUX is perhaps the best in terms of performance, but offers less functionality than other FTP server software. TUX is installed by default with Red Hat Linux 9.