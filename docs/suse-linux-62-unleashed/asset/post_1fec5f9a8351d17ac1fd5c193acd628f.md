
# System Service Tools
CHAPTER 6

Also, they are not automatically added when an ordinary user executes the su (superuser/substitute user) command. After an su command, you will see the # prompt, but many root-only commands will be apparently unavailable; they are simply not in your path. Use the following code to fix this:

```bash
# PATH=/sbin:/usr/bin:${PATH}; export PATH
```

You can also use the - or login shell option to inherit the root operator environment:

```bash
# su -
```

## Configuration Files in /etc

The /etc directory is normally used to store system-wide configuration files required by many programs. Some of the important files in /etc are as follows:

- passwd
- shadow
- fstab
- group
- hosts
- inittab
- motd
- profile
- shells
- services
- lilo.conf

The first two files in this list, /etc/passwd and /etc/shadow, define the authorized users for a system. The /etc/passwd file contains all of the information about a user except the encrypted password, which is contained in /etc/shadow for security reasons. The password information in /etc/shadow was previously incorporated into /etc/passwd, which is a world-readable file. This was reasonably safe because the passwords were irreversibly encrypted. Nevertheless, a number of unfortunate incidents, especially the Morris Internet Worm, convinced people that a separate /etc/shadow file, readable only by root, was necessary.

SuSE recommends that you not manually edit these files, especially for changing user information. To add or change user information, use the yast command.

The next file on the list, /etc/fstab, contains a list of devices the system knows how to mount automatically. This file is known as the filesystem table. A typical SuSE Linux fstab for a PC with a single-partition filesystem may look like the following:

```
/dev/sda6 swap swap defaults 0 0
/dev/sda1 / ext2 defaults 1 1
/dev/hdc /cdrom iso9660 ro,noauto,user 0 0
/dev/fd0 /floppy auto noauto,user 0 0
none /proc proc defaults 0 0
```
# End of YaST-generated fstab lines

Each line defines a complete, split into fields and separated by whitespace, as many other Linux and UNIX configuration files. The first entry for the root partition, /dev/sda1, indicates the device to mount in the file name hierarchy. The next field, ext2, indicates what type of filesystem the device contains, while the rest of the line contains mount options, meaning depends on the particular type of filesystem being mounted. In the case of ext2 entries, the numbers following the default indicate the actions and priorities for performing the potentially time-consuming file check (fsck) during system boot. The option noauto means not to mount the system automatically during boot. This option is important for removable media, such as floppy disks and CD-ROMs. See the mount command's man for further details.

/etc/hosts file contains a list of IP addresses and the corresponding hostnames (aliases). This list is used to resolve the IP address of a machine when its name is given. A sample entry might look like the following:

```
# IP hostname alias
192.168.1.34 localhost home.org
```

/etc/motd is the file in which the system administrator puts the message of the day (hence the name motd). Usually it contains information related to the system downtime or upgrades of software, but it can contain anything. The default content of this file for SuSE Linux is a lot of fun...

/etc/profile is the default initialization file for users whose shell is either ksh, or bash (the default shell). It is mostly used for settings such as PATH and umask (the discussion of umask command in the bash documentation). The /etc/shells file also pertains to shells. It is a list of "approved" shells. One primary uses is to prevent people from accidentally changing their shells to something unusable, although any program can set up a user's shell in /etc/passwd to launch login:

/etc/services contains a list of symbolic names of well known ports used by various services. The entries will look something like the following:

```
telnet 23/tcp
www 80/tcp
```
The first field (telnet) is the name of the service, the second field is the port on which service runs (23), and the final field (tcp) is the type of service. From the preceding lines you can see that Telnet runs on port 23, and HTTP runs on port 80, which are the standard ports for those services.

The last file on the list is /etc/lilo.conf. This file contains a description of the system's behavior at boot time, with a list of all the bootable images on the system (see Chapter 3 for more information). In addition to the files discussed, many other configuration files are found in the /etc directory, especially SuSE's rc.config. Many of the settings in these files are automatically created, changed, and saved by the yast command.

## /home

The /home directory is where all home directories for all users on a system are stored. Although other Linux distributions may use the /home directory for pseudo-users, such as ftp or httpd, these directories are placed under /usr/local in the SuSE system.

## /mnt

By convention, the /mnt directory is the directory under which other filesystems—such as DOS, network-mounted NFS filesystems, or removable media such as CD-ROMs, floppy disks, Zip disks, or Jaz disks—are mounted. SuSE Linux, however, uses the /floppy and /cdrom directories by default for those media. You do not have this approach and can use /etc/fstab for the more traditional /mnt directory. However, you'll need to create the new directories under /mnt. In a system with multiple CD-ROM drives, the names might be modified to include cdrom0, cdrom1, and so on. By using subdirectories under /mnt to house all of your mounted media, you keep the /directory clean. Judicious use of symbolic links can be very useful to disguise the actual mount point of disks, so that, for instance, /home/smith is

## /tmp and /var

The /tmp and /var directories are used to hold temporary files or files with constantly varying content. The /tmp directory is usually a dumping ground for files that only need to be used briefly and afford to be deleted at any time. It is quite unstructured. On a multiuser system, most users abide by the convention of creating a personal directory (named the same as their username) in /tmp for storing their temporary files. The most common use of /tmp (other than as a location for throwaway files) is as starting point for building and installing programs.

Some versions of UNIX used to place logic in the boot sequence to clean out /tmp every time a system was booted. This is no longer common, but some systems (such as SuSE) do periodic cron jobs that discard items in /tmp and /usr/tmp that have not been accessed or modified recently. Under SuSE Linux, the /usr/tmp directory is a link to the /var/tmp directory.

## /var

The /var directory is used by various core system services to store constantly changing, and sometimes growing, files. A prime example is the spool subdirectory, which contains various types of queues, such as the unsent mail queue, the print job queue, pending batch and scheduled jobs, and UUCP traffic. Another important subdirectory is /var/run, which contains the process IDs of various running system services. It is sometimes better to look in /var/run than to fish through the process table if you're in a hurry to kill a rogue process.
