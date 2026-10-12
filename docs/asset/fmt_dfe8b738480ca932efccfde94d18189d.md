
`/lib/modules/2.2.16-22/fs/autofs.o`
`/lib/modules/2.2.16-22/fs/binfmt_aout.o`
`/lib/modules/2.2.16-22/fs/binfmt_aout.o`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/net/ipv4/af_inet.c`
`/lib/modules/2.2.16-22/proc/kernel/`

## 准备内核

在实际启动内核之前，你应该：

你可能想获取你正在使用的内核版本。获取它的命令是：

```bash
uname -r
```

## 选择模块

接下来，你需要选择要启用或禁用的模块。执行此操作的步骤是：

+ 以 `root` 用户登录并移动到 `/src/linux` 目录。
+ 打开内核编辑工具。两个常用的工具是：
    + `menuconfig`。`menuconfig` 的界面显示在图 11-1。
    
    ![image/a46d40e45425826819863c401_0.png](image/a46d40e45425826819863c401_0.png)
    
    图 11 `menuconfig` 工具。
    + `xconfig`：这是一个桌面工具。`xconfig` 工具显示在图 11-2。
    
    ![image/a46d40e45425826819863c401_1.png](image/a46d40e45425826819863c401_1.png)
    
    图 11-2 `xconfig` 工具。
+ 一旦你调用编辑工具，请根据需要编辑内核。
+ 退出编辑工具。当你这样做时，文件 `/usr/src/linux/.config` 会被创建。`/usr/src/linux/.config` 文件包含了内核的配置选项。

## 构建内核

接下来，你需要构建内核。构建内核的步骤如下：

+ 选择要启用的模块，然后生成依赖文件。
  生成依赖文件的命令如下
  ```bash
  make dep clean
  ```
+ 创建内核镜像。如果你想让镜像文件使用 `gzip` 压缩，输入以下命令：
  ```bash
  make zimage
  ```
  否则，如果你想让镜像文件使用 `bzip2` 压缩，请执行以下命令：
  ```bash
  make bImage
  ```
+ 安装内核模块。要执行此操作，你需要执行以下命令：
  ```bash
  make modules_install
  ```

在你执行这些步骤之后，你就可以安装内核了。安装内核，请执行以下步骤：

+ 将 `zimage` 和 `bImage` 重命名为 `vmlinux<version>`。将此文件移动到根分区。通常，内核存储在 `/boot` 目录。
+ 将新内核添加到启动管理器中。
+ 创建一个可启动的恢复磁盘。

# 重新编译内核

在向 Linux 系统中添加某些硬件后，你可能需要重新编译内核。在 Linux 系统的安装过程完成后，你也应该重新编译内核。

修改内核的另一个原因是为你的系统定制其某些数据结构。你可能需要执行的修改包括增加内核可以支持的进程数量，以及修改某些缓冲区的大小。要修改内核，你需要内核源代码。你可以从互联网上的各种网站获取源代码。对于从 CD-ROM 安装 Linux 的用户，源代码可以作为发行版的一部分找到。

重新编译内核时需要记住的某些准则如下：

- 你应该检查内核将要安装的目录。某些源码会将内核安装到由内核版本指定的目录，而不是 `linux` 目录。你可以通过执行以下命令来检查内核的安装目录：
  ```bash
  tar -txvf source_filename
  ```
