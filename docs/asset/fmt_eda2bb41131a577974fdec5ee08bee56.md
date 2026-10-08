
### 步骤 2
现在，将 `db.localhost` 文件的权限设置为 `(0664/-rw-r--)`，出于安全考虑由用户 `"named"` 所有。

- 更改 `db.localhost` 文件的权限模式和所有者，使用：
  `[root@deep]# chmod 664 /var/named/db.localhost`
  `[root@deep]# chown named:named /var/named/db.localhost`

# `/var/named/0.0.127.in-addr.arpa`: 反向映射文件
此部分适用于你可能安装在系统上的所有类型的名称服务器（缓存、主或从）。`0.0.127.in-addr.arpa` 文件通过为系统的环回地址提供反向映射来覆盖 localhost 网络。所有类型的 DNS 服务器都需要此配置文件才能正常工作。

### 步骤 1
在 `/var/named` 目录下创建文件。

- 创建 `0.0.127.in-addr.arpa` 文件 (`touch /var/named/0.0.127.in-addr.arpa`) 并文件中添加以下内容：

```
$TTL 86400

      IN SOA      localhost. root.localhost. (

                    00 ; Serial

                  10800 ; Refresh after 3 hours

                  3600 ; Retry after 1 hour

                  60480 ; Expire after 1 week

                  86400 ) Minimum

      IN NS       localhost.

      IN PTR      localhost.
```

### 步骤 2
现在，将 `0.0.127.in-addr.arpa` 文件的权限设置为 `(0644--rw-r--)`，由用户 `'named'` 所有，组权限设置为 `'named'` 出安全考虑。

- 更改 `0.0.127.in-addr.arpa` 文件的模式和所有者，使用：
  `[root@deep]# chmod 644 /var/named/0.0.127.in-addr.arpa`
  `[root@deep]# chown named:named /var/named/0.0.127.in-addr.arpa`

# ISC BIND & DNS 2
第8章

# 加载函数库。

`/etc/init.d/functions`

```bash
# 加载网络配置。
/etc/sysconfig/network
```

```bash
# 如果有额外的选项，则加载该选项。
if [ -f /etc/sysconfig/named ]; then
  /etc/sysconfig/named
fi
```

```bash
# 检查网络是否启动。
[ "${NETWORKING}" = "no" ] && exit 0
```

```bash
# 如果 Named 不可用，则现在停止。
[ -f /usr/sbin/named ] || exit 0
[ -f "${ROOTDIR}"/etc/named.conf ] || exit 0
```

```bash
# Named 二进制文件的路径。
named=/usr/sbin/named
```

```bash
RETVAL=0
prog="Named"
start() {
  echo -n "$Starting prog: "
  if [ -n "${ROOTDIR}" ] != [ -x "${ROOTDIR}" ]; then
    OPTIONS="${OPTIONS}" -t "${ROOTDIR}"
    daemon -u named ($OPTIONS)
    RETVAL=$?
  echo
  [ $RETVAL -eq 0 ] && touch /var/lock/subsys/named
  return $RETVAL
}
stop() {
  echo -n "$Shutting down prog: "
  killproc $named
  RETVAL=$?
  echo
  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/named
  return $RETVAL
}
```

```bash
# 查看我们是如何被调用的。
case "$1" in
  start)
    ;;
  stop)
    stop
    ;
  status)
    status $named
    RETVAL=$?
    ;;
  restart)
    stop
    start
    RETVAL=$?
    ;;
if [ -f /var/lock/subsystems/named ]; then
  stop
  start
  RETVAL=$?
fi
reload() {
  /usr/sbin/bindd reload /dev/null 2>&1 || /usr/bin/killall -HUP $named
  return $RETVAL
}
probe() {
  /usr/sbin/bindd reload /dev/null 2>&1 || echo start
  return $RETVAL
}
echo "Usage: $0 [start|status|restart|condrestart|reload|probe]"
exit 1
esac
exit $RETVAL
```

### Step 2
一旦创建了 `/etc/init.d/named` 文件，更改其默认权限、创建必要的链接并启动它是至关重要的。将此文件设为可执行文件将允许系统运行它；出于安全考虑，将其权限更改为仅允许 root 用户修改；而创建符号链接将让 Linux 的进程初始化（即在系统启动时运行的正常且授权的进程启动）在每次重启系统时自动为你启动该程序。

- `[root@deep] # chmod /etc/init.d/named`
- `[root@deep] # chmod 755 /etc/init.d/named`

