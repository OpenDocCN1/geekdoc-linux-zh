Stripped of most of its comment lines, the access-control directive has this format:

```
# First, we configure the "default" to be a
# very restrictive set of permissions.
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

# The following directory name should
# match DocumentRoot in httpd.conf
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride None
    order allow,deny
    allow from all
</Directory>

# The directory name should match the
# location of the cgi-bin directory
<Directory "/var/www/cgi-bin">
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
</Directory>
```

Access-control directives use a different syntax from the other Apache directives. The syntax is like that of HTML. Various access-control directives are enclosed within pairs of tags, such as <Directory> ... </Directory>.

The following list describes some of the access-control directives. In particular, notice the *AuthUserFile* directive; you can have password-based access control for specific directories.

+   * *Options* *opt1* *opt2* ....:Specifies the access-control options for the directory section in which this directive appears. The options can be one or more of the following:
+     * None disables all access-control features.
+     * All turns on all features for the directory.
+     * FollowSymLinks enables the server to follow symbolic links.
+     * SymlinksIfOwnerMatch follows symbolic links, only if the same user of the directory owns the linked directory.
+     * ExecCGI enables execution of CGI scripts in the directory.