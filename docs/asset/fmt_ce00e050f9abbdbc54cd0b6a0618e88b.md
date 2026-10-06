
# 第 11 章 网络服务

![](img/57e3c53e2eeaacba18095c31e47_0.png)

**图 11-2.** 从层 0 到层 3 的时间服务器。层级可以延伸到 16。

每当这些机器加载时，你将仅使用为它们分配的新路由器和新域名服务器。要查找更多可用的语句，请查阅 `dhcpcd.conf` 的 man页面。

## NTP 服务器

当你准备使用你的 CentOS 安装运行任何服务时，强烈建议设置一个用于同步时间的设施。你可能认为各个机器的时间戳已经足够了，但在某些情况下是不够的。例如，尝试检查你机器的时间相对于你朋友机器的时间，它们的小时可能相同但分钟会有差异。现在问自己哪个时间是正确的？答案并不是官方的，但这种非常简单的例子可以扩展到需要精确时间的生产系统。某些应用程序，例如日志记录，需要同步。当互联网连接正常时，客户端机器可以拥有自己的时间服务器并连接到最高层级，但这可能会产生时间差异。

解决此问题的答案是使用网络时间协议 `NTP`，它设计用于跨网络同步时间。默认情况下，时间标准是协调世界时 `UTC`。`NTP` 被组织成不同的层级，称为层 `strata`。最高层是同步数据的源，例如原子钟、`GPS` 钟和其他类型的无线钟。较低的层级 `strata 1` 及以下。最低的层级是 16，分配给新运行的服务器。图 11-2 显示了层级是如何分组的。

并不是严格规定客户端时间服务器只能引用比它们层级更高的机器。相同层级的服务器也可以分布时间数据。例如，在 `NTP` 设置中，第一台机器从公共时间服务器获取时间数据；第二台机器从第一台机器获取时间数据；第三台机器从第二台机器获取时间数据。这使得第三台机器成为服务器。根据前面的示例，我们的客户端机器现在可以使用网络上运行的两个时间服务器之一。

## NTP 配置模式

`NTP` 有五种可选的关联或配置模式，每种都有自己的用途：

- **客户端-服务器 Client-Server：** 设置一台机器作为 `NTP` 服务器，另一台机器作为 `NTP` 客户端从该服务器获取时间数据。`NTP` 客户端通常是网络中为其他机器提供时间数据的本地服务器。
- **对称主/备 Symmetric active/passive：** `NTP` 服务器配置为彼此的对等节点。如果两个对等节点都存在，它们将相互发送对称活动消息。如果一个对等节点掉线，剩余服务器将继续发送，时间数据仍然可用。
- **广播 Broadcast：** 这种配置通常部署在广域网中。
- **组播 Manycast：** `NTP` 版本 4 的新功能允许组播客户端主动搜索服务器。
- **孤儿 Orphan：** 如果没有可连接的时间服务器，`NTP` 可以在此模式下运行。它将使用本地时模拟 `UTC` 源。

在本节中，你将设置 `NTP` 以三种模式提供时间：客户端-服务器、对称和广播。通过输入 `install ntp` 安装 `NTP` 服务器及其池。

### 客户端-服务器模式

使用文本编辑器打开位于 `/etc` 的主配置文件 `ntp.conf`。接下来，找到以下条目：

```
server 0.pool.org

server 1.pool.org

server 2.pool.org
```

你的 `NTP` 服务器在安装时已经配置为 `NTP` 客户端。它通过 `server` 命令声明的时间服务器收集数据。`server` 命令可以接受其想要连接的服务器的主名或 IP。你可以从 `http://www.pool.ntp.org` 选择更多时间服务器以提高可用性。例如，我们想添加来自菲律宾的时间服务器 `ph.pool.ntp.org`。我们只需要添加另一个 `server` 条目：

```
server 0.pool.org

server 1.pool.org

server 2.pool.org

server ph.pool.ntp.org
```

添加新条目后，保存文件并启动 `NTP` 进程：

```
service ntpd start
```

或者如果你已经运行 `ntpd` 进程，则重启它。如果你想通过查看日志文件来实时查看运行情况，可以使用命令：

```
ntpd -d
```

