
use a given service if they supply the correct user name and password. Share-level authentication takes place by granting access based on the rights of the "guest account" on the UNIX system. This is true unless a client used a user name and password in this or a previous session. Needless to say, there is a lot to consider with user authentication.

The **smb.conf** file has an entry in which you can specify the security as "user" or "share," as shown in the following lines:

```
security = user
```

```
security = share
```

Most systems employ user-level security. When this is done users are checked against their names in the **passwd** file and access is granted accordingly.

There are many additional issues related to user authentication that you’ll want to investigate if you set up Samba. The documentation supplied with Samba as part of Red Hat Linux is excellent, and the background information on the Web sites listed later in this chapter is informative as well.

## Samba Utilities and Programs

We have used several Samba utilities and programs in this chapter. The following list gives a description of the most often used Samba-related commands. There are manual pages for all these that are part of most Samba installations.

- **smbd** - This is the daemon that provides file and print services to SMB clients, such as the Windows system used in our examples throughout this chapter.
- **nmbd** - This is the daemon that provides NetBIOS name server capability and browsing.
- **smbclient** - A program that gives the server access to remotely mounted SMB shares on other servers.
- **testparm** - A test program for `/etc/smb.conf`.
- **smbstatus** - Program that displays status information about current Samba connections.
- **smbpasswd** - Program used to change a user’s SMB password on the local machine.
- **smbrun** - Program that runs shell commands for `smbd`.
- **smbtar** - Program to back up SMB shares directly to a UNIX tape drive.
- **smbmount** - Used to mount an SMB file system.
- **smbumount** - Used to unmount an SMB file system.

The online manual pages for these and other Samba-related commands provide more detail. Even in a simple setup such as the one performed in this chapter, you will want to run some of these programs.

## Obtaining Samba

In the examples used throughout this chapter, we set up Samba on a Linux system that had Samba installed on it as part of the Red Hat Linux CD-ROM. If Samba does not come on the CD-ROM provided with your UNIX variant or if you wish to be sure that you’re loading the very latest Samba, then you can obtain Samba from the Web.

*www.samba.org* is the place to start. From this Web site you can select a "download site" in your country. You can also select "Web sites" on *www.samba.org* that provide a wealth of information on Samba, including the GNU General Public License mentioned earlier in the chapter.

There is extensive documentation on Samba-related Web sites, including detailed descriptions of the programs that I listed earlier and used in this chapter.

If you decide to download Samba, you'll probably be given an option of loading a precompiled Samba on your system or building and compiling Samba yourself. The choice you make depends on a lot of factors. If you have a good, reliable Samba distribution, as we did in this chapter when working with Red Hat Linux, then working with a precompiled Samba may be best. If you're interested in learning more about how Samba works and is configured, and want the very latest and greatest version, then download the source and compile yourself.

Even if you have a great prepackaged Samba, as we did in this chapter, it is still worth visiting the Samba-related Web sites to view the extensive documentation available.

# INDEX

## A

- Abbreviations and macros in vi, 434-435
- Absolute and relative path names, 81-84
- Access permissions, 77-81
- Adding text in vi, 411-412
- Addressing (IP), 463-471
  - address classes, 464-466
  - class A, 465
  - class B, 465
  - class C, 466
  - subnet mask, 466-471
- AIX specific CDE, 193-197
- Alias as part of bash, 257-260
- Alias as part of csh, 363-366
- Alias as part of ksh, 298-300
- Ampersand (&), 316
- Adjusting the screen in vi, 431-432
- Advanced Server for UNIX, 1200-1215
  - /etc/group, 1207
  - /etc/passwd, 1207
  - file system, 1212-1215
  - installation, 1202-1209
  - net commands, 1200-1205
  - printing, 1209-1212
  - shares, 1212
- Arguments in shell programming, 689-694
- ARPA services, 472-475
  - ftp, 472-475
  - telnet, 475
- Assignment (programming), 948
- at, 777
  - scheduling cron jobs, 772-777
- cron, 772-777
  - cron.allow, 776
  - cron.deny, 776
  - crontab, 772-777
    - -l, 775
- awk, 588-596
  - in ksh programming, 713-715
  - man page, 623-629

## B

- Background jobs, 315-318, 268-271, 374-376
  - ampersand (&), 316
  - bg, 317, 318, 375
  - control Z, 317
  - in csh, 374-376
  - jobs, 318
  - kill, 318
- Backup, 770-772
  - cpio, 771
  - dd, 771-772
  - dump and fsdump, 772
  - tar, 770-771
- Bash shell, 247-274
  - aliases, 257-260
  - .bashrc, 249-250, 257-258
  - command and path completion, 260-261
  - environment variables, 266-268
  - env, 266
  - export, 267-268
  - PS1, 267
  - /etc/profile, 250-251
  - file name expansion, 261-263
  - history, 251-256
    - initializing history, 251
    - recalling from history list, 254-256
    - set history, 251
  - issuing commands, 249-251
  - redirection, 264-265
  - umask and permissions, 271-274
  - .bashrc, 249-250
