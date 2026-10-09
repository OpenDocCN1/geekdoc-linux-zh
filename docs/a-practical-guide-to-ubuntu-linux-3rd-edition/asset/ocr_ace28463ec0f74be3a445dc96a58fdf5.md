Default: none (Apache will not start without this directive)
Ubuntu: Listen 80

# **Redirect**
*Tells the client to fetch a requested resource from a different, specified location.*
`Redirect [status] requested-path [new-URI]`

where *status* is the status that Apache returns along with the redirect. If you omit *status*, Apache assumes *temp*. The *status* can be an Apache error code in the range 300\~399 or one of the following:

+   - **permanent**	Returns status 301 (the resource has moved permanently)
+   - **temp**	Returns status 302 (the resource has moved temporarily)
+   - **seeother**	Returns status 303 (the resource has been replaced)
+   - **gone**	Returns status 410 (the resource has been removed—does not take a *new-URI* argument)

The *requested-path* is the absolute pathname of the ordinary file or directory that Apache is to redirect requests for. Apache redirects all requests that start with the absolute pathname specified by *requested-path*. (See the example below.) Use RedirectMatch (discussed next) if you want to use a regular expression in this argument.

The *new-URI* is the URL that Apache redirects requests to. If the *new-URI* starts with a slash (/*) and not *http://*, *ftp://*, or a similar prefix, Apache uses the same prefix that it was called with. Most Redirect directives require a *new-URI* argument.

A request must match all segments of the *requested-path* argument. Assume the following directive:

```
Redirect /www.example.com/pictures http://pictures.example.com/
```

Apache will redirect a request for *http://www.example.com/pictures/mom.jpg* to *http://pictures.example.com/mom.jpg* but, because the final segment does not match, it will not redirect a request for *http://www.example.com/pictures_mom.jpg*.

Contexts: server config, virtual host, directory, .htaccess
Specify in *sites-available/*\*
Default: none
Ubuntu: none

# **RedirectMatch**
*Tells the client to fetch a requested resource from a different location specified by a regular expression.*
`RedirectMatch [status] requested-path-re [new-URI]`

This directive is the same as Redirect (discussed above), except that you can use a regular expression (Appendix A) in *requested-path-re*.

Contexts: server config, virtual host, directory, .htaccess
Specify in *sites-available/*\*
Default: none
Ubuntu: none