
If the OpenSSH authentication is token based, ensure that the private key was properly copied over to the server from the remote system. Also, confirm that the public key is stored in the `~/.ssh/authorized_keys` file on the client side.

![](img/c0a399aca0d18f8822d714ad0a173123_695_0.png)

If your users are employing a remote desktop application, such as VNC, xrdp, NX, or SPICE, review their configurations. More information can be found on these topics in Chapter 8.

## Authentication

Layered authentication software could be at the problem’s heart. One place to check is PAM (covered in Chapter 16). Look through the PAM configuration files, such as `/etc/pam.d/sshd`, to ensure that directives are properly set. Also employ the `pam_tally2` or `faillock` utility to check if the user’s account is locked due to too many failed login attempts.

Does your system employ other authentication products, such as LDAP (covered in Chapter 16) or Kerberos (covered in Chapter 19, “Embracing Best Security Practices”)? You’ll want to check their configuration files. Also take a look through their log files to ensure that a policy violation has not locked out the user’s account.

Don’t forget to check your Linux kernel security module, such as SELinux or AppArmor (covered in Chapter 15, “Applying Ownership and Permissions”). While the purpose of these modules is to protect the system from attackers, sometimes policy violations can lock out legitimate users. For AppArmor, policy violations are stored in either `audit.log` (produced by `auditd`) or `messages.log`, depending on its configuration. If using the `auditd` service, you can search for AppArmor policy violations in the `audit.log` file using the `ausearch` command.

For SELinux, check the audit log file using the `sealert` command, as shown in Listing 22.9. Notice that no SELinux policy violations were logged.

### Listing 22.9: Checking SELinux policy violations with the `sealert` command

```
$ sealert -a /var/log/audit/audit.log
100%: done
found 0 alerts in /var/log/audit/audit.log
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_695_1.png)

For authentication issues, peruse through these various log files as well:

- `/var/log/auth.log` (Debian-based distros)
- `/var/log/secure` (Red Hat–based distros)

These log files typically contain information such as authentication failures and can provide you with a great deal of information. Use *grep* to search for a particular username, if desired.

## Examining File Obstacles

Various problems may ensue when managing files. Understanding the typical problems will help in your file troubleshooting efforts.

### File Permissions

You’re editing a configuration file using the `vim` editor, but when you try to save the file, you get a “Can’t open file for writing” error message. That’s frustrating. Problems like this are directly related to file permissions.

When encountering these issues, first use the `ls -l` command to view a file’s permission settings and ownerships (covered in Chapter 15). Note the file’s owner and group. Then determine the permissions of the owner, group, and everyone else (world or other). An example is shown in Listing 22.10.

**Listing 22.10:** Determining file permissions with the `ls -l` command

```
$ ls -l HelloWorld.sh
-rwxr-xr-- 1 root wheel 72 Jan 4 09:29 HelloWorld.sh
$
```

In this case, the file is owned by *root*, who has permission to read, write to, and execute the file. The file’s group is *wheel*. Those members can read and execute the file. Finally, everyone else who is not the file’s owner or does not belong to the file’s group can only read the file.

If a problem occurs trying to access this file, determine the user’s username and group memberships using the `id` command. Match their identity against the file’s permissions to find the problem. An example is shown in Listing 22.11.

**Listing 22.11:** Troubleshooting file access with the `id` command

```
$ whoami
Christine
$
$ ./HelloWorld.sh
-bash: ./HelloWorld.sh: Permission denied
$ id Christine
uid=1001(Christine) gid=1001(Christine) groups=1001(Christine)
$
```

Christine cannot execute this file because she is not the file’s owner, nor is she in the file’s group (see Listing 22.10). The third permission set applies to her and only allows her to read the file. To let her run the file, add her to the wheel group, set her as the file’s owner, or modify the file’s world permissions.

### Directory Permissions

While the directory permission settings look very similar to file permissions, their effect is different. Table 22.1 shows permission effects on actions (covered in Chapter 15) associated with the entity to whom the permission applies (owner, group, or other).

**TABLE 22.1 Directory permission effects**

| Permission | Effect |
| :--------- | :---- |
| r | Allows user to display directory’s files |
| w | Allows user to create, move (rename), modify attributes, and delete files within the directory |
| x | Allows user to change their present working directory to this directory (via the cd command) as long as this permission is set in all parent directories as well |

A few examples will help you to understand these permissions. For example, the user Christine can list the /etc directory’s contents, due to the directory’s read permission for other (world), as shown snipped in Listing 22.12.

**Listing 22.12:** Understanding directory permission effects of the read privilege

```
$ whoami
Christine
$ ls -1d /etc
drwxr-xr-x. 143 root root 12288 Jan  4 09:22 /etc
$
$ ls /etc
abrt                 gshadow-             profile
adjtime              gss                  profile.d
[...]
$
```

The next example, Listing 22.13, shows that the parent directory (/home) does allow a user to use cd to change their present working directory to it. However, a subdirectory (Samantha) blocks it by not granting the execute (x) privilege.

**Listing 22.13:** Understanding directory permission effects of the execute privilege

```
$ whoami
Christine
$ ls -ld /home/
drwxr-x-x. 5 root root 52 Nov 8 14:31 /home/
$ cd /home
$ pwd
/home
$ ls -ld /home/Samantha
drwx------. 5 Samantha Samantha 128 Nov 8 14:38 /home/Samantha
$ cd /home/Samantha
-bash: cd: /home/Samantha: Permission denied
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_698_0.png)

