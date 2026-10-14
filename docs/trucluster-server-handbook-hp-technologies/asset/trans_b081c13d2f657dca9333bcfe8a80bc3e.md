

# 20.1.4 gated 的配置文件

如前所述，每个成员的 aliasd 守护进程（第 16 章讨论的集群 alias 组件的一部分）将创建一个成员特定的 gated.conf 文件（不是 CDS L），命名为 /etc/gated.conf.membern（其中的 "n" 用成员编号替换）。以下示例展示了成员特定的 gated.conf 文件。（有关此文件语法的更多信息，请参阅以下参考页：gated.conf(4)、gated.control(4)、gated.proto(4)、gated_intro(4)）。

```
# cd /etc && file gated*

gated.conf: symbolic link to ../../cluster/members/(memb)/etc/gated.conf
gated.conf.default: c program text
gated.conf.member1: c program text
gated.conf.member2: c program text
```

```
# cat /etc/gated.conf.member1
# This file created automatically by "aliasd", DO NOT EDIT!
#

traceoptions "/usr/tmp/gated.log" replace size 1000k files 2 general;
# any dead interfaces will be entered here with a high (i.e. undesireable)
# preference, so that gated will be compelled to put a better route
# in the kernel forwarding table

interfaces {
    interface all passive;
};
# broadcast routes with RIP if at least one interface is healthy
# make a default route through the cluster interconnect look expensive
# If an interface has been marked as "dead" by NIFF then we
# will also exclude RIP routes via the affected interface.
# This closes a hole where gated doesn't qualify the interfaces
# over which it hears broadcasts, and will possibly install a route
# through a dead interface.
#
# Lastly, we place a catch-all "all nripin noripout" here so that
# if an interface is brought on-line after aliasd has started, it
# won't automatically get used by gated.
#
rip yes {
    broadcast;
    interface ics0 ripin ripout metricout 10;
    interface tu0 ripin ripout metricout 10;
    interface tu1 ripin ripout;
    interface all noripin noripout;
};
```

```
# one "host" or network number per alias
#
# alias will also reroute direct routes for interfaces
# marked as "dead" by NIF by inserting a new gateway
# for that route here
#
```

注意，接下来的几行描述了默认的集群 alias。

```
static {
    host 192.168.0.70 interface 127.0.0.1;
};

# arrange to export alias host/network routes:
#
# o don't publish routes learned through RIP
# o publish the "static" routes given above, except for
#   ophaned networks that we're routing around
# o publish direct routes for virtual subnets which have real
#   interfaces attached to them
#
# for the cluster interconnect, arrange to broadcast a
# high-cost default route over it
#
# this default may have been learned from RIP (proto rip)
# or it may have been statically configured (proto kernel)
# we give a slight advantage to a default route via RIP
```

注意，接下来的几行描述了集群互连 Cluster Interconnect (CI) 虚拟地址。

```
export proto rip interface 10.0.0.1 {
    proto rip {
        default;
    };
    proto kernel {
        default metric 3;
    };
};
```

注意，接下来的几行描述了 LAN 互连。

```
export proto rip interface 10.1.0.1 {
    proto rip {
        default;
    };
    proto kernel {
        default metric 3;
    };
};

export proto rip interface 192.168.0.68 {
    proto rip restrict;
};
```

够丑的吧？你可能开始明白为什么 HP 建议除非你非常熟悉 gated 和网络管理，否则不要将系统设置成 IP 路由器。（参见 gated.conf.membern 文件的第一行：“# This file created automatically by "aliasd", DO NOT EDIT!”）

还是想试试？那么请根据文档集中的 *TruCluster* Server Cluster Administration Guide 中的步骤进行操作（第 6 章）：如果 gated 正在运行，请使用以下命令停止它：

```
`# /sbin/init.d/gateway stop`
```

- 1. 输入以下命令：
  
      `# cluamgr -r start,nogated`

- 2. 修改 gated.conf（改为你正在使用的配置文件名）。
  
  使用 “cluamgr -r nogated,start” 命令创建的 `/etc/gated.conf.membern` 版本作为自定义 gated 配置文件编辑的基础。你需要将 `/etc/gated.conf.membern` 文件中的集群 alias 信息正确合并到你的自定义配置文件中。

- 3. 使用以下命令启动 gated：
  
      `# /sbin/init.d/gateway start`

在这种特殊情况下，你将为 gated 提供一个非标准的配置文件供其使用（也许需要使用开放最短路径优先 Open Shortest Path First (OSPF) 而不是 RIP）；因此，你需要在 `/etc/rc.config.common` 中为 CLUA_ROUTE_ARGS 输入字符串 “nogated”，以防止 aliasd 在重启时使用 gated.conf.membern 文件重新启动 gated。

检索 rc.config.common 文件中的 CLUA_ROUTE_ARGS。我们这样做是为了验证是否没有之前的属性值（并在必要时合并内容）。

```
`# rcmgr -q get CLUA_ROUTE_ARGS`
```

添加 CLUA_ROUTE_ARGS 环境变量的新值。

```
`# rcmgr -s set CLUA_ROUTE_ARGS "nogated"`
```

## NOTE：

不要将 CLUA_ROUTE_ARGS 环境变量放在成员特定的 `rc.config` 文件中。

