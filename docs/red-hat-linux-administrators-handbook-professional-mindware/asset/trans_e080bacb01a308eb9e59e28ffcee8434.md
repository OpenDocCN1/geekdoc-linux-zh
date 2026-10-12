

## 网络文件系统

在此，您可以为高级网络文件系统配置内核。

**Coda 文件系统支持（高级网络 fs）（CONFIG_CODA_FS）[N/y/m/?]**

Coda 文件系统尚未广泛使用，我不建议将其添加到内核中；您可以选择将其作为模块添加。

**NFS 文件系统支持（CONFIG_NFS_FS）[Y/m/n/?]**

如果您打算使用 NFS，请选择默认答案。

**模拟 SUN NFS 服务器（CONFIG_NFSD_SUN）[N/y/?]**

除非您希望您的 Linux NFS 服务器表现得像基于 Sun 的 NFS 服务器那样，允许 NFS 客户端访问本地文件系统上的挂载点目录，否则请保持默认设置。

**SMB 文件系统支持（用于挂载 WfW 共享等）（CONFIG_SMB_FS）[N/y/m/?]**

如果您想在 Linux 系统上将 Windows 95/98/NT/2000 文件系统作为 SMB 文件系统挂载，则需要选择 yes 或将此功能设置为模块。

**NCP 文件系统支持（用于挂载 NetWare 卷）（CONFIG_NCP_FS）[N/y/m/?]**

除非您计划在 Linux 系统上挂载 NetWare 卷，否则请保持默认答案。

## 分区类型

如果您希望支持基于 BSD、Macintosh、Solaris 等的磁盘分区，请根据以下问题相应作答：

- *BSD 磁盘标签（BSD 分区表）支持（CONFIG_BSD_DISKLABEL）[N/y/?]*
- *Macintosh 分区映射支持（CONFIG_MAC_PARTITION）[N/y/?]*
- *SMD 磁盘标签（Sun 分区表）支持（CONFIG_SMD_DISKLABEL）[N/y/?]*
- *Solaris (x86) 分区表支持（CONFIG_SOLARIS_X86_PARTITION）[N/y/?]*

在大多数情况下，默认答案已足够。

## 控制台驱动程序

在本节中，您可以设置以下内容：

- `VGA 文本控制台 (CONFIG_VGA_CONSOLE) [Y/n/?]`
  - 如果您想要 VGA 文本控制台，请保持默认。

- `视频模式选择支持 (CONFIG_VIDEO_SELECT) [N/y/?]`
  - 如果您希望能够在内核启动时指定文本模式，请选择此选项，或保持默认。

## 声音

假设您在服务器系统中可能不需要声卡，您可以对以下问题保持默认答案：

`声卡支持 (CONFIG_SOUND) [N/y/m/?]`

## 内核调试

本节中唯一可用的选项是对 Magic SysRq 键的支持。如果您通过回答 yes 来启用对此键的支持，即使系统已崩溃，您也可以按 SysRq+Alt+PrintScreen 来转储状态信息。

- `Magic SysRq 键 (CONFIG_MAGIC_SYSRQ) [N/y/?]`
  - 这仅对内核开发人员有用。此处选择 no。

一旦您回答了所有这些问题，配置脚本将在 `/usr/src/linux` 目录中创建一个 `.config` 文件。您可能想要查看该文件的内容，以确保所有功能都已按您的指定进行配置。

> **注意**
> 
> 如果您不想了解还可以如何配置内核，而是准备编译内核，请跳过接下来的两节，直接进入“编译、安装和引导新内核”。

使用 `make config` 配置内核是一个相当漫长的过程。它也有点繁琐；然而，如果您碰巧通过远程服务器上的 Telnet 连接配置内核，这非常合适。

基于命令行的界面可能不够优雅，但它适用于大多数场景，当以下两种方法不可用时，您应将其视为默认配置方法。

## 使用 make menuconfig 配置内核

基于 `make config` 的配置脚本的主要问题之一是，如果您犯了错误，除非重新开始，否则无法返回修复。此外，除非您手动使用文本编辑器查看 `/usr/src/linux/.config` 文件，否则无法回顾您的选择。

