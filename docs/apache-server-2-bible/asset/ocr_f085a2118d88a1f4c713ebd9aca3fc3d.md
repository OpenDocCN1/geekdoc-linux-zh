| Map Type | Description |
|---|---|
| dbm | A DBM file can be used as a map source. This can be venv useful and fast (compared to text files) when you have a large number of key-value pairs. Note that DBM-file-based maps are read during Apache startup and only reread if the file has been updated after the server is already up and running. The files are also reread during server restarts. |
| prg | An external program can generate the value. When a program is used, it is started at the Apache startup and data (key, value) is transferred between Apache and the program via standard input (stdin) and standard output (stdout). Make sure you use the RewriteLock directive to define a lock file when using an external program. When constructing such a program, also make sure that you read the input from the stdin and write it on stdout in a nonbuffered i/O mode. |

# ## RewriteBase

This directive is only useful if you are using rewrite rules in per-directory configuration files. It is also only required for URL paths that do not map to the physical directory of the target file. Set this directive to whatever alias you used for the directory. This will ensure that mod_rewrite will use the alias instead of the physical path in the final (substituted) URL.

+   * **Syntax:** RewriteBase base_URL
+   * **Default:** Current directory path of per-directory config (`.htaccess`)
+   * **Context:** Per-directory access control file (`.htaccess`)

For example, when an alias is set as follows:

```
```plain
Alias /icons/ "/www/nitec/htdocs/icons/"
```
```

and rewrite rules are enabled in the /www/nitec/htdocs/icons/.htaccess file, the RewriteBase directive should be set as follows:

```
```plain
RewriteBase /icons/
```
```

# ## RewriteLog

If you want to log the applications of your rewrite rules, use this directive to set a log filename. Like all other log directives, it assumes that a path without a leading slash (/) means that you want to write the log file in the server's root directory.