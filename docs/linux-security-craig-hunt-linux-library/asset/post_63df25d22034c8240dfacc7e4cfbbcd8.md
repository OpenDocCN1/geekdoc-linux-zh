
## Listing 7.3 Sample Apache password file

```
[ramon]$ more /etc/httpd/conf/user-list
alice:9ti4wVG8J3Yug
bob:vsh73lcf4ph2
charlie:WqBo5s8Vas8XJg
```

Earlier in this section, you learned about the .htaccess file and the directives that you can add to make use of mod_auth module authentication. Table 7.1 includes the complete list of available directives, including their syntax and their meaning.

### Table 7.1 mod_auth Directives

| Directive | Meaning |
|---|---|
| AuthName auth-domain | Specifies the authentication domain to send the HTTP client. |
| AuthType type | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| AuthGroupFile filename | Specifies the name of the file containing the group authentication information. |
| AuthUserFile filename | Specifies the name of the file containing the user authentication information. |
| AuthAuthoritative [ on \| off ] | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

For example, consider the entry in Listing 7.4 from the /var/www/html/.htaccess file.

### Listing 7.4 Using the mod_auth directives

```
AuthName 'Private Information'
AuthType Basic
AuthUserFile /etc/httpd/conf/user-list
AuthGroupFile /etc/httpd/conf/group-list
AuthAuthoritative on
Require valid-user
```

The directives in Listing 7.4 have the following meanings:

- `AuthName 'Private Information'` specifies a domain, a concept used by the Apache authentication modules to refer to the resource (directory) in question. A domain translates to the directory structure below the one in question. Once the browser has successfully authenticated, it can access any resources within the realm.
- `AuthType Basic` defines standard, in-the-clear transmission of the password.
- The `AuthUserFile` directive defines the path to the password file as `/etc/httpd/conf/user-list`.
- The `AuthGroupFile` directive defines the path to the group file `/etc/httpd/conf/group-list`.
- The `AuthAuthoritative` directive ensures that access is simply denied if the user does not exist. (Apache has the ability to cascade this password to other authentication methods if the first request fails).
- The `Require valid-user` directive instructs Apache to only grant access to a user that is present in the `AuthUserFile`. Alternatively, you could have specified the following:
  ```
  Require user alice
  Require user bob
  ```
  These two directives limit access to just the two users alice and bob. Username charlie, who also happens to be present in the `AuthUserFile`, is denied access. This is useful for restricting certain subdirectories within the Apache content tree to specific users, while relying on one central `AuthUserFile`. Furthermore, you can limit access to users within a certain group, using the following directive:
  ```
  Require group administrators
  ```
  This directive restricts access to those users who successfully authenticate as an authorized user in the password file and are also members of the administrators group.

> **WARNING** While it is possible to use the standard Linux /etc/passwd to perform Apache server authentication, I strongly recommend against this practice. If the username/password pair exchanged for Apache authentication is captured (it typically travels in the clear), the intruder could then penetrate the user's shell account as well. In addition, Apache imposes no limit on unsuccessful logins, so an attacker could use a brute-force approach to guess system passwords by attempting repeated HTTP requests.

## mod_auth_dbm

The `mod_auth_dbm` module provides simple username/password authentication using Linux DBM format for the user database. User lookups are much faster than those of `mod_auth` are, and the `mod_auth_dbm` module can support a very large user population (typically thousands of users). As with `mod_auth`, the use of `mod_auth_dbm` is controlled by directives that can be included in the `.htaccess` directory within the Apache content tree. Table 7.2 lists the directives available for the `mod_auth_dbm` module.

### Table 7.2 mod_auth_dbm Directives

| Directive | Meaning |
|---|---|
| `AuthName auth-domain` | Specifies the authentication domain to send the HTTP client. |
| `AuthType type` | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| `AuthDBMGroupFile filename` | Specifies the name of the DBM file containing the group authentication information. |
| `AuthDBMUserFile filename` | Specifies the name of the DBM file containing the user authentication information. |
| `AuthDBMAuthoritative [ on \| off ]` | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

