
## Reference

- `mysqldump`—Dumps or backs up MySQL data or tables
- `pgaccess`—Accesses a PostgreSQL database server
- `pg_ctl`—Controls a PostgreSQL server or queries its status
- `psql`—Accesses PostgreSQL via an interactive terminal

- **http://www.mysql.com/**—This is the official website of the MySQL database server. Here you can find the latest versions as well as up-to-date information and online documentation for MySQL. You can also purchase support contracts here. You might want to look into this if you will be using MySQL in a corporate setting. (Many corporations balk at the idea of using software for which the company has no support contract in place.)
- **http://www.postgresql.org/**—This is the official website of the PostgreSQL database server. You are asked to select a mirror when you arrive at this site. After you select a mirror, you are taken to the main site. From there, you can find information on the latest versions of PostgreSQL and read the online documentation.
- **http://www.postgresql.org/docs/8.1/interactive/tutorial-start.html**—This interactive HTML documentation tree is a great place to get started with learning how to use PostgreSQL.
- **http://www.psql.com/**—This is a commercial company that provides fee-based support contracts for the PostgreSQL database.

## CHAPTER 19
# File and Print

In the early days of computing, file and printer sharing was pretty much impossible because of the lack of good networking standards and interoperability. If you wanted to use a printer connected to another computer, you had to save the file to a floppy disk and walk over.

Nowadays, both file and printer sharing have become second nature in a world where it is not unusual for someone to own more than one computer. Whether it be for sharing photographs among various computers, or having a central repository available for collaboration, file sharing is an important part of our information age. Alongside this is the need to be able to share printers; after all, no one wants to have to plug and unplug a computer to a printer just to print out a quick letter.

Whatever your reasons for needing to share files and printers across a network, you will find out how to do both in this chapter. It looks at how you can share files using the popular UNIX Network File System (NFS) protocol, as well as the more Windows-friendly Samba system. You will also find out how to configure network attached printers with interfaces such as JetDirect. The chapter covers both graphical and command-line tools, so you should find something to suit the way you work.

### Using the Network File System

NFS is the protocol developed by Sun Microsystems that allows computers to use a remote file system as if it were a real part of the local machine. A common use of NFS is to allow users' home directories to appear on every local machine they use, thus eliminating the need to have physical home directories. This opens up hot-desking and other flexible working arrangements, especially because no matter where the user is, his home directory follows him around.

Another popular use for NFS is to share binary files between similar computers. If you have a new version of a package that you want all machines to have, you have to do the upgrade only on the NFS server, and all hosts running the same version of Fedora will have the same upgraded package.

### IN THIS CHAPTER

- Using the Network File System
- Putting Samba to Work
- Network and Remote Printing with Fedora
- Using the Common UNIX Printing System GUI
- Console Print Control
- Avoiding Printer Support Problems
- Reference

### NFS Server Configuration

You configure the NFS server by editing the /etc/exports file. This file is similar to the /etc/fstab file in that it is used to set the permissions for the file systems being exported. The entries look like this:

```
/file/system yourhost(options) *.yourdomain.com(options) 192.168.2.0/24(options)
```

This shows three common clients to which to share /file/system. The first, yourhost, shares /file/system to just one host. The second, .yourdomain.com, uses the asterisk (*) as a wildcard to enable all hosts in yourdomain.com to access /file/system. The third share enables all hosts of the Class C network, 192.168.0.0, to access /file/share. For security, it is best not to use shares like the last two across the Internet because all data will be readable by any network the data passes by. Some common options are shown in Table 19.1.

**TABLE 19.1 /etc/exports Options**

| Option | Purpose |
| :--- | :--- |
| rw | Gives read and write access |
| ro | Gives read-only access |
| async | Writes data when the server, not the client, feels the need |
| sync | Writes data as it is received |

The following is an example of an /etc/exports file:

```
# /etc/exports file for myhost.mydomain.com
/usr/local yourhost(ro,show)
/home/ahudson *.yourdomain.com(rw,hide, sync)
```

This file exports (makes available) /usr/local to yourhost. The mount is read-only (which is good for a directory of binary files that don’t get written to). It also allows users on yourhost to see the contents of file systems that might be mounted on /usr/local. The second export mounts /home/ahudson to any host in yourdomain.com. It doesn’t allow subsidiary file systems to be viewed, but you can read and write to the file system.

After you have finished with the /etc/exports file, you will check to see whether the NFS service is started by using the command:

```
# service nfs status
```

If you see a message saying that services are stopped, issue the following command:

```
# service nfs start
```

and watch as the related NFS services are started. When the services are started, you can enter the command

```
# /usr/sbin/exportfs -r
```

to export all the file systems in the `/etc/exports` file to a list named `xtab` under the `/var/lib/nfs` directory, which is used as a guide for mounting when a remote computer asks for a directory to be exported. The `-r` option to the command reads the entire `/etc/exports` file and mounts all the entries. The `exportfs` command can also be used to export specific files temporarily. Here's an example of using `exportfs` to export a file system:

```
# /usr/sbin/exportfs -o async yourhost:/usr/tmp
```

This command exports `/usr/tmp` to `yourhost` with the `async` option.

Be sure to restart the NFS server after making any changes to `/etc/exports`. If you prefer, you can use Fedora's *system-config-nfs* graphical client to set up NFS while using X. Start the client by going to System, Administration, Server Settings, NFS.

After you press Enter, you are prompted for the root password. Type in the password and click OK, and you see the main window. Click the Add button, and you see the Add NFS Share dialog box, as shown in Figure 19.1.

![](img/34e72348d53ca54c2a1d9c871316691b_446_0.png)

FIGURE 19.1 Fedora's *system-config-nfs* client can be used to quickly set up local directories for export via NFS.

In the Directory text box, type a name of a directory to be exported; in the Host(s) text box, type a hostname or the IP address of a remote host that is to be allowed access to the directory. By default, a directory is exported as read-only, but you can choose read and write access by clicking either option in the Basic Permissions area of the dialog box. When finished, click the OK button, click the Apply button, and then use the File menu to quit.

### NOTE

As part of your configuration for using NFS, you might need to enable the port on your firewall. Go to System, Administration, Firewall to open the Firewall configuration utility. Check the box next to NFS4 and click Apply to apply the new firewall policy.

### NFS Client Configuration

To configure your host as an NFS client (to acquire remote files or directories), edit the /etc/fstab file as you would to mount any local file system. However, rather than use a device name to be mounted (such as /dev/sda1), enter the remote hostname and the desired file system to be imported. For example, one entry might look like this:

| Device | Mount Point | Type | Options | Freq | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| yourhost:/usr/local | /usr/local | nfs | nfsvers=4,ro | 0 | 0 |

### NOTE

If you use autofs on your system, you need to use proper autofs entries for your remote NFS mounts. See the section 5 man page for autofs.

The options column uses the same options as standard fstab file entries with some additional options, such as nfsvers=4, which specifies the fourth version of NFS. You can also use the mount command, as root, to quickly attach a remote directory to a local file system by using a remote host's name and exported directory. For example:

```
# mount -t nfs 192.168.0.11:/home/andrew \
/home/andrew/test/foo
```

After you press Enter, the entire remote directory appears on your file system. You can verify the imported file system by using the df command, like so:

```
# df
Filesystem 1K-blocks Used Available Use% Mounted on
/dev/mapper/Vol1Group00-LogVol00 73575592 58627032 11580752 85% /
/dev/sda1 101086 18697 77170 20% /boot
tmpfs 512724 0 512724 0% /dev/shm
192.168.0.11:/home/andrew 35740416 5554304 28341248 17% /home/andrew/test/foo
```
