
除非你拥有来自受信任第三方的证书，否则你的用户将获得与上述图 5.13 中相同的警告。除了看起来不专业之外，由于大型组织中不太可能所有用户都能分辨出由 IT 部门生成的合法密钥和由恶意第三方生成的密钥之间的区别，这也是一项实际风险。在这种情况下，你需要从受信任的第三方购买证书，例如 `GeoTrust`（被 Google 使用）、`DigiCert`、`Comodo`、`Thawte` 或 `VeriSign`（例如被 Facebook 使用）。对于其他情况，特别是当你想为自己使用 https（即保护你的管理面板）时，自签名证书就足够了。

### 5.4 下载文件

在这里你可以下载本教程中使用的配置文件：`ConfigFile.zip`

你还可以下载一个有用的 pdf 文件：`Openssl.pdf`

## 第 6 章

### Nginx Websockets 代理指南

#### 6.1 介绍

根据 `IETF`（互联网工程任务组）发布的 `RFC`（请求评论）`#6455`，`WebSocket` 是一种通过单个 `TCP` 连接提供全双工通信通道的协议，它旨在在 Web 浏览器和服务器中实现，但任何客户端或服务器应用程序都可以使用它。

与 `TCP` 一样，`WebSocket` 在低延迟连接中实现了全双工通信，但它与 `TCP` 的不同之处在于，它启用的是消息流而不是字节流。

换句话说，客户端和服务器之间存在持久连接，并且其中任何一方都可以在任何时间开始发送数据。因此，每当你需要客户端和服务器之间接近实时的连接时，无论是否在 Web 环境中，你都会想到使用 `WebSockets`。

请注意，`Nginx` 从 `1.3.13` 版本开始（2013 年 2 月发布）支持 `Websockets`，并且可以在核心产品中访问。旧版本不支持此协议。

在本教程中，我们还将配置 `Upstart`（Ubuntu 开发者编写的 `init.d` 的现代替代品），以确保我们的 `websocket` 应用程序（用 `Node.js` 编写）在崩溃时自动重启，并在服务器启动时启动。

#### 6.2 安装 Node.js

首先，让我们在主目录内创建一个目录，用于下载 `Node.js` 的源代码（参见图 6.1）。请注意，为了清晰起见，该目录位于与我们在教程 #1 中解释的下载 `Nginx` 源代码的目录相同的级别。然后我们将使用相同的目录来解包 `tarball` 的内容，并使用常规程序安装 `Node.js`：

（我们在这里遵循通常的构建过程，因为 `checkinstall` 方法在构建 `deb` 包时产生了错误。）

```
sudo ./configure, sudo make, sudo make install
```

在撰写本文时，`Node.js` 的最新版本是 `v0.10.21`，可以从 `http://nodejs.org/download/` 下载（32 位或 64 位版本），使用以下命令（参见图 6.2，出于隐私原因，正在使用的代理服务器及其 IP 地址已模糊处理）：

```
wget http://nodejs.org/dist/v0.10.21/node-v0.10.21.tar.gz
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_63_0.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_63_1.png)

#### 6.3 安装额外的库

接下来，我们将安装 `socket.io`，这是一个用于实时 Web 应用的 JavaScript 库。它有两个部分：

- 一个在浏览器中运行的客户端库
- 一个用于 `node.js` 的服务器端库（`Socket.io`, Wikipedia），使用 `npm`（`node.js` 的官方包管理器，`sudo npm install socket.io`，参见图 6.3）以及 `express`，一个用于 `node.js` 的 Web 应用程序框架。

![](img/3adf2b91cc40e3d0012eab041f055ca8_63_2.png)

为了下载 `express` 框架，我们需要在一个为应用程序创建的目录中的 `json` 文件（`package.json`）中定义几个设置 - 在本例中为 `~/chatroom`（参见图 6.4）。然后我们继续下载并安装它：

```
npm install -d
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_64_0.png)

图 6.4：`package.json` 文件

由于本教程重点在于讲解 `Nginx` 如何与 `websockets` 协同工作，而非使用 `node.js` 进行编程，因此我们不会从零开始开发一个 Web 应用，而是会使用一个已有的、可通过 GitHub 获取的应用（聊天室示例）。我们需要使用以下命令下载 `index.html` 和 `app.js` 文件（见图 6.5）：

```bash
wget https://github.com/mmkohin/pitsmike_example_1/archive/master.zip
```

![](img/3adf2b91cc40e3d0012eab041f055ca8_64_1.png)

图 6.5：从 GitHub 下载聊天室 Web 应用

然后，我们将解压之前提到的文件，并使用 `node app.js` 启动应用（见图 6.6）。如果 `Apache` 正在端口 `8080` 上运行，我们可能需要停止它。

![](img/3adf2b91cc40e3d0012eab041f055ca8_64_2.png)

图 6.6：启动 Web 应用程序

结果（见图 6.7 和 6.8）尚未使用 `Nginx`，我们也尚未提及为何需要使用带 `websockets` 的 `Nginx`，但毕竟已经完成了一半。到目前为止，我们拥有一个类似聊天室的 Web 应用程序，它可以实时显示发送和接收的消息，以及服务器响应。

![](img/3adf2b91cc40e3d0012eab041f055ca8_65_0.png)

![](img/3adf2b91cc40e3d0012eab041f055ca8_65_1.png)

### 6.4 那么……Nginx 与此有何关系？

如果我们需要在正式（生产）环境中使用此应用程序，我们可能希望它监听 `80` 端口（大多数企业级防火墙允许通过该端口进行通信）。但 `Nginx` 已经在监听该端口。我们现在该怎么办？一如既往，我们强大的 `Nginx` Web 服务器给出了答案。我们只需将传入的 `80` 端口请求（外部连接）转发到另一个端口（在本例中为内部连接的 `8080` 端口）。这样，我们就使用 `Nginx` 作为反向代理，外部世界无法直接与聊天室应用通信，而是通过充当前端服务器的 `Nginx` 进行通信。此场景还将允许我们使用 `SSL` 证书来加密流量。

我们将继续编辑 `nginx.conf` 文件（见图 6.9），并添加几个来自代理模块的指令。

```nginx
server {
    listen            80;
    server_name       NGINXTEST.com;
    root      /home/gacanepa/chatroom;
    access_log /home/gacanepa/nginx-1.5.6/html/access_log MyLogFormat;
    error_log /home/gacanepa/nginx-1.5.6/html/error_log;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        index index.html index.htm;
    }
}
```

图 6.9：主配置文件 `nginx.conf`

我们将详细讨论每个指令：

- `proxy_pass` `http://localhost:8080`：通过指定位置（在本例中为同一主机，端口 `8080`）实现对后端服务器的反向代理。
- `proxy_http_version` `1.1`：设置用于与代理后端通信的 HTTP 版本。默认值为 HTTP 1.0，但如果我们需要启用 `keepalive` 连接，最好将此指令设置为 `1.1`。
- `proxy_set_header`：此指令允许您重新定义要传输到后端服务器的头部值。如我们所见，它可以声明多次。
- `proxy_set_header` `Host` `$host`：转发到后端服务器的请求中的 `Host` HTTP 头部默认值在配置文件中指定为代理主机名。此设置让 `Nginx` 使用客户端请求中的原始 `Host`。有关 `http` 头部的完整列表，请参阅教程 #2。
