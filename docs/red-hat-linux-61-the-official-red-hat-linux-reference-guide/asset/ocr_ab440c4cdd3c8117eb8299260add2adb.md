198

Chapter 14. Pluggable Authentication Modules (PAM)

# 14.3.1. Module Interface

There are four types of PAM module interfaces which correlate to different aspects of the authorization process:

+   - auth — These modules authenticate the user by, for example, asking for and checking a password. Modules with this interface can also set credentials, such as group membership or Kerberos tickets.
- account — These modules verify that access is allowed. For example, it can check if a user account is expired or is allowed to log in at a particular time of day.
- password — These modules set and verify passwords.
- session — These modules configure and manage user sessions. Modules with this interface can also perform additional tasks that are needed to allow access, like mounting a user's home directory and making the user's mailbox available.

![](bbox=[0.095, 0.323, 0.135, 0.353])

Note

An individual module can provide any or all module interfaces. For instance, pam_unix.so provides all four interfaces.

In a PAM configuration file, the module interface is the first field defined. For example a typical line in a configuration may look like:

```
auth required /lib/security/pam_unix.so
```

This instructs PAM to use the pam_unix.so module's auth interface.

# 14.3.1.1. Stacking Modules

Module directives can be stacked, or placed upon one another, so that multiple modules are used together for one purpose. For this reason, the order in which the modules are listed is very important to the authentication process.

Stacking makes it very easy for an administrator to require specific conditions to exist before allowing the user to authenticate. For example, login normally uses five stacked auth modules, as seen in its PAM configuration file:

```
auth required /lib/security/pam_nologin.so
auth required /lib/security/pam_securetty.so
auth required /lib/security/pam_env.so
auth sufficient /lib/security/pam_hosts_auth.so
auth required /lib/security/pam_stack.so service=system-auth
```

Before someone is allowed to use login, PAM verifies that the /etc/in file does not exist, that they are not trying to log in remotely as a root user over an unencrypted network connection, and that any environmental variables can be loaded. If, a successful hosts authentication is performed, the connection is allowed. If the hosts authentication fails, then a standard password authentication is performed.