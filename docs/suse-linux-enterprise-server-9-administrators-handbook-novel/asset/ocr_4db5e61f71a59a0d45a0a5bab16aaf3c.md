servers, such as **atftp** by Jean-Pierre Lefebvre (`ftp://ftp.mamalinux.com/pub/atftp`) and **tftp-hpa** (`http://www.kernel.org/pub/software/network/tftp`), are available for various Linux/Unix distributions.

This section shows you how to set up an FTP server using the Very Secure FTP Daemon (**vsftpd**) and Pure-FTPd (**pure-ftpd**) packages included in SLES 9. In addition, we cover ways to set up a TFTP server using the standard TFTP server, **in.tftpd**, included with SLES 9; **atftp** is also included with SLES 9 but is not discussed here.

# Using Pure-FTPd

Pure-FTPd is pretty much a command-line-driven application. All its options are to be specified on the command line. You can get a full listing from its man page (man **pure-ftpd**) or by typing the following at a terminal prompt:

```
pure-ftpd --help
```

You’ll find that Pure-FTPd uses all 26 letters (both upper- and lowercase) plus a few numerals for switches. The following list briefly explains some of the more commonly used options:

+   - `-A` will chroot everyone but root.
+   - `-b` tells pure-ftpd to ignore some more standards to deal with broken clients such as Internet Explorer.
+   - `-B` starts the standalone server in the background (that is, in “daemonized” mode), which is the same as running `./pure-ftpd &`.
+   - `-c #` limits the maximum number of clients to #; the default is 50.
+   - `-C #` limits the number of simultaneous connections from the same IP address to #; the default is 50 (or the maximum number of clients).
+   - `-e` allows only anonymous users. This option is mutually exclusive with `-E`.
+   - `-E` allows only authenticated users (that is, disables anonymous FTP access).
+   - `-H` prevents resolving a client’s IP address into a DNS name (so 10.58.2.5 will be logged instead of `ws2.UniversalExports.ca`). This can speed up connections significantly, and it helps to reduce (reverse-DNS) bandwidth usage on busy servers, especially on public FTP servers.
+   - `-j` creates the user’s home directory if one doesn’t exist. This allows home directories to be created on demand. This option is especially useful when used in conjunction with something other than Unix-based