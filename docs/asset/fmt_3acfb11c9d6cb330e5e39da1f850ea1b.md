
abort "this host is not allowed to use dosemu"

## 启动 DOS

运行 DOSEmu 的最简单方法是在控制台或 `xterm` 窗口内使用 `dos` 命令。当你输入以下命令时：

`$ dos`

DOSEmu 将从 `/etc/dosemu.conf` 中指定的启动设备加载并启动。默认情况下，对于 Red Hat 5，这意味着从提供的磁盘镜像文件启动。图 29.1 显示了执行 `dos` 命令后 `xterm` 窗口中的 DOS 提示符。

### 图 29.1
在 `xterm` 窗口中运行 DOS

![](img/fc6031a87613cd795a3b3e870054f8f7_679_0.png)

一旦 DOS 运行，你就可以使用标准的 DOS 命令和语法从软磁盘运行程序，或者正如本章稍后所示，运行包含在重定向目录中的应用程序。

## 在独立窗口中启动 DOS

除了在当前窗口运行 DOS 之外，在运行 X Windows 时，还可以在自己的窗口中启动 DOS。你可以通过运行以下命令来实现：

`$ xdos`

`xdos` 实际上是主 `dos` 文件的链接。通过 `xdos` 链接运行程序与执行以下命令的效果相同：

`$ dos -X`

## 在 Linux 中运行 DOS 应用程序

在独立的 X 窗口中运行 DOS 的结果如图 29.2 所示。

### 图 29.2
在独立的 X 窗口中运行 DOS

![](img/fc6031a87613cd795a3b3e870054f8f7_680_0.png)

## 有用的 DOSEmu 命令

DOSEmu 自带的磁盘镜像（Red Hat 5.1 默认启动）包含了下表所示的几个命令和实用程序。

表 29.1: DOSEmu 命令
| 命令 | 描述 |
| --- | --- |
| `eject.com` | 弹出 CD-ROM 驱动器 |
| `emumouse.com` | 调整 DOSEmu 鼠标驱动程序 |
| `exitemu.com` | 退出 DOSEmu |
| `1redir.com` | 将 Unix 目录重定向到 DOS 盘器号 |
| `unix.com` | 在 DOSEmu 内部执行 Linux 命令 |

## 使用 Lredir 挂载目录

为了让 DOSEmu 变得有用，它不仅仅处理磁盘镜像或软磁盘。它必须能够访问 Linux 目录结构的部分，就像它们是 DOS 磁盘驱动一样。这种能力允许你的 DOS 环境访问存储在系统任何现有 DOS 或 Linux 分区或硬盘上的数据和应用程序。

该过程的第一步发生在 DOSEmu 环境启动之前：你需要确保想要访问的分区已挂载到 Linux 目录结构中的逻辑位置。例如，如果你有一个现有的 DOS 分区，可以将其挂载到 `/`。

一旦所有可用的目录和分区在 Linux 中均可用，你就可以通过以下命令启动 DOS 环境：

`$ dos`

或

`$ xdos`

一旦 DOS 运行，你可以使用 `lredir` 命令将 Linux 目录重定向到 DOS 盘器号。基本语法为：

```
lredir <drive letter>: linux\fs<linux> directory
```

这将导致指定的 Linux 目录通过指定的盘器号在 DOS 中可用。例如，要将 Linux 中已挂载为 `/dos` 的 DOS 分区在你的 DOSEmu 环境中作为 `D:` 可用，你可以使用命令：

```
lredir D: linux\fs$HOME
```

`lredir` 的另一个有用应用是使用用户的家目录在预指定的 DOS 盘器号上可用。要实现此，请使用我们刚刚看到的 `lredir` 命令的变体：

```
lredir E: linux\fs$(HOME)
```

在这里，用户的家目录是从 Linux 环境变量 `HOME` 获取的，Red Hat（以及大多数 Linux 版本）在该处存储当前用户的家目录。

最后，如果你是从提供的磁盘镜像启动，但希望从从加载 `config.sys` 文件开始的所有启动操作都从另一个位置（例如挂载的 DOS 分区）发生，你可以使用简单的两步技巧：

- 编辑用于启动 DOSEmu 环境的初始磁盘镜像上的 `config.sys` 文件。将以下行作为文件的第一行（假设 DOS 分区挂载在 Linux 的 `/dos` 下）：

```
install=c:\redir.exe linux\fs/dos
```
