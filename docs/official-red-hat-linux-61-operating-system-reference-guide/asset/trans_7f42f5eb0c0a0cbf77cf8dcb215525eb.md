
# 请注意

关于这些实用工具，还有一些值得关注的要点：

- 无论是否启用用户私有组（shadowing），这些实用工具都能正常工作。
- 这些实用工具已稍作修改以支持 Red Hat 的用户私有组方案。有关修改的详细描述，请参阅 `useradd` 手册页。有关用户私有组的更多信息，请参见第 2.3.3 节，*用户私有组*。
- `adduser` 脚本已被替换为指向 `/usr/sbin/useradd` 的符号链接。

## 2.8 构建自定义内核

许多 Linux 新手经常问：“我为什么要自己构建内核？” 鉴于在 kernel modules（内核模块）使用方面所取得的进展，对该问题最准确的回答是：“除非你知道自己为什么需要构建自定义内核，否则你很可能不需要这么做。” 因此，除非你有特定的理由来构建一个自定义内核（或者你只是单纯的好奇），否则你可以跳至第 2.9 节，*Sendmail*。

在过去，当你在系统中添加新硬件时，需要重新编译内核。换句话说，内核是**静态的**。Linux 2.0.x 内核的改进使得大部分硬件驱动程序能够被**模块化**为只能按需插入的组件。然而，在系统中拥有为不同改进特性（一个典型的例子是 SMP 与 UP 内核）编译的多个内核时，存在*重大问题*。随着 Linux 2.2.x 内核在模块化方面的进一步进步，多个内核可以更轻松地共存（尽管它们*不能*共享模块）。

有关处理内核模块的信息，请参见第 3.2.2 节，加载内核模块。除了为系统重新编译自定义内核之外，大多数更改都是隐藏的。

### 2.8.1 构建模块化内核

这些说明使你能通过内核模块化来利用其强大的功能和灵活性。如果你不想利用模块化，请参阅第 2.8.3 节，构建单体内核，以了解构建和安装单体内核的不同方面。假设你已经安装了 `kernel-headers` 和 `kernel-source` 包，并且你从 `/usr/src/linux` 目录执行所有命令。

最重要的步骤是确保你有一个可用的紧急启动磁盘，以防你在下面操作中出错。如果你在安装期间没有制作启动磁盘，请使用 `mkbootdisk` 命令制作一个。标准命令类似于 `mkbootdisk --device /dev/fd0 2.2.x`。完成后，测试启动磁盘以确保它能启动系统。

以已知状态开始内核构建源树很重要。因此，建议从命令 `make mrproper` 开始。这将删除任何配置文件以及可能散落在源树中的任何先前构建的残留物。现在你必须创建一个配置文件，该文件将确定在新内核中包含哪些组件。可用的内核配置方法如下：

- `make config` -- 交互式文本程序。组件会依次呈现，你使用 **Y**（是）、**N**（否）或 **M**（模块）进行回答。
- `make menuconfig` -- 图形化、菜单驱动的程序。组件在分类菜单中呈现，你使用与 Red Hat Linux 安装程序相同的方式选择所需组件。切换对应于你要包含的项目的标签：**Y**（是）、**N**（否）或 **M**（模块）。
- `make xconfig` -- X Window 系统程序。组件在不同层级的菜单中列出，并使用鼠标进行选择。同样，选择 **Y**（是）、**N**（否）或 **M**（模块）。
- `make oldconfig` -- 这是一个非交互式脚本，它将把你的 Makefile 设置为默认设置。如果你使用的是 Red Hat 补丁内核，它将配置设置为随你的机器发行的内核配置。这在将内核设置为已知可用的默认值并关闭你不想使用的功能时很有用。

> **请注意**
> 为了使用 kmod（有关详细信息，请参见第 3.2.2 节，加载内核模块）和内核模块，你必须在配置中回答 **Yes** 到 *kmod support* 和 *module version* (*CONFIG_MODVERSIONS*) 支持。

