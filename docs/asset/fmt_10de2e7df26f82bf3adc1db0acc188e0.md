
```bash
acl all src 0.0.0.0/0.0.0.0
acl manager proto cache_object
acl localhost src 127.0.0.1/255.255.255.255
acl SSL_ports port 443 563
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 563 # https, snews
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
acl Safe_ports port 777 # multiling http
acl CONNECT method CONNECT
```

当 `Squid` 试图确定某台特定计算机属于哪个组时，它会从上到下进行检查。在第一行中，所有主机计算机（地址/子网掩码全为零）都被添加到`acl`组`all`中。在第二行中，您创建了一个名为`manager`的管理员组，该组拥有访问您的`cache_object`的权限（即从缓存中获取内容的功能）。`localhost`组被分配给您的回环地址。安全套接层（SSL）端口被分配给数字 443 和 563，而`Safe_ports`被分配给上面显示的数字。最后一行定义了一个名为`CONNECT`的组，您可以使用它来允许访问 SSL 端口。

为了拒绝或启用 `Squid` 计算机上 HTTP 服务的访问，设置了以下定义：

```bash
http_access allow manager localhost
http_access deny manager
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost
http_access deny all
```

这些定义相当严格。第一行允许来自本地主机请求缓存对象（manager）的人这样做，但第二行拒绝其他任何人发出此类请求。访问未被拒绝的那些定义为安全端口的端口。此外，通过代理的套接字连接在所有端口上都已被拒绝，但 SSL 端口（`SSL_ports`）除外。HTTP 访问仅允许来自本地主机，并拒绝所有其他主机。

要允许您网络中的客户端计算机访问您的 HTTP 服务，您需要创建自己的`http_access`条目。您可能希望执行比简单声明`http_access allow all`更严格的限制。以下是一个更严格的`acl`组的示例以及如何将该组分配给 HTTP 访问的方法：

```bash
acl ourlan src 10.0.0.1-10.0.0.100
http_access allow ourlan
```

在前面的示例中，IP 地址从 10.0.0.1 到 10.0.0.100 的所有计算机都被分配给`ourlan`组。然后通过`http_access`行允许`ourlan`的访问。

### 在 `squid.conf` 中配置缓存

就代理服务器而言，缓存是在发送数据的 Web 服务器和接收数据的客户端之间的中间系统上存储数据的过程。其假设是，对相同数据的后续请求可以更快得到服务，因为无需完全返回到原始服务器。相反，代理服务器可以简单地从其缓存副本中向您发送内容。缓存的另一个好处是，它减少了对网络资源和信息服务器的需求。

您可以与其他缓存代理服务器协同工作以形成缓存层次结构。其思想是让一个`父缓存`存在于互联网骨干网的入口附近。当`子缓存`请求一个对象时，如果父缓存没有该对象，父缓存会出去获取该对象，向子缓存发送一份副本，并自己保留一份副本。这样，如果针对该数据的另一个请求到达父缓存，它可能可以在不向原始服务器发出另一个请求的情况下服务该请求。这种层次结构还支持`同级缓存`，它们实际上可以在同一级别创建一个缓存服务器池。

> **注意**
>
> 如果您不加以限制，缓存可能会消耗大量硬盘空间。如果您的系统有独立分区，请确保`/var`中有足够的空间来处理增加的负载。

以下是一些建议您考虑设置的缓存相关标签：

*   `cache_peer` — 如果存在一个可以使用其资源的缓存父级，您可以使用此标签添加父缓存。您需要从父缓存的管理员处获取父缓存的主机名、缓存类型（parent）、代理端口（可能是 3128）和 ICP 端口（可能是 3130）。如果没有父缓存，则无需设置此值。这是一个`cache_peer`条目的示例：

    ```bash
    cache_peer parent.handsonhistory.com parent 3128 3130
    ```

    您还可以在行尾添加选项，例如`proxy-only`，这样从父级获取的内容就不会在本地存储，以及`weight=n`（其中`n`替换为大于 1 的数字，表示应优先于其他父级使用该父级）。如果该父级作为最后手段使用（即当其他所有父级都没有请求的数据时），请添加`default`。

