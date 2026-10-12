
### 管理工具

作为一名 Linux 管理员，你有许多其他可用工具。本节涵盖的工具并不难使用，但可以在许多方面帮助到你。虽然我已经向你展示了如何挂载 Red Linux 安装 CD，但如果你能通过网络从单一源访问 Red Linux 安装文件，将会变得更容易。

换句话说你作为管理员的经历：错误总会发生。关键文件可能会丢失，或者缺乏经验的 Linux 管理员可能会犯错。为了理解可能出错的地方，我将向你介绍 Linux 启动过程的基础。然后我将向你展示如何使用 Linux 救援盘。最后，我将帮助你学习更详细地管理你的用户。

## 管理安装文件

第 2 章展示了如何使用 `rpm` 命令安装和删除 RPM 包。但对于系统管理员来说，该命令是不够的。有三张 Red Hat 安装 CD，你并不总是随身携带 CD。

## 创建安装源

一旦你将 Red Hat 安装文件复制到网络上的单一源，你就可以像连接其他 Samba 目录一样连接它。要复制 Red Hat 安装文件，首先创建一个共享目录，从第一张 CD 复制 `base` 和 `rpm` 子目录，然后从第二张和第三张安装 CD 复制 RPM 包。我假设你已经知道如何在 Microsoft 计算机（Windows）上执行这些操作。无论何种情况，你都需要一台拥有约 2GB 空闲空间的计算机。要在 Linux 计算机上设置此项，请遵循以下步骤：

1. 以 `root` 用户身份登录。如果你在 GUI 中，请打开一个命令行界面。在桌面上点击右键，并在弹出菜单中点击“新建终端”（New Terminal）。
2. 为安装文件创建一个单独的目录。为了练习，我将创建 `/mnt/source` 目录。

```
mkdir /mnt/source
```

3. 挂载 Red Hat 安装 CD。如果你在 GUI 中，插入 CD 时这会自动发生；否则运行以下命令：

```
mount /mnt/cdrom
```

4. 从第一张 CD 复制所需的文件和目录。记住，因为你正在传输数百 MB 的文件，这可能需要几分钟。如表 3 所示，以下命令将 `RedHat` 目录下的所有文件复制到 `/mnt/source`：

```
cp -r /mnt/cdrom/RedHat/* /mnt/source
```

5. 卸载第一张 CD 并插入第二张 CD。如果你在 GUI 中，插入 CD 时这会自动发生；否则运行以下命令：

```
umount /mnt/cdrom
mount /mnt/cdrom
```

6. 从第二张 CD 复制所需的文件和目录。记住，因为你正在传输数百 MB 的文件，这可能需要几分钟。如表 3 所示，以下命令将 `RedHat` 目录下的所有文件复制到 `/mnt/source`：

```
cp -r /mnt/cdrom/RedHat/* /mnt/source
```

7. 卸载第二张 CD 并插入第三张 CD。如果你在 GUI 中，插入 CD 时这会自动发生；否则运行以下命令：

```
umount /mnt/cdrom
mount /mnt/cdrom
```

8. 从第三张 CD 复制所需的文件和目录。记住，因为你正在传输数百 MB 的文件，这可能需要几分钟。如表 3 所示，以下命令将 `RedHat` 目录下的所有文件复制到 `/mnt/source`：

```
cp -r /mnt/cdrom/RedHat/* /mnt/source
```

## 第 8 章：管理与维护 251

```
# 由 anaconda 生成的 grub.conf
#
# 注意：修改此文件后，你不需要重新运行 grub
# 注意：你有一个 /boot 分区。这意味着
# 所有内核和 initrd 路径都是相对于 /boot/ 的，例如：
### root (hd0,1)
# kernel/vmlinuz-version ro=/dev/hda3
### initrd/initrd-version.img
#boot=/dev/hda3
default=0
timeout=30
splashimage=(hd0,1)/grub/splash.xgm
title Red Hat Linux 2.4.0-29
root (hd0,1)
kernel/vmlinuz-2.4.0-29 ro=LABEL; hd=ide-scsi
initrd/initrd-2.4.0-29
title Windows Server
root=(hd0,0)
chainloader +1
```

