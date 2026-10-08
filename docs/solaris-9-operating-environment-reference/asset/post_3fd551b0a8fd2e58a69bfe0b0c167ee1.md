
renice

1165

# Operands

ID A process ID, process group ID, or user name/user ID, depending on the option selected.

priority The value specified is taken as the actual system scheduling priority instead of as an increment to the existing system scheduling priority. Specifying a scheduling priority higher than that of the existing process can require appropriate privileges.

# Examples

The following example adjusts the system scheduling priority so that process IDs 987 and 32 have a lower scheduling priority.

```
castle% renice -n 5 -p 987 32
castle%
```

The following example adjusts the system scheduling priority so that group IDs 324 and 76 have a higher scheduling priority if the user has the appropriate privileges to raise the priority.

```
castle% renice -n 4 -g 324 76
castle%
```

The following example adjusts the system scheduling priority so that numeric ID 1002 and user ray have a lower scheduling priority.

```
castle% renice -n 4 -u 1002 ray
castle%
```

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of renice: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+ 0 Successful completion.
> 0 An error occurred.

# Files

/etc/passwd Map user names to user IDs.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNMcs |

# See Also

nice(1), passwd(1), priocntl(1), attributes(5), environ(5)

# reset — Establish or Restore Terminal Characteristics

Synopsis

```
/usr/ucb/reset [-] [-ec] [-I] [-kc] [-n] [-Q] [-r] [-s] [-m [indent]
test baudrate]: type... [type]
```

Description

See tset(1).

# return — Shell Built-in Function to Advance Beyond a Sequence of Steps

Synopsis

```
sh
return [n]
csh
* return [n]
```

Description

See exit(1).

# rksh — Korn Shell, a Standard/Restricted Command and Programming Language

Synopsis

```
/usr/bin/rksh [+ abCefhikmnoprstuvx] [+ o option]... [-c string]
arg...]
```

Description

See ksh(1).

# rlogin — Remote Login

Synopsis

```
/usr/bin/rlogin [-8EL] [-ec] [-1 username] hostname
```

# Description

Use login to establish a remote login session from your terminal to the remote system named hostname.

Host names are listed in the hosts database, which can be contained in the /etc/hosts file and /etc/inet/ipodes file—new in the Solaris 8 release—the Network Information Service (NIS) hosts map, the Internet name server, or a combination of these. Each host has one official name (the first name in the database entry) and, optionally, one or more nicknames. You can specify either official host names or nicknames as hostname.

> Note - The Network Information Service (NIS) was formerly known as Sun Yellow Pages (YP). The functionality of the two remains the same;

Each system can have a file /etc/hosts.equiv containing a list of trusted hosts with which it shares users. Users with the same username on both the local and remote system can invoke login from the systems listed in the remote /etc/hosts.equiv file without supplying a password. Individual users can set up a similar equivalence list with the file .hosts in their home directories. Each line in this file contains two names: hostname and a username separated by a space. In an user's remote .hosts file permits the remote username who is logged into hostname to log to the remote system as a user without supplying a password. If the name of the local host is not found in the /etc/hosts.equiv file on the remote system and the local username and hostname are not found in the remote system's .hosts file, then the remote system prompts for a password. Hosts names listed in /etc/hosts.equiv and .hosts files must be the official names listed in the hosts database: nicknames cannot be used in either of these files.

> Note - When a system is listed in hosts.equiv, its security must be as good as local security. One insecure system listed in hosts.equiv can compromise the security of the entire system.

For security reasons, the .hosts file must be owned either by the remote user or root.
The remote terminal type is the same as your local terminal type (as given in the TERM environment variable). The terminal or window size is also copied to the remote system if the server supports it, and changes in size are reflected well. All echoing takes place at the remote site so that the remote login is transparent. Flow control with Control-S and Control-Q and flushing of input and output on interrupts are handled properly.

> Note - This implementation can use only the TCP network service.

# Options

- Pass 8-bit data across the net instead of 7-bit data.
- Specify a different escape character, c for the line used to disconnect from the remote host.
- Stop any character from being recognized as an escape character.

# 1168

# login

-l username

Specify a different username for the remote login. If you do not use this option, the remote username used is the same as your local username.

-L Run the login session in printout mode.

# Escape Sequences

Lines that you type with the tilde character are escape sequences (you can change the escape character with the -e option).

~ Disconnect from the remote host. This action is not the same as a logout because the local host breaks the connection with no warning to the remote end.

~susp suspend the login session (only if you are using a shell with job control). susp is your suspend character, see tty(1).

~dsusp suspend the input half of login, but output is still seen (only if you are using a shell with job control). dsusp is your "deferred suspend" usually Control-Y; see tty(1).

# Operands

hostname The name of the remote system on which login establishes the remote login session.

# Files

/etc/passwd Contains information about users' accounts.

/etc/hosts Hosts database for IPv4 hosts. Starting with the Solaris 8 release, it's also a symbolic link to /etc/inet/hosts.

/etc/equiv List of trusted host names with shared user names.

/etc/inet/ipnodes Hosts database for IPv6 hosts. New in the Solaris 8 release.

/etc/nologin Message displayed to users attempting to log in during system shutdown.

$HOME/.hosts Private list of trusted hostname/username combinations.

/usr/hosts/* For host-name version of the command.

# rm, rdir

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNwcmd |

# See Also

- rsh(1), stty(1), tty(1), in.named(1), hosts(4), hosts.equiv(4), ipnodes(4), noglogin(4), attributes(5)

# Diagnostics

NO LOGINS: System going down in N minutes

The system is in the process of being down and logins have been disabled.

# rm, rdir — Remove Directory Entries

# Synopsis

```
/usr/bin/rm [-f] [-i] file...
/usr/bin/rm -R [-f] [-i] dirname...[file...]
/usr/xpg4/bin [-fiR] file...
/usr/bin/rmdir [-ps] dirname...
```

# Description

/usr/bin/rm, /usr/xpg4/bin/rm remove files. The rm command removes the entry specified by each file argument. If a file has no write permission and the standard input is a terminal, the full set of permissions (octal) for the file is printed, followed by a question mark. The question mark is a prompt for confirmation. If your answer begins with y (yes), the file is deleted; otherwise, the file remains.

If it is a symbolic link, the link is removed but the file or directory to which it refers is not. You do not need write permission to remove a symbolic link provided you write permissions in the directory.

If you specify multiple files and removal of any files for any reason, rm writes a diagnostic message to standard error, nothing more to the current file, and goes on any remaining files.

If the standard input is not a terminal, the command operates as if you specified - option.

> Note — A enables you to explicitly mark the end of any command-line options, allowing rm to recognize file arguments that begin with a -. As an aid to BSD migration, rm accepts - as a synonym for --. This migration may disappear in a future release. If you use -- twice in the same command line, the second is interpreted as a file.
