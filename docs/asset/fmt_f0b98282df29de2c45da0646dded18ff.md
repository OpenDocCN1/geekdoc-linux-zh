
Cherokee 服务器会将 HTTP 请求的 Host 与虚拟服务器名称进行比较，如果找到匹配（例如，虚拟服务器的名称为 `webserver.dynu.com`），则由特定的虚拟服务器处理该请求。

尽管如此，当使用端口转发 DDNS 服务时，之前的事件序列不会发生，所有的客户端-服务器消息都将路由到 DDNS 服务提供者的端口转发服务。当 DDNS 服务接收到已启用端口转发的域名请求时，DDNS 服务将用其自身的端口转发服务器 IP 地址进行响应，而不是 Cherokee 服务器前端路由器的公 IP 地址。当端口转发服务器接收到客户端的 HTTP 请求时，端口转发会将客户端重定向到 Cherokee 服务器前端路由器的公 IP 地址发送新的 HTTP 连接，而不是默认端口号 80（即你的服务器监听的端口，例如端口 8080）。端口转发服务器会修改 HTTP 连接请求中 Host 的域名（例如，将从 `webserver.dynu.com` 变为 `<router's-public-ip-address:8080>`）。端口和域名都必须先在 DDNS 服务提供者处注册（这在第 6 章中已完成）。

为了说明这一事件序列，我们将查看初始的 HTTP 请求（来自客户端系统）以及 Web 服务器接收到的 HTTP 请求。我们将查看两种情况：启用端口转发和禁用端口转发。我们将检查 HTTP 协议的标头，并将使用在线网络工具 HTTP Viewer：

`http://www.rexswain.com/httpviewer.html`

另一个提供类似服务的网站是 `http://web-sniffer.net`。让我们先看禁用 DDNS 端口转发服务的情况。在 HTTP Viewer 服务器网站的 URL 字段中：

`http://webserver.dynu.com:8080`

![](img/5bf591327968a4c0190eb6adbf83042b_136_0.png)

点击 `Submit` 按钮后，出现以下页面：

![](img/5bf591327968a4c0190eb6adbf83042b_136_1.png)

以下是该页面提供的部分信息。它包含了 `rexswain.com` 对 `webserver.dynu.com:8080` 的请求，该请求解析路由器的公 IP 地址（87.202.110.63），并最终通过虚拟服务器路由器配置到达分配端口 8080 的服务器，即你的 Web 服务器。

```
GET / HTTP/1.1

Host: webserver.dynu.com:8080

User-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.336 (KHTML, like Gecko) Chrome/43.0.2357.65 Safari/537.36

Referer: http://www.rexswain.com/htptpview.html

Connection: close

Finding host ip...

Host IP address = 87.202.110.63

Finding TCP protocol...

Binding to local socket...

Connecting to host...

Sending request...

Waiting for response...

Receiving Header:
```

## 客户端请求中的 Host 字段为：

`http://webserver.dynu.com:8080`

网页还包括 Web 服务器对客户端（`rexswain.com`）的回复。这是一个 OK 类型的消息：

```
HTTP/1.1-200-OK(CR)(LF)

Connection:close(CR)(LF)

Date: Sun, 24-May-2015-04:38:37(CR)(LF)

Server: Cherokee/1.2.101 (UNIX)(CR)(LF)

Content-Length: 670(CR)(LF)

Content-Type: text/html(CR)(LF)

Expires: Tue, 01-Jan-1970-00:00:00+0000(CR)(LF)
```
注意 `(CR)` 和 `(LF)` 对应回车和换行符，作为 HTTP 字段的分隔符。

接下来，登录你的 DDNS 提供商管理网站并启用端口转发。返回 HTTP Viewer (`www.rexswain.com`) 并使用以下 URL：

```
http://webserver.com
```

由于启用了端口转发，不再给出端口号（8080）。结果如下所示：

![](img/5bf591327968a4c0190eb6adbf83042b_138_0.png)

### 以下是客户端到转发服务器的请求以及 rexswain.com 页面列出的服务器回复：

```
GET / HTTP/1.1

Host: webserver.dynu.com

User-Agent: Mozilla/5.0 (Windows NT 10.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.65 Safari/537.36

Referer: http://www.rexswain.com/httpview.html

Connection: close
```
- Host IP address = 173.208.132.91
- Finding TCP protocol...
- Binding to local socket...
- Connecting to host...
- Sending request...
- Waiting for response...

Receiving Header:

### 这次，客户端发送的 *Host* 为：

`http://webserver.dynu.com`

同时也列出了对应此 URL 的 IP 地址信息。该 IP 地址是 DDNS 服务提供者的端口转发服务器的 IP 地址：

Host IP address = 173.208.132.91

### 端口转发服务器回复以下消息：

```
HTTP/1.1:302-Object-moved(CR)(LF)

Date: Sat, 23-May-2015-05:58:19-GMT(CR)(LF)

Server: Dyn-Web-Server(CR)(LF)

X-Powered-By: Dyn-Dynamic-DNS-Service(CR)(LF)

Location: http://87.202.110.63:8080/(CR)(LF)

Content-Length: 145(CR)(LF)

Content-Type: text/html(CR)(LF)
```

之前是 `rexswain.com` 向 DDNS 提供的者的端口转发服务器发送连接请求。端口转发服务器使用“对象已移动”（Object Moved）消息将客户端重定向到 Web 服务器局域网路由的公网 IP 地址，端口为 8080，这正是被转发的端口。随后是另一个步骤，通过另一个连接请求让客户端（`rexswain.com`）连接路由器并最终连接 Web 服务器。从 `rexswain.com` 到 Web 服务器的连接是通过两个请求完成的。第二个连接请求消息也包含在 rexswain 的网页中：

```
GET / HTTP/1.1

Host: 87.202.110.63:8080

User-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.65 Safari/537.36

Referer: http://www.rexswain.com/httpview.html

Connection: close
```
- 正在查找 TCP 协议...
- 正在绑定到本地套接字...
- 正在连接到主机...
- 正在发送请求...
- 等待响应:...

接收到报头：

### Web 服务器的响应是 HTTP 消息 200 (OK)：

```
HTTP/1.1-200-OK(CR)(LF)

Connection: close(CR)(LF)

Date: Sun, 24-May-2015 03:58:46-GMT(CR)(LF)

Server: Cherokee/1.2.101 (UNIX)(CR)(LF)

Content-Length: 6708(CR)(LF)

Content-Type: text/html(CR)(LF)

Expires: Tue, 01-Jan-1970-00:00:00-GMT(CR)(LF)

(CR)(LF)
```

在禁用端口转发时，客户端消息中的 Host 字段对应服务器的域名。然而，在启用端口转发时，发送到服务器的第一个请求消息的 Host 字段虽然对应服务器的域名，但它会被重定向。随后的第二个连接请求消息将具有一个修改过的 Host 字段。

你也可以使用数据包嗅探器检查到达服务器计算机的客户端 HTTP 请求，数据包嗅探器是一种用于捕获和分析通过网络的数据包的程序。如果你没有数据包嗅探器，你需要安装 Wireshark。从你 Web 服务器的 Linux 终端上运行：

```
$ sudo apt-get install wireshark
```

安装完成后，在终端窗口中输入以下内容：

```
$ sudo wireshark
```
