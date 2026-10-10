
编辑 `squid.conf` 文件 (`vi /etc/squid/squid.conf`) 并添加：

```
http_port 80
icp_port 0
acl QUERY query regex \?
obj_cache deny QUERY
cache_mem 16 MB
cache_dir ufs /cache 200 16 256
emulate_httpd_log on
direct_rewrite_host_header off
replacement_policy GDSF
acl all allow
httpd_accel off
```

关于此页面的意见和建议请邮寄至 gmouriani@videotron.ca

GDFS 通过在缓存中保留较小的热门对象来优化命中率，从而有更大的命中机会。由于它会驱除（可能的）较大的对象，因此它比 LFUDA 具有更低的比特率。

LFU 无论对象大小如何都将热门对象保留在缓存中，因此以牺牲命中率率为代价来优化命中率；一个巨大的热门对象会阻止许多较小的、流行程度稍低的对象被缓存。

![](img/4444dd2a96323af53b5149a2b33efe8b_292_0.png)

图 1：SPECWeb 命中率

1 和 2 显示了 Squid 2 在 SPECWeb 负载和 http 负载中的实现命中率。在命中率方面，原始的 SPECWeb 验证与此揭示之间的差异很小，相对顺序没有改变，且曲线的形状大致相似。SPECWeb 版本中的策略变异更大，并注意 http 测试的运行时间略长。

图 2：http 命中率

这是惠尔惠惠公司 1999 年的图表。

### half_closed_clients

此选项 `half_closed_clients` 如果设置为 off，会告诉 Squid 在 `read(2)` 返回无可读数据时立即关闭客户端连接；某些客户端可能会关闭 TCP 连接的一端，而保持其接收端开启。有时，Squid 无法区分半关闭和完全关闭的 TCP 连接。

### acl all 0.0.0.0/0 and http_access allow all

这些选项 `acl` 和 `http_access` 定义了一个访问控制列表。请参阅您的文档获取更多信息。`acl` 和 `http_access` 允许所有人连接到代理服务器，我们使用此代理来加速我们的 Web 服务器。

### cache_mgr_admin

此选项 `cache_mgr_admin` 指定本地缓存管理员的电子邮件地址，如果缓存崩溃，该地址将收到邮件。

### cache_effective_user squid and cache_effective_group squid

此选项 `cache_effective_user` 和 `cache_effective_group` 指定了缓存运行的 UID:GID。这是一个安全功能，你绝不能以 `root` 用户运行 Squid。在我们的配置中，我们使用 `Squid` 和 GID `squid`。

### httpd_acc_host 208.164.186.3 and httpd_acc_port 80

© Copyright 1999 Open Network Architecture ®

配置选项 `httpd_accel_host` `httpd_accel_port` 定义了真实 HTTP 服务器的名称和端口号。在我们的配置中，真实 HTTP 服务器位于 IP 地址 208.164.186.3 (`www.openarch`) 并使用端口 (`80`)。`www.openarch` 是我们网络上的另一个主机，由于 Squid 服务器与 Apache HTTP Web 服务器不在同一主机上，我们可以将端口 (`80`) 用于我们的 Squid 代理服务器，将端口 (`80`) 用于我们的 Apache Web 服务器，这种幻觉（效果）是完美的。

### log_icp_queries off

此选项 `log_icp_queries` 指定了你是否想要将 ICP 查询记录到 `access.log`。由于我们不使用 ICP，我们关闭了此选项。

### buffered_logs on

此选项 `buffered_logs` 如果“开启”，可以稍微加快某些日志文件的写入速度。这是一个优化功能。

# 将 `etc/rc.d/init.d/squid` 脚本作为 http 加速器配置

你的脚本已被修改，为 `cache` 设置 squid 交换缓存，而不是 `var/spool/squid`。

创建 squid 脚本文件（`touch /etc/rc.d/init.d/squid`）并添加：

```bash
#!/bin/bash
# squid
# 此脚本负责启动和停止
# Squid 互联网对象缓存

# chkconfig:- 90 25
# description: Squid 互联网对象缓存. 互联网缓存是：
# 一种将请求的互联网对象（即，通过
# HTTP、FTP 和 gopher 协议可用的数据）存储在比
# 请求站点更近系统上的方法。浏览器可以使用
# 本地 squid 缓存作为代理 HTTP 服务器，减少访问时间\
# 以及带宽消耗。
# pidfile=/var/run/squid.pid
# config:etc/squid/squid.conf
```

```bash
PATH=/usr/bin:/sbin:/usr/sbin
export PATH

# 加载函数库。
./etc/rc.d/init.d/functions

# 加载网络配置。
# /sysconfig/network
```

```bash
# 检查网络是否就绪。
[ $NETWORKING = "no" ] && exit 0
```

```bash
# 检查 squid 配置文件是否存在
[ -f /etc/squid/squid.conf ] && exit 0
```

```bash
# 确定 squid 二进制文件
[ -x /sbin/squid ] && SQUID=squid
[ -z "$SQUID" ] && exit 0

# 确定哪一个是 cache_swap 目录
CACHE_SWAP=$(sed -e 's/.*:\/etc/squid/squid.conf//' | \
grep cache_swap_dir | sed -e 's/.*cache_dir///' | \
cut -d'\'' -f2)
[ -z "$CACHE_SWAP" ] && exit 0
```

```bash
# #默认 squid 选项
# -D 禁用初始检查。如果启动 squid 时可能不需要
# 互联网连接，请提交此项
SQUID_OPTS="-D"

RETVAL=0
case "$1" in
  start)
    echo -n "Starting SQUID"
    for adir in $CACHE_SWAP; do
      if [ ! -d "$adir" ]; then
        echo -n "init_cache_dir $adir..."
        $SQUID -D 2>/dev/null
      fi
    done
    $SQUID $SQUID_OPTS &
    RETVAL=$?
    echo $SQUID
    [ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SQUID
    ;;
  stop)
    echo -n "Stopping SQUID:"
    $SQUID -n
    RETVAL=$?
    if [ $RETVAL -eq 0 ]; then
      rm -f /var/lock/subsys/$SQUID
      while : ; do
        [ -f /var/run/squid.pid ] || break
        sleep 2
      done
      echo -n "done"
    fi
      echo
    ;;
  reload)
    $SQUID $SQUID_OPTS -reconfigure
    exit $?
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  status)
    $SQUID check
    exit $?
    ;;
  probe)
    exit 0
    ;;
  *)
    echo "Usage: $0 [start|stop|status|restart]"
    exit 1
esac
exit $RETVAL
```

现在，使此脚本具有执行权限并更改其默认权限：

`[root#] chmod 700 /etc/rc.d/init.d/squid`

使用命令为 Squid 创建 rc.d 链接：

`[root#] chconfig --add squid`

默认情况下，脚本在重启时不会自动启动代理。你可以通过执行以下命令更改默认设置：
