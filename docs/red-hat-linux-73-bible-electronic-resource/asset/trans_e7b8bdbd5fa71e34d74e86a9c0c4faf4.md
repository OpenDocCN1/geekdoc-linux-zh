

## 使用 rpm 验证软件包

如果软件包中的某些功能无法正常工作，或者你怀疑系统已被篡改，rpm 的验证（`-V`）选项可以帮助你验证软件包的内容。每个已安装软件包的信息都会存储在计算机的 RPM 数据库中。通过使用验证选项，你可以检查软件包中的组件是否发生了任何更改。

在验证操作期间，会进行各种文件大小和权限测试。如果一切正常，则不会有任何输出。然而，自安装以来发生任何变更的组件都会被打印出来，并附上指示其变更方式的信息。示例如下：

```bash
# rpm -V ppp
S.5....T c /etc/ppp/chap-secrets
S.5....T c /etc/ppp/options
S.5....T c /etc/ppp/pap-secrets
```

此输出表明，ppp 软件包（用于拨号连接到 TCP/IP 网络，例如互联网）自安装以来有三个文件被修改了。开头的符号表示文件大小（S）、MD5 校验和（5）以及修改时间（T）均已发生变化。字母 c 表示这些都是配置文件。通过检查这些文件，发现更改仅是为了配置 PPP 正常工作而做的修改，可以验证该软件包没有问题。

验证配置文件内容时，你可能会看到以下指示符：

- 5 — MD5 校验和 — MD5 校验和表明文件内容已发生变化。
- S — 文件大小 — 文件中的字符数量已发生变化。
- L — 符号链接 — 该文件已成为指向其他文件的符号链接。
- T — 修改时间 — 文件的修改时间已发生变化。
- D — 设备 — 该文件已成为设备特殊文件。
- U — 用户 — 拥有该文件的用户名已发生变化。
- G — 组 — 分配给该文件的组已发生变化。
- M — 权限 — 如果文件的所有权或权限已发生变化。

> **提示：** 在 Windows 系统中有一个实用程序可以浏览 RPM 文件的内容。通过使用 *rpmbrowser.exe* 实用程序，你可以列出并提取 RPM 发行版中的文件。此实用程序可从 winsite.com 获取（请在 www.winsite.com/ws_search.html 上搜索 rpmbrowser）。

# 从源代码构建和安装

如果无法获取所需软件包的二进制版本，或者你只是想根据需求定制软件包，你可以始终从源代码安装该包。随 Red Hat Linux 附带的源代码 CD 包含你已安装的二进制软件包的等效源代码（SRPMS）。你可以修改源代码并根据需求重新构建。

> **注意：** 虽然本书未随附 Red Hat Linux 源代码 CD，但你可以从出版商处获取副本。请参阅本书背面的 Linux 源代码邮寄索取券。

无法以 SRPMS 格式获得的软件包通常以 `tar/gzip` 格式提供。虽然从源代码存档安装应用程序的确切说明有所不同，但许多以 `.gz` 和 `.tar` 格式提供的软件包都遵循相同的基本步骤。

> **提示：** 在从源代码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议在 Red Hat 安装过程中推荐的所有软件开发包都予以安装。（由于缺少组件导致安装失败是很烦人的，你最终可能浪费大量时间查找缺少的内容。）

以下是 C 语言编程软件开发工具的最小列表：

- `gcc` — 包含 `gcc`（GNU C 编译器）编译器。
- `make` — 包含用于根据 Makefile 生成二进制文件的 `make` 命令。
- `glibc` — 包含重要的共享库、C 库和标准数学库。
- `glibc-devel` — 包含创建可执行文件所需的标准头文件。
- `binutils` — 包含编译程序所需的实用程序（如汇编器和链接器）。
- `kernel-source` — 包含 Linux 内核源代码，重新构建内核时需要。
- `libc` — 包含基于 `libc 5` 的程序所需的库，以便旧应用程序可以在 `glibc`（`libc 6`）系统上运行。

## 安装 SRPMS 格式的软件

要从 Red Hat Linux 源 CD 安装源包，请使用以下程序：

