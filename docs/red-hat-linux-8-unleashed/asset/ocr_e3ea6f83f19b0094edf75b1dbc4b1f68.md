# Apache Modules

mod_auth_dbm.so mod_env.so mod_proxy_connect.so mod_unique_id.so
mod_auth_digest.so mod_expires.so mod_proxy_ftp.so mod_userdir.so
mod_auth_mysql.so mod_headers.so mod_proxy_http.so mod_usertrack.so
mod_auth_pgsql.so mod_imap.so mod_proxy.so mod_vhost_alias.so
mod_auth.so mod_include.so mod_python.so mod_autoindex.so
mod_info.so mod_rewrite.so

Each module adds directives that can be used in your configuration files. As you might guess, there are far too many extra commands, switches, and options to describe all them in this chapter. The following sections briefly describe those modules available with Red Hat’s Apache installation.

# mod_access

mod_access controls access to areas of your Web server by IP addresses, hostnames, or environment variables. For example, you might want to allow anyone from your own domain to access certain areas of the Web. Refer to the "File System Authentication and Access Control" section for more information.

# mod_alias

mod_alias manipulates the URLs of incoming HTTP requests, such as redirecting a client request to another URL. It can also map a part of the file system into your Web hierarchy. For example,

```
Alias /images/ /home/wsb/graphics/
```

would fetch contents from the /home/wsb/graphics directory for any URL that starts with /images/. This is done without the client knowing anything about it. If you use redirection, the client will be instructed to go to another URL to find the requested content. More advanced URL manipulation can be accomplished with mod_rewrite.

# mod_asis

mod_asis is used to specify, in fine detail, all information to be included in a response. This will completely bypass headers that Apache might otherwise have added to the response. All files with an .asis extension will be sent straight to the client without any changes.

As a short example of the use of mod_asis, assume that you've moved content from one location to another on your site. You must inform people who try to access this resource that it has moved, as well as redirect them to the new location automatically. To provide this information and redirection, you can add the following code to a file with an .asis extension: