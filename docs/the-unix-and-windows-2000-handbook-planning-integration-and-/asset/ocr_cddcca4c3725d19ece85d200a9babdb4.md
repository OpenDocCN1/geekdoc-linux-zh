# Internet Information Server 5.0

Microsoft’s Internet Information Server (IIS) has quickly become a popular Web server platform. IIS 5.0 builds on previous releases of Internet Information Server with new features and capabilities. IIS 5.0 is integrated into Windows 2000 Server and can be installed during the initial system setup or afterward using the Add/Remove Programs Control Panel applet. IIS 5.0 provides the following key features:

+   - World Wide Web (WWW) services.
+   - File Transfer Protocol (FTP) services.
+   - News (NNTP) services.
+   - Mail (SMTP) services.

As you can see, IIS 5.0 is much more than just a Web server. In this chapter, we will describe the steps necessary to install a basic IIS 5.0 system, the basic configuration of default WWW services, and the basic configuration of default FTP services. While there is much more to IIS than what this chapter will describe, we cannot possibly cover everything here. For advanced configuration options and features, you should consult the IIS 5.0 documentation or the Internet Information Server Resource Kit.

# Installing IIS 5.0

You can install IIS 5.0 during the initial setup of Windows 2000 Server, or afterward using the Add/Remove Programs Control Panel applet. In both cases, you must select which IIS options you intend to install. If you are using the Add/Remove Programs Control Panel applet, you should select the Add/Remove Windows Components option to select the IIS options you wish to install. The options selection screen for IIS is shown in Figure 16.2.

For the basic IIS installation we will discuss in this chapter, we suggest you select the following IIS components:

+   - Common Files
+   - Documentation
+   - File Transfer Protocol (FTP) Server
+   - FrontPage 2000 Server Extensions
+   - Internet Information Services Snap-In
+   - Internet Services Manager (HTML)
+   - World Wide Web Server

Once you have completed copying files, IIS 5.0 will be ready to begin processing WWW and FTP requests. By default, IIS 5.0 uses C:\InetPub