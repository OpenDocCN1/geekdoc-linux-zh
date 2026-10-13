# FIGURE 10-11

The PAM
/etc/pam.d/login
configuration file

```
#PAM-1.0
auth [user_unknown=ignore success=ok ignore=ignore default=bad] pam_securetty.so
auth include system-auth
account required pam_nologin.so
account include system-auth
password include system-auth
# pam_selinux.so close should be the first session rule
session required pam_selinux.so close
session required pam_loginuid.so
session optional pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed in the
user context
session required pam_selinux.so open
session required pam_namespace.so
session optional pam_keyinit.so force revoke
session include system-auth
-session optional pam_ck_connector.so
~
~
"/etc/pam.d/login" 16L, 728C
```

The module_type, as described previously, can be auth, account, password, or session. The control_flag determines what PAM does if the module succeeds or fails. The module_path specifies the location of the actual PAM module file. Finally, as with regular shell commands, you can specify arguments for each module.

The control_flag field requires additional explanation. It determines how the configuration file reacts when a module flags success or failure. The five different control flags are described in Table 10-5.

# TABLE 10-5

PAM Control Flags

| control_flag | Description |
|---|---|
| required | If the module works, the command proceeds. If it fails, PAM proceeds to the next command in the configuration file—but the command controlled by PAM will still fail. |
| requisite | Stops the process if the module fails. |
| sufficient | If the module works, the login or other authentication proceeds. No other commands need be processed. |
| optional | PAM ignores success or failure of this module, unless no other modules are used. |
| include | Includes all module_type directives from the noted configuration file; for example, if the directive is password include system-auth, this includes all password directives from the PAM system-auth file. |