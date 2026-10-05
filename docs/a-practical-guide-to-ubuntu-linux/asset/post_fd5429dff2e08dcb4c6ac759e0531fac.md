
# SECURING A SERVER

fewer resources to keep a process in RAM (or swap space) than it does to restart it periodically. Also, a developer can now handle socket communications more easily using various toolkits.

Two ways you can secure a server are by using TCP wrappers and by setting up a chroot jail. This section describes these techniques.

# TCP WRAPPERS: SECURE A SERVER (hosts.allow AND hosts.deny)

Follow these guidelines when you open a local system to access from remote systems:

- Open the local system only to systems you want to access it.
- Allow each remote system to access only the data you want it to access.
- Allow each remote system to access data only in the appropriate manner (readonly, read/write, write only).

### libwrap As part of the client/server model, TCP wrappers, which can be used for anyone that is linked against libwrap, rely on the /etc/hosts.allow and /etc/hosts.deny files as the basis of a simple access control language (ACL). This access control defines rules that selectively allow clients to access server daemons on a local system based on the client's address and the daemon it tries to access. The output of id shows that the shared library of sshd is libwrap:

```
$ ldd /usr/sbin/sshd | grep libwrap
1libwrap.so.0 => /lib/6/libwrap.so.0 (0xb7ec7000)
```

### hosts.allow and hosts.deny Each line in the hosts.allow and hosts.deny files has the following format:

```
daemon_list : client_list [: command]]
```

where daemon_list is a comma-separated list of one or more server daemons (such as portmap, vsftpd, and sshd), client_list is a comma-separated list of one or more clients (see Table 11-2 on page 461), and the optional command is the command that is executed when a client from client_list tries to access a server daemon from daemon_list.

When a client requests a connection to a server, the hosts.allow and hosts.deny files on the server are consulted in the order until a match is found:

- 1. If the daemon/client pair matches a line in hosts.allow, access is granted.
- 2. If the daemon/client pair matches a line in hosts.deny, access is denied.
- 3. If there is no match in the hosts.allow or hosts.deny file, access is granted.

The first match determines whether the client is allowed to access the server. When either hosts.allow or hosts.deny does not exist, it is as though that file was empty.

Although it is not recommended, you can allow access to all daemons for all clients by removing both files.

### Examples For a more secure system, put the following line in **hosts.deny** to allow all access:

```
$ cat /etc/hosts.deny
```

```
ALL : ALL : echo '%%c tried to connect to %%d and was blocked ' >> /var/log/tcpwrappers.log
```

This prevents any client from connecting to any service, unless specifically permitted to so in /log/tcpwrappers.log. When this is matched, it adds a line to the file /var/log/tcpwrappers.log. The %%c expands to client information and the %%d expands to the name of the daemon the client attempted to connect.

With the preceding **hosts.deny** in place, you can include lines in **hosts.allow** to explicitly allow access to certain services and systems. For example, the following hosts.allow file allows anyone to connect to the OpenSSH daemon (ssh, scp, sftp) but allows telnet connections from the same network as the local system and users on the 192.168.*subnet:

```
$ cat /etc/hosts.allow
sshd: ALL
in.telnet: LOCAL
in.telnet: 192.168.* 127.0.0.1
...
```

The first line allows connection from any system (ALL). The second line allows connection from any system in the same domain as the server (LOCAL). The third line matches any system whose IP address starts with 192.168. as well as the local system.

# SETTING UP A chroot JAIL

On early UNIX systems, the root directory was a fixed point in the filesystem. In modern UNIX systems, including Linux, you can define the root directory on a per-basis. The chroot utility allows you to run a process with a root directory other than /.

The root directory appears at the top of the directory hierarchy and has no parent. Thus a process cannot access files above the root directory because none exists. For example, you run a program (process) and specify its root directory as /tmp/jail, the program would have no concept of any files in /tmp or above: jail is the program's root directory and is labeled / (not jail).

This prevents a program from accessing, executing, or modifying—possibly maliciously—files outside the directory hierarchy starting at its root. You must set up a chroot jail properly to increase security: If you do not set up the chroot jail correctly, you can make it easier for a malicious user to gain access to a system than if there were no chroot jail.

# USING chroot

Creating a chroot jail is simple: Working with root privileges, give the command /usr/sbin/chroot directory. The directory becomes the root directory and the process attempts to run the default shell. The following command sets up a chroot jail in the (existing) /tmp/jail:

