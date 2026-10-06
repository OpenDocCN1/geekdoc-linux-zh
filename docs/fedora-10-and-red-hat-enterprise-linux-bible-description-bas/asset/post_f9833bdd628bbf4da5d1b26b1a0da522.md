
# Part IV: Fedora RHEL Network and Server Setup

- User mapping — If the same users have login accounts for a set of computers (and they have the same IDs), NFS, by default, will map those IDs. This means that if the user named mike (UID 110) on maple has account on pine (mike, UID 110), he could use his own remotely mounted files from either computer.

If a client who is not set up on the server creates a file on the NFS directory, it is assigned to the owner's UID and GID. (An ls -l on the server would show the UID of the owner.) You can identify a file that contains user mappings using the map_static option.

> TIP: The exports page describes the map_static option, which should let you create a file with new mappings. These mappings should let you remap client IDs into different IDs on the server.

## Exporting the shared file systems

After you have added entries to /etc/exports files, you can actually export the directories listed using the exports command. If you reboot your computer or restart the NFS service, the exports command runs automatically to export your directories. If you want to export them immediately, you can do so by running exports from the command line (as root).

> TIP: It's a good idea to run the exports command after you change the exports file. If there are any errors in the file, exports will identify these errors for you. If you are not able to immediately access shares from clients, you might need to restart the NFS and portmap services.

Here’s an example of the exports command:

```
# /usr/sbin/exports -v
exporting maple:/pub
exporting spruce:/pub
exporting maple:/home
exporting spruce:/home
exporting :/media/win
```

The -a option indicates that all directories listed in /etc/exports should be exported. The -v option says to verbose output. In this example, the /pub and /home directories from the local server are immediately available for mounting by those client computers that are named (maple and spruce). The /media/win is available to all client computers.

Running the exports command makes your exported NFS directories available. Any changes to your /etc/export file will be used again the next time you reboot or otherwise restart the NFS service.

## Starting the nfs daemons

For security purposes, the NFS service is turned off by default on your Fedora or RHEL system. You can use the chkconfig command to turn on the NFS service so that your files are exported and the nfsd daemon are running when your system boots.

There are two startup scripts you want to turn on for the NFS service to work properly. NFS service exports files from (/etc/exports) and the nfs daemon listens for service requests. The nlock service starts the lockd daemon, which allows file locking to prevent multiple simultaneous use of critical files over the network.

> NOTE: If you see the message "Cannot register service: RPC: Unable to receive; errno= connection refused," you probably not need to start the portmap service on the client machine.

You can use the chkconfig command to turn on the NFS service by typing the following commands (as root user):

```
# chkconfig nfs on
```

The next time you start your computer, the NFS service will start automatically and your exported directories will be available. If you want to start the service immediately, waiting for a reboot, you can type the following:

```
# /etc/init.d/nfs start
```

The NFS service should now be running and ready to share directories with other computers on your network.

## Using NFS file systems

After a server exports a directory over the network using NFS, a client computer connects to its own file system using the mount command. The mount command is the same used to mount file systems from local hard disks, CDs, and USB flash drives. The options to mount are slightly different.

Mount can automatically mount NFS directories by editing the /etc/fstab file, as it does with local disks. NFS directories can also be added to the /etc/fstab file in such a way that are not automatically mounted. With a noauto option, an NFS directory listed in /etc/fstab is inactive until the mount command is used, after the system is up and running, to mount the file system.

## Manually mounting an NFS file system

If you know that the directory from a computer has been exported (that is, made available for mounting), you can mount that directory manually using the mount command. This is a good way to make sure that it is available and working before you set it up permanently. Here's an example of mounting the /home/chris/files directory from a computer named maple on your local computer:

```
# mkdir /media/maple
# mount maple:/home/chris/files /media/maple
```

The first command (mkdir) creates the mount point directory (/media is a common place to put put temporarily mounted disks and NFS file systems. The mount command identifies the remote computer and shared file system by a colon (maple:home/chris/files). Then, the local mount point follows (/media/maple).

> NOTE: If the mount failed, make sure the NFS service is running on the server and your firewall rules don't deny access to the service. From the server, type ps | grep nfs. You should see a list of nfs processes. If not follow as described in the previous section. View your firewall rules, type iptables -l (see Chapter 14 for a description of firewalls). By default, the nfs daemon listens for NFS requests on port number 2049.

To ensure that the mount occurred, here is an example of:

```
# host:directory mountpoint nfs options 0 0
```

(Note: The remaining text appears to be repetitive or garbled in the OCR source, but the logical flow follows the manual mounting process.)

