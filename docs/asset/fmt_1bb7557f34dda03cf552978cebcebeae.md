
如果系统在启动时卡住并显示“PCMIA: Starting services”消息或发生其他奇怪的情况，可以在启动提示符处输入 `NOPCMIA=yes` 以防止在下次系统启动时启动 PCMIA。为了进一步隔离错误，请手动使用以下命令（以 root 用户身份）加载 PCMIA 系统的三个基础模块：

```
modprobe -t <dir> pcmcia_core
modprobe -t pcmcia-external i82365
```

对于外部 PCMIA，或

```
modprobe -t pcmcia yenta_system
```

对于内核 PCMIA（在极少数情况下，使用 `modprobe -t <dir> toic`）

以及

```
modprobe -t <dir> ds
```

关键模块是前两个。如果在加载 `pcmia_core` 时发生错误，请参阅 `pcmia_core` 的手册页以获取更多信息。使用为为 `modprobe` 测试中描述的选项进行首次测试。例如，关闭 PCMCIA 模块的 APM 支持。在某些情况下，这可能会出现问题。使用设置 `do_apm=0` 来停用电源管理：

```
modprobe -t <dir> pcmiacore do_apm=0
```

如果所选选项成功，请将其写入 `/etc/sysconfig/pcmia` 中的变量 `PCMIA_CORE_OPTS` 以永久使用：

```
PCMIA_CORE_OPTS="do_apm=0"
```

如果选择 I/O 被其他组件占用可能会出现问题。通过使用 `probe_io=0` 避免这种情况：

```
PCMIA_CORE_OPTS="do_apm=0"
```

如果在加载 `i8265` 模块时发生错误，请参阅 `i8265` 的手册页以获取更多信息。如果中断、I/O 端口或内存区域被占用，则会导致资源冲突。检查 I/O 可能会导致问题。在这种情况下，使用 `do_apm=0` 来：

```
PCMIA_CORE_OPTS="do_apm=0"
```

系统资源的分配可以通过 `manddev` 进行监控（多个 PCI 设备共享相同的 IRQ 是正常的）。一种可能的解决方案是使用 `list=9,10` 来：

```
PCIA_CORE_OPTS="list=9,10"
```

模块 `i82365` 的合适的选项（许多驱动模块都有选项）。通过命令 `modinfo /lib/modules/<pcmciirectory>/<driver>` 找到这些（需要完整的路径才能找到正确的驱动）。大多数模块都带有手册页。`rpm -ql pcmia | grep man` 列出了 `pcmia` 包包含的所有手册页。

## 工作异常或无法使用的 PCMCIA 卡

这里基本上有三种情况：未检测到卡、驱动程序无法加载或接口设置错误。确定卡是由卡管理器还是热插拔管理的。对于外部 PCMIA，卡管理器始终接管控制。对于内核 PCMIA，卡管理器管理卡。在这里，只有卡被管理。

## 无法识别的卡

`/var/log/messages` 中的“Unsupported Card in Slot x”表示卡管理器未能为卡分配驱动程序。该数据库可以使用现有条目作为参考轻松扩展。使用 `cardctl` 找出卡如何识别自己。修改 `/etc/pcmmia/config` 或 `/etc/pcmmia/*.conf` 后，重新加载驱动分配。

## 驱动未加载

驱动数据库中卡和驱动的错误分配可能导致驱动未加载。这可能是因为在看似相同的卡中使用了不同的芯片。替代驱动程序可能比默认分配更好地支持某个特定的卡。在这些情况下，需要卡的精确信息。如果需要，可以高级支持服务或通过邮件列表获取进一步帮助。

资源冲突可能是驱动未加载的另一个原因。对于 PCMCIA 卡，操作哪个 IRQ、I/O 端口或内存区域无关，但存在例外。首先只测试一个卡，如果，关闭其他系统组件，如声卡、红外、调制器或打印机。系统资源的分配可以通过 `manddev` 进行监控（多个 PCI 设备共享相同的 IRQ 是正常的）。一种可能的解决方案是使用 `i82365` 模块的合适的选项（许多驱动模块都有选项）。通过命令 `modinfo /lib/modules/<pcmciirectory>/<driver>` 找到这些（需要完整的路径才能找到正确的驱动）。大多数模块都带有手册页。`rpm -ql pcmia | grep man` 列出了 `pcmia` 包包含的所有手册页。

