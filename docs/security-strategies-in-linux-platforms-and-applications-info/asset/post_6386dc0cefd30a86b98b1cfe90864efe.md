
## CHAPTER 4 | User Privileges and Permissions

require the ability to write to that directory. users do not have the ability to overwrite or delete files written by other users.

While other users may be able to read what is written to /tmp, they won't be to delete or overwrite those files. If you want to set the sticky bit on a different directory, the chmod command can help. The following command sets the sticky bit on the /newtmp directory:

```
# chmod o+t /newtmp
```

Alternatively, the following command sets the sticky bit with read, write, and execute permissions for all users on the /newtmp directory:

```
# chmod 1777 /newtmp
```

## Tracking Access Logs

Linux supports logging for services and the kernel. Until recently, this was configured in two different service daemons, syslog and klog, in the /sbin/ directory. The latest versions of Linux include a successor, the /sbin/rslog daemon. The functionality has not changed. The system and kernel logs are intertwined, they're usually part of the same package, rsyslog or syslog. Ubuntu and Red Hat take different approaches to logging configurations from this file.

This section focuses on tracking access—that is, finding those logs record login attempts and especially login failures. These services classify log messages in a number of areas. The relevant areas are auth and authpriv. In the language of the log-service configuration files, auth and authpriv are known as "facilities." While both transmit the same messages, the authpriv facility is normally associated with a more secure file.

This section addresses the basics of tracking access through logs. If you're an administrator for multiple systems, however, you may prefer a system that sends you an alert when something goes wrong. That's a log-monitoring system. One option for monitoring is the logwatch log analyzer service, described in Chapter 12.

## Authorization Log Options

Many Linux distributions are in transition from syslog to the rsyslog package. The main syslog configuration file is /etc/syslog.conf. The main configuration file from the /rsyslog package package is /etc/rsyslog.conf. On Ubuntu, it refers to the 50-default.conf file in /etc/rsyslog.d/

Despite the changes to the names and locations of the configuration files, the basic directives have changed. Specifically, for Debian-based systems direct sends information on login attempts to the /var/log/auth.log file:

- auth, authpriv. * /var/log/auth.log

For Red-Hat systems, the following directive sends information on login attempts de to the /var/log/secure file:

- authpriv* /var/log/secure

![](img/c0608a8c8a0777903dfec4ff61fdffa1_126_0.png)

# FIGURE 4-2

Feb 21 10:49:28 RHELserver ssh[27551]: Invalid user test from 60.217.234.134
Feb 21 10:49:28 RHELserver ssh[27552]: input_userauth: invalid user test for user
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): check pass; user unknown known
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 rhost=60.217.234.134: retrieval error
Feb 21 10:49:28 RHELserver ssh[27551]: pam_succeeded if(sshhd:auth): error retrieving information about user test
Feb 21 10:49:30 RHELserver ssh[27551]: Failed password for invalid user test from 60.217.234.134 port 22
Feb 21 10:49:30 RHELserver ssh[27552]: Received disconnect from 60.217.234.134:
Feb 21 10:49:32 RHELserver ssh[27553]: Invalid user test from 60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27554]: input_userauth: invalid user test for
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): check pass; user unknown
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 tty=ssh rhost=60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27553]: pam_succeeded if(sshhd:auth): error retrieving information about user test

Failed remote login attempts.

## Authorization Log Files

The aforementioned log files are important tools to keep a secure system. Courtesy of the /etc/logrotate.conf file and a regular cron script, logs are rotated on a weekly basis. Linux systems configured in this way typically contain several weeks of logs. Logs from previous versions have a ? where the ? is a number. (The ? is a standard Linux alphanumeric wildcard).

The size of these logs may be important. A jump in the size of any log file indicates increased activity. While this increased activity may just be a result of user-based cron jobs running more frequently

The log excerpt in Figure 4-2 displays messages associated with an attempt to log into a system named RHELserver, first as user test and then as user test1. It provides information on the protocol, the user.

## Pluggable Modules

This section addresses the basics of tracking access through logs. If you're an administrator for multiple systems, however, you may prefer a system that sends you an alert when something goes wrong. That's a log-monitoring system. One option for monitoring is the logwatch log analyzer service, described in Chapter 12.

The aforementioned log files are important tools to keep a secure system. Courtesy of the /etc/logrotate.conf file and a regular cron script, logs are rotated on a weekly basis. Linux systems configured in this way typically contain several weeks of logs. Logs from previous versions have a ? where the ? is a number. (The ? is a standard Linux alphanumeric wildcard).

The size of these logs may be important. A jump in the size of any log file indicates increased activity. While this increased activity may just be a result of user-based cron jobs running more frequently

The log excerpt in Figure 4-2 displays messages associated with an attempt to log into a system named RHELserver, first as user test and then as user test1. It provides information on the protocol, the user.

# 102 PART 2 | Layered Security and Linux

# FIGURE 4-2

```text
Feb 21 10:49:28 RHELserver ssh[27551]: Invalid user test from 60.217.234.134
Feb 21 10:49:28 RHELserver ssh[27552]: input_userauth: invalid user test for user
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): check pass; user unknown known
Feb 21 10:49:28 RHELserver ssh[27551]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 rhost=60.217.234.134: retrieval error
Feb 21 10:49:28 RHELserver ssh[27551]: pam_succeeded if(sshhd:auth): error retrieving information about user test
Feb 21 10:49:30 RHELserver ssh[27551]: Failed password for invalid user test from 60.217.234.134 port 22
Feb 21 10:49:30 RHELserver ssh[27552]: Received disconnect from 60.217.234.134:
Feb 21 10:49:32 RHELserver ssh[27553]: Invalid user test from 60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27554]: input_userauth: invalid user test for
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): check pass; user unknown
Feb 21 10:49:32 RHELserver ssh[27553]: pam_unix(sshhd:auth): authentication failure
user login: uid=0 eid=0 tty=ssh rhost=60.217.234.134
Feb 21 10:49:32 RHELserver ssh[27553]: pam_succeeded if(sshhd:auth): error retrieving information about user test
```

Failed remote login attempts.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_126_0.png)

# CHAPTER 4 | Privileges and Permissions

# 102 PART 2 | Layered Security and Linux

```text
# apt-cache libpam
```

- pam-apparmor
- pam-blue
- pam-crack
- pam-doc
- pam-gnome-keyring
- pam-kerberos
- pam-ldap
- pam-mount
- pam-radius
- pam-runtime
- pam-sam
- pam-smart
- pam-session

PAM is configured in specific files in the /etc/pam.d/. These files, such as password and ssh, accurately depict the command or service that is regulated.

## The Structure of a PAM Configuration File

The structure of a PAM configuration file is based on its modules, available from the /lib/security/ directory. If you don't find a desired module here, you may need to install another PAM-related package. Each line in a PAM configuration file is set up in the following format:

module_type control_flag module_file (arguments)

Older versions of PAM required the full path to the module. Current versions assume the module is in the /lib/security/ directory. If installed, more information on a module_file, such as the arguments used for a module, may be available from a man page. That leaves the module_type and control_flag options. First, there are four different module types:

- authAuthenticates users by verifying passwords, group memberships, and even Kerberos tokens. Also known as authentication management.
- account—Checks the validity of the account based on expiration dates, time limits, or configuration files with restricted users. Also known as account management.
- password—Controls changes to user password. May also control the number of login attempts. Also known as password management.
- session—Makes the connection work; it may mount appropriate directories and information to system logs. Also known as session management.

There is an implicit default module type, include, which incorporates the configuration directives from another file.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_128_0.png)
