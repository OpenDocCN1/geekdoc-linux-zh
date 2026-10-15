
# 第 15 章 工作负载管理器

```
# /etc/wlm.conf
#
# HP-UX WLM 配置：最初由 wlmcw(1M) 创建。
# 详情请阅 wlmconf(4) 和 /opt/wlm/share/doc/WLM.*。
# 使用 /opt/wlm/bin/wlmd -c <filename> 进行验证。
# 使用 /opt/wlm/bin/wlmd -a <filename> 激活。

#
# 动态分区设置的主机。
primary_host = "zoo21.fc.com";

#
# PRM 结构用于定义工作负载组，并可选地将
# 和用户分配给这些组。
prm {
  groups =
    sales_db : 2,
    finance_db : 3;

  apps =
    sales_db : /oracle/app/oracle/product/9.2.0/1.0/bin/oracle*sales,
    finance_db : /oracle/app/oracle/product/9.2.0/1.0/bin/oracle*finance;
}
#
# SLO（服务级别目标）结构。
slo sales_db_slo {
  # 此 SLO 的优先级。
  pri = 15;
  # SLO 应用的工作负载组。
  entity = RM group sales_db;
  # 请求少于可用份额的 mincpu。
  mincpu = 1;
  # 当资源需要时迁移资源可能会导致不必要的延迟。
  maxcpu = 1;
  # 目标。
  goal = 1
}
#
# SLO（服务级别目标）结构。
slo finance_db_slo {
  # 此 SLO 的优先级。
  pri = 15;
  # SLO 应用的工作负载组。
  entity = RM group finance_db;
  # 请求少于可用份额的 mincpu。
  mincpu = 1;
  # 当资源需要时迁移资源可能会导致不必要的延迟。
  maxcpu = 1;
  # 目标。
  goal = 1
}
#
# 全局调优结构用于为全局调优
# 变量设置值。
tune {
    # 设置 share 的解释：
    # 1 => 1 个 CPU 的 1/100
    # 0 => share 是所有 CPU 的 1/100
    # 如果使用 PSET 组，请勿设置为 0。
    absolute_cpu_units = 1;

    # 如果剩余资源，则将其分配给用户定义的组
    # (1 = 是； 0 = 否)；
    distribute_excess = 1;

    # 设置 WLM 更改资源
    # 分配的间隔（秒）：
    wlm_interval = 5;
}
```

## 在第二个虚拟分区上启动工作负载管理器

现在 zoo21 上已经就绪了两个配置文件，您应该验证文件的语法。命令 `/opt/wlm/bin/wlmd -c /etc/wlm.conf` 将验证配置文件是否包含错误。当手动编辑 WLM 配置时，这一步尤为重要。

下一步是使用命令 `/opt/wlm/bin/wlmd -a /etc/wlm.conf` 在 zoo21 vPar 上启动 WLM 守护进程。运行此命令后，WLM 守护进程将运行，并调整分配给 zoo21 内部每个工作负载的资源。然而，您尚未设置全局仲裁器（global arbiter），因此资源将将不会在两个 vPars 之间进行迁移。

为了启动全局仲裁器，应检查其配置文件是否存在错误。验证和启动 `wlmp` 守护进程的命令与用于 `wlmd` 守护进程的命令非常相似，但全局仲裁器的命令是 `wlmp` 而不是 `wlmd`。要检查全局仲裁器的配置文件，请执行命令 `/opt/wlm/bin/wlmp - /etc/wlmpar.conf`。假设没有错误，可以使用 `/opt/wlm/bin/wlmp -a /etc/wlmpar.conf` 启动全局仲裁器。

除了启动两个确保满足 SLO 的 WLM 守护进程外，您还可以启动另一个守护进程，允许您使用 WLM GUI 监控工作负载和 SLO。可以通过执行 `/opt/wlm/bin/wlcmd` 命令启动该守护进程。

zoo21 的最后一个配置任务是配置 WLM 使其在系统启动时自动启动。为此目的，在 `/etc/rc.config.d/wlm` 中提供了一个配置文件。应该修改该文件，通过将变量 `WL_ENABLE` 设置为 1 来使 `wlmd` 守护进程自动启动。全局仲裁器变量 `WLMPARD_ENABLE` 也应设置为 1，且 `WLMCOMD` 应该设置为 1。HP 还建议您显式配置为相应守护进程的 `wlmd` 和 `wlmp` 配置文件的位置。如果这两个配置文件没有被显式配置，WLM 将使用每个守护进程上一次执行时所使用的配置文件。

