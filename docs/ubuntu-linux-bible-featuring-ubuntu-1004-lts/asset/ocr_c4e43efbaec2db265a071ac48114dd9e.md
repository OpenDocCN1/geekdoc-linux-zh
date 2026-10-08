# NFS Users and Authentication.

NFS uses the user ID (UID) and group ID (GID) of each user from a system's password file (/etc/passwd) to determine who can write to and access exported files and directories, based on the UID and GID that own those on the file server. This means that all of your users should have the same UID and GID on all systems to which NFS directories such as home directories are exported.

In small networks, it is often sufficient to make sure that you create the same users and groups on all of your systems, or make sure that the password and group files on your file server contain the correct entries for all of the users and groups who will access any directory that they export.

In larger networks, this is impractical, so you will want to consider network-oriented authentication mechanisms, such as Kerberos, which is discussed in Chapter 27, or the traditional Network Information System (NIS), which was developed by Sun Microsystems for use with NFS. Unfortunately, discussing NIS installation and setup on Linux systems is a history lesson rather than something that modern systems actually do, it is outside the scope of this chapter. If you need to use NIS on Linux, you can find a variety of excellent information about it online in documents such as the NIS HOWTO (www.linux-nis.org/nis-howto/), which is even available in multiple languages. NIS was great in its day and can still be quite useful in networks of heterogeneous and aging UNIX systems, but it's not the way to go in a modern networked environment comprising Linux systems, Mac OS X systems, and the occasional Windows system.

# Installing an NFS Server

You can use the Synaptic Package Manager, the Adept Package Manager, or the command-line package management utilities described in Chapter 19 to install the packages required to run and monitor an NFS server on your Ubuntu system. You must install both the nfs-common and nfs-kernel-server packages on any system where you want to run an NFS server—only the nfs-common package is required on a system on which you want to mount NFS files-systems. (Installing the nfs-kernel-server package on a system will automatically install the nfs-common package as a requirement.) Once the installation completes, you're ready to configure your server to share data from your system with any system that supports NFS.



If you are going to use Kerberos as the authentication mechanism for your NFS server (and your computing environment in general), see the section of Chapter 27 entitled "Configuring Kerberos Authentication." This chapter focuses on setting up an NFS server in small networks where common user and group IDs can be manually maintained, although Kerberos requirements or alternatives are explained wherever possible. ■