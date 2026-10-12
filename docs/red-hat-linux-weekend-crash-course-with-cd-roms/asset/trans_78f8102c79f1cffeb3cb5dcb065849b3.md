
窗口右下角分组在一起的四个按钮可让你执行特定操作，例如保存配置和退出。要更改配置选项，请单击一个按钮。例如，如果你单击左上角标记为 Processor type and features 的按钮，配置程序会显示另一个窗口，其中包含你可以设置的所有选项。从新窗口中，你可以设置特定选项。该窗口中每个选项旁边都有一个帮助按钮。每当你对某个选项有疑问时，单击相应的上下文相关帮助按钮即可查看该选项的帮助信息。你可以采用这种方法——选择类别按钮、定位选项、如果需要帮助则单击帮助——来指定选项并完成配置步骤。当你完成选项的指定后，在主窗口中单击“保存并退出”按钮（参见图 24-1）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_303_0.png)

## 构建和安装内核及模块

本节描述了重建内核的接下来三个关键阶段：构建内核、构建和安装模块，以及设置 LILO 在重启系统时加载新内核。

### 构建内核

你应该使用单条命令行启动接下来的三个任务（在同一行输入多个用分号分隔的命令），这样你就可以输入该行，按 Enter，然后休息一下，因为构建内核需要一段时间。根据你的系统，制作新内核可能需要几分钟到一个多小时。

在单行输入以下内容以启动构建过程：

```
make dep; make clean; make zImage
```

make dep 命令确定哪些文件已更改以及哪些需要重新编译。make clean 命令删除旧的、无用的文件（如旧的内核副本）。最后，make zImage 在压缩文件中创建新的内核并将其放置在某个目录中。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_304_0.png)

配置内核时，不要通过回答配置选项的“是”来将太多功能链接到内核中。内核文件大小可能太大，无法放入 PC 启动时可用的 640KB 内存中。这个 640KB 限制存在是因为 Intel x86 处理器启动时进入所谓的实模式，只能访问 1MB 内存（其中 640KB 可供程序使用）。这个限制是旧 MS-DOS 时代的遗留问题，仅在 PC 启动时 Linux 内核初始加载时适用。如果内核文件大小太大，make 命令会显示如下错误信息：

```
System is too big. Try using bzImage or modules.
```

如果你收到“System too big”错误，输入 make bzImage 以使用可能适合内存限制的另一种类型的压缩内核。否则，再次进行 make config 步骤并通过对那些配置问题回答“否”来消除不必要的特性。对于你真正需要或可能想尝试的其他特性，输入 m 以创建模块。虽然内核大小在启动时有限制，但启动过程完成后内核可以根据需要加载尽可能多的模块。

在内核构建过程中，你会看到屏幕上出现大量消息。完成后，一个名为 zImage 的压缩文件形式的新内核会出现在 /usr/src/linux/arch/i386/boot 目录中。

要使用新内核，你必须将内核复制到 /boot 目录下并使用特定名称，并编辑 /etc/lilo.conf 文件以设置 LILO（Linux Loader）。你将在本节后面的“安装新内核和其他必需文件”部分学习这些步骤。但是，在继续内核安装之前，你必须先构建和安装模块。

### 构建和安装模块

如果你在内核配置期间选择了任何模块，你必须构建这些模块并安装它们。按以下步骤执行这些任务：

- 1. 输入以下命令以构建模块：
    - cd /usr/src/linux
    - make modules

2. 当前模块集所在的目录以运行系统的 Linux 内核版本命名。例如，如果你的系统运行内核版本 2.2.16-21，模块位于以下目录：

```
/lib/modules/2.2.16-21
```

按如下方式将模块目录移动到新位置：

```
mv /lib/modules/2.2.16-21 /lib/modules/2.2.16-21-old
```

3. 使用以下命令安装新模块：

```
make modules_install
```

现在你可以安装内核并使其可由 LILO 启动。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_305_0.png)

### 安装新内核并设置 LILO

Red Hat Linux 使用 LILO 从磁盘加载新构建的 Linux 内核。你必须配置并安装 LILO 以使用内核。配置文件 /etc/lilo.conf 列出了 LILO 运行的内核二进制文件。你可以通过输入以下命令来检查 LILO 配置文件的内容：

