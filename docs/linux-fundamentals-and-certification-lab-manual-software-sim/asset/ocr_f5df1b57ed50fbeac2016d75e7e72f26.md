+   • Hyperlink  A section of text on a Web page that, when selected, retrieves another Web document from the Web server.

Apache HTTP server is a popular Web server, used in more than 60 percent of Web sites on the Internet, and can be used by Linux and other operating systems. The Apache HTTP Server Project develops and maintains the open-source HTTP server for most operating systems.

# NOTE

A recent survey of over 44 million Web sites conducted by news.netcraft.com determined that Apache HTTP server has over 67% market share with an increasing trend over the last few years. Microsoft IIS has 21% market share with a decreasing trend since February 2002, and all other HTTP servers have less than 3% market share with decreasing trends.

A Web server can be run on almost any size machine. The level of service determines what size machine to use. If you are running a personal Web server you can manage the content on a personal desktop machine with access to the Internet or intranet. But if you are managing a Web server for a corporation with hundreds or thousands of pages you will need a larger server. Large Web servers often are run on multiple machines to provide high availability. The software requires little in the way of resources, but with larger sites, the increased number of users requires more RAM and faster network connections.

# File Servers

A file server is a computer that controls a central repository of data that can be downloaded or manipulated in some manner by a client. A file server is often used to provide additional disk space for individual users. By using a central location to store files, administrators can easily back up user content without having to manage multiple machines.

A popular file server application for Linux is Samba, an open-source/free software suite that provides seamless file and print services to SMB/CIFS clients. Server Message Block (SMB) is a protocol that provides file and printer sharing between computers. Common Internet File System (CIFS) is an Internet file system protocol based on Microsoft’s SMB.

With Samba a server can provide file and print services to Windows-based clients using TCP/IP as the underlying transport protocol. It allows you to use Linux and Windows machines together without requiring a separate Windows server.

Another file sharing system, Network File System (NFS), was developed by Sun Microsystems as a standard for sharing files over a network. This service allows integrating a file system into a remote system where it is used seamlessly with other local file systems. NFS is available by every Unix and Linux system.

A file server’s size is determined by its usage. Again, if you have one user with limited needs a personal desktop will suffice; but if you have hundreds of users you will need a larger server and a much larger data store.

# Messaging Servers

A messaging server provides access to e-mail by clients. It quickly delivers e-mail with content that could include embedded sound, graphics, video files, HTML forms, Java applets, and desktop applications. Message servers use several protocols, as shown in Figure 2–2. Some of the protocols are Simple Mail Transfer Protocol (SMTP), Internet Message Access Protocol version 4 (IMAP4), Post Office Protocol 3 (POP3), and Hyper Text Transfer Protocol (HTTP).

SMTP is used to communicate client to server and server to server and uses port 25 to communicate. Information about SMTP can be found in RFC-821. RFCs, requests for comments, are managed by the Internet Engineering Task Force (IETF) and can be found at http://www.ietf.org.