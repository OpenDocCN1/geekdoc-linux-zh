# CONFIGURATION DIRECTIVES 913

Apache uses ServerName to construct a URI when it redirects a client (page 935). See Also UseCanonicalName (page 922).

Contexts: server config, virtual host
Specify in sites-available/*
Default: none
Ubuntu: none

DocumentRoot Points to the root of the directory hierarchy that holds the server's content.

```
DocumentRoot dirname
```

where dirname is the absolute pathname of the directory at the root of the directory hierarchy that holds the Apache serves. Do not use a trailing slash. You can put the directory root wherever you like, as long as the www-data has read access to the ordinary files and execute access to the directory files in directory hierarchy. The DHS (page 213) specifies /srv as the top-level directory for this purpose. The following directive puts the document root at /srv/www:

```
DocumentRoot /srv/www
```

Contexts: server config, virtual host
Specify in sites-available/*
Default: /usr/local/apache/htdocs
Ubuntu: /var/www

UserDir Allows users to publish content from their home directories.

```
UserDir disabled \| enabled user-list
```

where dirname is the name of a directory, if it appears in a user's home directory, Apache publishes to the Web. The disabled keyword prevents content from being published from users' home directories; enables causes content to be published from the home directories of users in the SPACE-separated user-list. When you do not specify a dirname, Apache publishes to ~/public/html.

Apache can combine the effects of multiple UserDir directives. Suppose you have

```
UserDir disabled
UserDir enabled user1 user2 user3
UserDir web
```

The first directive turns off user publishing for all users. The second directive enables publishing for three users. The third directive makes the web of the directory that, if it appears in one of the specified users' home directories, Apache publishes to the Web.

To cause a browser to display the content published by a user, specify in the location bar the name of the Web site followed by a ~ and the user's username. For example, if Sam published content in the public_html directory in his home directory and the URL of the Web site was www.example.com, you would enter http://www.example.com/~sam