这将打印 `NTP` 在运行期间执行的所有活动。你可以通过按 `Ctrl+C` 停止服务器。当你完成工作并准备将服务器投入生产环境时，可以使用先前的命令。

### 对称主/备模式

我们将在练习中使用另一个 `NTP` 服务器。我们假设第一台 `NTP` 服务器的 IP 地址为 `192.168.1.104`，第二台为 `192.168.1.100`。为了让它们相互认识

对于对称主动/被动设置的对等节点 `peers`，我们将在配置文件中使用 `peer` 命令。`peer` 命令将 `NTP` 对等节点的主机或 IP 地址作为其参数。

打开第一台机器的主配置文件，并在底部添加以下行：
`peer 192.168.1.100`

保存文件。使用 `ntppd restart` 重启 `ntppd` 服务。对第二台机器执行相同的操作，使用 `192.168.1.104` 作为 `peer` 命令的参数。

在两台机器上都添加了 `peer` 行后，它们现在运行在对称主动/被动模式。如果由于某种原因，第一台机器无法访问任何公共时间服务器，而第二台机器可以，前者将向后者请求时间数据。时间数据将分发给客户端。

### 广播模式

在我们的设置中，第一台机器将扮演能够访问公共时间服务器的 `NTP` 服务器的角色，第二台将作为 `NTP` 服务器。第一台机器将广播消息，客户端在接收到消息时将开始从服务器检索时间数据。因此，第一台机器将同时扮演服务器和机器客户端的角色。

1. 在我们之前添加的 `peer` 命令前加上哈希符号 `#`。这将使其成为注释，因此 `NTP` 进程将忽略它：`# peer 192.168.1.100`
2. 在底部添加以下行：
`broadcast 192.168.1.255`
`disable auth`
3. `broadcast` 命令将在其被分配的网络上发送消息。在示例中，它将向每个以 IP 地址 `192.168.1` 开头的 `NTP` 客户端通告公告。`disable auth` 行允许我们在没有身份验证的情况下运行设置。默认情况下，广播需要通过 `Autokey` 协议提供安全保障。
4. 对于客户端，注释掉配置文件中所有的 `server` 命令条目。我们将从 `NTP` 服务器广播中获取时间数据。
5. 仍在客户端上，注释掉 `peer` 命令条目以忽略它。然后在文件末尾添加以下内容：
`broadcastclient`
`disable auth`

上述行将使客户端监听由 `NTP` 服务器发送的、无需严格身份验证的广播消息，用于测试。保存文件并重启 `ntppd` 进程。
你可以使用 `ntpq` 的 `associations` 命令来监控客户端和服务器之间的交互。你可能需要等待几分钟才能看到操作结果，因为两台机器都需要找到对方。

## ntpq

你可以使用 `NTP` 查询工具 `ntpq` 监控正在运行的 `NTP` 服务器。通过 `ntpq`，你可以获取有关 `NTP` 服务器的信息，例如其对等节点和 `nppd` 进程的操作情况。`ntpq` 工具可以在命令行或交互式模式下运行。在命令行中使用 `ntpq` 工具时，使用以下语法：

```
ntpq [given_command] [target_ntp_host]
```

其中 `[given_command]` 是你想配合 `ntpq` 使用的命令，`[target_ntp_host]` 是你想要使用 `ntpq` 查询的 `NTP` 服务器。在命令行上可以使用 `ntpq` 使用的一些命令包括 `-p` 和 `-i`。`-p` 让 `ntpq` 打印 `NTP` 服务器的对等节点，`-i` 则强制其在交互式模式下运行。省略 `[target_ntp_host]` 部分将使 `ntpq` 在你的本地 `NTP` 服务器上进行交互，如列表 11-5 所示。

### 列表 11-5 交互模式下的 ntpq 提示符

```
ntpq>
```

你可以在此提示符处输入命令来显示你的 `ntpq` 进程如何运行。例如，要查找 `NTP` 服务器的对等节点，请使用 `peers` 命令列出它们，如图 11-3 所示。

