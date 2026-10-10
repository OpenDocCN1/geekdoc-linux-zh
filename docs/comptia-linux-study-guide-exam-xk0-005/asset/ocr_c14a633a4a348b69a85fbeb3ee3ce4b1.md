# Enforcing Strong Passwords

When a password is modified via the `passwd` command, PAM is employed. These various PAM modules can help to enforce strong passwords:

+   *   `pam_unix.so`
+   *   `pam_pwquality.so`

![](bbox=[0.13, 0.27, 0.87, 0.38])

The `pam_unix.so` module performs authentication using account and password data stored in the `/etc/passwd` and `/etc/shadow` files.

The `pam_pwhistory.so` module checks a user’s newly entered password against a history database to prevent a user from reusing an old password. The password history file, `/etc/security/opasswd`, is locked down. Passwords are also stored salted and hashed, using the same hashing algorithm employed for passwords stored in the `/etc/shadow` file.

To use the `pam_pwhistory.so` module, you must modify one of the `/etc/pam.d` configuration files. Along with specifying the password type and the module name, you can set one or more of the *MODULE-OPTIONS* listed in Table 16.3.

**TABLE 16.3** The *MODULE-OPTIONS* for password reuse prevention
| Module option | Description |
| :--- | :--- |
| `enforce_for_root` | If this option is used, the root account must have its password checked for reuse when resetting its password. |
| `remember=N` | Designates that *N* passwords will be remembered. The default is 10, and the maximum is 40. |
| `retry=N` | Limits the number of reused password entries to *N* before returning with an error. The default is 1. |

For Ubuntu, you need to put this configuration information in the `/etc/pam.d/` `common-password` and `/etc/pam.d/` `common-auth` files. For other distributions, you put this configuration in the system’s default `/etc/pam.d/` files `password-auth` and `system-auth`.