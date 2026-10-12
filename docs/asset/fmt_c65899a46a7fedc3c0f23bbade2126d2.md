
`Enhanced IDE/MFN/MWR disk/cdrom/tape support` (`CONFIG_BLK_DEV_IDE`) [Y/n?]

`Include IDE/ATAPI CDROM support` (`CONFIG_BLK_DEV_IDECD`) [Y/n?]

## 4. 安装

对于 SCSI CD-ROM 驱动器，请启用这些选项：

- SCSI 支持 (`CONFIG_SCSI`) [Y/n/m]
- SCSI CD-ROM 支持 (`CONFIG_BLK_DEV_SR`) [Y/n/m/]

此外，根据需要启用对你的 SCSI 主机适配器的支持，例如：

- Adaptec AHA152X (`CONFIG_SCSI_AHA152X`) [Y/n/m]

对于专有接口 CD-ROM 驱动器，请启用相应的驱动。你可以使用之前列出的表格来确定适用于你模型的驱动。几乎所有的 CD-ROM 都使用 `ISO-9660` 文件系统，你还必须启用：

- ISO9660 cdrom 文件系统支持 (`CONFIG_ISO9660_FS`) [Y/n/m]

虽然 CD-ROM 不需要，但如果你有一张 Linux 支持的声卡，你可能也想在此时启用并配置内核声卡驱动。`Sound HOWTO` http://sunite.unc.edu/LDP/HOWTO/Sound-HOWTO.html 在此是一个非常有用的参考。你应该按照通常的程序编译并安装内核。在按照下一节描述创建设备文件并设置任何启动参数之前，请勿使用新内核启动。

`ISO-9660` 文件系统和几乎所有的 CD-ROM 驱动程序都可以编译为可加载内核模块。这种方案允许在不重启内核的情况下加载和卸载内核驱动程序，从而释放内存。我建议你先使用编译进驱动程序进行 CD-ROM 安装。如何使用模块已在模块文档和 `Kernel HOWTO` http://sunite.unc.edu/LDP/Kernel-HOWTO.html 中说明。

如果此处列出的驱动器类型不支持你的内核，你可能需要升级到更新版本。你可能需要使用独立于内核源码的驱动程序。这通常涉及内核打补丁。`Kernel HOWTO` http://sunite.unc.edu/LDP/HOWTO/Kernel-HOWTO.html 解释了如何操作。

注意，可以通过 `make menuconfig` 调用的基于菜单的内核配置程序，以及通过 `make xconfig` 调用的基于 X11 的图形界面。所有三种配置方法都提供在线帮助。

## 4.3 创建设备文件和设置启动时间参数

内核使用设备文件来识别使用哪个设备。如果你运行的是标准的 Linux 发行版，你可能在安装期间已经创建了必要的设备文件。例如，在 Slackware Linux 下，有一个基于菜单的设置，包含了 CD-ROM 设置，并且大多数系统都有 `/dev/MAKDEV`。如果你不使用这些方法，可以使用本节列出的更手动的程序。如果你使用这些方法中的任一种，建议至少根据本节的信息对设备文件进行验证。

你通过运行对应驱动器类型的 shell 命令来创建设备文件。这应该以 `root` 身份执行。注意，某些 Linux 发行版使用的 CD-ROM 设备名称与此处列出的略有不同。

建议你还为 CD-ROM 设备创建一个符号链接以便于记忆。例如，对于位于次要接口上的第二个设备 IDE CD-ROM 驱动器，将创建链接：

```bash
# ln -s /dev/hdd /dev/cdrom
```

如果你想播放音频 CD，你需要设置设备文件（真实文件，而不是它的符号链接）的权限以允许所有用户读取，例如：

```bash
# chmod 664 /dev/hdd
# ls -l /dev/hdd
bw-rw-r-- 1 root disk 22 Feb 4 1995 /dev/hdd
```

