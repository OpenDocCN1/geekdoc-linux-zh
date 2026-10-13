
从互联网获取 `"db.cache"` 文件后，忘记将其复制到你安装 DNS 服务器的服务器的 `var/named/` 目录。

# 从用名称服务器

从用名称服务器的目的是与主服务器分担负载，或者在主服务器宕机时处理负载。从用名称服务器通过网络从另一个名称服务器加载数据（通常是主名称服务器，但也可以从其他名称服务器加载）。此过程被称为区域传输（zone transfer）。

设置从用名称服务器所需的文件：

- `named.conf`
- `db.127.0.0`
- `db.cache`
- `named` 脚本

# 从用服务器的 `/etc/named.conf` 文件配置

将此配置用于你网络中作为从用名称服务器运行的服务器。修改从用服务器主机上的 `named.conf` 文件。除 `0.0.127.in-addr.arpa` 之外，将所有的 `primary` 更改为 `secondary`，并如下所示添加带有主服务器 IP 地址的 `masters` 行。

创建 `named.conf` 文件（执行 `touch /etc/named.conf`）并添加内容：

```
options {

  directory "var/named";

  fetch-glue no;

  recursion no;

  allow-query { 208.164.186/24; 127.0.0.8 };

  allow-transfer { 208.164.186.1 };

}
```

```
// 这些文件不属于任何特定区域
zone "*" {
  type hint;
  file "db.cache";
}
```

```
// 这些是我们的从用区域文件
zone "0.0.127.in-addr.arpa" {
  type master;
  file "db.127.0.0";
}
```

```
zone "opens.com" {
  type slave;
  file "db.openna";
  masters { 208.164.186.1 };
}
```

```
zone "208.164.186.in-addr.arpa" {
  type slave;
  file "db.208.164.186";
  masters { 208.164.186.1 };
}
```

# 服务器软件 (BIND/DNS 网络服务) 第4章

这告诉名称服务器它是 `openna.com` 区域的从用服务器，并且应该跟踪主服务器上保留的该区域的版本。

名称服务器不需要通过网络检索所有的数据库 (`db`) 文件，因为这些 `db.openna` 和 `db.cache` 文件与主主服务器上的文件相同，因此你可以在服务器上保留这些文件的本地副本。

从主服务器将 `db.openna` 文件复制到名称服务器。
从主服务器将 `db.cache` 文件复制到名称服务器。

# 所有类型名称服务器的 `/etc/rc.d/init.d/named` 脚本配置

配置你的 `/etc/rc.d/init.d/named` 脚本以启动和停止服务器上的 BIND/DNS daemon。此配置文件适用于所有类型的名称服务器（缓存、主或从）。

创建 `named` 脚本（执行 `touch /etc/rc.d/init.d/named`）并添加内容：

```
#!/bin/sh

# named      此脚本负责启动和停止 BIND/DNS 守护进程。

# description: named (BIND) 域名服务器 (DNS)，用于解析主机名到 IP 地址。

# probe: true

# 来源库：
./etc/rc.d/functions

# 来源网络配置。
./etc/sysconfig/network

# 检查网络是否可用。
[ $NETWORKING = "no" ] && exit 0

[ -f /usr/sbin/named ] || exit 0

RETVAL=0

# 如何调用。
case "$1" in
  start)
    # 启动守护进程。
    echo -n "Starting named:"
    named
    RETVAL=$?
    [ $RETVAL -eq 0 ] && touch /var/lock/named
    echo
    ;;
  stop)
    # 停止守护进程。
    echo -n "Shutting down named:"
    kill named
    RETVAL=$?
    [ $RETVAL -eq 0 ] && rm -f /var/lock/named
    echo
    ;;
  status)
    /usr/sbin/named status
    exit
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  reload)
    /usr/sbin/named reload
    ;;
  probe)
    # named 知道如何重载，我们并不每次都重载
    named reload >/dev/null 2>&1
    ;;
  *)
    echo "Usage: named (start|stop|restart)"
    exit 1
    ;;
esac

exit $RETVAL
```

现在使脚本具有可执行权限并更改默认设置：
`[root@deep ~]# chmod 700 /etc/rc.d/init.d/named`

使用以下命令为 BIND/DNS 创建 rc.d 符号链接：
`[root@deep ~]# chkconfig --add named`

BIND/DNS 脚本在重启服务器时不会自动启动。你可以通过执行以下命令更改默认：
`[root@deep ~]# chkconfig -level 3 on`

使用以下命令手动启动 DNS 服务器：
`[root@deep ~]# /etc/rc.d/init.d/named start`
Starting: [ OK ]

# 安全 BIND/DNS

在 chroot jail 中运行 BIND/DNS
此部分关注防止 BIND/DNS 被用来入侵托管它的系统。由于 BIND/DNS 执行的功能相对大量且复杂，该软件的安全漏洞风险很高。事实上，已经存在漏洞允许远程攻击者获取运行 BIND/DNS 的主机访问。

为了最小化这种风险，可以让 BIND/DNS 以非 root 用户身份运行，这将限制作为本地 shell 普通用户造成的损害。当然，这对于大多数 DNS 服务器的安全要求是不够的，因此可以采取额外的步骤——即在 chroot jail 中运行 BIND/DNS。

`chroot` jail 的主要优势是它将限制 DNS 守护程序可见的文件系统部分为 jail 的根目录。此外，由于 jail 只需要支持 DNS，因此 jail 中与 BIND/DNS 相关的程序可以极其有限。最重要的是不需要 `setuid-root` 程序，这些程序可用于获取 root 权限并跳出 jail。

![](img/a6c32ca5fbc6de5023dbdd2b49130dff_249_0.png)

Linux 上的文件系统。

注意：`named` 二进制程序必须位于 `PATH` 变量列出的目录中才能工作。对于文档的其余部分，我假设原始 `named` 程序的路径为 `/usr/sbin/named`。

以下是在 `chroot` jail 中运行 ISC BIND/DNS 软件所需的步骤：

# 服务器软件 (BIND/DNS 网络服务) | 第 4 章

```
[root@deep #] mkdir /chroot/dev
[root@deep #] mkdir /chroot/named/lib
[root@deep #] mkdir /chroot/named/etc
[root@deep #] mkdir -p /chroot/named/usr/sbin
[root@deep #] mkdir -p /chroot/named/var/run
[root@deep #] mkdir /chroot/named/var
```

现在将主配置文件、区域文件、`named` 和 `named-xfer` 程序复制到 `chroot` 监狱（`chroot` jail）目录的相应位置位置：

```
[root@deep #] cp /etc/named.conf /chroot/named/etc/
[root@deep #] cd /var/ && cp -a /chroot/named/var/
[root@deep #] mknod /chroot/named/dev/null c 1 3
[root@deep #] chmod 666 /chroot/named/dev/null
[root@deep #] cp /usr/sbin/named /chroot/named/usr/sbin/
```