*   `cache_mem` — 指定用于存储传输中对象（当前正在使用的对象）、热对象（经常使用的对象）和负面缓存对象（最近失败的请求）的缓存内存（RAM）量。默认值为 8 MB，但您可以提高该值。要将`cache_mem`设置为 16 MB，请输入以下内容：

    ```bash
    cache_mem    16 MB
    ```

    > **说明**
    >
    > 由于`Squid`可能总共使用分配给它空间的三倍来进行所有处理，`Squid 文档`建议您使用实际可用于`Squid`的空间三分之一的`cache_mem`大小。

*   `cache_dir` — 指定存储缓存交换文件的目录（或者如果您希望将缓存分布在多个磁盘或分区上，则可以指定多个目录）。默认是`/var/spool/squid`目录。您还可以指定缓存使用的磁盘空间大小（以兆字节为单位，默认值为 100）、要创建的第一级目录数量（默认值为 16）和第二级目录数量（默认值为 256）。这是一个示例：

    ```bash
    cache_dir ufs /var/spool/squid 100 16 256
    ```

    > **说明** 缓存目录必须存在。Squid 不会为您创建它。但是，它会创建第一级和第二级目录。

*   `cache_mgr` — 添加如果缓存守护进程停止运行时应收取电子邮件的用户的电子邮件地址。默认情况下，电子邮件发送到`root`。要显式将`cache_mgr`设置为 root 用户，请使用以下命令：

    ```bash
    cache_mgr root
    ```

*   `cache_effective_user` — 在作为`root`启动`squid`守护进程之后，后续进程将作为`squid`用户和组运行（默认情况下）。要将后续用户更改为其他名称（例如`nobody`），请如下设置`cache_effective_user`：

    ```bash
    cache_effective_user nobody
    ```

    > **说明** 当我更改`cache_effective_user`名称，使得除 squid 以外的用户运行 squid 守护进程时，消息日志记录了在进程退出之前几次初始化 squid 缓存失败的尝试。当我将用户名改回`squid`时，进程正常启动。要有效使用`cache_effective_user`功能，您必须更改`/var/spool/squid`及其子目录的所有权。

### 在 `squid.conf` 中配置端口号

当您配置客户端计算机以使用您的 `Squid` 代理服务时，客户端需要知道您计算机的名称或 IP 地址以及与服务相关的端口号。对于希望通过您的代理访问 Web 的客户端，HTTP 端口是所需的数字。以下是您在 `Squid` 中为不同服务设置端口值时使用的标签及其默认值：

*   `http_port 3128` —`http_port`默认设置为 3128。客户端工作站需要知道此数字才能访问您的代理服务器以使用 HTTP 服务。

*   `icp_port 3130` — ICP 请求默认通过端口 3130 在相邻缓存之间发送和接收。

*   `htcp_port 4827` — ICP 默认通过端口 4827 在相邻缓存之间发送和接收 HTCP 请求。

### 调试 `Squid`

如果您设置 `Squid` 后它没有正常工作，或者您只是想监控 `Squid` 活动，有几个工具和日志文件可以帮助您。

## 第四部分 网络

### 检查 `squid.conf` 文件

通过以`-X`选项（前文已描述）运行`squid`守护进程，你可以检查 squid 配置文件正在设置哪些内容。你可以在`/etc/init.d/squid`文件的`SQUIDOPTS`行中添加`-X`选项。然后运行`/etc/init.d/squid restart`。系统将输出大量信息，其中详细说明了从 squid.conf 中设置的内容。如果文件中存在语法错误，它们将在此处显示。

### 检查 `Squid` 日志文件

