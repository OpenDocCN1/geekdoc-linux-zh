
module. There are four such keywords: required, requisite, sufficient, and optional.

The Linux-PAM library interprets these keywords in the following manner:

-   * required: This indicates that the success of the module is required for the module-type facility to succeed. Failure of this module will not be apparent to the user until all of the remaining modules (of the same module-type) have been executed.

-   * requisite: Like required, except that if such a module returns a failure, control is directly returned to the application. The return value is that associated with the first required or requisite module to fail. This flag can be used to protect against the possibility of a user getting the opportunity to enter a password over an unsafe medium. It is conceivable that such behavior might inform an attacker of valid accounts on a system. This possibility should be weighed against the not insignificant concerns of exposing a sensitive password in a hostile environment.

-   * sufficient: The success of this module is deemed sufficient to satisfy the Linux-PAM library that this module-type has succeeded in its purpose. In the event that no previous required module has failed, no more "stacked" modules of this type are invoked. (In this case, subsequent required modules are not invoked). A failure of this module is not deemed as fatal to satisfying the application that this module-type has succeeded.

-   * optional: As its name suggests, this control-flag marks the module as not being critical to the success or failure of the user's application for service. In general, Linux-PAM ignores such a module when determining if the module stack will succeed or fail. However, in the absence of any definite successes or failures of previous or subsequent stacked modules, this module will determine the nature of the response to the application. One example of this latter case is when the other modules return something like PAM_IGNORE.

The more elaborate (newer) syntax is much more specific and gives the administrator a great deal of control over how the user is authenticated. This form of the control-flag is delimited with square brackets and consists of a series of value=action tokens:

```
[value1=action1 value2=action2 ...]
```

Here, value1 is one of the following return values:

```
success; open_err; symbol_err; service_err; system_err; buf_err; perm_denied; auth_err; cred_insufficient; authinfo_unavail; user_unknown; maxtries; new_authtok_req; acct_expired; session_err; cred_unavail; acct_expired; cred_err; no_module_data; conv_err; authtok_err; authtok_recover_err; authtok_lock_busy; authtok_disable_aging; try_again; ignore; abort; authtok_expired;
module_unknown; bad_item; and default.
```

The last of these (default) can be used to set the action for those return values that are not explicitly defined.

The action can be a positive integer or one of the following tokens: ignore; ok; done; bad; die; and reset. A positive integer, J, when specified as the action, can be used to indicate that the next J modules of the current module-type will be skipped. In this way, the administrator can develop a moderately sophisticated stack of modules with a number of different paths of execution. Which path is taken can be determined by the reactions of individual modules.

-   - ignore: When used with a stack of modules, the module's return status will not contribute to the return code the application obtains.

-   - bad: This action indicates that the return code should be thought of as indicative of the module failing. If this module is the first in the stack to fail, its status value will be used for that of the whole stack.

-   - die: Equivalent to bad with the side effect of terminating the module stack and PAM immediately returning to the application.

-   - ok: This tells PAM that the administrator thinks this return code should contribute directly to the return code of the full stack of modules. In other words, if the former state of the stack would lead to a return of PAM.SUCCESS, the module's return code will override this value. Note, if the former state of the stack holds some value that is indicative of a module's failure, this ok value will not be used to override that value.

-   - done: Equivalent to ok with the side effect of terminating the module stack and PAM immediately returning to the application.

-   - reset: Clears all memory of the state of the module stack and starts again with the next stacked module.

Each of the four keywords, required, requisite, sufficient; and optional, have an equivalent expression in terms of the [...] syntax. They are as follows:

-   - required is equivalent to [success=ok new.authtok.reqd=ok ignore=ignore default=bad].

-   - requisite is equivalent to [success=ok new.authtok.reqd=ok ignore=ignore default=die].

-   - sufficient is equivalent to [success=done new.authtok.reqd=done default=ignore].

-   - optional is equivalent to [success=ok new.authtok.reqd=ok default=ignore].

