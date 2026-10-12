
# 在 `~/.pinerc` 中

`editor=emacsclient`

## Emacs 配置与编程

`Emacs` 的默认设置——从颜色布局到键盘快捷键——都可以任意修改。有两种方法：为了此目的使用菜单和配置掩码（即通过鼠标进行配置），或者通过编辑器直接修改配置文件 `.emacs`。

为了让你能够充分利用 `.emacs` 的所有可能性，本章需要足够的材料来描述 `Emacs` 内部的 `Lisp` 编程语言以及所有可用的扩展函数和变量。这个主题足以写一整本书了！本章仅仅是一个非常初步的、以实践为导向的尝试。

由于 `Lisp` `GNU Emacs` 和 `XEmacs` 之间并不完全兼容，且两个版本通常提供不同的扩展函数，这使得变得更加困难。然而——除非另有说明，否则本章包含的基础信息适用于两个 `Emacs` 版本（`GNU` 版本 20.2，`X` 版本 20.4）。

> 关于 `.emacs` 中某些防止键盘问题和/或外语言特殊字符的非常基础指令的信息，可以参见第 539 页。

## 17.1 基础

### 配置文件

当 `GNU Emacs` 启动时，会按顺序读取三个文件（如果存在）：

```bash
/usr/share/emacs/site-lisp/site-start.el
./emacs
/usr/share/emacs/20.2/lisp/default.el
```

对于 `XEmacs`，读取四个文件：

```bash
/usr/X11R/lib/emacs-20.4/lisp/site-start.el
./emacs
./emacs-options
/usr/X11R/lib/emacs-20.4/lisp/default.el
```

如果根据发行版的不同程序安装在不同的目录（`/usr/lib` 和 `/usr/local`），则显然必须更改路径规范。如果需要，请使用 `locate` 搜索这些文件。

`site-start.el` 是全局设置的地方，任何情况下都应该执行，而 `.emacs` 是个人配置设置。`default.emacs` 同样适用于所有用户，但可以通过 `.emacs` 中的激活（`setq inhibit-init 1`）单独禁用。

`.emacs-options` 文件由 `XEmacs` 在你第一次在 `OPTIONS` 菜单中更改并保存时自动创建。此外，`XEmacs` 在 `.emacs` 文件中增加了一些额外的行，以确保 `XEmacs` 自动加载 `.emacs-options`（但 `GNU Emacs` 不加载）。

> `SuSE Linux` 包含了 `.emacs` 文件（参见 `/etc/sk` 目录），根据 `Emacs` 版本会自动加载 `gnu-emacs-emacs-custom`。此外，通过 `Alt-X customize-browse`（参见第 572 页）所做的更改会自动存储在 `.emacs-custom` 而不是 `.emacs`。然而，这种机制并不是标准的。

### Lisp 文件目录

大多数 `Emacs` 函数，特别是所有的 `Emacs` 扩展和处理模式都是用 `Emacs` 内部编程语言（`Lisp` 的一种方言）实现的。在这方面，`.emacs` 没什么特别；它连接了现有的 `Lisp` 进制文件。

`Lisp` 文件通常位于两个目录：`Emacs Lisp` 目录包含属于标准 `Emacs` 的 `Lisp` 文件。`site Lisp` 目录是放置扩展 `Emacs` 功能的文件的正确位置。（原则上，这些文件也可以安装在 `Emacs Lisp` 目录中，但在下次 `Emacs` 更新时将会丢失）。

## 通过鼠标点击配置

![](img/b30873dd3d753687a59253fb9ad26a0b_600_0.png)

图 17.2 更改信息模式下标题的属性。

- `Alt+X` 允许进行相同的设置，但导航是通过窗口对话框进行的。（`customize` 是 `customize-browse` 的前身。）
- 在 `Emacs` 中，你也可以在一个极其深度嵌套的菜单中指定自定义设置，该菜单以 `OPTIONS | CUSTOMIZE | EMACS` 开头。
- 另一种，在 `Emacs` 中，你可以通过 `OPTIONS` 菜单的其余项目进行许多设置。不要忘记使用 `OPTIONS | SAVE OPTIONS!` 存储这些设置。

