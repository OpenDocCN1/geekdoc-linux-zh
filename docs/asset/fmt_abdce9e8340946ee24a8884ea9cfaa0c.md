
在此情况下，特殊选项用于传递远程 IP 可访问的的名称；因此，发往该网络的所有数据包都可以通过远程 IP 进行路由。

现在我们将讨论 `ip-up` 脚本的“相反”脚本，称为 `ip-down`。当点对点链路断开（掉线）时，就会调用该脚本。因此，`ip-down` 脚本的作用是在 `ip-up` 脚本之后进行清理工作、移除路由等。以下是一个基础 `ip-down` 脚本示例：

```
#!/bin/sh
# ip-down <interface> <myaddr> <daemon.pid> <local> <#remote> <arg>

# ip-down 脚本示例。
# 它在设备关闭后，将以与 ip-up 相同的参数被调用。
# 它可以用于移除代理 ARP，或者（如此处所示）
# 用于日志记录等目的。

umask 022
PATH=/bin:/bin:/usr/sbin:/usr/usr/bin

# 日志示例
now=date "+%b %d %T"
echo "$now - interface $1 is down: $**" >> /var/log/cipe.log

# 移除进程 PID 文件
rm -f /var/run/cipe/$6.pid /var/run/cipe/$1.pid

route del -net sk netmask 255.255.255.0

# 如果系统运行了 gated，告诉它发生了什么
#gdc  interface
```

```
exit 0
```

该脚本简单地记录了 CIPE 点对点链路掉线的事实，并移除了通过该链路可访问的远程网络的路由。

# CIPE 配置

## 在 gated 中使用 CIPE

请注意，如果你运行 `gated`（网关路由守护进程），你应该将与 CIPE 隧道相关的静态路由条目放在 `/etc/gated.conf` 中。实现此点的更简单方法是通过直接调用 `gated` 的用户界面工具 `gdc` 来通知 `gated` 接口配置的变化。前述 `ip-down` 脚本的最后四行显示了一个简单的命令，将告诉 `gated` 重新检查接口配置。只需删除 `gdc interface` 命令前的注释标记 `#` 即可启用它。

## 使用多个配置文件

如果你想使用多个 CIPE 连接，你需要一种方法根据每次连接选择不同的 `options`、`ip-up` 和 `ip-down` 文件。你可以通过为连接分配唯一名称并为每个名称创建一组配置文件来实现。

例如，如果你有三个 CIPE 隧道 `bbone`、`telework` 和 `v42b`，你可以为每个隧道创建一个目录，并将 `options`、`ip-up` 和 `ip-down` 文件复制到这些目录。然后你应该修改每个 `options` 文件以指向正确的 `ip-up` 脚本。例如，`bbone` 的 `options` 文件可能如下：

```
ptaddr 10.1.3.1
ipaddr 10.1.3.2
me bbone.rtr-1.uucp-nonex.com:9999
peer bbone.rtr-2.europe-nonex.com:9999
ipup /etc/cipe/bbone/ip-up
ipdown /etc/cipe/bbone/ip-down
key 458b9002adf9c00ccf99ecc2393bbbb3e4
```

如你所示，`ipup` 和 `ipdown` 选项通常指向专门为适应 `bbone` 接口定制的相应 `ip-up` 和 `ip-down` 脚本。

随后，每当你想要运行 `ciped` 时，都应该通知它你想使用哪个 `options` 文件。例如：

```
[root@fox cipe-1.5.1]# ciped-cb -o /etc/cipe/options
```

# /etc/cipe/options 支持的参数列表

在这里我们描述 CIPE 版本 1.5.1 支持的参数/选项。参数列表由两部分组成：第一部分描述所需的参数，第二部分给出了可选参数列表。表 9.1 列出了每个参数选项。

## 表 9.1 /etc/cipe/options 的必选和可选参数