- 要为 ISC BIND & DNS 创建符号 rc.d 链接，请使用以下命令：
- `[root@deep] # chconfig --add named`
- `[root@deep] # chconfig --level 235 named on`

- 要手动启动 ISC BIND & DNS 软件，请使用以下命令：
- `[root@deep] # /etc/init.d/named start`
Starting Name: [OK]

# 将 ISC BIND & DNS 作为主服务器运行
本节仅适用于你选择在系统中安装并使用 ISC BIND & DNS 作为主名称服务器的情况。主服务器是关于域信息的终极源头。主服务器是一个配置为一个或多个从名称服务器的区域源的权威服务器。主服务器从磁盘上的文件存储数据。

# `/etc/named.conf`: ISC BIND & DNS 配置文件
此 `named.conf` 配置文件用于你网络中充当主名称服务器的服务器。在任何一个正规的网络环境中，你都需要为你的网络设置至少一个主域名服务器。我们将使用 `"openna.com"` 作为示例域名，并假设你使用的 IP 网络地址为207.35.78.0。当然，你必须更改所有的 IP 网络地址和示例域名以适应你自己的参数。

### Step 1
要执行此操作，请向你的 `/etc/named.conf` 文件添加/更改以下行。**粗粗**部分是配置文件与之前的 `named.conf` 文件不同的部分。不要忘记根据你的需求调整这些值。

- 创建 `named.conf` 文件（`touch /etc/named.conf`）并在文件中添加以下行。以下是我建议你设置的内容：

```bind
// 授权的源地址。
acl "trusted" {
    localhost;
    192.168.1.0/24;
    207.35.78.0/24;
};
```

```bind
// 已知的伪源地址不应被响应。
acl "bogon" {
    0.0.0.0/8;
    1.0.0.0/8;
    2.0.0.0/8;
    192.0.2.0/24;
    192.0.20.0/24;
    198.51.100.0/24;
    203.0.113.0/24;
};
```

```bind
options {
    directory "/var/named";
    allow-transfer { any };
    allow-query { trusted };
    allow-recursion { trusted };
    blackhole { bogon };
    tcp-clients { any };
    forwarders { none };
    version "Linux";
};
```

```bind
logging {
    category lame-servers { };
};
```

```bind
// 根服务器提示
zone "." { 
    type hint; 
    file "db.root"; 
};
```

```bind
// 为回环地址 127.0.0.1/8 提供反向映射
zone "1.0.0.127.in-addr.arpa" {
    type master;
    file "db.localhost";
    notify no;
};
```

```bind
// 为域 207.35.78.0/24 提供反向映射
zone "0.78.35.207.in-addr.arpa" {
    type master;
    file "db.207.35.78";
    notify no;
};
```

```bind
// 我们是 openna.com 的主服务器
zone "openna.com" {
    type master;
    file "db.openna";
    allow-query { any };
};
```

# ISC BIND & DNS v2
第8章

`version "Linux";` 该版本语句允许我们隐藏 ISC BIND & DNS 服务器的真实版本。当来自互联网的尝试扫描我们的域名服务器是否存在存在漏洞的软件版本时，这将非常有用。你可以更改 `"Linux"` 字符串。

`"zone"` 语句使得我们的主名称服务器成为 `"openna.com"`的主服务器。按照常例，`zone` 定义告知 BIND `"openna.com"` 域在其管辖范围内，`type` 定义意味着此 DNS 服务器是 `"openna.com"` 的主服务器，`file` 定义告知软件从哪里找到处理所有域信息的文件，而 `allow-query` 意味着外部主机都可以向我们的主名称服务器查询关于名为 openna.com 域的信息。

这就是我们向主域名服务器定义名称的方法。如果我有另一个域名需要添加到我的主域名服务器，我将按照上面所示的方法进行，但肯定会更改域名和 db 名称以反映新域名相关的名称。

# `/var/named/db.openna`: 地址到主机名的映射文件
本节仅适用于你选择在系统中安装并使用 ISC BIND DNS 作为主名称服务器（Primary Name Server）的情况。请将此配置文件用于网络中作为主名称服务器（Master Name Server）的服务器。`db.openna` 文件将地址映射到主机名。

### 第一步
在你的 `/var/named/named/` 目录下创建该文件。

- 创建 `db.openna` 文件（执行 `touch /var/named/db.openna`）并在文件中添加以下行：

