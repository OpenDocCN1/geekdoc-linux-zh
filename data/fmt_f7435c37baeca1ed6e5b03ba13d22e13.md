
systemd 的主要优势之一是它对依赖关系的感知。服务（在 systemd 控制下运行的程序）配置包含了它所依赖的所有其他服务的信息，也可以指向依赖于它的服务。此外，服务可以告知 systemd 它运行所需的哪些目标（targets）：如果你的服务需要启动并运行，你可以将此信息放入配置中，systemd 将确保只有在网络正确配置后，才会启动你的守护进程。

## 详细了解 Linux 服务

以下是 systemd 提供的一部分工具和实用程序列表：

- `systemd`: 这是主系统和内核管理器。它是控制服务及其他系统组件初始化和管理的主程序。
- `systemctl`: 这是用于管理系统服务和其他系统组件的命令行实用程序。它可以用于启动、停止、重启、启用和禁用服务，以及查看服务和其他系统组件的状态。
- `journalctl`: 这用于查看和操作由 systemd 管理的系统日志。它可以用于查看日志、根据标准过滤消息以及将日志数据导出到文件。
- `coredump`: 这是一个实用程序，顾如其名，它帮助从 systemd 日志中检索核心转储（core dumps）。
- `systemd-analyze`: 这可以用于分析系统的启动性能。它测量系统启动所需的时间，以及识别潜在瓶颈和性能问题所需的时间。
- `systemd-cgroups`: 这是一个查看系统上控制组层级结构的命令行工具。控制组（或 cgroups）被 systemd 用于管理系统资源并将进程进行相互隔离。
- `systemd-delta`: 这是一个用于分析 systemd 提供的默认配置文件与这些文件的任何本地修改之间差异的命令行工具。
- `systemd-detect-virt`: 这是一个用于检测系统运行的虚拟化环境的命令行工具。它可以确定系统是运行在虚拟机 (VM)、容器还是裸机上。
- `systemd-inhibit`: 这是一个防止执行某些系统操作（如挂起或关机系统）的命令行工具。
- `systemd-nspawn`: 这是一个在轻量级容器中运行进程的命令行工具。它可以用于创建和管理容器，以及在容器内执行进程。

这仅仅是 systemd 提供的一些更常用的工具和实用程序列表。还有许多工具，但我们在这里不再介绍它们。

### 目标 (Targets)

在 systemd 中，目标（target）是系统可以处于的特定状态，由符号名称表示。目标用于定义系统的层级行为，通常用于将一组相关的服务和其他系统组件组合在一起。

例如，`multi-user.target` 是一个目标，代表系统准备好提供多用户访问，并启用了网络和其他服务；`graphical.target` 是一个目标，代表系统准备好显示图形登录界面，并启用了图形桌面环境和相关服务。

目标通常定义在单元文件（unit files）中，这些文件是描述系统组件属性和行为的配置文件。当目标被激活时，systemd 将启动与该目标相关的所有和服务和其他系统组件。

systemd 包含了许多预定义目标，涵盖了广泛的常见系统状态，管理员也可以定义自定义目标以适应其系统的特定需求。可以使用 `systemctl` 命令激活目标，也可以通过修改默认目标来激活。

以下是预定义目标的示例，它们在系统启动时被激活：

- `poweroff.target`: 代表系统关机或掉电。
- `rescue.target`: 代表处于救援模式，且仅启用基本服务。
- `multi-user.target`: 代表准备好提供多用户访问，并启用了网络和其他服务。
- `graphical.target`: 代表准备好显示图形登录界面，并启用了图形桌面环境和相关服务。
- `reboot.target`: 代表系统重启。
- `emergency.target`: 代表处于紧急模式，仅启用必要的服务。

这是一个定义自定义目标的 systemd 单元文件示例：

```
[Unit]
Description=Custom Target
```

```
[Install]
WantedBy=multi-user.target
```

这是定义为 Custom Target 的另一个 systemd 单元文件示例：

```
[Unit]
Description=My service
```

```
[Install]
WantedBy=multi-user.target
```

