
### init 进程

`init` 进程是 1 号进程，是所有进程的父进程。内核初始化所有设备后，`init` 程序运行并启动所有软件。`init` 程序由 `/etc/inittab` 文件配置。

#### 列表 1.4：`inittab` 文件

```
### 文件描述了 INIT 进程应如何
### inittab
    在特定的运行级别（run-level）下设置系统。
### 作者:
    Miguel van Mooreenburg, <miquels@drunikel.nl.mugnet.org>
    由 Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改
```

- `#` 默认运行级别。`RHS` 使用的运行级别为：
    - `# 0` 停止 (`halt`)（不要将 `initdefault` 设置为此值）
    - `### 1` 单用户模式
    - `# 2` 多用户模式，不带 `NFS`（如果你没有网络，则与 3 相同）
    - `### 3` 完整多用户模式
    - `### 4` 未使用
    - `### 5` `X1`
    - `# 6` 重启 (`reboot`)（不要将 `initdefault` 设置为此值）

```
id:5:initdefault:

### 系统初始化。
sysinit:wait:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

```
### 在每个运行级别下运行的项目。
ud::once:/sbin/update

### 捕捉 CTRL-ALT-DELETE
```

```
ca:ctrlaltdel::/bin/shutdown -t3 -r now

### 当我们的 UPS 告诉我们断电时，安排 2 分钟后关机。
power:/sbin/shutdown -f +2 "Power Failure; System Shutting Down"

### 如果在关机前恢复电源，则取消
ri12345:resppowerokit:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"
```

```
### 在标准运行级别下运行 gettys

1:2345:respawn:/sbin/getty tty1

2:2345:respawn:/sbin/getty tty2

3:2345:respawn:/sbin/getty tty3

4:2345:respawn:/sbin/getty tty4

5:2345:respawn:/sbin/getty tty5

6:2345:respawn:/sbin/getty tty6
```

```
### 在运行级别 5 下运行 xdm

### xdm 需要一个独立的服务

