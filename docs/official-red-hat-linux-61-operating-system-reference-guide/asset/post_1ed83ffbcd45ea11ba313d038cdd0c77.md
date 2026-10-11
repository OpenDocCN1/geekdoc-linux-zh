
- `auth` modules provide the actual authentication, perhaps asking for and checking a password, and they set "credentials" such as group membership or kerberos "tickets."
- `account` modules check to make sure that the authentication is allowed (the account has not expired, the user is allowed to log in at this time of day, and so on).
- `password` modules are used to set passwords.
- `session` modules are used once a user has been authenticated to allow them to use their account, perhaps mounting the user’s home directory or making their mailbox available.

These modules may be stacked, so that multiple modules are used. For instance, `rlogin` normally makes use of at least two authentication methods: if `rhosts` authentication succeeds, it is sufficient to allow the connection; if it fails, then standard password authentication is done.

New modules can be added at any time, and PAM-aware applications can then be made to use them. For instance, if you have a one-time-password calculator system, and you can write a module to support it (documentation on writing modules is included with the system in `/usr/doc/pam*`), PAM-aware programs can use the new module and work with the new one-time-password calculators without being recompiled or otherwise modified in any way.

## 2.6.2 Services

Each program using PAM defines its own "service" name. The login program defines the service type `login`, ftpd defines the service type `ftp`, and so on. In general, the service type is the name of the program used to access the service, not (if there is a difference) the program used to provide the service.

## 2.6.3 The Configuration Files

The directory `/etc/pam.d` is used to configure all PAM applications. (This used to be `/etc/pam.conf` in earlier PAM versions; while the `pam.conf` file is still read if no `/etc/pam.d/` entry is found, its use is deprecated.) Each application (really, each *service*) has its own file. A file looks like this:

```
#$PAM-1.0
auth       required     /lib/security/pam_securtty.so
auth       required     /lib/security/pam_pwdb.so shadow nullok
auth       required     /lib/security/pam_nologin.so
account    required     /lib/security/pam_pwdb.so
password   required     /lib/security/pam_cracklib.so
password   required     /lib/security/pam_pwdb.so shadow nullok use_authtok
session    required     /lib/security/pam_pwdb.so
```

The first line is a comment. (Any line that starts with a # character is a comment.) Lines two through four stack up three modules to use for login authorization. Line two makes sure that *if* the user is trying to log in as root, the tty on which they are logging in is listed in the `/etc/securtty` file *if* that file exists. Line three causes the user to be asked for a password and the password checked. Line four checks to see if the file `/etc/nologin` exists, and *if* it does, displays the contents of the file, and *if* the user is not root, does not let him or her log in.

Note that all three modules are checked, *even if the first module fails*. This is a security decision -- it is designed to prevent the user from knowing why their authentication was disallowed, because knowing why it was disallowed might allow them to break the authentication more easily. You can change this behavior by changing *required* to *requisite*; if any requisite module returns failure, PAM fails immediately without calling any other modules.

The fifth line causes any necessary accounting to be done. For example, if shadow passwords have been enabled, the `pam_pwdb.so` module will check to see if the account has expired, or *if* the user has not changed his or her password and the grace period for changing the password has expired.

The sixth line subjects a newly changed password to a series of tests to ensure that it cannot, for example, be easily determined by a dictionary-based password cracking program.

The seventh line (which may be wrapped) specifies that *if* the `login` program changes the user's password, it should use the `pam_pwdb.so` module to do so. (It will do so only if an auth module has determined that the password needs to be changed --- for example, if a shadow password has expired.)

The eighth and final line specifies that the *pam_pwdb.so* module should be used to manage the session. Currently, that module doesn’t do anything; it could be replaced (or supplemented by *stacking*) by any necessary module.

Note that the order of the lines within each file matters. While it doesn’t really matter much in which order required modules are called, there are other *control* flags available. While *optional* is rarely used, and never used by default on a Red Hat Linux system, sufficient and requisite cause order to become important.

Let’s look at the *auth* configuration for *rlogin*:

```
auth    required     /lib/security/pam_security.so
auth    sufficient   /lib/security/pam_rhosts_auth.so
auth    required     /lib/security/pam_pwdb.so shadow nullok
auth    required     /lib/security/pam_nologin.so
```

That looks *almost* like the *login* entry, but there’s an extra line specifying an extra module, and the modules are specified in a different order.

First, *pam_security.so* keeps root logins from happening on insecure terminals. This effectively disallows all root *rlogin* attempts. If you wish to allow them (in which case we recommend that you not be Internet-connected or be behind a good firewall), you can simply remove that line.

Second, if *pam_rhosts_auth.so* authenticates the user, PAM immediately returns success to *rlogin* without any password checking. If *pam_rhosts_auth.so* fails to authenticate the user, that failed authentication is ignored.

Third, if *pam_rhosts_auth.so* has failed to authenticate the user, the *pam_pwdb.so* module performs normal password authentication.

Finally *pam_nologin.so* checks */etc/nologin*, as specified above.

Note that if you do not want to prompt for a password if the security check fails, you can change the *pam_security.so* module from *required* to *requisite*.

## 2.6.4 Shadow Passwords

The pam_pwdb.so module will automatically detect that you are using shadow passwords and make all necessary adjustments. Please refer to Section 2.7, Shadow Utilities for more information.

## 2.6.5 Rexec and PAM

For security reasons, rexec is not enabled in Red Hat Linux 6.2. Should you wish to enable it, you will need to comment out one line in the file /etc/pam.d/rexec. Here is a sample of the file (note that your file may differ slightly):

```
#PAM-1.0
auth            required      /lib/security/pam_pwdb.so shadow nullok
auth            required      /lib/security/pam_nologin.so
account         required      /lib/security/pam_pwdb.so
```

To enable rexec, the line referring to the pam_nologin.so module must be commented out:

```
#PAM-1.0
auth            required      /lib/security/pam_pwdb.so shadow nullok
#auth            required      /lib/security/pam_nologin.so
account         required      /lib/security/pam_pwdb.so
```

After this file is modified, rexec will be enabled.

> **Please Note**
> 
> If your /etc/pam.d/rexec file contains a line referring to the pam_security.so module, you will not be able to rexec as root. To do so, you must also comment out the line referring to the pam_security.so module.

## More Information

This is just an introduction to PAM. More information is included in the /usr/doc/pam* directory, including a System Administrators' Guide, a Module Writers’ Manual, an Application Developers’ Manual, and the PAM standard, DCE-RFC 86.0.

# 2.7 Shadow Utilities

Shadow passwords are a method of improving system security by moving the encrypted passwords (normally found in /etc/passwd) to /etc/shadow which is readable only by root. During the installation of Red Hat Linux, you were given the option of setting up shadow password protection on your system.

The shadow-utils package contains a number of utilities that support:

- Conversion from normal to shadowed passwords and back (pwconv, pwconv)
- Verification of the password, group, and associated shadow files (pwck, grpck)
- Industry-standard methods of adding, deleting and modifying user accounts (useradd, usermod, and userdel)
- Industry-standard methods of adding, deleting, and modifying user groups (groupadd, groupmod, and groupdel)
- Industry-standard method of administering the /etc/group file (gpasswd)
