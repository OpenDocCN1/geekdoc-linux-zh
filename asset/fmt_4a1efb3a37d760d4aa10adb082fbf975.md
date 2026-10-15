
以下章节进一步描述了 ICS 服务器进程。

# 第 18 章

## 18.1.2.1 来自进程池的 ICS 守护进程 [`icssvr_daemon_fr`]

某些服务能够共享一个守护进程池，以动态满足其处理需求。使用该守护进程池的服务包括 CFS、CLSM、DRD 和 KGS。这些服务的服务的活动水平在集群的生命周期内可能会有很大差异。因此，处理它们的 ICS 请求时，让系统在活动激增期间动态创建更多此类守护进程是有意义的。

注意，守护进程的数量具有向下调优的灵活性，因此在某一个时刻你可能会看到 N 个此类守护进程，而在另一个时刻你可能会看到 N-2 个。

## 18.1.2.2 每个节点的 ICS 服务器守护进程 [`icssvr_daemon_pe`]

某些服务需要一个更具预测性的服务器环境。这种可预测性基于服务器守护进程节点。这就像有一条多道道的公路，每条车道通向一个位置。从技术上讲，这些车道被称为“通道”。（至少你不需要担心出口编号，也不需要在这些车道上行驶时跟上交通。）需要这种服务器环境的服务有 CLUA、CNX、DLM、内存通道（Memory Channel）等。

## 18.1.2.3 杂项 ICS 服务器守护进程

存在两个 ICS 守护进程用于处理特殊情况。当分配失败且需要线程上下文等待内存释放时，使用 `icssvr_nomem_daemon`。该守护进程很少需要。`icssvr_throttle_daemon` 也很少使用。它负责在客户端由于内存问题被节流（throttled）一旦解决后唤醒它们。

## 18.1.2.4 ICS 通道

集群成员之间的流量通过通道传输。每个通道可以处理零或多个服务。参考前章节的多道公路示例，将一个集群成员的分布式锁（Distributed Lock Manager）服务放在通道（道）的一端，将另一个集群成员的分布式锁服务放在另一端。放在通道保证了目标服务的交付顺序。对于 DLM 这样的服务，这对于确保锁定资源的访问至关重要。现在想象一条多个服务使用同一条车道的公路，这种策略由 CFS、AdvFS 和 CMS 执行。由于这些服务都是经过评估的，这种方法运行良好。18-1 显示了由 fs 生成的与其通道相关的统计数据。

| 通道 # | 服务 | 集群子系统 | 服务数量 | ICS 守护进程 |
| :--- | :--- | :--- | :--- | :--- |
| BOOT 0 | CNX | cnx | | 每个节点 |
| | (CLUSTER_PANIC) | ics_hl | 3 | 自定义 |
| | SIGNAL | ics_hl | | 来自池 |
| PRIO 1 | none | n/a | 0 | n/a |
| PRI1 2 | none | n/a | | n/a |
| | ADVFS, CFS, FS | cfs | | 来自池 |
| CFS 3 | CMS | | 4 | 来自池 |
| NET 4 | CLUMGT | clubase | 2 | 来自池 |
| | ICSNET | ics_net | | 自定义 |
| CLSM 5 | CLSM | clsm | 1 | 来自池 |
| DRD 6 | DRDV1, DRDV2 | drd | | 来自池 |
| TUNL 7 | TUNNEL | clua | 1 | 每个节点 |
| CLUA 8 | CLUA | clua | 1 | 每个节点 |
| KEVM 9 | KEVM | kevm_clu | | 每个节点 |
| CFSR 10 | CFSREC | cfs | 1 | 来自池 |
| | RBLD | cnx | | 来自池 |
| RBLD 11 | SSN | n/a | 2 | 来自池 |
| KCH 12 | KCH | kch | | 来自池 |
| DLM 13 | DLM | dlm | 1 | 每个节点 |
| TEST 14 | (TEST1), (TEST2), (TEST3), (TEST4), (TEST5), (TEST6), (TEST7) | n/a | 7 | 变动 |
| PBT 15 | MCTCTL_SVC | ics_11_mct | 1 | 每个节点 |

### 18-1: 每个通道 ICS 服务 [`icssvr_nanny`]

## 18.1.2.5 ICS 服务器保姆 (Nanny)

那么谁负责所有这些活跃的 ICS 服务器进程呢？当你年轻时，可能有一个保姆照顾你（或者你有一个哥哥、一个邻居，或者街上古怪的老 Hal）；同样，ICS 服务器进程由“nanny”进程监看。它会在需要时创建基于池的进程，并在作为成员离开集群时创建基于节点的进程。如果你是一个非常调皮的孩子，并且有很多兄弟姐妹，你可能需要第二个保姆。同样，当 ICS 服务器保姆压力过大时，可能会其他保姆加入（我们假设你会在需要时呼叫备份援助）。注意，在本文编写时，看到一个以上的保姆是不常的。

## 18.1.3 ICS 属性

以下输出提供了支持 ICS 的 sysconfig 属性信息。

### 注意：

典型的集群成员会使用 `ics11_tcp` 或 `ics11_mct` 属性，但两者不同使用，尽管两组属性都是可见的。此外，请注意低级属性没有文档，除非 HP 工程工程师指示更改它们，否则不应修改。我们在这里包含它们是为了显示 ICS 子系统内软件级别的存在。

```
# for i in $(sysconfig -m | grep ics | cut -d;- -f)
do
  print
  sysconfig -q $i
done
```

`ics_hl`:

```
ics_hl_debug = 1
Module_Config_Name = attribute does not allow this operation
ics_hl_verbose = 2
ics_idle_daemons_lwm = 4
ics_idle_daemons_hwm = 15
```

`ics_11_tcp`:

```
Module_Config_Name = attribute does not allow this operation
ics_11_tcp_rendezvous_port = 0
ics_11_tcp_ports[0] =
ics_11_tcp_netmask =
ics_11_tcp_mtu = 1500
ics_11_tcp_nr0] =
ics_11_tcp_nr[7] =
ics_11_tcp_adapter =
```

ICS 高级属性。

ICS 低 TCP 属性。

网络接口通信。

`icsnet`:

```
hwdr_addr = 42:00:00:00:00:01
verbose = 0
icsnet_mtu = 7000
```

内部管理的 MAC 地址

为了处理来自 ICS 请求无序活动（如 CFS 和 DRD）的活动高峰，保留了一个空闲进程池。`ics_hl` 系统属性 `ics_idle_daemons_lwm` 设置了该池的低水位。进程计数可能会增长到 `ics_idle_daemons_hwm` 并超出以处理密集的活动高峰。

```
# sysconfig -q ics_hl ics_idle_daions_hwm
ics_hl:
ics_idle_daemons_hwm = 15
```

之前的输出显示了属性值，然后计算进程数量。在这种情况下，计数超过了高水位。如果出现这种情况，可能需要提高 `ics_idle_daemons_hwm`，因为这表明 ICS 守护进程在不断创建和删除。如果内核进程显示出明显的 CPU 时间，你应该提高高水位。

```
# ps -eo user,pid,time,command | awk '/USER/kproc/ { print $0 }'
USER PID TIME COMMAND
root 524290 0:00.05 [kproc_creator_da]
```
