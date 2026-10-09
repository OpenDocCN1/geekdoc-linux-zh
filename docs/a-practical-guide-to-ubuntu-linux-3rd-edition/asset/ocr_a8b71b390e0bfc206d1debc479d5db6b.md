you gave the **su** command. When you give the command **su -** (you can use `~l` or `--login` in place of the hyphen), you get a **root** login shell: It is as though you logged in as **root**. Not only do the shell's user and group IDs match those of **root**, but the environment is identical to that of **root**. The login shell executes the appropriate startup files (page 293) before displaying a prompt.

The id utility displays the changes in your user and group IDs and in the groups you are associated with:

```
$ id
 uid=1002(sam) gid=1002(sam) groups=117(admin),1002(sam)
$ su
 Password:
# id
 uid=0(root) gid=0(root) groups=0(root)
```

You can use su with the `-c` option to run a command line with **root** privileges, returning to the original shell when the command finishes executing. The following example first shows that a user is not permitted to kill (page 455) a process. With the use of **su -c** and the **root** password, however, the user is permitted to kill the process. The quotation marks are necessary because **su -c** takes its command as a single argument.

```
$ kill -15 4982
 -bash: kill: (4982) - Operation not permitted
$ su -c "kill -15 4982"
 Password:
$
```

**Superuser, PATH, and security**

> The fewer directories you keep in **PATH** when you are working as **root**, the less likely you will be to execute an untrusted program as **root**. *Never include the working directory in* **PATH** (as, *, or:* any*where in* **PATH**, *or: as the last element of* **PATH**). For more information refer to “PATH: Where the Shell Looks for Programs” on page 319.

# THE UPSTART EVENT-BASED INIT DAEMON

Because the traditional System V **init** daemon (SysVinit) does not deal well with modern hardware, including hotplug (page 502) devices, USB hard and flash drives, and network-mounted filesystems, Ubuntu replaced it with the Upstart **init** daemon (upstart.ubuntu.com and upstart.ubuntu.com/wiki).

Several other replacements for SysVinit are also available. One of the most prominent is **init** (initing.sourceforge.net/trac). In addition, Solaris uses **SMF** (Service Management Facility) and macOS uses **launchd**. Over time, Ubuntu will incorporate features of each of these systems into Upstart.

The runlevel-based SysVinit daemon uses runlevels (recovery/single-user, multi- user, and more) and links from the /etc/rc.d/ directories to the init scripts in