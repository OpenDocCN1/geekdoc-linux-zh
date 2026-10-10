# Logging Options

The following options help define how logging is done on your Samba server:

+   - log file — Defines the location of the Samba smb log file. By default, Samba log files are contained in `/var/log/samba` (with filenames `nmbd.log`, `smbd.log`, and `smb.log`). In this option, the %m is replaced by the name of each host that tries to connect to the local Samba server. So, for example, for a client computer named flashg, the smb log file would be `/var/log/samba/flashg.log`.

+   - max log size — Sets the maximum amount of space, in kilobytes, that the log files can consume. By default, the value is set to 0 (no limit).

# Printing Options

The CUPS options field is used to define options that are passed to the CUPS service. By default, only the raw option is set, which causes printing data to be passed directly to the Samba printer.

# Browse Options

A browse list is a list of computers that are available on the network to SMB services. Clients use this list to find computers that are not only on their own LAN, but also computers in their workgroups that may be on other reachable networks.

In Samba, browsing is configured by options described below and implemented by the `nmbd` daemon. If you are using Samba for a workgroup within a single LAN, you probably don't need to concern yourself with the browsing options. If, however, you are using Samba to provide services across several physical subnetworks, you might want to consider configuring Samba as a domain master browser. Here are some points to think about:

+   - Samba can be configured as a master browser. This allows it to gather lists of computers from local browse masters to form a wide-area server list.

+   - If Samba is acting as a domain master browser, Samba should use a WINS server to help browse clients resolve the names from this list.

+   - Samba can be used as a WINS server, although it can also rely on other types of operating systems to provide that service.

+   - There should be only one domain master browser for each workgroup. Don't use Samba as a domain master for a workgroup with the same name as an NT domain.

If you are working in an environment that has a mix of Samba and Windows NT servers, you should use an NT server as your WINS server. If Samba is your only file server, you should choose a single Samba server (`nmbd` daemon) to supply the WINS services.

> A WINS server is basically a name server for NetBIOS names. It provides the same service that a DNS server does with TCP/IP domain names. It can translate names into addresses. A DNS server is particularly useful for allowing computers to communicate with SMB across multiple subnetworks where information is not being broadcast across the subnetworks' boundaries.