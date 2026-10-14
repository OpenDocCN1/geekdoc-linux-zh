
```
user www-data;
worker_processes 1;

# error_log /var/log/nginx/error.log;

events {
    worker_connections 1024;
}
```

# 配置 Nginx 服务器

```http
http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    access_log /var/log/nginx/access.log;

    sendfile on;

    tcp_nopush on;
    #tcp_nodelay on;

    #keepalive_timeout 0;
    keepalive_timeout 65;

    gzip on;

    include /etc/nginx/sites-enabled/*;
}
```

`nginx.conf` 文件包含以下部分：

- `user processes`（用户进程）——你用于运行 Nginx 的系统用户。默认是 `www-data`。你可以通过插入第二个条目来向设置中添加一个组：

  `user www-data;`

- `worker processes`（工作进程）——允许你设置 Nginx 在服务器上启动多少个进程。对于大多数用户来说，默认值 `1` 就足够了，尽管有些人建议将其设置为 `4`。你可以进行尝试，但要要谨慎。

- `error_log`（错误日志）——在本示例中该行被注释掉了。如果你不想使用默认的日志位置，可以通过删除标记该行作为 Nginx 不处理的注释的 `#` 号并调整目录位置来设置错误日志的位置。

- `events` and `worker_connections`（事件与工作连接）——这些设置调整了 Nginx 每个进程允许的并发连接数。这样想可能有所帮助：`worker_connections` 乘以 `worker_processes` 将得到连接到你服务器的最大客户端数量。内存是你的服务器是否能够实际处理你配置的所有允许连接的因素，如果你不确定服务器是否有足够的内存支持更高的数值，请保持两个设置为默认值，这样就可以了。

- `http`——此部分包含 HTTP 访问的基础设置：

除非你喜欢尝试找出为什么内容没有显示，或者你知道必须调整允许的内容类型，否则请保持 `include` 和 `default_type` 行不变。

你可以随意调整 `access_log` 的位置，它记录了所有尝试连接服务器的操作，或者注释掉该行来禁用它。

当你允许 Nginx 忽略其正在发送的文件内容时，就会 `sendfile`。这在提供不需要多次请求确认的大文件时有用，从而释放系统资源给需要 Nginx 监控的项目。除非你明确为什么要关闭它，否则建议保留此设置，因为它可以节省提供图形等内容时的资源。

`tcp_nopush` 在一个数据包中发送 HTTP 响应头，这实际上是件很好的事情，尝试使用它是可以的。

`tcp_nodelay` 用于不需要响应的项目，但大多数通用 Web 使用都需要响应，因此这通常最好被注释掉，尽管尝试看看在你的情况下是否会产生差异也是可以的。

`keepalive_timeout` 设置了发送请求时 Nginx 保持连接打开的秒数。默认保持连接打开一分钟，如果你可用的连接数有限，这似乎有点奇怪，因为保持连接会导致在超时发生之前，另一个请求者无法使用该槽位。将其设置为 `2` 或 `3` 秒等低数值将允许在分钟内有更多的人连接。如果你提供的是流量很小的网站，那么流量并不重要。如果你有大量流量，使用较小的数值通常是一个好主意。

`gzip` 允许使用即时的 gzip 压缩，这可以使数据传输更快。

`include` 定义了位于 `nginx.conf` 文件之外的文件，供 Nginx 读取并用于其配置。你可以包含多个文件；只需为每个文件创建一个新行。我们的示例包含了一个指令，用于包含通常用于虚拟主机的目录中列出的所有内容，正如后面的“虚拟主机”部分所述。你可以在此处放置一个服务器变量并定义它（正如你将在“虚拟主机”部分将做的那样），而不是使用 `include`，但如果你有多个站点，为每个站点单独配置 Nginx 的工作方式是有用的，特别是当你有一个站点流量很大而另一个站点流量很小时。

每当你更改 `nginx.conf` 文件时，都必须重启 Nginx 重新加载配置以使更改生效，如下所示：

```
matthew@semour:-$ sudo systemctl start nginx
```

## 虚拟主机

有些人倾向于停止并启动它，也许是在其之间进行配置工作。这非常常见，因为过去 Nginx 有过不执行重启的习惯。根据我们的经验，糟糕的重置很少见，但使用这种方法可以消除任何疑问：

```
matthew@seymour:~ sudo systemctl stop nginx
matthew@seymour:~ sudo systemctl start nginx
```

Web 服务器提供的流行服务之一是托管虚拟域名。虚拟域名也称为虚拟主机，如果它是一台独立机器，它将是一个拥有自己域名的完整网站，但它与其他网站托管在同一台机器上。

Nginx 以简单的方式实现了这一功能：为你的虚拟主机创建一个配置文件，将其命名，并将其放在 `/etc/nginx/sites-available`。我们倾向于将文件放置在 `/etc/nginx/sites-available` 并在 `sites-enabled` 中创建符号链接，但并非强制。这样做允许你通过简单的删除符号链接并重新加载 Nginx 来禁用多个站点中的一个，同时保留该站点的完整配置，因此我们建议你尝试一下。

你可以将网站的文件放置在你喜欢的任何地方。配置详情告诉 Nginx 在何处找到它们。这里有一个虚拟主机的示例，我们将其称为 `yourdomain.com`：

```nginx
# 第服务器
server {
    listen 80;
    server_name yourdomain.com;
    root /home/<username>/public_html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

# 第二服务器
server {
    listen 80;
    server_name www.yourdomain.com;
    root /home/<username>/public_html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

## 第 26 章 Nginx 服务器管理

在本节的早些时候，我们提到过你可以放置网站文件。这里你需要检查你打算安装和使用的任何 PHP 应用程序的要求。

### 设置 PHP

如果你有 CGI 或其他脚本内容（例如用 PHP 编写的网站），你将需要更多工作。虽然 Nginx 默认提供了服务 PHP 的能力，但仍需要设置。在本节中，我们将添加服务 PHP 的能力。首先，你需要确保服务器上安装了 PHP。有很多方法可以实现。对于本示例，你可以使用 PHP-FPM，你可以在 https://php-fpm.org 了解更多。

安装以下包：`php7.4-cli`, `php7.4-cgi`, `phpm` 和 `php7.4-fpm`。

编辑文件 `/etc/php/fpm.d/www.conf` 使 `php-fpm` 使用 UNIX socket 而不是 TCP/IP 连接，找到此行：

```conf
listen = 127.0.0.1:9000
```

将其替换为：

```conf
listen = /tmp/php-fpm.sock
```

接下来，你需要编辑 `/etc/nginx/nginx.conf` 或早期示例中的虚拟主机文件 `/etc/nginx/sites-enabled/yourdomain.com`，以包含 Nginx 能够处理 PHP 内容的信息。编辑任何一个都可以的；区别在于编辑虚拟主机将只影响该网站，而编辑 `nginx.conf` 将影响你服务器上的所有内容。

```nginx
#if a server request is made without www, this next line will rewrite it
rewrite ^/(.*) http://yourdomain.com/$1 permanent;
}
```
