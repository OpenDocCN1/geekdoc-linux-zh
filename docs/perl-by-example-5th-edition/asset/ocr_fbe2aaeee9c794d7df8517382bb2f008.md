| Function | Description |
|---|---|
| getnetbyname | getnetbyname(NAME) |
|  | Translates a network name to its corresponding network address. Returns a list from the network database, `/etc/networks`. In scalar context, returns only the network address. |
|  | See getnetent(3). |
| getnetent | getnetent |
|  | setnetent(STAYOPEN) |
|  | endnetent |
|  | Iterates through the `/etc/networks` file and returns the entry as a list. Returns a list from the network database, `/etc/networks`. In scalar context, returns only the network name. |
|  | See getnetent(3). |
| getpeername | getpeername(SOCKET) |
|  | Returns the packed socket address of other end of the SOCKET connection. |
|  | See getpeername(2). |
| getpgrp | getpgrp(PID) |
|  | getpgrp PID |
|  | Returns the current process group for the specified PID (PID 0 is the current process). Without `EXPR`, returns the process group of the current process. |
|  | See getpgrp(2). |
| getppid | getppid |
|  | Returns the *pid* of the parent process. If 1 is returned, that is the *pid* for *init*. *init* adopts a process whose parent has died. |
|  | See getppid(2). |
| getpriority | getpriority(WHICH, WHO) |
|  | Returns the current *priority*, *nice* value, for *WHICH*—a process, a process group, or a user. *WHO* is relative to *WHICH* group. A *WHO* value of zero denotes the current process, process group, or user. |
|  | See getpriority(2). |
| getprotobyname | getprotobyname(NAME) |
|  | Translates a protocol NAME to its corresponding number and returns a list including the protocol name, aliases, and the protocol number. Returns a line from the network protocol database, `/etc/protocols`. |
|  | See getprotoent(3). |