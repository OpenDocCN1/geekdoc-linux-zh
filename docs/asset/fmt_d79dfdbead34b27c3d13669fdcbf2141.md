
由于 syslog 是操作系统主要的日志机制，偶尔使用 syslog 从系统管理脚本生成自定义消息是有意义的。从脚本或命令行向 syslog 发送消息的标准机制是 `logger(1)` 命令。`logger` 命令为 syslog() 例程提供了一个方便的命令行界面。该工具的语法允许指定设施和严重性级别对；此外，它还提供了指定要记录的消息或包含消息文本的文件的能力。例如，在命令行输入以下命令

```bash
# logger -p user.debug "Program error"
```

将导致 syslog 记录以下消息：

```
# tail /var/adm/syslog/current/user.log
Jul 13 23:05 root: Program error
```

此消息将最终位于 `/etc/syslog.conf` 中为 "user.debug" 设施指定的目标位置。

**在联系支持之前**：如果系统没有将预期消息记录到 syslog 设施：

- syslog 守护进程是否正在运行？
- `/dev/log` 和 `/dev/k` 设备文件是否存在？它们具有正确的主设备和从设备号吗？
- 配置文件 `/etc/syslog.conf` 是否有问题？文件是否存在？文件格式是否正确？
- 使用 `logger(1)` 命令时，你是否成功发送了测试消息？
- syslog 是否正确配置，以记录你正在查找的设施的消息？

## 3.1.2 事件管理器

事件管理器（`evm`）是 Tru64 UNIX 设施，旨在将来自各种通道的事件报告简化并统一到单一源中。它与旧的机制（如 syslog 和 binlogd）协作工作。在本节中，我们将简要概述 evm 及其使用方法。

构成 evm 设施的组件如下：

- 事件（Events）——发生了某些指示
- 事件通道（Event channel）——用于发布或检索事件信息的设施
- 事件发布者（Event poster）——将事件发布到 evm 守护进程的组件
- 事件订阅者（Event subscriber）——对特定指示感兴趣的实体

当发生有趣的事情（称为事件）时，事件管理器就会启动。组件创建一个 evm 事件包，描述发生了什么，并将事件发布到 evm 守护进程。守护进程接收事件并根据其模板事件数据库对其增强，然后将事件发送给任何对这类事件注册了兴趣的订阅客户端。订阅客户端接收事件并可能据此执行某些操作。此外，系统管理员可以使用 `evmget(1)` 命令查看事件。

evm 设施还使用了许多命令行工具，可用于显示、检索、排序和发布事件。还有一个 SysMan 接口，但此处未作介绍。五个 evm 命令行工具如下：

1. `evmshow`——将二进制事件转换为人类可读的格式
2. `evmget`——检索事件
3. `evmsort`——对事件流进行排序
4. `evmwatch`——订阅一组事件
5. `evmpost`——发布事件

### 3.1.2.1 evmshow

最常用的 evm 命令行工具是 `evmshow`。你可以使用此命令查看存储的事件，因为它们是二进制格式的。要显示旧日志文件的内容，可以使用如下命令

```bash
# evmshow /var/evm/evmlog/evmlog.20010606
```

要插入时间戳，重新运行命令并指定包含时间戳：

```bash
# evmshow -t "@timestamp @@" /var/evm/evmlog/evmlog.20010606
```

有关 evm 命令行工具的详情，请参相应的参考页或 evm 文档。

### 3.1.2.2 evmget

`evmget` 命令用于检索二进制事件流。`evmget` 命令与 evm 守护子进程 get-server 建立连接，并根据 get-server 的授权检查处理用户授权的事件。输出通常传递给 `evmshow` 命令。

## 3.1 系统级错误报告设施

```
# evmget -f "priority > 300" | |
evmshow -t "@timestamp @@"
```

该命令检索用户授权的优先级大于 300 的所有事件，并通过 `evmshow` 命令通过时间戳显示它们。`-f` 选项（过滤器）允许选择所需的事件。

### 3.1.2.3 evmsort

当 `evmget` 检索时，事件可能没有特定的顺序，因此在过程中需要进行排序。`evmsort` 命令顾其实名，正是为此设计的。`evmsort` 命令读取二进制事件，并与 `evmget` 配合管道使用。在上一个示例的基础上添加排序功能：

