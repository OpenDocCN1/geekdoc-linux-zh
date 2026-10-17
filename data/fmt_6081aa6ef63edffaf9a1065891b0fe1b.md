
# 74 在线文档

确定输出格式。默认设置是 `ps` 用于 `ps`。其他可能的设置有 `dvi`（用于 `dvi` 文件）、`ascii` 用于 ASCII 文本（产生这些结果），以及 `latin1`（类似于 `ascii`，但带有外语言的特殊字符）。

在 Linux 发行版中，man 文本仅以预格式形式提供，因此无法应用 `groff`。然而，在这种情况下，`man` 命令允许将格式化的 man 页面转换为其他格式（PostScript、HTML 等）（参见第 82 页）。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_99_0.png)

## 4.3 info - 用于 GNU 工具和 Emacs 的超文本在线帮助

`info` 是一个比 `man` 强大得多的程序。它特别适用于显示大量的帮助文本，因为它可以处理跨多个文件的交叉引用。`info` 是所有 GNU 工具（如 `find`、`grep`）、带有所有扩展和库的 GNU 编译器以及 Emacs 文本编辑首选文档格式。

`info` 命令的主要缺点是它的操作相当繁琐。具体来说，不能使用光标方向键在文本内部进行导航，这会导致意外跳转到其他主题，并且在某些情况下会导致程序崩溃。

如果你不是使用 `info`，而是启动 Emacs 编辑器并使用 `Alt+X` 或 `Ctrl+X` 切换到 `info` 模式（见第 336 页），就可以绕过这个限制。原则上，`info` 程序只是限制在 `info` 模式下的 Emacs 版本。X 版本 Emacs 让生活变得简单：所有的交叉引用都用特定的颜色突出，并且点击鼠标即可选择。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_99_1.png)

如果 `info` 文本以 HTML 格式提供，阅读起来更加简单。你可以使用任何 WWW 浏览器读取这些文本。某些发行版（SUSE）已经提供了大量的 HTML 格式的 `info` 文件。在随附的文档中，你会找到这种格式的 Emacs 文档。在第 81 页，有关于你自己创建 `info` 文本 WWW 版本的描述。

通常，`info` 文本存储在 `/usr/local/info` 或 `/usr/share/info`。较大的帮助文本通常以几个压缩文件的形式发布，文件名以 `.info-nn.gz` 或仅以 `--nn.gz` 结尾。

```
info [options][subject]
```

`info` 通常带有参数 `subject` 调用。该主题指示要查看 `/usr/info` 目录下的哪个 `info` 文件。如果 `info` 启动时没有参数，程序将显示可用帮助主题的概述（文件 `/usr/info/dir` 主题）。未包含在 `dir` 中的主题只能通过选项 `-f` 查看。例如，`elisp` 文件（Emacs 的文档）就是这种情况。因此，`info` 无法自动处理 `/usr/info` 中包含的所有 `info`。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_99_2.png)

- `file` 加载指定的文件而不是来自 `/usr/info` 的文件。必须提供完整的文件名而不是主题名（例如 `jarg300`, `info.gz`，而不仅仅是 `larg300`）。如果 `info` 文本分布在多个文件中，必须指定第一个文件（例如 `elisp-1.gz`）。

`info` 最重要的键盘命令如下：

- `空格键`（Spacebar）向下滚动文本
- `退格键`（Backspace）向上滚动文本
- `B`, `E` 跳到 `info` 单元的开头/结尾
- `Tab` 键移动光标到交叉引用
- `/` 跟踪交叉引用到不同的单元
- `N` 下一个同层级的 `info` 单元
- `P` 上一个同层级的 `info` 单元
- `U` 向上一个层级
- `L` 回到上次显示的文本
- `H` 详细的使用说明（帮助）
- `?` 命令返回上一级
- `Ctrl+X, D` 关闭帮助窗口（是 `D`，不是 `O`）

