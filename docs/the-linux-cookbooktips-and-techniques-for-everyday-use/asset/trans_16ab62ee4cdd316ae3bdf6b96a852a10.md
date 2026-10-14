

## 《Linux  cookbook》：日常使用的技巧与技术：

可以使用 zless 代替 less。

Linux 文档项目（LDP）监督创建了超过 100 个 “HOWTO” 文件，每个文件都涵盖 Linux 系统安装或使用的某个特定方面。

LDP HOWTO 文件是存储在 `/usr/doc/HOWTO` 目录中的压缩文本文件；要查看它们，请使用 zless。文件 `/usr/doc/HOWTO/HOWTO-Index.gz` 包含已安装在系统上的所有 HOWTO 文档的带注释索引。[1]

最后，`/usr/doc/FAQ` 目录包含许多关于各种主题的常见问题解答（FAQ）文件，而 Debian FAQ 的文件位于 `/usr/doc/debian/FAQ` 目录中。Debian FAQ 既有 HTML 格式，可在 Web 浏览器中查看（见 Browsing Files 部分），也有压缩文本文件格式，可在 zless 中查看。

- 要在 lynx Web 浏览器中查看 Debian FAQ 的 HTML 版本，请输入：

```
$ lynx /usr/doc/debian/FAQ/debian-faq.html RET
```

- 要在 zless 中查看 Debian FAQ 的压缩文本版本，请输入：

```
$ zless /usr/doc/debian/FAQ/debian-faq.txt.gz RET
```

NOTE: 通常使用 Web 浏览器浏览这些目录中的文档文件非常有用——见 Browsing Files。

在某些系统上，`/usr/doc` 已被 `/usr/share/doc` 目录取代。

## 4. Shell

本章的主题是 shell，即读取你的命令输入并运行指定命令的程序。Shell 环境是与系统交互的最基本方式——从你成功登录系统那一刻起，你就被认为“在”一个 shell 中。

光标前面的 ` $ ` 字符称为 shell 提示符；它告诉你系统已准备好并等待输入。在 Debian 系统上，默认的 shell 提示符还包括当前目录的名称（见 Files and Directories 部分）。波浪号字符（` ~ `）表示你的主目录，你在登录时就会位于该目录。

例如，一个典型用户的 shell 提示符可能如下所示：

```
~ $ _
```

如果你的 shell 提示符显示的是数字符号（` # `）而不是 ` $ `，这意味着你是以超级用户或 root 账户登录的。注意：root 账户对系统具有完全控制权；一个错误的按键就可能意外地将其破坏得非常严重。你需要为自己创建一个不同的用户账户，并使用该账户进行常规操作（见 Making a User Account 部分）。

每个 Linux 系统至少有一个 shell 程序，大多数系统有多个。我们将介绍 bash，它是大多数 Linux 系统上的标准 shell。 （其名称代表 “Bourne again shell”——这是对 Steve Bourne 名字的双关，他是传统 Unix shell，即 Bourne shell 的作者。）

> NOTE: 有关使用 bash 的更多信息，请参阅 Info 文件 `bashref.info`，节点 `Top`。

- 4.1 Keys for Command Line Editing
- 使用命令行。
- 4.2 Redirecting Input and Output
- 如何重定向输入和输出。
- 4.3 Managing Jobs
- 管理你的任务。
- 4.4 Command History
- 使用命令历史。
- 4.5 Recording a Shell Session
- 制作 shell 会话的 typescript。
- 4.6 Customizing Your Shell
- 自定义 shell 的流行方式。

### 4.1 Keys for Command Line Editing

在 Running a Command 中，你学习了如何在 shell 提示符下输入命令来运行命令。你在 shell 提示符下输入的文本称为命令行（也称为输入行）。

下表描述了用于输入命令行的按键。

| KEYSTROKES | DESCRIPTION |
|---|---|
| *text* | 在光标所在位置插入 *text*；如果光标右侧有文本，则会向右移动。 |
| **BKSP** | 删除光标左侧的字符。 |
| **DEL** | 删除光标下方的字符。 |
| **RET** | 将命令行发送给 bash 执行（换句话说，它运行在 shell 提示符下输入的命令）。你不必位于命令行的最右端才能输入 **RET**；你可以在光标位于命令行上的任何位置时输入它。 |
| `C-a` | 将光标移动到输入行的开头。 |
| `C-d` | 与 **DEL** 相同（这是 Emacs 的等价方式）。 |
| `C-e` | 将光标移动到输入行的末尾。 |
| `C-k` | 杀死，或“剪切”，输入行上从光标下方字符到行尾的所有文本。 |
| `C-l` | 清除终端屏幕。 |
| `C-u` | 杀死整个输入行。 |
| `C-y` | 提取，或“粘贴”，最后一次被杀死的文本。文本插入在光标所在位置。 |
| `C-_` | 撤消在此命令行上输入的最后一次操作。 |
| `@leftarrow` | 将光标向左移动一个字符。 [GNU INFO BUG: 前一行中的任何 <> 应该是 ← 方向键。] |
| `@rightarrow` | 将光标向右移动一个字符。 [GNU INFO BUG: 前一行中的任何 <> 应该是 → 方向键。] |
| `@uparrowanddownarrow` | 在命令历史中循环（见 section [Command History](#command-history)）。 [GNU INFO BUG: 前一行中的任何 <> 应该是 上下 方向键。] |

**NOTE:** 这些键盘命令与 Emacs 编辑器（见 section [Emacs](#emacs)）使用的命令相同。许多其他 Emacs 键盘命令在命令行上也有效（见 section [Basic Emacs Editing Keys](#basic-emacs-editing-keys)）。而且，对于 Vi 爱好者，可以配置 bash 以识别 Vi 风格的绑定。

以下各节描述了命令行编辑的一些重要功能，例如引用特殊字符和字符串，让 shell 完成你的输入，重新运行命令，以及运行多个命令。有关 bash 命令行编辑功能的更多信息，请参阅 Info 文件 'bashref.info'，节点 'Command Line Editing'。

- [4.1.1 Passing Special Characters to Commands](#4.1.1) — 引用特殊字符和字符串。
- [4.1.2 Letting the Shell Complete What You Type](#4.1.2) — 让 bash 完成你输入的内容。
- [4.1.3 Repeating the Last Command You Typed](#4.1.3) — 多次运行一个命令。

