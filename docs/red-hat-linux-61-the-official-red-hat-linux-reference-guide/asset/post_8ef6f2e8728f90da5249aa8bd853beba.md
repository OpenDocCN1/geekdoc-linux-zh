
# Pluggable Authentication Modules (PAM)

Programs which allow users access to a system verify the user's identity through a process called authentication. Historically, each such program had its own way of performing the task of authentication. Under Red Hat Linux, many such programs are configured to use a centralized authentication process called Pluggable Authentication Modules (PAM).

PAM uses a pluggable, modular architecture, which affords the system administrator a great deal of flexibility in setting authentication policies for the system.

In most situations, the default PAM configuration file for a PAM-aware application is sufficient. However, sometimes it may become necessary to edit a PAM configuration file. Because misconfiguration of PAM can compromise system security, it is important to understand the structure of these files before making any modifications (refer to Section 14.3 PAM Configuration File Format for more information).

## 14.1. Advantages of PAM

PAM offers the following advantages:

- Provides a common authentication scheme that can be used with a wide variety of applications.
- Allows a large amount of flexibility and control over authentication for both the system administrator and application developer.
- Allows application developers to develop programs without creating their own authentication scheme.

## 14.2. /etc/pam.d/ Configuration Files

The directory /etc/pam.d/ contains the PAM configuration files for each PAM-aware applications. In earlier versions of PAM, the file /etc/pam.conf was used, but this file is now deprecated and pam.conf is only read if the /etc/pam.d/ directory does not exist.

### 14.2.1. PAM Service Files

Each PAM-aware application or service has a file within the /etc/pam.d/ directory. Each of these is named after the service for which it controls access.

It is up to the PAM-aware program to define its service name and install the PAM configuration file in the /etc/pam.d/ directory. For example, the login program defines its service name as /etc/pam.d/login.

## 14.3. PAM Configuration File Format

Each PAM configuration file contains a group of directives formatted as follows:

```
<module interface> <control flag> <module path> <module arguments>
```

Each of these elements are explained in the following sections.

### 14.3.1. Module Interface

There are four types of PAM module interfaces which correlate to different aspects of the authorization process:

- auth — These modules authenticate the user by, for example, asking for and checking a password. Modules with this interface can also set credentials, such as group membership or Kerberos tickets.
- account — These modules verify that access is allowed. For example, it can check if a user account is expired or is allowed to log in at a particular time of day.
- password — These modules set and verify passwords.
- session — These modules configure and manage user sessions. Modules with this interface can also perform additional tasks that are needed to allow access, like mounting a user's home directory and making the user's mailbox available.

![](img/31025704b51d5760c0228ff0f3db98bf_213_0.png)

Note

An individual module can provide any or all module interfaces. For instance, pam_unix.so provides all four interfaces.

In a PAM configuration file, the module interface is the first field defined. For example, a typical line in a configuration may look like:

```
auth required /lib/security/pam_unix.so
```

This instructs PAM to use the pam_unix.so module's auth interface.

### 14.3.1.1. Stacking Modules

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

## 14.3.2. Control Flag

All PAM modules generate a success or failure result when called. Control flags tell PAM what to do with the result. Since modules can be stacked in a particular order, control flags decide how important the success or failure of a particular module is to the overall goal of authenticating the user to the service.

There are four predefined flags:

- **required**— The module must be successful for authentication to continue. If a required module fails, the user is not notified until all modules referencing that interface are completed.
- **requisite**— The module must be successful for authentication to continue. However, if a requisite module fails, the user is notified immediately.
- **sufficient**— The module must be successful for authentication to continue. If a sufficient module succeeds, the authentication is allowed unless a previous required module failed.
- **optional**— The module result is ignored if it fails, unless it is the only module in the stack.

In a PAM configuration file, the module interface is the first field defined. For example a typical line in a configuration may look like:

```
auth required /lib/security/pam_unix.so
```

This instructs PAM to use the pam_unix.so module's auth interface.

### 14.3.3. Module Path

Module paths tell PAM where to find the module. Usually, it is in `/lib/security/`, the location for PAM.

### 14.3.4. Module Arguments

PAM uses arguments to pass information to the module. For example, `pam_unix.so` takes `db` argument.

## 14.4. Sample Configuration Files

Below is a sample application configuration:

```
#PAM-1.0
auth required /lib/security/pam_security.so
auth required /lib/security/pam_unix.so nullock
auth required /lib/security/pam_login.so
account required /lib/security/pam_unix.so
password required /lib/security/pam_cracklib.so retry=3
password required /lib/security/pam_unix.so shadow nullok
session required /lib/security/pam_unix.so
```

The first line is a comment as demonstrated by the hash mark (#) at the beginning of the line. Lines through three are for login authentication.