有趣的是，有一个 `man` 文本描述了如何使用 `info` 程序的各种。

### `info` 内部原理

`info` 文本是用 `Texinfo` 生成的。`Texinfo` 系统的巨大优势是源文件（`*.texi`）可以同时生成 `info` 和 `DVI` 文件。生成的 `*.texi` 文件可以使用 `dvips` 转换为 PostScript 文件并稍后打印。因此，`*.texi` 文件既适用于生成在线文档，也适用于准备高质量的排版手册（`TeX` 和 `dvips` 在第 351 页开始的独立章节中描述）。

将 `*.texi` 文件转换为 `*.info` 文件是通过命令 `makeinfo name.texi` 完成的。对于复杂文档（如多个文件的分解，例如 Emacs 手册），使用 `Makefile` 文件来控制转换过程。在这种情况下，你只需要在相应的目录下执行 `make`。

```
makeinfo name.texi
```

转换为 `DVI` 文件通过一系列三个命令完成。（只运行一次 `tex` 就足够了——但将丢失索引和交叉引用。）通过 `dvips` 生成一个 PostScript 文件。只有在安装了 `TEX` 的情况下才能转换。

```
tex name.texi
tex name.texi
dvips name.dvi -o name.ps
```

因此，`*.texi` 文件既适用于生成在线文档，也适用于准备高质量的排版手册（`TeX` 和 `dvips` 在第 351 页开始的独立章节中描述）。

将 `*.texi` 文件转换为 `*.info` 文件是通过命令 `makeinfo name.texi` 完成的。对于复杂文档（如多个文件的分解，如 Emacs 手册），使用 `Makefile` 文件来控制转换过程。在这种情况下，你只需要在相应的目录下执行 `make`。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_100_0.png)

## 4.4 HOWTO - 如何工作的？

HOWTO 文本可能是关于 LINUX 安装、配置和硬件最重要的信息源。

### FAQ - 常见问题

在 Linux 下，FAQ 的作用相对于 HOWTO 文本是次要的。然而，有关于各种编程语言、网络对象和其他 Unix 主题（安全等）的无数 FAQ。通常，你可以在 `/usr/doc/faq` 或 `../FAQ` 目录下找到 FAQ。以下 FAQ 对 Linux 特别重要：

- `faq/linux.faq`：当遇到 Linux 问题时，此文件应该是首选方案。它涵盖了安装、兼容性问题、Linux 文件系统处理、X 窗口系统等主题。
- `faq/GCC-FAQ`：此文件对 C 程序员感兴趣。它处理了 `GCC` 编译器在获取阶段的许多基础困难。

在 RedHat 发行版中，你还会在 `/usr/doc/FAQ` 目录下找到额外的 RedHat FAQ，它处理特殊的 RedHat 问题。

这些主题包括对特殊硬件组件的处理（SCSI 磁盘、CD-ROM、以太网卡、键盘）以及 Linux 使用的特殊功能（打印、使用 `UUCP`、`Term` 和 `News` 进行网络配置等）。在 ASCII 格式下，HOWTO 总共占据近 3 Mbytes——这文字比这整本书还要多！

### Linux HOWTO（教程）

| BootPrompt | Ftape | Keystroke | SCSI-Programming |
| :--- | :--- | :--- | :--- |
| Bootdisk | German | Mail | Serial |
| Busmouse | HAM | NET-2 | Shadow-Password |
| CDROM | Hardware | NIS | Sound |
| Commercial | | News | Term |
| Cyrillic | IPX | PCI | Tips |
| DOSEMU | Installation | PCMCIA | UMDOS |
| Danish | Italian | PPP | UPS |
| Distribution | JE | Portuguese | UUCP |
| ELF | Java | Printing | XFree86 |
| Ethernet | Kernel | Printing-Usage | |
| Firewall | Keyboard | SCSI | |
| ADSM-Backup | Getty-ps | Modeline | Tiny-News |
