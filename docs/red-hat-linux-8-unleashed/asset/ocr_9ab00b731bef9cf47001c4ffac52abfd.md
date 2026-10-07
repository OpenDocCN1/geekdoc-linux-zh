# TABLE 16.2 Continued Description

| Switch | Description |
| ExecC | CGI programs are permitted in this directory, even if it isn't a directory defined in the ScriptAlias directive.
| MultiViews | This is part of the mod_negotiation module. When a client requests a document that can't be found, the server tries to figure out which document best fits the client's requirements. See http://localhost/manuals/mod/mod_negotiation.html for your local copy of the Apache documentation. |

> NOTE
This directives also affect all subdirectories of the specified directory.

AllowOverrides Directives
The AllowOverrides directives specify which configuration options .htaccess files can override. You can set this directive individually for each directory. For example, you can have different standards about what can be overridden in the main document root and in UserDir directories.

This capability is particularly useful for user directories, where the user doesn't have access to the main server configuration files.

AllowOverrides can be set to All or any combination of Options, FileInfo, AuthConfig, and Limit. These options are explained in Table 16.4.

# TABLE 16.4 Switches Used by the AllowOverrides Directive

| Switch | Description |
| Options | The .htaccess file can add options not listed in the Options directive for this directory.
| FileInfo | The .htaccess file can include directives for modifying document type information.
| AuthConfig | The .htaccess file may contain authorization directives.
| Limit | The .htaccess file may contain allow, deny, and order directives. |

# File System Authentication and Access Control

You're likely to include material on your Web site that isn't supposed to be available to the public. You must be able to lock out this material from public access and provide designated users with the means to unlock the material. Apache provides two methods for accomplishing this type of access: authentication and authorization. You can use different