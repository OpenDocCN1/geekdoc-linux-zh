
还有一些选项与保持已建立连接有关。其原理是服务器必须保持的每个连接都会消耗资源。如果你的服务器在给定时刻非常繁忙，它将耗尽资源并拒绝新的

# 优化性能

463

当没有可用资源时，接入的客户端。由于在大多数情况下，客户端建立连接是非常容易的，你可能希望对服务器进行调优，使其尽快检测到失败的连接。

与维护连接相关的第一个参数是 `tcp_synack_retries`。该参数定义了内核对新入的新请求连接发送响应的次数。默认值为 5。鉴于目前的网络连接质量，3 可能足够了，而且对于忙碌的服务器来说更好，因为它可以让连接更快地建立。使用以下命令更改它：

```
sysctl -w net.ipv4.tcp_synack_retries=3
```

接下来是 `tcp_retries_2` 选项。这与服务器尝试向已建立会话的远程主机重发数据的次数有关。由于连接断开对客户端来说是不方便的，因此默认值 15 高于 `tcp_synack_retries` 的默认值。然而，15 次意味着当你的服务器尝试重发数据时，它无法将资源用于其他地方。因此，最好将此参数减到更合理的数值 5。

```
sysctl -w net.ipv4.tcp_retries_2=5
```

刚刚讨论的参数与看似消失的会话有关。另一个你可以进行优化的领域是维护空闲会话。默认情况下，TCP 会话将永久空闲。你可能不希望这样，所以使用 `tcp_keepalive_time` 选项来确定已建立的空闲会话维持多久。默认情况下，它为 7200 秒，即两小时。如果你的服务器由于由于入请求过多而耗尽资源，请将其限制在较短的时间内，如下所示：

```
sysctl -w net.ipv4.tcp_keepalive_time=90
```

与 `keepalive_interval` 相关的是服务器在决定连接已死之前将发送的数据包数量。你可以使用 `tcp_keepalive_probes` 参数来管理它。默认情况下，在服务器被认为死亡之前会发送 9 个数据包。如果你想终止死连接，请将其更改为 3，如下所示：

```
sysctl -w net.ipv4.tcp_keepalive_probes=3
```

与 `keepalive_interval` 的数量相关的是你发送这些探测的间隔。默认情况下，这每隔 75 秒发生一次。因此，即使有三次探测，你的服务器设置该连接失败之前仍然需要超过三分钟。为了缩短这段时间，给 `tcp_keepalive_intvl` 参数赋值 15，如下所示：

```
sysctl -w net.ipv4.tcp_keepalive_intvl=15
```

为了完成维护连接的介绍，你还需要两个参数。默认情况下，内核在重用 socket 之前会等待一会儿。如果你运行忙碌的服务器，关闭此功能将有利于性能。要执行此操作，请使用以下命令：

```
sysctl -w net.ipv4.tcp_tw_reuse=1
```

```
sysctl -w net.ipv4.tcp_tw_recycle=1
```

# 通用网络性能优化技巧

到为止，我只讨论了内核参数。在优化网络性能时，还有一些通用的提示提示需要遵循。你可能已经应用了所有这些提示，但为了以起起见，让我们重复一些最重要的提示：

- 确保你拥有最新的网络驱动程序模块。
- 使用网卡绑定（teaming）来创建一个绑定接口，使用两块物理网卡来提高服务器上网卡的性能。
- 检查以太网配置设置，如帧大小、MTU、速度和双工模式，确保参与网络通信的所有设备都使用相同的设置。

# 使用 cgroups 优化 Linux 性能

在 Linux 提供的最新性能优化功能中，包含了 cgroups（控制组的缩写）。使用 cgroups 是一种允许你创建资源组并将其分配给特定服务的技术。通过这种解决方案，你可以确保服务器上固定百分比的资源始终供你需要的程序可用。

要开始使用 cgroups，请确保已安装了 `libcgroup` RPM 软件包。一旦确认安装，你就需要启动 `cgconfig` 和 `cgroup` 服务。确保将这些服务放入服务器的运行级别（runlevels）中，使用 `chconfig cgconfig on` 和 `chconfig cgroup on`。接下来确保启动这些服务。这将创建一个 `/cgroup` 目录，其中包含几个子目录。这些子目录被称为控制器（controllers）。控制器指的是你可以使用 cgroups 限制的系统资源。一些最有趣的控制器包括：

- `blkio`：使用此限制可以处理的 I/O 数量。
- `cpu`：用于限制 CPU 周期。
- `memory`：使用此限制分配给进程的内存量。

还有其他控制器，但它们没有描述的那么有用。现在假设你正在服务器上运行 Oracle 数据库，并希望确保它运行在一个可以访问 75% 可用内存和 CPU 周期的 cgroup 中。第一步是创建一个定义了 CPU 和内存资源访问的 cgroup。以下命令将创建一个名为 `oracle1` 的 cgroup：`cgcreate -p cpu,memory oracle1`。通过这种方式定义组后，你会发现 `/cgroups/cpu` 和 `/cgroups/memory_` 目录下创建了一个名为 `oracle1` 的子目录。在这个子目录中，有不同的参数可供使用。这些控制器指的是你可以使用 cgroups 限制的系统资源。

# 优化性能 465

列表17.30：在你的 cgroup 子目录中，你会发现所有可调参数

```
[root@hn1]# cd /cgroup/cpu/oracle/

[root@oracle ~]# ls

cgroup.procs          cpu.rt_period_us   cpu.stat

cpu.cfs_period_us    cpu.rt_runtime_us  notify_on_release

cpu.cfs_quota_us      cpu.shares         tasks
```

为新创建的 cgroup 指定可用 CPU 资源，将使用 `cpu.shares` 参数。这是一个相对参数，只有当全部使用 cgroups 时才有意义，它定义了该 cgroup 中可用的份额。这意味着如果你在 oracle cgroup 中赋予 80，在包含所有其他进程的 cgroup 中赋予 20，oracle cgroup 将获得 80% 的可用 CPU 资源。要设置该参数，可以使用 `cgset` 命令：`cgset -r cpu.shares=80 oracle`

设置好 cgroup 的 CPU 份额后，你可以将进程放入。最好的方法是将要放入 cgroup 的进程作为 `cgexec` 命令的参数。在示例中，这意味着你运行 `cgexec -g cgroup:cpu/oracle/path/to/oracle`。此时，oracle 进程及其所有子进程将出现在 `/cgroup/cpu/oracle/tasks` 文件中，你已经将 oracle 分配了它的特定 cgroup。

在这个示例中，你学习了如何手动创建 cgroups、为 cgroup 提供可用资源并将进程放入其中。这种方法的缺点是，系统重启后，所有设置将丢失。为了让 cgroups 持久化，你需要使用 `/etc/cgconfig.conf` 和 `cgred` 服务。`cgconfig` 服务读取其配置文件 `/etc/cgconfig.conf`，其中定义了 cgroups，包括定义你想分配给 cgroup 的资源。列表17.31 显示了对于 oracle 示例的情况。

# 列表17.31：示例 cgconfig.conf 文件

```
group oracle {

  cpu {

    cpu.shares=80

  }

  memory {

  }

}
```

接下来，你需要创建 `cgrules.conf` 文件，它指定了必须自动放入特定 cgroup 的进程。该文件在 `cgred` 服务启动时读取。对于 oracle 组，它的内容如下所示：

```
*:oracle cpu,memory /oracle
```
