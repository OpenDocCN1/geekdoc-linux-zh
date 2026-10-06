
# Answers to Review Questions

- 1. C. To add the device, specify the device name and the IP address.

- 2. A, C, D. You can bring down the device by using /sbin/ifdown or ifconfig; however, ifconfig does not accept the script name ifcfg-eth1 as an argument.

- 3. D. The -r flag causes the netstat command to report the routing table.

- 4. A, B. The command requires a device name; you must not specify a path.

- 5. C. The Windows 95 file system has type vfat. It's possible to mount a Windows 95 file system as an mdos file system, but doing so may disrupt the long filenames of files that you manipulate.

- 6. A, B, C, D. Any of the alternatives will work; in addition, pressing Ctrl+Alt+Del will reboot the system.

# Chapter 16

# Using the cron System

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Understand the cron system and be capable of scheduling jobs using cron and anacron.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_396_0.png)

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

## The cron System

The cron system lets users schedule jobs for automatic execution at specified times and intervals. The jobs run using the owner's login; by default, the results of jobs are sent to the owner via e-mail. A utility program lets a user run a text editor to specify which jobs to run and when to run.

The cron system consists of the following components:

- /usr/sbin/cron, the cron service, which runs continuously
- /etc/crontab, the system cron table, which specifies default jobs defined by Red Hat
- /usr/bin/crontab, the program that lets users create and manage cron table entries
- /var/spool/cron, the directory that holds cron files created by users
- /etc/cron.d, the directory that holds cron files created by package installation scripts
- /etc/cron.allow and /etc/cron.deny, files that let restrict access to the cron system

The next section explains user cron tables and how to use them. How section explains the system cron table; remaining sections of the chapter explain the default jobs included in the system cron table.

## User crontabs

When a user accesses the cron system, the system creates the file /var/spool/cron/user, where user is the login name of the user. This file—the cron file, cron table, or crontab—contains entries that specify what jobs to run and when to run them.

By default, ordinary users are allowed to access the cron system. However, the system administrator can restrict this privilege. If the file /etc/cron.allow exists, only users listed in the file can access the cron system. Similarly, if the file /etc/cron.deny exists, no user listed in the file can access the cron system.

A user who is allowed to access the cron system can perform these operations:

- Revise the entries in the crontab.
- List the existing cron jobs.
- Delete the crontab.

The following subsections explain these operations.

## Editing the User crontab

A user can edit the user's crontab entries by issuing the command

```
crontab -e
```

Similarly, the root user can edit a user's crontab entries by issuing a command of the form

```
crontab -u user -e
```

where user is the login name of the user whose crontab is to be edited.

In response to the crontab -e command, the cron system will launch the default system editor. If you prefer to use a different editor, you can set the environment variable EDITOR before issuing the crontab command. For example,

```
export EDITOR=/usr/bin/pico
crontab -e
```

lets the user edit the crontab by using the pico editor.

A user can remove the user's crontab entirely, by issuing the command

```
crontab -r
```

The root user can remove a user's crontab by issuing a command of the form

```
crontab -u user -r
```

where user is the login name of the user whose crontab is to be removed.

The crontab entries are specified as specially formatted lines; the next subsection explains the format in which they may appear.

## Format of the crontab File

The crontab file may contain these sorts of lines:

- Comment lines
- Environment settings
- cron commands

Within a line, leading spaces and tabs are ignored. Blank lines and lines beginning with a hash mark (#) are considered comment lines and are ignored by the cron system.

## Specifying Environment Settings

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

Environment settings lines have the form

```
name = value
```

- SHELL is bound to /bin/sh
- LOGNAME is bound to /etc/passwd
- HOME is bound to /home

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

## Specifying Commands

Within a line, leading spaces and tabs are ignored. Blank lines and lines beginning with a hash mark (#) are considered comment lines and are ignored by the cron system.

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

| Field | Description |
| --- | --- |
| minute | A value from 0 to 59, or * |
| hour | A value from 0 to 23, or * |
| day_month | A value from 1 to 31, or * |
| month | A value from 1 to 12, or * |
| day_week | A value from 0 to 7, or * |

The cron system lets the system administrator and ordinary schedule jobs for automatic execution at specified intervals and times. By default, a Red Hat Linux system runs several cron jobs that facilitate system administration. As a Red Hat Linux system administrator, you, need to know how to manage the cron system. You also need to understand the jobs that cron is automatically configured to run on your behalf. This chapter describes the cron system and the default jobs it runs.

## Table 16.2 Example Time Specifications in the crontab

| Time Specification | Meaning |
| --- | --- |
| 5 12 * * * | Run at 5 minutes after noon, every day. |
| 5 * * * | Run at 5 minutes after each hour. |
| 15 17 1 * * | Run at 5:15 P.M. on the first of each month. |
| 45 16 * * * | Run at 4:45 P.M. on each Friday. |
| 00 15 * 12 5 | Run at 3:00 P.M. on each Friday in December. |

