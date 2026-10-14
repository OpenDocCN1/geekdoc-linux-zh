
“与正在运行内核匹配的内核源码树包含目录的位置在哪里？（`/lib/modules/$(uname -r)/build`）。在脚本进行猜测之前，获得正确的答案至关重要。在这里，我们运行的是 Linux 2.4 系列的内核，它会创建一个从 `/lib/modules/version/build` 指向内核源码树的符号链接，其中 `version` 是 Linux 内核版本。如果你移动或删除了内核源码，此链接将失效，你需要引导 `vmware-config.pl` 指向正确的方向。”

一旦你输入了路径，脚本就会解压并构建模块，并在过程中打印这些消息：

正在提取 vmmon 模块的源码。

正在构建 vmmon 模块。

```
make: Entering directory /tmp/vmware-config0/vmmon-only'
make[1]: Entering directory /tmp/vmware-config0/vmmon-only'
make[2]: Entering directory /tmp/vmware-config0/vmmon-only/driver-2.4.9'
make[2]: Leaving directory /tmp/vmware-config0/vmmon-only/driver-2.4.9'
make[2]: Entering directory /tmp/vmware-config0/vmmon-only/driver-2.4.9'
make[2]: Leaving directory /tmp/vmware-config0/vmmon-only/driver-2.4.9'
make[1]: Leaving directory /tmp/vmware-config0/vmmon-only'
make[1]: Leaving directory /tmp/vmware-config0/vmmon-only'
```

脚本尝试加载模块。成功后，你将看到此消息：

模块在正在运行的内核中完美加载。

如果构建失败，可能是因为你的内核源码树没有通过 `make prepare` 等命令进行设置，或者是因为你尝试构建一个 VMware 不支持的内核。如果你的内核非常新，后者的可能性较大；请访问 VMware 网站查看 VMware Workstation 的更新。

如果模块加载失败，通常会伴随着大量关于未知符号的错误消息，这表明你指定的内核头文件与你当前的内核不匹配。

# 第 3 章：安装 VMware Workstation

有一种极小的概率，插入使用不匹配头文件构建的模块会导致内核 oops（Linux 内核崩溃），这可能会导致整个系统崩溃。无论什么情况下，在 oops 之后重启通常都是好主意。

还有一种可能，你的内核版本与 VMware 的预构建模块之一匹配，但由于你的自定义设置而无法正常工作。在这种情况下，你必须使用 `vmware-config.pl --compile` 强制脚本编译模块。

除了 `vmmon` 模块外，你还需要 `vmnet` 模块来为 VMware 下的虚拟机启用主机主机或桥接网络。构建过程相同。如果 `vmmon` 构建成功，`vmnet`几乎也能正常工作。取决于你的内核版本，你可能还需要 `vmportuser` 来支持双向并行端口。

## 启动 Linux VMware Workstation

假设你在安装脚本中安装的二进制文件在你的路径中，你现在可以作为普通用户使用 `vm` 命令启动 VMware。

当 VMware 启动时，你将看到 VMware 窗口和一个要求你输入序列号（许可证密钥）的框。你需要许可证才能对 VMware Workstation 进行任何实际工作。如果你尝试在没有许可证的情况下启动，VMware 将禁用虚拟机的开启功能。访问 http://www.vmware.com/ 获取临时评估版许可证密钥或购买完整版。

处理好许可证密钥后，你有三个选择：运行配置向导、运行配置编辑器或打开现有配置。注意：如果是你第一次使用，请使用配置向导。

| 选项 | 描述 |
| :--- | :--- |
| 运行配置向导 | 开启虚拟机 |
| 运行配置编辑器 | 检查虚拟机 |
| 打开现有配置 | 检查虚拟机 |
| -x | 开启虚拟机 |
| -X | 开启虚拟机 |
| -name=value | 修改 VMware 名称 |
| -v | 显示当前统计信息 |
| -file.vmdk | 检查虚拟磁盘 |
| -Y.vmdk | 检查虚拟磁盘 |

## 3.12 VMware Workstation 启动脚本

