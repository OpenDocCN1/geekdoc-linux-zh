The list with the `http_access` entries should only be entered, for the sake of readability, at the designated position in the `/etc/squid.conf` file. That is, between the text

```
# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS
```

and the last

```
http_access deny all
```

**redirect_program /usr/bin/squidGuard** With this option, a redirector, such as SquidGuard, which is able to block unwanted URLs, can be specified. Internet access can be individually controlled for various user groups with the help of proxy authentication and the appropriate ACLs. SquidGuard is a package in and of itself that can be separately installed and configured.

**authenticate_program /usr/bin/pam_auth** If users must be authenticated on the proxy, a corresponding program, such as pam_auth, can be specified here. When accessing pam_auth for the first time, the user will see a login window where the user name and password must be entered. In addition, an ACL is still required so only clients with a valid login can use the Internet:

```
acl password proxy_auth REQUIRED
```

```
http_access allow password
http_access deny all
```

The REQUIRED after proxy_auth can be replaced with a list of permitted user names or with the path to such a list.

**ident_lookup_access allow <acl_name>** With this, have an ident request run for all ACL-defined clients to find each user’s identity. If you apply all to the `<acl_name>`, this will be valid for all clients. Also, an ident daemon must be running on all clients. For Linux, install the identd package for this purpose. For Windows, there is free software available to download from the Internet. To ensure that only clients with a successful ident lookup are permitted, a corresponding ACL will also have to be defined here:

```
acl identhosts ident REQUIRED
```

```
http_access allow identhosts
http_access deny all
```