```
$ sudo /usr/sbin/chroot /tmp/jail '/bin/bash': No such file or directory
/usr/sbin/chroot: cannot run /bin/bash
```

This example sets up a chroot jail, but when the system attempts to run bash, the operation fails. Once the jail is set up, the directory that was named takes over the name of the root directory /. As a consequence, chroot cannot find the file identified by the pathname /bin/bash. In this situation the chroot jail works correctly but is not useful.

Getting a chroot jail to work is more complicated. To have the preceding example run bash in a chroot jail, create a bash directory in (/tmp/jail/bin) and copy /bin/bash to this directory. Because the bash binary is dynamically linked to shared libraries, you need to copy these libraries into jail. The libraries go in lib: the next example creates the necessary directories, copies bash, uses ldd to display the shared dependencies of bash, and copies the necessary libraries to lib. linux-gate.so.1 is a dynamically shared object (DSO) produced by the kernel to speed system calls; you do not need to copy it.

```
$ pwd
/tmp/jail
$ mkdir lib bin/ bash
$ ldd bash
linux-gate.so.1 => /lib/6/linux-gate.so.1 (0x0032c00)
ncurses.so.5 => /lib/6/ncurses.so.5 (0x00d4d00)
ld.so.2 => /lib/6/cmov/ld.so.2 (0x0091d00)
libc.so.6 => /lib/6/cmov/libc.so.6 (0x00110000)
linux.so.2 (0x0026a00)
```

```
$ cp ncurses.so.5,linux.so.2 lib
$ cp ld.so.2,libc.so.6 lib

```

Now start the chroot jail again. Although all the setup can be done by an ordinary user, you must be working with root privileges to run chroot:

```
$ sudo /usr/sbin/chroot /tmp/jail
bash# pwd
/
bash# ls: command not found
bash# exit
$
```

# CHAPTER 11 SYSTEM ADMINISTRATION: CORE CONCEPTS

This time chroot finds and starts bash (bash#). The pwd command works because it is a shell builtin. However, bash cannot find the ls utility because it is not in the chroot jail. You can copy /bin/ls and its libraries into the chroot jail if you want users in the jail to be able to use ls. An exit command allows you to escape chroot.

If you provide chroot a second argument, it takes that as the name of the program to run inside the chroot jail. The following command is equivalent to the preceding one:

```
$ sudo /usr/sbin/chroot /tmp/jail /bin/bash
```

To set up a useful chroot jail, first determine which utilities of the chroot jail need. Then copy the appropriate binaries and libraries into the jail. Alternatively, you can build static copies of the binaries and put them in the jail without installing separate libraries. The statically linked binaries are considerably larger than their dynamic counterparts. The size of the system with bash and the core utilities exceeds 50 megabytes. You can find the source code for most common utilities in the bash and coreutils source pages.

The chroot utility fails unless you run it with root privileges—the preceding examples used sudo to gain these privileges. The result of running chroot with root privileges is a root shell (a shell with root privileges) running inside a chroot jail. Because a user with root privileges can break out of a chroot jail, it is imperative that you run a program in the chroot with reduced privileges (i.e., privileges other than root).

There are several ways to reduce the privileges of a user. You can use su or sudo in the jail and then start a shell or a daemon inside the jail, using one of these programs to reduce the privileges of the user working in the jail. A command such as the following starts a shell with reduced privileges inside the jail:

```
$ sudo /usr/sbin/chroot jailpath /usr/bin/sudo -u user /bin/bash &
```

where jailpath is the pathname of the jail directory, and user is the username whose privileges the shell runs. The problem with this scenario is su and, as for Ubuntu, call PAM. You need to put all of PAM, including its libraries and configuration files, in the jail, along with sudo (or su) and the /etc/passwd file. Alternatively, you can recompile su sudo. The source code calls PAM, however, you would need to modify the source so it does not call PAM. Either of these techniques is time-consuming and introduces complexities that can lead to an insecure jail.

The following C program¹ runs a program with reduced privileges in a chroot jail. Because this program obtains the UID and GID of the user you specify on the command line before calling chroot(), you do not need to put /etc/passwd in the jail.

- 1. Thanks to David Chisnall and the Étoile Project (etoiles.com) for the uchroot.c program.
