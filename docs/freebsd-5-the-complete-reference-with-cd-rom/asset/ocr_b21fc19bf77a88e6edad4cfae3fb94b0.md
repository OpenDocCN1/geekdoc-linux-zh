■ **IfModule** This directive begins a directive block that applies only if the named module is present. For instance, `<IfModule prefork.c>` begins a directive block that applies only if the prefork.c module is present. (This module is compiled into the main FreeBSD Apache binary.) The directive’s meaning can be reversed by preceding the module name with an exclamation mark ( ! ), as in `<IfModule !mpm_netware.c>`, which denotes a directive that applies only if the mpm_netware.c module is *not* available. The default FreeBSD `httpd.conf` file uses this directive heavily.

You can learn what modules are compiled into the main Apache binary by using the -1 option to httpd, thus:

```
$ /usr/local/sbin/httpd -1
Compiled in modules:
core.c
prefork.c
http_core.c
mod_so.c
```

Combining this command with the list of LoadModule directives in httpd.conf provides you with a complete list of the available modules. You can, of course, add more by installing the module (if necessary) and adding a LoadModule directive to make it available.

> A simple Apache server isn’t likely to need any modules except those that it comes preconfigured to use. You may need to adjust your module configuration if you replace your Apache binary with one that includes a different mix of modules or if you need some unusual feature that can be provided by a module, such as the ability to convert text into a graphic on the fly or various types of database interfaces. Detailing all the options is well beyond the scope of this book, however.
> 
> In some cases, you may want to comment out modules provided in the standard FreeBSD Apache configuration. For instance, the default configuration includes the following line:

```
LoadModule cgi_module libexec/apache/mod_cgi.so
```

This line enables support for the Common Gateway Interface (CGI), which enables Apache to run scripts to generate web pages dynamically. This advanced feature is very useful on servers that need to customize their output, such as web search engines or e-commerce sites; but it’s a potential security threat because a poorly written CGI script could serve as an entry point for crackers. Thus, if your web server doesn’t need to serve CGI scripts, you may want to comment out this line. Other modules may also be unnecessary; for instance, the userdir_module handles user directories, so if your site lacks these, you can comment out the line that loads this module.