Syntax for specifying a NBD device using TCP “nbd:<server-ip>:<port>[<exportna=
<export>]”

Syntax for specifying a NBD device using Unix Domain Sockets “nbd:unix:<domain-
socket>[<exportna=<export>]”

Example for TCP

```
```tex
qe-system-i386 --drive file=nbd:192.0.2.1:30000
```
```

Example for Unix Domain Sockets

```
```tex
qe-system-i386 --drive file=nbd:unix:/tmp/nbd-socket
```
```

# SSH

QEMU supports SSH (Secure Shell) access to remote disks.

Examples:

```
```tex
qe-system-i386 -drive file= qe-system-i386 -drive
file.driver=ssh, file.user=user,
file.host=host, file.port=22, file.path=/path/to/disk.img
```
```

Currently authentication st be done using ssh-agent. Other authentication thods may
be supported in future.

# Sheepdog

Sheepdog is a distributed storage system for QEMU. QEMU supports using either local
sheepdog devices or remote networked devices.

Syntax for specifying a sheepdog device

```
```tex
sheepdog[+tcp|+unix]://[host:port]/vdima [?socket=path][#snapid|#tag]
```
```

Example

```
```tex
qe-system-i386 --drive file=sheepdog://192.0.2.1:30000/MyVirtualMachine
```
```

See also <>.

# GlusterFS

GlusterFS is an user space distributed file system. QEMU supports the use of
GlusterFS volus for hosting VM disk images using TCP, Unix Domain Sockets and
RDMA transport protocols.

Syntax for specifying a VM disk image on GlusterFS volu is

```
```tex
gluster[+transport]://[server[:port]]/volna/image[?socket=...]
```
```

Example

```
```tex
qe-system-x86_64 --drive file=gluster://192.0.2.1/testvol/a.img
```
```

See also <>.

# HTTP/HTTPS/FTP/FTPS/TFTP

QEMU supports read-only access to files accessed over http(s), ftp(s) and tftp.

Syntax using a single filena:

```
```tex
<protocol>://[<username>[<password>]@]host>/<path>
```
```