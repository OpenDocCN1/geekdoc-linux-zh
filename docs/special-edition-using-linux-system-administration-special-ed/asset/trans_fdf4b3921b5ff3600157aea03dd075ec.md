
Apache 会在与 `httpd.conf` 相同的目录中查找其他配置文件，或者遵循 `httpd.conf` 中的任何指令，以指向备用 `access.conf` 和 `srm.conf` 文件的位置。

## 停止服务器

你可以使用 kill 命令停止服务器。Apache 将其进程 ID 存储在文件 `/var/run/httpd.pid` 中，因此你可以使用以下命令终止 Apache：

```sh
# kill `cat /var/run/httpd.pid`
```

## 重启服务器

你可以通过使用 kill 命令向正在运行的 Apache 守护进程发送 `SIGHUP` 信号，强制其重新加载配置文件：

```sh
# kill -HUP `cat /var/run/httpd.pid`
```

如果你确实需要停止 Apache 并重新启动它，可以使用以下命令：

```sh
# kill `cat /var/run/httpd.pid`
# /usr/sbin/httpd
```

## 测试服务器的状态和配置文件

你可以使用 `httpd` 命令的 `-t` 和 `-s` 标志来检查 Apache 配置文件的准确性：

```sh
# /usr/sbin/httpd -t -S
```

`-t` 标志测试你的配置语法，`-S` 标志显示虚拟主机配置的解析结果（如果有的话）。如果你需要指定配置文件的确切位置，请使用 `-f` 标志指明 `httpd.conf` 文件的位置：

```sh
# /usr/sbin/httpd -t -S -f /usr/local/apache/conf/httpd.conf
```

## 使用 Apache 进行虚拟主机托管

尽管许多 Web 服务器只服务单个网站，但内联网和互联网 Web 服务器托管多个站点的情况并不少见，每个站点都有自己独特的文档树和域名。例如，互联网服务提供商可能向其客户提供 Web 托管，或者组织中的每个部门可能在内联网上拥有一个独立且不同的网站。

要支持从单个 Web 服务器托管多个站点，需要使用虚拟主机。虚拟主机可以通过两种方式实现：

- 基于 IP 地址的虚拟主机（或硬件虚拟主机）：Web 服务器拥有多个 IP 地址，每个站点关联一个不同的 IP 地址。
- 基于主机名的虚拟主机（或软件虚拟主机）：Web 服务器响应单个 IP 地址，但该地址关联多个主机名，每个主机名与服务器上的一个不同网站相关联。

基于 IP 地址的主机托管具有一个优点：客户端无需向服务器提供任何特殊信息，服务器即可选择并提供正确的站点。然而，由于 IP 地址日益短缺，对于在公共互联网上提供网站的服务器来说，这种选择缺乏吸引力。

基于名称的虚拟主机要求客户端提供一个主机头字段，在其中指明所需站点的主机名。这是 HTTP 1.1 的一项功能，所有较新的浏览器都支持，但一些较旧的浏览器不支持。对于这些浏览器，服务器将在其 IP 地址上收到请求，但没有信息来确定要服务哪个站点。尽管如此，这种类型的软件虚拟主机正日益成为常态，因为它不会不必要地占用 IP 地址资源。在本章中，我们将讨论基于主机名的虚拟主机的实现。

实现基于名称的虚拟主机需要三个步骤：

- 为每个站点创建 DNS 条目
- 为站点创建目录层次结构
- 配置 Apache 以服务每个站点

### 为每个站点创建 DNS 条目

互联网上的 Web 服务器需要一条自身的 A 记录，以指明服务器的主域名。如果你的 Web 服务器的主域名是 www.my.domain，且其 IP 地址是 1.2.3.4，那么该服务器的 DNS A 记录将是：

```
www.my.domain.   IN   A   1.2.3.4
```

对于你希望使用基于名称的虚拟主机在系统上托管的每个附加站点，你必须创建一条规范名称（CNAME）记录，作为服务器的别名。例如，要将第二个域名 fun.my.domain 关联到同一台服务器，你可以使用以下 CNAME 记录：

```
fun.my.domain.   IN   CNAME   www.my.domain.
```

即使你想在主主机名所在域之外的其他域中创建虚拟主机，你仍然可以使用 CNAME 记录。例如，你可以通过在 another.domain 的 DNS 记录中使用以下 CNAME 条目，将 www.another.domain 别名指向 www.my.domain：

```
www.another.domain.   IN   CNAME   www.my.domain.
```

关于 DNS 管理以及 DNS 区域文件的创建和编辑的完整细节，将在第 22 章“DNS”中讨论。

