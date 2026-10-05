
# INTRODUCTION TO NFS 775

![](img/45ff4cd21497435daa35084a84b95d07_825_0.png)

**Figure 22-1** Flow of data in a typical NFS client/server setup

In the preceding example, Zach's home directory, /home/zach, is on the remote system. Using NFS, the /home/zach directory hierarchy on dog is mounted on plum; to make it easy to recognize, it is mounted as /dog.home/zach. The /gc1 and /gc5 filesystems on grape are mounted on plum as /grape.gc1 and /grape.gc5.

You can use the -T option of df to add a Type column to the display. The following command uses -t nfs to display NFS filesystems only:

```
zach@plum:~$ df -ht nfs
Filesystem      Size Used Ail% Mounted on
dog:/home/zach  19G 6.7G  11G 39% /dog.home/zach
grape:/gc1      98M 0.4M  10% /grape.gc1
grape:/gc5      39M 3.0G  81% /grape.gc5
```

Errors

Sometimes a client may lose access to files on an NFS server. For example, a network problem or a remote system crash may make these files temporarily unavailable. If you try to access a remote file in these circumstances, you will get an error message, such as NFS server not responding. When the local system can contact the remote server again, NFS will display another message, such as NFS server dog OK. A stable network and server (or not using NFS) is the best defense against this problem.

Security

NFS is based on the trusted-host paradigm (page 391), so it has all the security issues that plague other services based on this paradigm. In addition, NFS is not encrypted. From these issues, you should implement NFS on a single LAN segment only, where you can be (reasonably) sure systems on the LAN segment what they claim to be. Make sure a firewall blocks NFS traffic from outside the LAN and never use NFS over the Internet.

To improve security, make sure UIDs and GIDs are the same on the server and clients (page 788).

NFSv4 addresses many of these security issues, including the problem of users having UIDs on different systems (NFSv4 uses usernames, not UID numbers). The new version of NFS adds Kerberos authentication, provides for encrypted file transfers, and increases WAN performance.

# MORE INFORMATION

Good information on NFS, including the Linux NFS-HOWTO: nfs.sourceforge.net
- Running behind a firewall: wki.debian.org/SecuringNFS
- autofs tutorial: wki.linuxhq.com/issue/24/nielsen
- Local maps: autofs, auto-master, exports, exports, nfs (provides fstab information), rpc.bindmap, rpc.mount, rpc.nfsd, and showmount
- Linux NFS-HOWTO: nfs.sourceforge.net
- Netboot and PXE: Remote-Boot mini-HOWTO
- NFS Illustrated by Callaghan, Addison-Wesley (January 2000)

# RUNNING AN NFS CLIENT

This section describes how to set up an NFS client, mount remote directory hierarchies, and improve NFS performance.

# PREREQUISITES

Install the following package:

- nfs-common

The portmap utility (which is part of the portmap package and is installed as a dependency when you install nfs-common; page 406) must be running to enable reliable file locking.

When you install the nfs-common package, the dpkg postinst starts the daemon that an NFS client requires (not all daemons are always required): rpc.statd, rpc.lockd (does not run but starts NFS lock manager if necessary), rpc.idmapd, and rpc.gssd. You do not normally need to restart any of these daemons.

# JUMPSTART I: MOUNTING A REMOTE DIRECTORY HIERARCHY

To set up an NFS client, mount the remote directory hierarchy the same way you mount a local directory hierarchy (page 506).

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home/export with the local system. The /export directory on dog holds two directory hierarchies you want to mount: /export/progs and /export/oracle. The example mounts dog's /home directory on /dog.home/zach.

The example mounts dog's /home directory on /dog.home/zach.

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home/export with the local system. The /export directory on dog holds two directory hierarchies you want to mount: /export/progs and /export/oracle. The example mounts dog's /home directory on /dog.home/zach.

The example mounts1 / /home directory on on /dog.home/... The /gc1 and /gc5 filesystems on grape are mounted on plum as /grape.gc1 and /grape.gc5.

You can use the / of of to to to a Type to to the the.....gra11gra /gra /gragragragragragragragragragragra. on plum as /grape.gc1 and /gragra.gra5.gragragragragragra.gra.gra...gra......................gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.

