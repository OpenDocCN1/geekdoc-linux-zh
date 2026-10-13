> **exam watch**
> 
> *If the /etc/nologin file exists, regular users are not allowed to log in to the local console. Any regular user that tries to log in gets to read the contents of /etc/nologin as a message.*

500 and above. If these conditions are not met, the user is locked out (pam_deny.so).

Now return to the /etc/pam.d/login file. The next line, which looks for an account module type, checks for accounts not allowed to log in as listed in the /etc/nologin file:

```
account required pam_nologin.so
```

The following account module includes the account modules from the /etc/pam.d/system-auth configuration file:

```
account include system-auth
```

These are the account module type lines from /etc/pam.d/system-auth:

```
account required pam_unix.so
account sufficient pam_localuser.so
account sufficient pam_succeed_if.so uid < 500 quiet
account required pam_permit.so
```

The first line refers to the pam_unix.so module in the /lib/security directory, which brings up the normal username and password prompts. Based on the pam_localuser.so module, users found in /etc/passwd are automatically accepted. Based on the pam_succeed_if.so module, service users (with user IDs less than 500) are automatically logged in, without messages (quiet). The pam_permit.so module always returns success.

Now return to the /etc/pam.d/login file. The next line is a password module, which includes other password module type lines from the /etc/pam.d/system-auth file:

```
password include system-auth
```

These are the password module type lines from /etc/pam.d/system-auth:

```
password requisite pam_cracklib.so try_first_pass retry=3
password sufficient pam_unix.so sha512 shadow nullok try_first_pass \
use_authok
password required pam_deny.so
```

The first command from this list allows the use of a previously successful password (try_first_pass) and then sets a maximum of three retries. The next command encrypts passwords using the SHA512 hash, supports the Shadow Password Suite