为了解决这些缺点，可以使用以下命令：

```
make menuconfig
```

这将运行一个菜单驱动的配置工具，比 `make config` 脚本更加用户友好。

用户界面非常简单且易于导航。但是，配置问题完全相同。此配置程序还允许您保存和加载配置文件。换句话说，您可以创建具有不同设置的多个配置文件，并使用这些配置文件来尝试新内核的各种功能。

虽然 `make menuconfig` 脚本非常友好，但它确实对远程内核配置提出了一些额外要求。例如，如果您计划通过到远程服务器的 Telnet 连接来配置和编译内核，您必须确保您这边的 Telnet 客户端程序能够进行良好的终端仿真，这是全屏菜单应用程序所必需的。此外，`make menuconfig` 并不是配置内核最花哨的方式。这个头衔属于 `make xconfig` 脚本。

## 使用 make xconfig 配置内核

正如您可能从脚本名称猜到的那样，这种内核配置方法需要 X Window System。因为我不建议在服务器系统上安装 X Window System，所以我也无法推荐此方法。然而，我必须说，在安装了 X Window 的系统上，这是首选的内核配置方法。从 `/usr/src/linux` 运行 `make xconfig` 脚本（`wish -f scripts/kconfig.tk`）以启动 xconfig。

您可以单击任意按钮来配置整个配置的特定部分。这是一个非常用户友好的界面。该界面的另一个优点是您可以通过单击相应的按钮打开多个部分。例如，如果您正在配置“分区类型”部分，并想确认您已在“文件系统”部分启用了 UFS 文件系统支持，只需单击这两个部分的按钮并验证您的选择即可。

您应该能够确定哪种方法最适合您的环境。

## 编译、安装和引导新内核

要编译、安装并引导新内核，请执行以下操作：

1. 运行：
   ```
   make dep
   ```
   以确保源代码中的所有依赖关系均已正确设置。除非内核源代码本身存在问题，否则这应该会无错误返回。

2. 要编译并创建压缩的 Linux 内核，请运行以下命令：
   ```
   make bzImage
   ```

3. 如果您在配置期间将内核的任何部分配置为模块，请运行以下命令来编译模块：
   ```
   make modules
   ```

4. 编译模块后，使用以下命令将它们安装在 `/lib/modules/2.2.2` 目录中：
   ```
   make modules_install
   ```

5. 将新内核复制到 `/boot` 目录，如下所示：
   ```
   cp /usr/src/linux-2.2.2/arch/i386/boot/bzImage /boot/vmlinuz-2.2.2
   ```

6. 复制并重命名新的 **System.map** 文件到 `/boot` 目录，如下所示：
   ```
   cp /usr/src/linux-2.2.2/System.map /boot/System.map-2.2.2
   ```

7. 使用 `rm -f /boot/System.map` 命令删除该文件。

8. 创建一个名为 `/boot/System.map` 的新符号链接，如下所示：
   ```
   ln -s /boot/System.map-2.2.2 /boot/System.map
   ```

9. 接下来，创建一个新的初始 ramdisk，如下所示：
   ```
   mkinitrd /boot/initrd-2.2.2.img 2.2.2
   ```

10. 在引导新内核之前的最后一步是为新内核准备 **LILO**。有关如何在 `/etc/lilo.conf` 中为新内核创建新配置段的详细信息，请参阅前面的“配置 LILO”部分。修改 `/etc/lilo.conf` 文件并运行 `/sbin/lilo` 后，您可以重新引导系统并开始使用新内核。

如果一切顺利，您将拥有一个全新的、自定义配置的内核，运行您所有喜爱的 Linux 应用程序。

**提示**
别忘了使用 `mkbootdisk --device /dev/fd0 2.2.2` 命令制作一张新的启动软盘。

## 修补内核

需要修补现有内核以使某些功能按您想要的方式工作的情况并不罕见。在这种情况下，您可以简单地修补源代码并重新构建内核。您可以从 `/usr/src` 目录使用以下命令修补内核源代码：

```bash
gzip -cd patchXX.gz | patch -p0
```