启动 Linux 时，设备驱动程序会通过探测特定地址来尝试确定合适的设备是否存在。许多驱动程序会在几个地址进行自动探测，由于配置差异、可能的设备冲突和硬件限制，驱动程序有时会帮助识别地址和其他参数。大多数驱动程序支持内核命令行上的选项，以便将此信息传递给设备驱动程序。这可以通过主动完成，或者更常见的是配置到你的根加载器中。例如，使用 `LILO`，你可以在 `/etc/lilo.conf` 文件中添加如下 `append` 命令：

```
append = "spbcd=0x230,SoundBlaster"
```

查看 `LILO` 文档获取信息，包括设备文件和启动参数。

在下一节中，我们将讨论特定设备驱动程序的问题以及不同驱动程序的功能。你可能只需要阅读与你的驱动器类型相关的章节。`README` 文件通常位于 `/usr/src/linux/Documentation/cdrom` 目录。

### 4.3.1 Spbcd 驱动

- 主要作者：Eberhard Moenbergberg (`smoenke@gwdg.de`)
- 多会话支持：是（但并非所有驱动器）
- 多个驱动器支持：是
- 可加载模块支持：是
- 读取音频帧：是（仅限 `CR-562`, `CR-563`, `CD-200`）
- 自动探测：是
- 设备文件：`/dev/spbcd`，主设备 `25`
- 配置文件：`spbcd.h`
- 内核配置选项：Matsushita/Panasonic CDROM 支持
- `README` 文件：`spbcd`

此驱动程序接受如下形式的内核命令行：

```
spbcd=<io-address,<interface-type>
```

其中第一个参数是设备的基地址（例如 `0x230`），且 `<interface-type>` 是其中之一。

可以使用以下命令创建设备文件：

```
# mknod /dev/spbcd 25
```

查看 `spbcd` 文件以获取提示。

### 4.3.2 Sony55

- 主要作者：Ken Pizzini (`ken@halcyon.com`)
- 多会话支持：否
- 多个驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/sony35`，主设备 `24`
- 配置文件：`sony35.h`
- 内核配置选项：Sony CDROM 支持

此驱动程序接受如下形式的命令行：

```
sony35=<io-address>
```

如果驱动器已连接，则第三个可选参数为 "PAS"。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/sony35 24
```

查看 `sony35` 文件以获取更多信息。

### 4.3.3 Cdu1a 驱动

- 主要作者：Corey Minyard (`minyard@rch.com`)
- 多会话支持：是
- 多个驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：是
- 自动探测：否
- 设备文件：`/dev/cdu1a`，主设备 `15`
- 配置文件：`cdu1a.h`
- 内核配置选项：Sony CDU3A 支持
- `README` 文件：`cdu1a`

此驱动程序接受如下形式的命令行：

```
cdu1a_port=<io-address> cdu1a_irq=<interrupt>
```

其中第一个数字是必须的，第二个是可选的。

可以使用以下命令创建设备文件：

```bash
# mknod /dev/cdcd0 15
```

查看 `cdu1a` 文件以获取更多信息。另查看 Jeffrey Oxenmeier (`zureal@infinet.com mailto:zureal@infinet.com`) 制作的网页，它涵盖了许多此类驱动器的常见问题。可以在此处找到：`http://www.infinet.com/~zureal/cdu1a.html`

### 4.3.4 Aztcd 驱动

- 主要作者：Werner Zimmermann (`zimmerma@rz.fht-esslingen.de`)
- 多会话支持：是
- 多个驱动器支持：否
- 可加载模块支持：是
- 读取音频帧：否
- 自动探测：否
- 设备文件：`/dev/azcd0`，主设备 `29`
- 配置文件：`azcd.h`
- 内核配置选项：Aztech/Orchid/Ukano/Wearneas (非 IDE) CDROM 支持
- `README` 文件：`aztcd`

此驱动程序接受如下形式的命令行：

```
aztcd=<io-address>
```

可以使用以下命令创建设备文件：

```bash
# mknod /dev/azcd0 29
```
