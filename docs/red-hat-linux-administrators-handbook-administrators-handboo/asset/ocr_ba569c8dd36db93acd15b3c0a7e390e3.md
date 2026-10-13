tory container. For example, the following configuration defines a caching proxy server that writes cache files to the /www/cache directory:

```
<Directory proxy:*>
CacheRoot /www/cache
CacheSize 1024
CacheMaxExpire 24
</Directory>
```

It is permitted to write 1,024K of data (1MB), and the cache must expire after each day (24 hours).

To prevent outside people from abusing your proxy, you can restrict proxy access either by host or by username/password authentication.

To control which hosts have access to the proxy server, create a configuration such as the following, which denies access to all but myhost.nitec.com:

```
<Directory proxy:*>
AuthType Basic
AuthName Proxy
order deny,allow
deny from all
allow from myhost.nitec.com
</Directory>
```

If you want to use username/password authentication, you can use something similar to the following:

```
<Directory proxy:*>
AuthType Basic
AuthName Proxy
AuthUserFile /path/to/proxy/.htpasswd
AuthName Proxy
require valid-user
</Directory>
```

Create the .htpasswd file by using the htpasswd utility that comes with Apache.