# FTP Clients

The Internet is a network of computers around the world you can access with an Internet address and a set of Internet tools. Many computers on the Internet are configured to operate as servers, providing information to anyone who requests it. The information is contained in files you can access and copy. Each server, often referred to as a site, has its own Internet address by which it can be located. Linux provides a set of Internet tools you can use to access sites on the Internet, and then locate and download information from them. These tools are known as clients. A client application, such as an FTP or a Web client, can communicate with a corresponding server application running on a remote system. An FTP client can communicate with an FTP server program on another system. The server lets the client access certain specified resources on its system and lets an FTP client transfer certain files. Several popular FTP clients are shown in Table 14-4.

The primary tools for accessing Internet sites are FTP clients and Web browsers. With FTP clients, you can connect to a corresponding FTP site and download files from it. FTP clients are commonly used to download software from FTP sites that operate as software repositories. Most Linux software applications can be downloaded to your Linux system from such sites. A distribution site like ftp.redhat.com is an example of one such FTP site, holding an extensive set of packaged Linux applications you can download using an FTP client and then easily install on your system. In the last few years, Web browsers have become the primary tool for accessing information on the Internet. Most of the tasks you perform on the Internet can be done easily with a Web browser. You only need to use an FTP client to download or upload files from or to a specific FTP site.

Other Internet tools are also available for your use, such as telnet and IRC clients. The telnet protocol enables you to log into an account directly on another system. IRC clients set up chat rooms through which you can communicate with other users over the Internet. Telnet and IRC clients are discussed in Chapter 15.

# Network File Transfer: FTP

You can use File Transfer Protocol (FTP) clients to transfer extremely large files directly from one site to another. FTP can handle both text and binary files. This is one of the TCP/IP protocols, and it operates on systems connected to networks that use the TCP/IP protocols, such as the Internet. FTP performs a remote login to another account on another system connected to you on a network. Once logged into that other system, you can transfer files to and from it. To log in, you need to know the login name and password for the account on the remote system. For example, if you have accounts at two different sites on the Internet, you can use FTP to transfer files from one to the other. Many sites on the Internet allow public access using FTP, however. Such sites serve as depositories for large files anyone can access and download. These sites are often referred to as FTP sites, and in many cases, their Internet address begins with the word ftp, such as ftp.gnome.org or ftp.redhat.com. Others begin with other names, such as metalab.unc.edu. These public sites allow anonymous FTP login from any user. For the login name, you use the word "anonymous," and for the password you use your Internet address. You can then transfer files from that site to your own system.

Table 14-4: Linux FTP Clients

| FTP Clients | Description |
|---|---|
| Konqueror | K Desktop file manager |
| Nautilus | GNOME file manager |
| gFTP | GNOME FTP client |
| NcFTP | Screen-based FTP client |
| ftp | Command line FTP client |

You can perform FTP operations using any one of a number of FTP client programs. For Linux systems, you can choose from several FTP clients. Many now operate using GUI interfaces such as GNOME. Some, such as Mozilla, have limited capabilities, whereas others, such as NcFTP, include an extensive set of