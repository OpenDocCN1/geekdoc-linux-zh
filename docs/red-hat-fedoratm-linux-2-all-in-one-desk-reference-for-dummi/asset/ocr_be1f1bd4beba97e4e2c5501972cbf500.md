+   * `Includes` enables server-side include files in this directory (the term *server-side include* refers to directives, placed in an HTML file, that the Web server processes before returning the results to the Web browser).
+   * `Indexes` enables clients to request indexes (directory listings) for the directory.
+   * `IncludesNOEXEC` disables the `fexec` command in server-side includes.

+   ❖ `AllowOverride directive1 directive2 ...` : Specifies which access-control directives can be overridden on a per-directory basis. The directive list can contain one or more of the following:
+   * `None` stops any directive from being overridden.
+   * `All` enables overriding of any directive on a per-directory basis.
+   * `Options` enables the use of the `Options` directive in the directory-level file.
+   * `FileInfo` enables the use of directives controlling document type, such as `AddType` and `AddEncoding`.
+   * `AuthConfig` enables the use of authorization directives, such as `AuthName`, `AuthType`, `AuthUserFile`, and `AuthGroupFile`.
+   * `Limit` enables the use of `Limit` directives (`allow`, `deny`, and `order`) in a directory's access-configuration file.

+   ❖ `AuthName name`: Specifies the authorization name for a directory.

+   ❖ `AuthType type`: Specifies the type of authorization to be used. The only supported authorization type is `Basic`.

+   ❖ `AuthUserFile filename`: Specifies the file in which usernames and passwords are stored for authorization. For example, the following directive sets the authorization file to `/etc/htpd/conf/passwd`:
+   `AuthUserFile /etc/htpd/conf/passwd`

You have to create the authorization file with the `/usr/bin/httpasswd support` program. To create the authorization file and add the password for a user named `jdoe`, specify the following:

```
`/usr/bin/httpasswd -C /etc/htpd/conf/passwd jdoe`
```

When prompted for the *password*, enter the password and then confirm it by typing it again.

+   ❖ `AuthGroupFile filename`: Specifies the file to consult for a list of user groups for authentication.

+   ❖ `order ord`: Specifies the order in which two other directives — `allow` and `deny` — are evaluated. The order is one of the following:
+   * `deny, allow` causes the Web server to evaluate the `deny` directive before `allow`.