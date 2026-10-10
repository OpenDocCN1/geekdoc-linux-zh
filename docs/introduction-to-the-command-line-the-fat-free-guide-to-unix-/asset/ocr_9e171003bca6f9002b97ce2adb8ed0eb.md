# ## Important Files

In addition to sharing a similar directory structure, most systems will also have the important files listed in following table.

| File | Purpose |
| :--- | :--- |
| /etc/passwd | User account settings |
| /etc/shadow | Encrypted passwords for user accounts |
| /etc/group | Group settings |
| /etc/fstab | Local file system settings |
| /etc/mtab | Mounted file systems |
| /etc/inittab | System startup settings |
| /etc/exportso | NFS share settings |
| /etc/hosts | Static name resolution file |
| /etc/hostname | System host name setting |
| /etc/hosts.allow | Network hosts allowed to connect to the system |
| /etc/resolv.conf | DNS settings |
| /etc/hosts.deny | Network hosts not allowed to connect to the system |
| /etc/issue | Message displayed at shell login |
| /etc/issue.net | Remote login message |
| /etc/motd | Message displayed after logging in |
| /etc/profile | Shell environment settings |
| /etc/shells | Valid shells permitted to login |
| /etc/sudoers | Users allowed to use the su command (discussed on page 91) |
| /var/log/messages | Kernel messages log file |
| /var/log/wtmp | Current user login log file |
| /var/log/lastlog | User login history log file |
| /var/log/kern.log | Kernel log file |
| /var/log/syslog | Syslog messages log file |

This is just a brief list of the most commonly used files shared across most platforms. As a general rule, configuration files are located in the `/etc` directory and system logs are stored in `/var/log. As you become more familiar with Unix, Linux, and BSD systems you will begin working with these files to manage system configuration and troubleshoot problems.