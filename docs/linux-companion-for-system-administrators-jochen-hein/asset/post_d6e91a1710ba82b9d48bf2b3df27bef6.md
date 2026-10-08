
# THE AUTOMOUTER 451

If a file or subdirectory is sought in the /mount directory, the automounter finds additional information in the file /etc/auto.mount. An example for this file can be found in Listing 17.5.

```
# The file /etc/auto.mount has the format
# key [ -mount-options ] source
kernel    -ro ftp.kernel.org:/pub/linux
cdrom     -fstype=iso960,ro :dev/scd0
floppy   -fstype=auto :dev/fd0
dos      -fstype=vat,uid=0,gid=100,umask=002 :dev/sda1
```

**Listing 17.5** The file /etc/auto.mount.

The first entry mounts the NFS volume ftp.kernel.org:/pub/linux when the directory /mount/kernel is referenced. The other three entries have no host names specified in the third field, therefore a local mount is executed. After five minutes, the file system is removed.

Here too, it is only possible to work with different keys and architectures. However, this is only required in very large installations. More information can be found in the man page autofofs(5). In the near future, the amd will be replaced by autofofs, at least under LINUX.

| Additional Information and Sources |
|---|---|
| ftp server: | ftp.kernel.org /pub/linux/daemons/autofofs |
| ftp path: | autofofs-0.3.14.tar.gz |
| File name: Size: | about 50 Kbytes |
| Mailing list: | autofofs@kernel.org Subscribe quoting 'subscribe autofofs' with majordomo@linux.kernel.org |

# Anonymous
FTP servers

The ftppd daemon is installed on practically every networked UNIX system. In the standard version, each authorized user can transfer files to and from the system. Users are authorized if they have a valid user ID (which also presumes that the login shell is registered in the file /etc/shells and is not registered in the file /etc/ftpusers).

For a computer in a local network, this is acceptable. However, users without an anonymous ftp server may often need to view or transfer files. To make this possible, an anonymous ftp server can be installed. This is a sensible solution if you want to distribute freeware programs or if you want to provide information or program patches or similar items to the general public. http servers (Web servers) are employed for this purpose, but they have several disadvantages: uploads of users must be implemented by means of special constructions; the protocol has not been developed for the transfer of larger amounts of data; and after a transmission failure, the transfer process must be started all over again.

When setting up an ftp server, several issues must be considered to prevent alien users from having full access to all files of the computer. Or if you want to make the relevant data accessible in the easiest possible way, but you certainly do not wish to neglect all security aspects.

There are various ftp daemons, which are in part configured in a different manner. When choosing your server, you should make sure that you can monitor all actions by the users, if at all possible, so that you can trace what happens on your computer. This is an important tool for ensuring the security of your computer and for preventing its misuse as an intermediate storage place for copies or other unauthorized files. Furthermore, it might be a good idea to deactivate specific commands and to provide useful features such as a searchable index.

When a user logs under the user name anonymous or ftp, a special directory (for example /home/ftp) is usually the current directory. For this purpose, the system call chroot (2) is used which declares this directory to be the new root directory for this process (and for all of its child processes). This is used to prevent anonymous ftp users from having access to files outside this directory.

After entering the user name ftp or anonymous, the email address of the user is often entered. Often, a login is refused if the address is not correct, if it does not contain the 'at' sign (@). Many servers also try to find the name of the computer by asking for the name server.

Another alternative is the use of ident to determine the identity of the user more precisely. However, this leads to frequent problems with PC users, since no UID IDs exists on these systems. Furthermore, data protection issues which prohibiting rendering of the user ID, have not yet been clarified. Another problem is that users behind a (misconfigured) firewall have to wait for timeouts to occur.

In the whole directory tree under ~ftp, all directories and files should be available for anonymous users in read-only mode. This is intended to prevent, storage of a file .hosts on the computer that allows interactive access. The simplest solution is that no directory owned by the user ID under which the ftp server is running.

Some special directories (such as incoming) should be exempted from these restrictions to allow users without ID to make files publicly available as well. However, these files should be made available to other users only after they have been checked by the system administrator. This should be sufficient to prevent unauthorized distribution of data via your computer.

In unauthorized use, files with the name ... or with names that contain control characters are very popular. Therefore, you should search the transfer statistics for unusual names, so that you can exert some control function.

A very helpful feature for users is the use of special functions such as the automatic combination of all files in a directory into one archive. This allows users to transfer a complete directory tree with a single command. You may deactivate this function for individual directories, which would be a sensible thing to do, for example, the root directory.

In some clients (such as ncftp), this function is integrated; in most programs, however, it is not. Another useful feature is to restart an interrupted transmission where it left off by means of the re command. Unfortunately, most WWW browsers do not use this function. A further reason for using a 'normal' ftp client is that it will allow you to issue special commands, for example, to search in the index file or change permissions. These commands are initiated with QUOTE. Depending on the ftp server, different commands are supported; help can be obtained by the command QUOTE HELP.

## 18.1 Installing the wu-ftpd

As mentioned above, there are various ftp daemons. Many ftp servers on the Internet use the wu-ftpd, because it provides many special features for an anonymous ftp server, carries out extensive monitoring, and allows corrected versions to be quickly installed in the event of security problems. The striking argument in his favour is the availability of the source code, which allows local adaptations to be made.

For the system administrator, installing this daemon is slightly more laborious than the one supplied as a standard with UNIX. Nevertheless it is sensible to use a daemon whose source code is available, if you wish to be able to react promptly to problems. The wu-ftpd can be installed on almost all UNIX platforms, with some adaptations in different files are required.

The paths to important configuration files.h must be set prior to compilation in the file src/pathnames.h. here, you enter the specific paths used on your system. Development of this daemon does not take place under LINUX, so you will have to make several changes. The following list indicates the paths used on my system:

- PATH_USERS "/etc/ftpusers": This file contains the names of those who are not allowed to log in via ftp. Usually, these are the users root, bin, and some other system IDs.
- PATH_FTPACCESS "/etc/ftpaccess": Here is where the central configuration of the ftp server takes place. The contents of this file, which is evaluated at runtime, is described in many detail the main page ftpaccess.
- PATH_FTPHOSTS "/etc/ftphosts": This can be used for admission or refusal of individual users of various computers.
- PATH_EXECPATH "/bin/ftp-exec": This specifies the path under which programs are started. For anonymous users, chroot() is used to switch to the ~ftp directory, so this path is relative to it. For all other users, you may have to create an appropriate symbolic link. This is meant for the security of your server; therefore you

Many LINUX distributions already include the wu-ftpd; commercial UNIX systems, on the other hand, do not.
