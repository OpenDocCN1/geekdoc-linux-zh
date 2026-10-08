# 96 CONFIGURATION AND ADMINISTRATION

a login without a password is allowed. If this is the case, the user check terminates at this point.

```
auth required      /lib/security/pam_securetty.so
auth sufficient    /lib/security/pam_rhosts_auth.so
auth required       /lib/security/pam_pwdb.so \
               shadow nullok
auth required      /lib/security/pam_login.so
account required    /lib/security/pam_pwdb.so
password required   /lib/security/pam_cracklib.so
password required   /lib/security/pam_pwdb.so \
               shadow nullok use authtok
session required    /lib/security/pam_pwdb.so
```

**Listing 4.10** the /etc/pam.d/login as a second example.

If a login without a password is not possible, the normal password routine of the UNIX system is used. Again, a few and relatively simple modules are sufficient to emulate the behaviour of traditional UNIX systems. It is expected that more and more LINUX distributions and other UNIX systems will include this library. However, I would not recommend a manual change without the aid of a distribution.

LINUX PAM contains lots of modules for authentication or session management. You may use even a Windows system to authenticate against, as well as LDAP or RADIUS servers. The Debian Distribution has created a mini-Policy regarding the usage of PAM in other packages, so all packages use PAM in the same way.

For a complete list of modules, their usage and parameters refer to the documentation included in the PAM package.

| Additional Information and Sources |
|---|
| ftp host: tsx-11.with.edu |
| ftp path: /pub/linux/ALPHA/PAM/ |
| PAM RFC: http://www.pilgrim.umass.edu/pub/os_dce/RFC/rfc86.0.txt |
| LINUX PAM: http://parc.power.net/morgan/Linux-PAM/ |

# User groups

In the /etc/passwd file, a user ID is assigned to a group. Which group this can be discovered by means of the id command or can be read from the password file. This group is the standard group of the user and is used, for