```
cat /etc/lilo.conf
```

当我在装有 SCSI 适配器的系统上尝试此命令时，我看到以下内容：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
image=/boot/vmlinuz-2.2.16-21
    label=linux
    root=/dev/hda3
    initrd=/boot/initrd-2.2.16-21.img
    read-only
other=/dev/hda1
    label=dos
    table=/dev/hda
```

注意 LILO 配置文件的以下内容：

- 最后三行用于从 DOS 分区启动。（Microsoft Windows 安装在该分区中。）
- 以 `image=/boot/vmlinuz-2.2.16-21` 开头的五行定义了 LILO 可以启动的特定内核文件。你可以通过向配置文件添加类似的部分来使 LILO 启动另一个内核。
- `image=/boot/vmlinuz-2.2.16-21` 行标识 LILO 加载的内核。在这种情况下，内核文件是 `vmlinuz-2.2.16-21`，你可以在 `/boot` 目录中找到它。
- `label=linux` 行为内核命名。在这种情况下，你可以在 boot: 提示符下输入 `linux` 以使 LILO 启动此特定内核。
- `root=/dev/hda3` 行指定根 Linux 文件系统所在的磁盘分区。这在你的系统上可能不同。
- `initrd=/boot/initrd-2.2.16-21.img` 行指定一个文件，其中包含在磁盘可用之前用作文件系统的初始 RAM 磁盘映像。只有当你的系统具有 SCSI 适配器并且内核使用模块化 SCSI 驱动程序时，你才会看到 `initrd` 行。在这种情况下，内核使用 RAM 磁盘——用作磁盘的内存块——来启动。然后它加载 SCSI 驱动程序模块并开始使用 SCSI 硬盘。如果你创建的内核将 SCSI 适配器支持内置到内核中，则不需要 `initrd` 行。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_306_0.png)

在具有 MS-DOS 分区的系统上，LILO 配置文件可以包含另一个部分，其中包含该分区上操作系统（可能是 Windows 95、98 或 2000）的详细信息。

要配置 LILO 以启动另一个内核（你刚刚构建的内核），你需要执行以下步骤：

- 1. 将新内核二进制文件复制到 `/boot` 目录。新的压缩内核文件位于 `/usr/src/linux/arch/i386/boot` 目录。我只是将新内核二进制文件复制到 `/boot` 目录并使用相同的名称：
  
  ```
  cp /usr/src/linux/arch/i386/boot/zImage /boot
  ```
  
  如果——在你构建内核时——你输入命令 `make zImage`，内核文件名就是 `zImage`。如果由于内核太大而使用 `make bzImage` 命令构建内核，文件名就是 `bzImage`。你可以使用任何你想要的其他文件名，只要你在步骤 3 的 `/etc/lilo.conf` 文件中引用内核时使用相同的名称即可。

2. 保存 /boot 目录中的旧 System.map 文件并复制新的映射文件。（我假设你在更改一些配置选项后重新构建内核版本 2.2.16-21）：

```
mv /boot/System.map-2.2.16-21 /boot/System.map-2.2.16-21-old
cp /usr/src/linux/System.map /boot/System.map-2.2.16-21
cd /boot
ln -s System.map-2.2.16-21 System.map
```

3. 使用你喜欢的文本编辑器编辑 /etc/lilo.conf 文件，并在文件中的 timeout 行之后添加以下行：

```
image=/boot/zImage
label=new
root=/dev/hda3
read-only
```

在你的系统上，你应该确保 root 行正确——而不是 /dev/hda3，列出 Linux 根目录（/）所在的正确磁盘分区。此外，使用内核映像文件的正确文件名（例如，如果内核文件如此命名，则为 /boot/bzImage）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_307_0.png)

我不再显示 initrd 行，因为我假设你不再使用模块化 SCSI 驱动程序，即使你的系统具有 SCSI 适配器。

4. 保存 lilo.conf 文件并退出编辑器。

5. 使用以下命令再次安装 LILO：

```
/sbin/lilo
```

现在你可以重新启动系统并尝试新内核。

### 重新启动系统

在你完成 LILO 的配置和安装后，你将返回到 Linux 提示符。在你仍以 root 身份登录时，输入以下命令重新启动系统：

```
reboot
```
