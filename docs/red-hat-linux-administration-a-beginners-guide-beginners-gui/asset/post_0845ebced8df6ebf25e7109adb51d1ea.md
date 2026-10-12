
## Ask the Expert

**Q:** So NFS is a user-space daemon, then? I thought I saw some kernel options for NFS?

**A:** The NFS server was originally a user-space process. That is, no special kernel support was necessary for it to work. With the introduction of the 2.2 kernel, an optional kernel mode NFS server was introduced, with critical parts of the process actually compiled into the kernel for performance reasons. Recently (particularly in 2.4 kernels) the user-space version of the NFS server has fallen by the wayside in favor of the kernel mode version. Because only critical parts of the server are compiled into the kernel, user-space daemons exist to handle the rest of the protocol.

## Progress Check

- 1. What is the command to stop NFS without shutting the server down?
- 2. When a request to mount a partition is made, which file is consulted to determine access to the requested directory?

**Answer to Progress Check:**
1. `/etc/init.d/nfs stop`.
2. The permission is stored in the `/etc/exports` file.

### CRITICAL SKILL 16.3

## Configuring NFS Servers

Setting up an NFS server is a two-step process. The first step is to create the `/etc/exports` file. This file defines which parts of your server’s disk get shared with the rest of your network and the rules by which they get shared. (For example, is a client allowed only to read a partition or is it allowed to write to that partition?) The second step is to start the NFS server processes that read the `/etc/exports` file and follow the specifications. Pretty straightforward, isn’t it?

![](img/ec2066d370d3af1a767664d36aa7ddfe_489_0.png)

### The /etc/exports Configuration File

NFS servers have only one configuration file: `/etc/exports`. This file lists the partitions that are shareable, the hosts they can be shared with, and with what permissions. Here is the format of each entry in the `/etc/exports` file:

```
/dir/to/export  client1(permissions) client2(permissions) \
                 client3(permissions) client4(permissions)
```

- `/dir/to/export` is the directory you want to share with other users; for example, `/export/home`.
- `client1`, `client2`, and so forth, are the host names of the NFS clients. The wildcard characters `*` and `?` may be used. Netgroups may also be specified using the `@group` syntax. See Module 17 for more information on netgroups. Clients can also be specified by IP address or IP network block.
- Permissions are the corresponding permissions for each client.

Table 16-1 describes the most useful permissions for each client.

**Table 16-1** Commonly Used Permissions for NFS Exports

| Permission | Description |
|---|---|
| ro | Files are read-only. No files may be written to (or newly created) on this mount. This is the default. |
| rw | Allow both read and write requests to this volume. Useful for home directories, mail spools, etc. |
| async | This option attempts to improve performance by not waiting for the server to actually flush all data to the disk. If the server crashes at an inopportune time, this can result in data loss. Using this option without a specific reason is not recommended. In the past, this was the default, but recently the default has changed to sync. |
| sync | The opposite of the async option. Attempts to write data don’t return until the data is actually flushed to disk. In order to match other NFS implementations, this is now the default. Because the default recently changed from async to sync, exportfs may issue a warning if neither option has been explicitly specified, so that admins are aware of the change. |
| anonuid | NFS supports the concept of an “anonymous” user, mostly in conjunction with the “squash” options listed next. By default this is mapped to the user nobody, but you can map this to a different user ID (UID) using the anonuid option. A corresponding anogid option also exists for remapping the anonymous group. |
| root_squash | Attempts to access files from the root user will be remapped as if they came from the anonymous user. Don't overestimate how much security this will buy you, however. Someone with root access on a client machine can always su to a user that does have access to a given file. What you may be able to get from this is a limited protection for files that are owned by root on the server, marked as only readable, writable, or executable by owner. This is the default. |
| no_root_squash | Disables the root_squash option just described. This is most useful on diskless workstations that mount their entire file tree over NFS, and preventing root access to some files (/etc/shadow, for example) causes its own problems. |
| all_squash | This works much like the root_squash option, except that all user access is remapped as if it came from the anonymous user. |
| insecure | By default, the NFS server will only accept connections from “secure” ports—that is, port numbers below 1024. If you need to allow non-root users to mount NFS exports, then you'll need to specify the insecure option. |
| no_wdelay | The NFS server tries to improve overall performance by not committing a write to disk if it suspects that a related write will arrive soon. This allows multiple write requests to be performed with a single disk operation. If you have a situation where lots of small unrelated writes are likely to occur, you may wish to turn this off by setting the no_wdelay option. |
| no_subtree_check | When the directory that you're exporting is only a portion of a disk volume, the NFS server checks to make sure that all requests refer to files that are in that subtree. If the directory that you're exporting involves an entire disk partition, you can speed things up by specifying no_subtree_check. |
| insecure_locks | Normally NFS will require authentication before honoring a lock request. Some older NFS implementations didn't have the concept of authenticating locks, so you may need to specify insecure_locks if you have to interoperate with one of these older implementations. |