Just to get a feel for the power of this new syntax, here is a taste of what you can do with it. With Linux-PAM-0.63, the notion of client plug-in agents was introduced. This makes it possible for PAM to support machine-machine authentication using the transport protocol inherent to the client/server application. With the [...] syntax, the administrator can specify which protocol is used for each connection.

value=action ... J control syntax, it is possible for an application to be configured to support binary prompts with compliant clients, but to gracefully fail over into an alternative authentication mode for legacy applications.

**module-path** The pathname of the dynamically loadable object file; the pluggable module itself. If the first character of the module path is \"/\", it is assumed to be a complete path. If this is not the case, the given module path is appended to the default module path: /lib/security (but see the previous notes).

The arguments are a list of tokens that are passed to the module when it is invoked, much like arguments to a typical Linux shell command. Generally, valid arguments are optional and are specific to any given module. Invalid arguments are ignored by a module; however, when encountering an invalid argument, the module is required to write an error to syslog(3). For a list of generic options, see the next section.

If you wish to include spaces in an argument, you should surround that argument with square brackets. For example:

```
squid auth required pam_mysq1.so user=passwd_query passwd=mada \
 db=emlence fquery=select user_name from internet_service where \
 user_name=%u and password=PASSWORD(%p) and service=web_proxy]
```

When using this convention, you can include \"[\" characters inside the string, and if you wish to have a \"[\" character inside the string that will survive the argument parsing, you should use \"\\[\". In other words,

```
[\.\.\..] --> .\.\.\..
```

Any line in one of the configuration files that is not formatted correctly will generally tend (erring on the side of caution) to make the authentication process fail. A corresponding error is written to the system log files with a call to syslog(3).

## 27.2.2 Example System Configurations

The following is an example /etc/pam.d/login configuration file. This example had all options uncommented and is probably not usable because it stacks many conditions before allowing successful completion of the login process. Essentially, all conditions can be disabled by commenting them out, except the calls to pam_pwdb.so.

### 27.2.2.1 PAM: Original Login Config

```
#%PAM-1.0
#
The PAM configuration file for the login service
#
auth required pam_security7.so
auth required pam_nologin.so
# auth required pam_dialup.so
# auth optional pam_mail.so
auth required pam_pwdb.so shadow md5
# account requisite pam_time.so
account required pam_pwdb.so
session required pam_pwdb.so
# session optional pam_lastlog.so
# password required pam_cracklib.so retry=3
password required pam_pwdb.so shadow md5
```

### 27.2.2.2 PAM: Login Using pam_smbpass

PAM allows use of replaceable modules. Those available on a sample system include:

$ /bin/ls /lib/security

| Column 1 | Column 2 | Column 3 |
| :--- | :--- | :--- |
| pam_access.so | pam_ftp.so | pam_limits.so |
| pam_ncp_auth.so | pam_rhosts.auth.so | pam_sieve.so |
| pam_cracklib.so | pam_group.so | pam_listfile.so |
| pam_nologin.so | pam_rootok.so | pam_tally.so |
| pam_deny.so | pam_issuu.so | pam_mail.so |
| pam_permit.so | pam_security7.so | pam_time.so |
| pam_dialup.so | pam_lastlog.so | pam_mkhome/dir.so |
| pam_pwdb.so | pam_shells.so | pam_unix.so |
| pam_env.so | pam_ldap.so | pam_motd.so |
| pam_radius.so | pam_smbpass.so | pam_unix.acct.so |
| pam_wheel.so | pam_unix.auth.so | pam_unix_passwd.so |
| pam_userdb.so | pam_warn.so | pam_unix_session.so |

The following example for the login program replaces the use of the pam_pwdb.so module that uses the system password database (/etc/passwd, /etc/shadow, /etc/group) with the module pam_smbpass.so, which uses the Samba database containing the Microsoft MD4 encrypted password hashes. This database is stored either in /usr/local/samba/private/smbpasswd, /etc/samba/smbpasswd or in /etc/samba.d/smbpasswd, depending on the Samba implementation for your UNIX/Linux system. The pam_smbpass.so module is provided by Samba version 2.2.1 or later. It can be compiled by specifying the --with-pam_smbpass options when running Samba's configure script. For more information on
