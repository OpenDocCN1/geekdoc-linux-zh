124

Chapter 10. Apache HTTP Server

| Action | dbmmanage command (1.3) | Equivalent httpdb command (2.0) |
|---|---|--|
| Add user to database (using given password) | dbmmanage authdb username password | httpdb -b -TDB authdb username |
| Add user to database (prompts for password) | dbmmanage authdb addduser username | httpdb -TDB authdb username |
| Remove user from database | dbmmanage authdb delete username | httpdb -x -TDB authdb username |
| List users in database | dbmmanage authdb view | httpdb -l -TDB authdb |
| Verify a password | dbmmanage authdb check username | httpdb -v -TDB authdb username |

Table 10-1. Migrating from dbmmanage to httpdb

The -m and -s options work with both dbmmanage and httpdb, enabling the use of the MD5 and SHA1 algorithms for hashing passwords, respectively.

When creating a new database with httpdb, the -c option must be used.
For this topic, refer to the following documentation on the Apache Software Foundation's website:

+   - http://httpd.apache.org/docs-2.0/mod/mod_auth_dbm.html

# 10.2.4.5. The mod_perl Module

The configuration for mod_perl has been moved from httpd.conf into the file /etc/httpd/conf.d/mod_perl.conf. For this file to be loaded, and hence mod_perl to work, the statement Include conf.d/* must be included in the httpd.conf as described in Section 10.2.1.3 Dynamic Shared Object (DSO) Support.
Occurrences of Apache: in the httpd.conf must be replaced with ModPerl:: Additionally, the manner in which handlers are registered has been changed.
This is a sample Apache HTTP Server 1.3 mod_perl configuration:

```
<Directory /var/www/perl>
  SetHandler perl-script
  PerlHandler Apache::Registry
  Options +ExecCGI
</Directory>
```

This is the equivalent mod_perl for Apache HTTP Server 2.0:

```
<Directory /var/www/perl>
  SetHandler perl-script
  PerlModule ModPerl::Registry
  PerlHandler ModPerl::Registry::handler
  Options +ExecCGI
</Directory>
```

Most modules for mod_perl 1.x should work without modification with mod_perl 2.x. XS modules require recompilation and possibly require minor Makefile modifications.