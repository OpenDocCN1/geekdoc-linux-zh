# ## The Cryptographic File System

The Cryptographic File System (CFS) was developed by Unix pioneer Matt Blaze and constitutes the first full-blown integration of secret-key encryption into the Linux file system. One of the most important advantages of CFS is its support of both local filesystem types (e.g., ext2) as well as remote file systems such as NFS. This support protects your data as it sits in your server, and also as it travels through the network whenever you share an NFS mount point. CFS supports several encryption algorithms including DES, 3DES, MacGuffin, SAFER-SK128, and Blowfish.

CFS’s main drawback, however, is performance. If you elect to use 3DES encryption (which I recommend, since DES is barely adequate nowadays), you will pay a price, and you’ll see a noticeable delay in your disk access, especially for large files. This is partly due to the fact that CFS operates in user space (outside of the kernel.) However, running in user space can actually be an advantage, because other cryptographic filesystem modules are offered as a patch to particular versions of Linux kernels, and they’re often not available for the latest stable kernel.

Let’s start by installing the software on our server.

# ### Installing CFS

While the package can be obtained in source form, it’s also available from www.zedz.net (or ftp.zedz.net) in RPM format, as shown in Listing 2.5.

# **Listing 2.5** Downloading the CFS distribution in RPM format

```
[ramon]$ ftp ftp.zedz.net
Connected to ftp.zedz.net.
220 warez.zedz.net FTP server ready.
Name (ftp.zedz.net:ramon): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: rhontanon@sbyex.com
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd /pub/crypto/disk/cfs/
250 CWD command successful.
ftp> get cfs-1.3.3bf-1.i386.rpm
local: cfs-1.3.3bf-1.i386.rpm remote: cfs-1.3.3bf-1.i386.rpm
200 PORT command successful.
150 Opening BINARY mode data connection for cfs-1.3.3bf-1.i386.rpm (194436 bytes).
226 Transfer complete.
```