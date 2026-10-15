# 23.8.4.4 rsyslog

System logging can be accomplished in a more precise, capable, and extensive way using the rsyslog utility. By default, rsyslog is not installed on PC-BSD or Solaris systems. It can be installed by using the pkg management utility on both systems via the following command:

```
% pkg install rsyslog
```

The syslogd daemon must then be disabled on both PC-BSD and Solaris before you can use rsyslog. To accomplish this in Solaris, use the following command:

```
% svcadm disable svc:/system/system-log:default
```

On PC-BSD, follow the instructions given at the end of the pkg install command. For more information on rsyslog, see the website www.rsyslog.com.

# 23.9 SYSTEM SECURITY

There are various techniques for securing a UNIX system, implemented from the single-user level on up to the most general system level. These techniques fall into the following areas:

+   - Password-Based Authentication
+   - Access Control: Discretionary (DAC), Mandatory (MAC), or Role-Based (RBAC)
+   - Using Access Control Lists (ACLs) in PC-BSD
+   - Intrusion Detection and Intrusion Detection Systems
+   - UNIX Security Software
+   - System Firewall

# 23.9.1 Password-Based Authentication

The first line of defense in system security, and the technique employed almost universally across many types of computer system, is password-based authentication. The UNIX system compares a user-entered password at login for a users ID, compares the password to a previously established and stored one held in a password file for that user, and based on the comparison authenticates the user. The ID not only determines whether the user can gain access to the system itself, but also determines what privileges the user has—for example, superuser privilege. Also, the ID is used in discretionary access control (DAC), as shown in the Section 23.9.2. The password file and a hash/salt scheme using a SHA256 hashing algorithm for encrypting the password, work together to authenticate a users ID. The password file on the system, in /etc/passwd, holds user information and works in conjunction with the /etc/shadow (on Solaris) or /etc/master.passwd (on PC-BSD) file to authenticate a user ID.