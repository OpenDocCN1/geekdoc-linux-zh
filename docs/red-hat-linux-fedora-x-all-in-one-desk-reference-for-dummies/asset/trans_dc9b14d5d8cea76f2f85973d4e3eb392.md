

## 从源文件构建软件包 471

## 从源文件构建软件

解压压缩归包后，所有源文件都在一个通常带有软件包版本后缀的目录中。例如，XMMS 1.2.10 版本的源文件提取到 `xmms-1.2.10` 目录。要开始构建软件，使用以下命令切换目录：

```bash
cd xmms*
```

你不需要输入完整的名称——shell 可以扩展名称并进入 `xmms-1.2.10` 目录。

几乎所有的软件包都带有一个 `README` 或 `INSTALL` 文件——该文件会告诉你如何构建和安装软件包。XMMS 例外；它带有一个 `README` 文件，你可以阅读它。`INSTALL` 文件包含了构建和安装 XMMS 的指令。

大多数开源软件包（包括 XMMS）还带有一个名为 `COPYING` 的文件。该文件包含了通用许可证（GPL），规定了你可以使用和重新分发软件的条件。如果你不熟悉 GPL，请阅读此文件以获得对你业务适用性的完整解释和评估。

![](img/d9230b719dc0ef80851f36d8c6f571_497_0.png)

要构建软件包，请遵循 `README` 或 `INSTALL` 文件的指令。对于 XMMS 软件包，`README` 文件列出了一些前提条件（如库），并告诉如何构建和安装软件包。在 XMMS 的情况下，指令步骤如下：

1. 输入 `./configure` 运行脚本，创建系统配置并生成名为 `Makefile` 的文件——用于构建和安装软件包的命令。你可以输入 `./configure-help` 查看接受的选项列表。
2. 输入 `make` 构建软件。此步骤编译所有子目录下的源文件；源代码将每个源文件转换为计算机可以理解的对象文件。
3. 输入 `make install` 安装软件。此步骤将库和可执行二进制文件拷贝到系统的相应目录。

| 第六卷 第四章 管理 | 从源文件构建软件包 472

尽管这些步骤适用于 XMMS，但大多数软件包也遵循 `configure`、`make` 和 `install` 步骤。`configure` 脚本检测系统相关变量并创建构建和安装软件所需的 `Makefile`。

通常情况下，你不需要输入任何命令来构建软件，但在安装系统时必须安装软件开发工具。安装 Fedora Core 时必须安装软件开发软件包。为了构建运行 XMMS，必须输入以下命令运行 `configure` 脚本（输入此命令时必须位于 `xmms-1.2.10` 目录）：

```bash
./configure
```

`configure` 脚本运行并在编译系统各种特性时打印日志信息——从 C 编译器到构建 XMMS 需要的各种库。最后，`configure` 脚本创建一个用于构建软件的 `Makefile`。

如果 `configure` 脚本显示错误并失败，请查看 `INSTALL` 和 `README` 文件寻找解决线索。你可以通过命令行参数向 `configure` 脚本提供信息来规避问题。

在 `configure` 脚本完成后，输入 `make` 构建软件。`make` 命令运行 GNU 工具，它读取 `Makefile` 并根据其中指定的信息编译源文件。`make` 命令遍历所有源目录，编译源文件，并创建运行 XMMS 需要的可执行文件和库。在编译每个文件时，你会看到大量消息。这些消息显示了编译和链接文件的命令。

`make` 命令可能需要 10 到 15 分钟才能完成。`make` 完成后，可以使用以下命令安装 XMMS 软件：

```bash
make install
```

此命令运行 GNU make，但 `install` 参数指示 GNU make 执行 `Makefile` 中的一组特定命令。这些指令实质上遍历了所有子目录并将所有文件拷贝到它们的最终位置。例如，二进制可执行文件 `xmms`、`gnomexmms`、`wmxmms` 和 `xmms-config` 拷贝到 `/usr/bin` 目录。

![](img/d9230b719dc0ef80851f36d8c6f571_498_0.png)
![](img/d9230b719dc0ef80851f36d8c6f571_498_1.png)

## 从源文件构建软件包 473

现在你已经安装了 XMMS，尝试通过在终端输入 `xmms` 或选择主菜单中的声音音频播放器从 GNOME 或 KDE 桌面运行它。XMMS 随 Fedora Core 自带，但现在你获得了新版本的 XMMS（区别是新构建的版本无需任何插件即可播放 MP3 文件）。在 XMMS 窗口中，按 `L` 键打开加载文件对话框并选择一个 MP3 文件播放。你的电脑必须有声卡，并且必须正确配置声卡以便 XMMS 运行。图 4-1 显示了 XMMS 的典型视图。

图 4-1 显示了 XMMS 的典型视图。
img/d9230b719dc0ef80851f36d8c6f571_499_0.png

## 第六卷 第四章 管理应用程序

## 从源文件构建软件包 473

## 安装 SRPMS

如果你有 Fedora Core 的源 CD（你可以从 fedora.redhat.com/download/mirrors.html 列出的网站下载源 CD 镜像），你可以直接从源安装源文件并构建应用程序。Red Hat 在 RPM 中包含源代码文件，就像二进制文件一样，这些源 RPM 通常被称为 SRPMS（源 RPM）。

要安装源 RPM 并构建应用程序，请遵循以下步骤：

- 1. 输入 `/mnt/cdrom` 挂载 DVD-ROM，或等待 GNOME 桌面自动挂载 DVD。

- 2. 通常源 RPM 位于 `SRPMS` 目录。输入以下命令切换到该目录：
```bash
/mnt/cdrom/SRPMS
```

- 3. 使用 `-i` 命令安装 RPM 文件。例如，安装服务器（httpd 源）：
```bash
rpm -ivh httpd*.src.rpm
```

文件安装在 `/usr/src/redhat/SOURCES` 目录。带有 .spec 扩展名的 spec 文件被放置在 `/usr/src/redhat/specs` 目录。spec 文件描述了软件并包含了构建和安装软件的信息。

- 4. 使用 `rpmbuild` 命令配合 spec 文件构建软件。通过使用 `rpmbuild` 命令的不同选项，你可以执行从解压源文件到构建二进制文件的不同任务。例如，处理整个 spec 文件：
```bash
rpmbuild -ba packageName.spec
```

此处 `packageName` 是 SRPM 的名称。该命令通常会构建软件并安装二进制文件。

## 474 使用 Update 更新 Fedora Core 

Fedora Core 自带 Updatedate —— 一个图形化更新代理，它可以下载你系统所需的任何新 RPM 文件并为你安装这些文件。我简要提供如何使用 Updatedate 更新系统的概述。

