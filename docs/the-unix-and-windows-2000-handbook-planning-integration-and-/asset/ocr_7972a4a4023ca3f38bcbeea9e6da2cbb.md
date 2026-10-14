```
[printers]
comment = All printers in /etc/printcap
path = /var/spool/samba
printable = yes
```

As discussed in Chapter 8, the printing setting does not have to be set to bsd, but can be set to any valid option.

Once you have made these additions, you will need to restart the SAMBA service on your UNIX system. Once you have restarted the service, you should be able to print to any printer defined in the /etc/printcap file from a Windows client.

Refer to Chapter 8 for a more detailed description of the SAMBA options discussed here. You may also want to review the SAMBA documentation for additional information.

# CONNECTING CLIENTS TO SAMBA SHARED PRINTERS

Connecting to SAMBA printers is nearly identical to connecting to Windows 2000 printers. Follow the steps described above to connect to a SAMBA printer, but keep the following in mind:

+   ■ You must install the printer driver locally, since it is not part of the share on SAMBA servers.
+   ■ You must be logged into Windows with a valid UNIX username and password to connect to the printer, or the SAMBA server must be able to authenticate against a Windows 2000 domain controller (this is the configuration we recommended in Chapter 8).
+   ■ You must connect to the printer share with the \\SERVER\share syntax.

Once you have connected to the SAMBA printer, it should behave just as if it were shared from a Windows 2000 server.

# Summary

Though supporting printing is often frustrating, it is necessary. The paperless society predicted by the digital prognosticators has not yet materialized. In this chapter, we discussed the basics of printing for UNIX and Windows 2000.