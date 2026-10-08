# passwd

character set of "digits" shown above. If m = M = 0 (derived from the string _or_..), the user is forced to change his password next time he logs in (and the "age" disappears from his entry in the password file).  If m > M (signified, for example, by the string _/_) , then only a superuser (not the user) can change the password. Not allowing the user to ever change the password is discouraged, especially on a trusted system.

Trusted systems support password aging and password generation. For more information on converting to trusted system and on password, see the HP-UX System Administration Tasks Manual and sam(lM).

getpwent(3C) designates values to the fields in the following structure declared in <pwd.h>:

```
struct passwd {
 char *pw_name;
 char *pw_passwd;
 uid_t pw_uid;
 gid_t pw_gid;
 char *pw_age;
 char *pw_comment;
 char *pw_gecos;
 char *pw_dir;
 char *pw_shell;
 aid_t pw_auid;
 int pw_audflg;
};
```

It is suggested that the range 0-99 not be used for user and group IDs (pw_uid and pw_gid in the above structure) so that IDs that might be assigned for system software do not conflict.

The user's full name, office location, extension, and home phone stored in the pw_gecos field of the passwd structure can be set by use of the chfn command (see chfn(l)) and is used by the finger(l) command. These two commands assume the information in this field is in the order listed above. A portion of the user's real name can be represented in the pw_gecos field by an & character, which some utilities (including finger) expand by substituting the login name for it and shifting the first letter of the login name to uppercase.

# SECURITY FEATURES

On trusted systems, the encrypted password for each user is stored in the file /tcb/files/auth/c/user_name (where c is the first letter in user name).  Password information files are not accessible to the public. The encrypted password can be longer than 13 characters for example, the password file for user david is stored in /tcb/files/auth/d/david. In addition to the password, the user profile in /tcb/files/auth/c/user_name also contains:

+   - numerical audit ID
- numerical audit flag

Like /etc/passwd, this file is an ASCII file. Fields within each user's entry are separated by colons. Refer to autchpac(4) and prwd(4) for details. The passwords contained in /tcb/files/auth/c/* take precedence over those contained in the encrypted password field of /etc/passwd. User authentication is done using the encrypted passwords in this file. The password aging mechanism described in passwd(l), under the section called SECURITY FEATURES, applies to this password.

# NETWORKING FEATURES

NFS