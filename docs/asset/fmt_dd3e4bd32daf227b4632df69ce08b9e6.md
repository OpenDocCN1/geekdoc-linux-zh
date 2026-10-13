
# 列表 21-2（继续）

```apache
Options Indexes Includes FollowSymLinks

AllowOverride None

Order allow,deny

Allow from all

<Directory>

UserDir public_html

DirectoryIndex index.html index.htm index.shtml index.php index.php4

index.php3.cgi

AccessFileName .htaccess

<Files ~ "^\.ht">

  Order allow,deny

  Deny from all

</Files>

UseCanonicalName On

TypesConfig /etc/mime.types

DefaultType text/plain

<IfModule mod_magic.c>

  MIMagFile conf/magic

</IfModule>

HostnameLookups Off

ErrorLog /var/log/httpd/error_log

LogLevel warn

LogFormat "%h %l %u %r* %s %b \"(Referer)i\" \"(User-Agent)i\" d

LogFormat "%h %l %u %r* %s %b" common

LogFormat "%%(Referer)i -> %%U" refer

LogFormat "%%(User-agent)i" agent

CustomLog /var/log/httpd/access_log combined

ServerSignature On

Alias /icons/ "/var/www/icons/"

<Directory "/var/www/icons/">

  Options Indexes MultiViews

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>

ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"

<Directory "/var/www/cgi-bin">

  AllowOverride None

  Options ExecCGI

  Order allow,deny

  Allow from all

</Directory>
```

# 第 21 章：配置 Web 服务 495

```apache
IndexOptions FancyIndexing

AddIconByEncoding (CMP,/icons/text.compressed.gif) x-compress x-gzip

AddIconByType (TXT,/icons/text.gif) text/*

AddIconByType (IMG,/icons/image2.gif) image/*

AddIconByType (SND,/icons/sound2.gif) audio/*

AddIconByType (VID,/icons/movie.gif) video/*

AddIcon /icons/binary.bin .exe

AddIcon /icons/binhex.gif .hqx

AddIcon /icons/tar.gif .tar

AddIcon /icons/world2.gif .wrl .wrl .vrm .vrm .iv

AddIcon /icons/compressed.gif .z .zip .tgz .zip

AddIcon /icons/a.gif .ps .ai .eps

AddIcon /icons/layout.gif .html .shtml .htm .pdf

AddIcon /icons/text.gif .txt

AddIcon /icons/c.gif .c

AddIcon /icons/p.gif .pl .py

AddIcon /icons/f.gif .for

AddIcon /icons/dvi.gif .dvi

AddIcon /icons/uencoded.gif .uu

AddIcon /icons/script.gif .conf .sh .sh .csh .ksh .tcl

AddIcon /icons/text.gif .tex

AddIcon /icons/bomb.gif .core

AddIcon /icons/back.gif ..

AddIcon /icons/hand.right.gif ^^DIRECTORY^^

AddIcon /icons/folder.gif ^^DIRECTORY^^
```
