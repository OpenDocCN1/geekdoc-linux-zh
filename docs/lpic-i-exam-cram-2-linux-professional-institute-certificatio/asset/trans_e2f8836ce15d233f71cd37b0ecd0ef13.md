

## 查看您的模块

要查看当前系统上加载了哪些模块，请使用 `lsmod` 命令：

```bash
lsmod
```

这将返回一个包含四列的输出，例如：

| 模块 | 大小 | 被使用次数 | 标记: PF |
|---|---|---|---|
| pnet32 | 15968 | 1 | (autoclean) |
| ide-cd | 38272 | 0 | (autoclean) |
| cdrom | 32192 | 0 | (autoclean) [ide-cd] |
| vmhgf3 | 37184 | 4 |  |
| usb-uHCI | 24484 | 0 | (unused) |
| usbsore | 73152 | 1 | [usb-uHCI] |
| ext3 | 67136 | 2 |  |
| sd_mod | 12864 | 6 |  |
| scsi_mod | 108576 | 2 | [BusLogic sd_mod] |

输出显示了一个包含四列的列表：

- **第 1 列**—模块名称
- **第 2 列**—模块在内存中的大小
- **第 3 列**—使用计数，即当前有多少其他模块依赖于它
- **第 4 列**—引用当前行模块的模块列表

请注意，`cdrom` 模块被 `ide-cd` 模块引用，而 `usbsore` 模块被 `usb-uHCI` 模块引用。

## 加载和卸载模块

如果您想要加载的模块是单个模块，使用 `insmod` 命令加载它相对简单。您可以使用以下命令从 `/lib/modules/`uname -r`/kernel/drivers` 子目录加载模块：

```bash
insmod modulename
```

如果您需要加载多个模块，或者一组具有相互依赖关系的模块，您可以使用 `modprobe` 命令：

```bash
modprobe modulename
```

您卸载模块的能力受模块是否被其他模块引用的影响，因为模块必须按顺序卸载，这就像从一堆箱子的顶部移除箱子，而不是从中间移除。

![](img/49f4f38f3aec011238fa50f89e643db3_388_0.png)

> **modinfo** 命令用于确定模块的作者、许可证及其他信息。语法为：
> **modinfo** *modulename*
> 这将返回列出模块的许可证、依赖项和别名的输出。

### 使用 modprobe 管理模块

`modprobe` 命令用于单独、成组或匹配特定模式地加载和卸载模块。在指代要加载或卸载的一组模块时，使用短语 *module stack*（模块堆栈）。使用 `modprobe` 加载模块时，请使用此处显示的命令：

```bash
modprobe modulename
```

要加载模块堆栈（包含所有依赖项的顶层模块），`modules.dep` 文件必须列出适当的依赖关系，您只需列出顶层模块：

```bash
modprobe -a modulename
```

要查看 `modprobe` 正在执行的所有操作，请使用 `-v` 选项，并观察它如何向 `insmod` 命令发送所需的命令和选项，以加载相互引用的一组模块：

```bash
modprobe -v ide-cd
```

这将产生类似以下的输出：

```bash
/sbin/insmod /lib/modules/2.4.18-3/kernel/drivers/cdrom/cdrom.o
Using /lib/modules/2.4.18-3/kernel/drivers/cdrom/cdrom.o
Symbol version prefix ''
/sbin/insmod /lib/modules/2.4.18-3/kernel/drivers/ide/ide-cd.o
Using /lib/modules/2.4.18-3/kernel/drivers/ide/ide-cd.o
```

使用 `modprobe` 移除模块与使用 `insmod` 命令略有不同。`modprobe` 读取 `modules.dep` 文件，然后通过在正确顺序下向 `insmod` 命令发送适当命令来卸载模块或模块堆栈。

此外，请记住，`kmod` 进程广泛使用 `modprobe` 来加载模块组，但当前版本的内核中 `kmod` 不会卸载模块。已经做出决定，将用于在指定时间后从较早版本的内核中卸载模块的 `kernel` 进程淘汰。

如果您使用 `lsmod` 命令查看模块，有些会在最右侧列中标记为 *autoclean*（自动清理）。如果某个模块被标记为 *autoclean*，这意味着在约 60 秒的不活动后，如果它未被其他模块引用，就可以使用 `modprobe -r` 命令将其从内核中清除。

> **注意**
> 
> Red Hat 发行版附带了一个 *cron* 作业，该作业每 10 分钟运行一次，以移除标记为 *autoclean* 的模块，或者在未使用时可移除的模块。

> **警报**
> 
> 如果您需要在加载可加载模块时指定选项，可以使用 `/boot/module-info` 文件来设置这些选项。
> 
> 您系统中的许多驱动程序需要别名以兼容其他名称，例如将以太网设备从模块名称别名为 **ethX**（其中 *X* 是接口的编号）。

## 修补内核

