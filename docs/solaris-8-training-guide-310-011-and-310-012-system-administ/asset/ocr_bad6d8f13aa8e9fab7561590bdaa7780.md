# Configuring a NIS Master Server

Before configuring a NIS master server, be sure the NIS package is installed. The package names are SUNWypu and SUNWypr. Use the pkginfo command to check for these packages. Both packages are part of the standard Solaris 8 release. The daemons that support the NIS service are described in Table 18.3.

**TABLE 18.3**
**NIS DAEMONS**

| Daemon | Function |
|---|---|
| ypserv | This daemon is the NIS database lookup server. The ypserv daemon's primary function is to look up information in its local database of NIS maps. If the /var/yp/ypserv.log file exists when ypserv starts up, log information is written to it if error conditions arise. At least one ypserv daemon must be present on the network for the NIS service to function. |
| ypbind | This daemon is the NIS binding process that runs on all client systems that are set up to use NIS. The function of ypbind is to remember information that lets all NIS client processes on a node communicate with some NIS server process. |
| ypxfr | This daemon is the high-speed map transfer. ypxfr moves a NIS map in the default domain to the local host. It creates a temporary map in the directory /var/yp/ypdomain. |
| rpc.yppasswdd | This daemon handles password change requests from the yppasswd command. It changes a password entry in the passwd, shadow, and security/passwd.adjunct files. |
| rpc.ypupdated | This daemon updates NIS information. ypupdated consults the updaters file in the /var/yp directory to determine which NIS maps should be updated and how to change them. |

The commands that you use to manage the NIS service are shown in Table 18.4. I'll describe some of these commands in more detail later as I show examples of setting up NIS.