
## 2.5.2 Educating Users

Many nontechnical users know almost nothing about computers and certainly almost nothing about security. Most have only experienced Macs or Windows, which hide many details from all but the most curious users.

Take the time to explain some of the basic concepts such as the following:

- Linux is designed to handle multiple users simultaneously.
- Each user is identified by her account name.
- Each account gets a unique number, similar to a customer number, called a User ID or UID.
- Some accounts are grouped together into named groups, for example, the “users” group.
- Each file is owned by one account and has permissions that determine which accounts may read from it, write to it, or, if it is a program, run it.
- A set of files are collected into a directory (for file directory). Directories are like paper folders that can hold other documents. On Linux, directories are like ordinary files with names, accounts that own them, and permissions that determine which accounts can have certain kinds of access to them.
- It is important that the permissions on each file, including directories, be correct to prevent the wrong people from doing improper things with the file.
- There are commands to list files' names, ownership, permissions, and sizes, to change file permissions, move them around, edit them, and copy them between systems. You might want to talk about ls, chown, mv, rm, vi or emacs, ftp or ssh. This depends on what each user will be doing. In some cases a user may simply log in and invoke an application and “stay in” that all day. In this case, unless it is a captive account that does not get a normal login shell, the user will want to know about e-mail and Netscape.

- In an e-mail address or News posting, the sender's name and e-mail address can be faked (spoofed) easily and should not be trusted for important e-mail. Important e-mail needs to be verified by other trusted methods, such as PGP signatures or telephone, FAX, or paper mail to contact good numbers or addresses.

> A captive account is one where the person does not log in and use a normal shell. In many cases, the system would be configured to “drop” the person directly into an application, either by having the application listed as the login shell or by using an exec command, in each user’s .profile or .bashrc file. Other captive accounts might allow access only via popd, pop3s, and Samba.

## 2.6 Forgiveness Is Better than Permission

**DANGER LEVEL 💀 💀 💀 💀**

When I find this strategy to work well with management, it also applies to System Administration file permissions. Recognize that any file (including a directory or device file) that has permission available to a potential cracker might weaken your system's security. Linux is based on UNIX, which was developed by Bell Labs researchers before most systems were on the Internet. As such, many system files are readable by everyone and are writable.

When I get onto someone else's system, sometimes I am surprised at how many severe file permission problems I notice. Most users were never informed about permissions and their SysAdmins never dropped a

```
umask 027
```

or

```
umask 022
```

into the system's or individuals' startup scripts.

Why should a SysAdmin care about world-readable or world-writable files? After all, the users are trusted employees and the system is secure. Even under these circumstances there are dangers. Maybe some user may have a weak password that gets cracked. Maybe a cracker discovered a bug in a CGI script that allows him the full access of the UID running Apache. Thus, it is important to limit the damage of any breach. We looked at this in "Moving to Rings of Security" on page 20.

> Before systems were networked to the Internet, most people did not worry about file permissions much. If an employee did something she should not have, she was simply fired.

1. A hacker is a good and innovative programmer. If an ethical hacker/cracker enters else's system without authorization and causes time on the part of SysAdmins trying to track them down, I do not see a difference from a cracker. It is a person's right not to be helped.
A tiger, on the other hand, is authorized by management at some level to try to find vulnerabilities. This authorization should always be in writing to avoid misunderstandings later and possibly even night at the "country hotel."

2. While the vast majority of Linux systems use Apache as the httpd web server, most of the discussion of Apache also applies to other servers too. The Apache and httpd will be used interchangeably. On many distributions, Apache's default user and group will be nobody. It is suggested the UID be different from that of NFS's nobody and similar unrelated applications.

One common problem which occurs frequently is that there is no defined policy about who is responsible for putting aside mask in startup scripts or educating the users—the SysAdmin, who uses themselves, or someone else. Umask could be put in the global startup scripts for the various shells in /etc. These include csh.login and csh.csh for csh and tcsh, and profile for sh and bash. It is recommended that if this is a problem at your shop, you suggest to management that you write a draft policy for their approval. You will need to decide what is appropriate for your company's culture.

### 2.6.1 Directories and the Sticky Bit

![](img/7d04225c75a86d3cf4bd6077596f35b2_73_0.png)

Very few files should have world access. Among those that should be your tmp dirs with mode 1777 (typically /tmp or either /var/tmp or /usr/tmp). As you recall, if someone has access to a directory, Linux will allow that person to create new files in that directory, remove existing files, or move files in, out of, or within that.

The problem is that this allows a malicious user to remove someone else's temporary files from /tmp. This is not as much of a problem as you might think because many programs like vi and Mail created their temporary files in /tmp mode 600 (rw-------) so other users cannot read or write them and keep an open file descriptor referencing the file.

Linux and UNIX have an unusual feature in that the kernel keeps track of not only the link count of the directory entries that point to a given inode number, but how many open file descriptors in running programs reference it.

The kernel does not free the inode or files until there are no more directory links to the inode, and running programs that have the file (inode) open either close it or exit. Thus, if a malicious user removes a temporary file that your program has, you would not lose any data or be inconvenienced. Not all programs keep their temporary files during processing. (This technique of a program keeping its temporary files fails NFS because the NFS daemon will close files not accessed for a while because there are no explicit NFS command.)

Thus, a user's temporary files in the temporary directories, such as /tmp, are at risk for a malicious user removing them. The temporary files are, however, protected from being read or modified if the program that you is using creates mode 600.

Even if the program asks for file permissions 666, a true ideal, the user or SysAdmin can have this by specifying a umask of 027 or 022. Very few programs are so badly written that they will override umask to force more permissions.

The solution to this dilemma is to use the sticky bit, oct 1000. The graybeards will recall that originally, on ancient systems, the sole purpose of this sticky bit was to keep a copy of a program in swap space after every user running the programs running it. Thus, when the next person invoked the program it did not have to be read from the file system again. This resulted in fewer system resources being needed to start the program and less waiting time for the person invoking it. Typically a heavily used program as the editor got its sticky bit set.

In Linux (most Unix systems today), if a directory has the sticky bit on, the kernel will not allow someone to remove or rename files in that directory that she does not own even if the directory's write permissions would allow it otherwise.

The point is that directories where different users each need to be able to create files but should not remove each other's files should have the sticky bit set. One of these directories, say /tmp, might have its permissions correctly set via

```
chmod 1777 /tmp
```

It might be to extend this concept by enhancing the kernel so that setting a different prevents all but a directory's owner from creating a symbolic link in it. It will stop most "symlink attacks."

### 2.6.2 Finding Permission Problems

![](img/7d04225c75a86d3cf4bd6077596f35b2_74_0.png)

Most of the Linux distributions carry on the proud yet inappropriate philosophy of defaulting to having much more permissive a set of file permissions they should. Note that some of the character devices in /dev are mode 666 but this is correct for some of them. The /dev/null file allows any data written to it mode 666 is safe for it. It is suggested that you go through your system and find unneeded permissions and then turn off the unneeded permissions. Later, in "Finding Suspicious Files" on page 382, the periodic use of search for files left behind by crackers is discussed.

The following command will send you a mail message listing all world-writable files for bash (Bourne) shell users:

```
find / -fstype proc -perm -2 ! -type l -ls 2>&1 | \
Mail -s 'world writable' your_address
```

Csh users should use the following instead:

```
find / -fstype proc -perm -2 ! -type l -ls \
|& Mail -s 'world writable' your_address
```

The find command searches the directory trees listed (/ in this case) looking for files that match your specification. Unless parentheses or the -o operator (which means OR) is used, all expressions are ANDed together.

In the

```
! -fstype proc
```
