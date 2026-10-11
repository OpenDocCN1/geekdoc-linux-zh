
## 需求概述

- 锁定密码。
- 告诉 `nginx`，任何在 `443` 端口设置时输入用户/密码的人都可以查看 `5000` 端口的 `Frigate`。

## 为 Frigate 使用用户名/密码身份验证

- 使用 `iptables` 允许来自 `127.0.0.1` 到 `5000` 端口的所有流量，以便 `nginx` 能够连接到 `Frigate`。
- 允许来自 `192.168.5.4` 的所有流量连接到 `5000` 端口的 `Frigate`。
- 阻止 `5000` 端口上的其他所有流量。
- 在 `443` 端口设置 `nginx` 并使用 `https`。
- 告诉 `nginx`，访问 `nginx` web 服务器的用户需要提交用户名和密码才能进入。
- 锁定密码。

## 6.1 安装 nginx

1. 安装 `nginx`：
   - `sudo apt update`
   - `sudo apt install nginx`

2. 运行以下命令：

创建自签名证书：

```bash
openssl req -x509 -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-signed.key -out /etc/ssl/certs/nginx-signed.crt
```

> 注意：对于通用名称 `CN`，使用你的本地域名。

3. Strong Diffie-Hellman：

```bash
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

4. 创建 Basic 密码：

```bash
sudo apt install apache2-utils
sudo htpasswd -c /etc/nginx/.htpassword username
```

## 6.2 配置 nginx

创建一个 `nginx` 配置文件：

```bash
sudo nano /etc/nginx/sites-available/frigate
```

如果此目录不存在，你可能在使用较新版本的 `nginx`，它使用 `/etc/nginx/conf.d`。

添加以下配置：记得将 `happycloud.home.arpa` 和 `192.168.5.2` 替换为你的主机名和 IP 地址：
