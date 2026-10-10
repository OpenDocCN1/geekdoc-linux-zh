
## 内核调试

这组选项允许你调试内核，并使用 SysRq 键（相当于按下 Alt+Print Screen）在系统崩溃后立即获取重要的状态信息。如果你是预计需要调试内核的 Linux 开发者，这些信息将非常有用。大多数用户会选择回答“否”以禁用这些选项（因为大多数用户运行的是稳定版本的内核，且并不预期需要修复内核错误）。

## 安全选项

通过这些选项，你可以包含对 Security Enhanced Linux（SELinux，安全增强型 Linux）的支持，该技术由美国国家安全局（NSA）开发。SELinux 随 Linux 附带提供，但你可以通过在启动时提供 `selinux=0` 作为启动选项来将其关闭。有关 SELinux 的更多信息，请访问 www.nsa.gov/selinux。

## 加密支持

这组选项用于在内核中启用加密支持。你可以启用支持，如下选项的默认选择所示：

*   加密选项
    *   加密 API (CRYPTO) [Y/?] Y
    *   HMAC 支持 (CRYPTO_HMAC) [Y/?] Y
    *   空算法 (CRYPTO_NULL) [M/n/?]
    *   MD4 摘要算法 (CRYPTO_MD4) [M/n/y/?]
    *   MD5 摘要算法 (CRYPTO_MD5) [Y/m/?]
    *   SHA1 摘要算法 (CRYPTO_SHA1) [M/y/?]
    *   SHA256 摘要算法 (CRYPTO_SHA256) [M/n/y/?]
    *   SHA384 和 SHA512 摘要算法 (CRYPTO_SHA512) [W/n/y/?]
    *   ... 省略的行 ...

你还可以启用对某些硬件加密设备的支持，并构建几个循环冗余校验（CRC）算法的模块。

## 构建内核和模块

在配置完内核选项后，你必须构建内核。这部分可能需要一些时间。根据你的系统不同，制作新内核可能需要几分钟到一小时以上。

在单行中输入以下内容以启动该过程：

```
make
```

## 安装模块

make 命令会创建新内核，以及通过配置步骤指定的任何模块。

![](img/792720823146d68f19fd50c99ebfce4b_517_0.png)

随着内核的构建，你会在屏幕上看到许多消息。完成后，新内核以名为 `bzImage` 的压缩文件形式出现在内核源代码所在位置的 `arch/i386/boot` 子目录中。

要使用新内核，你必须将内核文件和 `System.map` 文件复制到一个特定的名称下的 `/boot` 目录中，并编辑 GRUB 菜单以设置 GRUB —— 即启动加载程序。然而，在进行内核安装之前，你必须先安装模块并构建一个新的初始 RAM 磁盘。

如果你在内核配置过程中选择了任何模块，内核构建步骤也会构建这些模块。你只需安装它们即可。使用以下命令执行此任务：

```
cd /usr/src/linux*
make modules_install
```

`make modules_install` 命令会将所有模块复制到 `/lib/modules` 目录下的一个新子目录中。该子目录的名称应与内核版本号相同。

现在你可以安装内核并使其可供 GRUB 启动。

## 创建初始 RAM 磁盘文件

新内核需要一个新的初始 RAM 磁盘文件，你可以使用 `mkinitrd` 命令来创建它。通常，初始 RAM 磁盘映像存储在一个以 `initrd` 开头的文件中。正如你可能猜到的那样，`initrd` 是初始 RAM 磁盘的缩写，而 `mkinitrd` 命令之所以这样命名，是因为它创建 `initrd` 文件。

`mkinitrd` 程序位于 `/sbin` 目录中，你必须以 root 身份登录，并使用以下形式创建 initrd 文件：

```
/sbin/mkinitrd /boot/initrd-filename.img module-directory
```

initrd 文件必须位于 `/boot` 目录中，内核也位于此目录。你可以为 `initrd-filename` 使用任何文件名。`module-directory` 是 `/lib/modules` 中存放新内核模块文件的目录名称。`make modules_install` 步骤将模块放入一个以内核版本号命名的目录中。例如，如果你的内核版本（由 `uname -r` 命令报告）是 2.6.11，那么在 `make modules_install` 步骤后，`module-directory` 就是 `2.6.11`。

