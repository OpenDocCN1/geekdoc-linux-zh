
```
# dhtadm -P
| Name | Type | Value |
| :--- | :--- | :--- |
| 192.168.28.0 | Macro | Subnet=255.255.255.0 Router=192.168.28.28 Broadcast=192.168.28.255 |
| ultra10 | Macro | Include=192.168.28.28 LeaseTime=8640 LeaseNeg=0 domain=xyz.com server=192.168.28.28 UTC=0 |
```

注意，`dhtadm -P` 的输出结果与 `cat` 命令相同，例如查看 `dhcptab` 文件。`dhcptab` 表之所以可读，是因为使用了基于 ASCII 文件的数据存储类型。对 `dhcptab` 表所做的任何更改都需要 DHCP 服务器读取。记住，需要向 `dhcpd` 进程发送 `SIGHUP` `-HUP` 以让它读取 `dhcptab` 表并实施任何已更改。

最常用的 `dhtadm` 选项是：

- `-A` 使用此选项向表中添加并定义符号或宏。
- `-M` 使用此选项修改表中现有的符号或宏。
- `-D` 使用此选项从表中删除现有的符号或宏。
- `-P` 使用此选项打印（查看）`dhcptab` 表的内容。

## 启动和停止 DHCP 服务器

DHCP 服务器在启动时通过启动脚本 `/etc/rc.d/dhcpd` 启动。只有当配置文件 `/etc/inet/dhcp.conf` 存在且配置文件中的 `DAEMON_ENABLED` 变量设置为 `TRUE` 时，`dhcpd` 进程才会启动。

要停止运行的 DHCP 服务器，输入以下命令：

```
ultra10# /etc/rc.d/dhcpd stop
```

这将手动关闭 DHCP 服务器。

要手动启动 DHCP 服务器，输入以下命令：

```
ultra10# /etc/rc.d/dhcpd start
```

## 卸载 DHCP 服务器

如果不再需要 DHCP，或者你希望从系统中移除 DHCP 服务器，可以使用 `dhcpconfig` 命令来卸载服务器并可选地移除主机项和数据库表：

```
ultra# dhcpconfig -U -f
```

选项如下：

- `-U` 这是卸载 DHCP 服务器的选项。
- `-f` 此子选项表示不需要操作确认。如果省略此子选项，在移除 DHCP 服务器之前会显示确认消息。
- `-x` 此子选项移除数据库表。
- `-h` 此子选项移除为托管 IP 地址添加的主机项。

以下示例显示了在省略 `-f` 参数的情况下卸载 DHCP 服务器：

```
ultra@# dhcpconfig -U -h
卸载将停止 DHCP 服务并移除 配置文件。
你确定要卸载 DHCP 服务器吗？([Y]/N): y
DHCP 服务器关闭。
从 dhcpab 中删除了服务器宏。
除了网络 192.168.28.0 的表。
删除了 dhcpab。
删除了配置文件。
```

该命令的第一步是停止服务器进程。然后移除数据库表以及主机项，最后移除配置文件。

注意，主机项从本地 `/etc/hosts` 文件中移除是因为最初配置 DHCP 服务器时指定了此选项。

## 配置 DHCP 客户端

DHCP 客户端的配置过程比 DHCP 服务器简单得多，后者。如果你在安装 Solaris 9 时选择了使用 DHCP，则无需进行其他工作，DHCP 客户端将会被启用。

默认情况下，根据 DHCP 服务器的设置，DHCP 客户端启用动态请求主机名。

要在已经在运行 Solaris 9 的系统上开始使用 DHCP，为主主接口创建一个空文件，并编辑 `/etc/default/dhcpagent` 文件，以便客户端在关闭或重启时释放分配的 IP 地址：

1. 以 root 身份登录客户端。
2. 编辑客户端 DHCP 参数文件 `/etc/default/dhcpagent`。
3. 找到 `RELEASE_ON_SIGTERM=yes` 项。该项默认被注释掉，请取消注释以让客户端在关闭或重启时释放 IP 地址。
4. 创建适当的接口文件以启用 DHCP。例如，如果你的系统有一个 `hme0` 接口，创建文件 `/etc/dhcp.hme0` 如下：

