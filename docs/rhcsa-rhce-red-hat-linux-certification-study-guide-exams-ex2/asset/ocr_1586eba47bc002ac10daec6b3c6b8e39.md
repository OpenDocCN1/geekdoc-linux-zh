# The Anatomy of /etc/gshadow

| Field | Example | Purpose |
|---|---|---|
| Groupname | mj | Each user gets his own group, with the same name as his username. Specific users may be assigned as administrators for unique groups. |
| Password | ! | Most groups have a '!', which indicates no password; some groups may have a hashed password similar to that shown in the /etc/shadow file. |
| Group ID | 500 | The numeric group ID (GID) associated with that user. By default, RHEL creates a new group for every new user. If you want to create a special group such as managers, you should assign a GID number outside the standard range; otherwise, Red Hat GIDs and UIDs would probably get out of sequence. |
| Group members | mj,vp | A comma-delimited list of usernames that are members of the group. If it's blank, and there is a username that is identical to the group name, that user is the only member of that group. |

# The /etc/login.defs File

The /etc/login.defs file provides the baseline for a number of parameters in the shadow password suite. This section provides a brief analysis of each active directive in the default version of this file. As you'll see, the directives go somewhat beyond authentication. The first directive specifies the directory with locally delivered e-mail, listed by username:

```
MAIL_DIR /var/spool/mail
```

The next four directives relate to default password aging information. The directives are explained in the file comments, and in Table 8-5.

# /etc/login.defs Password Aging Directives

| Directive | Purpose |
|---|---|
| PASS_MAX_DAYS | After this number of days, the password must be changed. |
| PASS_MIN_DAYS | Passwords must be kept for at least this number of days. |
| PASS_MIN_LEN | A warning is given when a user tries to use a password shorter than this length. |
| PASS_WARN_AGE | Users are warned this number of days before PASS_MAX_DAYS. |