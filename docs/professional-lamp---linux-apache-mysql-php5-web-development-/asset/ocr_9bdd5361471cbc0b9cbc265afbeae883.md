# Chapter 6

# AuthMySQLGroupTable

This is used to set the name of the table containing group information, when Apache is told to check groups instead of individual users (*require group* versus *require valid-user* ).

# AuthMySQLGroupCondition

Similar to *AuthMySQLUserCondition*, this directive allows you to specify conditional statements to include in the WHERE clause when matching user groups.

# AuthMySQLGroupField

This is the name of the field in the database that contains the group names. This field is used when matching groups using Apache's *require group* directive.

# AuthMySQLAuthoritative

This tells Apache whether or not to fallback to other modules if MySQL authentication fails.

# Apache and SSL

Protecting your web folders with Basic Authentication by using either *htpasswd* or *mod_auth_mysql* increases security. Unfortunately, that added layer of security afforded by Basic Authentication can be eliminated by a serious hacker looking to break into your system. The problem: when you use Basic Authentication on a standard server, the username and password are actually transmitted unencrypted from the client to the server. A network-savvy hacker could be monitoring the transmission between your machine and the server, and sniff out the plain-text passwords as they zing by.

The solution: encrypt the communication between the client and the server. In Apache, this can be achieved by using Secure Sockets Layer (SSL). SSL in Apache comes in the form of *mod_ssl*, an Apache module that SSL-enables a website that Apache controls, allowing any communication to and from Apache to be encrypted using a wide range of encryption schemes.

To enable SSL in Apache, first check to see if SSL is included in your existing Apache binary or as a loadable module:

```
```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```
```

If you don't see *mod_ssl.c* in the first command output or *mod_ssl.so* in the listing of the Apache modules, you'll need to build Apache SSL functionality yourself. To statically enable SSL, add *enable-ssl* to your Apache *configure* script when building from source:

```
```
./configure \
--enable-ssl \
# ...and any other configure settings you use
```
```