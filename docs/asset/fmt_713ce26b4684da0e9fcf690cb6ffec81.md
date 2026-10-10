
在下面的演示中，我们将使用 Red Hat Linux。关于编译 Squid 的指令，请访问 http://squid-docs.sourceforge.net/latest/x。

1. 要确保系统上安装了 Squid，输入以下命令：

```
rpm -qa | grep squid
```

2. 如果已安装 Squid，你应该收到以下内容：

```
squid-2.3.STABLE-1
```

3. 如果没有响应，访问 www.redhat.com 点击 Download 链接。在 Find RPMs By 字段中输入 `squid` 进行 RPM 搜索。点击 Search。将出现最新版本的 Squid；在此情况下，它是 `squid-2.3.STABLE-1`，如图 10.8 所示。

4. 下载最新版本的 Squid。

5. 使用 `rpm -i` 命令安装 RPM。安装完成后，你就准备好配置 Squid 了。

## 图 10.8 为 Red Hat Linux 下载 Squid RPM

![](img/a7a9caa80ec85507179284d91e216f9f_520_0.png)

## 配置 Squid

安装 Squid 后，你必须使用 `/etc/squid/squid.conf` 文件对其进行配置。该文件定义了 Squid 配置，例如 Squid 监听 HTTP 请求的 HTTP 端口号、入站请求、超时信息以及防火墙访问数据。在 Squid 安装期间，会创建一个一个 `/etc/squid/squid.conf` 文件。

`squid.conf` 文件配置了 Squid 的默认设置，在进行若干更改后即可可以使用，因为 Squid 默认拒绝所有浏览器的访问。在修改 `squid.conf` 之前，Squid 是完全没有用的。

正如默认 Squid 配置文件所示，如果你不需要更改默认设置，则无需取消该设置的注释。默认 Squid 配置文件 `/etc/squid/squid.conf` 如图 10.9 所示。

# 部署 Squid 代理缓存服务器 第10章 521

### 10.9 使用 `/etc/squid/squid.conf` 配置 Squid

```
root@we-23-08-8:00 squid.net: /etc/squid
# Squid Options Help
NETWORK OPTIONS
TAG: http_port
  Usage: port
    hostname=port
    3128

  Squid 监听 HTTP 客户端的套接地址。
    你可以指定多个套接地址。
    有三个字段：port, hostname 和，或 port
    address，然后是 port。如果你指定了 hostname 和
    address，则 Squid 将套接绑定到多个
    地址。这取代了旧的特定 IP 地址的
    方法，因此你可以单独使用端口号。

  默认端口号为 3128。

  如果你在加速器模式下运行 Squid，你
    可能也想监听 80 端口，或者使用
    -a 行选项将覆盖这里的 "*" 端口
    监听器。然而，这将覆盖 IP
    地址。

  你可以在多行中指定多个地址：
http_port 3128
  TAG: tcp_port
    Squid 向邻居发送和接收 TCP 查询
    的端口号。默认是 3130。禁用请使用
    "0"。可能在命令行上通过 -u 覆盖。
```

`squid.conf` 中的每个配置选项都被识别为一个标签（tag）。每个标签代表一条 Squid 配置。例如，HTTP 客户端请求端口的设置被识别为 `http_port` 标签。我们将 `squid.conf` 的设置称为标签。

在 10.9 节中，`squid.conf` 文件显示了“网络选项（Network Options）”部分。它显示了 Squid 监听 HTTP 客户端请求的套接地址配置。指定的默认端口号 TCP 端口 `3128` 也是代理客户端向代理缓存服务器发送请求时使用的默认端口。如果你在代理缓存服务器上更改了此端口，你也将需要在代理客户端上进行相应的更改。

请注意，`squid.conf` 文件中的所有标签都被注释掉了。这意味着在没有指定标签的情况下，Squid 将使用默认设置。从理论上讲，此文件可以是空的，Squid 仍然会以默认设置运行。如果你指定了一个标签，Squid 将使用该标签而不是默认设置。另外注意，`/etc/squid/squid.conf` 中包含默认设置的文件也列在配置文件中。

![](img/a7a9caa80ec85507179284d91e216f9f_521_0.png)

`http_port` 描述中提到的 Squid “加速器模式（accelerator mode）”允许 Squid充当 Web 服务器。Squid 基本上通过更改目标端口来翻译客户端 Web 请求，并将请求发送到 Web 服务器。响应会被缓存，并由 Squid 发送给客户端。这减少了到 Web 服务器的流量（它“加速”了慢速 Web 服务器），并且可以通过过滤保护 Web 服务器。本章将不会演示加速模式，但你应该对此有所了解。

## http_port 标签

`http_port` 标签配置 Squid 监听代理客户端的 HTTP 端口。默认情况下，Squid 不在任何端口上监听代理客户端。因此，你必须至少打开一个端口让 Squid 使用 `http_port` 标签工作。默认端口是 `3128`，如图 10.9 所示。端口 `8080` 也用于此服务。你可以通过在 `http_port` 标签中包含每个数字来配置 Squid 同时监听两个端口。在接下来的步骤中，你将配置 Squid 为代理客户端监听 `3128` 和 `8080` 端口。

1. 输入以下命令打开 `/etc/squid/squid.conf` 文件：

```
vi /etc/squid/squid.conf
```

2. 按 `i` 进入插入模式。找到 `http_port` 设置：

```
# http_port 3128
```

3. 注释 (`#`) 并输入以下内容向设置中添加端口 `8080`：

```
http_port 3128 8080
```

4. 你的 `http_port` 标签应该类似于图 10.10。

### 图 10.10 配置 http_port 标签以监听端口 3128 和 8080

```
root@24-138-0-170.neme.net ~/squid
File Sessions Options Help
address, then Squid binds the socket to that
address. By configuring the IP address, you can specify
action. Most likely, you do not need to bind to a specific
address, so you can use any port number alone.
The default port number is 3128.
If you are running Squid in accelerator mode, you would
probably want to listen on even ports, or instead
the -command line option will override the -first* port
number listed here. That option will override an IP
address, Number.
You may specify multiple socket addresses on multiple lines.
http_port 3128 8080
-- INSERT
```

![](img/a7a9caa80ec85507179284d91e216f9f_522_0.png)

* syngress.com

5. 点击 `Esc` 退出插入模式。输入以下内容写入：

```
:w
```

## cache_dir 标签

`cache_dir` 标签指定了缓存数据的存储位置。你可以使用多个目录为缓存指定不同的目录。在本演示中，你将使用一个。图 10.11 显示了 `cache_dir` 设置。

![](img/a7a9caa80ec85507179284d91e216f9f_523_0.png)

默认情况下，`cache_dir` 的值为：

```
cache_dir ufs /var/spool/squid 100 256
```

### 表 10.3 定义 cache_dir

| 标签 | 描述 |
| :--- | :--- |
| `cache_dir ufs` | 定义目录。Squid 使用 Unix 文件系统 (`ufs`)。 |
| `/var/spool/squid` | 缓存目录 `/var/spool/squid` |
| `100` | Squid 将存储的缓存数据。默认大小为 100MB。 |
| `16` | 设置子目录的数量。 |
| `256` | 设置二级子目录的数量。 |
