
### Section 1: Global Environment

```
ServerRoot "/usr/local/apache"

PidFile logs/httpd.pid

<IfModule !perchild.c>

ScoreBoardFile logs/apache_runtime_status

</IfModule>

Timeout 300

KeepAlive On

MaxKeepAliveRequests 100

KeepAliveTimeout 15

<IfModule prefork.c>

StartServers      5

MinSpareServers   5

MaxSpareServers  10

MaxClients        20

MaxRequestsPerChild  0

</IfModule>

<IfModule threaded.c>

StartServers      3

MaxClients        8

MinSpareThreads   5

MaxSpareThreads  10

ThreadsPerChild  25

MaxRequestsPerChild  0

</IfModule>

<IfModule perchild.c>

NumServers        5

StartThreads      5

MinSpareThreads   5

MaxSpareThreads  10

MaxThreadsPerChild 20

MaxRequestsPerChild  0

</IfModule>
```

### Section 2: 'Main' server configuration

```
Port 80

User nobody

Group #-1

ServerAdmin you@your.address

# Added

ServerName www.domain.com

DocumentRoot "/usr/local/apache/htdocs"

<Directory />

    Options FollowSymLinks

    AllowOverride None

</Directory>

<Directory "/usr/local/apache/htdocs">

    Options Indexes FollowSymLinks MultiViews

    AllowOverride None

    Order allow,deny

    Allow from all

</Directory>

UserDir public_html

DirectoryIndex index.html

AccessFileName .htaccess

<Files ~ "^\.ht">

    Order allow,deny

    Deny from all

</Files>

UseCanonicalName On

TypesConfig conf/mime.types

DefaultType text/plain

<IfModule mod_mime_magic.c>

    MIMEMagicFile conf/magic

</IfModule>

HostnameLookups Off

ErrorLog logs/error_log

LogLevel warn

LogFormat ">%h %l %u %t \"%r\" %>s %b\" %i {Referer}\" \"%{User-Agent}i\" combined

LogFormat ">%h %l %u %t \"%r\" %>s %b\" common

LogFormat ">{Referer}i\" -> \"%U" referer

LogFormat ">%{User-agent}i" agent

CustomLog logs/access_log common

ServerSignature On

Alias /icons/ "/usr/local/apache/icons/"

<Directory "/usr/local/apache/icons">

    Options Indexes MultiViews

    AllowOverride None

    Order allow,deny

    Allow from all

  </Directory>

  ScriptAlias /cgi-bin/ "/usr/local/apache/cgi-bin/"

  <Directory "/usr/local/apache/cgi-bin">

    AllowOverride None

    Options None

    Order allow,deny

    Allow from all

  </Directory>

  IndexOptions FancyIndexing VersionSort

  AddIconByEncoding (CMP,/icons/compressed.gif) x-compress x-gzip

  AddIconByType (TXT,/icons/text.gif) text/*

  # Many more AddIconByType directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  AddIcon /icons/binary.gif .bin .exe

  # Many more AddIcon directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  DefaultIcon /icons/unknown.gif

  ReadmeName README

  IndexIgnore .??* *~ \* HEADER\* README\* RCS CVS \*,v \*,t

  AddEncoding x-compress Z

  AddEncoding x-gzip .gz .tgz

  AddLanguage da .dk

  AddLanguage nl .nl

  AddLanguage en .en

  # Many more AddLanguage directives follow in the

  # default httpd.conf but removed here to keep

  # this simple.

  LanguagePriority da nl et fr de el it ja kr no pl pt pt-br lts ca es sv tw

  AddDefaultCharset ISO-8859-1

  AddCharset ISO-8859-1 .iso8859-1 .latin1

  AddCharset ISO-8859-2 .iso8859-2 .latin2 .cen

  # Many more AddCharset directives follow in the

  # default httpd.conf but removed here to keep

# this simple.

AddType application/x-tar .tgz

BrowserMatch "Mozilla/2" nokeepalive

BrowserMatch "MSIE 4\.0b2;" nokeepalive downgrade-1.0 force-response-1.0

BrowserMatch "RealPlayer 4\.0" force-response-1.0

BrowserMatch "Java/1\.0" force-response-1.0

BrowserMatch "JDK/1\..0" force-response-1.0
```

### Section 3: Virtual Hosts

```
# No virtual server defined in this chapter.
```
