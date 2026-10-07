# CHAPTER 13 Network Connectivity

The diskless passacaglia will get its boot information from server toccata.fugue.com and use vmunix.passacaglia kernel. All other TCP/IP configuration can also be included.

> CAUTION

Remember, only one DHCP server can exist on a network. Your DHCP might not work correctly on a LAN with hosts running legacy operating systems. Often Windows NT servers will have the Windows DHCP server installed by default. Because there is no configuration file for NT to sort through, DHCP server will configure your host before the Linux server if both machines are on the same LAN. Check your NT servers for this situation and disable DHCP on the NT server; afterward, your other DHCP-enabled hosts should configure correctly. Also, check to make sure there are no conflicts if you use a cable or DSL modem, wireless access point (WAP), or another intelligent router over your LAN that can provide DHCP.

# Other Uses for DHCP

The DHCP server distribution contains an example of the dhcpd.conf file that you can use as a template for your network. The file shows a basic configuration that you can get started with explanations for the options used.

# Using the Network File System (NFS)

The Network File System (NFS) was developed by Sun Microsystems as a way for computers to share files as they were local to the remote machine. NFS is commonly used to share home directories between hosts within a network. This reduces the need to have a home directory on every computer and ensures that no matter what computer you log in, your home directory will be consistent.

Another popular use for NFS is to share binary files between similar computers. If you have a new version of a package that you want all machines to have, you only have to do the upgrade to the NFS server, and all hosts running the same version of Red Hat will have the same upgraded package.

# Installing and Starting Stopping NFS

NFS installs by default on Red Hat Linux and consists of several programs that work together to provide the NFS server. One is rpc.portmapper, which maps NFS requests to the correct daemon. Another is rpc.nfsd, which is the NFS daemon. A third is rpc.mountd, which controls the mounts and unmounts of filesystems.