```
# evmget -f "priority > 300" | evmsort |
evmshow -t "@timestamp @@"
```

请参阅 `evmsort` 参考页面获取有关根据不同字段微调排序的信息。

### 3.1.2.4 evmwatch

`evmwatch` 工具允许实时查看事件。同样，输出将通过 `evmshow` 进行处理，你可以使用过滤器来选择某些事件（例如，优先级大于 300 的事件）：

```
# evmwatch -f "priority > 300" | |
evmshow -t "@timestamp @@"
```

管道中不需要 `evmsort`，因为这些事件将在发生时立即显示。任何事件都将显示时间戳。

### 3.1.2.5 evmpost

`evmpost` 工具顾其实名，向 evm 守护进程发布事件。它接收文件或事件源流的形式输入，将其转换为二进制事件格式，并发布到 evm 守护进程进行分发。简单的示例是发布一个系统管理员事件，指示特定操作已完成：

```
# evmpost -a "Disk dsk42 was successfully replaced"
```

## 3.1.3 二进制错误日志

如前，`syslog` 存在于所有现代 UNIX 实现中；但二进制错误日志设施是 Tru64 UNIX 特有的。该设施（通常根据关联守护进程 `binlogd` 称为 `binlog`）生成二进制错误日志。`binlog` 是一种功能类似于 `syslog` 的机制，用于收集和记录来自内核的消息。`binlog` 守护进程记录硬件和软件错误以及操作事件，如系统启动和关闭。

显然，这些消息对系统管理员具有很大价值，理解如何检查和解释二进制错误日志是成功解决系统问题的关键之一。`binlog` 有两个组件：`binlog` 守护进程 `/usr/sbin/binlog` 和 `binlog` 配置文件 `/etc/binlog.conf`。此外，生成的错误日志不是人类可读的格式，HP 提供了三个工具来查看和操作此日志。按产品出现的先后顺序排列，它们是 DECevent、DECevent 和 Compaq Analyze。

### 3.1.3.1 二进制错误日志守护进程

二进制错误日志守护进程 `binlogd` 是一个可执行的系统实用程序，通常在启动时启动，并在系统处于多用户模式时始终运行。`binlog` 读取系统内核发送给它的消息。这些消息可以是信息性的、警告或需要注意的错误。消息本身是单行的，可选包含一个指示消息严重程度的优先级值。`binlogd` 从两个源接收消息。Tru64 UNIX 内核通过设备特殊文件 `/dev/binlog` 向 `binlog` 提交消息。此外，`binlog` 可能通过 `/etc/services` 文件指定的 socket 通过网络从其他系统接收消息。提到这两个源的唯一目的是为了在排排除 `binlog` 问题时确定检查的地方。

例如，如果内核消息没有接收到二进制错误日志中，请确保 `/dev/binlog` 文件存在：

```
# ls -l /dev/binlog
cr-------- 1 root 31,0 Apr 24 22:11 /dev/binlog
```

如果文件丢失或不正确（例如它不是字符特殊文件），只需重新创建 `kbinlog` 文件：

```
# cd /dev
# ./MAKEDEV kbinlog
```

同样，如果其他 Tru64 UNIX 系统向特定系统发送二进制错误日志消息但消息未被记录，请确保 `/etc/services` 文件存在并包含以下条目：

```
binlogd 706/udp
```

同时确保 `/etc/binlog.auth` 文件配置恰当（见第 3.1.3.3.2 节）。

### 3.1.3.2 启动和停止 binlog

二进制错误日志守护进程 `binlog` 通常由启动脚本 `/sbin/rc3.d/S10binlog` 在启动时启动，该脚本实际上是 `/sbin/init.d/binlog` 的符号链接。`binlog` 守护进程在启动过程早期启动，是因为它在错误日志过程中非常重要。当 `binlog` 启动时，会创建文件 `/var/run/binlog.pid`。该文件包含单行 `binlog` 进程的 PID。当需要停止或重启 `binlog` 时，可以使用此文件获取 `binlog` 的 PID。

例如，你可以使用以下命令中的任一个来终止 `binlog`：