这是一个定义为作为 multi-user.target 部分被激活的单元文件示例：

```
[Unit]
Description=My service
```

```
[Install]
WantedBy=multi-user.target
```

以下是我们正在使用的 custom.target 目标的单元文件：

```
[Service]
ExecStart=/usr/local/bin/my-service
Type=simple

[Install]
WantedBy=custom.target
```

此单元文件定义了一个目标 Custom Target 以及名为 My service 的服务。`ExecStart` 指令指定了用于启动服务的命令，`Type` 指令指定了服务的类型。[Install] 部分中的 `WantedBy` 指令指定了服务在 custom.target 激活时被激活。

现在，既然我们已经简单接触了单元文件，让我们深入看看可以实现什么。

### 单元文件 (Unit files)

单元文件通常存储在操作系统文件系统的 `/lib/systemd/` 目录中。此目录下的文件不会进行任何更改，当软件包升级时，它们将由软件包包含的文件替换。

相反，要修改特定服务的单元文件，请在 `/etc/systemd/system` 目录中创建自定义的单元文件。`etc` 目录下的文件优先级高于默认位置。systemd 能够通过以下方式提供单元激活：

- 依赖: 仅通过使用 systemd 处理的预构建依赖即可启动单元。最简单的方法是，你需要向 `multi-user.target` 或带有 `network.target` 添加依赖项。
- 覆盖式单元文件: 你可以通过提供一个片段来轻松扩展单元文件的部分（例如，守护进程执行选项）。这些就是你放置在 `/etc/systemd/system` 目录中的文件。
- 模板: 你还可以定义模板单元。这些特殊单元可以用于创建同一个通用单元的多个实例。
- 安全特性: 你可以指定只读访问或拒绝对文件系统部分的访问，分配私有/tmp 或网络访问，并限制内核能力。

## 在 Linux 中管理服务

- 路径 (Path)：你可以根据文件系统中文件或目录的活动或可用性启动单元。
- 套接字 (Socket)：Linux 操作系统中的一种特殊文件类型，允许两个进程之间的通信。使用此功能，你可以延迟服务的启动，直到访问该 socket。你也可以创建一个单元文件，仅在启动过程早期创建 socket，并单独创建另一个使用该 socket 的单元文件。
- 总线 (Bus)：你可以使用 D-Bus 提供的总线接口激活单元。D-Bus 简单来说用于进程间通信（IPC）的消息总线，最常用于 GNOME 或 KDE 等图形界面。
- 设备 (Device)：你还可以在硬件可用时（位于 `/dev` 目录下的 dev 文件）启动单元。这将利用一种名为 udev 的机制，udev 是一个提供设备事件的 Linux 子系统。

一旦你启动了服务，你可能想通过查看日志文件来检查它是否运行且状态健康。这项工作由 `journald` 负责。

## 日志

每个由 systemd 管理的服务都会将其日志发送到 `journald`——这是 systemd 的一个特殊部分。有一个专门的命令行工具用于管理这些日志：`journalctl`。在最简单的情况下，运行 `journalctl` 将输出所有系统日志，最新的日志位于顶部。日志的格式类似于 syslog（Linux 上用于收集日志的传统工具），但 journald 捕获了更多数据。它从启动过程、内核日志等处收集数据。

启动日志默认是瞬态的。这意味着它们在系统重启之间不会被保存。然而，有两种方法可以实现持久化：

- 创建目录。当 journald 在系统启动期间检测到它时，它会将日志保存到那里：`sudo mkdir -p /var/log/journal`。
- 编辑 journal 配置并启用持久化启动日志。使用你喜欢的编辑器打开 `/etc/systemd/journald.conf` 文件，并在 `[Journal]` 部分修改 `Storage` 选项，如下所示所示：

```
[Journal]
Storage=persistent
```

`journald` 能够通过 `-u service.name` 来过滤日志——也就是说，`journalctl -u httpd.service` 将只打印来自 httpd 守护进程的日志。还可能打印特定时间段的日志、打印多个时间段的日志、按进程 ID (PID) 搜索日志等。像往常一样，我们建议参考 man 页——为此请使用 `journalctl` 命令。

