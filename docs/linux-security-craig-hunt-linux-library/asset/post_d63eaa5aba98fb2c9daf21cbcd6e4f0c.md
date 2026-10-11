
prompt the user for one. Note that if no password is available or the password is not appropriate, the user is denied access altogether.

- `md5`: Use the MD5 algorithm to encrypt the password.
- `bigcrypt`: Use Compaq's C2 extension to the conventional Linux `crypt` function to encrypt the password.

**Session** No arguments are required for the session management group.

In `/etc/pam.d/login`, you can use `pam_pwdb` to make sure that the incoming user's account and password is still active:

```
account       required      pam_pwdb.so
```

You can also use the `pam_pwdb` module in the authentication stage. The following example allows the use of a password from a previously stacked module:

```
auth          required      pam_pwdb.so try_first_pass
```

## The pam_rootok Module

The `pam_rootok` module allows the root user to gain access to a service without having to enter a password. The `pam_rootok` module authenticates the user if their user ID is set to 0 (the standard Linux user ID for root).

The `pam_rootok` module takes one command-line argument, `debug`, that makes the module write diagnostic information to `syslog`. The entries in the `/etc/pam.d/su` file have the following format:

```
auth          control_flag    module_path [debug]
```

The following lines in `/etc/pam.d/su` allow the root user to `su` to a regular user without having to issue a password while writing diagnostic information to the `syslog` utility via the `debug` argument:

```
auth          sufficient    pam_rootok.so  debug
auth          required      pam_unix.so
```

## The pam_securitty Module

The `pam_securitty` module checks to make sure that the root user is logging in from a secure terminal. If root is not logging in from a secure terminal, authentication for root fails unless `PAM_TTY` (the environment variable containing the terminal descriptor for the request) is set to a string listed in the `/etc/securitty` file. For all other users, it succeeds.

To force the root user to use a secure terminal, add the following directives to `/etc/pam.d/login` as the first line in the file:

```
auth required pam_secruity.so
```

## The pam_unix Module

The `pam_unix` module is the standard Unix authentication module. It uses standard calls from the system’s libraries to retrieve and set account information as well as to perform authentication. Usually this information is obtained from the `/etc/passwd` file, and from the `/etc/shadow` file as well if shadow is enabled.

The arguments available on the `pam_unix` module vary according to the management group in question.

### Account

The arguments for the account management group are as follows:

- `debug`: This option makes the module write diagnostic information to `syslog`.
- `audit`: This option forces additional (more pedantic) information to be written to `syslog`.

### Authentication

The arguments for the authentication management group are as follows:

- `debug`: This argument makes the `pam_unix` module write diagnostic information to `syslog`.
- `audit`: This argument forces additional (more pedantic) information to be written to `syslog`.
- `use_first_pass`: This argument forces the `pam_unix` module to attempt to use the previous stacked authentication module’s password and effectively never prompts the user for one. Note that if no password is available or the password is not appropriate, the user is denied access altogether.
- `try_first_pass`: This argument forces the `pam_unix` module to attempt the previous stacked authentication module’s password in case that satisfies this module as well.
- `nullok`: By default, the `pam_unix` module does not permit the user access to a service if their password is blank. The `nullok` argument overrides this default.
- `nodeley`: By default, the `pam_unix` module requests a delay-on-failure of the order of one second. The `nodeley` argument discourages the authentication component from requesting a delay should the authentication as a whole fail.

### Password

The arguments for the password management group are as follows:

