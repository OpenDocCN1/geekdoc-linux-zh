
在此处，流往 `admin.com` 和 `www.admin.com` 的流量将以轮询（默认方式）分发到 `web1` 和 `web2` 服务器。

此配置还为后端服务器设置了健康检查。每 30 秒（`interval=30`）会在 `/health_check` 端点（`uri=/health_check`）对每个服务器进行一次检查。如果健康检查连续三次尝试失败（`fails=3`），NGINX 将将服务器标记为下线，但如果成功一次（`passes=1`），则会将服务器加回轮询。

`match` 关键字是 NGINX 特有的。它规定了健康检查被认为成功的条件。在这种情况下，NGINX 必须接收到 200 响应码，Content-Type 头部必须设置为 `text/html`，且响应体必须包含 "Red Leader, Standing By" 短语。

我们在 `upstream connect` 内部添加了一个额外条件，将最大连接尝试失败次数设置为二。这意味着，如果 NGINX 在两次尝试内完全无法连接到服务器，它将放弃并将服务器从池中移除。这是一种加性连接检查，补充了 `health_check` 子句中更具结构化的检查。

# 第19 章 Web 托管

## 19.6 HAProxy

HAProxy 是最广泛使用的开源负载均衡软件。它代理 HTTP 和 TCP，支持会话保持（sticky sessions）将给定客户端固定到特定的 Web 服务器，并提供高级的健康检查功能。最新版本还支持 TLS、IPv6 和 HTTP 压缩。对 HTTP/2 的支持进行中，预计将在 HAProxy 1.7 版本迅速成熟。

HAProxy 的配置通常包含在一个文件 `haproxy.cfg` 中。这是因为操作系统供应商通常不会将事情复杂化，而是采用项目建议的默认目录结构。

在 Debian 和 RHEL 系统上，配置位于 `/etc/happroxy/happroxy.cfg`。FreeBSD 不提供默认配置，因为负载均衡对其来说没有意义；它完全取决于你的设置。在安装 HAProxy 软件包后，你可以在 FreeBSD 的 `/usr/local/share/examples/happroxy` 找到示例配置。

以下示例配置将 HAProxy 设置为监听 80 端口，并以轮方式在 8080 端口上的两个 Web 服务器（`web1` 和 `web2`）之间分配请求。

```
global

  daemon

    maxconn 5000

default

  mode http

    timeout connect 5000 # 毫秒

    timeout client 10000

    timeout server 10000

frontend http-in

  bind *:80

  default_backend webservers

backend webservers

  balance roundrobin

  server web1 10.0.0.10:8080

  server web2 10.0.0.11:8080
```

此示例引入了 HAProxy 的 `frontend` 和 `backend` 关键字，如图 G 所示。

`frontend` 规定了 HAProxy 如何接收来自客户端的请求：使用的地址和端口、服务的流量类型以及面向客户端的考虑因素。`backend` 配置处理请求的服务器集合。多个 `frontend`/`backend` 对的存在允许 HAProxy 服务多个站点。`timeout` 设置允许精细控制在尝试打开服务器新连接时等待的时间，以及连接建立后保持多久。对于繁忙的服务器很重要。在本地网络中，`timeout connect` 值可以很低，因为新连接应该快速建立。

# 健康检查

尽管之前的配置提供了基本功能，但它并没有检查下游服务器的状态。如果 `web1` 或 `web2` 离线，入站请求将开始失败。HAProxy 的 `status-check` 功能通过执行常规 HTTP 请求来确定每个服务器的健康状况。只要服务器响应 HTTP 200 ，它们就保持运行并继续接收负载均衡器的请求。如果服务器状态检查失败（返回非 200），则 HAProxy 将其从池中移除。然而，HAProxy 继续对服务器执行健康检查。如果它再次响应，HAProxy 将将其返回池。

健康检查的细节

```
backend webservers

balance roundrobin

option httpchk GET /

server web1 10.0.0.10:8080 check inter 30s

server web2 10.0.0.11:8080 check inter 30s
```

可以放心的是，良好的应用程序通常暴露一个健康检查端点以确定其真实健康状况。如果可用，可以使用更复杂的检查。

# 服务器统计

HAProxy 提供了一个方便的 Web 界面显示服务器统计，类似于 Apache 的 `mod_status`。HAProxy 版本显示池中每个服务器的状态，并允许按需要手动启用和禁用服务器。

语法非常简单：

```
listen stats :8000

mode http

stats enable

stats hide

stats auth mypass
```

# 会话保持

HAProxy 使用 Cookie 确保客户端路由到相同的后端服务器。这对于在服务器上本地维护会话的应用程序特别有用。HAProxy 有几种方法实现会话保持，包括基于 Cookie 和基于 IP 方法。

常用的方法是使用 Cookie。HAProxy 可以向客户端插入会话 Cookie。客户端在所有后续请求中包含此 Cookie，HAProxy 使用它将请求路由到正确的后端。以下示例显示了如何使用 Cookie 配置会话保持：

```
backend webservers

  balance roundrobin

  cookie SERVERID insert track

  server web1 10.0.0.10:8080 cookie SERVERID=1

  server web2 10.0.0.11:8080 cookie SERVERID=2
```

在此示例中，`cookie` 指令告诉 HAProxy 在响应中插入名为 `SERVERID` 的 Cookie。`insert` 选项指定如果 Cookie 不存在则添加它。`track` 选项告诉 HAProxy 使用 Cookie 路由请求。每个服务器分配一个唯一的 `SERVERID` Cookie 值。

另一种实现会话保持的方法是使用客户端的 IP 地址。这对于客户端不支持 Cookie（例如某些移动设备或旧留系统）的情况有用。

```
backend webservers

  balance ip

  server web1 10.0.0.10:8080

  server web2 10.0.0.11:8080
```

然而，如果多个客户端位于同一个 NAT 网关后，基于 IP 的会话保持可能无效，因为它们共享相同的 IP 地址并路由到同一个服务器。

# TLS 终止

HAProxy 1.5 及更高版本包含 TLS 支持。常见的配置是在 HAProxy 服务器终止 TLS，并通过 HTTP 与后端服务器通信。这种方法减轻了后端服务器的加密开销，并减少了需要私密钥的系统数量。

对于对安全特别敏感的站点，也可以从 HAProxy 使用 HTTPS 到后端服务器。可以使用相同的 TLS 证书或另一个；无论哪，你都需要在代理处终止并重新启动 TLS。

由于 HAProxy 终止客户端的 TLS 连接，你需要在 `frontend` 中添加相关配置。

```
frontend https-in own  bind *:443 ssl crt /etc/ssl/private/admin.com.pem

  backend webservers
```

Apache 和 NGINX 要求私钥和证书为 PEM 格式的单独文件，但 HAProxy 期望这两个组件存在于同一个文件中。你可以简单地合并文件来创建一个复合文件：

```
# cat /etc/ssl/private/admin.com.key /etc/ssl/certs/admin.com.crt > /etc/ssl/private/admin.com.pem

# chmod 400 /etc/ssl/private/admin.com.pem

# ls -l /etc/ssl/private/admin.com.pem

-r-------- 1 root root 3688 Jun 18 17:46 /etc/ssl/private/admin.com.pem
```
