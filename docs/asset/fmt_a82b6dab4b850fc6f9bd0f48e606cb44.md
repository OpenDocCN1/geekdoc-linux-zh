
# 第 15 章 负载调度器

在下一个屏幕之后，将显示 CPU 分配屏幕。这与图 15-17 中 vPar WLM 场景期间显示的屏幕相同。与 vPar 场景一样，`tomcat_pkg` 工作负载将使用非指标的 CPU 使用策略。当工作负载消耗超过其额定资源的 75% 时，WLM 将为工作负载分配额外资源。当 `tomcat_pkg` 的 CPU 资源消耗低于其额度的 50% 时，WLM 将释放资源。

它们会在最合适的时间激活，而不会过快或过慢地频繁激活和去用处理器。最后，第 47 行指定了用于激活未许可 CPU 的授权管理员的联系信息。

## 列表 15-4 rex04 负载调度器配置文件

```
prm {
  groups = =
    tomcat_pkg : 2 ,
    excess: 60;

  users =
    www : tomcat_pkg;
}
nslo tomcat_slo {
  pri = 1;
  entity = PRM group tomcat_pkg;
  minpcpu = 1;
  maxcpu = 400;
  goal = usage_CPU;
  condition = metric tomcat_pkg_active;
}
slo excess_slo {
  pri = 100;
  entity = PRM group excess;
  minpcpu = 400;
  maxcpu = 400;
  goal = metric ticod_metric > -1;
}
tune {
  absolute_cpu_units = 1;
  distribute_excess = 1;
  transient_groups = 1;
  coll_argv = wlmrcvdc;
  wim_interval = '10'
}
tune tomcat_pkg_active {
  coll_argv = wlmrcvdc
  sg_pkg_active tomcat_pkg;
}
tune ticod_metric {
  coll_argv =
  /opt/nlm/toolkits/utility/bin/utilitydc
  -g excess
  -i temporary-icod
  -m 2
  -f 6
  -d "Bryan Jacquot:bryanj@rex04.fc.hp.com:555.555.4700";
}
```

## 启动负载调度器

最后一步是在开始 WLM 配置验证之前执行的。应该使用 WLM 命令 `/opt/wlm/bin/wlmd -c /etc/wlm.conf` 来确保配置文件没有错误。验证通过后，使用命令 `/opt/wlm/bin/wlmd -a /etc/wlm.conf` 激活配置。

此时，WLM 配置已处于激活状态。只要 Servicepackage 在 zoo601 上运行，rex04 分区就不会有任何用户可见的变化。当 `tomcat_pkg` 服务故障转移到 rex04 成为自适应节点时，针对 `tomcat_pkg` 负载的 WLM SLO 将被激活。随着负载需求的增加，WLM 将在 rex04 中激活未许可 CPU；当负载减少或包迁移回 zoo601 时，任何已激活的未许可 CPU 都将被去激活。为了监控 rex04 上的 `tomcat_pkg` 负载，必须执行 `/opt/wlm/bin/wlmcmd` 命令启动 `wlmcmd` 守护进程。

为了确保 WLM 在重启 rex04 后能够启动，应该更新 `/etc/rc.config.d/wlm` 文件。应将 `WLM_ENABLE` 变量设置为 1，如果需要远程监控，也应将 `WLMCOMD_ENABLE` 变量设置为 1。还应显式配置 `WLM_STARTUP_SLFILE` 变量，以确保在 WLM 启动时使用正确的配置文件。

## 监控负载调度器

当 Serviceguard 簇包未在 rex04 上运行时，负载组会被禁用，如下面的 `wlminfo` 命令所示。

```
# /opt/wlm/bin/wlminfo -s tomcat_slo
```

2004年12月5日 周五 15:16:01

| SLO 名称 | 组 | 优先级 | 请求 | 份额 | 状态 | 关注 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `tomcat_slo` | `tomcat_pkg` | 1 | | 0 | OFF | |

