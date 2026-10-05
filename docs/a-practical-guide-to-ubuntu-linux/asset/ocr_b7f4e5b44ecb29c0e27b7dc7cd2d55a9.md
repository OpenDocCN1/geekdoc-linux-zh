Although it is not recommended, you can allow access to all daemons for all clients
by removing both files.

Examples For a more secure system, put the following line in **hosts.deny** to allow all access:

```
$ cat /etc/hosts.deny
```

```
ALL : ALL : echo '%%c tried to connect to %%d and was blocked ' >> /var/log/tcpwrappers.log
```

This prevents any client from connecting to any service, unless specifically
ditted to so in /log/tcpwrappers.log. When this is matched, it adds a line to the file
*/log/tcpwrappers.log. The %%c expands to client information and the
%%d expands to the name of the daemon the client attempted to connect.

With the preceding **hosts.deny** in place, you can include lines in **hosts.allow** to
explicitly allow access to certain services and systems. For example, the following
hosts.allow file allows anyone to connect to the OpenSSH daemon (ssh, scp, sftp)
but allows telnet connections from the same network as the local system and
users on the 192.168.subnet:

```
$ cat /etc/hosts.allow
sshd: ALL
in.telnet: LOCAL
in.telnet: 192.168.* 127.0.0.1
...
```

The first line allows connection from any system (ALL). The second linenallows connection from any system in the same domain as the server (LOCAL). The
third line matches any system whose IP address starts with 192.168. as well as the
local system.

# SETTING UP A chroot JAIL

On early UNIX systems, the root directory was a fixed point in the filesystem.
modern UNIX systems, including Linux, you can define the root directory on a per-
basis. The chroot utility allows you to run a process with a root directory
other than /.

The root directory appears at the top of the directory hierarchy and has no parent.
Thus a process cannot access files above the root directory because none exists.
For example, you run a program (process) and specify its root directory as
/tmp/jail, the program would have no concept of any files in /tmp or above: jail is
t program's root directory and is labeled / (not jail).

By a program from accessing, executing, or modifying—possibly maliciously—files
outside the directory hierarchy starting at its root. You must set up a chroot jail
properly to increase security: If you do not set up the chroot jail correctly, you can
make it easier for a malicious user to gain access to a system than there were no
chroot jail.