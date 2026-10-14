

## 设置 Tor Browser Bundle

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_10_0.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_10_1.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_10_2.png)

### 1 下载并启动

该 bundle 包含连接 Tor 网络所需的一切，包括 Tor Browser，即 Firefox 的定制版本。解压后，切换到 CLI 中的目录以运行 ./start-tor-browser 脚本。

### 2 匿名浏览

此脚本会启动 Vidalia 控制面板，它将连接至 Tor 网络。连接后，Tor Browser 将启动并指向 http://check.torproject.org，该页面会确认你正在匿名浏览。

### 3 查看网络

在 Vidalia 中点击“View the Network”，即可打开一张世界地图，显示你的路由和活跃中继。完成后，关闭任意窗口会自动清空浏览器的缓存并断开连接。

一个主要区别是它只使用经过认证的合作伙伴作为节点。此外，你还可以选择希望路由流量经过的代理节点。你可以查看其代理的位置并据此选择以提高安全性。JonDo 对免费用户限制连接速度，但你可以订阅其高级服务，其速度与 VPN 服务一样快。该项目还提供了在保持匿名的同时为服务付费的详细说明。

JonDoBrowser 预先配置为与 JonDo 代理配合使用。此外，与 Tor 不同的是，你可以使用 JonDo 应用关闭匿名性，同时仍继续使用 JonDoBrowser。你也可以在不同浏览器或不同的网络应用（如即时通讯或电子邮件客户端）中使用 JonDo 和 Tor。只需将应用程序配置为将其所有流量通过这些应用路由即可。要通过它们路由流量，请进入应用的连接设置页面并指定以下手动代理设置。对于 JonDo，选择 SOCKSv5 代理，并使用 127.0.0.1 作为主机，4001 作为端口。要将流量通过 Tor 网络传递，如果你正在运行 bundle，请使用 9150 作为端口。还请记住，如果你是 JonDo 的免费用户，你只能连接到用于网页浏览的端口，即 HTTP 的 80 和 HTTPS 的 443。对于其他应用，你必须订阅其高级服务。尽管很难比较 JonDo 和 Tor，但许多人认为前者是更安全的选择。Tor 更容易受到内部攻击，即节点运营商本身攻击网络。这种可能性

### 我了解 JonDo

要使用该服务，请下载基于 Java 的 JonDo 客户端，解压其内容并以 root 身份运行其安装脚本。脚本会将客户端安装在 /usr/local 下。完成后，你可以通过在命令行输入 jondo 来启动它。首次启动时，安装向导会引导你完成简短的连接过程。完成后，应用将连接到代理服务器。你可以从下拉列表中选择要使用的代理网络。每个网络的地理位置都以其国家旗帜标记。除了 JonDo 工具外，该项目还提供了一个适用于 Firefox 的安全配置，称为 JonDoFox。或者，你可以下载 JonDo 自家的基于 Firefox 的浏览器，称为 JonDoBrowser。你可以从项目网站下载并安装浏览器的 Deb 包，或将其仓库添加到基于 Debian 的发行版中。该

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_10_3.png)

避免被追踪，可通过伪造网卡的 MAC 地址，例如 ifconfig eth0 hw ether 0A:A0:04:DA:AA:11

### 安全附加组件

除了使用代理服务外，为你的网页浏览器配备一堆安全和隐私增强插件也是个好主意。使用 AdBlock Plus，你可以对特定广告商进行黑名单和白名单设置。另一个有用的补充是 NoScript Security Suite，它会阻止 JavaScript、Java、Flash、Silverlight 和其他可执行内容运行。此附加组件可防止跨站脚本攻击、跨区域 DNS  rebinding、路由器入侵和点击劫持。

