```
# symbolic links and aliases may be used to point to other locations.
DocumentRoot "/var/www/html"
```

# Setting access options and overrides

You can set individual access permissions for each directory in the Web server's directory structure. The default is fairly restrictive. Here is the default:

```
<Directory />
    Options FollowSymLinks
        AllowOverride None
</Directory>
```

This segment sets up a default block of permissions for the Options and AllowOverride directives. The `<Directory />...< /Directory>` tags enclose the directives that are to be applied to the / directory (which is /var/www/html by default).

The Options FollowSymLinks directive instructs the server that symbolic links within the directory can be followed to allow content that resides in other locations on the computer. None of the other special server features will be active in the / directory, or in any directory below that, without being explicitly specified later. Next, the following access options are specifically set for the root of your Web server (/var/www/html). (I removed the comments here for clarity.)

```
<Directory "/var/www/html">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

If you have changed the value of DocumentRoot earlier in this file, you need to change the /var/www/html to match that value. The Options set for the directory are Indexes and FollowSysLinks. Those and other special server features are described in Table 21-2. The AllowOverride None directive instructs the server that the .htaccess file (or the value of AccessFileName) cannot override any of the special access features. You can replace None with any of the special access features described in Table 21-3.

> NOTE: Remember that unless you specifically enable a feature described in Tables 21-2 and 21-3, that feature is not enabled for your server (with the exceptions of Indexes and FollowSymLinks).

# Table 21-2: Special Server Features for the Options Directive

| Feature | Description |
| :--- | :--- |
| ExecCGI | The execution of CGI scripts is permitted. |
| FollowSymLinks | The server will traverse symbolic links. |