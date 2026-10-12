
However, avoid using the root account or any superuser-equivalent account to do everyday tasks, such as sending e-mail, browsing the Web, running an IRC client to talk to friends or co-workers, transferring files via FTP, and so on.

![](img/f9ec99365f159bfe663f8ac29732663c_447_0.png)

**Tip**
Sometimes, new system administrators wonder why they can't Telnet to a system as the root user. The reason is that the */etc/securetty* file specifies which tty devices can be used for root logins. Typically, */etc/securetty* lists *tty[0-8]* as allowed devices. Because Telnet access will use pseudo tty device *pty[0-f]*, root cannot log in via Telnet. Keep */etc/securetty* as is.

- Do not log in as root or an equivalent superuser from anywhere. The preferred method of performing administrative tasks is to log in as a normal user and then use the *su* command to become a superuser (such as root). This reduces the chances of accidental damage to your system.

![](img/f9ec99365f159bfe663f8ac29732663c_447_1.png)

**Tip**
Run the *su* command with *--* as an argument so that it will make the shell a login shell, which in turn will make the shell read the shell startup files (such as *.bashrc*). This argument also makes *su* change the directory to the user's home directory.

- If you have a situation in which others need to have superuser access to perform their jobs, consider using *sudo* instead of giving everyone a superuser account. If others need to run some programs that require superuser access, you can specify these users in the */etc/sudoers* file such that they will be able to run these programs with no need to login as superuser. (The *sudo* command allows a normal user to run certain commands (specified by the superuser) as a superuser. This is a good mechanism because it is less risky than giving someone full superuser access. The *sudo* command itself runs as a setuid root. This means that when *sudo* runs, it runs as a root user process, which allows it to run other programs that require superuser privileges. Red Hat Linux does not come with the *sudo* package, but you can get it from ftp://ftp.redhat.com/ftp/site. Typically, accessing Red Hat's busy FTP servers is hard, so if you are having no luck with its servers, try http://www.courtesan.com/sudo/, the official sudo Web site, which has a great deal of information on sudo, including a list of FTP sites for sudo.

The main idea is to reduce superuser privileges whenever you can.

## Restricting all access in an emergency or attack

In many cases, when a system administrator detects an attack or emergency (such as a disk problem), the first task is to disallow user logins until the problem has been resolved or the system has been taken offline. Sometimes, a bit of deliberation is required by the administrator before the system can be shut down. In such a case, disallowing new logins becomes important. To disallow new logins quickly, create a file called `/etc/nologin` with an appropriate message to let users know why you are blocking them and when the system is expected to come back online. The presence of this file disallows any normal user login. Because superusers are allowed to log in only from the console, be sure you have physical console access to the system, or else you might accidentally log out of your current shell sessions and lock yourself out of the system.

## Using Shadow Passwords

Only a handful of programs, including login, passwd, and so on, really need the encrypted password field in the /etc/passwd file. All the other programs need only user information, such as the username, UID, GID, and shell. Consequently, you can relocate the encrypted passwords from /etc/passwd to another file and change the programs that need access to encrypted passwords in a way that they can read this file. This file won't be world-readable, because the programs that will be allowed access will be run as setuid-root programs. In other words, those programs will run as root user to read the new password file. A package called Shadow Utils does all of this for you.

Shadow password support is found in the Shadow Utils package, which is not installed by default. Once installed, this package provides utilities that enable you to convert your /etc/passwd file into a password-free file. The encrypted passwords will be relocated in /etc/shadow, which will be readable only by root and any program run as setuid root. This means that a miscreant who exploits weak programs to get access to /etc/passwd may still get to it, but the file will not provide any password information. The shadow utility package provides other interesting features, too, such as password aging, account expiration, and locking features. The following section describes how to use shadow passwords on your system.

### Installing the shadow utility package

Get the file shadow-utils-(version-release-architecture).rpm (for instance, shadow-utils-980403-4.i386.rpm) from your Red Hat CD-ROM or the Red Hat FTP site. Install it using the rpm utility, as follows:

```
rpm -ivh shadow utility rpm file
```

After you install the package, you need to convert the existing /etc/passwd file into a shadow password-based /etc/passwd file.

### Converting /etc/passwd and /etc/group to shadow format

The traditional /etc/passwd file has the following format:

```
username:passwd:UID:GID:full_name:directory:shell
```

To convert the /etc/passwd and /etc/group files to shadow /etc/passwd format, simply run

```
/usr/sbin/pwconv
```

After you convert /etc/passwd, it will have the following format:

```
username:x:UID:GID:full_name:directory:shell
```

The second field now has an x instead of the encrypted password. You also have another file called /etc/shadow, which has the following format:

```
username:passwd:last:max:min:warn:expire:disable:reserved
```

The encrypted password field (passwd) is now in this file. All the fields in the /etc/shadow file are described in Table 15-1.

**Table 15-1 Fields in the /etc/shadow File**

| Fields | Description |
|---|---|
| *username* | The username |
| *passwd* | The encrypted character password |
| *last* | Date of last password change |
| *min* | Minimum number of days after which the current password may be changed |
| *max* | Maximum number of days after which the current password must be changed |
| *warn* | Number of days after which the user will be warned about the current password becoming expired |
| *expire* | Number of days after which the current password expires and the account is disabled |
| *disable* | Number of days since the account has expired |

The new fields (everything but the *username* and *passwd*) can be used to provide the user accounting functionality, such as account expiration and password aging. The */usr/sbin/pwconv* utility uses the *PASS_MAX_DAYS* (maximum number of days after which the current password must be changed), *PASS_MIN_DAYS* (minimum number of days after which the current password may be changed), and *PASS_WARN_AGE* (number of days after which the user will be warned about the current password becoming expired) values from */etc/login.defs* file. Modify the */etc/login.defs* file to set desirable values for these fields.

### Managing user accounts

The shadow utility package installs replacements for utilities such as useradd, userdel, usermod, groupadd, groupdel, and groupmod, which typically are used to manage user accounts. You can run the following *rpm* command to find out what actually got copied when you installed this package:

```
rpm -q -l shadow-utils-version-release
```

Replace *version-release* with actual version and release information from your copy of the shadow utility package.

The new and increasingly popular *linuxconf* utility is also capable of working with shadow password systems. This dialog box becomes part of the user account creation process and allows you to specify information
