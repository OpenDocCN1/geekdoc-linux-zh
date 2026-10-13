
# 修复启动文件系统问题（以及引导性练习）

## 实验

### 控制启动过程

![](img/3c5dfc78dee328600013666607c8aa7b_304_0.png)

## 选择启动目标

### 目标

完成本节后，你应该能够：

- 描述 Red Hat Enterprise Linux 启动过程。
- 设置启动时使用的默认目标。
- 将系统引导到非默认目标。

## 描述 Red Hat Enterprise Linux 8 启动过程

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序通过软件处理了某些特定的硬件任务。

- 机器开机。系统固件（现代 UEFI 或旧版 BIOS）运行上电自检 `POST` 并开始初始化某些硬件。

  使用 BIOS 或 UEFI 配置设置进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些设置。
- 系统固件搜索引导加载程序，即在 UEFI 启动固件中配置的设备，或按照 BIOS 配置的顺序搜索所有磁盘上的主引导记录 `MBR`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- 系统固件从磁盘读取引导加载程序并将系统控制权交给引导加载程序。在 Red Hat Enterprise Linux 8 系统上，引导加载程序是 `GRUB2`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- 引导加载程序从磁盘读取内核和 `initramfs`，并将系统控制权交给内核。在 Red Hat Enterprise Linux 8 系统上，内核初始化 `systemd` 管理器。

  使用 BIOS 或 UEFI 配置设置进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些设置。
- `GRUB2` 菜单允许你编辑内核参数并选择引导哪个内核。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- 内核启动 `systemd` 管理器作为 `PID 1`。`systemd` 随后启动命令行中指定的默认目标。

  使用 BIOS 或 UEFI 配置设置进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些设置。

### 描述 Red Hat Enterprise Linux 8 启动过程（继续）

内核初始化硬件并将根文件系统挂载为只读。如果根文件系统不在 `initramfs` 中，内核将切换到根文件系统并重新挂载为读写。然后 `systemd` 启动默认目标，将系统带入状态。

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

- 机器开机。系统固件（现代 UEFI 或旧版 BIOS）运行上电自检 `POST` 并开始初始化某些硬件。

  使用 BIOS 或 UEFI 配置设置进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些设置。
- 系统固件搜索引导加载程序，即在 UEFI 启动固件中配置的设备，或按照 BIOS 配置的顺序搜索所有磁盘上的主引导记录 `MBR`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- 系统固件从磁盘读取引导加载程序并将系统控制权交给引导加载程序。在 Red Hat Enterprise Linux 8 系统上，引导加载程序是 `GRUB2`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- `GRUB2` 菜单允许你编辑内核参数并选择引导哪个内核。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。

### 控制启动过程（继续）

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

- 机器开机。系统固件（现代 UEFI 或旧版 BIOS）运行上电自检 `POST` 并开始初始化某些硬件。

  使用 BIOS 或 UEFI 配置设置进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些设置。
- 系统固件搜索引导加载程序，即在 UEFI 启动固件中配置的设备，或按照 BIOS 配置的顺序搜索所有磁盘上的主引导记录 `MBR`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。
- 系统固件从磁盘读取引导加载程序并将系统控制权交给引导加载程序。在 Red Hat Enterprise Linux 8 系统上，引导加载程序是 `GRUB2`。

  使用 BIOS 或 UEFI 屏幕进行配置，你通常可以在启动早期按下特殊的键组合（如 `F2`）进入这些屏幕。

### 控制启动过程（继续）

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

### 控制启动过程（继续）

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

### 控制启动过程（继续）

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

### 控制启动过程（继续）

现代计算机系统是硬件和软件的复杂组合。从未定义的、关机状态到带有登录提示符的运行系统，需要大量的硬件和软件协同工作。以下列表提供了物理 x86_64 启动系统 Red Hat Enterprise Linux 8 涉及任务的高级概述。x86_64 虚拟机的列表类似，但虚拟机管理程序处理了某些特定的硬件任务。

## 第 1 章 | 控制启动过程

并非所有目标都是隔离的。你只能隔离在其单元文件中设置了 `AllowIsolate=yes` 的目标。例如，你可以隔离图形目标（`graphical target`），但不能隔离加密设置目标（`cryptsetup target`）。

```
[user@host ~]$ systemctl cat graphical.target
# /usr/lib/systemd/system/graphical.target
# ...output omitted...
[Unit]
Description=Graphical Interface
Documentation=man:system.special(7)
Requires=multi-user.target
Wants=display-manager.service
Conflicts=rescue.target
After=multi-user.target rescue.target display-manager.service
AllowIsolate=yes
[user@host ~]$ systemctl cat cryptsetup.target
# /usr/lib/systemd/system/cryptsetup.target
# ...output omitted...
[Unit]
Description=Local Encrypted Volumes
Documentation=man:system.special
```

## 设置默认目标
