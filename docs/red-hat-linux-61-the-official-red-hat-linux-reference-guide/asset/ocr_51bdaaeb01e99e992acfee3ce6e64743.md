# Chapter 10. Apache HTTP Server

tictory and its subdirectories. Any directive which is applicable to a directory may be used within <Directory> tags.

By default, restrictive parameters are applied to the root directory (/), using the Options (see Section 10.5.25 Options) and AllowOverride (see Section 10.5.26 AllowOverride) directives. Under this configuration, any directory on the system which needs permissive permissions must be explicitly given those settings.

In the default configuration, another Directory container is configured for the DocumentRoot which assigns rigid parameters to the directory tree so that the Apache HTTP Server can access the files residing.

The Directory container can also be used to configure additional cgi-bin directories for serveride applications outside of the directory specified in the ScriptAlias directive (refer to Section 10.5.44 ScriptAlias for more information about the ScriptAlias directive).

To accomplish this, the Directory container must set the ExecCGI option for that directory.

For example, if CGI scripts are located in /home/my_cgi_directory, add the following Directory container to the httpd.conf file:

```
<Directory>/home/my_cgi_directory>
Options ExecCGI
</Directory>
```

Next, the AddHandler directive must not be uncommented to identify files with the .cgi extension as CGI scripts. See Section 10.5.59 AddHandler for instructions on setting AddHandler.
For this work, permissions for CGI scripts, and the entire path to the scripts, must be set to 0755.

# 10.5.25. Options

The Options directive controls which features are available in a particular directory. For example, the restrictive parameters specified for the root directory, Options is set to only FollowSymLinks. No features are enabled, except that the server is allowed to follow symbolic links in the root directory.

By default, the DocumentRoot directory, Options is set to include Indexes and FollowSymLinks. Indexes permits the server to generate a directory listing for a directory if no DirectoryIndex (for example, index.html) is specified. FollowSymLinks allows the server to follow symbolic links in that directory.

> Note
Options statements from the main server configuration section needs to be replicated to each VirtualHost containers individually. Refer to Section 10.5.69 VirtualHost for more information about VirtualHost containers.

# 10.5.26. AllowOverride

The AllowOverride directive sets which or not any Options can be overridden by the declarations in an .htaccess file. By default, both root directory and the DocumentRoot are set to allow no .htaccess overrides.