```
ultra5# touch /etc/dhcp.hme0
```

5. 重启客户端。

当你创建空接口文件（如 `/etc/dhcp.hme0`）时，不需要删除对应的原始文件（如 `/etc/hostname.hme0`）。如果你在客户端上禁用了 DHCP，则仍然需要它。

### 配置 DHCP 客户端请求特定主机名

请求特定主机名而非从 DHCP 服务器请求动态主机名的客户端配置略有不同。此处显示了针对使用 `hme0` 网络接口且主机名为 `ultra_test` 的系统的操作步骤：

- 1. 在客户端上以 root 身份登录。
- 2. 编辑默认参数文件 `/etc/default/dhcpagent`。
- 3. 找到 `REQUEST_HOSTNAME=no` 项。默认情况下，该项是被注释掉的，请取消注释并将其修改为 `REQUEST_HOSTNAME=yes`。
- 4. 编辑主机名接口文件，例如 `/etc/hostname.hme0`，并插入以下内容以标识系统主机名为为 `ultra_test`：

```
inet ultra_test
```

- 5. 禁用 `dhcpagent` 进程并删除状态文件（如果存在），操作如下所示：

```
ultra5# kill dhcpagent
ultra5# rm /etc/dhcp/hme0.dhc
```

- 6. 重启客户端。

你应该注意，如果你想在客户端启动时使用 DHCP，仍然需要存在 `/etc/dhcp.<interface>` 文件。如果删除了此文件，DHCP 将不会启动。此外，在指定主机名时，它必须已经在 DHCP 服务器上被配置为具有有效 IP 地址的有效主机名——你不能随意选择任何主机名。

![](img/b8864f367e279929da7f8395589b04dd_258_0.png)

当你选择指定主机名时，DHCP 服务器会首先检查该主机名在网络上已被占用，然后再将其分配给客户端。

## 如何动态更新 DNS

当客户端由 DHCP 服务器分配 IP 地址和主机名时，服务器还可以更新 DNS，使得新的主机名在本地域之外可见。要配置 DNS 动态更新，需要修改 DNS 服务器和 DHCP 服务器。

### 第 11 章

以下步骤显示了如何从 IP 为 `192.168.28.28` 的 DHCP 服务器启用动态 DNS 更新。

- 1. 在 DNS 服务器上，登录并编辑相关区域的 `/etc/named.conf` 文件，更新区域文件项和反向查找项，并添加以下行：

`allow-update { 127.0.0.1; 192.168.28.28 };`

注意，必须更新两个区域项以允许 A 记录和 PTR 记录更新。

此处显示了第 10 章“域名系统 (DNS)”中修改后的 `/etc/named.conf` 文件，以演示动态 DNS 更新的应用：

```
ultra10# cat /etc/named.conf
options {
  directory "/var/named";
}
acl "slaves" {
  {192.168.28.0/24 };
}
zone ".*" in {
  type hint;
  file "named.ca";
}
zone "xyz.com" in {
  type master;
  file "db.xyz";
  allow-transfer {"slaves";};
  allow-update { 127.0.0.1; 192.168.28.28 };
}
zone "28.168.192.in-addr.arpa" in {
  type master;
  file "xyz.rev";
  allow-update { 127.0.0.1; 192.168.28.28 };
}
zone "0.0.127.in-addr.arpa" in {
  type master;
  file "named.local";
}
```

- 2. 如下所示重启 DNS 服务器进程 `in.named`：

`ultra10# pkill -HUP in.named`

- 3. 在 DHCP 服务器上，在 CDE 窗口中输入以下命令启动 DHCP 服务器管理器：

`ultra10# /usr/sadm/admin/bin/dhcpcmgr &`

## 基础动态主机主机配置协议 (DHCP)

出现 DHCP 管理器窗口。图 11.21 显示了一个在 `192.168.28.0` 网络上仅配置了两个 IP 地址的 DHCP 服务器示例。

![](img/b8864f367e279929da7f8395589b04dd_260_0.png)

图 11.21 带有两个 IP 地址的 DHCP 管理窗口。
