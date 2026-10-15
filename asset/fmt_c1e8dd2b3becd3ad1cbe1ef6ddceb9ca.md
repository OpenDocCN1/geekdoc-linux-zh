
我们将为每个新的子网络创建一个区域，并为每个新区域创建一个名称服务器。新的名称服务器将连接到它们所服务的子网络。

新配置将需要对单域/区域（在“配置基础 DNS 服务器”部分中描述）进行以下修改：

- 保留 `chivas` 作为 `paunchy.net` 域的主名称服务器：`Chivas` 将被修改以充当新子域名的辅助名称服务器。它的 `named.conf` 文件将需要修改，但它的区域文件保持不变。
- 为新子域名 `lab.paunchy.net` 和 `syseng.paunchy.net` 创建主名称服务器：新服务器分别为 `pachuca` 和 `toluca`。

假设你创建了两个 Linux 节点作为名称服务器，你必须执行以下步骤来修改之前的示例以与新的子域名配合：

- 如下所示，在 `chivas` 的 `/etc/named.conf` 中添加新区域：

```
options {
  directory "/var/named";
}

zone "." {
  type master;
  file "root.zone";
}

zone "localhost" {
  type master;
  file "localhost.zone";
}

zone "paunchy.net" {
  type master;
  file "paunchy.zone";
}

zone "lab.paunchy.net" {
  type slave;
  file "lab.paunchy.zone";
  masters { 192.168.1.250 };
}

zone "syseng.paunchy.net" {
  type slave;
  file "syseng.paunchy.zone";
  masters { 192.168.1.250 };
}

zone "192.168.2.0" {
  type slave;
  file "192.168.2.0.zone";
  masters { 192.168.1.250 };
}

zone "192.168.3.0" {
  type slave;
  file "192.168.3.0.zone";
  masters { 192.168.1.250 };
}
```

# 第三部分：提供基础 Internet 服务

`xferkey` 选项是一个任意的文件名前缀，用于存储结果。

从以 `.private` 为后缀的结果文件中提取共享密钥。该 `.private` 文件的内容类似于所示：

```
Private-key-format: v1.2
Algorithm: 157 (HMAC-MD5)
Key: ByrncuulmYoA8fLXQYTog==
```

字符串 `ByrncuulmYoA8fLXQYTog==` 代表该密钥。

- 按照如下方式将密钥放入 `/etc/named.conf` 文件中：

```
key xferkey;
algorithm hmac-md5;
secret "ByrncuulmYoA8fLXQYTog==";
```

- 将包含密钥的 `named.conf` 密钥部分复制到第二台机器。在这种情况下，第二台机器是 `pachuca`：

```
key xferkey;
algorithm hmac-md5;
secret "ByrncuulmYoA8fLXQYTog==";
```

- 在 `chivas` 的 `named.conf` 上添加以下部分，以强制 `chivas` 的 `named` 在允许传输到 `pachuca` 之前验证密钥：

```
server 192.168.1.251 {
keys ( xferkey; );
}
```

- 在 `pachuca` 的 `named.conf` 上添加以下内容，以允许来自 `chivas` 的区域传输：

```
server 192.168.1.250 {
keys ( xferkey; );
}
```

- 重启两台机器上的 `named`：

```
/etc/init.d/named restart
```

在你在两台机器上都配置了 TSIG 之后，没有其他名称服务器可以执行区域传输。主服务器。

# 在 chroot 环境中运行 named

`chroot` 命令创建一个虚拟文件系统。该虚拟文件系统的根目录被设置在现有文件系统内的某个任意点。经过“chroot”处理的文件系统限制了运行在其内部的进程对受限文件系统的访问。这种受限的环境增强了安全性，因为入侵者无法获得像往常那样的工具。

通过 `named` 访问系统的黑客始终是一个危险因素。`named` 设计用于响应外部网络查询，是一个广受欢迎的目标。在 `chroot` 环境中运行 `named` 增加了其安全性。任何发现并利用 `named` 漏洞的人都被限制在 `chroot` 内部工作。我们将创建一个几乎不包含任何可供操作的 `chroot` 环境。

