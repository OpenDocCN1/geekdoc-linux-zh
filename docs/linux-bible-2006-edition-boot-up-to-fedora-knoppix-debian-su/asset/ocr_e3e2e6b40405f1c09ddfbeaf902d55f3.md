# 706 Part V Running Servers

To enable Web-based CUPS administration, the cupsd daemon listens on port 631 for all network interfaces to your computer based on this entry: Listen *:631.

By turning BrowseRelay (it's off by default), you can allow CUPS information to be passed between two or more networks. The source-address and destination-address can be individual IP addresses or represent network numbers:

```
BrowseRelay source-address destination-address
```

This is a good way to enable users on several connected LANs to discover and use printers on other nearby LANs.

You can allow or deny access to different features of the CUPS server. An access definition for a CUPS printer (created from the Printer Configuration window) may appear as follows:

```
<Location /printers/ns1-hp1>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

Here, printing to the ns1-hp1 printer is allowed for users over the local host (127.0.0.1). No password is needed (AuthType None). To access to the administration tool, CUPS must be configured to prompt for a password (AuthType Basic).

# Starting the CUPS Server

For Linux systems use SystemV-startup scripts (such as Fedora, RHEL, and SUSE), starting and shutting down the CUPS service is pretty easy. Use chkconfig command to turn on CUPS so it starts at each reboot. Run the startup script to have the CUPS service start immediately. Type the following as

```
# chkconfig cupsd on
# /etc/init.d/cups start
```

If the CUPS service was already running, you should restart instead start. Using the restart option is also a good way to reread any configuration options you may have changed in the cupsd.conf file.

Other Linux systems vary in how they start up the CUPS service. For example, in Slackware, you can turn on CUPS printing permanently by simply making the rc.cups script executable and then it it immediately by executing it (the following as root):

```
# chmod 755 /etc/rc.d/rc.cups
# /etc/rc.d/rc.cups start
```