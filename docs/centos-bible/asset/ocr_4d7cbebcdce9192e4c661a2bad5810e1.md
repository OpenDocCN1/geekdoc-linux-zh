# Part IV Networking

```
#
Alias /icons/ "/var/www/icons/"

&lt;Directory "/var/www/icons/"
    Options Indexes MultiViews FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
&lt;/Directory&gt;

# ScriptAlias: This controls which directories contain server scripts.
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

# "/var/www/cgi-bin" should be changed to whatever your ScriptAlias
# CGI directory exists, if you have that configured.
#
&lt;Directory "/var/www/cgi-bin/"
    AllowOverride None
    Options None
    Order allow,deny
    Allow from all
&lt;/Directory&gt;
```

The Alias directive points to a file system location (not necessarily within the DocumentRoot). For example, with the following line in place, requests for documents in /bigjob/www.mybox.com/bigjob/index.html would result in the retrieval of /home/newguy/proj/index.html.

```
Alias /bigjob /home/newguy/proj
```

The icons alias allows access to the Apache icons used by the Web Server for your web site. The icons directory is accessible from the /var/www directory.

The ScriptAlias directive performs a related function, but directories that it aliases contain executable code (most likely CGI scripts). The syntax is the same as for the Alias directive. Pay special attention whenever you use ScriptAlias. Because ScriptAlias defines where scripts that can be run from Web content on the server are located, you should make sure that you assign only those directories that contain scripts that are secured and won’t open security holes in your system.

# Redirecting Requests for Old Content

As content changes on your Web Server, some content will become obsolete, while other content may move to a different place in the file system or to a different server. Using the Redirect directive, you can re-direct requests for old content to new locations.

By default, there are no Redirect directives set for your Apache server. However, you can uncomment the following example and tailor it to your needs:

```
# Redirect permanent /foo http://www.example.com/bar
```

792