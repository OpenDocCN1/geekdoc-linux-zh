# rpcinfo

```
rpcinfo [ option ] [ host ]
```

Displays information about the Network File System. This utility provides a useful way to check that all the required NFS daemons are installed and running properly.

# OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -n n | Display information about the port number specified by n |
| -u host n | Display information about the program number n running on the specified host |
| -P [ host ] | Display information about the NFS daemons running on the current system or the specified host |

# EXAMPLE

| This Command | Does the Following |
| --- | --- |
| rpcinfo -p | Displays a list of all the NFS daemons currently running, if any. |

# showmount

```
showmount [ option ] [ host ]
```

Displays the Network File System mounts available. Optionally, shows the mounts available on the specified host.

# OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -a, -all | List both the client hostname and mounted directory in host:dir format |