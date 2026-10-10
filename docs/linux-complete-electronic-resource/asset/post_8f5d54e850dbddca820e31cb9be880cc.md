
# SHOWRC

Running `rpm --showrc` shows the values RPM will use for all of the options that may be set in *rpmrc* files.

# FTP OPTIONS

RPM includes a simple FTP client to simplify installing and querying packages which are available over the Internet. Package files for install, upgrade, and query operations may be specified as an ftp style URL:

```
ftp://<user>:<password>@hostname/path/to/package.rpm
```

If the **@password** portion is omitted, the password will be prompted for (once per user/hostname pair). If both the user and password are omitted, anonymous ftp is used. In all cases passive (PASV) ftp transfers are used.

RPM allows the following options to be used with ftp URLs:

- `--ftp-proxy <hostname>` The host <hostname> will be used as a proxy server for all transfers, which allows users to ftp through firewall machines which use proxy systems. This option may also be specified in an *rpmrc* file.
- `--ftport <port>` Specifies the TCP port number to use for the ftp connection instead of the default port. This option may also be specified in an *rpmrc* file.

# FILES

- /etc/rpmrc
- /.rpmrc
- ./var/lib/rpm/packages
- ./var/lib/rpm/pathidx
- ./var/lib/rpm/nameidx
- ./tmp/rpm*

# SEE ALSO

*glint(8)*, *rpm2cpio(8)*, *http://www.redhat.com/rpm*

# AUTHORS

Marc Ewing `<marc@redhat.com>`
Erik Troan `<ewt@redhat.com>`

# SHUTDOWN(8)

## NAME

**shutdown** - Bring the system down.

## SYNOPSIS

/sbin/**shutdown** `[-t sec] [-rkhncf] time [warning-message]`

## DESCRIPTION

**Shutdown** brings the system down in a secure way. All logged in users are notified that the system is going down, and *login(1)* is blocked. It is possible to shut the system programs immediately, or after a delay. All processes are first notified that the system is going down by the signal SIGTERM. This gives programs like *vi(1)* the time to save the file being edited, mail and news processing programs a chance to exit cleanly, etc. **Shutdown** does it's job by signalling the **init** process, asking it to change the *runlevel*. **Runlevel 0** is used to halt the system, **runlevel 6** is used to reboot the system and **runlevel 1** is used to put the system into a state where administrative tasks can be performed; this is the default if neither the *-h* or *-r* flag is given to **shutdown**. To see which actions are taken on halt or reboot see the appropriate entries of these *runlevels* in the file */etc/inittab*.

## OPTIONS

- `-t sec`
  Tell init to wait *sec* seconds between sending processes the warning and the kill signal, before changing to another *runlevel*.
- `-k`
  Don't really shutdown; only send the warning messages to everybody.
- `-r`
  Reboot after shutdown.
- `-h`
  Halt after shutdown.
- `-n`
  [DEPRECATED] Don’t call init to do the shutdown but do it ourselves. The use of this option is discouraged, and its results are not always what you’d expect.
- `-f`
  Do a ‘fast’ reboot.
- `-c`
  Cancel an already running shutdown. With this option it is, of course, not possible to give the **time** argument, but you can enter an explanatory message on the command line that will be sent to all users.
- *time*
  When to shutdown.
- *warning-message*
  Message to send to all users.

The *time* argument can have different formats. First, it can be an absolute time in the format *hh:mm*, in which *hh* is the hour (1 or 2 digits) and *mm* is the minute of the *hour* (in two digits). Second, it can be in the format **+m**, in which *m* is the number of minutes to wait. The word **now** is an alias for **+0**.

The *-f* flag means ‘reboot fast’. This only creates an advisory file */fastboot* which can be tested by the system when it comes up again. The boot *rc* file can test if this file is present, and decide not to run *fsck*(1) since the system has been shut down in the proper way. After that, the boot process should remove */fastboot*.

The *-n* flag causes *shutdown* not to call *init*, but to kill all running processes itself. After all processes are killed, *shutdown* will try to run the script */etc/rc.d/rc.halt* *fast* (or *rc.reboot*). It also tests for the presence of the equivalent files *rc.0* and *rc.6*. If this script returns or can’t be executed (because it’s not present for example) *shutdown* will turn off *quota* and *accounting*, turn off *swapping* and *unmount* all filesystems.

## ACCESS CONTROL

