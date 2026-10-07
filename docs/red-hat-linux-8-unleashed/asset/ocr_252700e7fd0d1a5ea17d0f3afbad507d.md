# CHAPTER 16 Apache Web Server Management

To limit server configurations the .htaccess files override, use the AllowOverride directive. AllowOverride can be set globally or per directory. For example, in your httpd.conf file, you could use the following:

```
# Each directory to which Apache has access can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).
#
# First, we configure the "default" to be a very restrictive set of
# permissions.
#
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

Directives
To configure which configuration options are available to Apache by default, you must use the Options directive. Options can be None, or any combination of Indexes, Includes, FollowSymLinks, ExecCGI, or MultiViews. MultiViews isn't included in All and must be specified explicitly. These options are explained in Table 16.2.

# TABLE 16.2 Switches Used by the Options Directive

| Switch | Description |
| --- | --- |
| None | None of the available options are enabled for this directory. |
| All | All the available options, except for MultiViews, are enabled for this directory. |
| Indexes | In the absence of an index.html file or another DirectoryIndex file, a listing of the files in the directory will be generated as an HTML page for display to the user. |
| Includes | Server-side (SSIs) are permitted in this directory. This can also be written as IncludesNoExec if you want to allow includes, but don't want to allow the exec option in them. For security reasons, this is usually a good idea in directories over which you don't have complete control, as UserDir. |
| FollowSymLinks | Allows access to directories that are symbolically linked to a document directory. Setting this is a bad idea; you should never set this globally for the whole server and only rarely for individual directories. This option is a potential security risk because it allows Web users to escape from the document directory, and it could potentially allow them access to portions of your file system where you really don't want people peeking around. |