# 138 Part II ♦ The SUSE System

Administration. Man pages are stored under a single directory hierarchy, the directory /usr/share/man on Linux systems. (Older Linux and other Unix-like systems store these under the directory /usr/man.) Each section has its own subdirectory—for example, man1, man2, man3,` and so on.

Table 5-1 lists the man pages sections and their corresponding types of information.

| Table 5-1 Man Pages Sections |
| Section Number | Type of Man Pages |
| 1 | User commands |
| 2 | System calls |
| 3 | Subroutines and library functions |
| 4 | Devices, special files, device drivers, and associated file formats |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System administration commands |
| 9 | Kernel |
| N | New |

In certain cases, man pages may have the same name but different content in sections. Thus, for example, you will see the man page for the crontab program with the following:

```
user@bible:--> man 1 crontab
```

However, you will see the man page describing the structure of a crontab file with the following:

```
user@bible:--> man 5 crontab
```

When searching for man pages on a particular command-line program, you may therefore want to consider the type of information that you are looking for and provide a specific man page section to zero in the information. As mentioned in the