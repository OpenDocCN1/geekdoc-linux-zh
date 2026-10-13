
privileges. Red Hat Linux does not come with the sudo package, but you can get it from the ftp://contrib.redhat.com/ site. Typically, accessing Red Hat's busy FTP servers is hard, so if you are having no luck with its servers, try the http://www.courtesan.com/sudo/ site, the official sudo Web site, which has a great deal of information on sudo, including a list of FTP sites for sudo.

The main idea is to reduce superuser privileges whenever you can.

## Restricting all access in an emergency or attack

In many cases, when a system administrator detects an attack or emergency (such as a disk problem), the first task is to disallow user logins until the problem has been resolved or the system has been taken offline. Sometimes, a bit of deliberation is required by the administrator before the system can be shut down. In such a case, disallowing new logins becomes important. To disallow new logins quickly, create a file called /etc/nologin with an appropriate message to let users know why you are blocking them and when the system is expected to come back online. The presence of this file disallows any normal user login. Because superusers are allowed to log in only from the console, be sure that you have physical console access to the system, or else you might accidentally log out of your current shell sessions and lock yourself out of the system.

## Using Shadow Passwords

Only a handful of programs, including login, passwd, and so on, really need the encrypted password field in the /etc/passwd file. All the other programs just need user information, such as the username, UID, GID, and shell. Consequently, you can relocate the encrypted passwords from /etc/passwd to another file and change the programs that need access to encrypted passwords in a way that they can read this file. This file won't be world-readable, because the programs that will be allowed access will run as setuid root programs. In other words, these programs will run as root user to read the new password file. A package called Shadow Utils does all of this for you.

Shadow password support is found in the Shadow Utils package, which is not installed by default. Once installed, this package provides utilities that enable you to convert your /etc/passwd file into a password-free file. The encrypted passwords will be relocated in /etc/shadow, which will be readable only by root and any program run as setuid root. This means that a bad guy who exploits weak programs to get access to /etc/passwd may still get it, but the file will not provide any password information. The shadow utility package provides other interesting features, too, such as password aging, account expiration, and locking features. The following section describes how to use shadow passwords on your system.

## Installing the shadow utility package

Get the file shadow-utils-(version-release-architecture).rpm (for instance, shadow-utils-980403-4.i386.rpm) from your Red Hat CD-ROM or the Red Hat FTP site. Install it using the rpm utility, as follows:

```
rpm -ivh shadow utility rpm file
```

After you install the package, you need to convert the existing /etc/passwd file into a shadow password-based /etc/passwd file.

## Converting /etc/passwd and /etc/group to shadow format

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
username:passwd:last:max:must:warn:expire:disable:reserved
```

The encrypted password field (*passwd*) is now in this file. All the fields in the */etc/shadow* file are described in Table 15-1.

### Table 15-1 Fields in the /etc/shadow File

| Fields | Description |
|---|---|
| username | The username |
| passwd | The encrypted character password |
| last | Date of last password change |
| max | Minimum number of days after which the current password may be changed |
| must | Maximum number of days after which the current password must be changed |
| warn | Number of days after which the user will be warned about the current password becoming expired |
| expire | Number of days after which the current password expires and the account is disabled |
| disable | Number of days since the account has expired |

The new fields (everything but the *username* and *passwd*) can be used to provide the user accounting functionality, such as account expiration and password aging. The */usr/sbin/pwconv* utility uses the *PASS_MAX_DAYS* (maximum number of days after which the current password must be changed), *PASS_MIN_DAYS* (minimum number of days after which the current password may be changed), and *PASS_WARN_AGE* (number of days after which the user will be warned about the current password becoming expired) values from */etc/login.defs* file. Modify the */etc/login.defs* file to set desirable values for these fields.

## Managing user accounts

The shadow utility package installs replacements for utilities such as useradd, userdel, usermod, groupadd, groupdel, and groupmod, which typically are used to manage user accounts. You can run the following rpm command to find out what actually got installed when you installed this package:

```
rpm -q -l shadow-utils-version-release
```

Replace *version-release* with actual version and release information from your copy of the shadow utility package.

The new and increasingly popular linuxconf utility is also capable of working with shadow password systems. This dialog box becomes part of the user account creation process and allows you to specify information about password aging, account expiration, and so on. You can also change the default values for PASS_MAX_DAYS, PASS_MIN_DAYS, and PASS_WARN_AGE, which are stored in /etc/login.defs, using linuxconf.

## Using Pluggable Authentication Modules (PAM)

You may wonder how programs such as chsh, chfn, ftp, imap, linuxconf, login, rexec, rsh, su, login, and passwd suddenly understand the shadow password scheme and use the /etc/shadow password file for authentication. They can do so because Red Hat distributes these programs with shadow password capabilities. Actually, Red Hat ships these programs with a much grander scheme of authentication support called Pluggable Authentication Modules (PAMs). These PAM-aware programs are capable of using not only the shadow password scheme but virtually any other authentication scheme that you care to implement to enhance your system security.

Traditionally, authentication schemes are built into programs that grant privileges to users. Programs such as login or passwd used to be built with the necessary code to handle authentication. Over time, this approach proved to be really nonscalable, because incorporating a new authentication scheme required that privilege-granting programs be recoded and recompiled. To relieve the privilege-granting software developer from writing secure authentication code, PAM was developed. Figure 15-1 shows how PAM works with privilege-granting applications.

When a privilege-granting application such as /bin/login is made into a PAM-aware application, it typically works in the manner shown in Figure 15-1 and described here:

- 1. First, a user invokes such an application to access the service it offers.
- 2. The PAM-aware application calls the underlying PAM library to perform the authentication.
- 3. The PAM library looks up an application-specific configuration file in the /etc/pam.d/ directory. This file tells PAM what type of authentication is required for this application.

![](img/c2419364ebb911c809b6a79991707c27_458_0.png)

### Figure 15-1 How PAM-aware applications work

- 4. The PAM library loads the required authentication module(s).
- 5. These modules can then make PAM communicate with the conversation functions available in the application.
- 6. The conversation functions can be used to request information from the user. For example, the user can be asked to enter a password or look into a retinal scanner.
- 7. The user responds to the request by providing requested information.
- 8. The PAM authentication modules supply the application with an authentication status message via the PAM library.
- 9. If the authentication process is successful, the application grants the requested privileges to the user or informs the user about the failure.
