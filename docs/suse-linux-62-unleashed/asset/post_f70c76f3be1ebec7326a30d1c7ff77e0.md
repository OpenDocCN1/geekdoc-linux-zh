
# LISTING 11.2 CONTINUED

```c
AddModule mod_include.c
AddModule mod_autoindex.c
AddModule mod_dir.c
AddModule mod_cgi.c
AddModule mod_asis.c
AddModule mod_imap.c
AddModule mod_actions.c
AddModule mod_spelling.c
AddModule mod_userdir.c
AddModule mod_proxy.c
AddModule mod_alias.c
AddModule mod_rewrite.c
AddModule mod_access.c
AddModule mod_auth.c
AddModule mod_auth_anon.c
AddModule mod_auth_dbm.c
AddModule mod_auth_db.c
AddModule mod_digest.c
AddModule mod_cern_meta.c
AddModule mod_expires.c
AddModule mod_headers.c
AddModule mod_usrack.c
AddModule mod_example.c
AddModule mod_unique_id.c
AddModule mod_so.c
AddModule mod_setenvif.c
AddModule mod_perl.c
AddModule mod_php3.c
```

```apache
#
# ExtendedStatus controls whether Apache generate "full" status
# information (ExtendedStatus On) or just basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.

#ExtendedStatus On

### Section 2: 'Main' server configuration
#
# The directives in this section set up the values used by the 'main'
# server, which responds to any requests that aren't handled by a
# <VirtualHost> definition. These values provide defaults for
# any <VirtualHost> containers you may define later in the file.
```

# Apache Server
CHAPTER 11

# LISTING 11.2 CONTINUED

# 11

```apache
#
# All of these directives may appear inside <VirtualHost> containers,
# in which case these default settings will be overridden for the
# virtual host being defined.

#
# If Server directive (set earlier in the 'Global Environment'
# section) is set to 'inetd', the next few directives don't have any
# effect since their settings are defined by the inetd configuration.
# Skip ahead to the ServerAdmin directive.

#
# Port: The port to which the standalone server listens. For
# ports < 1023, you will need httpd to be run as root initially.

Port 80

# If you wish httpd to run as a different user or group, you must run
# httpd as root initially and it will switch.

# User/Group: The name (or #number) of the user/group to run httpd as.
# On SCO (DOT 3) use "User Peter" and "group nogroup".
# On HPUX you may not be able to use shared memory as nobody, and the
# suggested workaround is to create a user www and use that user.
# NOTE that some kernels refuse to setgid(Group) or semctl(IPC_SET)
# when the value of (unsigned)Group is above 60000;
# don't use Group nogroup on these systems!

User wwwrun
Group nogroup

# ServerAdmin: Your address, where problems with the server should be
# e-mailed. This address appears on some server-generated pages, such
# error documents.

ServerAdmin root@localhost
```

![](img/cbac72550c7126a22162e94d91a0c360_428_0.png)

# Networking and Internet Services
PART II

# LISTING 11.2 CONTINUED

```apache
# ServerName allows you to set a host name which is sent back to clients for
# your server if it's different than the one the program would get (i.e., use
# "www" instead of the host's real name).

# Note: You cannot just invent host names and hope they work. The name you
# define here must be a valid DNS name for your host. If you don't understand
# this, ask your network administrator.
# If your host doesn't have a registered DNS name, enter its IP address here.
# You will have to access it by its address (e.g., http://123.45.67.89/)
# anyway, and this will make redirections work in a sensible way.

# ServerName allen.suse.de

# DocumentRoot : The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.

DocumentRoot "/usr/local/httpd/htdocs"

# Each directory to which Apache has access, can be configured with
# to which services and features are allowed and/or disabled in that
# directory (and its subdirectories).

# First, we configure the "default" to be a very restrictive set of
# permissions.

<Directory />
Options FollowSymLinks
AllowOverride None
</Directory>

# Note that from this point forward you must specifically allow
# particular features to be enabled - so if something's not working as
# you might expect, make sure that you have specifically enabled it
# below.

# This should be changed to whatever you set DocumentRoot to.
```