`Options` 并不是 `OPTIONS CUSTOMIZE` 的额外变体，而是 `Emacs` 开发过程中出现的一种替代方案。这些设置存储在 `.emacs-options` 中（而不是 `.emacs` 中），并且专门适用于 `Emacs`。取决于加载 `.emacs-options` 的行位于 `.emacs` 中其他选项之前还是之后，菜单设置或 `customize` 设置将优先。为了防止冲突和混乱，你不应该同时使用 `OPTIONS` 和 `CUSTOMIZE` 设置。请在这两种变体中选择其一！

## 17.3 编程技术

为了让你了解 `Emacs` 配置文件的样子，这里有一个典型的代码段：在这四行中，定义了一个新的 `Emacs` 函数 `jump-to-position`，它将光标移动到之前存储在寄存器 1 中的位置。该函数分配了键盘快捷键 `F6` 以备高效使用。

```lisp
(defun jump-to-position() ;定义一个
  (interactive)
  ;新函数
  (jump-to-register 1))
(global-set-key [F6] 'jump-to-position) ;新快捷键 F6
```

当你编辑 `.emacs` 文件时，可以执行命令 `Alt+X eval-buffer`。通过此命令，活动文件中的所有 `Lisp` 命令都会被执行。该命令可以让你无需不断重启 `Emacs` 就能尝试修改后的 `.emacs` 版本。

如果 `.emacs` 中存在语法错误，`Emacs` 将从错误行开始忽略该文件。错误消息会显示在状态行下方，但在 `Emacs` 启动加载文件时它会变得不可见。在这种情况下，该行将显示关于最近操作的消息——例如关于语法高亮的消息。

换句话说：`.emacs` 中的语法错误很容易被忽略，你会疑惑为什么 `.emacs` 中的后续更改没有生效。跟踪错误的最佳方法是将 `.emacs` 下载到编辑器中，并通过 `Alt+X eval-buffer` 显式执行其中包含的命令。错误的指令将被立即识别。

另一个用于测试单个 `Lisp` 指令非常有用的命令是 `Alt+X eval-region`。此命令仅执行标记点（`Ctrl+Space`）和当前光标位置之间的指令。

### 执行 Lisp 代码

- `Alt+X eval-buffer` 执行活动缓冲区中的 `Lisp` 指令
- `Alt+X eval-region` 执行标记点和光标位置之间的指令

### 关于 Lisp 编程的在线帮助

`Emacs` 在线文档包含许多关于 `Emacs` 编程的有用信息：`F1`、`F function-name` 提供指定 `Lisp` 函数的简短描述。`F1`、`Tab` 提供所有可用 `Lisp` 函数的列表。为了查看此列表，必须用 `Ctrl+G` 取消命令。然后，你可以通过 `Ctrl+X B *Com-*` 切换到包含函数列表的缓冲区。

如果你经常需要该列表，应该将缓冲区保存到文件（`Ctrl+X, W`）。同样，你可以通过快捷键 `C-h, V` 获取有关 `Emacs` 已知所有变量的信息。

你可能想知道通过给定快捷键启动的 `Lisp` 函数名称（例如，如果你想在自己的函数中使用此函数）；在这种情况下，使用快捷键 `C-h, C`。`Emacs` 会在屏幕底行显示该函数名称。

### 关于函数和变量的帮助

- `C-h function.name` 关于指定 `Lisp` 函数的信息
- `C-h Tab` 所有已知函数的列表
- `C-h vname` 关于指定 `Lisp` 变量的信息
- `C-h Tab` 所有已知变量的列表
- `C-h C` 关联的 `Lisp` 函数的名称

此外，针对 `GNU Emacs` 有两本极好的编程手册：`elisp-manual` 是超过 700 页的 `GNU Lisp` 方言，`emacs-lisp-intro` 提供了更简洁的编程介绍。

遗憾的是，这些文档包仅在少数发行版中提供（而且大多是旧版本）。然而，在互联网上很容易找到不同格式（`PostScript`, `HTML`）的最新版本：

```
http://www.gnu.org/manual/manual.html
```

当你使用 `Emacs` 工作时，广泛的 `Lisp` 语言参考被集成在 `info` 系统中。在 `Info` 开始菜单中查找 `lispref`。

### 调用 Lisp 函数

`Lisp` 函数通常必须包含在括号内。函数名和参数之间仅用空格分隔。`Lisp` 典型的括号级累积发生在函数作为参数传递给其他函数时。

```lisp
(set-input-mode (car (current-input-mode))
  (nth 1 current-input-mode) 0))
```