Wait, you can use the -T option of df to add a Type column to the display. The following command uses -t nfs to display NFS filesystems only:

```
zach@plum:~$ df -ht nfs
Filesystem      Size Used Ail% Mounted on
dog:/home/zach  19G 6.7G  11G 39% /dog.home/zach
grape:/gc1      98M 0.4M  10% /grape.gc1
grape:/gc5      39M 3.0G  81% /grape.gc5
```

Errors Sometimes a client may lose access to files on an NFS server. For example, a network problem or a remote system crash may make these files temporarily unavailable. If you try to access a remote file in these circumstances, you will get an error message, as as

NFS server not responding. When the local system can contact the remote server again, NFS will display another message, such as NFS server dog OK. A stable network and server (or not using NFS) is the best defense against this problem.

SecurityNFS is based on the trusted-host paradigm (page 391), so it has all the securityဆောင် that plague other services based on this paradigm. In addition, NFS is not encrypted. From these issues, you should implement NFS on a single LAN segment only, where you can be (reasonably) sure systems on the LAN segment what they claim to be. Make sure a firewall blocks NFS traffic from outside the LAN and never use NFS over the Internet.

To improve security, make sure UIDs and GIDs are the same on the server and clients (page 788).

NFSv4 addresses many of these security issues, including the problem of users having UIDs on different systems (NFSv4 uses usernames, not UID numbers). The new version of NFS adds Kerberos authentication, provides for encrypted file transfers, and increases WAN performance.

# MORE INFORMATION

Good information on NFS, including the Linux NFS-HOWTO: nfs.sourceforge.net Running behind a firewall: wki.debian.org/SecuringNFS autofs tutorial: wki.linuxhq.com/issue/24/nielsen

Local maps: autofs, auto-master, exports, exports, nfs (provides fstab information), rpc.bindmap, rpc.mount, rpc.nfsd, and showmount

Linux NFS-HOWTO: nfs.sourceforge.net Netboot and PXE: Remote-Boot mini-HOWTO

NFS Illustrated by Callaghan, Addison-Wesley (January 2000)

# RUNNING AN NFS CLIENT

This section describes how to set up an NFS client, mount remote directory hierarchies, and improve NFS performance.

# PREREQUISITES

Install the following package:

+   - nfs-common

The portmap utility (which is part of the portmap package and is installed as a dependency when you install nfs-common; page 406) must be running to enable reliable file locking.

When you install the nfs-common package, the dpkg postinst starts the daemon that an NFS client requires (not all daemons are always required): rpc.statd,

rpc.lockd (does not run but starts NFS lock manager if necessary), rpc.idmapd, and rpc.gssd. You do not normally need to restart any of these daemons.

# # JumpStart I: MOUNTING A REMOTE DIRECTORY HIERARCHY

To set up an NFS client, mount the remote directory hierarchy the same way you mount a local directory hierarchy (page 506).

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home/export with the local system. The /export directory on dog holds two directory hierarchies you want to mount: /export/progs and /export/oracle. The example mounts dog's /home directory on /dog.home/zach.

The example mounts dog's /home directory on /dog.home/zach.

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home/export with the local system. The /export directory on dog holds two directory hierarchies you want to mount: /export/progs and /export/oracle. The example mounts dog's /home directory on /dog.home/zach.

The example mounts dog's /home directory on /dog.home/zach.

The example mounts dog's /home directory on /dog.home/zach.

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home.exportgra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra

The following examples show two ways to mount a remote directory hierarchy, assuming dog is on the same network as the local system and is sharing /home/export with the local system. The /export directory on dog holds two directory hierarchies you want to mount: /export/progs and /export/oracle. The example mounts dog's /home directory on /dog.home/zach.

The example mounts dog's /home directory on /dog.home/zach.

gra.gra.gra.gra.gra/gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gra.gragragra.gra.gra.gra.gra.gragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragra.gragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragragra the data in the cache is current. The data in the cache is current.

The kernel uses the modification time of the file to determine when its cache is out-of-date. If the time the attribute cache was saved is later than the modification time of the file itself, the data in the cache is current. The server must periodically refresh the
