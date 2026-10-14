The root user has absolute power over the running of the system. This user has access to all files and all devices and can make any changes to the system. The root user is said to have superuser privileges.

The following is a list of tasks ordinarily performed by root users:

+   - Edit files not usually changeable by ordinary users (for example, `/etc/passwd`)
+   - Change ownership and permissions of all files
+   - Execute restricted commands like mount or reboot
+   - Kill any process running on your system
+   - Add and remove user accounts
+   - Boot and shut down the system
+   - Back up the system

Many of the preceding tasks are performed by system administrators who require superuser privileges. The system administrator’s job is to manage the system by performing the preceding tasks, installing new software, analyzing system performance, and reporting hardware failures.

Depending upon your computing environment, you may or may not be the system administrator for your system or have root privileges. Your site configuration as well as your job responsibilities will determine your privileges.

If you work from a terminal or workstation that accesses a centralized system, you will probably not be the system administrator or have root privileges. In this situation, the system administrator, who is in charge of maintaining, configuring, and upgrading the system, will be the person who has root privileges.

If you perform your tasks from a workstation that is either independent or networked to other workstations or systems, you may indeed have root privileges for your own workstation, but not be the system administrator of your site. In this situation, you would maintain your own workstation only. However, the system administrator would still maintain shared machines and networks.

To become a root user, use the su command. You must also know the password for the root user. The format of the su command is:

# su

The following example shows how Juan becomes a root user to perform an administrative task:

```
```text
$ su
Password: ...
```
```