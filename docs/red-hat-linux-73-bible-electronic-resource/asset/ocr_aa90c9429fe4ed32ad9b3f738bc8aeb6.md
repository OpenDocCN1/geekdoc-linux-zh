# Table 21-1: Dynamic Shared Object (DSO) Modules

| Module | Description |
| :--- | :--- |
| mod_access | Provides access control based on originating host name/IP address. |
| mod_actions | Conditionally executes CGI scripts based on the file's MIME type or the request method. |
| mod_alias | Allows for redirection and mapping parts of the physical file system into logical entities accessible through the Web server. |
| mod_asis | Enables files to be transferred without adding any HTTP headers (for example, the Status, Location, and Content-type header fields). |
| mod_auth | Provides access-control based on user name/password pairs. The authentication information is stored in a plain-text file, although the password is encrypted using the crypt() system call. |
| mod_auth_anon | Similar to anonymous FTP, this module enables predefined user names access to authenticated areas by using a valid e-mail address as a password. |
| mod_auth_db | Provides access-control based on user name/password pairs. The authentication information is stored in a Berkeley DB binary database file, with encrypted passwords. |
| mod_auth_dbm | Provides access-control based on user name/password pairs. The authentication information is stored in a DBM binary database file, with encrypted passwords. |
| mod_autoindex | Implements automatically generated directory indexes. |
| mod_bandwidth | Allows bandwidth limits to be set based on a per-connection or total server basis. |
| mod_cgi | Controls the execution of files that are parsed by the “cgi-script” handler or that have a MIME type of x-httpd-cgi. |
| mod_digest | Provides access-control based on user name/password pairs. The authentication information is MD5-encrypted and stored in a plain-text file. |
| mod_dir | Sets the list of filenames that may be used if no explicit filename is selected in a URL that references a directory. |
| mod_env | Controls environment variables passed to CGI scripts. |
| mod_example | Illustrates how the server handles module references. |
| mod_expires | Implements time limits on cached documents by using the Expires HTTP header. |
| mod_headers | Enables the creation and generation of custom HTTP headers. |