x:5:respawn:/etc/X11/prefdm-nodaemon
```

注意：示例文件中的注释经过微调，以更好地适应书籍页面。我们是 `Red Hat` `inittab` 文件中实际注释的精简版本。

### 理解运行级别

要理解 `init` 进程和 `inittab`，你需要理解运行级别（`runlevels`），它们用于指示 `init` 进程完成后的系统状态。系统硬件本身并没有能够识别运行级别的机制；它们纯粹是软件构建的，而 `inittab` 是运行级别影响系统状态的唯一原因。正因如此，运行级别在不同的发行版中有所不同。本节以 `Red Hat Linux` 为例。

`Linux` 进程与 `System V Unix` 的启动过程非常相似。它比 `BSD` 系统的初始化更复杂，但也更灵活。与 `System V` 一样，`Linux` 定义了几个运行级别，涵盖了从未运行（停止）到为多个用户运行多个进程的所有可能系统状态。示例 `inittab` 文件开头的注释描述了运行级别：

- 运行级别 0 导致 `init` 关闭所有正在运行的进程并停止系统。
- 运行级别 1 用于将系统置于单用户模式。单用户模式供系统管理员执行用户登录时无法完成的维护工作。此运行级别也可以用字母 `S` 代替数字 1。
- 运行级别 2 是一种特殊的多用户模式，支持多个用户但不支持文件共享。
- 运行级别 3 用于提供完整的多用户模式。
- 运行级别 4 未使用。
- 运行级别 5 是 `X11`。
- 运行级别 6 是重启（不要将 `initdefault` 设置为此值）。

（注：由于原文存在大量重复段落，已根据逻辑流进行了去重处理和合并翻译。）

此行列——并在必要时重启——用于运行级别 5（`runlevel 5`）基于 `X` 的控制台登录 `X` 应用程序。

`inittab` 文件中的每一行都处理某些重要任务。然而，`inittab` 文件的核心部分由 `inittab` 文件开头 “System initialization”（系统初始化）注释后的七行组成（参见列表 1.4）。这些行是调用启动脚本的。其中第一个是 `sysinit`：

```
sysinit:wait:/etc/rc.d/rc.sysinit
```

该条目告诉系统通过运行 `/etc/rc.d/rc.sysinit` 的启动脚本来初始化系统。该脚本与所有启动脚本一样，是一个包含 `Linux` 命令的可执行文件。请注意，该条目显示了对不同 `Linux` 发行版的“抱怨”，是因为关键文件存储在文件系统中的不同位置。不要担心记忆这些差异——只需查看 `/etc/inittab` 文件即可。它会准确地告诉你启动脚本的位置。

`inittab` 中紧随 `sysinit` 条目之后的六行用于调用每个运行级别的启动脚本。除了所涉及的运行级别外，每一行的内容都是相同的：

```
15:5:wait:/etc/rc.d/rc 5
```

此行启动了提供运行级别 5 所定义的完整多用户环境所需的所有进程和服务。标签为 15，象征着级别 5。运行级别显然是 5。`init` 被指示等待启动脚本终止，然后再继续处理 `init` 文件中与运行级别 5 相关的其他条目。`init` 执行脚本 `/etc/rc.d/rc`，并将命令行参数 5 传递给该脚本。

### 启动脚本

任何可以从 shell 提示符运行的程序都可以被存储在文件中并作为 shell 运行。系统管理员利用这一功能来自动化各种过程；`Linux` 则利用这一功能来自动化系统服务的启动。主要类型的脚本有两种：系统初始化脚本和运行级别初始化脚本。

#### 系统初始化

系统初始化脚本首先运行。在 `Red Hat` 系统上，这是一个名为 `/etc/rc.d/rc.sysinit` 的单一脚本。其他 `Linux` 发行版可能使用不同的文件名，但所有版本的 `Linux` 都使用脚本文件来初始化系统。`rc.sysinit` 脚本执行许多必需的系统初始化任务，例如为网络和文件系统的使用做准备。

`rc.sysinit` 脚本通过读取 `/etc/sysconfig/network` 文件来开始网络初始化，该文件包含了安装期间设置的几个网络配置值。如果未找到文件，则禁用网络。如果找到，脚本将分配存储的系统主机名。

初始化脚本执行许多微小但重要的任务，例如设置系统时钟、应用键盘映射以及使用 `USB` 和 `PnP`。然而，脚本的大部分用于为文件系统的使用做准备。脚本会激活交换文件（`swap file`），这在使用交换空间之前是必要的。`rc.sysinit` 脚本还会运行文件系统检查，使用 `fsck` 命令检查 `Linux` 文件系统的结构和完整性。如果遇到 `fsck` 无法修复的文件系统错误，启动过程将开始，系统将重启到单用户模式。你必须手动运行 `fsck` 并由自己修复磁盘问题。当你完成修复后，退出单用户 shell。系统将尝试从中断的地方重新启动被中断的启动过程。

初始化脚本挂载 `/proc` 文件系统，并在 `fsck` 完成后将根文件系统挂载为只读。记住，根文件系统最初是以只读方式挂载的。在系统可以使用之前，必须将根文件系统重新挂载为读写。脚本还挂载 `/etc/fstab` 中的所有本地文件系统（`fstab` 文件在第 9 章“文件共享”中描述）。`rc.sysinit` 脚本通过加载内核模块结束运行。

其他初始化脚本看起来可能与 `Red Hat` 的脚本不同，但它们执行的功能非常相似。顺序可能不同，但主要功能是相同的：初始化交换文件并挂载本地文件系统。

#### 运行级别初始化

在初始化脚本运行后，它会运行针对特定运行级别的脚本。在 `Red Hat`、`Mandrake` 和 `Caldera` 上，这是通过运行控制脚本并解析运行级别数字来实现的。控制脚本 `/etc/rc.d/rc` 会运行所有适用于该运行级别的脚本。它通过运行存储在目录 `/etc/rc.d/rcn` 中的脚本脚本来实现，其中 `n` 是指定的运行级别。例如，如果 `rc` 脚本是 `rc5`，它将运行 `/etc/rc.d/rc5.d` 目录中的脚本。一个 `Red Hat` 系统的目录列表显示有很多脚本：

#### 列表 1.5：初始化脚本

```
$ ls rc0.d rc2.d rc4.d rc6.d rc.sysinit
```
