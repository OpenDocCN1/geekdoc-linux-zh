
# 852 Part IV: Fedora RHEL Network and Server Setup

```
# LoadModule foo_module modules/mod_foo.so
#nLoadModule auth_basic_module modules/mod_auth_basic.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule authn_file_module modules/mod_authn_file.so
```

```
LoadModule file_cache_module modules/mod_file_cache.so
LoadModule mem_cache_module modules/mod_mem_cache.so
LoadModule cgi_module modules/mod_cgi.so
```

Apache modules are included in the list of active modules using the LoadModule directive. ClearModuleList removes all entries from the current list of active modules. Each of the standard modules that come with Apache is described in Table 21-1.

If a particular module contains features that are not needed, it can be easily commented out of the preceding list. In fact, it is a good security practice to comment unused modules. Similarly, you might want to add the features or functionality of a third-party module (for example, mod_perl, which integrates the Perl runtime library for faster Perl script execution, or mod_php, which provides a scripting language embedded within HTML documents) by including these modules in the list.

> NOTE: Some modules, including prefork, http_core, and mod_so, are commented out in the http daemon in Fedora and RHEL. To see the list of modules compiled into the daemon, type the http -l command.

## Table 21-1: Dynamic Shared Object (DSO) Modules

| Module | Description |
| --- | --- |
| mod_actions | Conditionally executes CGI scripts based on the file's MIME type or the request method. |
| mod_alias | Allows for redirection and mapping parts of the file system into logical entities accessible through the Web server. |
| mod_asis | Enables files to be transferred without adding any HTTP headers (for example, the Status, Location, and Content-type header fields). |
| mod_auth_basic | Provides HTTP Basic Authentication. It is used in combination with authentication modules (such as mod_auth_file) and authorization modules (such as mod_auth_user). |
| mod_auth_digest | Provides MD5 Digest user authentication. |
| mod_authn_alias | Lets you create extended authenticators that are assigned to aliases. Later you can reference the aliases using AuthBasicProvider of AuthDigestProvider directives. |

## Chapter 21: Setting Up a Web Server

| Module | Description |
| --- | --- |
| mod_authn_anon | Similar to anonymous FTP, this module enables predefined usernames access to authenticated areas by using a valid e-mail address as a password. |
| mod_authn_dbd | Provides access to SQL tables to authenticate. It lets you use mod_auth_basic and mod_auth_digest fronts. |
| mod_authn_dbm | Provides access control based on username/password pairs. The authentication information is stored in a DBM database file, with encrypted passwords. |
| mod_authn_default | Offers a fallback authentication, if no other is used. Any credentials presented by the user are rejected. |
| mod_authn_file | Provides access control by user look-up in plain text files (Similar to mod_authn_dbm, but without exception). |
| mod_authz_ldap | Lets you use an LDAP directory to store the HTTP authentication database. |
| mod_authz_dbm | Provides access control to authenticated users based on group name. The authentication information is stored in a DBM database file. |
| mod_authz_default | If such as mod_authz_user or mod_authz_group are not configured, the module provides a fallback (simply rejecting authorization requests). |
| mod_authz_groupfile | Provides access control based on group membership. |
| mod_authz_host | Provides access control based on client hostname, IP address or other environment characteristics. |
| mod_authz_owner | With a verified username and password, this module allows access to files based on ownership. |
| mod_authz_user | Allows access to files based on whether an authenticated user is listed in a Required User directory. |
| mod_autoindex | Implements automatically generated directory indexes. |
| mod_cache | Allows local or proxied Web to be cached. Used with mod_disk_cache or mod_mem_cache modules. |
| mod_cern_meta | Offers a method of emulating CERN HTTPD file semantics. |
| mod_cgi | Controls the execution of files that are parsed by the "cgi-script" handler or for a MIME type of x-httpd-cgi ScriptAlias sets the default directory. |
| mod_cgid | Similar to mod_cgi with the exception that this module offers a ScriptSock directive to the node used with the cgi daemon. |

## Part IV: Fedora RHEL Network and Server Setup

| Module | Description |
|---|---|---|
| mod_dav | Provides Web-based Distributed Authororing and Versioning (WebDAV) to upload Web content using copy, create, move, and delete resources. |
| mod_dav_fs | Used to provide file system features to the mod_dav module, used with Web-based Distributed Authororing and Versioning (WebDAV). |
| mod_dbd | Uses apr to manage SQL database connections. (The apr_dbd framework offers a common API for different SQL databases.) |
| mod_deflate | Includes the DEFLATE output filter, to compress data before it sent. |
| mod_dir | Sets the default directory if no filename is specified. |
| mod_disk_cache | Used with mod_cache to provide disk-based storage. |
| mod_dumpio | Can log all bytes of data sent and received. |
| mod_env | Controls environment variables passed to CGI scripts. |
| mod_expires | Implements time limits on cached documents using Expires header. |
| mod_ext_filter | Before delivering a response to the client, pass it through an external filter. |
| mod_filter | Allows customized filtering. |
| mod_headers | Enables the creation of custom HTTP headers. |
| mod_ident | Lets you query an RFC 1413-compatible daemon for information on the owner of a connection. |
| mod_include | Implements Server-Side Includes (SSI), which are HTML documents containing conditional statements parsed by the server. |
| mod_info | Provides a detailed summary of the server's configuration, including a list of actively loaded modules. |
| mod_ldap | Used to speed performance of Web sites using LDAP servers. |
| mod_proxy | Implements an HTTP 1.1 proxy/gateway server. |
| mod_proxy_ajp | Uses mod_proxy for Apache JServer Protocol (version 1.3). |
| mod_proxy_balancer | Extension to mod_proxy to handle load balancing. |
| mod_proxy_connect | Extension to mod_proxy to handle CONNECT requests. |
| mod_proxy_ftp | Extension to mod_proxy to handle FTP requests. |
| mod_proxy_http | Extension to mod_proxy to handle HTTP requests. |
| mod_rewrite | Provides a flexible and extensible method for redirecting client requests and mapping incoming URLs to other locations in the file system. |
| mod_setenv | Conditionally sets environment variables based on the contents of various HTTP header fields. |
| mod_speling | Attempts to correct misspellings automatically in requested URLs. |
| mod_ssl | Implements cryptography using SSL and TLS protocols. |
| mod_status | Provides a summary of the activity of each individual http server process, including CPU and bandwidth usage. |
| mod_sueexec | Lets CGI scripts run with permission of a particular user or group. |
| mod_unique_id | Assigns the UNIQUE_ID environment variable to provide a unique identifier for each request. |
| mod_userdir | Specifies locations that can contain individual users' HTML documents. |
