+   Maintain a current list of authorized users and what they are authorized to do on the system.
+   
+   Set up passwords, groups, file ownerships, and file permissions to allow only authorized users to access the files.

Table 4-2 lists some important system files in Linux, showing the numeric permission setting for each file. (See Chapter 2 of this minibook for more on numeric permission settings.)

**Table 4-2**  **Important System Files and Their Permissions**

| File Pathname | Permission | Description |
| :--- | :--- | :--- |
| /boot/grub/menu.lst | 600 | GRUB bootloader menu file |
| /etc/cron.allow | 400 | List of users permitted to use cron to submit periodic jobs |
| /etc/cron.deny | 400 | List of users who cannot use cron to submit periodic jobs |
| /etc/crontab | 644 | System-wide periodic jobs |
| /etc/hosts.allow | 644 | List of hosts allowed to use Internet services that are started using TCP wrappers |
| /etc/hosts.deny | 644 | List of hosts denied access to Internet services that are started using TCP wrappers |
| /etc/logrotate.conf | 644 | File that controls how log files rotate |
| /etc/pam.d | 755 | Directory with configuration files for pluggable authentication modules (PAMs) |
| /etc/passwd | 644 | Old-style password file with user account information but not the passwords |
| /etc/rc.d | 755 | Directory with system-startup scripts |
| /etc/security | 600 | TTY interfaces (terminals) from which root can log in |
| /etc/security | 755 | Policy files that control system access |
| /etc/shadow | 400 | File with encrypted passwords and password expiration information |
| /etc/shutdown.allow | 400 | Users who can shut down or reboot by pressing Ctrl+Alt+Delete |
| /etc/ssh | 755 | Directory with configuration files for the Secure Shell (SSH) |
| /etc/sysconfig | 755 | System configuration files |
| /etc/sysctl.conf | 644 | Kernel configuration parameters |
| /etc/syslog.conf | 644 | Configuration file for the syslogd server that logs messages |