在 `CentOS` 中，`Squid` 日志文件默认存储在`/var/log/squid`目录中。以下是创建在该目录中的日志文件、它们包含内容的描述，以及它们可能如何帮助你调试潜在问题的说明：

*   **access.log** — 包含记录条目，描述每当客户端请求 HTTP 内容时缓存被命中或未命中的情况。与这些信息一起记录的是发起请求的主机身份（IP 地址）以及他们请求的内容。使用这些信息可以了解内容何时从缓存中调用，以及何时必须访问远程服务器才能获取内容。以下是部分访问结果代码的含义：

    *   `TCP_DENIED` — `Squid` 拒绝了该请求的访问。
    *   `TCP_HIT` — 缓存中包含该对象的有效副本。
    *   `TCP_IMS_HIT` — 当客户端询问内容是否已更改时，请求对象的较新版本仍在缓存中。
    *   `TCP_IMS_MISS` — 客户端针对过期对象发出了 If-Modified-Since 请求。
    *   `TCP_MEM_HIT` — 内存中包含该对象的有效副本。
    *   `TCP_MISS` — 缓存中未包含该对象。
    *   `TCP_NEGATIVE_HIT` — 该对象被负向缓存，这意味着当请求该对象时返回了错误（例如文件未找到）。
    *   `TCP_REF_FAIL_HIT` — 由于验证对象的请求失败，缓存返回了过期对象。
    *   `TCP_REFRESH_HIT` — 缓存中存在对象的过期副本，但对服务器的请求返回了对象未修改的信息。
    *   `TCP_REFRESH_MISS` — 过期的缓存对象被新的、更新的内容替换。
    *   `TCP_SWAPFAIL` — 尽管认为对象应该存在，但无法从缓存中访问该对象。

*   **cache.log** — 当 squid 守护进程启动时，包含关于 `Squid` 配置的宝贵信息。你可以查看可用的内存大小（Max Mem）、交换空间大小（Max Swap）、缓存目录的位置（`/var/spool/Squid`）、正在接受连接的类型（HTTP、ICP 和 SNMP），以及接受连接的端口。你还可以看到大量关于缓存对象的信息（例如已加载、过期或取消的对象数量）。

*   **store.log** — 包含记录条目，显示内容何时从内存交换到缓存（`SWAPOUT`）、从缓存交换回内存（`SWAPIN`），或从缓存释放（`RELEASE`）。你可以查看内容的原始来源及其在缓存中的存储位置。该文件中的时间以原始 UNIX 时间（以毫秒为单位）记录。

你可能对其他日志文件也很感兴趣：`/var/log/messages`。该文件包含描述`squid`守护进程启动和退出状态的条目。

### 使用 `top` 命令

运行`top`命令查看有关运行中进程（包括`Squid`进程）的信息。如果你担心过多的`Squid`活动导致性能下降，请在 top 窗口内输入`M`。`M`选项显示按每个进程使用的内存百分比排序的运行中进程信息。如果你发现`Squid`消耗了系统内存的过大比例，你可以通过重置`squid.conf`文件中的`cache_mem`值来减少内存使用量。

### 设置代理客户端

为了让你的`Linux`代理服务器为网络上的`Windows`和`Linux`客户端计算机提供 Web 浏览访问（HTTP），每个客户端都需要在 Web 浏览器中进行一些设置。使用代理服务器的好处在于你的客户端计算机不需要知道的信息，例如以下几点：

*   `DNS`服务器的地址
*   `ISP`的电话号码
*   连接`ISP`的聊天脚本

可能还有其他客户端不需要知道的内容，但你应该明白其中的意思。在代理服务器拥有到 Internet 的连接并允许局域网（LAN）上的客户端计算机访问该服务后，客户端只需要知道以下信息：

*   **主机名** — 代理服务器的名称或 IP 地址。这假设客户端可以通过`LAN`或其他基于 IP 的网络访问代理。
*   **端口号** —`HTTP`服务的端口号（默认为 3128）。相同的端口号也可用于`FTP`服务。

