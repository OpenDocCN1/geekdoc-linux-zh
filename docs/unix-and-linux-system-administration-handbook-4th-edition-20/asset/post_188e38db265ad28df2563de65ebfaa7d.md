
# 19 Sharing System Files

We're all familiar with the concept of sharing data among computers, whether that's accomplished through email attachments, transfer protocols such as HTTP and FTP, or file-sharing services like those provided by NFS and CIFS. These mechanisms are designed primarily as a way for users to share files and application data. However, UNIX and Linux systems can benefit from another type of sharing: the distribution of administrative configuration data. This kind of sharing centralizes administrative control and promotes consistency among systems.

User logins and passwords are a real-world example of the need for this kind of sharing. You rarely want to add a user to a single machine; in most cases, you want to define that on an entire class or network of machines. In addition, some organizations are now faced with the need to support a mix of platforms—some UNIX, some Linux, and some Windows—and are increasingly annoyed when they have to remember (and) a different password on each platform. Fortunately, it's not that hard to synchronize configuration and user information across different systems.

Sharing system files isn't as easy as it sounds. Attempts to develop distributed administrative databases for large networks go back several decades and have produced a number of interesting systems. However, none of the systems in general use seem exactly in their approach. Some are simple but not secure and not scalable. Others are functional unwieldy. All the systems have limitations that prevent you from setting up the network the way you want to, and none of them manage all the information you may want to share across your machines.

In this chapter we first discuss some basic techniques for keeping configuration files synchronized on a network. Next, we address the Lightweight Directory Access Protocol (LDAP), a more sophisticated, platform-independent database system that is becoming a de facto standard in both the UNIX and Windows worlds. Most sites are migrating towards LDAP, in large part because Microsoft's adoption (of the LDAP standard in their Active Directory product and the desire to better integrate Linux and Windows environments. Finally, we cover NIS, a popular database system that lingers in some environments but probably should not be deployed at new sites.

Note that sharing system files is different from system configuration and software deployment. These domains have different needs, and in practice, they are addressed by different solutions. See Chapter 12, *Installation and Management*, for details about going beyond that particular wall.

# 19.1 WHAT TO SHARE

Of the many configuration files on a UNIX or Linux system, only a subset can be usefully shared among machines. In modern times, the most pressing need for sharing relates to the contents of the **password**, **hosts**, and **aliases** files; however, other configuration files can become shared entities as well. Table 19.1 shows some of the most commonly shared files.

Table 19.1 System files that are commonly shared

| Filename | Function |
| --- | --- |
| /etc/passwd | User account information database |
| /etc/shadow* | Holds user account passwords |
| /etc/group | Defines UNIX groups |
| /etc/hosts | Maps between hostnames and IP addresses |
| /etc/mail/aliases | Holds electronic mail aliases |
| /etc/sudoers | Grants privileges for the **sudo** command |
| /etc/skel* | Holds default configuration files for new home directories |

* a. Not necessarily sharable among flavors of UNIX since the encryption can vary; see page 179.

Table 19.1 is far from being a comprehensive list; your exact configuration depends on how similar you want the machines at your site to be. For the most part, though, additional configuration files are associated with specific applications and are not supported by administrative directory systems such as LDAP; you must share the files by copying them.

Many of the files in Table 19.1 are intended to be accessed through routines in standard C library. For example, the /etc/passwd file can be searched with tgetpwuid, getpwnam, and getpwent routines. These routines take care of opening, and parsing the passwd file so user-level programs don't have to do them. Modern systems also use pluggable authentication modules for security-linked loops. PAM allows systems such as Kerberos and LDAP to be easily integrated into the system. The complement of data sources that are collected by the system administrator; see Prioritizing sources of administrative information page 739 for details.

See page 908 for more information about PAM.

# The NFS option

# 19.2 COPYING FILES AROUND

Many of the files in Table 19.1 are intended to be accessed through routines in standard C library. For example, the /etc/passwd file can be searched with tgetpwuid, getpwnam, and getpwent routines. These routines take care of opening, and parsing the passwd file so user-level programs don't have to do them. Modern systems also use pluggable authentication modules for security-linked loops. PAM allows systems such as Kerberos and LDAP to be easily integrated into the system. The complement of data sources that are collected by the system administrator; see Prioritizing sources of administrative information page 739 for details.

# Push systems vs. pull systems

Once you get away from the shared filesystem, file-copying systems generally either use a "push" model or a "pull" model. With push, the master server periodically distributes the files to each client, unless the client wants them. Files can be pushed explicitly whenever a change is made, or they can simply be distributed on a regular schedule.

The push model has the advantage of keeping the distribution centralized on one machine. Files, lists of contents, update scripts, and timetables are stored in one place, making the scheme easy to control. One disadvantage is that each client must let the master modify its files, creating a security hazard.

In a pull system, each client is responsible for updating itself from the server. It is a less centralized way of distributing files, but it is also more adaptable and secure. When data is shared across administrative boundaries, a pull system is especially attractive because the master and client machines need not be run by the same administrative group.

# rdist: push files

The **rdist** command is the easiest to distribute files from a central server. It has something of the flavor of make: you use a text editor to create a specification of the files to be distributed, and then you use **rdist** to bring reality into life with your specification. **rdist** copies files only when they are out of date, so you can write your specification as if all files were to be copied and let **rdist** optimize out unnecessary work.

rdist preserves the owner, group, and modification time of files. When it updates an existing file, **rdist** first deletes the old version before installing the new. This feature makes **rdist** suitable for transferring executables that might be in use during the update.¹

rdist historically ran on top of **rsh** and used **rsh** authentication to gain access to remote systems. However, this system is not secure and is disabled by default on modern operating systems. Even though the rdist documentation continues to talk about rsh, do not be fooled into thinking that **rsh** security is a reasonable choice.

Current versions of rdist are better in that they allow any command that understands the syntax to be substituted for **rsh**. In practice, the substitute is **ssh**, which uses cryptography to verify the identity of hosts and to prevent network eavesdroppers from obtaining copies of your data.

¹ The root disappears from the filesystem namespace, it continues to exist until all references have been released. You must also be aware of this effect when managing log files.
