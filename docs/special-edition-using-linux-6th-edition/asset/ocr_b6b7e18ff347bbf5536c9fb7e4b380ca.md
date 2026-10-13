**Table 15.1 Continued**

| Module | Type | Arguments | Description |
|---|---|---|---|
|  |  | nodelay<br>nis<br>remember=X |  |
| user_db | auth | debug<br>db=[path]<br>icase<br>dump | Uses a .db database file to authenticate users. |
| warn | all | none | Always returns IGNORE. Makes an entry in syslog. Is a diagnostic tool. |
| wheel | auth | debug<br>user_uid<br>trust<br>deny<br>group= | Allows only root authentication to members of wheel group. This group is used on some systems as the administration group (but is not used as such in most Linux distributions). |

# STACKING MODULES

When required, more than one module can be used for any given type. This is often the case with auth. If you look at Listing 15.2 again, you’ll see that four different modules are checked for the auth type. If root is trying to log in, he must first be on a secure terminal, but he is still going to pass through the other tests. Anyone listed in an .rhosts or hosts.equiv file and permitted access stops at the second module; otherwise, all further modules are run.

This provides a great deal of flexibility and a “layered defense” so that one weak link doesn’t cause a breach. Be careful. You should thoroughly test several scenarios after changing the pam authentication file for a service because you can easily defeat any security you had through a misconfiguration. Be sure you understand the module and its use before trying to install it.

# MODIFYING YOUR PAM CONFIGURATION

Three files that you might think should be somewhat similar are the three “r” command PAM files. The r commands are considered extremely insecure (and rightly so); therefore, the PAM files should be fairly strict.

Examining the default rlogin file from Caldera OpenLinux in Listing 15.3, you can see that it is fairly strict.

```
**Listing 15.3 — Default rlogin Listing**

```text
#%PAM-1.0
auth       required     /lib/security/pam_securetty.so
auth       sufficient   /lib/security/pam_rhosts_auth.so
auth       required     /lib/security/pam_pwdb.so shadow nullok
auth       required     /lib/security/pam_nologin.so
account    required     /lib/security/pam_pwdb.so
#password  required     /lib/security/pam_cracklib.so
password   required     /lib/security/pam_pwdb.so shadow nullok use_authtok
session    required     /lib/security/pam_pwdb.so
```
```