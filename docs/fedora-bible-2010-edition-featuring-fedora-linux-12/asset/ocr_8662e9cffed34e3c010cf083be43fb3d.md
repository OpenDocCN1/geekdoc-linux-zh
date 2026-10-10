# 798 Part IV: Fedora Network and Server Setup

```
</Directory>
```

The *Alias* directive points to a file system location (not necessarily within *DocumentRoot*). For example, with the following line in place, requests for documents in /bigjob (`http://www.mybox.com/bigjob/index.html`) would result in the retrieval of /home/newguy/proj/index.html.

```
Alias /bigjob /home/newguy/proj
```

The *icons* alias allows access to the Apache icons used by the Web server for your Web site. The *icons* directory is accessible from the /var/www directory.

The *ScriptAlias* directive performs a related function, but directories that it aliases contain executable code (most likely CGI scripts). The syntax is the same as for the *Alias* directive. Pay special attention whenever you use *ScriptAlias*. Because *ScriptAlias* defines the location of scripts that can be run from Web content on the server, make sure you assign only those directories that contain scripts that can be secured and won't open security holes in your system.

# Redirecting requests for old content

As content changes on your Web server, some of that content will become obsolete while other content may move to a different place in the file system or to a different server. Using the *Redirect* directive, you can redirect requests for old content to new locations.

By default, there are no *Redirect* directives set for your Apache server. However, you can uncomment the following example and tailor it to your needs:

```
# Redirect permanent /foo http://www.example.com/bar
```

*Redirect* can be used to instruct clients that the document they seek has moved elsewhere (to the same server or to an external location) by simply indicating the old and new locations. If the previous *Redirect* option were in place, a client’s attempt to access `http://www.mybox.com/foo` would redirect to `http://www.example.com/bar`.

Besides using *permanent* as the service for *Redirect* (which results in a redirect status 301), you could instead use *temp* (a redirect status of 302), *seeother* (a replaced status of 303), or *gone* (a permanently removed status of 401). You could also give any status code between 300 and 399 as the service, which represent different error responses. (These numbers are HTTP status codes.)

> **CROSS-REFERENCE:** The HTTP status codes are defined as part of the HTTP protocol in RFC 2616. Refer to that document at www.w3.org/Protocols/rfc2616/rfc2616.txt.