如果你希望使用你已经通过上述方法之一创建的配置文件（`/usr/src/linux/.config` -- 该文件是在执行上述任一方法后创建的）来构建内核，你可以省略 `make mrproper` 和 `make config` 命令，并使用命令 `make dep` 后跟 `make clean` 来为构建准备源树。

构建模块化内核的下一步是简单地编辑 `/usr/src/linux/Makefile` 并将源代码组件编译成你的机器可用于启动的工作程序。这里描述的方法是在发生意外时最容易恢复的方法。如果你对其他可能性感兴趣，可以在 Kernel-HOWTO 或你的 Linux 系统 `/usr/src/linux` 中的 Makefile 中找到详细信息。

- 编辑 Makefile 并更改行：`EXTRAVERSION =` 以匹配一个“唯一”的名称（例如，在字符串末尾添加你的首字母，如 `EXTRAVERSION = -2.5.0sj`）。这将允许你在同一系统中同时保留旧的可用内核和新内核。
- 使用 `make bzImage` 构建内核。
- 使用 `make modules` 构建你配置的任何模块。

安装新模块（即使你没有构建任何模块），使用 `make modules_install`。这将使用在 `Makefile` 中指定的路径名称将内核模块安装到文件路径 `/lib/modules/` 中。我们的例子将是 `/lib/modules/2.2.15-2.5.0sjs/`。

如果你有一个 SCSI 适配器并且将你的 SCSI 驱动制作成了模块，请构建一个新的 `initrd` 映像（参见第 2.8.2 节，*制作 initrd 映像*；注意，在自定义内核中将 SCSI 驱动模块化的实际原因很少）。除非你有特定理由创建 `initrd` 映像，否则不要创建它，也不要将其添加到 `lilo.conf` 中。

为了提供冗余的启动源以保护免受新内核中可能出现的错误影响，你应该保留原始内核可用。将内核添加到 LILO 菜单与重命名 `/boot` 中的原始内核、将新内核复制到 `/boot`、在 `/etc/lilo.conf` 中添加几行并运行 `/sbin/lilo` 一样简单。以下是 Red Hat Linux 随附的默认 `/etc/lilo.conf` 文件的示例：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
default=linux

linear

image=/boot/vmlinuz-2.2.15-2.5.0
label=linux
initrd=/boot/initrd-2.2.15-2.5.0.img
read-only
root=/dev/hda8

other=/dev/hda1
  label=dos
```

现在你必须更新 `/etc/lilo.conf`。如果你构建了一个新的 `initrd` 映像，你必须告诉 LILO 使用它。在这个 `/etc/lilo.conf` 的示例中，我们在文件中间添加了四行以指示另一个可启动的内核。我们将 `/boot/vmlinuz` 重命名为 `/boot/vmlinuz.old` 并将其标签更改为 `old`。我们还为新内核添加了一行 `initrd`：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
default=linux

linear

image=/boot/vmlinuz-2.2.15-2.5.0
label=linux
initrd=/boot/initrd-2.2.15-2.5.0.img
read-only
root=/dev/hda8

image=/boot/vmlinuz-2.2.15-2.5.0sjs
label=test
initrd=/boot/initrd-2.2.15-2.5.0sjs.img
read-only
root=/dev/hda8

other=/dev/hda1
label=dos
```

现在当系统启动且你在 LILO 的 `boot:` 提示符处按 [Tab] 键时，将显示可用选项；

```
LILO boot:
linux test dos
```

要启动旧内核（**linux**），只需按 [Enter] 键，或等待 LILO 超时。如果你想启动新内核（**test**），输入 **test** 并按 [Enter] 键。

以下是步骤摘要：

- 使用你之前对 Makefile 进行更改后生成的名称，将编译结果内核复制到你的 `/boot` 目录中。这是一个示例：

```
cp -P
/usr/src/linux/arch/i386/boot/bzImage
```
