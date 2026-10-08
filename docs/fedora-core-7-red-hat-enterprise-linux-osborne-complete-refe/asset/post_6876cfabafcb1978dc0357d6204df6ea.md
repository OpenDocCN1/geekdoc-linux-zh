
## Netflix Rules

You can further control access using Netfilter to check transmissions from certain hosts on the ports used by NFS services. (See Chapter 20 for an explanation of Netfilter.) The portmapper uses port 111, and nfsd uses 2049. Netfilter is helpful if you have a private network that has an Internet connection, and you want to protect it from the Internet. Usually a specific network device, such as an Ethernet card, is dedicated to the Internet connection. The following examples assume that device eth1 is connected to the Internet. Any packets attempting access on port 111 or 2049 are refused.

```
iptables -A INPUT -i eth1 -p 111 -j DENY
iptables -A INPUT -i eth1 -p 2049 -j DENY
```

To enable NFS for your local network, you will have to allow packet fragments. Assuming that eth0 is the device used for the local network, you could use the following example:

```
iptables -A INPUT -i eth0 -f -j ACCEPT
```

> **NOTE** A root user on a remote host can try to access a remote NFS server as a root user with root level permissions. The root_squash option (a default) will automatically change the remote root user to the nobody (anonymous) user.

Check the `nfs` Man page for NFSv4 options.

## Mounting NFS File Systems: NFS Clients

Once NFS makes directories available to different hosts, those hosts can then mount those directories on their own systems and access them. The host needs to be able to operate as an NFS client. Current Linux kernels all have NFS client capability built in. This means that any NFS client can mount a remote NFS directory that it has access to by performing a simple mount operation.

## Mounting NFS Automatically: /etc/fstab

You can mount an NFS directory either by an entry in the `/etc/fstab` file or by an explicit mount command. You have your NFS file systems mounted automatically by placing entries for them in the `/etc/fstab` file. An NFS entry in the `/etc/fstab` file has a mount type of NFS. An NFS file system name consists of the hostname of the computer it is located on, followed by the pathname of the directory where it is mounted. The two are separated by a colon. For example, `rabbit.trek.com:/home/project` specifies a file system mounted at `/home/project` on the `rabbit.trek.com` computer. The format for an NFS entry in the `/etc/fstab` file follows. Notice that the file type is `nfs`.

```
host:remote-directory local-directory nfs options 0 0
```

You can also include several NFS-specific mount options with your NFS entry. You can specify the size of datagrams sent back and forth, and the amount of time your computer waits for a response from the host system. You can also specify whether a file system is to be hard-mounted or soft-mounted. For a hard-mounted file system, your computer continually tries to make contact if for some reason the remote system fails to respond. A soft-mounted file system, after a specified interval, gives up trying to make contact and issues an error message. A hard mount is the default. A system making a hard-mount attempt that continues to fail will stop responding to user input as it tries continually to achieve the mount. For this reason, soft mounts may be preferable, as they will simply stop attempting a mount that continually fails. Table 38-2 and the Man pages for **mount** contain a listing of these NFS client options. They differ from the NFS server options indicated previously.

An example of an NFS entry follows. The remote system is **rabbit.mytrek.com**, and the file system is mounted on */home/projects*. This file system is to be mounted on the local system as the */home/dylan/projects* directory. The */home/dylan/projects* directory must already be created on the local system. The type of system is NFS, and the **timeo** option specifies the local system waits up to 20 tenths of a second (two seconds) for a response. The mount is a soft mount and can be interrupted by NFS.

```
rabbit.mytrek.com:/home/projects /home/dylan/projects nfs soft,intr,timeo=20
```

## Mounting NFS Manually: mount

You can also use the **mount** command with the **-t nfs** option to mount an NFS file system explicitly. For a NFSv4 file system you would use **-t nfs4**. To mount the previous entry explicitly, use the following command:

```
# mount -t nfs -o soft,intr,timeo=20 \
rabbit.mytrek.com:/home/projects /home/dylan/projects
```

| Option | Description |
| :--- | :--- |
| **rsize=n** | The number of bytes NFS uses when reading files from an NFS server. The default is 1,024 bytes. A size of 8,192 can greatly improve performance. |
| **wsize=n** | The number of bytes NFS uses when writing files to an NFS server. The default is 1,024 bytes. A size of 8,192 can greatly improve performance. |
| **timeo=n** | The value in tenths of a second before sending the first retransmission after a timeout. The default value is seven-tenths of a second. |
| **retry=n** | The number of minutes to retry an NFS mount operation before giving up. The default is 10,000 minutes (one week). |
| **retrans=n** | The number of retransmissions or minor timeouts for an NFS mount operation before a major timeout (default is 3). At that time, the connection is canceled or a “server not responding” message is displayed. |
| **soft** | Mount system using soft mount. |
| **hard** | Mount system using hard mount. This is the default. |
| **intr** | Allow NFS to interrupt the file operation and return to the calling program. The default is not to allow file operations to be interrupted. |
| **bg** | If the first mount attempt times out, continue trying the mount in the background. The default is to fail without backgrounding. |
| **tcp** | Mount the NFS file system using the TCP protocol, instead of the default UDP protocol. |

**TABLE 38-2 NFS Mount Options**

You can, of course, unmount an NFS directory with the `umount` command. You can specify either the local mountpoint or the remote host and directory, as shown here:

```
umount /home/dylan/projects
umount rabbit.mytrek.com:/home/projects
```

> **NOTE** You can also mount and unmount all your NFS file systems at once with the `/etc/rc.d/init.d/netfs` script, which you can invoke with the `service` command. This script reads the NFS entries in the `/etc/fstab` file, using them to mount and unmount NFS remote directories. Using the `stop` argument unmounts the file systems, and with the `start` argument, you mount them again. The `restart` argument first unmounts and then remounts the file systems.

## Mounting NFS on Demand: autofs

You can also mount NFS file systems using the automount service, `autofs`. This requires added configuration on the client’s part. The `autofs` service will mount a file system only when you try to access it. A directory change operation (`cd`) to a specified directory will trigger the mount operation, mounting the remote file system at that time.

The `autofs` service is configured using a master file to list map files, which in turn lists the file systems to be mounted. The `/etc/auto.master` file is the `autofs` master file. The master file will list the root pathnames where file systems can be mounted along with a map file for each of those pathnames. The map file will then list a key (subdirectory), mount options, and the file systems that can be mounted in that root pathname directory. On some distributions, the `/auto` directory is already implemented as the root pathname for file systems automatically mounted. You could add your own file systems in the `/etc/auto.master` file along with your own map files, if you wish. You will find that the `/etc/auto.master` file contains the following entry for the `/auto` directory, listing `auto.misc` as its map file:

```
/auto auto.misc --timeout 60
```

Following the map file, you can add options, as shown in the preceding example. The `timeout` option specifies the number of seconds of inactivity to wait before trying to automatically unmount.

In the map file, you list the key, the mount options, and the file system to be mounted. The key will be the subdirectory on the local system where the file system is mounted. For example, to mount the `/home/projects` directory on the `rabbit.mytrek.com` host to the `/auto/projects` directory, you would use the following entry:

```
projects soft,intr,timeo=20 rabbit.mytrek.com:/home/projects
```

You could also create a new entry in the master file for an NFS file system, as shown here:

```
/myprojects auto.myprojects --timeout 60
```

You would then create an `/etc/auto.myprojects` file and place entries in it for NFS file system mounts, like the following:

```
dylan soft,intr,rw rabbit.mytrek.com:/home/projects
newgame soft,intr,ro lizzard.mytrek.com:/home/supergame
```
