
## Using the Network File System

*Network File System (NFS)* is the protocol developed by Sun Microsystems that allows computers to use a remote file system as if it were a real part of the local machine. A common use of NFS is to allow users home directories to appear on every local machine they use, thus eliminating the need to have physical home directories. This opens up hot desking and other flexible working arrangements, especially because no matter where the user is, his home directory follows him around.

Another popular use for NFS is to share binary files between similar computers. If you have a new version of a package that you want all machines to have, you have to upgrade only on the NFS server, and all hosts running the same version of Ubuntu will have the same upgraded package.

## Installing and Starting or Stopping NFS

NFS is not installed by default on Ubuntu, so you need to install the nfs-common, nfs-kernel-server, and portmap packages. NFS itself consists of several programs that work together to provide the NFS server service. One is rpc.portmapper, which maps NFS requests to the correct daemon. Two others are rpc.nfsd, which is the NFS daemon, and rpc.mountd, which controls the mounting and unmounting of file systems.

Ubuntu automatically adds NFS to the system startup scripts, so it will always be available after you have configured it. To check this, use the command sudo /etc/init.d/nfs-kernel-server status and it will show you that the service is running. If you need to manually start the NFS server, use the following command:

```
$ sudo /etc/init.d/nfs-kernel-server start
Starting NFS services:          [ OK ]
Starting NFS quotas:            [ OK ]
Starting NFS daemon:            [ OK ]
Starting NFS mounted:           [ OK ]
```

In this example, NFS has been started. Use the stop keyword instead to stop the service, or restart to restart the server. This approach to controlling NFS proves handy, especially after configuration changes have been made. See the next section on how to configure NFS support on your Ubuntu system.

## NFS Server Configuration

You can configure the NFS server by editing the /etc/exports file. This file is similar to the /etc/fstab file in that it is used to set the permissions for the file systems being exported. The entries look like this:

```
/file/system yourhost(options) *.yourdomain.com(options) 192.168.0.0/24(options)
```

This shows three common clients to which to share /file/system. The first, yourhost, shares /file/system to just one host. The second, *.yourdomain.com, uses the asterisk (*) as a wildcard to enable all hosts in yourdomain.com to access /file/system. The third share enables all hosts of the Class C network, 192.168.0.0, to access /file/share. For security, it is best not to use shares like the last two across the Internet because all data will be readable by any network the data passes by.

### TABLE 16.1 /etc/fstab Options

| Option | Purpose |
| --- | --- |
| rw | Gives read and write access |
| ro | Gives read-only access |
| async | Writes data when the server, not the client, feels the need |
| sync | Writes data as it is received |

The following is an example of an /etc/exports file:

```
# /etc/exports: the access control list for filesystems which may be exported
# to NFS clients. See exports(5).
/home/andrew 192.168.0.0/24(rw,no_root_squash)
```

This file exports (makes available) /home/andrew to any host in 192.168.0.* and allows users to read from and write to /home/andrew.

After you have finished with the /etc/exports file, the following command

```
$ sudo exportfs -a
```

exports all the file systems in the /etc/exports file to a list named xtab under the /var/lib/nfs directory, which is used as a guide for mounting when a remote computer asks for a directory to be exported. The -r option to the command reads the entire /etc/exports file and mounts all the entries. You can also use the exportfs command to export specific files temporarily. Here's an example using exportfs to export a file system:

```
/usr/sbin/exportfs -o async yourhost:/usr/tmp
```

This command exports /usr/tmp to yourhost with the async option.

Be sure to restart the NFS server after making any changes to /etc/exports. If you prefer, you can use Ubuntu's shares-admin graphical client to set up NFS while using the X Window System. Start the client by clicking the System menu and then selecting the Shared Folders menu item from the Administration menu.

After you press Enter, you are prompted for your password. Type in the password and click OK; the main window will then display. Click the Add button to open the Add Share dialog box, as shown in Figure 16.1.