如何在客户端上设置代理服务，更多取决于你使用的浏览器，而不是你使用的操作系统。请按照以下部分中概述的步骤设置`Firefox`、`Microsoft Internet Explorer`、`Mosaic`或`Lynx`浏览器。

### 配置 `Firefox` 使用代理

通常，你会设置 Firefox 通过电话线上的 Internet 上的 TCP/IP 连接或通过局域网上的路由器直接浏览 Web。请按照此步骤更改 Firefox 以便通过你的代理服务器访问 Web：

1.  打开 Firefox。
2.  选择 **编辑 > 首选项**。首选项窗口将出现。
3.  选择“高级”类别，然后选择“网络”选项卡。
4.  单击“设置”按钮。连接设置窗口将出现。
5.  单击“手动代理配置”以启用代理配置（参见图 15-2 中 Firefox 连接设置页面的示例）。
6.  在 HTTP、FTP 和 Gopher 服务的地址框中输入代理服务器的名称或 IP 地址。
7.  在 HTTP、FTP 和 Gopher 服务的“端口”框中输入代理服务器上 HTTP 服务的端口号（通常为 3128）。你可以只填写 HTTP 代理的信息，并勾选“使用此代理服务器作为所有协议”选项，以便自动填充其他服务的信息。
8.  单击确定。

下次你从 Firefox 请求一个 web 地址时，它将联系代理服务器以尝试获取内容。

### 图 15-2

首选项窗口在 Firefox 中标识代理服务器和端口号。

![](img/2f265415ceec72538dd3c78ffca75c10_687_0.png)

### 配置其他浏览器使用代理

在 `Linux` 中可用的其他浏览器中，指示代理服务器有不同的方法。要让 Mosaic 或 Lynx 浏览器使用代理服务器访问 Internet，请在运行该浏览器的 shell 中添加一个环境变量。以下是如何使用`csh`或`tcsh`shell 将 HTTP 和 FTP 代理服务的环境变量设置为名为`maple`的代理计算机的方法：

```bash
setenv http_proxy http://maple:3128/
setenv ftp_proxy http://maple:3128/
```

如果你使用的是`ksh`或`bash`shell，请输入以下内容：

```bash
export http_proxy=http://maple:3128
export ftp_proxy=http://maple:3128
```

你可以将这些值中的任何一个添加到你的启动脚本中。或者，为了使其在全系统范围内可用，你可以将它们添加到系统配置文件中，例如`/etc/profile`或`/etc/skel/.bash_profile`。

对于`elinks`和`links`浏览器，你可以在`/etc/elinks.conf`文件中指示使用代理服务器。例如，以下是你需要添加到`/etc/elinks.conf`文件中的行，以便让`elinks`和`links`使用名为`maple`的计算机作为 FTP 和 HTTP 服务的代理：

```bash
protocol.ftp.proxy.host maple:3128
protocol.http.proxy.host maple:3128
```

### 摘要

连接到 Internet 为你的 `CentOS` 系统打开了一个充满可能性的世界。使用你的系统作为公共 Web 服务器、邮件服务器或 FTP 服务器取决于其连接 Internet 的能力。同样，如果你的计算机已经连接在局域网（LAN）中，添加一个 Internet 连接可以一劳永逸地为局域网上的所有用户提供 Internet 访问。

## 第四部分

### 网络

本章在互联网地址覆盖的基础上，介绍了互联网域的组织方式。建立到互联网的拨号连接重点描述了 PPP。本章还讨论了几种将局域网连接到互联网的不同技术。你可以将 `Linux` 计算机设置为路由器或 `Squid` 代理服务器。

为了使用互联网连接将敏感数据传输到公司私有网络中的另一位置，你可以配置 VPN。本章描述如何使用 IPsec 在 `CentOS` 中创建两个位置之间的 VPN 连接。

## 第 16 章

### 设置打印机和打印
