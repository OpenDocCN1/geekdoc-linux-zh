The first line prohibits root from using rlogin except from a secure terminal as listed in `/etc/securetty`. The second line will permit a login without going further if an rhosts file exists. If you believe that rhosts files are not a good idea, you might want to remove this line.

The rest of the file looks much like the login file, but it might be a good idea to copy the `pam_lastlog.so` line just to make sure the session is logged. However, remember that this last log entry must appear before the `pam_rhosts.so` line or the session will not be logged if access is permitted using the rhosts file.

Examining Listing 15.4, the default Caldera OpenLinux rexec, though, is a little on the thin side.

# LISTING 15.4 — THE DEFAULT rexec FILE

```
```text
#%PAM-1.0
auth       required    /lib/security/pam_pwdb.so shadow nullok
auth       required    /lib/security/pam_nologin.so
auth       required    /lib/security/pam_listfile.so file=/etc/ftpusers item=user
➜sense=deny onerr=succeed
account    required    /lib/security/pam_pwdb.so
```
```

This file completely prevents root from using rexec, and does not make use of the rhosts files at all (if you consider that desirable). No logging takes place with this rexec file. A great security improvement here (if there is such a thing as security with rexec) would be to use the rlogin file from listing 15.3 with the improvements mentioned above.

Examining Listing 15.5, the default Caldera OpenLinux rsh file is in the same shape as rexec.

# LISTING 15.5 — THE DEFAULT rsh FILE

```
```text
#%PAM-1.0
auth       required    /lib/security/pam_rhosts_auth.so
auth       required    /lib/security/pam_nologin.so
account    required    /lib/security/pam_pwdb.so
session    required    /lib/security/pam_pwdb.so
```
```

This file requires rhosts; you can’t use rsh without it. Beyond that, root is permitted along with everyone else. This prevents the passing of passwords in the clear, a problem with older restricted services. This file shows another way to provide an r command. You might want to at least add the `pam_lastlog` line and `pam_securetty` lines to improve security and add a log event. This file, with these modifications, would also suffice for both the rlogin and rexec files. The choices are yours.

# TROUBLESHOOTING

> > I tried to log in using telnet as root, but received a login incorrect, and I know I used the correct password for root.