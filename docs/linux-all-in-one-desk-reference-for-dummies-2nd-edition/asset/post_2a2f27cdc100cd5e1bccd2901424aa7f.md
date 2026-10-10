
## Typical Top 20 Computer Vulnerabilities

The SANS Top 20 Internet security vulnerabilities list includes several types of vulnerabilities, such as Windows, cross-platform, and UNIX. Of these, the UNIX and cross-platform vulnerabilities are relevant to Linux. Table 4-1 summarizes some common UNIX and cross-platform vulnerabilities that apply to Linux. You can read the complete details about these vulnerabilities at www.sans.org/top20.

**Table 4-1 Some Common Vulnerabilities to UNIX Systems**

| **Vulnerability Type** | **Description** |
|---|---|
| BIND DNS | Berkeley Internet Name Domain (BIND) is a package that implements Domain Name System (DNS), the Internet’s name service that translates a name to an IP address. Some versions of BIND have vulnerabilities. |
| Apache Web server | Some Apache Web server modules (such as `mod_ssl`) have known vulnerabilities. Any vulnerability in Common Gateway Interface (CGI) programs used with Web servers to process interactive Web pages can provide attackers a way to gain access to a system. |
| Authentication | User accounts often have no passwords or weak passwords that are easily cracked by password-cracking programs. |
| CVS, Subversion | Concurrent Versions System (CVS) is a popular source-code control system used in Linux systems. Subversion is another version control system for Linux that is becoming popular. These version control systems have vulnerabilities that can enable an attacker to execute arbitrary code on the system. |
| sendmail | `sendmail` is a complex program used to transport mail messages from one system to another, and some versions of `sendmail` have vulnerabilities. |
| SNMP | Simple Network Management Protocol (SNMP) is used to remotely monitor and administer various network-connected systems ranging from routers to computers. SNMP lacks good access control, so if SNMP is running on your system, an attacker may be able to reconfigure or shut down your system. |
| Open Secure Sockets Layer (OpenSSL) | Many applications, such as Apache Web server, use OpenSSL to provide cryptographic security for a network connection. Unfortunately, some versions of OpenSSL have known vulnerabilities that could be exploited. |
| Network File System (NFS) and Network Information Service (NIS) | Both NFS and NIS have many security problems (for example, buffer overflow, potential for denial-of-service attacks, and weak authentication). Also, NFS and NIS are often misconfigured, which could allow local and remote users to exploit the security holes. |
| Databases | Databases such as MySQL and PostgreSQL are complex applications and can be difficult to correctly configure and secure. These databases have many features that can be misused or exploited to compromise the confidentiality, availability, and integrity of data. To learn more about some of the common attacks on MySQL and how to defend against them, consult this paper: www.nextgenss.com/papers/HackprofingMySQL.pdf. |
| Linux kernel | The Linux kernel is susceptible to many vulnerabilities, such as denial of service, execution of arbitrary code, and root-level access to the system. |

### Host-security Review

When reviewing host security, focus on assessing the security mechanisms in each of the following areas:

- **Prevention:** Install operating system updates, secure passwords, improve file permissions, set up a password for a boot loader, and use encryption
- **Detection:** Capture log messages and check file integrity with Tripwire (a tool that can detect changes to system files)
- **Response:** Make routine backups and develop incident response procedures

I review a few of these host-security mechanisms in the upcoming sections.

### Operating System Updates

Linux distributions release updates soon after security vulnerabilities are found. Many distributions offer online updates that you can enable and use to keep your system up to date. The exact details of updating the operating system depend on the distribution. See Book V, Chapter 4 for information on how to update Linux online.

### File Permissions

Protect key system files with appropriate file ownerships and file permissions. The key procedures in assigning file-system ownerships and permissions are as follows:

- Figure out which files contain sensitive information and why. Some files may contain sensitive data related to your work or business, whereas many other files are sensitive because they control the Linux system configuration.
- Maintain a current list of authorized users and what they are authorized to do on the system.
- Set up passwords, groups, file ownerships, and file permissions to allow only authorized users to access the files.

Table 4-2 lists some important system files in Linux, showing the numeric permission setting for each file. (See Chapter 2 of this minibook for more on numeric permission settings.)

**Table 4-2 Important System Files and Their Permissions**

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
| /etc/udev/udev.conf | 644 | Configuration file for udev—the program that provides the ability to dynamically name hot-pluggable devices and create the device files in the `/dev` directory |
| /etc/vsftpd | 600 | Configuration file for the Very Secure FTP server |
| /etc/vsftpd.ftpusers | 600 | List of users who cannot use FTP to transfer files |
| /etc/xinetd.conf | 644 | Configuration file for the xinetd server |
| /etc/xinetd.d | 755 | Directory containing configuration files for specific services that the xinetd server can start |
| /var/log | 755 | Directory with all log files |
| /var/log/lastlog | 644 | Information about all previous logins |
| /var/log/messages | 644 | Main system message log file |
| /var/log/wtmp | 664 | Information about current logins |

Another important check is to look for executable program files that have the *setuid* permission. If a program has *setuid* permission and it’s owned by *root*, then the program runs with *root* privileges, no matter who actually runs the program. You can find all *setuid* programs with the following *find* command:

```bash
find / -perm +4000 -print
```

You may want to save the output in a file (just append > *filename* to the command) and then examine the file for any unusual *setuid* programs. For example, a *setuid* program in a user’s home directory is unusual.

### Password Security

Verify that the *password*, *group*, and *shadow* password files are protected. In particular, the shadow password file has to be write-protected and readable only by *root*. The filenames and their recommended permissions are shown in Table 4-3.

**Table 4-3 Ownership and Permission of Password Files**

| File Pathname | Ownership | Permission |
| :--- | :--- | :--- |
| /etc/group | root.root | 644 |
| /etc/passwd | root.root | 644 |
| /etc/shadow | root.root | 400 |
