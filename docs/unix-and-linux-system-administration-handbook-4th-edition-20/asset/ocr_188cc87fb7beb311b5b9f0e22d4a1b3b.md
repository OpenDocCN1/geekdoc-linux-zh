# A detailed Linux configuration example

Let’s look at the specific modules.

The pam_authtok_get library routine prompts the user for a login name (if one has not already been set) and password and stores these values in the token called PAM_AUTHTOK. The pam_dhkeys module is used for RPC (re-procedure call) authentication for NIS or NIS+ and is looking for Diffie-Hellman keys, hence the name.

The pam_unix_cred module sets the credentials for the authenticated user, and the pam_unix_auth module performs the actual authentication, checking the value stored in PAM_AUTHTOK is the user’s correct password. Finally, the module pam_dial_auth authenticates the user for dialup access according to the contents of /etc/dialups and /etc/d_passwd.

You may see the same module referred to more than once in a configuration file, with different module-type values. That’s fine; multiple type implementations are often collected into a single library if they share significant code.

# A detailed Linux configuration example

Linux moves each set of PAM configuration lines that refer to the same service into a separate file after that. The format is the same except that the service field is no longer needed.

For example, the /etc/pam.d/login file from a SUSE system is reproduced with the included expanded to form a more coherent example.

```
auth requisite pam_nologin.so
auth requisite [user_unknown]ignore success=ok ignore=ignore auth_err=die
      default=bad] pam_security.so
auth required pam_env.so
auth required pam_unix2.so
account required pam_unix2.so
password requisite pam_pwck.so null cracklib
password required pam_unix2.so use_authtok null
session required pam_loginuid.so
session required pam_limits.so
session required pam_unix2.so
session optional pam_umask.so
session optional required pam_lastlog.so nowtmp
session optional pam_mail.so standard
session optional pam_ck_connector.so
```

The auth stack includes several modules. On the first line, the pam_nologin module checks for the existence of the /etc/nologin file. If it exists, the module aborts the login immediately unless the user is root. The pam_secure module ensures that root can only log in on terminals listed in /etc/security. This line uses the alternative Linux syntax described in the pam.conf page. In this case, the requested behavior is similar to that of the required control flag. pam_env sets environment variables from /etc/security/pam_env.conf, and