*Shutdown* can be called from *init*(8) when the magic keys **CTRL-ALT-DEL** are pressed, by creating an appropriate entry in */etc/inittab*. This means that everyone who has physical access to the console keyboard can shut the system down. To prevent this, *shutdown* can check to see if an authorized user is logged in on one of the virtual consoles. If **shutdown** is called from **init**, it checks to see if the file */etc/shutdown.allow* is present. It then compares the login names in that file with the list of people that are logged in on a virtual console (from */var/run/utmp*). Only if one of those authorized users **or** **root** is logged in, it will proceed. Otherwise it will write the message

> shutdown: no authorized users logged in

to the (physical) system console. The format of */etc/shutdown.allow* is one user name per line. Empty lines and comment lines (prefixed by a **#**) are allowed. Currently there is a limit of 32 users in this file.

## FILES

- /fastboot
- /etc/inittab
- /etc/rc.d/rc.halt
- /etc/rc.d/rc.reboot
- /etc/shutdown.allow

## BUGS

Not really a bug, but most users forget to give the *time* argument and are then puzzled by the error message **shutdown** produces. The *time* argument is mandatory; in 90 percent of all cases this argument will be the word **now**.

## AUTHOR

Miquel van Smoorenburg <miquels@cistron.nl>

## SEE ALSO

fsck(8), init(1), halt(8), reboot(8)

# USERADD(8)

## NAME

**useradd** - Create a new user or update default new user information.

## SYNOPSIS

```
useradd  [-A {method|DEFAULT},... ] [-c comment]
       [-d home_dir]
       [-e expire_date] [-f inactive_time] [-g initial_group]
       [-G group[,...]] [-m [-k skeleton_dir] | -M] [-s shell]
       [-u uid [-o]] [-n] [-r] login
useradd  -D [-g default_group] [-b default_home]
       [-f default_inactive] [-e default_expiration]
       [-s default_shell]
```

## DESCRIPTION

### CREATING NEW USERS

When invoked without the -D option, the useradd command creates a new user account using the values specified on the command line and the default values from the system. The new user account will be entered into the system files as needed, the home directory will be created, and initial files copied, depending on the command line options. The version provided with Red Hat Linux will create a group for each user added to the system, unless -n option is given. The options which apply to the useradd command are

- `-A {method|DEFAULT},...` The value of the user’s authentication method. The authentication method is the name of a program which is responsible for validating the user’s identity. The string DEFAULT may be used to change the user’s authentication method to the standard system password method. This is a comma-separated list of program names. It may include DEFAULT exactly once.
- `-d home_dir` The new user will be created using home_dir as the value for the user’s login directory. The default is to append the login name to default_home and use that as the login directory name.
- `-e expire_date` The date on which the user account will be disabled. The date is specified in the format MM/DD/YY.
- `-f inactive_days` The number of days after a password expires until the account is permanently disabled. A value of 0 disables the account as soon as the password has expired, and a value of -1 disables the feature. The default value is -1.
- `-g initial_group` The group name or number of the user's initial login group. The group name must exist. A group number must refer to an already existing group. The default group number is 1.
- `-G group[,...]` A list of supplementary groups which the user is also a member of. Each group is separated from the next by a comma, with no intervening whitespace. The groups are subject to the same restrictions as the group given with the -g option. The default is for the user to belong only to the initial group.
- `-m` The user's home directory will be created if it does not exist. The files contained in skeleton_dir will be copied to the home directory if the -k option is used, otherwise the files contained in /etc/skel will be used instead. Any directories contained in skeleton_dir or /etc/skel will be created in the user's home directory as well. The -k option is only valid in conjunction with the -m option. The default is to not create the directory and to not copy any files.
- `-M` The user home directory will not be created, even if the system wide settings from /etc/login.defs is to create home dirs.
- `-n` A group having the same name as the user being added to the system will be created by default. This option will turn off this Red Hat Linux-specific behavior.
- `-r` This flag is used to create a system account. That is, an user with a UID lower than value of UID_MIN defined in /etc/login.defs. Note that useradd will not create a home directory for such an user, regardless of the default setting in /etc/login.defs. You have to specify -m option if you want a home directory for a system account to be created. This is an option added by Red Hat.
- `-s shell` The name of the user's login shell. The default is to leave this field blank, which causes the system to select the default login shell.
- `-u uid` The numerical value of the user's ID. This value must be unique, unless the -o option is used. The value must be
