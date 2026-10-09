# ## deny from env=variable

This directive, a variation of the `deny` directive, denies access capability for all hosts for which the specified environment is set.

**Syntax**: `deny from env=variable`

**Context**: Directory, location, per-directory access control file (.htaccess)

**Override**: Limit

For example, if you want to deny all hosts using Microsoft Internet Explorer access, you can use the `BrowserMatch` directive to set a variable called `ms$=browser` whenever a browser identified itself to the server with the string "MSIE".

```
```
BrowserMatch "MSIE" ms$=browser
```
```

Now you can use a `<Directory>` container to specify the `deny` directive, as follows:

```
```
<Directory /path/to/vbscript_directory>
    order deny,allow
    allow from all
    deny from env=ms_browser
</Directory>
```
```

If you are interested in blocking access to a specific HTTP request method, such as GET, POST, or PUT, you can use the `<Limit>` container to do so. For example:

```
```
<Location /cgi-bin>
    <Limit POST>
        order deny,allow
        deny from all
        allow from yourdomain.com
    </Limit>
</Location>
```
```

This example allows POST requests to the `cgi-bin` directory only if hosts in the `yourdomain.com` domain make the request. In other words, if this site has some HTML forms that send user input data via the HTTP POST method, only the users in yourdomain.com will be able to use these forms effectively. Typically, CGI applications are stored in the `cgi-bin` directory, and many sites feature HTML forms that use the POST method to dump data to CGI applications. Using the preceding host-based access-control configuration, a site can allow anyone to run a CGI script but only allow a certain site (in this case, yourdomain.com) to actually post data to one or more CGI scripts. This gives the CGI access in such a site a bit of read-only character. Everyone can run applications that generate output without taking any user input, but only users of a certain domain can provide input.