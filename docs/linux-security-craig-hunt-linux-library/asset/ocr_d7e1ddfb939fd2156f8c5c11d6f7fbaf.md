In addition, you can create a new group database, keyed by the username, where the value field is a comma-separated list of groups to which the user belongs, using the following command:

```
```bash
[ramon]$ sudo dbmmanage /etc/httpd/conf/group-list-DBM add alice
staff,operators,admin
User alice added with password encrypted to staff,operators,admin
using crypt

[ramon]$ sudo dbmmanage /etc/httpd/conf/group-list-DBM view alice
alice:staff,operators,admin
```
```

**mod_auth_db** Starting with Apache 1.1, the mod_auth_db module provides an alternative to mod_auth_dbm using the Berkeley Database (known as the Berkeley DB) format instead of the standard Linux DBM. The mod_auth_db directives, listed in Table 7.3, are similar to the ones for mod_auth_dbm.

### Table 7.3 *mod_auth_db* Directives

| Directive | Meaning |
| :--- | :--- |
| AuthName *auth-domain* | Specifies the authentication domain to send the HTTP client. |
| AuthType *type* | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| AuthDBGroupFile *filename* | Specifies the name of the DB file containing the group authentication information. |
| AuthDBUserFile *filename* | Specifies the name of the DB file containing the user authentication information. |
| AuthDBAuthoritative [ *on* | *off* ] | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

You use the *makedb* utility to create a Berkeley DB file for both your password and your group lists. Two items are needed for *makedb* in order to create the proper database format:

+   - Password: a username, a colon, and an encrypted password
+   - Group: a group name, a colon, and a comma-separated list of groups