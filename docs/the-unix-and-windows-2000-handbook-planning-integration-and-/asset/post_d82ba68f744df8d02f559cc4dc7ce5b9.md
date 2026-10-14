
Installation of Apache as a Windows 2000 service is accomplished with the -i option. The following command will add the Apache Web Server as service apache on Windows 2000:

```
E:\program files\Apache Group\Apache>apache -i
```

Renaming the service to Apache Web Server requires two steps. First, remove the apache service with:

```
E:\program files\Apache Group\Apache>apache -u
```

Next, install the service with its new name:

```
E:\program files\Apache Group\Apache>apache -i -n "Apache Web Server"
```

To specify a configuration file, enter the following:

```
E:\program files\Apache Group\Apache>apache -i -n "Apache Web Server" -f "myweb\conf\web.conf"
```

Once installed, the service can be manipulated with the Windows 2000 Control Panel's Administrative Services->Services interface.

Running Apache from the command line can be as simple as typing in Apache. Once Apache is running in a console window, you can stop it two different ways. The ungraceful way is to execute a <CTRL>-<C> in the console window. This will stop the Apache server and kill all requests currently being processed. To shut down gracefully, which will complete requests currently running, open a different console window and execute:

```
apache -k shutdown
```

Command-line options supported under Windows 2000 are included in Tables 16.2 and 16.7:

**Table 16.7 Windows 2000 Command-Line Options**

| Option | Result |
|--------|--------|
| -n name | Sets service name and uses it |
| -k shutdown | Tells running Apache to shut down |
| -k restart | Tells running Apache to do a graceful restart |
| -k start | Tells Apache to start |
| -i | Installs an Apache service |
| -u | Uninstalls an Apache service |

## Internet Information Server 5.0

Microsoft’s Internet Information Server (IIS) has quickly become a popular Web server platform. IIS 5.0 builds on previous releases of Internet Information Server with new features and capabilities. IIS 5.0 is integrated into Windows 2000 Server and can be installed during the initial system setup or afterward using the Add/Remove Programs Control Panel applet. IIS 5.0 provides the following key features:

- World Wide Web (WWW) services.
- File Transfer Protocol (FTP) services.
- News (NNTP) services.
- Mail (SMTP) services.

As you can see, IIS 5.0 is much more than just a Web server. In this chapter, we will describe the steps necessary to install a basic IIS 5.0 system, the basic configuration of default WWW services, and the basic configuration of default FTP services. While there is much more to IIS than what this chapter will describe, we cannot possibly cover everything here. For advanced configuration options and features, you should consult the IIS 5.0 documentation or the Internet Information Server Resource Kit.

### Installing IIS 5.0

You can install IIS 5.0 during the initial setup of Windows 2000 Server, or afterward using the Add/Remove Programs Control Panel applet. In both cases, you must select which IIS options you intend to install. If you are using the Add/Remove Programs Control Panel applet, you should select the Add/Remove Windows Components option to select the IIS options you wish to install. The options selection screen for IIS is shown in Figure 16.2.

**Figure 16.2** IIS installation options.

![](img/415c89a1ede71e11e5040a0038b6916c_672_0.png)

For the basic IIS installation we will discuss in this chapter, we suggest you select the following IIS components:

- Common Files
- Documentation
- File Transfer Protocol (FTP) Server
- FrontPage 2000 Server Extensions
- Internet Information Services Snap-In
- Internet Services Manager (HTML)
- World Wide Web Server

Once you have completed copying files, IIS 5.0 will be ready to begin processing WWW and FTP requests. By default, IIS 5.0 uses C:\InetPub for WWW and FTP document storage. Table 16.8 describes the default locations for document storage.

You have the ability to change the location of the default folders and/or to create virtual links to folders stored on other local hard drives. For our purposes, however, we will utilize the default settings. The next sections will describe the basic configuration options for WWW and FTP services.

### WWW Services

IIS 5.0 provides basic and advanced Web server functions such as Active Server Pages (ASPs) and Common Gateway Interface (CGI) scripting. This section will describe the configuration options available for the default Web site configured when IIS 5.0 is installed. The options are configured using

**Table 16.8 — Default IIS 5.0 Document Locations**

| Document Type | Description |
| --- | --- |
| Web Documents (*.html, *.htm) and Folders | Should be stored in or under `C:\InetPub\wwwroot` |
| FTP Documents and Folders | Should be stored in or under `C:\InetPub\ftproot` |
| Scripts | Should be stored in or under `C:\InetPub\scripts` |