| 参数/选项 | 格式 | 描述 |
| --- | --- | --- |
| `ipaddr` | IP | 点对点 CIPE 链路本地侧的 IP 地址。 |
| `ptaddr` | IP | 点对点 CIPE 链路对等端的 IP 地址。 |
| `me` | IP:port | 本地 CIPE IP 地址。 |
| `peer` | IP:port | CIPE 对等端的 IP 地址。 |
| `key` | 十六进制字符串 | 128 位共享密钥。 |
| `device` | String | CIPE 设备的名称。如果未提供，系统将选择一个空闲的。 |
| `debug` | Bool | 关闭；使用 stderr 代替 syslog。 |
| `mask` | IP | 子掩码。 |
| `bcast` | IP | CIPE 广播地址。 |
| `mtu` | Int | CIPE 设备的最大传输单元。 |
| `cttl` | Int | TTL 存活。 |
| `nockey` | Bool | 不加密。 |
| `socks` | IP:port | socks 地址和端口。 |
| `toxt` | Int | 密钥交换的超时时间。 |
| `tokey` | Int | 密钥有效期。 |
| `ipup` | String | 运行的 `ip-up` 脚本。 |
| `ipdown` | String | 运行的 `ip-down` 脚本。 |
| `arg` | String | 参数。 |

## 可选参数（续）

| 参数/选项 | 格式 | 描述 |
| --- | --- | --- |
| `maxerr` | Int | 允许错误次数。 |
| `ping` | Int | 探测的频率。 |
| `to` | Int | 超时时间。 |
| `dynip` | Bool | 动态 IP。 |
| `hwaddr` | String | MAC 地址。 |
| `ifconfig` | Bool | 接口配置。 |
| `checksum` | Bool | 使用校验和。 |

# 基于 CIPE 的配置

本部分将解释如何配置 CIPE。

## 设置密钥与身份

首先，每个使用 CIPE 的主机都必须有一个 `identity`。`identity` 包含两个文件：`identity` 和 `identity.priv`，它们分别代表公钥和私钥。这些文件由 `rsa-keygen` 脚本（`openssl` 命令行工具的封装）生成，该脚本包含在 CIPE 部分中。

### /etc/cipe/identity

注意 `/etc/cipe/identity.priv`（主机的私钥）必须仅供 root 读取。例如，你可以执行以下操作：

```
[root@cipe] chmod 400 /etc/cipe/identity.priv
[root@cipe] ls -l /etc/cipe/identity.priv
--------------- 1 root root 887 May 6 23:27 /etc/cipe/identity.priv
```

如果你之前创建了目录，身份文件已经在 `/etc/cipe` 中。如果由于某种原因它们不存在，你可以输入以下命令生成新的身份：

```
[root@cipe] rsa-keygen /etc/cipe/identity 1024
warning, not much extra random data, consider using the -rand option
Generating RSA private key, 1024 bit long modulus
+++++
+++++
  e is 65537 (0x10001)
read RSA key
writing RSA key
Private key in /etc/cipe/identity.priv, Public key in /etc/cipe/identity
```

### /etc/cipe/pk/*

记住，对于你想建立的每一个主机，都需要一个公钥。公钥存储在 `/etc/cipe/pk` 中，就是与你交互的主机的 `/etc/cipe/identity` 文件。

例如，如果你想连接 `juno.testbed.com`，你需要将该主机的 `/etc/cipe/identity` 复制到你的 `/etc/cipe/pk` 目录，并将其重命名为 `/etc/cipe/pk/juno`。对方必须将你的 `identity.pub` 复制到 `/etc/cipe/pk` 并以你的主机名命名。

## 公钥文件的命名

在对端主机上，你的公钥/身份文件的命名方式重要吗？实际上，这很重要。因为你的 `pkcipe` 将把其身份发送到远程端，而该名称将用于在 `/etc/cipe/pk` 中搜索公钥/身份文件 `pkcipe` 目前使用 `gethostname()` 调用来获取你的主机名。或者，你也可以在调用 `pkcipe` 的命令行中将名称作为最后一个参数传递给 `pkcipe`。只需使用以下命令：

```
[root@fox pk]# hostname -s
fox
```

因此，你可能会在 `/etc/cipe/pk` 目录中拥有多个不同主机的公钥。例如：

```
[root@fox pk]# ls -l /etc/cipe/pk
total 28
-rw-r--r-- 1 root 272 May 23:17 aleste
-rw-r--r-- 1 root 272 May 23:13 bravo
-rw-r--r-- 1 root 272 May 23:15 centipede
-rw-r--r-- 1 root 272 May 23:13 dexter
-rw-r--r-- 1 root 272 May 23:16 goonies
-rw-r--r-- 1 root 272 May 23:16 metal-gear
```