另一种常见的做法是通过将模块目录名称附加到 `initrd` 前缀之后来创建 `initrd` 文件名。因此，对于模块目录 2.6.11，`initrd` 文件将是 `initrd-2.6.11.img`。

要为新构建的内核创建初始 RAM 磁盘映像，请输入以下命令：

```
/sbin/mkinitrd /boot/2.6.11.img 2.6.11
```

此命令在 `/boot` 目录中创建文件 `initrd-2.6.11.img`。你必须在 GRUB 菜单文件（Fedora Core 中的 `/etc/grub.conf` 以及 Debian 和 SUSE 中的 `/boot/grub/menu.lst`）中引用此 `initrd` 文件。

## 安装新内核并设置 GRUB

大多数 Linux 发行版使用 GRUB 从磁盘加载 Linux 内核。你必须将新内核添加到 GRUB 菜单中，以便 GRUB 可以将其显示为可启动的选项。

在 Debian、MEPIS、SUSE 和 Ubuntu 中，GRUB 菜单是 `/boot/grub/menu.lst` 文件。在 Fedora Core 中，GRUB 菜单由 `/etc/grub.conf` 文件指定。你应该编辑适用于你发行版的文件。

以下是我系统中一个典型的 GRUB 菜单文件：

```
default
   0
# 设置超时（以秒为单位），在此之前自动启动默认项
#（通常是定义的第一个条目）。
   timeout
   5

# Ubuntu Linux
title		Ubuntu, kernel 2.6.10-5-386
root	(hd0,4)
kernel		/vmlinuz-2.6.10-5-386 root=/dev/hda3 ro acpi=off quiet splash
initrd		/initrd.img-2.6.10-5-386

# 下一个条目由 Debian 安装程序为 /dev/hdb3 上现有的
# linux 安装自动添加。
title Xandros on /dev/hdb3
root	(hdl,2)
chainloader	+1

# Windows XP
title		Windows XP
root	(hd0,1)
chainloader	+1
```

![](img/792720823146d68f19fd50c99ebfce4b_518_0.png)

以下是 GRUB 菜单文件中某些行的含义（以 # 开头的行是注释）：

-   **default 0：** 指定第一个启动项为 GRUB 启动的默认项。如果该行设置为 1，则 GRUB 启动第二个条目（2 意味着第三个条目，3 是第四个，等等）。
-   **timeout 5：** 使 GRUB 在等待 5 秒后自动启动默认项。如果文件中有其他启动项，用户可以从 GRUB 显示的启动菜单中选择其他项。
-   以 *title* 开头的行构成了第一个启动项或部分（下一个条目以另一个 *title* 行开始），此条目定义了 GRUB 可以启动的特定内核文件。你可以通过向配置文件添加类似的节来让 GRUB 启动另一个内核。此启动项中各行的含义如下：
    -   **root (hd0, 4)：** 将 *root* 设备设置为第一个硬盘的第一个逻辑分区。在此特定系统中，此分区是安装 Ubuntu 的 Linux 内核的位置。
    -   **kernel /vmlinuz-2.6.10-5-386 root=/dev/hda3 ro acpi=off quiet splash：** 标识如果用户选择此启动项，GRUB 将加载的内核。在这种情况下，内核文件是 */vmlinuz-2.6.10-5-386*，它位于 *root* 设备中。在 Linux 系统中，该分区通常挂载在 */boot* 目录上。换句话说，GRUB 加载内核文件 */boot/vmlinuz-2.6.10-5-386*。内核名称后的项目是提供给内核的选项。例如，*root* 选项标识包含 *root* 文件系统（/）的分区。
    -   **initrd /initrd.img-2.6.10-5-386：** 指定包含初始 RAM 磁盘（*initrd*）映像的文件，该映像在磁盘可用之前作为文件系统使用。Linux 内核使用 *RAM 磁盘* —— 作为磁盘使用的内存块 —— 来启动；然后它加载其他驱动程序模块并开始使用硬盘。
-   以 *title* 开始的下一个部分用于从第二个 IDE 硬盘的第三个分区启动 Xandros。Xandros 使用 LILO 启动加载程序，此启动项使用 GRUB 的 *chainloader* 命令将控制权转移给 LILO 启动加载程序。
-   以 *title* *Windows XP* 开始的下一个部分是第三个启动项，指代恰好位于此系统上的 Windows XP 操作系统。标题行旁边的文本会出现在 GRUB 菜单中，用户从中选择要启动的操作系统。