```
$ORIGIN.openna.com.
$TTL 17200
@ IN SOA ns1.openna.com. (
    01 ; Serial
    10800 ; Refresh after 3 hours
    3600 ; Retry after 1 hour
    604800 ; Expire after 1 week
    172800 ); Minimum TTL of 2 weeks
)
```

名称服务器 (NS) 记录。

```
IN NS ns1.openna.com.
IN NS ns2.openna.com.
```

邮件交换 (MX) 记录。

```
MX 0 smtp.openna.com.
```

规范名 (A) 记录的地址。

```
localhost IN A 127.0.0.1
router IN A 207.35.78.1
tgw IN A 207.35.78.2
www IN A 207.35.78.3
smtp IN A 207.35.78.4
```

### 第二步
现在，出于安全考虑，将 `db.openna` 文件的权限设置为 `(0644 /-rw-r--)`，并将所有者设置为用户 `'named'`，组权限也设置为 `"named"`。

- 使用以下命令更改 `db.openna` 文件的权限和所有权：
`[root@deep ]# chmod 644 /var/named/db.openna`
`[root@deep ]# chown named.named /var/named/db.openna`

# `/var/named/78.35.207.in-addr.arpa`: 主机名到地址映射
本节仅适用于你选择在系统中安装并使用 ISC BIND & DNS 作为主名称服务器（Primary Name Server）的情况。该配置文件用于网络中作为主服务器（Master Server）的服务器。`78.35.207.in-addr.arpa` 文件将主机映射到地址。

### 第一步
在你的用户 `/var/named/` 目录下创建文件。

- 创建 `78.35.207.in-addr.arpa` 文件（执行 `touch /var/named/78.35.207.in-addr.arpa`）并在文件中添加以下行：

```
$ORIGIN 78.35.207.in-addr.arpa.
$TTL IN SOA ns1.openna.com. (
01 ; Serial
10800 ; Refresh after 3 hours
3600 ; Retry after 1 hour
604800 ; Expire after 1 week
172800 ; Minimum TTL of 2 days
)
```

名称服务器 (NS) 记录。
```
IN NS ns1.openna.com.
IN NS ns2.openna.com.
```

反向查找指向规范名的地址 (PTR)
```
IN PTR router.openna.com.
IN PTR gtw.openna.com.
IN PTR www.openna.com.
IN PTR smtp.openna.com.
```

### 第二步
现在，出于安全考虑，将 `78.35.207.in-addr.arpa` 文件的权限设置为 `(0644/-rw-r----)`，并将所有者设置为用户 `'named'`，组权限设置为 `'named'`。

- 使用以下命令更改 `78.35.207.in-addr.arpa` 文件的权限和所有权：
`[root@]#] chmod 644 /var/named/78.35.207.in-addr.arpa`
`[root@]#] chown named /var/named/78.35.207.in-addr.arpa`

# 作为从名称服务器（Secondary Name Server）运行 ISC BIND & DNS
本节仅适用于你选择在系统中安装并使用 ISC BIND & DNS 作为从名称服务器（Secondary Name Server）的情况。从名称服务器（Slave Name Server）的目的是与主名称服务器分担负载，或者在主名称服务器宕机时处理负载。

从服务器是一个权威服务器，通过网络从另一个名称服务器（通常是主名称服务器）加载数据，但它也可以从另一个从名称服务器加载。这一过程被称为区域传输（zone transfer）。从服务器用于为网络提供必要的冗余。

# `/etc/named.conf`: ISC BIND & DNS 配置文件
将此配置用于网络中作为从名称服务器的服务器。你必须修改从名称服务器主机上的 `named.conf` 文件。**粗体**文本是文件中与之前的 `named.conf` 相比更改的部分。不要忘记调整值以满足你的需求。

### 第一步
将 `"0.0.127.in-addr.arpa"` 中所有出现的 primary 更改为 secondary，并添加带有主服务器 IP 地址的 master 行。

- 创建 `named.conf` 文件（执行 `touch /etc/named.conf`）并在文件中添加以下行。以下是我的建议内容：

```
// 授权的源地址。
acl "trusted" {
    localhost;
    192.168.1.0/24;
    207.35.78.0/24;
}
// 已知的伪地址不应被响应。
acl "bogon" {
    0.0.0.0/8;
    1.0.0.0/8;
    2.0.0.0/8;
    192.0.2.0/24;
    224.0.0.0/8;
    // 企业网络可能不是虚假的。
    10.0.0.0/8;
    172.16.0.0/12;
```
