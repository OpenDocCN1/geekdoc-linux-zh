**Syntax:** RewriteCond _test_string condition_pattern_ [_flag-list_]

**Default:** None

**Context:** Server config, virtual host, perl-directory config (`.htaccess`)

The test string may be constructed with plain text, server variables, or back-references from both the current rewrite rule and the last rewrite condition. To access the _nth_ back-reference from the last `RewriteRule` directive, use `$n`; to access the _nth_ back-reference from the last `RewriteCond` directive, use `%n`.

To access a server variable, use the `${_variable name_}` format. For example, to access the `REMOTE_USER` variable, specify `%{REMOTE_USER}` in the test string.

Table 9-3 lists several special data access formats.

| **Table 9-3**<br>**Data Access Formats for RewriteCond Directive** | | | | 
| --- | --- | --- | --- |
| Format Specifier | Meaning | | | 
| %{ENV:_variable_} | Use this to access any environment variable that is available to the Apache process. | | | 
| %{HTTP:_header_} | Use this to access the HTTP header used in the request. | | | 
| %{LA-U:_variable_} | Use this to access the value of a variable that is not available in the current stage of processing. For example, if you need to make use of the `REMOTE_USER` server variable in a rewrite condition stored in the server's configuration file (`httpd.conf`), you cannot use %{REMOTE_USER} because this variable is only defined after the server has performed the authentication phase, which comes after `mod_rewrite`'s URL processing phase. To look ahead at what the username of the successfully authenticated user is, you can use %{LA-U:REMOTE_USER} instead. However, if you are accessing the `REMOTE_USER` data from a RewriteCond in a per-directory configuration file, you can use %{REMOTE_USER} because the authorization phase has already finished and the server variable has become available as usual. The lookup is performed by generating a URL-based internal subrequest. | | | 
| %{LA-F:_variable_} | Same as the %{LA-U:_variable_} in most cases, but lookup is performed using a filename-based internal subrequest. | | |