```apache
#<Directory "/usr/local/httpd/htdocs">

# This may also be "None", "All", or any combination of Indexes,
# "Includes", "FollowSymLinks", "ExecCGI", or "MultiViews"
#
# Note that "MultiViews" must be named "explicitly" --- "Options All"
# doesn't give it to you.

Options Indexes FollowSymLinks

# This controls which options the .htaccess files in directories can
# override. Can also be "All", or any combination of "Options", "FileInfo",
# "AuthConfig", and "Limit"

AllowOverride None

# Controls who can get stuff from this server.

Order allow,deny
Allow from all
</Directory>

# UserDir: The name of the directory which is appended onto a user's home
# directory if a -user request is received.
UserDir public_html

# Control access to UserDir directories. The following is an example
# for a site where these directories are restricted to read-only.

#<Directory /*/public_html>
# AllowOverride FileInfo AuthConfig Limit
# Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
# <Limit GET POST OPTIONS PROIND>
# Order allow,deny
# Allow from all
```

```apache
# </Limit>
# <Limit> PUT DELETE PATCH PROPPATCH MKCOL COPY MOVE MOVE LOCK UNLOCK
# Order deny,allow
# Deny from all
# </Limit>
#</Directory>
```

# DirectoryIndex: Name of the file or files to use as a pre-written HTML directory index. Separate multiple entries with spaces.
# DirectoryIndex index.html

# AccessFileName: The name of the file to look for in each directory
# for access control information.
AccessFileName .htaccess

# The following lines prevent .htaccess files from being viewed by
# Web clients. Since .htaccess files often contain authorization
# information, access is disallowed for security reasons. Comment
# these lines out out if you want Web visitors to see the contents of
# .htaccess files. If you change the AccessFileName directive above,
# be sure to make the corresponding changes here.

<Files .htaccess>
Order allow,deny
Deny from all
</Files>

# CacheNegotiatedDocs: By default, Apache sends "Pragma: no-cache" with each
# document that was negotiated on the basis of the content. This asks proxy
# servers not to cache the document. Uncommenting the following line disables
# this behavior, and proxies will be allowed to cache the documents.
#
CacheNegotiatedDocs

# UseCanonicalName: (new for 1.3) With this setting turned on, whenever
# Apache needs to construct a self-referencing URL (a URL that refers to the
# server the response is coming from) it will use ServerName and
# Port to form a "canonical" name. With this setting off, Apache will
# use the hostname:port that the client supplied, when possible. This
# affects SERVER_NAME and SERVER_PORT in CGI scripts.

```apache
UseCanonicalName On
```

```apache
# TypesConfig describes where the mime.types file (or equivalent) is
# to be found.
```

```apache
TypesConfig /etc/httpd/mime.types
```

```apache
# DefaultType is the default MIME type the server will use for a document
# if it cannot otherwise determine one, as from extensions.
# If your server contains mostly text or HTML documents, 'text/plain' is
# a good value. Most of your content is binary, such as applications
# or images, you may want to use "application/octet-stream" instead to
# keep browsers from trying to display binary files as though they are
# text.

```apache
DefaultType text/plain
```

```apache
# The mod_mime_magic module allows the server to use various hints from the
# contents of the mime file itself to determine its type. The MIMEMagicFile
# directive tells the module where the hint definitions are located.
# mod_mime_magic is not part of the default server (if you have to add
# it yourself with a LoadModule [see the DSO paragraph in the 'Global
# Environment' section], or recompile the server and include mod_mime_magic
# as part of the configuration), so it is enclosed in an <IfModule> container.
# This means that the MIMEMagicFile directive will only be processed if the
# module is part of the server.
```

```apache
<IfModule mod_mime_magic.c>
MIMEMagicFile /etc/httpd/magic
</IfModule>
```

```apache
# HostnameLookups: Log the names of clients or just their IP addresses
```
