
make modules_install

现在，你需要按照如下方式将新内核拷贝到 `/boot` 目录：

```
cp /usr/src/linux-2.2.2/arch/i386/boot/vmlinuz-2.2.2
```

同样将新的 `System.map` 文件复制并重命名到 `/boot` 目录如下：

```
cp /usr/src/linux-2.2.1/System.map /boot/System.map-2.2.2
```

现在，按照如下命令删除现有的 `System.map` 符号链接：

```
rm -f /boot/System.map
```

最后，按照如下方式创建一个名为 `/boot/System.map` 的新符号链接：

```
ln -s /boot/System.map-2.2.2 /boot/System.map
```

你还需要按照如下方式创建一个初始内存盘（initial ramdisk）：

```
mkinitrd /boot/initrd-2.2.2.img 2.2.2
```

启动内核之前的最后一步是为新内核准备 LILO。详情请参见前面的章节“配置 LILO”，该章节将介绍如何在 `/etc/lilo.conf` 中为新内核创建一个新的配置段。一旦你修改了 `/etc/lilo.conf` 文件并运行 `/sbin/lilo`，你就可以重启系统并尝试如“使用新内核启动”中所讨论的那样使用新内核。

如果一切顺利，你现在就有了一个运行你所有喜爱的 Linux 应用的全新、自定义配置内核。

![](img/1d90939eac39ca76d12e353542e54751_561_0.png)

> 不要忘记使用 `mkbootdisk --device /dev/fd0 2.2.2` 命令制作一个新的启动软盘。

现在你已经了如何从源码配置、编译、安装和启动新内核。你还应该知道，通常你会遇到只更改了一小部分而非整个内核的情况。这时你需要知道如何补丁内核源码并重新创建一个新内核。

## 补丁内核

需要补丁现有内核以使功能按你的预期运行的情况并不罕见。在这种情况下，你只需对源码进行补丁并重建内核。你可以使用以下命令从 `/usr/src` 目录对内核进行补丁：

```
gzip -cd patchXX.gz | patch -p0
```

如果一个内核有多个补丁，请按顺序应用补丁。换而言之，在应用 `patch02.gz` 之前先应用 `patch01.gz`，以此此类推。

![](img/1d90939eac39ca76d12e353542e54751_562_0.png)

或者，你可以使用脚本 `patch-kernel` 来自动化此过程。将补丁文件存储在 `/usr/src` 目录；从 `/usr/src` 目录运行：

```
./linux/scripts/patch-kernel
```

补丁内核后，按照前面的指令编译并安装新内核。

由于现代 Linux 内核支持通过 `kerneld` 守护进程自动加载和卸载模块，你可能需要配置一个或多个参数以便这些模块正常工作。你可以使用 `kernelcfg` 来完成此工作。

## 创建初始内存盘

如前所述，`mkinitrd` 命令创建初始内存盘。将 `2.xx-x` 替换为你新内核的版本号，运行命令：

```
mk_initrd /boot/initrd-2.xx-x.img 2.2.2
```

这将创建 `/boot/initrd-2.xx-x.img` 初始内存盘文件。使用 `ls` 工具确认该文件已创建在 `/boot` 目录。一旦创建了初始内存盘，你需要修改 `/etc/lilo.conf` 文件为新内核配置 LILO。

## 第六部分：性能优化

## 配置 LILO

一旦你有了新的 Linux 内核，你需要使其能够启动。Linux 加载器（LILO）用于此。LILO 从磁盘读取内核，将其加载到内存并启动。`/etc/lilo.conf` 文件配置 LILO。

在你编译或下载（例如 SuSE Linux 内核包）一个新的 Linux 内核后，在运行 LILO 之前需要修改 `/etc/lilo.conf` 文件。假设你的新内核位于 `/usr/src/linux/arch/i386/boot` 目录并名为 `bimage`。将文件拷贝到 `/boot` 目录并将其命名为 `new_kernel_bz`：

```
cp /usr/src/linux/arch/i386/boot/bzImage /boot/new_kernel_bz
```

接下来，按照所示修改 `/etc/lilo.conf` 文件：

```
boot = /dev/hda

vga = normal

read-only

prompt

timeout = 30

image = /boot/vmlinuz

label = linux

root = /hda3

initrd = /boot/initrd
```

## 使用新内核启动

一旦你有了新的 Linux 内核，你需要使其能够启动。Linux 加载器（LILO）用于此。LILO 从磁盘读取内核，将其加载到内存并启动。`/etc/lilo.conf` 文件配置 LILO。

在你编译或下载（例如 SuSE Linux 内核包）一个新的 Linux 内核后，在运行 LILO 之前需要修改 `/etc/lilo.conf` 文件。假设你的新内核位于 `/usr/src/linux/arch/i386/boot` 目录并名为 `bimage`。将文件拷贝到 `/boot` 目录并将其命名为 `new_kernel_bz`：

```
cp /usr/src/linux/arch/i386/boot/bzImage /boot/new_kernel_bz
```

接下来，按照所示修改 `/etc/lilo.conf` 文件：

```
boot = /dev/hda

vga = normal

read-only

prompt

timeout = 30

image = /boot/vmlinuz

label = linux

root = /hda3

initrd = /boot/initrd
```