当你重启机器时，正在运行的内核没有模块，除非自动加载器或其他机制加载了它们。由于 VMware 需要 `vmnet` 模块，且在你作为用户运行时无法加载它，脚本会在启动时自动激活它。如果你的 Linux 系统使用 V init 系统，你的启动脚本位于 `/etc/init.d` 或 `/etc/rc.d`。VMware 安装程序在该目录下放置一个新的 `vmware` 脚本。要启动服务，让启动 root（假设你的 init.d 目录是 `/etc/init.d`）运行以下：

```
/etc/init.d/vmware start
```

要停止服务，使用此命令：

```
/etc/init.d/vmware stop
```

要获取 VMware 子系统的当前状态（包括激活的虚拟机数量），输入

```
/etc/init.d/vmware status
```

注意 对于 Red Hat 系统，使用 `/etc/rc.d/init.d/vmware` 代替 `/etc/init.d/vmware`。

VMware 安装程序会查找默认运行级别目录，并在其中创建一个 `S90vmware` 链接，该链接指向 `init.d` 目录下的 `vmware` 脚本。该链接建立后，在系统启动时会带有 `start` 参数运行 vm 脚本，从而启动你的 VMware 服务。同样，安装程序会查找你的系统关机运行级别（通常为 6），并在其中创建一个 `K8vmware` 链接，以便在系统正常关机时有序关闭服务。

由于安装程序在升级时使用了 `init.d/vmware` 系统启动脚本，该启动脚本与普通的 `init.d/vmware` 脚本略有不同，它在实际启动或停止 VMware 子系统之前定义了几个实用函数。

如果你不知道什么是 Bourne shell（伯恩壳），你可能不想更改（甚至不想查看）该启动脚本。你只需要知道，它会加载 `vmmon`、`vmnet` 和 `vmppuser` 模块，并在仅主机网络或 NAT 网络上启动 VMware 版本的 dhcdcp。

## 3.13 /etc/vmware 和 /dev 中的附加文件

VMware 安装程序会在你的系统上创建一个名为 `/etc/vmware` 的目录，其中存储了关于宿主机的所有配置信息。

### locations（位置）

`locations` 文件记录了 VMware 安装程序创建、移动或删除的所有文件和目录；如果 `vmware-config.pl` 需要添加新的内核模块，可能会向此文件追加内容。此外，`locations` 包含 VMware 启动脚本的配置数据（见第30页第3.11节），包括所有的网络设置。不要将其与配置文件中的参数（见下文）混淆。

卸载程序使用 `locations` 来确定卸载时需要删除的内容。此文件还提供了一种方便的方法，用于判断系统上的文件是否来自 VMware 安装、将 VMware 移动到另一台机器，或在几台机器上分发 VMware 安装。

### config（配置）

配置文件主要包含 VMware 二进制文件和库的完整路径，以及一些默认参数。`vm` 可执行程序加载这些值作为所有配置的默认值。你通常不需要更改此文件。

### installer.sh

`installer.sh` 文件是一个通常由 VMware 安装、配置和卸载工具运行的实用程序。虽然你通常不需要理会这个文件，因为它只是一个 shell 脚本，但你可以跳转到文件末尾查看其参数的作用。

## 第3章：安装 VMware Workstation

### /etc/vmware/vmnet 目录

如果你使用仅主机 NAT 网络配置了 VMware，你可能在 `/etc/vmnet` 中拥有一个或多个 `vmnet` 目录。这些目录包含运行在每个 vmnet 仅主机网络接口上的工具的配置文件。我们将在第9章中详细讨论此。

### not_configured（未配置）

你可能在 `/etc/vmware` 中看到 `not_configured` 文件，这是一个标志，告诉 VMware 服务启动程序运行 VMware 之前需要运行 `vmware-config.pl`。如果你在安装过程中选择不运行 `vmware-config.pl`，或者 VMware 启动脚本（`/etc/init.d/vmware`）未能运行其任何组件，则可能会出现此文件。在你启动 `vmware-config.pl` 时，它也可能出现。
