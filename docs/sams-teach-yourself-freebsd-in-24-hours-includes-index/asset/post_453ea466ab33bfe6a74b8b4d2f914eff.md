
specific folders in the filesystem that are exported, or made available over the network, and another machine connects to that machine requesting access to its shares. The client then mounts the desired share into its own filesystem, as though the NFS share were simply another UNIX disk or partition, and the user can list the files in it and work with them at the shell command line.

Like FTP, NFS has no built-in means for browsing, or the ability to get a listing of what servers or shares are available on a local network. An NFS client must know which servers it can connect to and what the available shares' names are before it can do anything useful.

An NFS server can control exactly which clients are able to connect to it—for example, by hostname or IP address; or by centralized login, as with NIS or Kerberos. Another feature of NFS is that it does not depend on LAN broadcasts for server discovery, it can be used across the Internet just as easily as across the LAN. A client in Boston can mount a share from a server in San Francisco, if necessary. By contrast, NetBIOS/SMB and AppleTalk only can operate within domains or zones on the local network (though AppleTalk/IP can cross the Internet freely).

The client-server structure of NFS is designed so that you can centralize the resources in your network. For example, an enterprise might give all its employees home directories on a central UNIX machine: Every other system in the network that supports NFS will be able to mount those home directories and access them remotely, rather than requiring each machine to have its own copy of every home directory. Figure 24.3 shows this kind of network topology in action. The same can be done for build directories (in a software development environment) or shared applications that are centrally installed (as in a university workstation cluster). NFS mounts can be used in conjunction with NIS (centralized login management) to provide the entire network with user authentication; then, file ownership and permissions on every file in a mounted share will work just as on the NFS server machine itself. You can even install FreeBSD over NFS if you mount the installation CD-ROM on the NFS server and point sysinstall toward it.

NFS doesn't have any built-in security or encryption, so it should be used over the Internet only if you're working with files that can safely be exposed to the public. Mission-critical or sensitive data should never be sent over wide-area NFS except inside a LAN protected by a firewall or through an encrypted VPN tunnel.

A FreeBSD machine can be configured to be an NFS server, an NFS client, or both. We'll talk first about setting it up as an NFS server and then about configuring it as a client.

![](img/ba0161b65b37e94cffc801ecbacaba5e_410_0.png)

FIGURE 24.3
An enterprise network with central NFS-mounted home directories.

## Configuring an NFS Server

Setting up your FreeBSD machine to be an NFS server involves adding the following two lines to /etc/rc.conf:

```
nfs_server_enable="YES"
rpcbind_enable="YES"
```

When you set the nfs_server_enable option and reboot, FreeBSD starts three different kinds of daemon processes after reading the contents of the /etc/exports file to determine what to share via NFS. These processes—nfsd, mountd, and rpcbind—each has its own role to play in NFS and can be tweaked for maximum performance by experts. The default configuration, however, should be adequate for most users' needs.

## Setting Up Shares: The /etc/exports File

The /etc/exports file lists what directory trees should be shared via NFS and who should be allowed to access them. If /etc/exports does not exist or is not readable when the network is started, the nfsd and mountd processes are not started.

The full format of /etc/exports is defined in man exports. A basic export line specifies one or more directories that should be exported (shared), any of several options, and then an optional list of hosts (by IP address, network, netgroup, or hostname) that are allowed to share the specified directories. For example, the following line shares the /home directory and all its subdirectories to anybody who connects:

/home -alldirs

Note that the -alldirs option can only be specified if the share is the mount point of a filesystem (for example, /usr or /home). If it isn't, for example if /home is not the point at which a filesystem is mounted (if your /home is just a directory inside /usr), the share will not be made available.

A share that can be accessed only by three specified hosts and is read-only would look like this:

```
/usr2 -ro -alldirs stripes.somewhere.com spots.somewhere.com 64.41.131.165
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_411_0.png)

> You can create groups of hosts (netgroups) by specifying them in the file /etc/netgroup. A group can be specified in the following form:
> groupname (host, user, domain) (host, user, domain) ...
> For instance, to create a group called desktops that contained three particular hosts (named sol, luna, and terra), the line would look like this:
> desktops (sol,,) (luna,,) (terra,,)
> A netgroup defined on usernames would look like this:
> developers (,frank,) (,bob,) (,alice,)
> You can then use any of these netgroup names instead of hostnames in /etc/exports to confine an NFS share to members of that group.

File ownership in an NFS share is mapped based on the UIDs of each file and directory. If the usernames and UIDs on the server and client machines are the same (for instance, if the machines' logins are synchronized via NIS or Kerberos), the permissions will match. However, if the UID 1045 maps on the server to the username bill, but UID 1045 on the client is john, John will own the files in the share that the server thinks Bill owns. When exporting a share containing files owned by many different users, make sure that the infrastructure is in place to provide consistent mappings between UIDs and usernames on all the machines on your network.

You can use the -maproot=<username> or -maproot=<UID> options to map ownership so that the username matching <username> or having the user ID <UID> on the client machine will have full root permissions in the share. For example, to share the entire filesystem of the NFS server with anybody in the 64.41.131 network, with the client user frank having full read/write access to all the files, use the following:

```
/ -maproot=frank -network 64.41.131 -mask 255.255.255.0
```

After making any changes to /etc/exports, you need to restart the mountd process. Do this by accessing the runtime PID file:

```
# kill -HUP `cat /var/run/mountd.pid`
```

![](img/ba0161b65b37e94cffc801ecbacaba5e_412_0.png)

> You can't have multiple export lines for mount points within the same partition or filesystem. This is to prevent problems in cases where the export permissions for different shares in the same filesystem would conflict. If you want to create multiple shares that are within the same filesystem, you must put them all on the same line. The following setup is illegal:
> 
> /home/frank 64.41.131.102
> /home/joe 64.41.131.102
> 
> But the following setup is correct:
> 
> /home/frank /home/joe 64.41.131.102

You can use the showmount program to display the valid shares and their permissions. This is how you can tell whether your /etc/exports setup is valid:

```
# showmount -e
Exports list on localhost:
/usr			Everyone
/home/frank		64.41.131.102
/home/joe		64.41.131.102
/			64.41.131.0
```

## Starting NFS Services Without Rebooting

The cleanest way to start NFS services is to reboot the system. However, if you need to start the services and you don't want to reboot, simply issue the following commands as root (omitting the rpcbind command if it's already running):

```
# rpcbind
# nfsd -u -t -n 4
# mountd -r
```

Then, use showmount -e to make sure that the NFS shares are being exported properly.

## Configuring an NFS Client

If your FreeBSD machine will be mounting NFS shares from other servers, you will need to configure it as a client. Technically this isn't really necessary—you can mount an NFS share in a rudimentary fashion right out of the box. However, configuring the system as an NFS client gives you a few features that ensure speedy and reliable performance.

To set up an NFS client machine, simply enable the following line in /etc/rc.conf:

```
nfs_client_enable="YES"
```
