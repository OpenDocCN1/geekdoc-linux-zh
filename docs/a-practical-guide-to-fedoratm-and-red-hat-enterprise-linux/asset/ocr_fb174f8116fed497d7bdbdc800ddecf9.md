# Notes

A Linux system running ftp can exchange files with any of the many operating systems that support FTP. Many sites offer archives of free information on an FTP server, although for many it is just an alternative to an easier-to-access Web site (see, for example, ftp://ftp.ibiblio.org/pub/Linux and http://www.ibiblio.org/software/linux). Most browsers can connect to and download files from FTP servers.

The ftp utility makes no assumptions about filesystem nomenclature or structure because you can use ftp to exchange files with non-UNIX/Linux systems (which might use different filenaming conventions).

# Running the ftp and sftp FTP Clients

This section describes how to use the ftp and sftp FTP clients. The commands covered here work with both utilities.

# Prerequisites

Install the following packages:

+   - **openssh-clients** (installed by default; contains sftp)
+   - **ftp**

There is no service to start for ftp or sftp clients.

# JUMPSTART I: Downloading Files Using ftp

This JumpStart section is broken into two parts: a description of the basic commands and a tutorial session that shows a user working with ftp.

# Basic Commands

Give the command

```
$ ftp hostname
```

where *hostname* is the name of the FTP server you want to connect to. If you have an account on the server, log in with your username and password. If it is a public system, log in as the user **anonymous** (or ftp) and give your email address as your password. Use the ls and cd ftp commands on the server as you would use the corresponding utilities from a shell. The command get file copies file from the server to the local system, put file copies file from the local system to the server, status displays information about the FTP connection, and help displays a list of commands.

The preceding commands, except for status, are also available in sftp, lftp, and ncftp.