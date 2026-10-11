
配置好内核设置后，输入以下命令编译内核：

```bash
cd /usr/src/linux
make dep ; make clean
make bzImage
make modules
```

如果您正在重新编译与之前相同的内核（在本例中为 2.0.36-3），您可能想通过以下命令将现有模块移动到备份目录：

```bash
cd /usr/src/linux
mv /lib/modules/2.0.36-3 /lib/modules/2.0.36-3-backup
```

现在，输入命令实际安装新模块：

```bash
cd /usr/src/linux
make modules_install
```

下一步是确保您的符号文件链接与新的内核树保持一致。实际上，这一步只需要一次，因此只有在你之前编译过自定义内核的情况下才需要执行以下操作：

```bash
cd /usr/src
cd /usr/include
rm -rf /usr/src/linux/include/asm-i386 asm
ln -s /usr/src/linux/include/linux linux
ln -s /usr/src/linux/include/scsi scsi
```

> 注意：上述步骤对于 2.2.x 或更高版本的内核已不再需要。

下一步是配置您的内核设置。这是构建自定义内核最重要的一步。如果您禁用了错误的设置，可能会遗漏对您需要的特性或硬件的支持。然而，如果您开启了错误的设置，将无谓地增大内核体积并浪费宝贵的系统内存

![](img/846ec8d157c5d667ec22f4e21c29db61_103_0.png)

（尽管如此，可能宁可选择后者也不要选择前者要好）。

确保您正确编译内核的最佳方法是了解您将需要使用哪些功能，以及系统中有哪些需要支持的硬件。在几次自定义内核经验后，这个过程就会变得“轻车熟路”，看起来不再那么令畏了！

输入以下内容开始配置过程：

```bash
cd /usr/src/linux
make mrproper
make menuconfig
```

（如果您运行着 X Window 系统，可以输入“`make xconfig`”代替“`make menuconfig`”：详情请参阅第 5 章如何使其运行。）

要配置内核，请浏览各种设置并选择（启用）任何您需要的项，并取消选择（禁用）您不需要的项。您可以选择将此类支持直接内置内核，或者将其构建为模块，由内核根据需要加载和卸载。（如果您将启动系统时实际需要的特性（例如 SCSI 驱动程序）编译为模块，您将需要创建一个 RAMDisk 镜像，否则系统将无法启动。这是通过“`mkinitrd`”命令完成的；该过程在后面稍有描述。）

在浏览配置设置时，您可以选择 `<Help>` 来查看特定内核选项的用途。

## 10.7 迁移到 2.2.x 内核

（注：由于原文中存在大量完全重复的段落，译文已根据核心逻辑进行了完整翻译。以下是最后新增章节的翻译：）

## 10.7 迁移到 2.2.x 内核

Linux 内核 2.2.0 于 1999 年 1 月 25 日发布，它带来了许多新功能、性能增强和硬件支持。任何 Linux 系统都可以以与 10.4 节描述相似的方式升级到这些新内核。

本节将描述如何将您的 RedHat 系统升级到新内核。由于 Red Hat Linux 6.0 及更高版本已默认配备新内核和支持包，因此本节仅对那些仍在使用旧版本（如 5.2）的用户有用。一旦我认为大多数用户已迁移到 6.0 及以后，我可能会从未来的文档中删除本节。

> 警告！如果您决定升级旧系统以支持新内核，请注意由于涉及大量的软件包升级，可能会发生严重的错误。一如既常，请准备好最新的备份以防万一。如果您没有使用 RPM 升级文件以及编译内核的经验，也许您想尝试：

```bash
mount root=/dev/h
```

上述命令假设您的“/”（根）分区位于 `/dev/hda`。Linux 应该能够正常启动（尽管由于您使用的是启动磁盘上的内核，某些服务或设备在此期间内可能无法正常工作），然后您可以恢复旧内核并重启。随后您可以尝试用不同的选项重新编译内核并再次尝试。

# 第 10 章 升级 Linux 及其他应用程序

升级到 Red Hat 6.1。

你可以选择升级到 Red Hat 提供的原生内核（stock kernel），或者通过编译自定义内核来升级。我建议先使用原生内核运行，稍后再像你通常常做的那样构建一个自定义内核（详情请参见第 10.5 节）。

为了使用最新的内核，首先有必要升级到最新的实用程序和库。Red Hat 已经确定了支持最新内核的需要升级的包，并将相应的 RPM 文件放置在他们的 FTP 站点：`ftp://ftp.redhat.com/updates/5.2/kernel-2.i386/`（适用于 i386 平台上的 Red Hat 5.2 用户）。

有一个非常好的方法，其中详细列出了迁移到 2.2.x 所需的适当系统工具，地址为：`http://www-stu.calvin.edu/~clug/users/jnho38/goto22.html`；我将尝试总结下面的信息（以“*”开头的项目表示你极可能需要为 Red Hat 5.2 升级该项；未标记此类的项可能没问题，但值得检查）。

- `initscripts-3.78-2.4` 或更高（输入 `rpm -q initscripts` 检查你的版本）

- `modutils-2.1.121` 或更高（输入 `rpm -q modutils` 检查你的版本）

- `mount-2.9-0` 或更高（输入 `rpm -q mount` 检查你的版本）

- `gcc-2.7.2.3` 或更高（使用 `rpm -q gcc`）

- `binutils-2.8.1.0.23` 或更高（使用 `rpm -q binutils`）

- `libc-5.4.46` 或更高（Red Hat 使用较新的 `glibc`。不需要。）

- `glibc-2.0.7-6` 或更高（使用 `rpm -q glibc`）

- `ld.1.9.9` 或更高（使用 `ls -l /lib/ld.so.`）

- `libgcc+-2.7.2.8` 或更高（使用 `rpm -q libgcc++`）

- `procsps-1.2.9` 或更高（使用 `rpm -q procsps`）

- `procinfo-15` 或更高（使用 `rpm -q procinfo`）

- `psmisc-17` 或更高（使用 `rpm -q psmisc`）

- `net-tools-1.50` 或更高（使用 `rpm -q net-tools`）

- `loadlin-1.6` 或更高（仅在你使用 Loadlin 从 DOS 启动 Linux 时需要。不确定如何计算版本号；请下载最新版本以确定。）

- `sh-utils-1.6` 或更高（使用 `rpm -q sh-utils`）

- `autofs-3.1.1` 或更高（使用 `rpm -q autofs`）

- `nfs-server-2.beta37` 或更高（使用 `rpm -q nfs-server`）；仅在你提供 NFS 文件服务器服务时需要。

- `bash-14.7` 或更高（使用 `rpm -q bash`）

- `ncpfs-2.2.0` 或更高（使用 `rpm -q ncpfs`）；仅在你需要挂载 Novell 文件系统时需要。

- `kernel-pccmia-cs-3.6` 或更高（使用 `rpm -q kernel-pccmia-cs`）；仅用于需要 PCMC 卡支持的笔记本电脑。
