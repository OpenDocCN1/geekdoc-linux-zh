+   * /etc/pam.d/gdm-smartcard
+   * /etc/pam.d/kdm
+   * /etc/pam.d/gdm-np
+   * /etc/pam.d/xdm

> WARNING
> 
> A blank /etc/security file does *not* prevent the *root* user from logging in remotely using the OpenSSH suite of tools because the console is not opened until after authentication.

Table 4.3. Disabling Root Logins

| Effects | Does Not Affect |
| --- |
| Prevents access to the **root** account using the console or the network. The following programs are prevented from accessing the **root** account:
* login
* gdm
* kdm
* xdm
* Other network services that open a tty |
| Programs that do not log in as **root**, but perform administrative tasks through *setuid* or other mechanisms. The following programs are *not* prevented from accessing the **root** account:
* su
* sudo
* ssh
* scp
* sftp |

Disabling root SSH logins
To prevent **root** logins through the SSH protocol, edit the SSH daemon's configuration file, /etc/ssh/sshd_config, and change the line that reads:

```
#PermitRootLogin yes
```

to read as follows:

```
PermitRootLogin no
```

Table 4.4. Disabling Root SSH Logins