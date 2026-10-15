# Can I use a web browser to access UNIX from a Windows NT machine?

Yes, assuming the UNIX machine is running a web server. One of the virtues of web technology is that it is, in large part, platform independent. So whether you are running a Netscape browser from your UNIX machine to get to your Windows NT machine, or Microsoft’s Internet Explorer from Windows NT to your UNIX machine, the results are pretty much the same. The available options for web servers and browsers will, however, be somewhat different.

# ADVANCED NETWORKING EMULATIONS

# What is SMB and why should I care?

SMB is short for server message blocks; it is the underlying technology that Microsoft networking uses. UNIX servers can also use SMB, allowing them to talk to machines running Windows NT (or any other Microsoft networking stack). There are both freeware and commercial implementations of SMB available for a wide variety of UNIX and Linux versions, allowing you to add Windows connectivity to your UNIX network easily and essentially transparently to the Windows users.

# What is NFS?

NFS is short for Network File System. Originally developed by Sun Microsystems, it is a pure TCP/IP method of providing file and printer sharing on a network. Since its origins are in the UNIX community, it tends to be the method of choice for sharing filesystems across UNIX networks. Implementations are available for Windows and Windows NT as well, but with some limitations.

# How can I make my UNIX server visible to my Windows and Windows NT users?

You can use either an SMB server on the UNIX box, or an NFS client on the Windows machines. Both ways will work, and the choice of technology will depend in large part on