## 配置第二个 vPar 分区

zoo019 vPar 的配置与 zoo201 vPar 的配置几乎相同。工作负载的名称和优先级不同，但其他所有内容都是相同的。在这种情况下，只需将 zoo201 的 `/etc/wlm.conf` 配置文件复制到 zoo019 并编辑工作负载名称行是最简单的方法。

列表 15-3 显示的文件是 zoo019 的结果配置文件。请注意主主机是 zoo201.fc.com。只有一个 vPars 作为主主机。还要注意，工作负载组的名称及其优先级已更新，以反映运行在此 vPar 内部的工作负载。

### 列表 15-3 适用于 zoo019 的工作负载管理器配置文件

```
# /etc/wlm.conf
#
# HP-UX WLM 配置：最初由 wlmcw(1M) 创建。
# 详情请阅 wlmconf(4) 和 /opt/wlm/share/doc/WLM.*。
# 使用 /opt/wlm/bin/wlmd -c <filename> 进行验证。
# 使用 /opt/wlm/bin/wlmd -a <filename> 激活。

#
# 动态分区设置的主机。
primary_host = "zoo21.fc.com";

#
# PRM 结构用于定义工作负载组，并可选地将
# 和用户分配给这些组。
prm {
  groups =
    sales_db : 2,
    finance_db : 3;

  apps =
    sales_db : /oracle/app/oracle/product/9.2.0/1.0/bin/oracle*sales,
    finance_db : /oracle/app/oracle/product/9.2.0/1.0/bin/oracle*finance;
}
#
# SLO（服务级别目标）结构。
slo sales_db_slo {
  # 此 SLO 的优先级。
  pri = 15;
  # SLO 应用的工作负载组。
  entity = RM group sales_db;
  # 请求少于可用份额的 mincpu。
  mincpu = 1;
  # 当资源需要时迁移资源可能会导致不必要的延迟。
  maxcpu = 1;
  # 目标。
  goal = 1
}
#
# SLO（服务级别目标）结构。
slo finance_db_slo {
  # 此 SLO 的优先级。
  pri = 15;
  # SLO 应用的工作负载组。
  entity = RM group finance_db;
  # 请求少于可用份额的 mincpu。
  mincpu = 1;
  # 当资源需要时迁移资源可能会导致不必要的延迟。
  maxcpu = 1;
  # 目标。
  goal = 1
}
```

## HP 虚拟服务器环境

![](img/fd7e17168a916afa5a44c7402dd35df2_381_0.png)

图 15-13 工作负载图形界面，添加分区集

“分区（partitions）”按钮会将分区集内所有分区的名称加载到列表中。记住，此分区集中的分区是在列表 15-2 所示的 WLM 分区配置文件中定义的。注意，列表中列出了两个 `zoo2021` 实例。这是符合预期的，因为第一个条目是主主机实例，而第二个是需要被监控的分区。在此屏幕上点击“确定”将连接每个分区并显示初始界面。

一旦进入 WLM GUI，如图 15-14 所示，屏幕上有多个不同的界面可用。屏幕顶部的三个主标签提供以下功能：

- *Monitor（监控）*：启用由 WLM 管理的一组工作负载。

- *Modify（修改）*：允许更新一组分区（包括远程分区）的工作负载配置。配置文件中支持的所有选项都可以通过此界面进行修改。

- *Deploy（部署）*：提供一个用于激活已修改配置的界面。

图 15-14 屏幕左侧的面板允许你定义作为组管理或监控的分区集。通常，这些分组是运行 WLM 的节点上的分区集。然而，并不要求所有列出的系统都位于同一个主主机下。分区列表可以是任何运行 WLM 的任意分区集合。例如，可以为所有运行 Oracle 实时应用集群 (RAC) 或 WebLogic 集群实例的分区创建一个分区集。诚然，WLM 无法跨越不同节点的分区分配资源，但可以创建图表来显示分配给集群中每个节点的各个资源。
