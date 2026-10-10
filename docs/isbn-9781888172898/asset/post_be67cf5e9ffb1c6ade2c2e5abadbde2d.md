
### 10.4 User Authentication with PAM

Programs which give users access to privileges of any sort need to be able to authenticate the users. When you log into a system, you provide your name and password, and the login process uses those to authenticate the login—to verify that you are who you say you are. Other forms of authentication than passwords are possible, and it is possible for the passwords to be stored in different ways.

PAM, which stands for “Pluggable Authentication Modules”, is a way of allowing the system administrator to set authentication policy without having to recompile programs which do authentication. With PAM, you control how the modules are plugged into the programs by editing a configuration file.

Most Red Hat Linux users will never need to touch this configuration file. When you use RPM to install programs that need to do authentication, they automatically make the changes that are needed to do normal password authentication. However, you may want to customize your configuration, in which case you need to understand the configuration file.

#### 10.4.1 Modules

There are four types of modules defined by the PAM standard. auth modules provide the actual authentication, perhaps asking for and checking a password, and set “credentials” such as group membership or kerberos “tickets”. account modules check to make sure that the authentication is allowed (the account has not expired, the user is allowed to log in at this time of day, etc.). password modules are used to set passwords. session modules are used once a user has been authenticated to make it possible for them to use their account, perhaps mounting the user’s home directory or making their mailbox available.

These modules may be *stacked*, so that multiple modules are used. For instance, login normally makes use of at least two authentication methods: if “rhopts” authentication succeeds, it is sufficient to allow the connection; if it fails, then standard password authentication is done.

New modules can be added at any time, and PAM-aware applications can then be made to use them. For instance, if you have a one-time-password calculator system, and you can write a module to support it (documentation on writing modules is included with the system). PAM-aware programs can use the new module and work with the new one-time-password calculators without being recompiled or otherwise modified in any way.

#### 10.4.2 Services

Each program which uses PAM defines its own “service” name. The login program defines the service type `login`, ftpd defines the service type `ftp`, etc. In general, the service type is the name of the program used to **provide** the service, not (if there is a difference) the program used to **access** the service.

#### 10.4.3 The Configuration Files

The directory `/etc/pam.d` is used to configure all PAM applications. (This used to be `/etc/pam.conf` in earlier PAM versions; while the pam.conf file is still read if no /etc/pam.d/ entry is found, its use is deprecated.) Each application (really, each **service**) has its own file. A file looks like this:

```
#%PAM-1.0

auth required /lib/security/pam_securtty.so
auth required /lib/security/pam_pwd.b.so shadow nullok
auth required /lib/security/pam_nologin.so
account required /lib/security/pam_pwd.b.so
password required /lib/security/pam_cracklib.so
password required /lib/security/pam_pwb.b.so shadow nullok use_authok
session required /lib/security/pam_pwd.b.so
```

The first line is a comment. Any line that starts with a `#` character is a comment. The next three lines stack up three modules to use for login authorization. The first line makes sure that if the user is trying to log in as root, the tty on which they are logging in is listed in the `/etc/securtty` file *if* that file exists. The second line causes the user to be asked for a password and the password checked. The third line checks to see if the file `/etc/nologin` exists, and if it does, displays the contents of the file, and if the user is not root, does not let him or her log in.

Note that all three modules are checked, even if the first module fails. This is a security decision—it is designed to not let the user know why their authentication failed.

The fourth line makes sure that the account is valid.

The fifth line causes any necessary accounting to be done. For example, if shadow passwords have been enabled, the pam_pwd.so module will check to see if the account has expired, or if the user has not changed his or her password and the grace period for changing the password has expired.

The sixth line specifies that if the login program changes the user's password, it should use the pam_pwd.so module to do so. (It will do so only if an auth module has determined that the password needs to be changed—for example, if a shadow password has expired.)

The final line specifies that the pam_pwd.so module should be used to manage the session. Currently, that module doesn't do anything; it could be replaced (or supplemented by stacking) by any necessary module.

Note that the order of the lines within each file matters. While it doesn't really matter much in which order required modules are called, there are other control flags available. While optional is rarely used, and never used by default on a Red Hat Linux system, sufficient and requisite cause order to become important.

Let's look at the auth configuration for rlogin:

```
auth    required    /lib/security/pam_security.so
auth    sufficient  /lib/security/pam_rhosts_auth.so
auth    required    /lib/security/pam_pwd.so shadow nullok
auth    required    /lib/security/pam_nologin.so
```

That looks almost like the login entry, but there's an extra line specifying an extra module, and the modules are specified in a different order.

First, pam_security.so keeps root logins from happening on insecure terminals. This effectively disallows all root login attempts. If you wish to allow them (in which case we recommend that you either not be internet-connected or be behind a good firewall), you can simply remove that line.

Second, pam_nologin.so checks /etc/nologin, as specified above.

Third, if `pam_rhosts_auth.so` authenticates the user, PAM immediately returns success to `rlogin` without any password checking being done. If `pam_rhosts_auth.so` fails to authenticate the user, that failed authentication is ignored.

Finally (if `pam_rhosts_auth.so` has failed to authenticate the user), the `pam_pwdb.so` module performs normal password authentication.

Note that if you do not want to prompt for a password if the `security` check fails, you can change the `pam_security.so` module from `required` to `requisite`

#### 10.4.4 Shadow Passwords

The default `pam_pwdb.so` module can support shadow passwords. In order to convert your system to shadow passwords, use these commands:

```
cd /etc
pwconv
chmod 600 passwd- shadow-
```

The `pam_pwdb.so` module will automatically detect that you are using shadow passwords and make all necessary adjustments.

#### 10.4.5 More Information

This is just an introduction to PAM. More information is included with the system in `/usr/doc/pam*`, including a *System Administrators' Guide*, a *Module Writers' Manual*, an *Application Developers' Manual*, and the PAM standard, DCE-RFC §6.0. In addition, documentation is available from the Red Hat web site, at `http://www.redhat.com/linux-info/pam/`.

## 10.5 The Boot Process, Init, and Shutdown

### 10.5.1 System V Init

This section is a brief description of the internals of the boot process. It basically covers in detail how the machine boots using SysV Init and the differences between the original init used in older Linux releases.

Init is the program that gets run by the kernel at boot time. It is in charge of starting all the normal processes that need to run at boot time. These include the gettys that allow you to log in, NFS daemons, FTP daemons, and anything else you want to run when your machine boots.

SysV Init is fast becoming the standard in the Linux world to control the startup of software at boot time. This is because it is easier to use and more powerful and flexible than the traditional BSD init.

SysV init also differs from BSD init in that the config files are in a subdirectory of /etc instead of residing directly in /etc. This directory is called **rc.d**. In there you will find **rc.sysinit** and the following directories:

- init.d
- rc0.d
- rc1.d
- rc2.d
- rc3.d
- rc4.d
- rc5.d
- rc6.d

**init.d** contains a bunch of scripts. Basically, you need one script for each service you may need to start at boot time or when entering another runlevel. Services include things like networking, nfs, sendmail, httpd, etc. Services do not include things like setserial that must only be run once and then exited. Things like that should go in **rc.local** or **rc.serial**.

If you want **rc.local**, it should be in /etc/rc.d. Most systems include one even though it doesn’t do much. You can also include an rc.serial in /etc/rc.d if you need to do serial port specific things at boot time.

The chain of events is as follows:
