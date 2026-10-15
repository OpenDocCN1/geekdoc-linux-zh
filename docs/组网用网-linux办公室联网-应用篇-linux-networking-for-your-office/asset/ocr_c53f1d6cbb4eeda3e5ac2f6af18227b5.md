connect your network to the Internet. If you use NetBEUI, this problem is also reduced because NetBEUI doesn't get past TCP/IP routers. If you're concerned about these issues, you should consult with your organization's networking personnel or with your ISP to determine how your computers are connected to the Internet.

# The SMB Protocols

At the top of the Windows networking protocols, controlling the show as it were, is the *Server Message Block* (SMB) protocol, which has been renamed the *Common Internet File System* (CIFS). In fact, Samba gets its name from the acronym SMB. Figure 11.2 shows the relationship between SMB, NetBIOS, NetBEUI, IPX, and TCP/IP.

![](bbox=[0.259, 0.34, 0.616, 0.454])

**FIGURE 11.2**
*Samba supports SMB only over TCP/IP, although Windows supports SMB over NetBEUI and IPX, as well.*

NetBIOS provides basic functionality—indeed, the B in NetBIOS stands for basic. SMB provides higher-level tools. This is similar to the relationship between a driver or BIOS for controlling a hard disk and the disk’s filesystem. SMB is, much like UNIX’s Network Filesystem (NFS), a filesystem for network use. Unlike a hard disk’s BIOS, though, in the case of Windows file sharing, there’s another level of protocols beneath the NetBIOS—namely TCP/IP, in the case of Samba.

# When to Use Samba

NetBIOS and SMB/CIFS were designed with networking for DOS and, later, Windows and OS/2 in mind. These protocols provide support for the specific features that DOS, Windows, and OS/2 programs expect of a filesystem. Other networking protocols, such as NFS, support a different set of features. Therefore, using SMB/CIFS is the best course of action when the client OS is DOS, Windows, or OS/2.

Note, however, that using Samba on Linux means that Samba has to convert the filesystem features supported by SMB into forms that Linux can handle. Basic functionality, such as file reading and writing, isn’t a problem; features like the hidden attribute, which isn’t supported by Linux, can cause difficulties, depending on how Samba is configured. For the most part, Samba has conquered these difficulties, so a Samba server can integrate quite seamlessly into