
![](img/c8827ea52a0796def3f6891892ed9d3a_257_0.png)

图 13.11 LaTeX 交互会话

## 查看和打印文件

如果想查看生成的 DVI 文件，请从“命令”（Command）菜单中选择“查看”（View）。一个调用 `xdvi` 的命令行（它应该是你的 TeX 安装程序的一部分）将出现在 minibuffer 中，以便你根据需要编辑它。

如果想生成可打印的 PostScript 文件，请从“打印”（Print）子菜单中选择 `ps`。`dvi2ps` 命令行将出现在 minibuffer 中。你需要一个 PostScript 查看器，如 `gv` 或 GhostScript，来查看该文件。请参阅本章前面标题为“打印过滤器”（Printing Filters）的边栏，了解有关打印 PostScript 文件的信息。

AUCTeX 中还有许多其他命令和功能超出了本简短介绍的范畴。AUCTeX 附带的 Info 文件写得很好且完整，应该是你下一个学习资料来源。

## Lout

Lout 文本处理系统是由澳大利亚悉尼大学的 Jeffrey H. Kingston 创立的。（Lout 是“layout”的缩写。）它具有 TeX/LaTeX 的大部分功能，但其大小和复杂度只是后者的一小部分。Lout 已经开发了 16 年。它最初是一个大学研究项目，后来演变为 GNU 许可的免费软件包。随着用户开始贡献功能和提出建议，经过多年发展，Lout 变得非常多功能且强大，但其学习曲线比 LaTeX 平缓。请参阅前文“LaTeX 还是 Lout？”（LaTeX or Lout?）部分，对两者进行比较。

从用户的角度来看，这两种格式系统有很多共同点。标签由某些保留字符指示。这些标签不仅控制结构格式（如章节），还控制字符级特征，例如字体选择。

Eric Marsden 为 Emacs 编写了一个名为 `lout-mode.el` 的 Lout 主模式。它没有 AUCTeX 那么大和复杂，但它拥有大多数标签的键绑定和菜单项。支持字体锁定（font locking），允许以柔和的颜色显示标签。你可以像 AUCTeX 一样在该模式下运行 Lout 处理器并逐步查看错误。

### 安装 Lout

你可以在本书 CD-ROM 的 `/cdrom/packages/lout` 目录中找到 RPM 和 `*.deb` 软件包。如果偏好自行编译，源文件归档也包含在内。使用你的发行版包管理工具来安装预构建的软件包。安装源软件包并不困难得多。你需要编辑 makefile，但文件顶部的说明很清晰。完成此操作后，输入

```
make ; make install
```

你就应该拥有一个随时可用的新 Lout 安装。

Lout 的文档在一个独立的发行版 RPM 或 `*.deb` 中。它以未处理的 Lout 文件形式包含在源文件归档中。

### 使用 lout-mode

你可以在 CD-ROM 目录 `/cdrom/packages` 中找到 `lout-mode.el`。将此文件复制到你的 site-lisp 目录，并将以下行插入你的 `~/.emacs` 文件：

```lisp
(autoload 'lout-mode "lout-mode" "Major mode for editing Lout text" t)
(setq auto-mode-alist
      (append '(("\\.lout$" . lout-mode)) auto-mode-alist))
```

后两行使得任何具有 `*.lout` 后缀的文件都在 lout-mode 下编辑。如果你想为 Lout 文件使用不同的后缀，请编辑最后一行，将 `\\.lout$` 改为你喜欢的任何内容。别忘了对该文件进行字节编译：加载 `lout-mode.el` 并从 Emacs-Lisp 菜单中选择“字节编译文件”（Byte-compile File）。

如果你不熟悉 Lout，你可能正在好奇 Lout 标记看起来是什么样子的。即使你安装了默认的 Lout 和文档发行软件包，你可能也想要将 CD-ROM 中的源文件归档解压到一个临时目录。删除除 `/doc` 目录以外的所有内容，然后使用 Dired 访问该目录。那里的文件没有识别后缀。它们是 Lout 文件，如果经过处理，将变成 Lout 文档 PostScript 文件。你不需要处理它们，因为假定你已经安装了 Lout 文档。它们是 Lout 文件的良好示例，让你了解这些文件是如何标记的。

在 Dired 缓冲区中的文件上点击鼠标中键将其加载。它出现在 Basic 模式而不是 Lout 模式下，因为文件没有后缀。按 M-x 并输入

```
lout-mode
```

然后按 M-x 并输入

```
font-lock-mode
```

你应该看到类似图 13.12 的内容。（字体锁定命令可能必需也可能不必需，这取决于你的 Emacs 配置。）

![](img/c8827ea52a0796def3f6891892ed9d3a_259_0.png)

![](img/c8827ea52a0796def3f6891892ed9d3a_260_0.png)

图 13.13 lout-mode 菜单

图 13.13 显示了 lout-mode 菜单，它将两个 AUCTeX 菜单的功能合二为一。

`lout-mode.el` 中有几个变量可能需要编辑以匹配你的系统。你可以在 Lisp 文件的开头找到它们：

```lisp
(defvar lout-view-command "gv -safe"
 "*The name of the Postscript previewer on your system.
This program is called from \\[lout-view]. You can include command-line
arguments such as \\ -dSAFER \" to protect against dangerous Postscript
commands.")
```

```lisp
(defvar lout-print-command "lpx -Pps"
 "*How to print Postscript files on your system.
If this is a string it will be sent to a shell, after having the
name of the Postscript file appended to it. If it is a function it
will be called with the name of the Postscript file as a parameter,
and should return a string which when passed to a shell, will print the
file.")
```

在第一行中，如果你没有安装 `gv`，可能需要将 `gv` 更改为 `ghostview`。你可能会考虑安装 `gv`，因为它是一个比 `ghostview` 功能更丰富且更便捷的 PostScript 查看器。

`print` 命令因你的 Linux 发行版、打印后台处理程序（print spooler）和过滤器设置而异。在许多系统上，简单的 `lpr` 就足够了。

## 处理和打印

从 Lout 菜单中选择 Loutify（或按 Ctrl-c Ctrl-b）会将你的文件发送到 Lout 文本处理器。一个新窗口打开，显示文件被编译为 PostScript 格式时的消息。如果发生错误，你可以从菜单中选择下一个错误（或按 Ctrl-c '），点（point）将移动到源文件中需要关注的地方。“预览”（Preview）和“打印”（Print）的菜单项和键绑定让你可以使用 PostScript 查看器查看完成的 PostScript 文件，然后将其发送去打印。

文件 `user.ps` 是 Lout 用户的全面且编写良好的指南。可以在 Lout 文档软件包中找到此文件。如果你从源文件归档安装了 Lout，你需要在 Lout 源目录的 `*/doc/user` 子目录中名为 "all" 的文件上运行 Lout。你需要在 "all" 文件上多次运行 Lout，因为在这种复杂索引文档中，需要进行多次编译才能解析交叉引用。

## 结论

尽管 HTML 和 LaTeX 是最流行的格式语言，Emacs 也具有一些使用较少语言的模式。

*troff*（及其 GNU 后代 *groff*）在早期 UNIX 系统上广泛用于文档格式设置，并且仍然是生成 UNIX、BSD 和 Linux 手册页的标准。*nroff*-mode 提供了用于创建此类文档的字体锁定和键绑定。

*psgnl* 除了作为 XEmacs HTML 模式的基础外，也是为编写 SGML 和 XML 文件提供的全功能辅助工具。

随着新的文档格式方法被开发，毫无疑问 Emacs 支持会紧随其后。

下一章介绍了许多节省时间的 Emacs 模式和实用工具。

