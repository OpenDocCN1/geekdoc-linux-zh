
![](img/110fa0d6324f0893fff03cee6394144d_115_0.png)

图 3.17 – TrustBoot 概述

### 注意

你可以通过阅读 kernel.org 存档看到 Oracle 的一些努力：https://lore.kernel.org/lkml/2023050415023.835096-1-ross.oracle.com/

# 工作原理

TrustBoot Loader 由 Linux 和 u-root 等知名组件组成。让我们仔细查看主要组件：

- 启用了 TrustBoot 的内核集成 u-root initfs
- 作为 u-root 扩展的 TrustBoot 安全引擎
- 可由引导程序加载的新映像

此构建过程所示：

![](img/110fa0d6324f0893fff03cee6394144d_116_0.png)

图 3.18 – TrustBoot 映像过程

使用 TrustBoot 的主要优势如下：

- **安全启动**：TrustBoot 提供了一个安全启动过程，确保系统上只执行受信任的软件。这防止了可能损害系统的恶意软件的执行。
- **运行时完整性**：TrustBoot 通过在运行时验证软件和数据的完整性，确保系统在启动后保持安全。它利用 Intel SGX 和 AMD SEV 等技术提供硬件隔离和证明。
- **防御攻击**：TrustBoot 针对各种类型的攻击提供了保护，包括固件攻击、恶意软件和内核根 root程序。
- **平台无关**：TrustBoot 是平台无关的，可以在不同的硬件平台上使用，包括 x86、Arm、RISC-V。
- **开源**：TrustBoot 是一个开源项目，这意味着任何人都可以检查代码并为其开发贡献。

# 移除 RHCK

在本教程中，你将学习如何移除 RHCK 及其独特的包依赖，同时保留所有依赖。请记住，在安装 Oracle Linux 时，安装程序会自动安装 Oracle UEK 作为默认内核，但你可以为了兼容性安装 RHCK。

## 如何操作

让我们看看如何从系统中移除 RHCK：

1. 首先，让我们使用 `grubby` 命令检查系统中运行的所有内核：

```bash
[root@ol8 ~#] grubby --ALL
index=0
kernel=/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-8.91.4.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-8.91.4.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-8.91.4.1.el8uek.x86_64
index=1
kernel=/boot/vmlinux-5.15.0-60.5.1.el8uek.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-5.15.0-60.5.1.el8uek.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (5.15.0-60.5.1.el8uek.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-5.15.0-60.5.1.el8uek.x86_64
index=2
kernel=/boot/vmlinux-4.18.0-425.13.1.el18_7.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_params
root=/dev/mapper/ol-root
initrd=/boot/initramfs-4.18.0-425.13.1.el18_7.x86_64 $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18_7.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-4.18.0-425.13.1.el18_7.x86_64
index=3
kernel=/boot/vmlinux-4.18.0-425.13.1.el18.x86_64
args=ro crashkernel-auto resume=/dev/mapper/ol-swap root.lv=/root root.lv-ol/s rw rh quiet $tuned_initrd
root=/dev/mapper/ol-root
initrd=/boot/initramfs-rescue-3f12beec0d247d9bb3922429792aaal $img $tuned_initrd
title="Oracle Linux Server 8 (4.18.0-425.13.1.el18.x86_64)"
id=3f12beec0d247d9bb3922429792aaal-0-rescue
[root@ol8 ~#]
```

![](img/110fa0d6324f0893fff03cee6394144d_118_0.png)

我们可以从前面的输出中看到，默认内核为 `/boot/vmlinux-5.15.0-8.91.4.1.el8uek.x86_64`，它是一个 UEK 内核；我们可以看到安装了多个类型的 RHCK（红帽兼容内核），即 `/boot/vmlinux-4.18.0-425.13.1.el18_7.x86_64` 和 `/boot/vmlinux-4.18.0-425.13.1.el18.x86_64`，我们可以安全地删除它们。

2. 现在既然我们知道正在使用 UEK，可以在 Oracle Linux 机器上使用 `dnf remove kernel` 命令安全地删除所需的 RHCK。它将检测到未使用的内核并显示它们的依赖关系。
