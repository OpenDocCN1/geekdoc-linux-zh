
## /etc/fstab

**filesystem (mount) table**

Contains a list of all mountable devices as specified by the system administrator. Programs do not write to this file but only read from it. Refer to “`fstab`: Keeps Track of Filesystems” on page 490.

## /etc/group

Groups allow users to share files or programs without giving all system users access to those files or programs. This scheme is useful when several users are working with files that are not public. The `/etc/group` file associates one or more user names with each group (number). Refer to “ACIs: Access Control Lists” on page 207 for another way to control file access.

An entry in the `/etc/group` file has four fields arranged in the following format:

`group-name:password:group-ID:login-name-list`

The *group-name* is the name of the group. The **password** is an optional encrypted password. This field frequently contains an x, indicating that group passwords are not used. The *group-ID* is a number, with 1–499 reserved for system accounts. The *login-name-list* is a comma-separated list of users who belong to the group. If an entry is too long to fit on one line, end the line with a backslash (\), which quotes the following RETURN, and continue the entry on the next line. A sample entry from a **group** file follows. The group is named `pubs`, has no password, and has a group ID of 503:

```
    pubs::x:503:alex, jenny, scott, hls, barbara
```

You can use the `groups` utility to display the groups that a user belongs to:

```
$ groups alex
    alex : alex pubs
```

Each user has a primary group, which is the group that user is assigned in the `/etc/passwd` file. By default, Fedora/RHEL users have private groups: Each user’s primary group has the same name as the user. In addition, a user can belong to other groups, depending on which *login-name-lists* the user appears on in the `/etc/group` file. In effect, you simultaneously belong both to your primary group and to any groups you are assigned to in `/etc/group`. When you attempt to access a file you do not own, the operating system checks whether you are a member of the group that has access to the file. If you are, you are subject to the group access permissions for the file. If you are not a member of the group that has access to the file and you do not own the file, you are subject to the public access permissions for the file.

When you create a new file, it is assigned to the group associated with the directory the file is being written into, assuming that you belong to that group. If you do not belong to the group that has access to the directory, the file is assigned to your primary group.

Refer to page 557 for information on using *system-config-users* to work with groups.

## /etc/hosts

The `/etc/hosts` file stores the name, IP address, and optional aliases of the other systems that the local system knows about. At the very least, this file must have the hostname and IP address that you have chosen for the local system and a special entry for localhost. This entry supports the *loopback service*, which allows the local system to talk to itself (for example, for RPC services). The IP address of the loopback service is always 127.0.0.1. Following is a simple /etc/hosts file for the system named rose with an IP address of 192.168.0.10:

```
$ cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1		rose localhost.localdomain localhost
192.168.0.1		bravo example.com		bravo
192.168.0.4		mpserver
192.168.0.5		workstation
192.168.0.10		rose
...
```

If you are not using NIS or DNS to look up hostnames (called *hostname resolution*), you must include in /etc/hosts all systems that you want the local system to be able to contact. The hosts entry in the /etc/nsswitch.conf file (page 455) controls the order in which hostname resolution services are checked.

## /etc/inittab

(RHEL) initialization table

Under RHEL, this file controls how the System V init process behaves. Fedora has replaced the System V init daemon with the Upstart init daemon; see page 417 for more information. Under Fedora, this file holds the initdefault line only. Each line in inittab contains four colon-separated fields:

id:runlevel:action:process

The *id* uniquely identifies an entry in the inittab file. The *runlevel* is the system run-level(s) at which *process* is executed. The *runlevel* consists of zero or more characters chosen from 0123456S. If more than one runlevel is listed, the associated *process* is executed at each of the specified runlevels. When you do not specify a runlevel, init executes *process* at all runlevels. When the system changes runlevels, the *processes* specified by all entries in inittab that do not include the new runlevel are sent the SIGTERM signal to allow them to terminate gracefully. After 5 seconds, these *processes* are killed with SIGKILL if they are still running. The *process* is any bash command line.

The *action* is one of the following keywords: respawn, wait, once, boot, bootwait, ondemand, powerfail, powerwait, powerokwait, powerfailnow, ctlaltdel, kbrequest, off, ondemand, initdefault, or sysinit. This keyword controls how the *process* is treated when it is executed. The most commonly used keywords are wait and respawn.

The *wait* keyword instructs init to start the *process* and wait for it to terminate. All subsequent scans of inittab ignore this wait entry. Because a *wait* entry is started only once (on entering *runlevel*) and is not executed again while the system remains at *runlevel*, it is often used to redirect init output to the console.

The *respawn* entry tells init to start the *process* if it does not exist but not to wait for it to terminate. If the *process* does exist, init moves on to the next entry in inittab.

The init utility continues to rescan inittab, looking for processes that have died. When a process dies, a respawn entry causes init to restart it.

The initedefault entry tells init which runlevel to bring the system to when it boots (see Table 11-1 on page 424). Without this information, init prompts for a runlevel on the system console. The value of the initedefault entry is set when you configure the system or when you edit inittab directly. By default, Fedora/RHEL sets initedefault to 5, which causes the system to come up in graphical multiuser mode.

### Use caution when you edit inittab

> Be careful when you edit inittab manually. Always make a backup copy in the same directory before you edit this file. If you make a mistake, you may not be able to boot the system. If you cannot boot the system, refer to “Rescue Mode” on page 411.

Each virtual console (page 137) has an inittab mingetty entry that includes a unique terminal identifier (such as tty1, which is short for /dev/tty1). You can add or remove mingetty lines to add or remove virtual consoles. Remember to leave a virtual console for each X window that you want to run. Following is the mingetty entry for /dev/tty2:

```
2:2345:respawn:/sbin/mingetty tty2
```

The id on a mingetty line corresponds to the tty number.

All of the actions are documented in the inittab man page. For more information refer to “Booting the System” on page 425.

## /etc/motd

Contains the message of the day, which can be displayed each time someone logs in using a textual login. This file typically contains site policy and legal information. Keep this file short because users tend to see the message many times.

## /etc/mtab

When you call mount without any arguments, it consults this file and displays a list of mounted devices. Each time you (or an init script) call mount or umount, these utilities make the necessary changes to mtab. Although this is an ASCII text file, you should not edit it. See also /etc/fstab.

### Fixing mtab

> The operating system maintains its own internal mount table in /proc/mounts. You can use cat to display the contents of /proc/mounts so that you can review the internal mount table. Sometimes the list of files in /etc/mtab may not be synchronized with the partitions in this table. To bring the mtab file in line with the operating system’s mount table, you can either reboot the system or replace /etc/mtab with a symbolic link to /proc/mounts (some information may be lost).

```
# rm /etc/mtab
# ln -s /proc/mounts /etc/mtab
```

## /etc/netgroup

Defines netgroups, which are used for checking permissions when performing remote logins and remote mounts and when starting remote shells.
