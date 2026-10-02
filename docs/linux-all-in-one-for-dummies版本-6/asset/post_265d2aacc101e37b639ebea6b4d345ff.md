
## TABLE 3-1 Some Vulnerabilities Common to Unix Systems

| Vulnerability Type | Description |
|---|---|
| BIND DNS | Berkeley Internet Name Domain (BIND) is a package that implements the Domain Name System (DNS), the Internet's name service that translates a name to an IP address. Some versions of BIND have vulnerabilities. |
| Apache Web Server | Some Apache Web Server modules (such as mod_ssl) have known vulnerabilities. Any vulnerability in Common Gateway Interface (CGI) programs used with web servers to process interactive web pages can give attackers a way to gain access to a system. |
| Authentication | User accounts sometimes have no passwords or have weak passwords that are easily cracked by password-cracking programs. |
| CVS, Subversion | Concurrent Versions System (CVS) is a popular source-code control system used in Linux systems. Subversion is another version control system for Linux that is becoming popular. These version control systems have vulnerabilities that can enable an attacker to execute arbitrary code on the system. |
| sendmail | sendmail is a complex program used to transport mail messages from one system to another, and some versions of sendmail have vulnerabilities. |
| SNMP | Simple Network Management Protocol (SNMP) is used to remotely monitor and administer various network-connected systems ranging from routers to computers. SNMP lacks good access control, so an attacker may be able to reconfigure or shut down your system if it's running SNMP. |
| Open Secure Sockets Layer (OpenSSL) | Many applications, such as Apache Web Server, use OpenSSL to provide cryptographic security for a network connection. Unfortunately, some versions of OpenSSL have known vulnerabilities that could be exploited. |
| Network File System (NFS) and Network Information Service (NIS) | Both NFS and NIS have many security problems (such as buffer overflow, potential for denial-of-service attacks, and weak authentication). Also, NFS and NIS are often misconfigured, which could allow local and remote users to exploit the security holes. |
| Databases | Databases such as MySQL and PostgreSQL are complex applications that can be difficult to configure and secure correctly. These databases have many features that can be misused or exploited to compromise the confidentiality, availability, and integrity of data. |
| Linux kernel | The Linux kernel is susceptible to many vulnerabilities, such as denial of service, execution of arbitrary code, and root-level access to the system. |

## Host-security review

When reviewing host security, focus on assessing the security mechanisms in each of the following areas:

- **Prevention:** Install operating-system updates, secure passwords, improve file permissions, set up a password for a bootloader, and use encryption.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_435_0.png)

- **Detection:** Capture log messages, and check file integrity with Tripwire (a tool that can detect changes in system files).

Tripwire started as open-source but no longer is. You can still search for and download the original.

- **Response:** Make routine backups and develop incident-response procedures.

The following sections review a few of these host-security mechanisms.

## Operating system updates

Linux distributions release updates soon. When security vulnerabilities are found, Linux distributions release an update to fix the problem. Many distributions offer online updates that you can enable and use to keep your system up to date. The details of updating the operating system depend on the distribution. (See Book 5, Chapter 4 for information on how to update Linux online.)

## File permissions

Protect important system files with appropriate file ownerships and file permissions. The key procedures in assigning file-system ownerships and permissions are as follows:

- Figure out which files contain sensitive information and why. Some files may contain sensitive data related to your work or business, whereas many other files are sensitive because they control the Linux system configuration.
- Maintain a current list of authorized users and what they're authorized to do on the system.
- Set up passwords, groups, file ownerships, and file permissions to allow only authorized users to access the files.

Table 3-2 lists some important system files in Linux, showing the typical numeric permission setting for each file (which may differ slightly depending on the distribution). See Book 6, Chapter 2 for more information on numeric permission settings.

Another important check is for executable program files that have the setuid permission. If a program has setuid permission and is owned by root, the program runs with root privileges no matter who actually runs the program. You can find all setuid programs with the following find command:

```
find / -perm +4000 -print
```

## TABLE 3-2 Important System Files and Their Permissions

| File Pathname | Permission | Description |
|---|---|---|
| /boot/grub/menu.lst | 600 | GRUB bootloader menu file |
| /etc/cron.allow | 400 | List of users permitted to use cron to submit periodic jobs |
| /etc/cron.deny | 400 | List of users who can't use cron to submit periodic jobs |
| /etc/crontab | 644 | Systemwide periodic jobs |
| /etc/hosts.allow | 644 | List of hosts allowed to use Internet services that are started with TCP wrappers |
| /etc/hosts.deny | 644 | List of hosts denied access to Internet services that are started with TCP wrappers |
| /etc/logrotate.conf | 644 | File that controls how log files rotate |
| /etc/pam.d | 755 | Directory with configuration files for pluggable authentication modules (PAMs) |
| /etc/passwd | 644 | Old-style password file with user account information but not the passwords |
| /etc/rc.d | 755 | Directory with system-startup scripts |
| /etc/securetty | 600 | TTY interfaces (terminals) from which root can log in |
| /etc/security | 755 | Policy files that control system access |
| /etc/shadow | 400 | File with encrypted passwords and password expiration information |
| /etc/shutdown.allow | 400 | Users who can shut down or reboot by pressing Ctrl+Alt+Delete |
| /etc/ssh | 755 | Directory with configuration files for SSH |
| /etc/sysconfig | 755 | System configuration files |
| /etc/sysctl.conf | 644 | Kernel configuration parameters |
| /etc/syslog.conf | 644 | Configuration file for the syslogd server that logs messages |
| /etc/udev/udev.conf | 644 | Configuration file for udev — the program that provides the capability to dynamically name hot-pluggable devices and create the device files in the /dev directory |
| /etc/vsftpd | 600 | Configuration file for the Very Secure FTP server |
| /etc/vsftpd.ftppers | 600 | List of users who aren't allowed to use FTP to transfer files |
| /etc/xinetd.conf | 644 | Configuration file for the xinetd server |
| /etc/xinetd.d | 755 | Directory containing configuration files for specific services that the xinetd server can start |
| /var/log | 755 | Directory with all log files |
| /var/log/lastlog | 644 | Information about all previous logins |
| /var/log/messages | 644 | Main system message log file |
| /var/log/wtmp | 664 | Information about current logins |

You may want to save the output in a file (append filename to the command) and then examine the file for any unusual setuid programs. A setuid program in a user's home directory, for example, is unusual.

## Password security

Verify that the password, group, and shadow password files are protected. In particular, the shadow password file has to be write-protected and readable only by root. Table 3-3 shows the password filenames and their recommended permissions.

## TABLE 3-3

## Ownership and Permission of Password Files

| File Pathname | Ownership | Permission |
|---|---|---|
| /etc/group | root.root | 644 |
| /etc/passwd | root.root | 644 |
| /etc/shadow | root.root | 400 |

## Incident response

Incident response is the policy that tells you what to do if something unusual happens to the system. The policy tells you how to proceed if someone breaks into your system.

Your response to an incident depends on how you use your system and how important the system is to you or your business. For a comprehensive incident response, remember these key points:

- Figure out how critical and important your computer and network are and identify who or what resources can help you protect your system.