> If a subdirectory does grant execute permission but one of its parent directories does not, a user will not be able to use cd to get to that subdirectory. All directories in that path must have the execute permission set on them for that user.

If you have a directory shared among users and they are able to delete each other's files but that is not desired, employ the sticky bit on the directory. This permission (covered in Chapter 15) will solve the problem.

## Working with Advanced Permissions

Besides the standard Linux file and directory permissions, you may run into a system that utilizes one of the more advanced Linux permission features.

Access control lists (ACLs) allow you to specify permissions for multiple users or groups besides the standard owner, group, and others set. If your Linux system utilizes ACLs, always check the getfacl utility for additional ACL permissions applied to a file or directory:

```
$ getfacl test.txt
# file: test.txt
# owner: rich
# group: rich
user::rw-
user:sales:r-x
mask::r-x
other::r--
```

In this example the owner has assigned sales group read permissions to the file using ACLs. To change ACL settings, use the `setfacl` utility.

Besides ACL permissions, Linux systems may also employ context-based permissions using either SELinux (most common in Red Hat‑based Linux distributions) or AppArmor (most common in Debian‑based Linux distributions).

To determine if SELinux is active on your Linux system, use the `sestatus` command:

```
$ sudo sestatus
SELinux status:               enabled
SELinuxfs mount:             /sys/fs/selinux
SELinux root directory:      /etc/selinux
Loaded policy name:          targeted
Current mode:                enforcing
Mode from config file:       enforcing
Policy MLS status:           enabled
Policy deny_unknown status:  allowed
Memory protection checking  actual (secure)
Max kernel policy version:   331
$
```

If SELinux is enabled, use the –Z command‑line option for the `ls` command to view additional context permissions for files and directories:

```
$ ls –Z test1.txt
unconfined_u:object_r:user_home_t:s0 test1.txt
$
```

You can change the security context for a file by using the `chcon` command:

```
chcon –u *newuser* –r *newrole* –t *newtype* *filename*
```

SELinux controls access to objects using policies. The `getsebool` command allows you to list the policies and determine if they’re active or disabled, and use the `setsebool` command to activate or deactivate them.

To determine if AppArmor is active on your system, use the `aa‑status` utility:

```
$ sudo aa‑status
apparmor module is loaded.
...
$
```
