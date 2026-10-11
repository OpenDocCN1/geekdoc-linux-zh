```
$ cat /etc/pam.d/login
#%PAM-1.0
auth [user_unknown=ignore success=ok ignore=ignore default=bad] pam_securityty.so
auth include system-auth
account required pam_nologin.so
account include system-auth
password include system-authFipFip99

# pam_selinux.so close should be the first session rule
session required pam_selinux.so close
session optional pam_keyinit.so force revoke
session include system-auth
session required pam_loginuid.so
session optional pam_console.so
# pam_selinux.so open should only be followed by sessions to be executed in the user context
session required pam_selinux.so open
session optional pam_ck_connector.so
```

The first line is a special comment; it will become significant only if another PAM format is released. Do not use \`#%\` other than in the first line of the preceding example.

The rest of the lines tell PAM to do something as part of the authentication process. Lines that begin with \`#\` are comments. The first word on each line is a module type indicator: **account**, **auth**, **password**, or **session** (Table 11-5). The second is a control flag (Table 11-6), which indicates the action PAM should take if authentication fails. The rest of the line contains the name of a PAM module (located in */lib/security*) and any arguments for that module. The PAM library itself uses the */etc/pam.d* files to determine which modules to delegate work to.

# Table 11-5 Module type indicators

| Module type | Description | Controls |
| :--- | :--- | :--- |
| account | Account management | Determining whether an already authenticated user is allowed to use the service she is trying to use, (that is, has the account expired? Is the user allowed to use this service at this time of day?) |
| auth | Authentication | Proving that the user is authorized to use the service. This task may be done using passwords or another mechanism. |
| password | Password modification | Updating authentication mechanisms such as user passwords. |
| session | Session management | Setting things up when the service is started (as when the user logs in) and breaking them down when the service is terminated (as when the user logs out). |