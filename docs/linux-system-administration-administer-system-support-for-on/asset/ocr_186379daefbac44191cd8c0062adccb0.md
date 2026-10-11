```
# This file defines server settings which affect which types of services
# are allowed, and in what circumstances.

# Each directory to which Apache has access, can be configured with respect
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).

# Originally by Rob McCool

# This should be changed to whatever you set DocumentRoot to.

<Directory /usr/local/etc/httpd/htdocs>
```

Remember the "It worked!" page from http://localhost/? It's located currently in the /var/lib/httpd/htdocs. You may want to change this line to reflect it, or you can move your main Web server pages into that directory. If you want, you can always specify another directory.

```
# This may also be "None", "All", or any combination of "Indexes",
# "Includes", "FollowSymLinks", "ExecCGI", or "MultiViews".

# Note that "MultiViews" must be named *explicitly* -- "Options All"
# doesn't give it to you (or at least, not yet).

Options Indexes FollowSymLinks
```

You can change this to include what other options you want. Options include server side includes, return the listing of the contents of a directory if there is no index.html file, or execute CGI scripts.

```
# This controls which options the .htaccess files in directories can
# override. Can also be "All", or any combination of "Options", "FileInfo",
# "AuthConfig", and "Limit"

AllowOverride None

# Controls who can get stuff from this server.

order allow,deny
allow from all
```