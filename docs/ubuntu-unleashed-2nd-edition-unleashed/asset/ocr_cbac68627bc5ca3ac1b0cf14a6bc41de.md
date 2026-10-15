# Options Directives

To configure which configuration options are available to Apache by default, you must use the Options directive. Options can be None; All; or any combination of Indexes, Includes, FollowSymLinks, ExecCGI, and Multiviews. Multiviews isn't included in All and must be specified explicitly. These options are explained in Table 20.2.

# TABLE 20.2 Switches Used by the Options Directive

| Switch | Description |
|---|---|
| None | None of the available options are enabled for this directory. |
| All | All the available options, except for Multiviews, are enabled for this directory. |
| Indexes | In the absence of an index.html file or another DirectoryIndex file, a listing of the files in the directory is generated as an HTML page for display to the user. |
| Includes | Server-side includes (SSIs) are permitted in this directory. This can also be written as IncludesNoExec if you want to allow includes but don't want to allow the exec option in them. For security reasons, this is usually a good idea in directories over which you don't have complete control, such as UserDir directories. |
| FollowSymLinks | Allows access to directories that are symbolically linked to a document directory. You should never set this globally for the whole server and only rarely for individual directories. This option is a potential security risk because it allows web users to escape from the document directory and could potentially allow them access to portions of your file system where you really don't want people poking around. |
| ExecCGI | CGI programs are permitted in this directory, even if it is not a directory defined in the ScriptAlias directive. |
| Multiviews | This is part of the mod_negotiation module. When a client requests a document that can't be found, the server tries to figure out which document best suits the client's requirements. See http://localhost/manuals/mod/_mod_negotiation.html for your local copy of the Apache documentation. |

> NOTE
> These directives also affect all subdirectories of the specified directory.

# AllowOverrides Directives

The AllowOverrides directives specify which configuration options .htaccess files can override. You can set this directive individually for each directory. For example, you can have different standards about what can be overridden in the main document root and in UserDir directories.

This capability is particularly useful for user directories, where the user does not have access to the main server configuration files.