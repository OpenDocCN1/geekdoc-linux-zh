
The path to the **ypinit** program may be different on your UNIX system. Check the path if the command produces an error message when trying to execute.

When the **ypinit** command executes, it scans all the NIS files named in the file /var/yp and produces the NIS maps that are used by the client processes. The /var/yp file may have a different directory name on some systems, such as SCO UNIX, which uses /etc/yp as a directory for all NIS files. Check your UNIX system documentation or man pages for proper file locations. The /var/yp file contains a list of all the maps to be generated, and you will usually not have to make any changes at all to this file.

A new directory (usually called /var/yp/*domainname*, where *domainname* is the NIS domain name) is created. The maps are placed in this new domain name. If you are setting up more than one domain all handled by the same NIS master machine, the maps for each domain will be beneath the domain name's subdirectory.

As the last step in **ypinit**, you are asked which machines are NIS slave servers, at which point you should enter their names. The slave names are saved in a file in the domain directory.

> **TIP**
> On some versions of Linux, the NIS utilities are not in the same directories mentioned throughout this chapter. A few versions move them to other locations. To verify the proper locations, use the **find** command with the program name.

After the maps have been generated properly, you can start the **ypserv** daemon. It is best to automate the startup by editing the startup rc files to do this for you when the machine boots. There is a section in an rc file (usually the one that starts RPC) that looks like this:

```bash
if [ -f /etc/yp/ypserv -a -d /var/yp/`domainname` ]
    then
        /etc/yp/ypserv
    fi
```

This script checks for the existence of the directory /var/yp/*domainname*, where *domainname* is the domain name for your NIS domain. The entry on the first line where *domainname* is located must be in single back quotes, which means the shell should execute the domainname command and use the results. If the directory exists, the **ypserv** daemon is started. You should replace the directory paths with those used by your UNIX system.

To manually start the ypserv daemon, log in as root and issue the following command, or whatever the path to your ypserv daemon is:

/etc/yp/ypserv

Next, you need to start the ypbind daemon on the server too (otherwise ypserv can't find the maps). Again, this is usually done through the rc startup scripts with an entry like this:

```bash
if [ -d /var/yp ]
then
    /etc/yp/ypbind
fi
```

Again, you should check that the directory path is correct. You can start the ypbind daemon manually by issuing it on the command line when logged in as root. Make sure the directory path is correct when you do so.

If you want to perform a quick test of the NIS daemons, issue a command like this one at the command line:

ypmatch tparser passwd

The ypmatch command asks NIS to use the maps to match up the next argument with the map of the third argument's name. In this example, ypmatch is instructed to look in the passwd file (passwd is the alias to passwd.byname) for the entry for tparser. You should get back the line that matches. Use any combination of map alias and entry you know exists in order to test the NIS server daemon.

## Setting Up NIS Slaves

In order to set up an NIS slave, the NIS master must be configured and running. When you are sure the master is operational, log in as root to the machine to be set up as the NIS slave. The domain name of the slave must be properly set before the configuration can proceed, so check the startup rc commands for the entry that sets the domainname variable or use the domainname command to set the domain name.

To set up the NIS slave and propagate the NIS files from the master to the slave, issue the following command, substituting for whatever path is correct on your system:

/etc/yp/ypbind

Check that the binding to the master is correct by issuing the `ypwhich` command. It should return the NIS master name.

Finally, issue this command, where the path is correct and servername is the name of your NIS master:

```bash
/etc/yp/ypinit -s servername
```

The `ypbind -s` option sets the local machine up as a slave. The `ypbind` command sets up directories on the local machine and transfers all the maps from the master to the slave.

After the setup is complete, you can test the slave setup with the `ypmatch` command as shown in the previous section.

To update the maps on the slaves at regular intervals, the `ypxfer` command is used on the slave, followed by the name of the map to be transferred. For example, this command transfers the `passwd.byname` file from the master to the slave:

```bash
ypxfer passwd.byname
```

Most administrators either create a set of cron entries for transferring all the NIS files at regular intervals (such as nightly) or use a script file executed by a network administrator.

## Setting Up NIS Clients

Setting up an NIS client requires that you have the domain name set properly, either with the `domainname` command or an entry in the rc start up files, and that the `ypbind` command has been issued properly, and the NIS client is bound to the NIS server.

When an entry in the `/etc/passwd` or `/etc/group` file must be searched for a match, the local files are examined first, and then the server is queried if no match is found. In order to instruct your client to go to the NIS master to match a login, you need to add the following entry to the bottom of the `/etc/passwd` file:

```bash
+:::0:0:::
```

If you know the format of the `/etc/passwd` file entries, you will recognize this as a legal entry with no information specified. The plus sign in the username field is to instruct `ypbind` to query the NIS master. This is called a *marker entry*. The plus sign entry can be anywhere in the file. When it is reached, NIS is used, and the file is read as before if no match has been found.

## Summary

As you can see, setting up NIS is not overly difficult. The hardest part of the process is usually getting the files that NIS uses to generate maps into proper shape, removing old entries and ensuring that security is maintained. Setting up the master and a slave can take less than half an hour, as most of the steps are automated. Often, actually finding the paths to the NIS utilities is more complex than setting up the server! From here you can read more about:

- Setting up Network File System to share directories across entire networks in Chapter 43, "NFS."
- Setting up cron and at to automate background processing in Chapter 46, "cron and at."
- Setting up your own Internet server or WWW server in Chapter 47, "Setting up an Internet Site."

## Backups

*by Tim Parker*

### In This Chapter

- Why make backups? 754
- Backup logs 758
- Using tar for backups 759

# CHAPTER 45

There are three rules of system administration: 1) Backup!, 2) Backup!, and 3) Backup! Although this may sound trite, the number of people who have lost important or valuable data—not to mention all the configuration information they spend days correcting—is enormous. Even if you don’t have a tape drive or other backup storage device, you should get in the habit of backing up your data. This chapter looks at how to properly do backups.

Let’s begin by putting this chapter in context: if you run a system that has many users, network access, email, and so on, backups should be a very important aspect of the daily routine. If your system is used more for your own pleasure and not for any important files, then backups are not as important except as a way to recover your configuration and setup information. In either case, you should make backups—the only difference is the frequency with which you make them and how much effort you go to in order to generate backups.

### Why Make Backups?

A backup is a copy of the file system or files on part of a file system stored onto another medium that can be used later to re-create the original. In most systems, the medium used for backups is tape, but floppy disks or secondary and removable hard disks can also be used.

There are so many potential sources of damage to a modern computer system, they seem to overwhelm you at times. Damage to your hard disks and their file systems and data can occur from hardware failures, power interruptions, or badly typed commands. Having a backup is sometimes your only chance of getting lost information back. While the actual process of forcing yourself to make backups can be tiresome and time-consuming, this is often outweighed by the time required to recoup any lost information in case of problems. With utilities like *cron* available, the task of backing up can be made much easier, too.

Part of the potential for damage (and hence the need for backups) with Linux is the nature of an operating system itself. Since Linux is a multiuser and multitasking operating system, at any moment there are many system files open. At most millisecond increments, data is being written to or read from a hard disk (even when the system has no users on it or user-started background processes).

Also, Linux maintains a lot of information in memory about its current state and the state of the file systems. This information must be written to disk frequently. When CPU processes are interrupted, system files and tables can be lost from memory. Disk files can be left in a temporary state that doesn’t match the real file system status.
