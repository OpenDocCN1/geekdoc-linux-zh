If you are not running rpc-quotad, you do not need to create or modify the quota file.
The ports used in the example are the ones suggested in the Linux NFS-HOWTO,
y you can use any unused ports as you like. See wiki.debian.org/SecuringNFS for more information.

If the NFS server system is running a firewall, you need to open ports 111 and 2049. To do so, use gufw (port 876) to set a policy that allows NFS service. In addition, open the ports you specified in the files in /etc/default, as explained earlier.
Because gufw has no defined policy for these ports, you need to specify the ports manually when you add a rule in gufw.

The rpc-mountd daemon uses TCP wrappers to control access to the server.
As explained on page 465, you can set up /etc/hosts.allow and /etc/hosts.deny to specify which clients can contact rpc-mountd on the server and there use NFS.
The name of the daemon in these files is mounted.

# START II: CONFIGURING AN NFS SERVER
Using shares-admin

The Shared Folders window (Figure 22-2) enables the local system to share directory hierarchies using Samba (Chapter 23) and/or NFS. To display this window, give the command shares-admin from a terminal emulator or Run Application window (ALT+2). Click the lock icon labeled Click to make changes and enter your password to enable this window to set up shares.

As part of process of setting up an NFS server, the Shared Folders window identifies the /etc/exports file. If the system is running a firewall, see “Firewall” on page 782. The shares-admin utility allows you to specify which directory hierarchies you want to share and how they are shared using NFS. Each exported hierarchy is called a share—terminology that is borrowed from Samba.

![](bbox=[0.319, 0.631, 0.813, 0.876])