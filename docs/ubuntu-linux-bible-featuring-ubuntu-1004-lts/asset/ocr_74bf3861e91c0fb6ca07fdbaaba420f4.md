# Part III: Ubuntu System Administrators

12. Includes the contents of the file /etc/pam.d/common-account, which provides a common set of PAM rules for verifying that the user has a valid account on the system. On Ubuntu systems that use /etc/passwd and /etc/shadow password authentication, this file contains the following PAM rules:

```
account [success=1 default=ignore] pam_unix.so
account requisite pam_deny.so
account required pam_permit.so
```

The first rule invokes the pam_unix.so module to perform the traditional Linux authentication check that the user's account is not marked as expired in the file /etc/shadow. This PAM sets the account stack value to 1 upon success but is not sufficient to enable a user to log in. If this succeeds, the other rules in this file are not invoked. If the first rule fails, the second rule immediately returns failure to prevent authentication. The third rule puts a positive return value on the auth stack if no value is already present, but should not be reached.

On Ubuntu systems where other authentication mechanisms, such as LDAP, Kerberos, or fingerprint sweeping, have been installed, this file would invoke the PAMs specific to verifying accounts as required by those services.

13. Includes the contents of the file /etc/pam.d/common-session, which provides a common set of PAM rules for interactive and noninteractive login sessions. On Ubuntu systems that use /etc/passwd and /etc/shadow authentication, this file contains the following PAM rules:

```
session [default=1] pam_permit.so
session requisite pam_deny.so
session required pam_permit.so
session required pam_unix.so
session optional pam_ck_connector.so noxill
```

The first rule invokes the pam_permit.so module to permit access to the system and sets the session stack value to 1 if no value has been set. If the first rule fails, the second rule immediately returns failure to prevent session authentication. If this rule fails for reason, the third rule puts a positive return value on the auth stack if no value is already present, but should not be reached. The fourth rule invokes the pam_unix.so module to create a log entry to the syslog service identifying the beginning of user's login session on the current system. This PAM succeeds but is not sufficient to enable a user to log in. The last rule invokes the pam_ck_connector.so module to register a non-X11 login session with the ConsoleKit daemon, meaning that the daemon recognizes that login on the physical console has occurred.

14. Includes the contents of the file /etc/pam.d/common-password, which provides a common set of PAM rules for actually checking a password. On Ubuntu systems that