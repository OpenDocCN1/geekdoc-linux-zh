Where NetBIOS over TCP/IP is enabled, use of a WINS server is highly recommended to aid the resolution of NetBIOS (SMB) names to IP addresses. WINS allows remote segment clients to obtain NetBIOS name-type information that cannot be provided by any other means of name resolution.

# 9.7.1 Browsing Support in Samba

Samba facilitates browsing. The browsing is supported by nmbd and is also controlled by options in the smb.conf file. Samba can act as an LMB for a workgroup, and the ability to support domain logons and scripts is now available.

Samba can also act as a DMB for a workgroup. This means that it will collate lists from LMBs into a wide-area network server list. In order for browse clients to resolve the names they may find in this list, it is recommended that both Samba and your clients use a WINS server.

Do not set Samba to be the domain master for a workgroup that has the same name as an NT Domain. On each wide-area network, you must only ever have one DMB per workgroup, regardless of whether it is NT, Samba, or any other type of domain master that is providing this service.

> NOTE
> 
> nmbd can be configured as a WINS server, but it is not necessary to specifically use Samba as your WINS server. MS Windows NT4, Server or Advanced Server 200x can be configured as your WINS server. In a mixed NT/200x server and Samba environment on a WAN, it is recommended that you use the Microsoft WINS server capabilities. In a Samba-only environment, it is recommended that you use one and only one Samba server as the WINS server.

To get browsing to work, you need to run nmbd as usual, but must use the workgroup option in smb.conf to control what workgroup Samba becomes a part of.

Samba also has a useful option for a Samba server to offer itself for browsing on another subnet. It is recommended that this option is used only for “unusual” purposes: announcements over the Internet, for example. See remote announce in the smb.conf man page.

# 9.7.2 Problem Resolution

If something does not work, the log.nmbd file will help to track down the problem. Try a log level of 2 or 3 for finding problems. Also note that the current browse list usually gets stored in text form in a file called browse.dat.