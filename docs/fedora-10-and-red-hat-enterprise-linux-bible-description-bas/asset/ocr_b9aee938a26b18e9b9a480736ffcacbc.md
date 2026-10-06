# Chapter 18: Setting Up a File Server 781

+   - log file Defines the location of the Samba log file. By default, Samba log files are contained in /var/log/samba (with file names nmbd.log and smbd.log, and smb.log). In this option, the %n is replaced by the name of each host that tries to connect to the Samba server.So, for example, for a client named maple, the smb log file is /var/log/samba/maple.log.
- max size Sets the maximum amount of space, in kilobytes, that the log files can consume. By default, the value is set to 0 (no limit).

Printing options
The options field is used to define options that are passed to the cups service. By default, only the raw option is set (which causes printing data to be passed directly to the Samba printer.

Browse options
A browse list is available to SMB services. Clients use this list to find computers that are not only on their own LAN, but also computers in the workgroups that may be on other reachable networks.

In Samba, browsing is configured by options described below and implemented by the nmbd daemon. If you are using Samba for a groupwork within a single LAN, you don't need to concern yourself with the browsing options. However, if you are using Samba to provide services over several physical networks, you might want to consider configuring Samba as a domain master browser. Here are some points to think:

+   - Samba can be configured as a master browser. This allows it to gather lists of computers from local masters to form a wide-area server list.
- If Samba is acting as a domain master browser, Samba should use a WINS server to help clients resolve the names from this list.
- Samba can be used as a WINS server, although it can also rely on other types of operating systems to provide that service.
- There should be only one domain master browser for each workgroup. Don't use Samba as a domain master for a workgroup with the same name as an NT domain.

If you are working in an environment that has a mix of Samba and Windows servers, you should use an NT server as your WINS server. Samba is your only file server, you should choose a single Samba server (nmbd daemon) to supply the WINS services.

> NOTE: Samba is basically a name server for NetBIOS. It provides the same service that a DNS server does with TCP/IP domain names: it can translate names into addresses. A WINS server is particularly useful for allowing computers to communicate with SMB across multiple subnets where information is not being broadcast across the subnetworks' boundaries.

To configure the browsing feature in Samba, you must have the workgroup properly named (described earlier in this section). Here are the global options related to SMB browsing.