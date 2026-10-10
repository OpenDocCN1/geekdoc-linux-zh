
```
<VirtualHost {IP address/hostname}:port number>

ServerAdmin {User name}@{Domain name}

DocumentRoot {DocumentRoot location}

ServerName {IP address/FQDN}

ErrorLog (Path of the error log file)

CustomLog (Path of the access log file) (Log level)

</VirtualHost>
```

- 5. 保存并关闭文件。
- 6. 输入 `service httpd configtest` 以检查 `httpd.conf` 文件是否配置正确。
- 7. 输入 `service httpd restart` 以重启 `httpd` 服务。

### 操作参考：限制用户访问

要限制用户访问：

- 1. 以 `root` 用户身份登录。
- 2. 使用 `vi` 编辑器打开 `/etc/httpd/conf/httpd.conf` 文件。
- 3. 添加一个 `Directory` 语句以拒绝来自特定域的访问。

```
<Directory "location of web pages">

Order deny,allow

Deny from {domain name} | {IP address}

</Directory>
```

![](img/477ccb2f05b6ba1b2d563ea74f18c197_649_0.png)

- 4. 保存并关闭文件。
- 5. 输入 `service httpd configtest` 以检查 `httpd.conf` 文件是否配置正确。
- 6. 输入 `service httpd restart` 以重启 `httpd` 服务，使配置更改生效。
- 7. 以被拒绝域中的用户身份登录。
- 8. 验证访问托管在 Web 服务器上的网站时，您被拒绝访问。

### 操作参考：身份验证用户以访问网站

要身份验证用户以访问网站：

- 1. 以 `root` 用户身份登录。
- 2. 使用 `vi` 编辑器打开 `/etc/httpd/conf/httpd.conf` 文件。
- 3. 添加一个 `Directory` 语句以调节对网站的访问。

```
<Directory "Location of the html page">

{
AllowOverride AuthConfig
}

</Directory>
```
