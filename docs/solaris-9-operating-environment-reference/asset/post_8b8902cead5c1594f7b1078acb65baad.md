
# 1188

# rsh, remsh, remote, shell

```
castle% rsh somehost dd=/dev/nrmt0 bs=20b | tar xvpbf -
```

Evidently, what happens is the tar terminates before the rsh. The rsh then tries to write into the broken pipe, and instead of terminating neatly, proceeds to compete with your shell for its standard input. Invoking rsh with the -n option avoids such incidents. This bug occurs only when rsh is at the beginning of a pipeline and is not reading standard input. Do not use the -n option if rsh actually needs to read standard input. For example, the following command does not produce the bug.

```
castle% tar cf - | rsh sundial dd=/dev/nrmt0 bs=20b
```

If you use the -n in a case like this, rsh incorrectly reads from /dev/null instead of the pipe.

# Operands

- **command**: The command to be executed on the specified hostname.
- **hostname**: The official host name or nickname of the specified system.

# Usage

See largefile(5) for the description of the behavior of rsh and remsh when encountering files greater than or to 2 Gbytes (2**31 bytes).

The rsh and remsh commands are IPv6 enabled starting in the Solaris 8 release. See ip6(7P).

Host names are specified in the hosts database, which may be contained in the /etc/hosts file, the Internet domain database, or both. Each host has one official name (the first name in the database entry) and optionally, one or more nicknames. You can specify official host names or nicknames as hostname.

If the name of the file from which you execute rsh is anything other than rsh, rsh takes this as its hostname argument. This feature enables you to create a symbolic link to rsh in a node of that host, when executed, invokes a remote shell. By creating a directory and populating it with symbolic links of commonly used hosts and including that in your shell's search path, you can run rsh by typing hostname to your shell.

If you invoke rsh with the basename rsh, rsh checks for the existence of the /usr/bin/remsh. If this file exists, rsh behaves as an alias for rsh. If /usr/bin/remsh does not exist, rsh behaves as rsh is a host.

Each remote system has a file named /etc/hosts containing a list of trusted hosts with which it shares user names. Users with the same name as the local system can run rsh from systems listed in the remote system /etc/hosts file. Individual users can use a similar equivalence list with the file .rhosts in their home directories. Each entry in this file contains two names: a hostname and a username separated by a space. The entry permits the user who is logged into hostname to use rsh to access the remote system as the remote user. If the name of the local host is not found in the /etc/hosts file on the remote system or the local username and hostname are not found in the user's .rhosts file, then the access is denied. Host names listed in the /etc/hosts.equiv and .rhosts files must be the official host names listed in the hosts database; nicknames cannot be used in either of these files.

![](img/185d23104c385dfb6a62d64cc96b897_1217_0.png)

# runat 1189

Note — When a system is listed in hosts.equiv, its security must be as good as local security. An insecure system listed in hosts.equiv can compromise the security of the entire system. rsh does not prompt for password if access is denied on the remote system unless you omit the argument.

# Examples

The following command appends the remote file lizard.file from the system called lizard to file.file on the system called castle:
```
castle$ rsh cat lizard.file >> castle.file
```

The following example appends the file lizard.file on the system called lizard to file.file2 which also resides on the system called lizard:
```
castle$ rsh cat lizard.file lizard.file2
```

# Files

| File | Description |
| :--- | :--- |
| /etc/hosts | Internet host table |
| /etc/hosts.equiv | Trusted hosts and users. |
| .rhosts | System file |
| /etc/passwd | password file |

# Exit Status

- 0: Successful completion.
- 1: An error occurred.

# Attributes

See attributes(5) for descriptions of the following:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | Enabled |

# See Also

- on(1)
- login(1)
- telnet(1)
- vi(1)
- hosts(4)
- hosts.equiv(4)
- attributes(5)
- largefile(5)
- ip6(7)

# runat — Execute Command in Extended Attribute Space

# Synopsis

```
/usr/bin/runat file [command]
```

# Description

Use the runat (attributes) command, new in the Solaris 9 Operating Environment, to execute commands in a file's hidden directory. In the Solaris 9 Operating Environment, UFS, NFS, and TMPFS systems are enhanced to include extended attributes. These file attributes enable developers to associate attributes with a file. The runat command changes the current working directory to the hidden directory associated with the file and executes the specified command in the Bourne shell (/bin/sh). If you specify no argument, an interactive shell is spawned. The SHELL environment variable defines the shell to be spawned. If this variable is undefined, the default shell /bin/sh is used.

Note — It is not always obvious why a command fails in runat when the command is unable to determine the current directory. The resulting errors can be confusing and ambiguous (see tcsh and zsh).

# Operands

| Operand | Description |
| :--- | :--- |
| file | Any file, including a directory, that can support extended attributes. |
| command | The command to be executed in the directory. |

# Errors

A non-zero exit status is returned if runat cannot access the file or if the file does not support extended attributes.

# Usage

See fsattr(5) for a detailed description of extended file attributes. The process context created by the runat command has its current working directory set to the hidden directory containing extended attributes. The parent of this directory (..) always refers to the file provided on the command line. As such, it cannot be a directory. Therefore, commands (such as pwd) that depend on the parent entry being well formed (that is, referring to a directory) may fail.

In the absence of the command, runat spawns a new interactive shell with its current working directory set to the provided file's hidden attribute directory. Notice that some shells (such as zsh and tcsh) are not well behaved when the parent is not a directory, as described above. Do not use these shells with runat.

Recommended methods for performing basic attribute operations are shown below.

| Operation | Command |
| :--- | :--- |
| Display | runat ls [options] |
| Read | runat file cat attribute |

# runat 1191

# Operation

Create/Modify
```
runat file cp absolute-file-path attribute
runat file rm attribute
```

Delete
```
runat file chmod mode attribute
runat file chgrp group attribute
runat file chown owner attribute
```

Change permissions

# Interactive shell

```
runat file /bin/sh
or set your SHELL to /bin/sh and type runat file
```

The above list of commands is known to work with runat. While many other commands may work, there is no guarantee that any beyond this list will work. Any command that relies on not being able to determine its current working directory is likely to fail.

# Examples

Before you use the runat command, you must first create the attributes file. See fsattr(5) for a detailed description of extended file attributes.

The following example shows two ways to use the runat command to add extended attributes already created in the /tmp/attrdata file to file.2.

```
example% runat file.2 cp /tmp/attrdata attr.1
example% runat file.2 cat /tmp/attrdata > attr.1
```

The following example shows how to list the attributes of a file.

```
example% runat file.2 ls -1
example% runat file.2 ls
```

The following example copies an attribute from one file to another.

```
example% runat file.2 cat attr.1 | runat file.1 "cat" > attr.1
```

The following example uses runat to spawn an interactive shell.

```
example% runat file.3 /bin/sh
```

This command spawns a new shell in the attribute directory for file.3. Notice that the shell cannot determine your current directory. To leave the attribute directory, exit the spawned shell or change directory (cd) with an absolute path.

The remaining examples show commands that are likely to fail.

The following example runs man in an attribute directory:
