
# 配置 Apache Web 服务器 389

```
ServerRoot "/etc/httpd"
PidFile run/httpd.pid
Timeout 60
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```

```
<IfModule prefork.c>
  StartServers 8
  MinSpareServers 5
  MaxSpareServers 20
  ServerLimit 256
  MaxClients 256
  MaxRequestsPerChild 4000
</IfModule>
```

```
<IfModule worker.c>
  StartServers 4
  MaxClients 300
  MinSpareThreads 25
  MaxSpareThreads 75
  ThreadsPerChild 25
  MaxRequestsPerChild 0
</IfModule>
```

```
#Listen 12.34.56.78:80
Listen 80
```

```
LoadModule auth_basic_module modules/mod_auth_basic.so
LoadModule auth_digest_module modules/mod_auth_digest.so
LoadModule autn_file_module modules/mod_authn_file.so
LoadModule auth_alias_module modules/mod_auth_alias.so
LoadModule authn_anon_module modules/mod_authn_anon.so
LoadModule authn_dbm_module modules/mod_authn_dbm.so
LoadModule authn_default_module modules/mod_authn_default.so
LoadModule authn_host_module modules/mod_authn_host.so
LoadModule authz_user_module modules/mod_authz_user.so
LoadModule authz_owner_module modules/mod_authz_owner.so
```

```
Include conf.d/*.conf
```

```
User apache
Group apache
ServerAdmin root@localhost
UseCanonicalName Off
DocumentRoot "/var/www/html/"
```

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>

<Directory "/var/www/html/">
    Options Indexes FollowSymLinks
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

```
<IfModule mod_userdir.c>
    UserDir disabled
</IfModule>
```

```
DirectoryIndex index.html index.html.var
AccessFileName .htaccess
```

```
<IfModule mod_mime_magic.c>
    # MIMEMagicFile /usr/share/magic/mime
    MIMEMagicFile conf/magic
</IfModule>
```

```
HostnameLookups Off
ErrorLog logs/error_log
LogLevel warn
CustomLog logs/access_log combined
ServerSignature On
Alias /icons/ "/var/www/icons/"
```

```
<Directory "/var/www/icons/">
```

# 390 第 16 章 .在 Red Hat Enterprise Linux 上配置 Apache

```
Options Indexes MultiViews FollowSymLinks
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

```
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/"
<Directory "/var/www/cgi-bin/">
AllowOverride None
Options None
Order allow, deny
Allow from all
</Directory>
```
