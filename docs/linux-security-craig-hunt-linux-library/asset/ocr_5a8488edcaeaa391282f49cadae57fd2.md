**mod_auth_dbm**  The `mod_auth_dbm` module provides simple username/password authentication using Linux DBM format for the user database. User lookups are much faster than those of `mod_auth` are, and the `mod_auth_dbm` module can support a very large user population (typically thousands of users). As with `mod_auth`, the use of `mod_auth_dbm` is controlled by directives that can be included in the `.htaccess` directory within the Apache content tree. Table 7.2 lists the directives available for the `mod_auth_dbm` module.

| Directive | Meaning |
|---|---|
| `AuthName auth-domain` | Specifies the authentication domain to send the HTTP client. |
| `AuthType type` | Specifies the type of password transmission: Basic (in the clear) or Digest (MD5). |
| `AuthDBMGroupFile filename` | Specifies the name of the DBM file containing the group authentication information. |
| `AuthDBMUserFile filename` | Specifies the name of the DBM file containing the user authentication information. |
| `AuthDBMAuthoritative [ on | off ]` | Avoid falling back to a lower form of authentication if user is not available. Defaults to on. |

As an example, consider the entry in Listing 7.5 from the `/var/www/html/.htaccess` file.

```
```text
AuthName 'Private Information'
AuthType Basic
AuthDBMUserFile /etc/httpd/conf/user-list-DBM
AuthDBMGroupFile /etc/httpd/conf/group-list-DBM
AuthDBMAuthoritative on
Require valid-user
```
```

The example in Listing 7.5 is similar to the example in Listing 7.4, except for the third and fourth lines. In Listing 7.5, the `AuthDBMUserFile` and `AuthDBMGroupFile` directives specify that the authentication lookup take place on DBM-format files called `/etc/httpd/conf/user-list-DBM` and `/etc/httpd/conf/group-list-DBM` instead of on the flat files used in the example in Listing 7.4.