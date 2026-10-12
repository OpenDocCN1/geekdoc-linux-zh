
## 所有的 BIND 消息都存储在 /var/log/syslog

# LinuxDeveloper 教程

这是关于 `LUKS` 设备的基本信息，它显示了加密、模式、哈希算法和其他加密数据。

此命令生成 `LUKS` 头部转储。所有的 `LUKS` 命令后面都可以跟一个命令：

```bash
$ user@ubuntu:~$ sudo cryptsetup -v /dev/sda1 /home/nitish/basefile

LUKS header Information for /home/nitish/basefile

cryptdm:

  name:        aes

  cipher:      plain64

  Hash algo:   sha256

  Payload offset: 4096

  Salt:

    d7 33 09 8e 11 1f 74 24 69 64 67 74 8c 15 1c 79 36 27 43

    17 2d 23 07 20 44 24 27 2c 21 21 3b 33 3d 80

  UUID:

    bc0a490d-8d2a-4f22-b5f9-fc25d3bd

iterations: 191616

Key Slot 0: ENABLED

  Salt:

    72 33 71 4c 68 40 63 82 65 64 61 63 65 52 57 23 65 8f

    b9 0c 63 64 77 79 48 62 85 55 28 37 23 8c 0

AF offset: 4000

Key Slot 1: DISABLED

Key Slot 2: DISABLED

Key Slot 3: ENABLED

Key Slot 4: DISABLED

Key Slot 5: DISABLED

Key Slot 6: DISABLED

nitish@ubuntu:~$
```

## 创建缓存 DNS 服务器

减少网络流量并更快速地响应 `DNS` 请求

![](img/7b0011b9ca05b82c33c02a484fd02e99_40_0.png)

```bash
$ host -t ns linuxer.co.uk linode

; connection timed out; rmBook:Downloads mtsouk$

$ host -t ns linuxer.

Using dns server:

Name: Linode

Address: 109.74.193.253#53

Aliases:

linuxer.co.uk server ns.hosteurope.com.

linuxer.co.uk server ns2.hosteurope.com.

$ host -t ns linuxer.co.uk linode

Using dns server:

Name: Linode

Address: 109.74.193.253#53

Aliases:
```

对于本教程而言，最有用的工具是 `named-checkconf`，它会检查配置（ACL）的语法有效性。如果你的当前配置没有错误，将不会有任何输出。没有任何工具可以检测本地 `DNS` 错误。

| OPTION | DOMAIN |
| --- | --- |
| AUTHORITY | |
| QUESTION | |
| ANSWER | |
| AUTHORITY | |
| SECTION | |
| AUTHORITY | |
| AUTHORITY OPTION | |

### 12 使用缓存 DNS 服务器

缓存服务器就像一个大型 `DNS` 服务器。如果你想减少局域网（`LAN`）的流量，将缓存服务器的 IP 放入 `/etc/resolv.conf` 文件中，而不是所有的其他 `DNS` 服务器。然而，如果缓存服务器停止工作，可能会导致问题；你的网络将无法运行。

### 14 访问控制列表 (ACL)

`acl` 列表定义了哪些主机可以访问 `DNS` 服务器。以下行定义了一个新的访问控制列表：

### 16 测试缓存 DNS 服务器

要测试你的 `DNS` 服务器，请查询一个不在缓存中的查询，并查看回答该查询需要多久。接下来再次查询相同的 `DNS` 查询，查看更好的响应时间。

```acl
acl OTENET {

  2/8;

  localhost;

  localnets;

};
```

列表的定义不会自动使其激活。你应该添加以下行来开启 `OTENET` 访问控制：

```acl
allow-query { any };
```

随着 `DNS` 服务器开始运行，许多主机将尝试连接它；因此，不要延迟生成任何访问列表，以保护你的 `DNS` 服务器。

### 17 缓存服务器的优势

在网络上使用缓存 `DNS` 服务器的优势是局域网流量和互联网速度。你的 `DNS` 服务器会对已经请求过的查询做出快速响应。`BIND` 有一个内存计数器，可以将所有到 `DNS` 服务器的请求转储，并在时间到达时重新读取这些内容。

### 13 BIND 的日志

所有的 `BIND` 消息都记录在 `/var/log/syslog` 中。`named` 命令可能会产生大量消息，因此你可能决定在确保你的 `DNS` 服务器运行无任何问题后，使用 `named` 降低日志级别。

### 15 检查你的配置

`BIND` 自带了许多工具，可以帮助你检查当前配置的正确性。这些工具包括 `named-checkzone` 和 `named-checkcompile`。

```bash
$ rndc dumpdb --all

# > /var/cache/bind/named_dump

# -r -r 1 bind 9446 Oct 15 11:15/var/cache/bind/named_dump
```

## 所有的来自 BIND 的消息都存储在 /var/log/syslog

# Linux 开发者教程

## 04 创建目标文件

现在 `cryptsetup` 已经成功安装，我们需要创建一个文件系统作为 `LUKS` 容器的占位符。创建文件有很多方法，但有几点需要注意：

- 文件应该是一个非稀疏文件（nonsparse file），这意味着合并设备应该被分配完整的磁盘空间。
- 文件中应该填充随机数据，确保它不是完全空的，这样数据才能从根本上被加密。

`dd` 命令虽然速度有点慢，但可以帮助创建一个满足上述要求的文件。只需使用 `/dev/random` 作为输入，目标文件作为输出即可。示例命令如下：

```
dd if=/dev/random of=/home/nitish/basefile bs= count=1
```