- Berkeley commands, 475-477
  - rcp, 475-476
  - remsh, 476-477
  - rlogin, 476
  - rwho, 477
- bg, 317, 318
- /bin/ksh, 679
- Block device file as file type, 51-52
- /boot (Linux), 64-65
- Branching and branching in csh, 718-720
  - else, 719-720
  - endif, 719-720
  - if, 718-720
- Bourne shell, see ksh which is a superset of Bourne
- break in while loop, 705
- Browser for internet accessing, 21-32
  - browser, 22-31
  - browser appearance, 25
  - browser applications, 26
  - browser cache, 32
  - browser disk space, 27
  - browser fonts, 25
  - browser proxy, 30-31
  - browser publishing, 29
  - browser roaming user, 28
  - http://, 23
  - protocol specifiers, 23-24
  - URL, 22-24

## C

- C and C++
  - C language, 999-1067
    - comments, 1003
    - constants, 1005
    - data types, 1007-1008
    - arithmetic, 1013-1016
    - arrays, 1041-1049
    - assignment operators, 1018-1019
    - character, 1011-1012
    - choice, 1032-1037
    - classes, 1062-1065
    - double precision, 1010-1011
    - dynamic memory allocation, 1065-1067
    - exponential notation, 1011
    - floating point, 1010
    - functions, 1037-1041
    - increment and decrement, 1017-1018
    - integer, 1008-1009
    - logical operators, 1030-1031
    - looping, 1023-1030
    - nested loops, 1031-1032
    - pointers, 1053-1062
    - precedence, 1021-1023
    - structures, 1049-1053
    - type conversion, 1019-1021
    - void, 1012-1013
  - C++ language, 1067-1096
    - comments, 1068-1069
    - data types and modifiers, 1076-1096
    - enumeration, 1071
    - headers, 1070-1071
    - I/O, 1069-1070
    - namespace, 1072-1075
    - precedence, 1071-1072
  - format of a c program, 1002
  - practices, 1002-1003
  - standard library, 1004
  - symbolic constants, 1005-1006
- C shell, 351-398
  - alias, 363-366
  - background jobs and job control, 373-376
    - ampersand (&), 376
    - bg, 375
    - ctrl-z (control z), 375
    - fg, 375
    - jobs, 376
    - kill, 376
    - time, 374
  - command substitution, 360-362
  - .cshrc, 353-354, 355
    - initialize history in .cshrc, 357
  - environment variables, 370-373
    - env, 371-372
    - set, 371
  - file name expansion, 366-368
  - history, 357-362
    - command line history, 358-360
    - history list, 360-362
    - initialize history in .cshrc, 357
    - recalling from history list, 362
  - issuing commands, 353
  - job control, 373-376
    - ampersand (&), 376
    - bg, 375
    - ctrl-z (control z), 375
    - fg, 375
    - jobs, 376
    - kill, 376
    - time, 374
  - .login, 354-355, 356
  - manual page, 386-398
  - redirection, 366-368
    - shell and environment variables, 370-373
      - env, 371-372
      - set, 371
  - umask and permissions, 376-379
    - chmod, 379-381
    - group, 381-384
    - other, 381-384
    - owner, 381-384
    - umask, 376-379
- CacheFS file system type, 54
- Caldera Linux mount example, 54-56
- case in csh, 727-729
  - endsw, 727-729
- case statement in ksh, 698-700
- Cases, uppercase and lowercase, 3
- cat, 130-138
  - command summary, 135
  - man page, 140-142
- catman command (manual pages), 15
- cc, 988-990
  - compilers, 985-986
  - options, 989-990
- cd, 83, 98-101, 116-120
  - command summary, 101
  - man page, 143-145
- CDE, 187-246
  - advanced topics, 224-225
  - AIX specific, 193-197
  - desktop, 192-197
  - HP-UX specific, 193-197
  - Motif, 226
    - configuration files, 227-242
  - performance, 243-246
  - sequence of events when starting, 242-243
  - Solaris specific, 197-207
  - X window system, 225
    - configuration files, 227-242
- CD file system type, 53
- Change directory (cd), 98-101, 116-120
  - man page for cd, 143-144
- Change mode (permissions), 101-106
  - man page for chmod, 145-148
- Changing text in vi, 416-419
- Character device files as file type, 51-52
  - character device file, 782-783
  - disk device file, 782
  - naming of device files, 781
  - raw device, 782-783
  - tape device file, 782
- chmod, 101-106, 321-326, 679
  - group, 381-384
  - other, 381-384
  - owner, 381-384
  - command summary, 106
  - man page, 145-148