- `debug`: This argument makes the `pam_unix` module write diagnostic information to `syslog`.
- `audit`: This argument forces additional (more pedantic) information to be written to `syslog`.
- `nullok`: By default, the `pam_unix` module does not permit the user access to a service if their password is blank. The `nullok` argument overrides this default.
- `not_set_pass`: This argument informs this module that it is not to pay attention to or make available the old or new passwords from/to other stacked password modules.
- `use_authtok`: This argument forces this module to set the new password to the one provided by the previously stacked password module.
- `try_first_pass`: This argument forces the `pam_unix` module to attempt the previous stacked authentication module's password in case that satisfies this module as well.
- `use_first_pass`: This argument forces the `pam_unix` module to attempt to use the previous stacked authentication module's password, and effectively never prompts the user for one. Note that if no password is available or the password is not appropriate, the user is denied access altogether.
- `md5`: This argument is used to force the module to perform password encryption with the MD5 algorithm instead of with the conventional Linux `crypt` function.
- `nodelay`: By default, the `pam_unix` module requests a delay-on-failure of the order of one second. The `nodelay` argument discourages the authentication component from requesting a delay should the authentication as a whole fail.
- `bigcrypt`: This argument forces the module to encrypt more than the first eight characters of a password with Compaq's `C2` extension to the standard Linux `crypt` function.
- `shadow`: This argument denotes that the encrypted passwords are kept in the `/etc/shadow` file.
- `nis`: This argument denotes that Sun's Network Information System (NIS) should be used for setting new passwords.
- `remember=N`: This argument takes one subargument, the number of previously used passwords to remember (save) for each user. Linux stores these passwords in `/etc/security/opasswd` to keep the user from using a recently selected password.

### Session

No arguments are required for the session management group.

The file `/etc/pam.d/system-auth` typically contain entries of the following type:

```
auth        sufficient        pam_unix.so md5 shadow
auth        required          pam_deny.so
account       sufficient        pam_unix.so
account       required          pam_deny.so
password      required          pam_cracklib.so retry=3
password      sufficient        pam_unix.so use_authtok md5 shadow
password      required          pam_deny.so
session       required          pam_unix.so
```

The entries in the preceding example illustrate the use of the `pam_unix` authentication module as a sufficient module, backed up by `pam_deny` as a required module, so that requests that cannot be properly authenticated are not granted.

Both the `auth` and `password` modules (the fifth and sixth lines in the preceding example) invoke `pam_unix` with the `md5` and `shadow` options. Note that in the `password` module (the sixth line), `pam_unix` features the `use_authtok` argument, which forces the module to set the new password to the one provided by the `pam_cracklib` module (stacked directly on top of `pam_unix`).

# Index

Note to the **Reader**: Throughout this index **boldfaced** page numbers indicate primary discussions of a topic. *Italicized* page numbers indicate illustrations.

- A
  - `-A` option
    - in ftpd, 403
    - in ipchains, 253
    - in iptables, 262
    - in kadm5.acl, 397
    - in klogind, 406
    - in kshd, 405
  - `-a` option
    - in ftpd, 403
    - in kadm5.acl, 397
    - in netstat, 121–122
    - in telnet, 404, 409
  - `%a` pattern, 115
  - `%A` pattern, 115
  - `a` property mask character, 85
  - accept action, 255
  - access.conf file, 188
  - access control
    - in Apache server, 198–202
    - as goal, 15–16
    - in Samba server, 229–234
  - access_log file, 204
  - access logs. See logs
  - access_times keyword, 102
  - account-flags field, 229
  - accounts. See user account security
  - ACK flag, 276
  - acl_file variable, 394
  - actions
    - in ipchains, 255
    - in opieaccess, 416
    - in swatchrc, 70
    - in syslog.conf, 67
  - add command, 194
  - add user script directive, 233
  - AddModule directive, 196
  - addrprn command, 398, 400–401
  - address spoofing, 21, 275
  - adduser command
    - in authsrv, 341
    - in dbmanage, 194
  - admin_keytab variable, 394, 399
  - admin_server variable, 392–393
  - Advanced Encryption Standard (AES), 14
  - ADVANCED_EXCLUDE_TCP variable, 150
  - ADVANCED_EXCLUDE_UDP variable, 150
  - ADVANCED_PORTS_TCP variable, 150–151
  - ADVANCED_PORTS_UDP variable, 150–151
  - Advanced Security Setting dialog box, 372, 372
  - Advanced Stealth Scan Detection Mode, 149
  - AES (Advanced Encryption Standard), 14
  - AHs (authentication headers), 351–352, 352