```
ntpq> associations

ind asID status conf reach condition last_event cnt

1 62519 9814 yes none reject reachable 1

2 62520 9814 yes none reject reachable 1

3 62521 9814 yes none reject reachable 1

4 62522 9814 yes none reject reachable 1

5 62523 9614 yes none sys.peer reachable 1

6 62524 8000 yes none reject 1

tpq> 
```

图 11-3. `peers` 命令输出示例

图 11-3 中的 `peers` 输出显示了服务器的 `NTP` 对等节点及其当前状态、`remote` 字段中的远程对等节点主机名或 IP 地址以及 `st` 列中的层级 `stratum`。你可以在 `ntpq` 手册中学习更多关于 `peers` 命令的知识。
可以通过输入 `q` 或 `r` 退出 `ntpq` 交互模式。

## DNS

域名系统 `DNS` 是一种用于识别网络上计算机的分布式命名系统。它由美国军开发，以便计算机能够拥有唯一的名称并进行正确的通信。在 `DNS` 出现之前，计算机的 `hosts` 文件 `HOSTS` 文件是网络上通过主机名识别计算机的唯一方法。必须手动更新此文件，以便在主机从网络中添加或删除时通知计算机。由于需要手动更新，导致主机间产生混淆的命名冲突非常常见。现代操作系统中仍然存在 `hosts` 文件，以便在网络上没有 `DNS` 的情况下提供识别计算机的方法。例如，Linux 使用 `/etc` 目录下的 `hosts` 文件。为了让计算机在 `DNS` 上拥有唯一名称，计算机名通过 `DNS` 进行管理。

