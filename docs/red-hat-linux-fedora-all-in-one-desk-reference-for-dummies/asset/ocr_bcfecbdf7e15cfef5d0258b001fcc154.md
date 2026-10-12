Here is a typical example of a <VirtualHost> directive that sets up the virtual host www.lnbsoft.com:

```
<VirtualHost www.lnbsoft.com>
    DocumentRoot /home/naba/httpd/htdocs
    ServerName www.lnbsoft.com
    ServerAdmin webmaster@lnbsoft.com
    ScriptAlias /cgi-bin/ /home/naba/httpd/cgi-bin/
    ErrorLog /home/naba/httpd/logs/error_log
    CustomLog /home/naba/httpd/logs/access_log common
</VirtualHost>
```

Here the name common in the CustomLog directive refers to the name of a format defined earlier in the httpd.conf file by the LogFormat directive, as follows:

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

This format string for the log produces lines in the log file looks like this:

```
dial236.dc.psn.net - - [13/Jul/2003:18:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

The format string contains two letter tokens that start with a percent sign (%). The meaning of these tokens is shown in Table 2-1.

Table 2-1 LogFormat Tokens

| Token | Meaning |
|-------|---------|
| %b | The number of bytes sent to the client, excluding header information |
| %h | The host name of the client machine |
| %l | The identity of the user, if available |
| %r | The HTTP request from the client (for example, GET / HTTP/1.0) |
| %s | The server response code from the Web server |
| %t | The current local date and time |
| %u | The user name the user supplies (only when access control rules require user name/password authentication) |