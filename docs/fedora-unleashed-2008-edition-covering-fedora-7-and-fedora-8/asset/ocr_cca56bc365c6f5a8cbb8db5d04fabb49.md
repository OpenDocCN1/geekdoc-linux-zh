# Using .htaccess Configuration Files

Apache also supports special configuration files, known as .htaccess files. Almost any directive that appears in httpd.conf can appear in an .htaccess file. This file, specified in the AccessFileName directive in httpd.conf (or srv.conf prior to version 1.3.4) sets configurations on a per-directory (usually in a user directory) basis. As the system admin- istrator, you can specify both the name of this file and which of the server configurations can be overridden by the contents of this file. This is especially useful for sites in which there are multiple content providers and you want to control what these people can do with their spaces.

To limit which server configurations the .htaccess files can override, use the AllowOverride directive. AllowOverride can be set globally or per directory. For example, in your httpd.conf file, you could use the following:

```
"# Each directory to which Apache has access can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, it's best to configure the "default" to be a very restrictive set of
# permissions.

<Directory />
    Options FollowSymlinks
    AllowOverride None
</Directory>"
```

# Options Directives

To configure which configuration options are available to Apache by default, you must use the Options directive. Options can be None, All; or any combination of Indexes, Includes, FollowSymlinks, ExecCGI, and MultiViews. MultiViews isn't included in All and must be specified explicitly. These options are explained in Table 17.2.

TABLE 17.2 Switches Used by the Options Directive

| Switch | Description |
| :--- | :--- |
| None | None of the available options are enabled for this directory. |
| All | All the available options, except for MultiViews, are enabled for this directory. |
| Indexes | In the absence of an index.html file or another DirectoryIndex file, a listing of the files in the directory is generated as an HTML page for display to the user. |
| Includes | Server-side includes (SSIs) are permitted in this directory. This can also be written as IncludesNoExec if you want to allow includes but don't want to allow the exec option in them. For security reasons, this is usually a good idea in directories over which you don't have complete control, such as userDir directories. |