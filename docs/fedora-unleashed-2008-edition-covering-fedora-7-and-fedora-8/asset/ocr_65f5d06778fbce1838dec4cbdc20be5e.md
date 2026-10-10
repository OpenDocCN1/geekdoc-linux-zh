# mod_dir and mod_env

The mod_dir module is used to determine which files are returned automatically when a user tries to access a directory. The default is index.html. If you have users who create web pages on Windows systems, you should also include index.htm, like this:

```
DirectoryIndex index.html index.htm
```

mod_env controls how environment variables are passed to CGI and SSI scripts.

# mod_expires

mod_expires is used to add an expiration date to content on your site by adding an Expires header to the HTTP response. Web browsers or cache servers don’t cache expired content.

# mod_headers

mod_headers is used to manipulate the HTTP headers of your server’s responses. You can replace, add, merge, or delete headers as you see fit. The module supplies a Header directive for this. Ordering of the Header directive is important. A set followed by an unset for the same HTTP header removes the header altogether. You can place Header directives almost anywhere within your configuration files. These directives are processed in the following order:

+   Core server
+   Virtual host
+   `<Directory>` and .htaccess files
+   `<Location>`
+   `<Files>`

# mod_info and mod_log_config

mod_info provides comprehensive information about your server’s configuration. For example, it displays all the installed modules, as well as all the directives used in its configuration files.

mod_log_config defines how your log files should look. See the “Logging” section for further information about this subject.