由于负载被禁用，不会消耗任何资源。当 zoo61 节点不可用或故障时，Tomcat 包将迁移到 rex04。图 15-24 显示了通过 `wlmui` 命令可用的 `tomcat_slo` 图表。注意在上方图表中，`tomcat_slo` 的 CPU 使用率高于 75%，负载正在请求更多 CPU 资源。由于激活未许可 CPU 有 60 秒的最小延迟，上图中负载的波动性质在 CPU 分配图中变得更加平滑。所有的

| 配置 | CPU | 负载组 | 服务级别目标 | 自定义 |
| :--- | :--- | :--- | :--- | :--- |
| `rex04.fc.hp.com` | `tomcat_slo` | | | |
| 新窗口 | `excess_slo` | | | |

![](img/fd7e17168a916afa5a44c7402dd35df2_397_0.png)

消息

| 消息内容 |
| :--- |
| rex04.fc.hp.com: 12/05/04 18:32:25 [I] (WLM UQ) WLM 处于激活模式 |
| rex04.fc.hp.com: 12/05/04 18:34:49 [M] (p1307) 没有激活的 SLO 达到最小值。 |
| rex04.fc.hp.com: 12/05/04 18:34:59 [M] (p1307) 没有激活的 SLO 达到最小值。 |

| 添加 | 删除 | 负载 | 保存 | 帮助 |

**图 15-24** 负载调度器服务级别目标图

18:35 到 18:39 之间的利用率峰值没有导致分配给负载的份额数量发生任何实质变化，因此在此期间没有激活任何未许可 CPU。

图 15-25 所示图说明了 rex04 nPar 中激活的 CPU 数量。在这种情况下，所有大于 2 的 CPU 值都表示正在消耗瞬时临时容量（Temporary Instant Capacity）。从该图中可以明显看出，CPU 正在非常规律地激活和去激活。因此，可能会增加 `wlm_interval` 值、增加 WLM 等待瞬时临时容量更改的间隔次数，或者两者兼顾。结果将是一个更平滑的图表，它将仅显示持续的负载峰值导致瞬时临时容量的分配，以及仅持续的负载闲置导致去激活未许可 CPU。

![](img/fd7e17168a916afa5a44c7402dd35df2_397_0.png)

**图 15-25** 负载调度器 CPU 图

## 查看即时容量

由于 WLM 自动激活和去激活 CPU，监控使用情况变得越来越重要。正如第 11 章所述，应配置电子邮件地址以便维护详细日志。列表 15-5 显示了即时容量的示例。

## 列表 15-5 负载调度器的激活与去激活

```
# cat /var/adm/icod.log

Date: 12/05/04 18:56:36
Log Type: 配置更改
总处理器: 4
激活处理器: 2
预期的激活 CPU: 2
Description: 剩余资源
更改者: Workload-Manager

Date: 12/05/04 18:59:41
Log Type: 配置更改
总处理器: 4
激活处理器: 3
预期的激活 CPU: 3
Description: SLO 失败
更改者: Workload-Manager

Date: 12/05/04 19:00:16
Log Type: 临时容量
CPU 分钟扣除: 30
许可处理器: 14
激活处理器:
nPar 激活
0 4
1*
2*
可用临时容量: 198 天 0 小时 0 分钟

Date: 5/04 19:00:18
Log Type: 配置更改
总处理器: 4
激活处理器: 4
预期的激活 CPU: 4
Description: SLO 失败
更改者: Workload-Manager

Date: 12/05/04 19:01:22
Log Type: 配置更改
总处理器: 4
激活处理器: 3
预期的激活 CPU: 3
Description: 剩余资源
更改者: Workload-Manager
```

## 总结

负载调度器构建在 HP 虚拟服务器环境提供的许多技术之上。WLM 允许管理员为一组负载配置所需的服务目标，并由它接管后续。
