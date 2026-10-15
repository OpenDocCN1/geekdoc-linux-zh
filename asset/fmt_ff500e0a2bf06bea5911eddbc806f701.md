
只有通过密码认证才能使你的 `Web` 服务器漏洞变得有意义。例如，如果你的网站是 `WordPress` CMS，管理页面密码可能被绕过。你可以将管理页面访问限制为你的 `IP` 或管理员的 `IP`。要执行此操作，打开 `Nginx` 配置文件并更新 `server` 块：

```bash
sudo nano /etc/nginx/sites-enabled/default
server {
    location /wp-admin/ {
        allow 10.2.74.45/24;
        allow 10.0.0.1/24;
        deny all;
    }
}
```

`www.linuxuser.com` 39

# Nginx 教程

在 `allow` 参数下（下文所示）的所有 `IP` 都可以访问管理页面，对于任何其他 `IP`，管理页面的访问将被锁定。`/24` 是子网掩码，您需要根据服务器配置数据对其进行更新。现在，重新加载 `Nginx` 服务器：

要启用 `NAXSI`，编辑 `nginx.conf` 并取消 `http` 部分中包含 `naxi_core.rules` 文件的注释：

```bash
$ sudo service nginx reload
```

```bash
$ sudo nano /etc/nginx/nginx.conf
http {
    nginx-naxi config
    ##
    # 如果安装了 naxi，请取消注释
    ##
    naxi include /etc/nginx/naxi_core.rules;
}
```

如果你使用任何其他 `IP` 访问 `Web`，将触发 `403` 错误：

# 06 安全审计

你可以使用安全审计工具独立扫描漏洞。有很多工具可以选择，但此处我们将使用 `Wapiti`。安装此 `Web` 漏洞扫描器：

```bash
$ sudo apt-get install wapiti
```

现在使用 `wapiti` 运行扫描：

在我们的示例中，`http://example.com` 是网站，`10` 表示限制具有相同模式的 `URL` 扫描数量为 `10` 以避免无限循环。将扫描范围限制为特定域名。

扫描结果创建在生成的 `generated-report` 目录中，该目录位于执行 `wapiti` 文件夹的位置。报告按漏洞类型分类：`SQL` 注入、绑定注入、处理等、跨站脚本、`CRLF`、资源消耗、请求头绕过、备份文件和潜在危险。

```bash
$ wapiti --http=example.com -n 10 -b folder
```

```bash
$ sudo nano /etc/nginx/naxi_core.rules
SecRulesEnabled:
#SecRulesDisabled:
DeniedUrl $1=".html";

# 检查规则
CheckRule($SQL= 8);
```

接下来更新 `NGINX` 配置文件中的 `server`：

```bash
$ sudo nano /etc/nginx/sites-enabled/default
location / {
    # 取消注释以在此位置启用 naxi
    include /etc/nginx/naxi.rules;
}
```

重新加载服务器。如果你想更新规则，请编辑 `naxi_core.rules` 文件中的主规则：

```bash
$ sudo service nginx reload
```

# 08 用于 NGINX 服务器的 Fail2ban

`Fail2ban` 防止恶意用户和机器人的攻击。该程序通过动态修改监狱策略（`jail policy`）来封禁 `IP` 地址。安装 `fail2ban` 的命令：

```bash
$ sudo apt-get update
sudo apt-get install fail2ban
```

当 `fail2ban` 在监控时检测到，`jail.conf` 文件会有条目。为了防止此文件在更新期间丢失，请执行：

```bash
$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

# 07 用于 NGINX 服务器的 NAXSI

`NAXSI` 是一个第三方模块，可以保护你的 `Web` 服务器免受各种攻击。从其发布页面下载 `NAXSI` 软件包，然后：

```bash
$ sudo dpkg -i nginx-naxi_1.1.19-ubuntu0.7amd64.deb
```

或者，从 `Ubuntu` 软件包列表中安装：

```bash
$ sudo apt-get update
$ sudo apt-get install nginx-naxi
```

![](img/a6a91935f07f13d62210d3016f91c5fc_39_0.png)

# NASXI 是一个第三方防火墙模块，可以保护你的 Web 服务器免受各种攻击

```ini
[DEFAULT]
ignore = 127.0.0.1/8 10.214.75/24
bantime = 3600
dime = 3600 # 这些行结合封禁失败的客户端
maxretry = 6 # 在半小时内认证 6 次
mta = mail
destmail = example@email.com
enail = Fail2BanAlert
```

```ini
## enabled = true
## logpath(fail) 页面获取更多信息
## action = 'connect and -' (后跟空格) 用于过滤
filter = nginx-distro-conf
## 攻击选项的全局定义。你可以激活它
```

```ini
log = /var/log/nginx/access.log
maxretry = 2
```

现在为新创建的监狱创建过滤器。进入过滤器目录：

```bash
cd /etc/fail2ban/filter
```

在此处为示例监狱创建文件：例如 `nginx-badbots.conf`、`nginx-nproxy.conf` 等，用于坏机器人配置，例如之后也用于 `Apache` 和其他服务的相同文件。

将你的 `IP` 地址连带子网掩码添加到 `ignoreip` 参数中。根据所需的封禁时间更新 `bantime`。`insta mta` 启用邮件发送操作，并通过邮件客户端和发送者保护 `mta`。

## 09 Fail2ban 配置

接下来，使用 `/etc/fail2ban/jail.local` 监控你的 `Web` 服务器日志中的特定模式。默认情况下仅启用了 `jail`。如果你想监控登录尝试，找到 `[nginx-http-auth]` 监狱并启用它：

```ini
[nginx-http-auth]
enabled = true
filter = nginx-http-auth
```

可以创建自定义监狱，例如用于存储恶意请求模式：

```ini
[nginx-badbots]
enabled = true
port = http_https
logpath = /var/log/nginx/access.log
maxretry = 2
```

要使用你的 `nginx` 服务器作为开放代理封禁客户端，创建一个监狱：

```ini
[nginx-nproxy]
enabled = true
port = http_https
filter = nginx-proxy
```

# Diffie-Hellman 参数

在创建自签名证书后，可以生成 `4096` 位 `DH` 参数：

```bash
$ openssl dhparam -out /etc/nginx/dhparam.pem 4096
```

在 `/etc/nginx/nginx.conf` 的 `NGINX` 配置文件中更新 `server` 块：

```nginx
server {
    server_name localhost;

    ### SSL 部分
    listen 443 ssl;
    ssl_certificate /etc/nginx/ssl.crt;
    ssl_certificate_key /etc/nginx/ssl.key;

    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256; 
    ssl_dhparam /etc/nginx/dhparam.pem;
}
```

重新加载服务器。如果你想更新规则，请编辑 `naxi_core.rules` 文件中的主规则：

```bash
$ sudo service nginx reload
```

最后，将使用分析工具（例如在线服务 `http://www.ssllabs.com/`）测试你的 `SSL` 配置。

# SuExec 教程

# 使用 SuExec 管理权限

`SuExec` 提高了安全性并允许 `Apache` 以原始用户运行 `CGI` 脚本

![](img/a6a91935f07f13d62210d3016f91c5fc_41_0.png)

# Hello, World.