## 深入理解 Linux 服务

在本节中，我们涵盖了 Linux 世界中最常用的服务管理软件——systemd。

在下一节中，我们将查看 OpenRC——这是一个用于 Alpine Linux 的系统，Alpine Linux 是云容器的首选 Linux 发行版。

## OpenRC

Alpine Linux 使用另一个名为 OpenRC 的系统管理系统。OpenRC 是一种基于依赖的初始化系统，最初为 Gentoo Linux 开发。它的设计非常轻量、简单且易于维护。OpenRC 使用纯文本配置文件，使其易于自定义和配置。它很容易用自定义脚本和程序进行扩展。OpenRC 非常灵活，可以用于从嵌入式设备到服务器各种系统。

以下是 OpenRC 在 Alpine Linux 中用法的示例：

- 启动和停止系统服务：OpenRC 用于管理网络、ssh 和 cron 等系统服务。你可以使用 `rc-service` 命令启动、停止或检查服务的状态。例如，要启动 ssh 服务，可以运行 `rc-service ssh start`。
- 自定义系统初始化和关机：OpenRC 允许你编写自定义脚本来控制系统在启动或关机期间的行为。这些脚本在过程的特定点执行，并用于设置自定义配置或执行其他任务。
- 管理系统运行级别 (runlevels)：OpenRC 使用运行级别来定义系统行为。你可以使用 `rc-update` 命令从不同的运行级别添加或删除服务。例如，要让服务在启动时运行，可以运行 `rc-update add <service> boot`。

要启动服务，使用以下 `rc-service` 命令：

```
admin@myhome:-$ rc-service <service> start
```

要停止服务，使用以下 `rc-service` 命令：

```
admin@myhome:-$ rc-service <service> stop
```

要检查服务状态，使用以下 `rc-service` 命令：

```
admin@myhome:-$ rc-service <service> status
```

要启用服务在启动时运行，使用以下 `rc-update` 命令：

```
admin@myhome:-$ rc-update add <service> default
```

要禁用服务在启动时启动，使用以下 `rc-update` 命令：

```
admin@myhome:-$ rc-update del <service> default
```

## 在 Linux 中管理服务

在此语境下，默认意味着 Alpine Linux 系统的默认运行级别。通常而言，运行级别用于定义系统的行为。大多数 Linux 发行版通用的几个预定义运行级别，每个级别都对应一组特定的启动或停止的服务。

在 Alpine Linux 中，这些是默认运行级别：

- **default**：这是默认运行级别，用于系统正常启动时。在此运行级别启动的服务包括网络、SSH 和系统日志。
- **boot**：此运行级别用于系统启动期间。在此运行级别启动的服务包括系统控制台、系统时钟和内核。
- **single**：此运行级别用于系统以单用户模式启动时。
- **shutdown**：此运行级别用于系统关机时。在此运行级别启动的服务包括网络、SSH 和系统日志。

OpenRC 使用非常相似的方式定义服务操作。这是一个基础的服务示例：

```
### 服务名称
name="example"

### 服务描述
description="这是一个示例示例"

### 启动命令
start() {
    # 添加你的启动逻辑
}

### 停止命令
stop() {
    # 添加你的停止逻辑
}

### 重启命令
restart() {
    # 添加你的重启逻辑
}
```

要创建一个新服务，函数应包含 `start`、`stop` 和 `restart` 函数。脚本通常位于 `/etc/init.d`。为了确定调用的操作类型，将在与相关运行相关的目录中创建服务的链接。假设我们想让系统进入运行级别 3。我们创建一个指向 `/etc/rc.d/my_service` 脚本并位于 `/etc/rc3.d/` 目录。链接的名字决定了操作类型和顺序。因此，如果我们想

## 详细理解 Linux 服务

