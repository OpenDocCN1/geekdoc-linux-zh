462

# Process Identifiers

Along with its PID, each process records the integer ID of its parent and its group membership, parent process identifier (PPID), and process group identifier (PGID). Process groups are collections of one or more processes. The group leader has a PGID equal to its PID, and each member has a PGID that matches the leader. Unless reset by a setgrp() call, a process inherits the PGID of its parent. Process groups provide a mechanism for signaling all processes within the group using the PGID. This eliminates the need to know each member's PID. The PID, PPID, and PGID are the primary handles used by the system administrator for controlling process behavior.

A nifty GNU tool written by Fred Hutch called ps-tree will graphically map process relationships on a text terminal screen. His latest ps-tree source code is available under the GNU public license from the Gerhard Mercator University. A fix was added to the source code starting with ps-tree.c version 2.17 that made the code compatible with AIX 5L.

```
http://freshmeat.net/projects/ps-tree/
ftp://ftp.thp.Uni-Duisburg.DE/pub/source/
```

# Effective and Real UID and GID

Processes are associated with an owning user identifier (UID) and group identifier (GID). The UID and GID name spaces are maintained as part of the system account management and are recorded in the /etc/passwd and /etc/group files (see Chapter 22). The real UID and real GID numbers identify process owners for accounting and process control purposes. An effective UID (EUID) and an effective GID (EGID) are assigned to each process and represent the permissions and privileges available to the process during its lifetime.

# Controlling Terminal

Processes other than system daemons are usually associated with a control terminal. The control terminal represents the default device for standard input, output, and error channels and for sending signals via keyboard control characters. The control character-to-signal mapping is user-customizable and recorded in the termio structure. The controlling terminal is identified in the ps TTY column.

You can reassign the system console to a different TTY, pseudo-terminal or file using the chcons command; however, the redirection will not take place until the next system restart. Additionally, you can mirror a console, tty, or pseudo-terminal if you need to by using the portmir command. Details on the chcons and portmir commands and on the mirord daemon can be found both in the man pages and in the DocSearch documentation library. There are two SMIT FastPaths for the console assignment and tty port mirroring:

```
# smitty console
# smitty portmir
```