A backslash at the end of the line indicates that the entry continues on to the next line. Comments can be added by using a pound symbol (`#`) at the beginning of the line.

## CAUTION

Keep those UIDs in sync! Every NFS client request to an NFS server includes the UID of the user making the request. This UID is used by the server to verify that the user has permissions to access the requested file. However, in order for NFS permission-checking to work correctly, the UIDs of the users must be synchronized between the client and server. Having the same username on both systems is not enough. (You can compare this to keeping System IDs (SIDs) synchronized under Windows.) One way of keeping the UIDs in sync is to use the Network Information Service (NIS), as described in Module 17.

Following is an example of a complete NFS `/etc/exports` file:

```
#
#  /etc/exports for gandalf.example.org
#
/export/home fredo(rw) sam(rw) pippen(rw) \
@shire(rw) \
unixadmin(rw,no_root_squash)
/export/usr/local legolas(rw) \
neirond(rw) galadriel(rw) \
192.168.3.0/24(ro,all_squash) \
*.rivendell.example.org (rw)
unixadmin(rw,no_root_squash)
/export/anonftp ftpserver(ro,all_squash,anonuid=14,anogid=50)
```

## Graphically configuring exports

Once again, Red Hat provides a graphical alternative for setting up your `/etc/exports` file. You can launch this GUI tool by selecting NFS Server from the Server Settings submenu or from the command line by typing `redhat-config-nfs`.

![](img/ec2066d370d3af1a767664d36aa7ddfe_492_0.png)

Adding exported directories from the main window is very straightforward. Either adding a new share or clicking on Properties for an existing share brings up a dialog box allowing you to adjust the options for that share.

![](img/ec2066d370d3af1a767664d36aa7ddfe_493_0.png)

The Basic tab holds settings for the hosts to which you want to export and settings for whether those hosts have write permissions. One of the oversights of the GUI tool is having to select either `ro` or `rw` for the entire list of hosts in the dialog box. If you want to mix `ro` and `rw` hosts, you have to make separate shares in the GUI tool.

Selecting the General Options tab brings up some additional selections that should seem familiar. The Allow Connections from Ports 1024 And Higher option corresponds to the insecure option mentioned earlier. You will probably recognize, without any difficulty, how to specify `insecure_locks`, `no_subtree_check`, and `sync` from the options presented on this tab. The last option, Force sync of write operations immediately, corresponds to the `no_wdelay` option.

Finally, the User Access tab lets you adjust the squash options. The Treat Remote Root User As Local Root affects the `no_root_squash` setting, and Treat All Client Users As Anonymous Users is the `all_squash` setting. Notice that you can't change the `anonuid` or `anogid` options with only `root_squash` enabled; instead, `all_squash` has to be enabled.

As usual, the GUI tool provides no support for commenting your /etc/exports file and doesn't mix well with hand edits. In some cases, even a simple, valid, hand-edited /etc/exports file will prove to be unparseable by the GUI tool. As of this writing, the stability of this tool is not quite what it should be, and although we expect that to improve with future updates, you may want to make sure that you understand the format of the exports file in case you find yourself having to edit it by hand.

## Telling the NFS Server Process About /etc/exports

Once you have an /etc/exports file written up, use the `exportfs` command to tell the NFS server processes to reread the configuration information. The parameters for `exportfs` are found in Table 16-2.
