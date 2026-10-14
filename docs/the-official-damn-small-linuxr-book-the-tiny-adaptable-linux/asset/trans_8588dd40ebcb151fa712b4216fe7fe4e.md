

## 下载 Damn Small Linux

如果你对 live CD 的概念还不熟悉，可能不知道如何下载 ISO 并制作可启动的 CD-ROM。第一步是找到一个本地的 DSL 下载镜像。你可以随时通过查看 Damn Small Linux 网站的下载部分来检查最新的可用下载站点列表，网址为：

```
http://www.damnsmalllinux.org/download.html
```

以 Ibiblio 站点为例，导航到该站点的当前目录：

```
ftp://ibiblio.org/pub/Linux/distributions/damnsmalllinux/current
```

根据之前的讨论，选择你想要下载的版本。你在大多数情况下想要的 DSL 的 ISOLINUX 版本，命名为 dsl-??.??.iso，其中 ?? 用 DSL 版本号替换。

有许多方法可以创建可启动的 CD，也有许多操作系统可以执行此任务。你需要使用具有刻录映像或写入磁盘选项的 CD 刻录程序。

许多 Linux 系统都有 k3b 实用程序和 cdrecord 命令来刻录 CD。对于 Windows 用户，Nero 和 Roxio 是流行的商业程序。Windows 上还提供免费软件 CD Burner XP Pro（www.cdburnerxp.se）和 Infra Recorder（http://infrarecorder.sourceforge.net）应用程序。

## 进入启动提示符

尝试启动 DSL live CD。如果 SYSLINUX 或 ISOLINUX 版本都无法让你进入启动屏幕，这里有一些你可以尝试的方法：

- 确保你的 CD 刻录没有失败。如果你自己下载并刻录了 CD，最好以非常低的速度刻录。我建议将刻录过程的速度降低到 4。 是的，即使你有新的 52X 刻录机。
- 有些计算机难以从 CD-RW CD 启动。最好使用 CD-R CD。
- 如果你有不同的 live CD（例如 KNOPPIX），尝试从该 live CD 启动，看看你的问题是否特定于 DSL。
- 你的计算机 BIOS 可能未设置为从 CD 启动。启动过程开始后立即进入计算机的 BIOS 设置（按 F2、Del 或其他键，如指示的那样进入 BIOS）。检查启动顺序是否包含从 CD 启动，并确保在启动顺序中 CD 在硬盘之前。

如果你的计算机无法从 CD 启动，你可以尝试创建启动软盘。下载 DSL 标准启动软盘映像，bootfloppy.img。你可能想检查本地下载镜像以减少下载时间。查看 Damn Small Linux 网站下载部分：www.damnsmalllinux.org/download.html。

接下来，定位要下载的文件。例如，

```
ftp://ibiblio.org/pub/Linux/distributions/damnsmalllinux/current/
bootfloppy.img
```

将此映像写入已知良好的软盘。不要使用旧软盘，因为它们在出现读取错误时很可能会导致问题。使用典型工具创建启动软盘。通常这意味着 Windows 下使用 rawwrite 或 Unix/Linux 类型系统使用 dd。

例如，如果你的 Unix/Linux 系统的第一个软盘设备位于 /dev/fd0，且 bootfloppy.img 位于你的当前目录，你可以使用以下 dd 命令将该映像写入插入的软盘：

```
# dd if=bootfloppy.img of=/dev/fd0 bs=16k
```

根据你使用的 rawwrite 版本，从 DOS 提示符下将 bootfloppy.img 文件写入软盘的过程（启动映像位于 C: 根目录，rawwrite 在 C:\windows\command 目录中）应类似于以下内容：

```
C:\> cd \windows\command
C:\windows\command> rawwrite
Enter disk image source file name: C:\bootfloppy.img
Enter target diskette drive: A:
Please insert a formatted diskette into drive
A: and press -Enter- : <Enter>
```

Windows 版的 rawwrite 程序可以在以下网站找到：

```
http://www.chrysocome.net/rawwrite
```

创建软盘后，请确保更改计算机的 BIOS，使软盘成为第一个启动设备。将新创建的软盘放入驱动器并打开或重新启动系统。如果你使用的是良好的软盘且没有读取错误，你将被呈现 DSL 启动屏幕。

希望你已到达 DSL 启动屏幕（参见图 2-2）。如果你因为需要启动软盘或需要下载并创建 SYSLINUX 版本而到达此处，只需在 DSL 启动提示符下按 Enter 即可。

在你可以看到 DSL 启动屏幕后，你可以在启动提示符下输入许多选项来引导启动过程的方向。以下各节描述了 DSL 启动过程以及如何修改它。

