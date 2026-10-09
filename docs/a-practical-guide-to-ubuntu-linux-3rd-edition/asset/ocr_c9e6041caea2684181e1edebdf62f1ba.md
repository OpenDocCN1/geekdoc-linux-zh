NFS server **dog** not responding. When the local system can contact the remote server again, NFS will display another message, such as **NFS server dog OK**. A stable network and server (or not using NFS) is the best defense against this problem.

**Security** NFS is based on the trusted-host paradigm (page 391), so it has all the security shortcomings that plague other services based on this paradigm. In addition, NFS is not encrypted. Because of these issues, you should implement NFS on a single LAN segment only, where you can be (reasonably) sure systems on the LAN segment are what they claim to be. Make sure a firewall blocks NFS traffic from outside the LAN and never use NFS over the Internet.

To improve security, make sure UIDs and GIDs are the same on the server and clients (page 788).

**NFSv4** NFSv4 addresses many of these security issues, including the problem of users having different UIDs on different systems (NFSv4 uses usernames, not UID numbers).

The new version of NFS adds Kerberos authentication, provides for encrypted file transfers, and increases WAN performance.

# MORE INFORMATION

+   * **Web** Good information on NFS, including the *Linux NFS-HOWTO*: nfs.sourceforge.net
+     * Running NFS behind a firewall: wiki.debian.org/SecuringNFS
+     * autofs tutorial: www.linuxhq.com/fg/lsguide24/nielsen.html

+   * **Local** *man* pages: autofs, autmount, auto.master, exportfs, exportrs, nfs (provides *fstab* information), rpc.rstatd, rpc.rquotad, rpc.nfsd, and showmount

+   * **HOWTO** *Linux NFS-HOWTO*: nfs.sourceforge.net
+     * *Netboot and PXE: Remote-Boot mini-HOWTO*
+     * *Automount mini-HOWTO*

+   * **Book** *NFS Illustrated* by Callaghan, Addison-Wesley (January 2000)

# RUNNING AN NFS CLIENT

This section describes how to set up an NFS client, mount remote directory hierarchies, and improve NFS performance.

# PREREQUISITES

+   * **Installation** Install the following package:
+     * **nfs-common**

+   * **portmap** The portmap utility (which is part of the **portmap** package and is installed as a dependency when you install **nfs-common**; page 406) must be running to enable reliable file locking.

+   * **nfs-common** init script When you install the **nfs-common** package, the **dpkg postinst** script starts the daemons that an NFS client requires (not all daemons are always required): **rpc.statd**.