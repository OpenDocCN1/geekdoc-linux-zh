
## 注意 LILO 配置文件的以下内容

- 最后三行用于从 DOS 分区启动。（Microsoft Windows 安装在该分区中。）
- 以 `image=/boot/vmlinuz-2.2.16-21` 开头的五行定义了 LILO 可以启动的特定内核文件。你可以通过向配置文件添加类似的部分来使 LILO 启动另一个内核。
- `image=/boot/vmlinuz-2.2.16-21` 行标识 LILO 加载的内核。在这种情况下，内核文件是 `vmlinuz-2.2.16-21`，你可以在 `/boot` 目录中找到它。
- `label=linux` 行为内核命名。在这种情况下，你可以在 `boot:` 提示符下输入 `linux` 以使 LILO 启动此特定内核。
- `root=/dev/hda3` 行指定根 Linux 文件系统所在的磁盘分区。这在你的系统上可能不同。
- `initrd=/boot/initrd-2.2.16-21.img` 行指定一个文件，其中包含在磁盘可用之前用作文件系统的初始 RAM 磁盘映像。只有当你的系统具有 SCSI 适配器并且内核使用模块化 SCSI 驱动程序时，你才会看到 `initrd` 行。在这种情况下，内核使用 RAM 磁盘——用作磁盘的内存块——来启动。然后它加载 SCSI 驱动程序模块并开始使用 SCSI 硬盘。如果你创建的内核将 SCSI 适配器支持内置到内核中，则不需要 `initrd` 行。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_306_0.png)

在具有 MS-DOS 分区的系统上，LILO 配置文件可以包含另一个部分，其中包含该分区上操作系统（可能是 Windows 95、98 或 2000）的详细信息。

## 要配置 LILO 以启动另一个内核

要配置 LILO 以启动另一个内核（你刚刚构建的内核），你需要执行以下步骤：

1. 将新内核二进制文件复制到 `/boot` 目录。新的压缩内核文件位于 `/usr/src/linux/arch/i386/boot` 目录。我只是将新内核二进制文件复制到 `/boot` 目录并使用相同的名称：

```
cp /usr/src/linux/arch/i386/boot/zImage /boot
```

如果——在你构建内核时——你输入命令 `make zImage`，内核文件名就是 `zImage`。如果由于内核太大而使用 `make bzImage` 命令构建内核，文件名就是 `bzImage`。你可以使用任何你想要的其他文件名，只要你在步骤 3 的 `/etc/lilo.conf` 文件中引用内核时使用相同的名称即可。

2. 保存 `/boot` 目录中的旧 `System.map` 文件并复制新的映射文件。（我假设你在更改一些配置选项后重新构建内核版本 2.2.16-21）：

```
mv /boot/System.map-2.2.16-21 /boot/System.map-2.2.16-21-old
cp /usr/src/linux/System.map /boot/System.map-2.2.16-21
cd /boot
ln -s System.map-2.2.16-21 System.map
```

3. 使用你喜欢的文本编辑器编辑 `/etc/lilo.conf` 文件，并在文件中的 `timeout` 行之后添加以下行：

```
image=/boot/zImage
label=new
root=/dev/hda3
read-only
```

在你的系统上，你应该确保 `root` 行正确——而不是 `/dev/hda3`，列出 Linux 根目录（`/`）所在的正确磁盘分区。此外，使用内核映像文件的正确文件名（例如，如果内核文件如此命名，则为 `/boot/bzImage`）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_307_0.png)

我不再显示 `initrd` 行，因为我假设你不再使用模块化 SCSI 驱动程序，即使你的系统具有 SCSI 适配器。

4. 保存 `lilo.conf` 文件并退出编辑器。

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
