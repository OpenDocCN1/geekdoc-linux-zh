
## Ubuntu 服务器管理

```
4:23:respawn:/bin/getty 38400 tty4
5:23:respawn:/bin/getty 38400 tty5
6:23:respawn:/bin/getty 38400 tty6
```

在 Upstart 系统中，每一个 `getty` 都是通过 `/etc/event.d` 目录下的 `tty` 文件启动的，其中 `x` 代表终端。虽然这些文件更具描述性，但它们包含相同的信息。所有六个终端都在运行级别 2 和 3 中启动。当用户从终端注销时，`respawn` 指令会重新带有新登录界面的终端。文本屏幕的通信以每秒 38400 比的速度足够快。

## 救援选项

即使在 Linux 中也会发生问题：关键文件可能被擦除，新的管理员可能会在启动文件中引入语法错误，驱动程序甚至卷可能会损坏，从不良源下载的内容可能会给其他系统带来麻烦。在现实生活中，Linux 管理员需要知道救援系统的选项。这包括单用户模式、来自安装光盘的救援选项，甚至 LiveCD 的使用。

## 恢复模式与单用户模式

从 GRUB 菜单访问恢复模式有两种方法。默认情况下，Ubuntu 在 GRUB 配置文件发布了一个恢复模式选项，即使在未启用 root 管理账户的情况下，它也能提供 Ubuntu 系统的 root 管理权限。

### 恢复模式

在本章前面的部分，我建议你禁用或至少为 GRUB 菜单中的恢复模式选项设置密码。风险在于恢复模式确实提供了对本地系统的 root 管理权限。GRUB 配置文件中相关段的标题将显示如下：

`Ubuntu 8.04, kernel 2.6.14-server (recovery mode)`

如果你选择此选项，Linux 将不隐藏任何启动消息的情况下启动。它随后启动一个恢复菜单（如图 4-4 所示），该菜单提供三个简单的选项：恢复正常启动（Resume Normal Boot）、进入 root shell 提示符（Drop To Root Shell Prompt）或尝试修复 X 服务器（Try To Fix X Server）。选项取决于 `/usr/share/recovery-mode/recovery-menu` 配置文件，与 `/usr/share/recovery-mode/recovery-mode/options` 目录中配置的选项相关。

- 恢复正常启动：启动过程将像标准运行级别 2 中启动常规内核一样进行。

## Ubuntu 服务器管理

如果你了解 GRUB 配置文件，那么你应该已经知道这里是指定顶层根目录 (`/`) 位置的地方。这可能会很复杂，特别是当该目录位于 RAID 设备或逻辑卷时。为了本节的演示，我假设（并且确实拥有）一个 Ubuntu 系统，其中该目录挂载在特定的分区 `/dev/sda2` 上。当操作系统加载并由 Upstart 接管时，它是以只读 (`ro`) 挂载的。

```
grub> kernel/vmlinuz-2.6.24-16 root=/dev/sda2 ro
```

但等一下，之前描述的 GRUB 配置文件为顶层根目录 (`/`) 指定了 UUID，如果你知道该目录挂载在哪里，就不需要 UUID。

最后，初始 RAM 磁盘通常通过 `initrd` 命令加载。同样地，我可以利用命令补全功能。首先，我输入以下内容：

```
grub> initrd /
```

然后我按 TAB 键查看所有文件，其中包含一个 `initrd.img-2.6.24-16-server` 文件：

```
grub> initrd/initrd.img-2.6.24-16-server
```

最后，要从 `grub>` 提示符启动引导过程，我使用 `boot` 命令：

```
grub> boot
```

如果成功，启动过程应该像（即）从普通的 GRUB 配置文件运行的那样进行。然后你可以使用另一个 Ubuntu 服务器系统的示例创建一个相应的 `/boot/grub/menu.lst` 配置文件。

## 安装光盘救援模式

有时，你只需要救援磁盘。缺少 GRUB 配置文件的示例是测试 Ubuntu 安装光盘可用救援模式的良好方法。为了本节的演示，我运行命令来禁用 GRUB 菜单：

```bash
$ sudo mv /boot/grub/menu.lst /home/michael
```
