
A system may have several devices of each type—for example, 10 hard disks or partitions, 20 terminals, 100 pseudoterminals, two solid state disks (SSDs), and so on. Our PC-BSD based system contains a total of 124 files in the /dev directory. This directory may contain several hundred—even over 1000—files in a network-based UNIX environment in a medium-to-large-sized organization.

### /etc:
The /etc directory contains commands, files, and scripts needed for system configuration and administration. A typical user is generally not allowed to use the commands and files in this directory. Some of the files and directories in this directory include crontab, csh, cshrc, csh.login, csh.logout, inetd.conf, login.access, login.conf, passwd, printcap, profile, rc.d, rcp, shells, services, ssh, ssl, and termcap. Discussion of most of the files in this directory is beyond the scope of this textbook. However, we briefly discuss the /etc/passwd file toward the end of this section. We discuss a few more files in this directory under "System Programming" in Chapters 18 through 21 and in Chapter 22 on "System Administration."

### /lib:
The library directory contains a collection of related files for a given language in a single file called an archive. A typical UNIX system today contains libraries for C and C++. The archive file for one of these languages can be used by applications developed in that language. The /lib directory contains libraries that are critical for the executable programs in the /bin and /sbin directories. The /usr/lib directory contains the shared and archive-type libraries (created by the ar command).

### /tmp:
Used by several commands and applications, the /tmp directory contains temporary files. You can use this directory for your own temporary files as well. All the files in this directory are deleted periodically so that the disk (or a partition of the disk) does not get filled with temporary files. The life of a file in the /tmp directory is set by the system administrator and varies from system to system, but it is usually only a few minutes. Files in /tmp may or may not exist when a system is rebooted.

### /usr:
The /usr directory contains subdirectories that hold, among other things, most of the utilities, system daemons (see Chapter 10), applications, programming tools, standard C include files, shared and archive-type language libraries, manual pages and other important documents, and source code (BSD and third-party). Two of the most important subdirectories in this directory are bin and lib, which contain binary images of most UNIX commands (utilities, tools, etc.) and language libraries, respectively.

### /usr/home:
Organized in some fashion, the /usr/home directory is normally used to hold the home directories of all the users of the system. For example, the system administrator can create subdirectories under this directory that contain home directories for certain types of users. For instance, the diagram in Figure 4.2, which shows a university setup, has one subdirectory each for the home directories of members of the administration, faculty, staff, students, and so on. These subdirectories are labeled admin, faculty, and students. Our system administrator created a symbolic link (see Chapter 8) called /home that points to /usr/home, as shown in the following session.

```
% ls -ld /home
lrwxr-xr-x 1 root root 9 Jul 9 19:05 /home -> /usr/home
%
```

This means that if a user, say john, changes the directory to his/her home directory and runs the pwd command, the command output would be /usr/home/john and not /home/john. We discuss links in UNIX, including symbolic links, in Chapter 8.

### /var:
The /var directory contains multipurpose log, temporary and spool files. Among several other directories, the /var/mail directory contains files for receiving and holding incoming e-mail messages of users. When you read your new e-mail, it comes from a file in this directory. The /var/spool/mqueue directory contains the undelivered mail queue and the /var/spool/output directory contains the line printer spooling directories. The /var/tmp directory contains temporary files that are kept between system reboots.

### /etc/passwd:
The /etc/passwd file contains one line for every user on the system and describes that user. Each line has seven fields, separated by colons. The following is the format of the line.

```
login_name:password:user_ID:group_ID:user_info:home_directory:login_shell
```

The login_name is the login name by which the user is known to the system and is what the user types to log in. The password field contains the dummy password x or * in newer systems (starting with System V Release 4—SVR4) and the encrypted version of the password in older systems. The newer versions store encrypted passwords in the /etc/master.passwd file. Only the superuser (i.e., root) has read and write access permissions for the master password file; nobody else can even read it. POSIX requires user_ID (UID) to be an integer type. Usually, the superuser is assigned a UID of 0. Several other login names are also assigned UIDs that are known (or from a known range). Typically, UIDs 1–499 or 1–999 are reserved. Depending on the UNIX system that you use, UIDs 1,000–32,767 or 1,000–65,536 are assigned to “normal” users like you and I. In systems that use 32-bit UIDs, this range is 1,000–4,294,967,296. The group_ID identifies the group that the user belongs to, and it also is an integer between 0 and 65,535 with, usually, integers 0–99 reserved. The user_info field contains information about the user, typically the user’s full name. The home_directory field contains the absolute pathname for the user’s home directory. The last field, login_shell, contains the absolute pathname for the user’s login shell. The command corresponding to the pathname specified in this field is executed by the system when the user logs on. Back-to-back colons mean that the field value is missing, which is sometimes done with the user_info field. The following session shows the line from the /etc/passwd file on our system for the user sarwar:

```
% cat /etc/passwd | grep "sarwar"
sarwar:*:1004:1008:Mansoor Sarwar:/home/sarwar:/bin/csh
%
```

In this line, the login name is sarwar, the password field contains *, the user ID is 1004, the group ID is 1008, the personal information is the user’s full name (Mansoor Sarwar), the home directory is /home/sarwar, and the login shell is /bin/csh, or the C shell. We usually work under the Bourne shell by running the /bin/sh command after login.
