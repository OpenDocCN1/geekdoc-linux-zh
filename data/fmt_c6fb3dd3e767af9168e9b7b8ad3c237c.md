
要真正使用 PEX，你需要在安装时加载 PEX 库、头文件和字体。位于 `/usr/lib/X11/fonts/PEX` 的 PEX 字体是运行大多数 PEX 程序所必需。

在下一节中，我们将展示如何使用链接套件（link kit）为支持三维图形的 X 扩展重新构建 X 服务。添加其他 X 扩展（例如巨大的图像扩展 XIE）的步骤基本上与这些步骤是相同的。我们选择 PEX 是因为我们看到了许多关于这个特定 X 扩展的问题。三维图形正变得越来越流行。不过，基础技术适用于你需要添加的任何 X 扩展。

> 再次，Linux 在这里可以提供一个方便的捷径。不需要重新构建 X 服务，可以从模块加载 PEX 支持。XF86Config 的主页提供了更多关于如何设置此内容的信息。
> 注意

## 配置服务器构建

在构建新的 X 服务之前，你必须编辑位于 `/usr/X11R/lib/Server/config/cf` 目录下的配置文件 `xf86site.def`。在该目录中，编辑 `xf86site.def` 文件（务必先进行备份）。在此文件中，你需要指定一些内容，包括（例如 PEX）以及要构建哪个 X 服务，例如 SuperVGA、XF86_SVGA 或 S3 XF86_S3。

在表 B.2 中，我们列出了我们成功使用的设置。注意，我们禁用了大多数 X 服务的创建，因为我们只需要 S3 和 SVGA X 服务。正因如此，你可能希望更改你的设置。

> 对于任何版本的 X，这些设置可能会发生变化，并且可能有很多种。请将表 B.2 作为指南，而不要将其视为真理。此时，由于你反正要重新构建 X 服务，你可能也想构建其他 X 扩展之一，例如 LBX 或 XIE。
> 注意

如果服务器是自动开启，你可以关闭不需要的部分。对于每个 X 服务器，特别是 SuperVGA 服务器，有一份你可以设置的驱动程序列表。我们总是选择默认值，并保持设置（`XF86SvgaDrivers`、`XF86Vga16Drivers`、`XF86Vga2Drivers` 和 `XF86MonoDrivers`）不变。

如果你构建了多个 X 服务器，你需要取消注释 `ServerInstall` 行，并放入通过 X 的符号链接安装的 X 服务器。否则，XF86_SVGA 将被设置为默认服务器 `X`。

注释掉 `XF86Contrib` 行以构建所有贡献软件。

### 表 B.2 xf86site.def 文件中的设置

| 设置项 | 数值 | 含义 |
| :--- | :--- | :--- |
| HasGcc | YES | Linux 使用 gcc C 编译器 |
| HasGcc2 | YES | Linux 使用 gcc 2.x 版本 |
| XF86SVGAServer | YES | 构建 256 色 SVGA X 服务器 |
| XF86VGA16Server | NO | 构建 16 色 VGA X 服务器 |
| XF86MonoServer | NO | 构建单色 VGA X 服务器 |
| XF86S3Server | YES | 构建 S3 X 服务器 |
| XF86Mach8Server | YES | 构建 Mach8 X 服务器 |
| XF86Mach32Server | NO | 构建 Mach32 X 服务器 |
| XF86Mach64Server | NO | 构建 Mach64 X 服务器 |
| XF86P9000Server | NO | 构建 P9000 X 服务器 |
| XF86AGXServer | NO | 构建 AGX X 服务器 |
| XF86W32Server | NO | 构建 ET4000/W32 X 服务器 |
| XF86B514Server | NO | 构建 IBM B514/A X 服务器 |
| XnestServer | NO | 构建 Xnest 服务器 |
| BuildPexExt | YES | 构建 PEX 扩展 |
| BuildXIE | NO | 构建 XIE 扩展 |
| BuildLBX | NO | 构建低带宽 X 扩展 |
| BuildScreenSaverExt | YES | 构建屏幕保护程序扩展 |

一旦设置好 `xf86site.def` 文件，你就可以开始构建新的 X 服务器了。

## 构建新的 X 服务器

作为 root 用户，你应该执行以下步骤来构建你的新 X 服务器：

1. 备份你当前的 X 服务器。
2. 构建所有的 Makefile。
3. 生成新的 X 服务器。
4. 退出 X。
5. 安装新的 X 服务器。
6. 确保 `/usr/X11R6/bin/X` 指向正确的 X 服务器。
7. 启动 X 以验证新的 X 服务器运行正常。
8. 运行 `xdpinfo` 查看新的 X 扩展是否可用。
9. 使用 `make clean` 清理 `/usr/X11R6/lib/Server` 目录。

在开始之前，始终备份你当前的 X 服务器。这样做在新构建失败时允许你继续。然后切换回 `/usr/X11R6/lib/Server` 目录，通过以下命令构建 Makefile：

```
mkmf
```

构建 X 服务器需要一些时间。完成 mkmf 后，请运行：

```
make
```

构建完成后，你可能需要安装新的 X 扩展。在 `/usr/X11R6/lib/Server` 目录中运行以下命令：

```
make install
```

安装完成后，运行以下命令以检查新的 X 扩展是否可用：

```
xdpinfo
```
