
is assumed to be valid for all run levels, 0 through 6.

Three other values, a, b and c, can also appear in the rstate field, even though they are not true run levels. Entries having these characters in the rstate field are processed only when a user init process requests them to be run (regardless of the current system run level). They differ from run levels in that boot init can never enter "run level" a, b, or c. Also, a request for the execution of any of these processes does not change the current numeric run level.

Furthermore, a process started by an a, b, or c option is not killed when boot init changes levels. A process is killed only if its line in inittab is marked off in the action field, its line is deleted entirely from inittab, or boot init goes into the single-user state.

## action
A keyword in this field tells boot init how to treat the process specified in the process field. The following actions can be specified:

- **boot**
Process the entry only at boot init's boot-time read of the inittab file. Boot init starts the process, does not wait for its termination, and when it dies, does not restart the process. In order for this instruction to be meaningful, the rstate should be the default or it must match boot init's run level at boot time. This action is useful for an initialization function following a hardware boot of the system.

- **bootwait**
Process the entry only at boot init's boot-time read of the inittab file. Boot init starts the process, waits for its termination, and, when it dies, does not restart the process.

- **initdefault**
An entry with this action is only scanned when boot init is initially invoked. Boot init uses this entry, if it exists, to determine which run level to enter initially. It does this by taking the highest run level specified in the rstate field and using that as its initial state. If the rstate field is empty, boot init enters run level 6.
The initdefault entry cannot specify that boot init start in the single-user state. Additionally, if boot init does not find an initdefault entry in inittab, it requests an initial run level from the user at boot time.

- **off**
If the process associated with this entry is currently running, send the warning signal (SIGTERM) and wait 20 seconds before forcibly terminating the process via the kill signal (SIGKILL). If the process is nonexistent, ignore the entry.

- **once**
When boot init enters a run level that matches the entry's rstate, start the process and do not wait for its termination. When it dies, do not restart the process. If boot init enters a new run level but the process is still running from a previous run level change, the process is not restarted.

- **ondemand**
This instruction is really a synonym for the respawn action. It is functionally identical to respawn but is given a different keyword in order to divorce its association with run levels. This is used only with the a, b, or c values described in the rstate field.

- **powerfail**
Execute the process associated with this entry only when boot init receives a power-fail signal (SIGPWR; see signal(5)).

- **powerwait**
Execute the process associated with this entry only when boot init receives a power-fail signal (SIGPWR) and wait until it terminates before continuing any processing of inittab.

- **respawn**
If the process does not exist, start the process; do not wait for its termination (continue scanning the inittab file). When it dies, restart the process. If the process currently exists, do nothing and continue scanning the inittab file.

- **sysinit**
Entries of this type are executed before boot init tries to access the console. It is expected that this entry will be only used to initialize devices on which boot init might attempt to obtain run level information. These entries are executed and waited for before continuing.

- **wait**
When boot init enters the run level that matches the entry's rstate, start the process and wait for its termination. Any subsequent reads of the inittab file while boot init is in the same run level cause boot init to ignore this entry.

- **process**
This is a sh command to be executed. The entire process field is prefixed with exec and passed to a forked sh as "sh -c 'exec command". For this reason, any sh syntax that can legally follow exec can appear in the process field. Comments can be inserted by using the # /comment syntax.

## WARNINGS

The use of a four-character id is strongly recommended. Many pty servers use the last two characters of the pty name as an id. If an id chosen by a pty server collides with one used in the inittab file, the /etc/utmp file can become corrupted. A corrupt /etc/utmp file can cause commands such as who to report inaccurate information.

## FILES

/etc/inittab File of processes dispatched by boot init.

## SEE ALSO

sh(1), getty(1M), exec(2), open(2), signal(5).

# mount

**mount - List mounted file systems or mount file systems.**

```
mount(1M)              mount(1M)

NAME
  mount (generic), umount (generic) - mount and unmount file systems

SYNOPSIS
  /usr/sbin/mount [-l] [-p|-v]
  /usr/sbin/mount -a [-F FStype] [-eQ]
  /usr/sbin/mount [-F FStype] [-eQrV] [-o specific_options]
  {special|directory}
  /usr/sbin/mount [-F FStype] [-eQrV] [-o specific_options]
  special directory
  /usr/sbin/umount [-v] [-V] {special|directory}
  /usr/sbin/umount -a [-F FStype] [-v]

DESCRIPTION
  The mount command mounts file systems. Only a superuser can mount
  file systems. Other users can use mount to list mounted file systems.

  The mount command attaches special, a removable file system, to
  directory, a directory on the file tree. directory, which must
  already exist, will become the name of the root of the newly mounted
  file system. special and directory must be given as absolute path
  names. If either special or directory is omitted, mount attempts to
  determine the missing value from an entry in the /etc/fstab file.
  mount can be invoked on any removable file system, except /.

  If mount is invoked without any arguments, it lists all of the mounted
  file systems from the file system mount table, /etc/mnttab.

  The umount command unmounts mounted file systems. Only a superuser
  can unmount file systems.
```

## Options (mount)

The mount command recognizes the following options:

- **-a**
Attempt to mount all file systems described in /etc/fstab. All optional fields in /etc/fstab must be included and supported. If the -F option is specified, all file systems in /etc/fstab with that FStype are mounted. File systems are not necessarily mounted in the order listed in /etc/fstab.

- **-e**
Verbose mode. Write a message to the standard output indicating which file system is being mounted.

- **-F FSType**
Specify FSType, the file system type on which to operate. See *fstyp*(1M). If this option is not included on the command line, then it is determined from either */etc/fstab*, by matching special with an entry in that file, or from file system statistics of special, obtained by statfsdev() (see *statfsdev*(3C)).

- **-l**
Limit actions to local file systems only.

- **-o specific_options**
Specify options specific to each file system type. specific_options is a list of comma separated suboptions and/or keyword/attribute pairs intended for a FSType-specific version of the command. See the FSType-specific manual entries for a description of the specific_options supported, if any.

- **-P**
Report the list of mounted file systems in the */etc/fstab* format.

- **-Q**
Prevent the display of error messages that result from an attempt to mount already mounted file systems.

- **-r**
Mount the specified file system as read-only. Physically write-protected file systems must be mounted in this way or errors occur when access times are updated, whether or not any explicit write is attempted.

- **-v**
Report the regular output with file system type and flags; however, the directory and special fields are reversed.

- **-V**
Echo the completed command line, but perform no other action. The command line is generated by incorporating the user-specified options and other information derived from */etc/fstab*. This option allows the user to verify the command line.

## Options (umount)

The *umount* command recognizes the following options:

- **-a**
Attempt to umount all file systems described in */etc/mntab*. All optional fields in */etc/mntab* must be included and supported. If FSType is specified, all file systems in */etc/mntab* with that FSType are umounted. File systems are not necessarily umounted in the order listed in */etc/mntab*.

- **-F FSType**
Specify FSType, the file system type on which to operate. If this option is not included on the command line, then it is determined from */etc/mntab* by matching special with an entry in that file. If no match is found, the command fails.

- **-v**
Verbose mode. Write a message to standard output indicating which file system is being umounted.