![图 11-4. 域名系统布局](https://example.com/dns-layout.png)
图 11-4. 域名系统布局

在图 11-4 中，`com` 域名是 `DNS` 查询的起始点。

### 名称服务器与区域

域名系统位于树中，`com` 域名是 `DNS` 查询的起始点。这些是名称服务器能够通过查询主机来将域名转换为 IP 地址。这些域名和子域名通常由实体维护 `区域`。在图 11-4 中，`com` 域名由 Apress 出版公司拥有，其服务器拥有 `www.appress.com` Web 服务器和 `ftp.appress.com` FTP 服务器。根服务器位于根顶层。

#### 域名解析

域名解析通过名称服务器在 `DNS` 中查找正确主机。这是通过递归查询权威名称服务器直到获得答案。以下是客户端想要加载 `www.appress.com` 网页时发起的 `DNS` 查询的步骤过程：

1. 获取域名并按点进行分割。这将告诉客户端名称服务器从哪里开始。分割后，FQDN `www.appress.com` 变为 `www` .appress `com`。
2. 客户端名称服务器将在 `com` 域名的根服务器开始查询。在图 11-4 中，这些是顶层的名称服务器，由查询 FQDN 最右侧的点表示。其中一个根服务器将提供关于 `com` 域名的权威答案，并将客户端名称服务器指向 `com` 域名名称服务器。
3. 客户端名称服务器根据来自根服务器的权威答案，查询 `com` 域名名称服务器。`com` 域名名称服务器拥有关于 `appress.com` 域名的权威信息，并将客户端名称服务器指向 `appress`。
4. 客户端名称服务器向 `appress.com` 域名查询 `www.appress.com` 域名。此时，`appress.com` 名称服务器拥有 `www.appress.com` 的主机信息并将计算机的 IP 地址返回给客户端名称服务器。客户端名称服务器会将该 IP 地址提供给请求查询的客户端。

此过程也用于其他需要 `DNS` 的服务器，例如托管 `ssh`、`http` 和 `ftp` 的服务器。如果你计划在网络中建立互联网连接，你应该安装并配置 `DNS` 服务器。本地 `DNS` 服务器有几个优势：它可以帮助你进行更快的 `DNS` 查询，提供备用 `DNS` 服务器，并允许你成为该区域的主服务器。在接下来的章节中，你将使用来自伯克利互联网命名域 `BIND` 软件包的工具。`BIND` 是 `DNS` 的开源实现，你可以通过输入命令 `install bind-chroot` 来安装它的配置文件和二进制文件。我们将使用带有 `chroot` 支持的 `BIND` 软件包，在你的系统中获得一个安全的服务器。如果攻击者设法通过 `DNS` 进入你的系统，他们只能看到 `bind-chroot` 软件包中指定的 `chroot` 目录 `/var/named/chroot` 内的任何内容。

## BIND 工具

运行和管理 `BIND` 的主要工具是 `rndc-conf`、`rndc` 和 `named`。通过这些工具，你将能够为 `DNS` 服务器创建配置文件、识别区域并为了维护管理服务器。

### rndc-conf

`rndc-conf` 命令用于为 `rndc` 和 `named` 生成 `rndc` 密钥和配置文件。不带任何参数运行它将产生包含这两个工具配置文件的输出。你必须将输出重定向到文件中并进行必要的更改以分离它们。当你创建第一个类型的名称服务器时，将学习更多关于该工具的知识。

### named

`named` 是用于 `named` 的命令行管理工具。你可以通过向 `rndc` 发布命令来控制 `named`，例如获取状态或重载区域。`rndc` 工具使用由 `rndc-conf` 生成的 `rndc.conf` 文件。

### named

`named` 是 `BIND` 工具的实际服务器名称。它用于创建和解析域名，并使用名为 `named.conf` 的配置文件，该文件也是由 `rndc-conf` 工具生成的。你将在本章的 `DNS` 部分大量使用 `named`。

还包含了其他工具用于在执行查找时测试正向和反向域名解析。这些包括 `nslookup`、`dig` 和 `host` 等。当你的名称服务器启动并运行时，稍后将讨论这些每一个工具。

## BIND 配置文件

在运行 `named` 和 `rndc` 之前，你需要使用 `rndc-conf` 工具创建它们的配置文件。你将不带任何参数运行它，并通过重定向到文件来保存内容。执行以下步骤创建配置文件。

1. 进入 `/var/named/chroot/etc` 目录并运行以下命令：
   `rndc-conf > named.conf`

这将重定向名为 `rndc.conf` 的文件。

使用 `GEdit` 等文本编辑器打开 `rndc.conf` 文件并浏览内容。
内容可能看起来如列表 11-6。

#### 列表 11-6. rndc 和 named 的配置文件

```bash
# Start of rndc.conf

key "rndckey" {

  algorithm hmac-md5;

  secret "9mt/YqRTHjIA2H924sfyg="

}

options {

  default-key "rndckey",

  default-server 127.0.0.1;

  default-port 953;

}

# End of rndc.conf
```

```bash
# 在 named.conf 中使用以下内容，并根据需要调整允许列表：

# key "rndckey" {

  algorithm hmac-md5;

  secret "9mt/YqRTHjIA2H924sfyg="

}

# controls {

  inet 127.0.0.1 port 953

  allow { 127.0.0.1; } keys "rndckey";

}

# End of named.conf
```

2. 该文件包含 `rndc` 和 `named` 的配置文件。`named` 的配置文件位于行下方的注释部分：

```
# End of rndc.conf
```

当 `rndc` 运行时将忽略该部分。你将移除被注释的配置文件并将其放入另一个名为 `named.conf` 的文件中。使用你的文本编辑器，剪切从这里开始的行：

`# Use with the following in named.conf, adjusting the allow list as needed:`

```bash
until
```
# End of named.conf
```

将这些行放在 `/var/named/chroot/etc` 目录内名为 `named.conf` 的新文本文件中并保存。我们将关注这个文件。

3. 完成此操作后，`rndc.conf` 文件应该看起来如列表 11-7。

#### 列表 11-7. rndc.conf 文件

```bash
# Start of rndc.conf
```

key "rndckey" {

  algorithm hmac-md5;

  secret "9gt/YqRTHjia2H924sfyg=";

}

noptions {

  default-key "rndckey"

  default-server 127.0.0.1;

  default-port 953;

}

# End of rndc.conf

```

保存文件。

4. `named.conf` 文件的内容仍用井号符号注释，你需要取消这些注释以便 `named` 能够读取这些命令。在进行这些更改后，`named.conf` 的内容应该看起来如列表 11-8。

#### 列表 11-8. named.conf 文件

```bash
# Use with the following in named.conf, adjusting the allow list as needed:

key "rndckey" {

  algorithm hmac-md5;

  secret "9mt/YqRTHjIA2H924sfyg="

}

controls {