在系统设置好并运行后，可能需要对您的系统，特别是内核应用许多补丁和修复。

尽管在高速连接广泛可用的当今时代，这不再那么重要，但下载内核补丁并应用它通常比下载最新补丁版本的完整内核源代码花更少的时间。

许多人使用 Red Hat、SuSE 和 Debian 提供的更新例程来使用最新补丁更新其内核。个人而言，我从未遇到过 Red Hat Network、Debian 的 apt-get 或 SuSE 的 Yast Online Update 搞坏内核补丁的情况，但在这种非常重要的问题上，您的体验可能会有所不同。

总体而言，修补内核使您可以下载更少的源代码，并使用您现有的内核 `.config` 文件，而不是费尽力气一次又一次地重新设置所有自定义设置。

在修补时，请记住内核补丁是非累积的，因此如果您当前运行的是 2.4.18 内核，而最新的补丁级别是 2.4.22，您需要按顺序下载并应用 .19、.20、.21 和 .22 的补丁才能保持最新。然后，在将这些补丁下载并应用到内核源代码之后，您可以重新编译。

`diff` 命令是一个有趣的工具，它使您可以获取更新的源代码树，基本上将新的代码树与旧的代码树进行比较，并获得一个作为您将要应用的补丁的快照文件。

## 使用 patch 命令

作为一种理解 patch 命令的简单方法，您可以使用以下一系列步骤来查看 patch 命令对单个文件能做什么。

在此示例中，我们将获取一个通常可用的名为 `watchdog.txt` 的文件并对它进行一些更改，将其保存为 `changedog.txt`。然后，我们将使用 `diff` 命令搜索新文件中不存在于旧文件中的项目；然后将这些写入一个名为 `diffdog.txt` 的新文件。

当 `diff` 或 `patch` 文件存在时，它可以轻松地应用到原始文件，使其与新文件匹配。

![](img/49f4f38f3aec011238fa50f89e643db3_390_0.png)

> 您必须已使用内核源包安装系统，例如在 Red Hat 7.3 系统中，该包名为 `kernel-source-2.4.18-3.src.rpm`。

执行以下操作：

1. 使用以下命令将 `/usr/src/linux-2.4/Documentation/watchdog.txt` 文件复制到您的用户主目录：
   ```bash
   cp /usr/src/linux-2.4/Documentation/watchdog.txt -
   ```

2. 切换到您的用户主目录，并将 `watchdog.txt` 文件复制到一个名为 `changedog.txt` 的新文件：
   ```bash
   cd -
   cp watchdog.txt changedog.txt
   ```

3. 使用 `vi` 编辑 `changedog.txt` 文件，并在文件显示在屏幕上时，输入以下字符串：
   ```bash
   :%s/interface/connector/g
   ```

4. 这将第一个术语更改为第二个术语，现在您可以使用以下操作保存并退出文件：
   ```bash
   Shift-zz
   ```

5. 文件保存后，使用 `diff` 命令比较这两个文件：
   ```bash
   diff changedog.txt watchdog.txt
   ```

这将显示以下输出：

```
18c18
< All six connectors provide /dev/watchdog,
---
> which when open must be written
> All six interfaces provide /dev/watchdog,
> which when open must be written
25c25
< A second temperature monitoring connector
>is available on the WDT501P cards
---
> A second temperature monitoring interface
36c36
>is available on the WDT501P cards
---
> The third interface logs kernel messages on additional alert events.
64c64
> The third interface logs kernel messages on additional alert events.
---
< The external event connectors on the WDT boards
>are not currently supported.
---
> The external event interfaces on the WDT boards
>are not currently supported.
```

6. 现在使用此处显示的命令创建一个捕获更改到名为 `diffdog.txt` 的第三个文件的补丁文件：
   ```bash
   diff -Naur watchdog.txt changedog.txt > diffdog.txt
   ```

7. 查看 diffdog.txt 文件，看到它仅包含 watchdog.txt 和 changedog.txt 之间的更改。

8. 使用以下命令将补丁应用到原始文件 watchdog.txt：
   ```bash
   cat diffdog.txt | patch
   ```

9. 通过比较 changedog.txt 和 watchdog.txt 文件验证补丁是否准确应用：
   ```bash
   diff changedog.txt watchdog.txt
   ```

10. 没有差异，您刚刚成功使用了补丁！

当您在修补代码树时，重要的是要记住，补丁的应用必须针对相同类型的对象。换句话说，将目录树的补丁应用到另一个目录树会获得更好的结果。

patch 命令提供了一些选项，以使补丁正确应用于绝对路径或相对路径。

如果您使用的是使用源代码树 /usr/src/linux 的全路径生成的补丁，它应该以全路径作为目标进行应用：
```bash
cat patchfile.txt | patch /usr/src/linux
```

如果您的系统上有不同的源代码树结构，您需要去除开头的斜杠和部分路径。例如，您可能会