该模块正在使用正确的 PCMCIA 系统。找到解决方案后，可以在 `/etc/pcmia/config.opts` 文件中允许或禁止特定资源的使用。你甚至可以为卡驱动程序指定选项。例如，如果模块 `pcnet_cs` 应该专门在 `IRQ5` 上运行，则需要以下条目：

```
module pcnet_cs opts irq_list=5
```

100/100-Mbit 网卡有时会出现一个问题，即传输方式自动识别不正确。使用 `ifport` 或 `mii_tool` 命令来查看和修改传输方式。为了让这些命令自动运行，必须调整 `/etc/pcmia/network` 脚本。

### 接口配置错误

在这种情况下，建议检查接口配置以消除配置错误。对于网卡，可以通过为 `/etc/sysconfig/network/config` 中的变量赋值 `DEBUG=yes` 来增加网络脚本的详细程度。对于其他网卡，或者如果此方法没有帮助，仍然可能通过显卡管理器在脚本中插入 `set -x` 行（参见 `/var/log/messages`）。这样，脚本的每个单独命令都会记录在日志中。如果你在脚本中发现了关键部分，可以在终端中输入相应的命令进行测试。

## 1.7.5 使用 PCMCIA 安装

如果你想通过网络安装，或者 CD-ROM 依赖 PCMCIA，则在安装时就已经需要 PCMCIA。要实现这一点，需要一个启动软盘以及其中一个模块软盘。

从软盘启动（或从 CD 选择“手动安装”启动）后，将启动模块 `linuxrc`。选择“Kernel Modules (Hardware Drivers)” -> “Load PCMCIA Module”。将出现两个输入字段，用于输入模块 `pcmia_core` 和 `i82365` 的选项。通常情况下，这些文件可以留空。`pcmia_core` 和 `i82365` 的帮助页以文本文件的形式位于第一张 CD 的目录中……

然后使用外部 PCMCIA 系统安装 SUSE LINUX。安装期间，系统消息会发送到虚拟控制台。使用 `(Alt)+(功能键)` 切换到这些控制台。之后当图形界面激活时，使用 `(Ctrl)+(Alt)+(功能键)`。

在安装过程中，有多个终端可以运行命令。只要 `linuxxc` 运行，请使用控制台 9（一个非常简陋的 shell）。YaST 启动后，控制台 2 将提供 Bash shell 和许多标准系统工具。

如果在安装期间加载了错误的 PCMCIA 卡驱动模块，必须手动修改启动软盘。这需要对 Linux 有深入了解。第一部分安装完成后，系统部分或完全重启。启动 PCMCIA 时，系统可能会挂起。此时，安装已达到高级阶段。你可以使用 `PCMCIA=` 启动选项以无 PCMCIA 模式启动 Linux。参见第 156 页的 7.1.4 节。你甚至可以在第一部分完成之前的第二个控制台上更改某些系统设置，以确保重启成功。

### 7.1.6 其他实用

`cardctl` 是获取 PCMCIA 信息和执行某些操作的重要工具。在 `cardctl` 中可以找到许多细节。只需输入 `cardctl` 即可获取有效命令列表。

主要功能可以通过图形前端 `cardinfo` 控制。为了进行此工作，必须安装 `pcmcia-cardinfo` 包。

来自 `pcmcia` 包的其他有用程序包括 `ifport`、`ifuser`、`probe` 和 `rpcmcia`。这些并不是总是需要的。要查找 `pcmcia` 中包含的所有内容，使用命令 `rpm -ql pcmia`。

### 7.1.7 更新内核或 PCMCIA 包

如果你想更新内核，应该使用 SUSE LINUX 提供的内核包。如果需要编译自己的内核，则必须重新编译 PCMCIA 模块。在重新编译这些模块时，新内核必须已经在运行状态，这一点非常重要，因为会从中提取各种信息。此时 `pcmcia` 包应该已经安装，但尚未启动。如有疑问，请运行命令 `rpcmcia stop`。安装 PCMCIA 包并运行 `rpm -ba /usr/src/packages/SPECS/pcmcia.spec`。

新包将存储在 `/usr/src/packages/RPMS/` 中。`pcmcia-modules` 包包含外部 PCMCIA 的 PCMCIA 模块。此包必须使用 `kernel rpm --force` 安装，因为模块文件在官方上属于内核包。

### 7.1.8 更多信息
