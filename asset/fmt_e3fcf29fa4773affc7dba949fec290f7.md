
```
  root /var/www/admin.com;

}

}

}
```

最外层的上下文（称为 `main`）是隐式的，用于配置核心功能。`events` 和 `http` 上下文位于 `main` 内部。`events` 是一个必需的上下文，用于配置连接处理。由于在本示例中它是空的，因此隐含了默认值。幸运的是，这些默认值是合理的：

- 运行一个工作进程（使用非特权用户账户）。
- 如果启动，则监听 80 端口，否则监听 8000 端口。
- 将日志写入 `/var/log/nginx`（编译时选择）。

`http` 上下文包含所有与 Web 和 HTTP 代理服务相关的指令。定义虚拟主机的 `server` 上下文嵌套在 `http` 内部。`http` 中的多个 `server` 上下文可以配置多个虚拟主机。

别名（Aliases）可以包含在 `server_name` 中，将 Host 头与一组子域名匹配：

```
http {

server {

  server_name admin.com www.admin.com;

  root /var/www/admin.com;

}

server {

  server_name example.com www.example.com;

  root /var/www/example.com;

}

}
```

`server_name` 的值也可以是正则表达式，匹配结果甚至可以捕获并命名为变量，供后续配置使用。通过使用此功能，你可以重构之前的配置为：

```
http {

server {

  server_name ^(www\.)?((?<domain>(example|admin).com);

  root /var/www/$/domain;

}

}
```

以波浪号（`~`）开头的正则表达式匹配 `example.com` 或 `admin.com`，前面可选的 `www.`。匹配到的域的值存储在 `$domain` 变量中，然后用于确定选择哪个服务器根目录.¹18

基于名的虚拟主机可以通过 `listen` 和 `server_name` 指令共同与基于 IP 的主机区分来。

```
server {

    listen 10.0.0.10:80

    server_name admin.com www.admin.com;

    root /var/www/admin.com/site1;

}

server {

    listen 10.0.0.11:80

    server_name admin.com www.admin.com;

    root /var/www/admin.com/site2;

}
```

此配置显示了从不同的 Web 根提供的两个版本的 `admin.com`。接收请求的接口的 IP 地址决定了用户看到的站点版本。

`root` 是存储虚拟主机的 HTML、图像、样式表、脚本和其他文件的基础目录。默认情况下，NGINX 直接从根目录提供服务，但你可以使用 `location` 指令进行更复杂的请求路由。如果路径未匹配，NGINX 将回退到根目录。

以下示例使用了 `location` 指令结合 `proxy_pass` 指令，NGINX 从根目录提供服务。

```
server {

    server_name admin.com www.admin.com;

    root /var/www/admin.com;

    location /nginx/

        proxy_pass http://nginx.org/;

}
```

`location` 可以使用正则表达式根据请求的内容路由到不同的源。NGINX 文档

* 18 注意，这种语法的使用会使 NGINX 对每个 HTTP 请求执行正则表达式。我们在此使用是为了演示 NGINX 的灵活性，但在实践中你会列出所有的加密套件。

# 第19 章 Web Hosting

分析 `server_name`、`listen` 和 `location` 指令如何路由请求。

发行版中的常见模式是在全局 `http` 上文中设置许多指令的默认值，然后使用 `include` 指令将站点虚拟主机添加到配置中。例如，Ubuntu 的默认 `nginx.conf` 包含了：

```
include /etc/nginx/conf.d/;
```

# 为 NGINX 配置 TLS

尽管 `nginx` 并没有借鉴 Apache 的配置风格，但其 TLS 配置是一个异常相似的区域。与 Apache 一样，配置键都指向 SSL（TLS 的早期名称）。

启用 TLS 并指向证书和私钥如下：

```
server {

  listen 443;

  ssl:

    ssl_certificate /etc/ssl/certs/admin.com.crt;

    ssl_certificate_key /etc/ssl/v1.1/private/admin.com.crt;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE...

    ssl_prefer_server_ciphers on;

  server_name admin.www.com;

  root /var/www/admin.com/site1;

}
```

应仅启用 TLS 协议（而不是旧的 SSL 版本）；所有 SSL 协议已被弃用。证书和密钥的权限应该遵循 Apache TLS 部分第702页的建议。

使用 `ssl_ciphers` 指令要求强加密套件并削弱加密算法。`ssl_prefer_server_ciphers` 选项结合 `ssl_ciphers` 使 `nginx` 从服务器列表而不是客户端列表中选择；否则客户端可以建议任何它喜欢的加密算法。

# 使用 NGINX 进行负载均衡

除了作为 Web 和缓存服务器外，NGINX 还是一个出色的负载均衡器。它的配置风格灵活但不直直观。

使用 `upstream` 模块可以创建命名的服务器组。例如，以下语句将 `admin-servers` 定义为包含两个服务器的集合：

```
upstream admin-servers {
```

- `server` `web1.admin.com:8080` `max_fails=2`;
- `server` `web2.admin.com:8080` `max_fails=2`;

```
}
```

`upstream` 组可以在虚拟主机定义中引用。特别是，它们可以像主机名一样作为代理目标：

```
http {

server {

    server_name admin.com www.admin.com;

    location / {

        proxy_pass http://admin-servers;

        health_check interval=30 fails=3 uri=/health_check

        match=admin-health # 原文件中未拆分行

    }

}

match admin-health {

    status 200;

    header Content-Type = text/html;

    body ~ "Red Leader, Standing By";

}
```
