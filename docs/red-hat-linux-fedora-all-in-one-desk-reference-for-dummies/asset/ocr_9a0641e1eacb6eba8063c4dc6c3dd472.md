The following list describes some of the access control directives. In particular, notice the AuthUserFile directive; you can have password-based access control for specific directories.

**Options** `opt1 opt2 ...` — Specifies the access control options for the directory section in which this directive appears. The options can be one or more of the following:

+   - `None` disables all access control features.
+   - `All` turns on all features for the directory.
+   - `FollowSymLinks` enables the server to follow symbolic links.
+   - `SymLinksIfOwnerMatch` follows symbolic links, only if the same user of the directory owns the linked directory.
+   - `ExecCGI` enables execution of CGI scripts in the directory.
+   - `Includes` enables server-side `include` files in this directory (the term *server-side include* refers to directives, placed in an HTML file, that the Web server processes before returning the results to the Web browser).
+   - `Indexes` enables clients to request indexes (directory listings) for the directory.
+   - `IncludesNOEXEC` disables the `#exec` command in server-side includes.

**AllowOverride** `directive1 directive2 ...` — Specifies which access control directives can be overridden on a per-directory basis. The directive list can contain one or more of the following:

+   - `None` stops any directive from being overridden.
+   - `All` enables overriding of any directive on a per-directory basis.
+   - `Options` enables the use of the `Options` directive in the directory-level file.
+   - `FileInfo` enables the use of directives controlling document type, such as `AddType` and `AddEncoding`.
+   - `AuthConfig` enables the use of authorization directives, such as `AuthName`, `AuthType`, `AuthUserFile`, and `AuthGroupFile`.
+   - `Limit` enables the use of `Limit` directives (`allow`, `deny`, and `order`) in a directory's access-configuration file.

**AuthName** `name` — Specifies the authorization name for a directory.

**AuthType** `type` — Specifies the type of authorization to be used. The only supported authorization type is Basic.