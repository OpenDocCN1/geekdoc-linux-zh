```
pc-updatemanager, pc-zmanager, pfctl, pkg, restore,
(rmformat), rmuser, rsync, setfacl, shutdown, su, sudo,
(svcadm), (svcs), sysctl, tar, (ufs dump), (ufsrestore),
uncompress, (useradd), (userdel), (usermgr), (usermod), zfs,
zpool
```

# 23.1 INTRODUCTION

In order to install and maintain a UNIX system composed of both hardware and software components, it is necessary to perform the set of common tasks shown in the following sections. These common tasks may be performed by an individual exclusively for their own use on their own personal desktop/laptop/tablet computer, or may be performed by an appointed administrator for a more complex computer system used by many people. It is also possible to divide these common tasks into those performed by an autonomous administrator and a group of ordinary users. In this chapter, we use a “learning by doing” approach aimed at the individual rather than at an appointed system administrator. Even though we show the basics of those common tasks, it is possible to extrapolate from what is presented to the wider context of a larger computer system.

In order to do any of the system administration tasks in this chapter, it is necessary to either have superuser or root user privileges on the system. That means you need to know the superuser password, which you (or a designated system administrator) can establish at installation for PC-BSD and Solaris.

Both the su and sudo commands are used to execute programs and other commands with root permissions. The root user has maximum permissions, and can do anything to the system that a system administrator needs to. Normal users execute programs and commands with reduced permissions.

To execute something that requires maximum permissions, you will first have to execute the su or sudo commands.

Using the su command makes you the superuser—or root user—when you execute it with no additional options. You are prompted to enter the root account’s password. Also, the su command allows you to switch to any user account. If you execute the command su bob, you’ll be prompted to enter bob’s password, and the command shell current working directory will switch to bob’s home directory.

Once you’re done running commands in the root shell, you should type exit to leave the root shell and go back to limited-privileges mode. The root shell is not the login shell.

In comparison, sudo runs a single command with root privileges. When you execute sudo command, the system prompts you for the current user account’s password before running command as the root user. More information on the sudo command can be found in Section 23.9.2.1.

In our “learning by doing” approach, the common tasks are