1. 将 Red Hat Linux 源 CD 插入 CD-ROM 驱动器。它应该自动挂载。（如果没有，请在终端窗口中键入 `mount /mnt/cdrom`。）
2. 切换到 CD 上的源代码目录。例如：

   ```bash
   # cd /mnt/cdrom/SRPMS
   ```

3. 选择要安装的包（键入 1s 查看软件包）并使用以下命令安装：

   ```bash
   # rpm -iv package name*.src.rpm
   ```

   （将 *packagename* 替换为你正在安装的软件包名称。）源将安装在 Red Hat Linux 源代码树（/usr/src/redhat）中。Spec 文件被复制到 /usr/src/redhat/SPECS。

4. 切换到 SPECS 目录，如下所示：

   ```bash
   # cd /usr/src/redhat/SPECS
   ```

5. 按如下所示解包源代码：

   ```bash
   # rpm -bp package name*.spec
   ```

6. 包的源代码安装在 /usr/src/redhat/BUILD/package 目录中。

7. 现在你可以对包 BUILD 目录中的文件进行修改。阅读 README、Makefile 和其他文档文件，了解如何构建单独的包。

## 安装 gzip/tar 格式的软件

以下是你可以用于安装许多以 gzip/tar 格式提供的 Linux 软件包的一些通用说明：

1. 从 Internet 或 CD 发行版获取源代码包，并将其复制到空目录中（最好使用标识该包名称的名称）。

2. 假设文件是使用 gzip 压缩的，使用以下命令解压缩文件：

   ```bash
   # gzip -d package.tar.gz
   ```

   结果是包被解压缩，并且包名称中的 .gz 被移除（例如，package.tar）。

3. 从生成的 tar 存档中，按如下所示运行 tar 命令：

   ```bash
   # tar xvf package.tar
   ```

   此命令从存档中提取文件，并将它们复制到当前目录的子目录中。

4. 将目录更改为第 3 步中创建的新子目录，如下所示：

   ```bash
   # cd newdir
   ```

5. 查找名为 INSTALL 或 README 的文件。这些文件之一应该提供有关如何继续安装的说明。通常，使用 make 命令来安装包。以下是当前目录中需要查找的一些事项：

   如果有 Makefile，请尝试运行：

   ```bash
   # ./configure -prefix=/usr
   # make all
   ```

   如果有 Imake 文件，请尝试运行：

   ```bash
   # xmkmf -a
   # make all
   ```

   如果有 Makefile，请尝试运行：

   ```bash
   # make all
   ```

   程序构建和安装后，你可能需要进行额外的配置。你应该查阅随软件提供的 man 手册页和/或 HOWTO 文档，以了解如何继续。

> **提示：** 即使你不是程序员，阅读用于编写程序的源代码通常也能让你深入了解该程序的工作原理。有时关于程序工作原理的说明可能会写在源代码中，但从未包含在文档中。

为了尝试这个步骤，我下载了 whichman 包，其中包含让你通过输入关键字来查找手册页的实用程序。我下载的文件 whichman-1.5.tar.gz 被放置在我创建的名为 /usr/sw/which 的目录中。然后，我分别使用 whichman-1.5.tar.gz 和 whichman-1.5.tar 作为选项运行了 gzip 和 tar 命令。

我更改到了新目录，cd /usr/sw/which/whichman-1.5。然后我列出了其内容。README 文件包含了有关包内容及其安装方法的信息。正如 README 文件所建议的那样，我输入了 make，然后是 make install。whichman、fwhich 和 ffff 命令被安装到 /usr/bin。（此时，你可以检查每个组件的 man 手册页以查看其功能。）

我在 README 文件中找到的最后一件事是需要进行一些配置。我在 $HOME/.bashrc 中添加了一个 MANPATH 变量，以标识要在计算机上被 whichman 实用程序搜索的手册页位置。我添加的行看起来像这样：

```bash
export MANPATH=/usr/man:/usr/X11R6/man:/usr/doc/samba-2.0.2/docs
```

如果你想知道，whichman、fwhich 和 ffff 是可用于搜索 man 手册页的命令。它们可以分别用于查找 man 手册页的多个位置、名称接近你输入的名称的 man 手册页，或位于目录结构中某一点之下的 man 手册页。