## 在公钥文件中保留选项

通过 `pkcipe`，你只能在 `/etc/cipe/options` 文件中添加影响所有连接的全局选项。如果你想添加特定于连接的选项，可以根据对端将它们添加到 `/etc/cipe/pk` 中的公钥中。为了说明，以下是为我们使用的一个远程主机添加了选项的示例公钥文件（`/etc/cipe/pk/dexter`）：

```
---BEGIN PUBLIC KEY----
MIGMA0QCS5G3B3OEBAQAAANADCCBIGkBgQ5Qt2tVbJdZee67Kk0+t6dR
ag25GCAvPg5d0bUGEQK/pcbub4Y0Gnx1Ic7jDuRfLH5cFTAteCaIHJDQIDVm
6Shb0ltXn5rVbBlkkorur3UIJtVdnWKc16MgQt+Kazc3VcX/1xCTTd2ZZ
UpPAAAyQgRp4drBzTYWIQAB
---END PUBLIC KEY---
```

```
ptpaddr         10.1.1.5
ipaddr         10.1.1.6
```

```
me              zyxel.erie.nonex.com:9999
peer            peer.erie.nonex.com:3001
```

```
debug           1
maxerr         3
```

```
ipup            /etc/cipe/dexter/ip-up
ipdown         /etc/cipe/dexter/ip-down
```

如你所见，前面的文件包含远程端的公钥以及与远程端连接相关的选项。这些选项将覆盖 `/etc/cipe/options` 中指定的所有全局选项。因此，在每个公钥文件中，你可以定义特定于对端的配置。

## 在 ip-up 脚本中添加一行以适配 pkpcipe

确保你在前述选项文件中引用的 `ip-up` 脚本包含以下行（来自 CIPE 分发包中 `pkpcipe/` 目录下的默认 `ip-*` 脚本）：

```
# Create/update PID file.
echo $3 $1 >/var/run/cipe/${6:-1}.pid
```

# pkpcipe 和入站连接

按照前面的解释设置好所有必要的密钥后，你需要决定如何运行 `pkcipe`。在做决定时，你需要记住 `pkpcipe` 使用 TCP 交换密钥，其中一方必须作为服务器，另一方作为客户端。

## 选项 1：从 inetd 或 xinetd 派生 pkpcipe

有几种可能的设置。可能最优雅的方法是使用 `inetd`（或 `xinetd`）将 `pkpcipe` 作为一个服务，在入站连接到达时派生。在这种情况下，你不需要担心执行 `ciped` 进程（每个进程都有不同的选项文件等等）。相反，`pkpcipe` 负责身份验证和密钥协商；如果一切正常，它将为每个连接派生 `pkcipe`。

在这种情况下，你需要做的是在系统上为 `pkpcipe` 指定单个端口（只需操作一次），并将其添加到 `inetd/xinetd` 配置中。因此，每当客户端 `pkcipe` 进程通过 TCP 连接到服务器管道时，它会传输其身份（例如 `dexter`），通过使用 `/etc/cipe/` 目录中的客户端公钥进行验证。随后，`pkpcipe` 会派生 `pkcipe`。

以下是关于如何将 `pkcipe` 添加为可执行服务的详细说明。首先，查看 `/etc/services` 并向文件中添加以下行（9950 是与 `pkpcipe` 服务关联的端口号）：

```
pkpcipe 9950/tcp
```

然后在在 `/etc/inetd.conf` 文件的末尾添加一行，如下：

```
pkpcipe stream nowait root /usr/local/sbin/pkpcipe pkpcipe
```

如果你倾向于使用 `xinetd` 包装器，如下：

```
pkpcipe stream nowait root /usr/local/sbin/pkpcipe
```

简单来说，该行告诉 `inetd` 在此后执行 `pkpcipe`。因此，每当客户端 `pkcipe` 进程通过 TCP 连接到服务器管道时，它会传输其身份（例如 `dexter`），通过使用 `/etc/cipe/` 目录中的客户端公钥进行验证。随后，`pkpcipe` 会派生 `pkcipe`。
