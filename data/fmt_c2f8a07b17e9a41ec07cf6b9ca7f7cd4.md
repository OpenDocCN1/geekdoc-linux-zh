
谷歌 Chrome 浏览器提供了一个名为“复制为 curl”的功能，它可以创建一个 `curl` 命令来模拟浏览器的行为，包括头部、cookie 以及细节。你可以轻松地通过各种调整重试请求，并看到与浏览器完全的结果。（在开发者工具面板的网络选项卡中右键点击资源名称即可发现此选项。）

# TCP 连接复用

TCP 连接是昂贵的。除了维护它们所需的内存外，建立每个新连接的三次握手会在 HTTP 请求甚至开始之前增加一次完整的往返延迟。

HTTP Archive 是一个跟踪网络统计的项目，估计平均网站每个页面加载请求 99 个资源。如果每个资源都需要新的 TCP 连接，互联网的性能将是灾难性的。这在互联网早期确实如此。

原始 HTTP/1.0 规范没有包含任何连接复用的规定，但一些勇敢的开发者作为扩展添加了实验性支持。`Connection: Keep-Alive` 头部被添加到客户端和服务器中，然后在 HTTP/1.1 中改进并成为默认值。有了 keep-alive，

- 4. TCP 快速打开 (`TFO`) 是一种提案，旨在通过在初始 SYN 包中发送数据来减少延迟。参见 `RFC 7413`。

# HTTP: 超文本协议

表 19.3 绝不是一个确定的列表。事实上，事务的双方都可以包含它们想要的任何头部信息。双方必须忽略它们不理解的头部信息。²

头部与消息正文之间用空行隔开。对于请求，正文可以包含参数（用于 POST 或 PUT 请求）或要上传的文件内容。对于响应，消息正文是所请求内容的负载（例如，HTML、图像数据或查询结果）。消息正文并不一定是人类可读的，因为它可能包含图像或其他二进制数据。正文可以是空的，例如 GET 请求或大多数错误响应。

# 第19 章 网络托管

一种可能性是定义虚拟网络接口，有效地允许多个 IP 地址绑定到单个物理。大多数系统允许这样做，并且运行良好，该方案非常繁琐，且需要在多个层进行管理。

更好的解决方案，虚拟主机，由 HTTP 1.1 提供。该方案定义了一个用户代理设置头部以指示它们尝试连接的内容。服务器检查头部并采取相应的行为。这节省了 IP 地址并简化了管理，特别是对于在单个物理上有数百或数千个网站的站点。

`/1.1` 要求用户代理提供 `Host` 头部，因此虚拟主机现在是处理多个的标准方法。

解决方案是 `SNI`，服务器名称指示，当客户端在初始 TLS 连接消息中提交它正在请求的主机时。现代服务器和客户端都自动处理 `SNI`。

## 19.1 虚拟主机

虚拟主机允许在单个 Web 服务器上托管多个网站。有三种主要的实现虚拟主机的方法：

1. 基于 IP 的虚拟主机：为每个网站分配不同的 IP 地址。这种方法会浪费 IP 地址资源。
2. 基于端口的虚拟主机：为每个网站分配不同的端口（例如 80 和 8080）。这种方法对用户来说不方便。
3. 基于头部的虚拟主机：这是最常见的方法，使用 HTTP 头部来区分不同的网站。

## 19.2 配置虚拟主机

我们将使用 Apache 来配置虚拟主机。Apache 使用“虚拟主机”（Virtual Hosts）文件来定义这些主机。

```
# /etc/apache2/sites-available/example-vhost.conf

<VirtualHost *:80>

    ServerName example.com

    DocumentRoot /var/www/example

</VirtualHost>

<VirtualHost *:80>

    ServerName www.example.com

    DocumentRoot /var/www/www

</VirtualHost>
```

配置完成后，我们需要使用 `a2ite` 命令来启用虚拟主机，并重启 Apache。

```bash
sudo a2ensite-vhost.conf
sudo systemctl restart apache2
```

## 19.3 使用 HTTPS 虚拟主机

为了安全，我们应该使用 HTTPS 托管网站。我们将使用 SSL 证书来配置 HTTPS 虚拟主机。

```apache
# /etc/apache2/sites-available/example-ssl.conf

<VirtualHost *:443>

    ServerName example.com

    DocumentRoot /var/www/example

    SSLEertificateFile /etc/ssl/certs/example.crt

    SSLCertificateKeyFile /etc/ssl/private/example.key

</VirtualHost>
```
