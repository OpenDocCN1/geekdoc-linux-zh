On Linux systems, the chage program controls password aging. Using chage, administrators can enforce minimum and maximum times between password changes, password expiration dates, the number of days to warn users before their passwords expire, the number of days of inactivity that are permissible before accounts are automatically locked, and more. The following command sets the minimum number of days between password changes to 2, the maximum number to 90, the expiration date to July 31, 2010, and warns the user for 14 days that the expiration date is approaching:

```
$ sudo chage -m 2 -M 90 -E 2010-07-31 -W 14 ben
```

Other systems implement password aging differently, usually with less granularity. Under Solaris, you set password aging preferences in /etc/default/password. Password aging on HP-UX systems is controlled through the smc console, and in AIX it's configured in the file /etc/security/user.

# Group logins and shared logins

Any login that is used by more than one person is bad news. Group logins (e.g., "guest" or "demo") are sure terrain for hackers to homestead and are prohibited in many contexts by federal regulations such as HIPAA. Don't allow them at your site. However, technical controls can't prevent users from sharing passwords, so education is the best enforcement tactic.

# User shells

In theory, you can set the shell for a user account to be just about any program, including a custom script. In practice, the use of shells other than standards such as bash and tcsh is a dangerous practice, and the risk is even greater for password-less logins that have a script as their shell. If you find yourself tempted to create such a login, you might consider a passphrase-less SSH key pair instead.

# Rootly entries

The only distinguishing feature of the root login is its UID of zero. Since there can be more than one entry in the /etc/passwd file that uses this UID, there can be more than one way to log in as root.

A common way for a hacker to install a back door after having obtained a root shell is to edit new root logins into /etc/passwd. Programs such as who and w refer to the name stored in utmp rather than the UID that owns the login shell, so they cannot expose hackers that appear to be innocent users but are really logged in as UID 0.

Don't allow root to log in remotely, even through the standard root account. Under OpenSSH, you can set the PermitRootLogin configuration option to No in the /etc/ssh/sshd_config file to enforce this restriction.

On Solaris, you can put CONSOLE=/dev/console in /etc/default/login to prohibit root logins from locations beside the console.