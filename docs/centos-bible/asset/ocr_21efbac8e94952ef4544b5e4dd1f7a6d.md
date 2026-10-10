# Setting Up Printers and Printing

TIP If you are receiving failure messages, make sure that the computer to which you are printing is accessible. For the previous example, you could type smbclient -L NS1 -U jwilson. Type the password (my9password, in this case). If you get a positive name-query response after you enter a password, you should see a list of shared printers and files from that server. Check the names, and try printing again.

# Adding a JetDirect Printer

A JetDirect printer (AppSocket/HP JetDirect) is one that is connected directly to your Ethernet network via a JetDirect device. You typically use port 9100 to print to a JetDirect printer, although additional interfaces may use ports 9101, 9102, and so on. To use a JetDirect printer from CentOS, enter the following information:

+   Host — Enter the name of the JetDirect printer.

+   Port Number — Enter the port number (typically 9100) to identify the interface to the JetDirect printer.

# Using Web-Based CUPS Administration

The Printer Configuration window effectively hides the underlying CUPS facility. There may be times, however, when you want to work directly with the tools and configuration files that come with CUPS. The following sections describe how to use these special CUPS features.

> CAUTION Plaintext configuration files are at the base of the CUPS printing facility. When different tools, such as the CUPS Web-based interface and the Printer Configuration window, manipulate the same config files, those files can become unusable by the other tool. When possible, you should use the system config printer (Printer Configuration window) to work with printers in CentOS. You will see warnings to this effect if you start to use the CUPS interface.

Although the preferred way to configure CUPS printing in CentOS is with the Printer Configuration window, CUPS offers its own Web-based administrative tool.

If CUPS is already running on your computer, you can immediately use CUPS Web-based administration from your Web browser. If CUPS is not running yet, refer to the following section describing the cupsd daemon for information on starting it.

CUPS listens on port 631 to provide access to the CUPS Web-based administrative interface. On the local computer, type the following into your Web browser’s location box:

```
`http://localhost:631/admin`
```

A screen similar to the one shown in Figure 16-3 appears.

By default, Web-based CUPS administration is available only from the local host. To access Web-based CUPS administration from another computer, you must change the /admin section