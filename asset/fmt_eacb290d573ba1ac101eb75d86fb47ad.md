
```apache
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnulix.org
    AuthType Basic
    AuthName "Server status"
    AuthUserFile "gnulixusers"
    Require valid-user
    Satisfy Any
</Location>
```

```bash
matthew@seymour:~$ sudo a2en module_name
```

```bash
matthew@seymour:~$ sudo a2dis module_name
```

```html
Status: 301 永久重定向
Location: http://gnulix.org/newstuff/
Content-type: text/html

<html>
<HEAD>
<TITLE>我们移动了....</TITLE>
</HEAD>
<BODY>
<P>我们已经移动了旧内容，现在你可以在这里找到：</P>

<html>
我们已经移动了旧内容，现在你可以在这里找到：</p>
```

```bash
matthew@seymour:~$ openssl genrsa -des3 -out server.key 2048
```

```bash
matthew@seymour:-$ openssl req -new -key server.key -out server.csr
```

```bash
matthew@seymour:-$ openssl x509 -req -days 365 -in server.csr -signkey server.key -nout server.crt
```

```bash
matthew@seymour:~$ cp server.crt /etc/nginx/ssl/
```

```bash
matthew@seymour:~$ cp server.key /etc/nginx/ssl/
```

```nginx
server {
    listen 80; #设置提供网站服务的 HTTP 端口
    listen 443 ssl;
    server_name www.yourdomain.com; # 使用 www 前缀命名服务器
    ssl_certificate /etc/nginx/ssl/server.crt
    ssl_certificate /etc/nginx/ssl/server.key
    if 如果发起的请求是不带 www 的 www，下一行将对其重写
        rewrite "/(.*)" http://yourdomain.com/$1 permanent;
}
```

```bash
matthew@seymour:~$ dpkg --get-selections | grep ftp | sort

ftp install
lftp install
```

```text
ftp:x:116:124:ftp daemon,,:/srv/ftp:/bin/false
```

```bash
# cat /etc/shadow

bin*:11899:0:99999:7:::
daemon*:11899:0:99999:7:::
adm*:11899:0:99999:7:::
lp**:11899:0:99999:7:::
...
ftp**:12276:0:99999:7:::
..
```

```bash
matthew@seymour:-$ sudo service vsftpd status
```

```bash
matthew@seymour:~$ status vsftpd
```

```conf
# 允许匿名 FTP 吗？（默认禁用）
anonymous_enable=NO

#
# 注消注释以允许本地用户登录。
local_enable=YES
