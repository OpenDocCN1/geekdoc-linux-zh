To create password files for use with mod_auth_dbm, you must use the htdigest utility. It has more or less the same functionality as the htpasswd utility. See the man page of htdigest for further information.

# mod_autoindex

The mod_autoindex module dynamically creates a file list for directory indexing. The list will be rendered in a user-friendly manner similar to those lists provided by ftp's built-in ls command.

# mod_cgi

mod_cgi allows execution of CGI programs on your server. CGI programs are executable files residing in the /var/www/cgi-bin directory, and are used to dynamically generate data (usually HTML) for the remote browser when requested.

# mod_dir and mod_env

The mod_dir module is used to determine which files are returned automatically when a user tries to access a directory. The default is index.html. If you have users who create Web pages on Windows systems, you'll probably want to also include index.html like this:

```
DirectoryIndex index.html index.htm
```

# mod_expires

mod_expires controls environment variables are passed to CGI and SSI scripts.

mod_expires is used to add an expiration date to content on your site by adding an Expires header to the HTTP response. Web browsers or cache servers won't cache expired content.

# mod_headers

mod_headers is used to manipulate the HTTP headers of your server's responses. You can add, merge, or delete headers as you see fit. The module provides a Header directive for this. Ordering of the Header directive is important. A set followed by an unset for the same HTTP header will remove the header altogether. You can place Header directives almost anywhere within your configuration files. These directives are processed in the order:

+   1. Core server
2. Virtual host
3. <Directory> and .htaccess
4. <Location>
5. <Files>