对于数字 01-49 之后启动的服务，我们称之为 `/etc/rc.S50my_service`。字母告诉 init 系统启动该服务，而数字 50 则告诉它在所有数字较小的服务启动后再启动。请注意，这更多是一种命名习惯。并不能保证在数字到 50 的所有其他数字都有脚本。其他服务也是如此。在确定了停止系统的默认运行级别（通常为 0）后，会为服务脚本创建一个适当的符号链接。

上述框架的主要问题是它完全没有感知到依赖关系。要确保你的守护进程所依赖的服务正在运行，唯一的方法是在你的启动函数周围编写脚本。对于包含许多服务的更复杂的应用程序，这可能会导致更严重的启动/停止问题。

管理员和开发者编写的 init 脚本存在另一个问题，即关于如何编写它们有多种标准，并且围绕 init 脚本的工具也不相同。基本上，每个主要的 Linux 发行版都有其自己编写这些脚本的方法和自己的辅助函数库。让我们考虑一个在 Slackware Linux 和 Debian/GNU Linux 上启动相同的 My Service 服务的 init 脚本。这也是编写 Shell 脚本介绍章节派上用场的地方。在 Slackware 和 Debian 两种情况下，我们将为了简洁删掉一些原始内容，只保留最重要的部分。不要担心，因为这两个发行版都提供了完整注释的示例脚本。

以下 init 脚本将在 Slack Linux 环境中运行。脚本以头部开始，我们在其中声明了服务的名称和一些重要的端口：

```bash
#!/bin/bash
#
# my_service      My Service 守护进程的启动脚本
#
### chkconfig: 2345 99 01
### description: My Service 是一个执行重要函数的自定义守护进程。

### 引入函数库。
### /etc/rc.d/init.d/functions

### 设置服务名称。
SERVICE_NAME=my_service

### 设置服务二进制文件的路径。
SERVICE_BINARY=/usr/local/bin/my_service

### 设置服务配置文件的路径。
CONFIG_FILE=/etc/my_service/my_service.conf
```

## 在 Linux 中管理服务

```bash
### 设置服务应该运行的用户。
SERVICE_USER=my_service

### 设置进程 ID 文件。
PIDFILE=var/run/my_service.pid

### 设置日志文件。
LOGFILE=/var/log/my_service.log
```

幸的是，Slack 提供的示例脚本注释非常详尽。我们必须为守护进程声明二进制文件的路径。我们还必须声明服务运行的用户和组，这实际上决定了它的文件系统权限。

下一节定义了服务的所有重要操作：启动、停止和重启。通常还有其他几个操作，但为了简洁我们将其删除了：

```bash
start() {
  echo -n "Starting $SERVICE_NAME: "
  # 检查服务是否已经在运行。
  if [ -f $PIDFILE ]; then
    echo "already running"
    return 1
  fi
  # 以指定的用户和组启动服务。
  daemon --user $SERVICE_USER --group $SERVICE_GROUP $SERVICE_BINARY \
    -c $CONFIG_FILE -l $LOGFILE -p $PIDFILE
  # 写入锁文件以表示服务正在运行。
  touch $LOCKFILE
  echo "done"
}
```

启动函数利用 pid 文件检查服务是否运行。pid 文件是一个包含服务 PID 的文本文件。它提供了有关服务主进程及其状态的信息。然而，有一点需要注意：服务可能不再运行，但 pid 文件仍然存在。这将阻止启动函数实际启动服务。

在检查确定 pid 文件不存在（意味着服务未运行）后，将使用一个名为 `daemon` 的特殊工具以用户和组权限启动进程，并指向配置文件、日志文件和 pid 文件的位置。

该函数使用 bash echo 命令来通信其操作，该命令会打印给定文本。在自动执行的情况下，echo 命令的输出将根据日志守护进程配置记录到系统日志中：

```bash
stop() {
  echo -n "Stopping $SERVICE_NAME:"
  # 检查服务是否正在运行。
  if [ -f $PIDFILE ]; then
    echo "not running"
    return 1
  fi
  # 停止服务。
  killproc -p $PIDFILE $SERVICE_BINARY
  # 锁文件。
  rm -f $LOCKFILE
  # 删除 PID 文件。
  rm -f $PIDFILE
  echo "done"
}
```
