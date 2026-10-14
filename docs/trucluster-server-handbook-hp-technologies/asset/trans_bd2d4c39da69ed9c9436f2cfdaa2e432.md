

```text
# mknod /dev/volconfig c 41 0
# mknod /dev/voltrace c 41 1
# mknod /dev/voliod c 41 2
# mknod /dev/volinfo c 41 3
# checkrc
```

使用 LSM 时需要这些额外步骤，因为“dn_setup –init”会完全删除 /devices 目录以及 /dev 的内容，而 dn_setup 不了解 LSM。我们将在第 14 章更详细地介绍 LSM。

## 7.5.2.2 如何检查我的设备特殊文件和目录层次结构是否存在不一致？

```text
# dn_setup --sanity_check
        Passed
```

请注意，这实际上等同于运行“dsfmgr –zx”，尽管“–z”开关未有文档记录。

## 7.5.2.3 如何从安装 CD 创建磁带设备特殊文件？

```text
# dn_setup -install_tape
```

截至本文撰写时，dn_setup 命令没有参考页。然而，它在 5.1B 版本之前的 Tru64 UNIX 系统管理手册以及 5.1B 版本起的 Tru64 UNIX 硬件管理手册中有文档说明。

## 7.6 参考文献

- *Tru64* UNIX 系统管理 – 版本 5.1、5.1A 和 5.1B。
- *Tru64* UNIX 硬件管理 – 版本 5.1B。
- 参考页（文中已注明）。

## Tru64 UNIX 集群钩子：

事件管理器

事件管理器（EVM）是 Tru64 UNIX 在操作系统 5.0 版本中新增的一个组件，是应客户要求提供对所有系统（和集群）事件信息的通用访问而添加的。

在之前的版本中，系统上发生的事件很可能会记录到两个主要记录器之一：系统消息记录器（syslogd）和二进制错误记录器（binlogd）——尽管也可以使用其他日志方法。EVM 与这些其他事件记录器协同工作以整合信息。图 8-1 说明了事件到 EVM 的路径。

![](img/a0df85c2e542a8d6c913113908553aa4_194_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_196_0.png)

图 8-2：EVM 根目录层次结构

![](img/a0df85c2e542a8d6c913113908553aa4_196_1.png)

图 8-3：EVM /usr 目录层次结构

![](img/a0df85c2e542a8d6c913113908553aa4_197_0.png)

图 8-4：EVM /var 目录层次结构

## 8.2.1 EVM 常驻组件

EVM 有三个主要组件用于事件管理：

- evmd
- evmchmgr
- evmlogger

### 8.2.1.1 EVM 守护进程（evmd）

EVM 守护进程是 EVM 的主要分发中心。它在系统初始化时于运行级别 2 启动，尽管它在运行级别 3 之前无法访问远程连接。对 evmd 的通信通过套接字连接处理。发布和订阅请求由 evmd 直接处理。

然而，事件检索由派生的 event_get 服务程序处理（实际上是 /usr/sbin/evmget_srv。参见 /etc/evmdaemon.conf）。

EVM 守护进程根据 /etc/evmdaemon.conf 文件启动 Channel Manager 和 Logger 进程。事实上，它也可以配置为启动任何站点定义的同步客户端进程。

有关更多信息，请参阅 evmd(8) 和 evmdaemon.conf(4) 参考页。

### 8.2.1.2 EVM 通道管理器（evmchmgr）

通道管理器负责监控和清理 /etc/evmchannel.conf 文件中定义的通道，前提是它们定义了监视器（fn_monitor）或清理（/fn_cleanup）服务例程。通道管理器由 evmd 守护进程自动启动，不应作为独立程序运行。

默认情况下，evmchmgr 会将任何错误输出写入 stderr。

有关更多信息，请参阅 evmchmgr(8) 和 evmchannel.conf(4) 参考页。

### 8.2.1.3 EVM 记录器（evmlogger）

记录器程序是根据 /etc/evmlogger.conf 文件定义的 EVM 事件的订阅者。此守护进程订阅事件，然后将它们写入事件日志（例如 /var/adm/evmlog/evmlog.dated）或使用转发命令转发它们（例如向 root 账户发送电子邮件）。记录器由 evmd 守护进程自动启动，但也可以通过创建配置文件并使用 “-c” 开关启动 evmlogger 进程作为独立程序运行。例如：

```
# evmlogger -c $HOME/evm/myEVMLogger.conf
```

默认情况下，evmlogger 会将任何错误输出写入 stderr。

有关更多信息，请参阅 evmlogger(8) 和 evmlogger.conf(4) 参考页。

