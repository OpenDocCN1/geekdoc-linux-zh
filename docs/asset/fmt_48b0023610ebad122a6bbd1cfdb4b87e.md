
| 3600000 | NS | L.ROOT-SERVERS.NET.<br>198.32.64.12 | |

| | 360000 | A | |

由 WDOE 运营

- M.ROOT-SERVERS.NET.

| | | | | | |

| :--- | :--- | :--- | :--- | :--- |

| 3600000 | NS | M.ROOT-SERVERS.NET.<br>202.127.0.33 | |

| | 360000 | A | |

- 文件结束

此文件包含 NS 和 A 记录，指定了根区域的权威名称服务器名称及其地址（由每个记录第一个字段中的分号指示）。文件中的注释行提供了根名称服务器位置的提示。共有十个根名称服务器；大部分位于美国。对于任何名称服务器来说，访问至少一个根名称服务器都是必须的。

## `/var/named/localhost.zone` 文件

`/etc/named.conf` 文件包含一个 `localhost` 区域语句，指定区域文件位于 Fedora Core 系统的 `/var/named` 目录。以下是 `/var/named/localhost.zone` 文件的内容：

```
$TTL 86400
$ORIGIN localhost.
@ 1D IN SOA
@ root ( serial (adams)
      42
      3H : refresh
      15M : retry
      1W : expiry
      1D ) minimum

1D IN NS
@ 1D IN A
127
```

该区域文件以 `$TTL` 指令开头，将后续记录的默认 TTL 设置为一天（86000 秒）。，`$ORIGIN` 指令将域名设置为 `localhost`。这两个指令之后，`/var/named/localhost.zone` 文件包含三个资源记录（RR）：一个 SOA 记录、一个 NS 记录和一个 A 记录。SOA 和 NS 记录指定 `localhost` 为主服务器。A 记录指定了 `localhost` 的地址为 127.0.0.1。

## `/var/named/named.local` 文件

`/etc/named.conf` 中的第三个区域语句指定了反向映射区域 `0.1.127-in-addr.arpa`。对于该区域，文件是 `/var/named/named.local`，内容如下：

```
$TTL 86400
@ IN SOA localhost. (
2700 : Serial
2800 : Refresh
14400 : Retry
360000 : Expire
86400 ) Minimum

IN NS localhost
```

SOA 和 NS 记录指定 `localhost` 为主名称服务器。SOA 记录还显示了域联系人的电子邮件地址（区域格式）。向该联系人发送电子邮件时，必须将第一个点替换为 `@` 并删除最后一个点。

## 缓存名称服务器：启动与测试

现在你已经有了缓存名称服务器的配置文件，可以启动名称服务器并使其运行。要启动名称服务器，请以 `root` 身份登录并在终端输入以下命令：

```
service named start
```

此命令启动 `named` 守护进程。要确保名称服务器在每次重启系统时启动，请以 `root` 身份登录并输入以下命令：

```
config named
```

## 配置 DNS

`named` 服务器会将诊断信息写入 `/var/log/messages`。启动 `named` 后，可以通过文本编辑器打开 `/var/log/messages` 查看消息。如果没有来自 `named` 的错误消息，就可以继续测试服务器。在使用缓存服务器之前，你必须指定一个名称服务器为主。为此，请确保 `/etc/resolv.conf` 中的第一行如下：

```
nameserver 127.0.0.1
```

现在你可以使用 `host` 测试名称服务器。例如，使用 `localhost` 上的缓存服务器查询 `www.google.com` 的 IP 地址，请输入以下命令：

```
host www.google.com localhost
```

这是 `host` 命令的预期输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
www.google.com has address 142.250.190.46
```

由于 `host` 命令使用 `localhost` 作为 DNS 服务器并返回 `www.google.com` 的 IP 地址，如果你得到类似的输出，说明缓存服务器已启动运行。

## 配置主名称服务器

配置主名称服务器的最佳方法是从配置缓存服务器开始（如前几节所述）。然后，为你想要让此服务器作为主名称服务器的域名添加主区域（master zones）。例如，假设我想为 `naba.net` 域名定义一个主名称服务器。以下是我配置该名称服务器的步骤（登录 `root` 之后）：

1. 在 `/etc/named.conf` 文件中添加以下区域语句：

```
zone "naba.net" {
  type master;
  file "naba.zone";
}
zone "168.192.in-addr.arpa" {
  type master;
  file "168.92.zone";
}
```

2. 创建 `/var/named/naba.zone` 文件并包含以下内容：

```
$TTL 86400
$ORIGIN naba.net.
@ IN SOA
root.naba.net. (
    100 : serial
    36000 : refresh
    14400 : retry
    60400 : expiry
    86400 ) minimum

1D IN NS @
1D IN A 192.168.0.7
```

```
XP A 192.168.0.2
```

3. 创建 `/var/named/168.92.zone` 文件并包含以下内容：

```
$TTL 86400
; Remember zone name is: 168.192.in-addr.arpa
@ IN SOA naba.net.root.naba.net. (
    1 : serial
    28000 : refresh
    14400 : retry
    360000 : expire
    86400 ) minimum

IN NS naba.net.
```

```
7 IN PTR naba.net.
2 IN PTR xp.naba.net.
```

4. 要测试新配置，使用以下命令重启名称服务器：

```
service named restart
```

5. 使用 `dig` 或 `host` 查询 DNS 服务器。例如，这里是我如何使用 `host` 命令在 `localhost` 上运行的 DNS 服务器检查 `xp.naba.net` 的地址：

```
host xp.naba.net localhost
```

这是 `host` 命令返回的输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
xp.naba.net has address 192.168.0.2
```

### 694 配置 DNS

如果你想使用 `dig` 来检查 DNS 服务器，请输入以下命令：

```bash
dig @localhost wpx.naba.net
```

这个 `@localhost` 部分指定了 `dig` 连接的 DNS 服务器。

当你成功使用 `dig` 连接到 DNS 服务器时，你可以对该服务器执行一些更复杂的操作。例如，这里是我尝试对 IP 地址 `192.168.0.2` 进行反向查找时输入的命令：

```
host 192.168.0.2 localhost
```

此命令显示如下输出：

+   Using domain server:

Name: localhost

Address: 127.0.0.1#53

Aliases:

```
2.0.168.192.in-addr.arpa domain name wpx.naba.net
```

# 第 6 章：运行 Samba 和 NFS

本章内容

- 使用 NFS 共享文件

- 使用 NFS 服务器配置向导

- 安装和配置 Samba

- 使用 Samba 建立 Windows 服务器

你的局域网与许多网络一样，它需要在运行 Linux 的系统与其他非 Linux 系统之间共享文件的能力。此 Fedora Core 包含了两个主要的文件共享服务：

- 网络文件系统 (`NFS`) 用于与其他 UNIX 系统（或安装了 NFS 客户端软件的 PC）共享文件

- `Samba` 用于与 Windows 系统进行文件共享和打印共享。

在本章中，我将描述如何使用 `NFS` 和 `Samba` 共享文件。

## 使用 NFS 共享文件