**图 6. 为双启动配置的 GRUB。**

与传统的启动引导加载程序（如 `LILO` 或 Windows 的 `NTLDR`）不同，你不需要编写引导加载程序来更改任何硬盘的引导记录（`MBR`）。正如你可能从第 1 章记得的，我在安装 Red Hat Linux 时将 `/boot` 目录挂载在单独的分区上。下面的通知表明 Linux 内核（`vmlinuz`）和初始 RAM 磁盘（`initrd` 文件）都存储在 `/boot` 目录中。

> **注意：你有一个 `/boot` 分区。这意味着**
> 所有内核和 `initrd` 路径都是相对于 `/boot/` 的，例如：
> `root (hd0,1)`
> `kernel/vmlinuz-version ro=/dev/hda3`
> `initrd/initrd-version.img`

现在这里很容易混淆。`root (hd0,1)` 注释告诉我 `/boot` 目录位于第一块硬盘 (0) 的第二个分区 (1) 上。`root=/dev/hda3` 注释告诉我，顶层目录（也称为“根目录”）位于第一块 IDE 硬盘的第三个分区上。

> Linux 对 `root` 的不同定义很容易让人迷失。有一种 `root` 用户（根用户），它是 Linux 计算机上的管理员用户。`root` 用户的家目录是 `/root`。`/root` 目录只是一个子目录。Linux 中的顶层目录 `/` 也称为根目录。在 GRUB 配置文件中，`root(hd0,1)` 变量代表包含 `/boot` 目录的分区。

最后，接下来的注释告诉我 Linux 的 `/boot` 目录位于我电脑上的第一块 IDE 硬盘上：

```
#boot=/dev/hda
```

如果 `/boot` 设备位于第一块 SCSI 硬盘上，那么这一行将读为：

```
#boot=/dev/sda
```

![](img/6ee4859e736a0839007ea9afb576c195_271_0.png)

# 面向 Windows 网络管理员的 Linux 迁移

我们刚刚查看了注释。现在让我们看看 `grub.conf` 配置文件中的实际命令。第一个命令指向默认操作系统。换句话说，以下命令将 Red Hat Linux 设置为默认值：

```
default=0
```

如果我在此文件中将该变量改为 `default=1`，它将指向第二个配置段（stanza），从而将 Microsoft Windows Server 设置为默认值。下一个命令设置了超时；在这种情况下，如果我在 10 秒内没有运行命令或点击向上或向下箭头，GRUB 将自动启动默认操作系统。

```
timeout=10
```

Red Hat Linux 有它自己的标准图形图像，带有 GRUB 引导加载程序，这与 `splashimage` 命令相关。根据文件中早前的 `root(hd0,1)` 注释，`splash.xpm` 文件位于 `/boot/grub` 目录中。

```
splashimage=(hd0,1)/grub/splash.xpm.gz
```

你很快就会看到它是什么样的。首先，让我们看看第一个配置段。`title` 命令设置你在 GRUB 菜单中看到的标签：

```
title Red Linux (2.4.0-29)
```

下一行告诉 GRUB `/boot` 目录的位置。正如之前描述的，它在第一块 IDE 硬盘的第二个主分区上：

```
root (hd0,1)
```

接下来的行实际上代表了三个命令。命令的第一部分告诉我，GRUB 可以在 `/boot` 目录的 `vmlinuz-2.4.0-29` 文件中找到内核，并且它应该以只读 (`ro`) 文件的形式读取到操作系统。命令的下部分标记了 Linux 的顶层目录 `/`。命令的最后部分是发送给内核关于 `hdc` 的消息，通常代表 PC 上的 CD 驱动器。Linux 需要 `ide-scsi` 设备来读取某些 CD 驱动器，并且 Red Linux 安装过程会自动包含所需的驱动程序：

```
kernel /vmlinuz-2.4.0-29 ro root=LABEL=/hdc=ide-scsi
```

当 Red Hat Linux 启动你的系统时，它首先加载初始 RAM 磁盘，该磁盘从 Linux 加载其他驱动程序到你的计算机。下一行确定 `/boot` 目录中初始 RAM 磁盘的位置。

```
initrd /initrd-2.4.0-29.img
```
