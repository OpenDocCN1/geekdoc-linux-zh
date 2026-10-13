This directive sets the directory access control filename. Some Web administrators change the default (.htaccess) to enhance security, because the .htaccess name is widely known. If you plan to change the name, choose a name that starts with a period so that it won't show up in directory listings. Also note that the default access.conf file prohibits Apache from looking into any directory level access control file. If you plan to use such access control files, make sure you modify the httpd.conf file accordingly. For example, the default httpd.conf file has the following configuration segment:

```
<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>
```

This configuration uses the AllowOverride directive to prohibit Apache from looking into the AccessFileName-specified file. If you are interested in allowing Apache to look for an access control file in a certain subsection of your site, use the following configuration:

```
<Directory "/path/to/your/dir">
Options FollowSymLinks
AllowOverride All
</Directory>
```

This configuration allows you to have an access control file such as .htaccess in the /path/to/your/dir directory or in any of the subdirectories below it. It also allows you to override all the allowed directives. If you are interested in a more restricted setting, set AllowOverride to one of the following settings:

+   - **AuthConfig:** Allows the authorization directives, such as AuthDBMGroupFile, AuthDBMUserFile, AuthGroupFile, AuthName, AuthType, AuthUserFile, and require.
+   - **FileInfo:** Allows the document types directives, such as AddEncoding, AddLanguage, AddType, DefaultType, ErrorDocument, and LanguagePriority.