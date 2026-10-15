
```
cupsys:x:100:106::/home/cupsys:/bin/false
messagebus:x:104:107::/var/run/dbus:/bin/false
haldaemon:x:108:108:Hardware abstraction layer,,,:/var/run/hal:/bin/false
gdm:x:105:111:Gnome Display Manager:/var/lib/gdm:/bin/false
hplip:x:106:7:HPLIP system user,,,:/var/run/hplip:/bin/false
andrew:x:1000:1000:Andrew Hudson,17,01225112233,01225445566:\
/home/andrew:/bin/bash
beagleindex:x:107:65534::/var/cache/beagle:/bin/false
```

Note that all the password fields do not show a password, but contain an x because they are shadow passwords, a useful security enhancement to Linux, discussed in the following section.

## Shadow Passwords

It is considered a security risk to keep any password in /etc/passwd because anyone with read access can run a cracking program on the file and obtain the passwords with little trouble. To avoid this risk, shadow passwords are used so that only an x appears in the password field of /etc/passwd; the real passwords are kept in /etc/shadow, a file that can only be read by the sysadmin (and PAM, the Pluggable Authentication Modules authentication manager; see the “PAM Explained” sidebar for an explanation of PAM).

Special versions of the traditional password and login programs must be used to enable shadow passwords. Shadow passwords are automatically enabled during the installation phase of the operating system on Ubuntu systems.

Let’s examine a listing of the shadow companion to /etc/passwd, the /etc/shadow file:

```
# cat /etc/shadow
root:*:13299:0:99999:7:::
daemon:*:13299:0:99999:7:::
bin:*:13299:0:99999:7:::
sys:*:13299:0:99999:7:::
sync:*:13299:0:99999:7:::
games:*:13299:0:99999:7:::
man:*:13299:0:99999:7:::
lp:*:13299:0:99999:7:::
mail:*:13299:0:99999:7:::
news:*:13299:0:99999:7:::
uucp:*:13299:0:99999:7:::
proxy:*:13299:0:99999:7:::
www-data:*:13299:0:99999:7:::
backup:*:13299:0:99999:7:::
list:*:13299:0:99999:7:::
irc:*:13299:0:99999:7:::
gnats:*:13299:0:99999:7:::
nobody:*:13299:0:99999:7:::
```

```
dhcp::!:13299:0:99999:7:::
syslog::!:13299:0:99999:7:::
klog::!:13299:0:99999:7:::
cupsys::!:13299:0:99999:7:::
messagebus::!:13299:0:99999:7:::
haldaemon::!:13299:0:99999:7:::
gdm::!:13299:0:99999:7:::
hplip::!:13299:0:99999:7:::
andrew:$1$6LT/qkWLs$PjP.20kpC8JPtRk906/:13299:0:99999:7:::
beagleindex::!:13299:0:99999:7:::
```

The fields are separated by colons and are, in order:

- The user's login name.
- The encrypted password for the user.
- The number of days since January 1, 1970 that the password was last changed. This date is known in UNIX circles as the epoch. Just so you know, the billionth second since the epoch occurred was in September 2001; that was the UNIX version of Y2K—not much happened because of it.
- The number of days before the password can be changed (prevents changing a password and then changing it back to the old password right away—a dangerous security practice).
- The number of days after which the password must be changed. This can be set to force the change of a newly issued password known to the system administrator.
- The number of days before the password expiration date that the user is warned it will expire.
- The number of days after the password expires that the account is disabled (for security).
- The number of days since January 1, 1970 that account has been disabled.
- The final field is a "reserved" field and is not currently allocated for any use.

Note that password expiration dates and warnings are disabled by default in Ubuntu. These features are not used on home systems and usually not used for small offices. It is the sysadmin's responsibility to establish and enforce password expiration policies.

The permissions on the /etc/shadow file should be set so that it is not writable or readable by regular users: The permissions should be 600.

## PAM Explained

Pluggable Authentication Modules (PAM) is a system of libraries that handle the tasks of authentication on your computer. It uses four management groups: account management, authentication management, password management, and session management. This allows the system administrator to choose how individual applications will authenticate users. Ubuntu has preinstalled and preconfigured all the necessary PAM files for you.