### 为站点创建目录层次结构

你的 Apache 系统所服务的每个站点都需要一个独立且不同的文档根目录，用于提供文件。通常，建议将这些文档根目录集中在一个位置以便于管理。例如，如果你的单站点 Web 服务器通常使用 `/usr/local/apache/htdocs/` 作为其文档根目录，那么当你转向虚拟主机时，你可能希望在此位置创建子目录，每个子目录作为不同站点的文档根目录。考虑前面为服务器定义的三个主机名：`www.my.domain`、`fun.my.domain` 和 `www.another.domain`。

在这种情况下，你可以为这些站点创建三个目录：

- `/usr/local/apache/htdocs/www.my.domain`
- `/usr/local/apache/htdocs/fun.my.domain`
- `/usr/local/apache/htdocs/www.another.domain`

你可以对网站的根文档目录使用任何组织方案。使用一致的方案（例如这里创建的方案）有助于确保随着站点的发展和增长，管理仍然轻松。

### 配置 Apache 以服务每个站点

你可以通过两种方式配置 Apache 以服务多个虚拟站点：

- 为每个站点运行独立的 Apache 守护进程
- 为所有站点运行共享的 Apache 守护进程

除非你计划为每个站点提供显著不同的配置，包括不同的 ServerRoot 值、不同的用户和组，或不同的 ServerType 值，否则请考虑后一种选择。运行单个 Apache 守护进程使管理更加容易：你只需维护一组配置文件，并且只需监控一个守护进程即可跟踪站点的健康状况。

使用单个 Apache 守护进程配置基于名称的虚拟主机的第一步，是将 NameVirtualHost 指令添加到你的 `httpd.conf` 文件中。该指令指明 Apache 应监听哪个 IP 地址以接受虚拟主机连接，其形式如下：

```
NameVirtualHost 1.2.3.4
```

`1.2.3.4` 是服务器的 IP 地址。

接下来，你需要在 `httpd.conf` 文件中添加特殊的 `<VirtualHost ...> ... </VirtualHost>` 部分。VirtualHost 部分允许你指定特定虚拟服务器的设置，包括唯一的文档根目录和服务器名称。每个 VirtualHost 部分采用以下一般形式：

```
<VirtualHost <IP Address>>
    <Directives>
</VirtualHost>
```

在基于名称的虚拟主机情况下，每个 `VirtualHost` 部分都与同一个 IP 地址关联，但其中的 `ServerName` 指令标识了服务器关联的名称。例如，在前面的三个虚拟 Web 服务器（`www.my.domain`、`fun.my.domain` 和 `www.another.domain`）示例中，你需要三个 `VirtualHost` 部分，每个部分至少包含一个 `ServerName` 和一个 `DocumentRoot` 指令：

```apache
<VirtualHost 1.2.3.4>
    ServerName www.my.domain
    DocumentRoot /usr/local/apache/htdocs/www.my.domain
</VirtualHost>

<VirtualHost 1.2.3.4>
    ServerName fun.my.domain
    DocumentRoot /usr/local/apache/htdocs/fun.my.domain
</VirtualHost>

<VirtualHost 1.2.3.4>
    ServerName www.another.domain
    DocumentRoot /usr/local/apache/htdocs/www.another.domain
</VirtualHost>
```

在每个 `VirtualHost` 部分中，你还可以放置其他指令，以创建每个站点特定的设置。

为你的虚拟站点配置 Apache 后，请重启 Apache 守护进程以重新加载其配置文件，如本章前面“重启服务器”一节所述。

### 提供向后兼容性

基于名称的虚拟主机为在单台服务器上运行多个网站的需求提供了一种简单、优雅的解决方案，无需过度使用稀缺的 IP 地址。然而，它与不使用 HTTP 1.1 Host 头字段来指示所请求站点名称的旧版 Web 浏览器存在不兼容问题。对于这些浏览器，你必须设置一个逻辑上的默认网站，用户可以从该网站链接到各个虚拟站点。

基本模型如下：

- 使用上述 `VirtualHost` 部分定义每个虚拟站点，但要在该部分中添加一个 `ServerPath` 指令。
- 添加一个默认的 `VirtualHost` 部分，用于捕获任何对未指定或不存在的站点的连接。该站点应包含指向所有虚拟站点的链接。

最终结果是，以下指令可用于定义本章示例服务器的虚拟主机：

```apache
<VirtualHost 1.2.3.4>
    DocumentRoot /usr/local/apache/htdocs/
</VirtualHost>
```