As an example, consider the entry in Listing 7.5 from the `/var/www/html/.htaccess` file.

### Listing 7.5

```text
AuthName 'Private Information'
AuthType Basic
AuthDBMUserFile /etc/httpd/conf/user-list-DBM
AuthDBMGroupFile /etc/httpd/conf/group-list-DBM
AuthDBMAuthoritative on
Require valid-user
```

The example in Listing 7.5 is similar to the example in Listing 7.4, except for the third and fourth lines. In Listing 7.5, the `AuthDBMUserFile` and `AuthDBMGroupFile` directives specify that the authentication lookup take place on DBM-format files called `/etc/httpd/conf/user-list-DBM` and `/etc/httpd/conf/group-list-DBM` instead of on the flat files used in the example in Listing 7.4.

Apache includes a Perl utility called `dbmmanage` (usually installed in `/usr/sbin`) that you can use to create the DBM database initially and to populate the database with new users and groups. The command-line usage of `dbmmanage` is as follows:

```
dbmmanage filename [ command [ username [pw [group1[,group2] [encpasswd ] ]
```

In the `dbmmanage` command line, `command` can be one of the following:

- `add`: This command adds an entry for `username` to `filename` using the encrypted password `encpasswd` or the group(s) in the list of `group1 [,group2]`.
- `adduser`: This command prompts for a password and adds an entry for `username` to `filename`.
- `check`: This command prompts for a password and then checks if `username` is in `filename` and if its password matches the one specified.
- `delete`: This command deletes the `username` entry from `filename`.
- `import`: This command reads the `username:password` entries (one per line) from the standard Linux input and appends them to `filename`. The password must already be encrypted.
- `update`: This command is equivalent to the `adduser` command, except that it ensures that `username` already exists in `filename`.
- `view`: This command displays the complete contents of the DBM database file.

For example, to create the DBM user database file `/etc/httpd/conf/user-list-DBM` and add a new user named `alice`, enter the following command:

```
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM adduser alice
New password:
Re-type new password:
User alice added with password encrypted to vqQ/X7Z7hYLXQ using crypt
```

To view your newly created entry, enter the following command:

```
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM view
alice:vqQ/X7Z7hYLXQ
```

To delete the database entry for `alice`, enter the following command:

```
[ramon]$ sudo dbmmanage /etc/httpd/conf/user-list-DBM delete alice
alice deleted
```

In addition, you can create a new group database, keyed by the username, where the value field is a comma-separated list of groups to which the user belongs, using the following command:

```bash
[ramon]$ sudo dbmmanage /etc/httpd/conf/group-list-DBM add alice
staff,operators,admin
User alice added with password encrypted to staff,operators,admin
using crypt

[ramon]$ sudo dbmmanage /etc/httpd/conf/group-list-DBM view alice
alice:staff,operators,admin
```

## mod_auth_db

Starting with Apache 1.1, the `mod_auth_db` module provides an alternative to `mod_auth_dbm` using the Berkeley Database (known as the Berkeley DB) format instead of the standard Linux DBM. The `mod_auth_db` directives, listed in Table 7.3, are similar to the ones for `mod_auth_dbm`.

### Table 7.3 mod_auth_db Directives

| Directive | Meaning |
| :--- | :--- |
| `AuthName auth-domain` | Specifies the authentication domain to send the HTTP client. |
| `AuthType type` | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| `AuthDBGroupFile filename` | Specifies the name of the DB file containing the group authentication information. |
| `AuthDBUserFile filename` | Specifies the name of the DB file containing the user authentication information. |
| `AuthDBAuthoritative [ on \| off ]` | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

You use the `makedb` utility to create a Berkeley DB file for both your password and your group lists. Two items are needed for `makedb` in order to create the proper database format:

- `Password`: a username, a colon, and an encrypted password
- `Group`: a group name, a colon, and a comma-separated list of groups