`chroot` 文件系统必须包含所有的应用程序、库和杂项系统。幸运的是，`named` 运行只需要几个系统。我们将创建一个任意目录 `/chroot` 作为 `chroot` 环境的根目录。`/chroot` 内部所需的目录有 `/chroot/etc`、`/chroot/var/run` 和 `/chroot/var/named`。

将 `named` 配置文件从 `/etc` 移动到 `/chroot/etc`，从 `/var/named` 移动到 `/chroot/var/named`；这些文件名为 `named.conf`、`hints.db`、`localhost.zone`、`paunchy.zone` 和 `192.168.192.zone`。`/chroot` 目录应包含以下文件：

- `/chroot/etc/named.conf`
- `/chroot/var/run`
- `/chroot/var/named/hints.db`
- `/chroot/var/named/localhost.zone`
- `/chroot/var/named/paunchy.zone`
- `/chroot/var/named/192.168.192.zone`

按照如下所示向 `/etc/rc.d/init.d/named` 脚本中添加以下行：

```
OPTIONS=-t named
ROOTDIR=/chroot
```

`OPTIONS` 参数强制 `named` 守护进程在用户空间运行；该用户专门用于运行 `named` 守护进程。设置 `ROOTDIR` 变量强制 `named` 在 `chroot` 环境中运行；在这种情况下，`named` 运行在根于 `/chroot` 的 `chroot` 环境中。

# 启动和停止名称服务器

`/etc/rc.d/init.d/named` 脚本控制 `bind9` 守护进程并提供有关运行服务的信息。通过运行带 `start` 参数的脚本来启动守护进程：`/etc/rc.d/init.d/named start`。通过使用 `stop` 参数停止 `named`：`/etc/rc.d/init.d/named stop`；你可以如下方式重启它：`/etc/rc.d/init.d/named restart`。你可以通过向 `named` 守护进程发送 `HUP` 信号来强制 `named` 重新读取配置：`killall -HUP named`。

或者，你可以使用与 `bind` 包的 `rndc` 工具。如果你不指定任何选项，`rndc` 将显示 `named` 的状态。根据你给 `rndc` 的选项，它将启动和停止 `named` 守护进程。`rndc` 还可以配置为使用密钥向 `named` 进行身份验证。

# 创建多个区域文件

本节扩展了之前的示例以包含额外的子域名。我们将为每个子域名创建一个额外的区域。此示例扩展了 `paunchy.net` 域以包含两个新的子域名：`lab.paunchy.net` 和 `syseng.paunchy.net`。新的子网络将使用不可路由的网络地址 `192.168.2.0` 和 `192.168.3.0`，并通过第 1 章描述的三网口 Linux 路由器路由到 `paunchy.net`—`192.168.1.0`。

> 我们将在我们的官方 `paunchy.net` 域内完全管理这些子域名；我们不需要向 InterNIC 注册这些子域名。

我们将为每个新的子网络创建一个区域，并为每个新区域创建一个名称服务器。新的名称服务器将连接到它们所服务的子网络。

新配置将需要对单域/区域（在“配置基础 DNS 服务器”部分中描述）进行以下修改：

- 保留 `chivas` 作为 `paunchy.net` 域的主名称服务器：`Chivas` 将被修改以充当新子域名的辅助名称服务器。它的 `named.conf` 文件将需要修改，但它的区域文件保持不变。
- 为新子域名 `lab.paunchy.net` 和 `syseng.paunchy.net` 创建主名称服务器：新服务器分别为 `pachuca` 和 `toluca`。

假设你创建了两个 Linux 节点作为名称服务器，你必须执行以下步骤来修改之前的示例以与新的子域名配合：

- 如下所示，在 `chivas` 的 `/etc/named.conf` 中添加新区域：
