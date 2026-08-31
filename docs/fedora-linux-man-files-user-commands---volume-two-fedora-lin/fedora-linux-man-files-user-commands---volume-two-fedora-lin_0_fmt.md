
# Fedora Linux 手册文件：用户命令 - 第二卷 (Fedora Linux 手册文件 - 用户命令指南 2)

![](img/00002.jpeg)

## 献辞

本书献给 Michael Kerrisk 以及 Linux 文档项目团队。

# ESPEAK

## 名称

`espeak` - 一个多语言软件语音合成器。

## 语法

`espeak` `[options]` `[words]`

## 描述

`espeak` 是一个用于英语及其他某些语言的软件语音合成器。

### 选项

`-ffile`

要说的文本文件。

`--stdin`

从 stdin 读取文本输入而非文件

如果既没有使用 `-f` 也没有使用 `--stdin`，则朗读 `words`；如果没有，则从 stdin 逐行读取文本。

`-ainteger`

幅度，0 到 20，默认值为 10。

`-ginteger`

词间距。在默认速度下，单词之间的暂停单位为 10 ms。

`-kinteger`

用以下方式指示大写字母：1=发音，2=读取单词 "capitals"，值越大音调越高（尝试 `-k20`）。

`-linteger`

行长度。如果不是零（默认值），则将小于此长度的行视为从句结束。

`-pinteger`

音调调整，0 到 99，默认值为 50。

`-sinteger`

速度为每分钟单词数，默认值为 160。

`-vvoicename`

使用 `espeak-data/voices` 中此名的语音文件。

`-wfile`

将输出写入此 WAV 文件，而不是直接朗读。

`-b`

输入文本为 8 位编码。

`-m`

指示文本包含 SSML（语音合成标记语言）标签或其他 XML 标签。支持的 SSML 标签将会被解释。其他标签（包括 HTML）将被忽略，但某些 HTML 标签（如 `<hr>` `<h2>` 和 `<li>`）会确保语音中断。

`-q`

静音模式，不产生任何语音（可能配合 `-x` 使用）。

`-x`

将音标助记符写入标准输出。

`-X`

将音标助记符和翻译轨迹写入标准输出。

`-z`

文本结束处不进行句末暂停。

`--compile=[voicename]`

编译当前目录下的发音规则和字典。`voicename` 是可选的，用于指定要使用的语言。

`--ipa=[ipa]`

使用国际音标将音标写入标准输出。如果 `ipa` 为 1 则使用连音，如果为 2 则使用 ZWJ，如果为 3 则用 `_` 分隔。

`--path=path`

指定包含 `espeak-data` 目录的路径。

`--pho`

将 mbrola 音标数据（`.pho`）写入标准输出或 `--phonout` 指定的文件。

`--phonout=filename`

将 `-x`、`-X` 命令的输出以及 mbrola 音标数据写入此文件。

`--punct=[characters]`

朗读时读取标点符号的名称。如果省略 `characters`，则朗读所有标点符号。

`--split=minutes`

每隔 `minutes` 分钟开始一个新的 WAV 文件。配合 `-w` 使用。

`--stdout`

将语音输出写入标准输出。

`--voices=[language]`

列出可用语音。如果存在 `language`，则仅列出适用于该语言的语音。

`-h`, `--help`

显示选项摘要。

`--version`

显示版本信息。

## 作者

eSpeak 由 Jonathan Duddington `<jonsd@jsd.clara.co.uk>` 编写。该软件包的网页可以在 http://espeak.sourceforge.net/ 找到。

本手册由 Luke Yelavich `<themuso@ubuntu.com>` 编写，用于 Ubuntu 项目（但其他人可以使用）。由 Jaroslav karvada `<jskarvad@redhat.com>` 进行了多次更新。

* * *

# EUTP

## 名称

`eutp` - EuroBraille 文件传输

## 语法

`eutp`

## 描述

`eutp` 允许你与 EuroBraile 的 Clio 终端交换文件。

## 命令行选项

目前无

## 返回值

| 1 | 错误 |

## Shell 扩展

就我们所知，本手册发布的所有文本除非另有说明，均属于公有领域。

我们非常重视对公有领域的承诺。

如果您有理由认为 LinuxManFiles.com 发布的文本尚未进入公有领域，请发送邮件至：`editor at linuxmanfiles.com`。

## 作者

Olivier Bert `<olivier.bert@laposte.net>`

* * *

# evince

## 名称

`evince` - GNOME 文档查看器

## 语法

`evince [--help] [--page-label=PAGE| --page-index=NUMBER| --named-dest=DEST] [--fullscreen] [--presentation] [--preview] [--find=STRING] [filename(s)...]`

## 描述

Evince 是一个能够显示多种格式（如 PDF 和 Postscript）的文档查看器。关于 Evince 的更多通用信息请访问我们的网站 http://www.gnome.org/projects/evince/

### 选项

`-?`, `-h`, `--help`

打印选项。

`-p`, `--page-label=PAGE`

根据标签打开文档。

`-i`, `--page-index=NUMBER`

根据索引打开文档（不是页标签）。

`-n`, `--named-dest=DEST`

根据指定的目标打开文档。

`-f`, `--fullscreen`

以全屏模式运行 evince。

`-s`, `--presentation`

以演示模式运行 evince。

`-l`, `--find=string`

你在此传递一个单词或短语。如果存在，Evince 将显示文档及第一个匹配项。

`filename(s)...`

指定启动 Evince 时打开的文件。如果没有指定，Evince 将打开一个空白窗口。可以通过空格分隔加载多个文件。Evince 还支持远程文件。例如，你可以传递网络位置或从 FTP 服务器加载文件，如 `ftp://adobe.com/sample.pdf`。

## 打印预览选项

这些选项主要用于 GTK+ 的打印预览功能。有关这些选项的更多信息请参阅 http://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-print-preview-command

`-w`, `--preview`

作为预览器运行 evince。

`--unlink-temp-file`

如果在预览模式运行 evince，这将解链 GTK+ 创建的临时文件。

`--print-settings %s %f`

这会将 PDF 文件的完整路径 `f` 和打印对话框的设置 `s` 发送到 evince。

## 缺陷

如果您发现 Bug，请在 http://bugzilla.gnome.org/enter_bug.cgi?product=evince 报告。

# VIM

## 名称

`vim` - Vi 提高版，一个程序员的文本编辑器

## 语法

`vim` [options] `-q` [errorfile]

`ex` `gex`

`view`

`gvim` `gview` `vimx` `evim` `eview`

`rvim` `rview` `rgvim` `rgview`

## 描述

`Vim` 是一个向后兼容 Vi 的文本编辑器。它可以编辑各种纯文本。它对于编辑程序特别有用。

相比于 Vi，它有很多增强功能：多级撤销、多窗口和缓冲区、语法高亮、命令行编辑、文件名补全、在线帮助、视化选择等。请参见 `:help vi_diff.txt` 获取 `Vim` 与 Vi 之间的差异总结。

在运行 `Vim` 时，可以通过 `:help` 命令从在线帮助系统中获取大量帮助。请参见下文的在线帮助部分。

通常通过以下命令启动 `Vim` 来编辑单个文件：

```
vim file
```

更通用地说，`Vim` 的启动方式为：

```
vim [options] [filelist]
```

如果缺少 `filelist`，编辑器将带有空缓冲区启动。否则，以下四个选项中恰好可以使用一个来选择一个或多个要编辑的文件。

- `file ..`

文件名列表。第一个文件将作为当前文件并读入缓冲区。光标将位于缓冲区的第一行。你可以使用 `:next` 命令跳转到其他文件。要编辑以连字符开头的文件，请在 `filelist` 前加 `--`。

- `-`

要编辑的文件从 `stdin` 读取。命令从 `stderr` 读取，后者应该是一个 TTY。

- `-t {tag}`

要编辑的文件和初始光标位置取决于一个“标记”（tag），类似于跳转标签。在 tags 文件中查找 `{tag}`，关联的文件将成为当前文件并执行关联的命令。这通常用于 C 程序，在这种情况下 `{tag}` 可以是一个函数名。其效果是包含该函数的文件成为当前文件，光标置于函数起始。请参见 `:help tag-commands`。

- `-q [errorfile]`

以快速修复（quickFix）模式启动。读取文件 `[errorfile]` 并显示第一个错误。如果省略 `[errorfile]`，则从 `errorfile` 选项获取文件名（Amiga 上默认为 `"AztecC.Err"`，其他系统上为 `"errors.err"`）。可以使用 `:cn` 命令跳转到后续错误。请参见 `:help quickfix`。

`Vim` 的行为取决于命令名称（可执行文件可能仍是同一个）。

`vim`

“普通”方式，一切均为默认。

`ex`

以 Ex 模式启动。使用 `:vi` 命令进入普通模式。也可以通过 `-e` 参数实现。

`view`

以只读模式启动。你将受到免写入保护。也可以通过 `-R` 参数实现。

`gvim` `gview`

GUI 版本。启动一个新窗口。

`gex`

在 Ex 模式下启动一个新的 `gvim` 窗口。也可以对 `gvim` 使用 `-e` 参数实现。

`vimx`

以类似于 `vim` 的 "Vi" 模式启动 `gvim`，但具有额外功能，如 xterm 剪贴板支持。

`evim` `eview`

简单模式下的 GUI 版本。启动一个新窗口。也可以通过 `-y` 参数实现。

`rvim` `rview` `rgvim` `rgview`

与上述相同，但带有限制。将无法启动 shell 命令或暂停 `Vim`。也可以通过 `-Z` 参数实现。

## 选项

选项可以任意顺序给出，位于文件名之前或之后。不带参数的选项可以组合在单个连字符之后。

- `+[num]`

对于第一个文件，光标将置于第 `"num"` 行。如果缺少 `"num"`，光标将置于最后一行。

- `+{pat}`

对于第一个文件，光标将置于 `{pat}` 第一次出现的地方。请参见 `:help search-pattern` 查看可用的搜索模式。

- `+{command}`

- `-c {command}`

在读取第一个文件后将执行 `{command}`。`{command}` 被解释为一条 Ex 命令。如果 `{command}` 包含空格，则必须用双引号括起来（这取决于所使用的 shell）。例如：`Vim "+set si" main.c`。

注意：你最多可以使用 10 get `+` 或 `-c` 命令。

- `-S {file}`

在读取第一个文件后将源化 `{file}`。这等同于 `-c "source {file}"`。`{file}` 不能以 `-` 开头。如果省略 `{file}`，则使用 `"Session.vim"`（仅当 `-S` 是最后一个参数时有效）。

- `--cmd {command}`

类似于使用 `-c`，但命令在处理任何 vimrc 文件之前执行。你可以使用最多 10 个 get 这样的命令，且与 `-c` 命令相互独立。

- `-A`

如果 `Vim` 编译时带有阿拉伯语支持（用于编辑从右向左的文件和阿拉伯键盘映射），此选项将以阿拉伯模式启动 `Vim`，即设置 `'arabic'`。否则将给出错误信息且 `Vim` 退出。

- `-b`

二进制模式。将设置一些选项，能够编辑二进制或可执行文件。

- `-C`

兼容模式。设置 `'compatible'` 选项。这会让 `Vim` 的行为主要类似于 Vi，尽管存在 `.vimrc` 文件。

- `-d`

以 diff 模式启动。应该有两个、三个或四个文件名参数。

- `-d {device}`

打开 `{device}` 作为终端。

- `-D`

调试。进入调试模式。

- `-e`

以 Ex 模式启动。

- `-E`

以改进模式启动 `Vim`。

- `-f`

前台。对于 GUI 版本，`Vim` 将等待。

- `-nofork`

GUI 版本。

- `-m`

禁用修改文件。

- `-M`

不允许修改。

- `-N`

非兼容模式。重置 `'compatible'` 选项。这会让 `Vim` 的行为更好，但与 Vi 的兼容性较低，尽管不存在 `.vimrc` 文件。

- `-n`

不使用交换文件。崩溃后恢复是不可能的。

- `-nb`

作为 NetBeans 的编辑器服务器。详情请阅文档。

- `-o[N]`

叠加打开 N 个窗口。

- `-O[N]`

并排打开 N 个窗口。

- `-p[N]`

打开 N 个标签页。

- `-R`

只读模式。将设置 `readonly` 选项。你仍然可以编辑缓冲区，但将防止意外覆盖文件。如果你确实想覆盖文件，请在 Ex 命令后添加感叹号，例如 `:w!`。`-R` 选项也隐含 `-n` 选项（见下文）。`readonly` 选项可以通过 `:set noro` 重置。查看 `:help 'readonly'`。

- `-r`

列出交换文件，并带有关于使用它们进行恢复的信息。

- `-r {file}`

恢复模式。交换文件用于恢复崩溃的编辑会话。交换文件是一个与文本文件名相同但带有 `.swp` 后缀。查看 `:help recovery`。

- `-s`

静默模式。只有当作为 "Ex" 启动或在 `-s` 选项之前给出 `-e` 选项时有效。

- `-s {scriptin}`

读取脚本文件 `{scriptin}`。文件中的字符被解释为就像你输入它们一样。可以使用命令 `:source! {scriptin}` 实现。如果在编辑器退出之前到达文件末尾，将从键盘继续读取字符。

- `-T {terminal}`

告诉 `Vim` 你正在使用的终端名称。仅在自动方式不起作用时需要。应该是 `Vim`（内置）已知的或在 `termcap` 或 `termin` 文件定义的终端。

- `-u {vimrc}`

使用文件 `{vimrc}` 中的命令进行初始化。跳过所有其他初始化。用此编辑特殊文件。也可以通过提供名称 `"NONE"` 跳过所有初始化。在 vim 中查看 `:help initialization` 以获取更多详情。

- `-U {gvimrc}`

使用文件 `{gvimrc}` 中的命令进行 GUI 初始化。跳过所有 GUI 初始化。也可以通过提供名称 `"NONE"` 跳过所有 GUI 初始化。在 vim 中查看 `:help gui-init` 以获取更多详情。

- `-V[N]`

详细模式。提供关于加载了哪些文件以及读写 viminfo 文件的消息。可选数字 `N` 是 `verbose` 的值。默认为 10。

- `-v`

以 Vi 模式启动 `Vim`，就像调用执行名为 "vi" 一样。这仅在调用执行名为 "ex" 时有效。

- `-w {scriptout}`

你输入的所有字符都会记录在文件 `{scriptout}` 中，直到你退出 `Vim`。如果你想创建一个用于 `vim -s` 或 `:source!` 的脚本文件，这非常有用。如果 `{scriptout}` 文件存在，则将追加字符。

- `-W {scriptout}`

类似于 `-w`，但会覆盖现有文件。

- `-x`

写文件时使用加密。将提示加密密钥。

- `-X`

不连接到 X 服务器。缩短终端中的启动时间，但不会使用窗口标题和剪贴板。

- `-y`

以简单模式启动 `Vim`，就像调用执行名为 "evim" 或 "eview" 一样。让 `Vim` 行为像一个点击并输入类型的编辑器。

- `-Z`

限制模式。工作类似于执行程序带有 `"r"` 启动。

- `--`

表示选项的结束。此后的参数将被视为文件名。这可以用于编辑以 `-` 开头的文件名。

- `--echo-wid`

仅限 GTK GUI：在标准输出上回窗口 ID。

- `--help`

提供帮助消息并退出，就像 `-h` 一样。

- `--literal`

按字面取文件名参数，不扩展通配符。这在 shell 扩展通配符的 Unix 上没有影响。

- `--noplugin`

跳过加载插件。由 `-u NONE` 隐含。

- `--remote`

连接到 Vim 服务器并让它编辑其余参数给出的文件。如果未找到服务器，将给出警告并在当前 Vim 中编辑文件。

- `--remote-expr {expr}`

连接到 Vim 服务器，在其中求值 `{expr}`并将结果打印到标准输出。

- `--remote-send {keys}`

连接到 Vim 服务器并向其发送 `{keys}`。

- `--remote-silent`

类似于 `--remote`，但在未找到服务器时不给出警告。

- `--remote-wait`

类似于 `--remote`，但在文件被编辑之前 `Vim` 不会退出。

- `--remote-wait-silent`

类似于 `--remote-wait`，但在未找到服务器时不给出警告。



`--remote-tab[-wait][-silent]`

类似于`--remote`，但为每个文件使用一个标签页。

`--role`

设置一个唯一的角色来识别主窗口。

`--serverlist`

列出可以找到的所有 Vim 服务器的名称。

`--servername {name}`

使用`{name}`作为服务器名称。用于当前 Vim，除非配合`--remote`参数使用，此时它是要连接的服务器名称。

`--socketid {id}`

仅限 GTK GUI：使用`GtkPlug`机制在另一个窗口中运行`gvim`。

`--version`

打印版本信息并退出。

## 在线帮助

在`Vim`中输入`:help`开始。输入`:help subject`获取有关特定主题的帮助。例如，`:help ZZ`获取`"ZZ"`命令的帮助。使用`<Tab>`和`CTRL-D`完成主题（`:help cmdline-completion`）。存在标签可以从一个地方跳转到另一个地方（类似于超链接，查看`:help`）。所有文档文件都可以以此方式查看，例如，`:help syntax.txt`。

# 文件

`/usr/share/vim/vim74/doc/*.txt`

`Vim`文档。

`/usr/share/vim/vim74/doc/tags`

`Vim`文档。用于查找文档的标签文件。

`/usr/share/vim/vim74/doc/syntax/*.vim`

语法文件。

`/etc/vimrc`

系统级。

`~/.vimrc`

你的初始化。

`/etc/gvimrc`

系统级初始化。

`~/.gvimrc`

你的个人初始化。

`/usr/share/vim/vim74/doc/optwin.vim`

用于选项的脚本。

`/usr/share/vim/vim74/doc/menu.vim`

系统级菜单。

`/usr/share/vim/vim74/doc/bugreport.vim`

生成报告的脚本。

`/usr/share/vim/vim74/doc/filetype.vim`

检测类型的脚本。

`/usr/share/vim/vim74/doc/scripts.vim`

检测类型的脚本。

`/usr/share/vim/vim74/doc/print/*.ps`

用于 PostScript 的文件。

`http://www.vim.org/`

## 参见

`vimutor(1)`

## 作者

大部分`Vim`由 Bram Moolenaar 制作，有许多人的帮助。查看`:help credits`在`Vim.`。

## 错误

可能。查看`:help todo`列表以获取问题。注意，某些被认为是错误的事情实际上是对 Vi 行为的过度忠实复制。如果你认为其他事情是“因为 Vi 的不同”。

## 作者

exempi 由 Hubert Figuiere 编写。

包含了 Adobe Systems Inc. 编写的 SDK。

## 许可证

exempi 根据 BSD 许可证许可。

# exempi

## 名称

`exempi` - 操作元数据的命令行工具

## 语法

`exempi { -h | [ -R ] | -x ] [ -w | -o <file> } ] [ -g <prop_name> | -s <prop_name> -v <value> ] <files>`

### 选项

`-h`：显示此帮助。

`-R`：不协调。

`-x`：转储 XML。

`-X`：文件(s) 是 XMP。

`-w`：原地写入。仅针对`-s`。不兼容`-o`。

`-o <file>`：将输出到。

`-n <ns> <prefix>`：设置命名空间的前缀。

`-g <prop_name>`：获取`prop_name`的值。

`-s <prop_name> -v <value>`：获取或获取值。

`<files>`：从文件读取。

## 安全

源代码没有经过安全审核。命令行工具没有强力的输入检查。

小心不要以超级用户身份运行该工具。如果你决定在在线（web）中使用它。

欢迎补丁和建议。

## 作者

exempi 由 Hubert Figuiere 编写。

它包含了 Adobe Systems Inc. 编写的 SDK。

## 许可证

exempi 根据 BSD 许可证许可。

# 扩展

## 名称

`expand` - 将制表符转换为空格

## 语法

`expand [OPTION]... [FILE]...`

## 描述

将每个`FILE`中的制表符转换为空格，写入到标准输出。

没有`FILE`，或者当`FILE`为`-`时，从标准输入读取。

长选项的强制参数对于短选项也是强制的。

`-i`，`--initial`

在非空白字符后不转换制表符。

`-t`，`--tabs=NUMBER`

制表符之间间隔`NUMBER`个字符，而不是 8 个。

`-t`，`--tabs=LIST`

使用逗号分隔的显式制表位置列表。

`--help`

显示此帮助并退出。

`--version`

输出版本信息并退出。

## 作者

由 David MacKenzie 编写。

## 错误报告

GNU coreutils 在线帮助文档：<http://www.gnu.org/software/coreutils/>

将 expand 翻译翻译错误报告至 <http://translationproject.org/team/>

## 版权

Copyright Š 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。

这是免费软件：你可以自由地更改和分发它。在法律允许范围内，不提供任何担保。

## 参见

`unexpand(1)`

完整文档位于：<http://www.gnu.org/software/coreutils/expand>

或通过本地信息可用：`info '(coreutils) expand invocation'`

# EXPR

## 名称

`expr` - 求值表达式

## 语法

`expr EXPRESSION`

`expr OPTION`

## 描述

`--help`

显示此帮助并退出。

`--version`

输出版本信息并退出。

将`EXPRESSION`的值打印到标准输出。下方的空行分隔优先级增加的组。`EXPRESSION`可以：

`ARG1 | ARG2`

如果`ARG1`既不为空为 0，则为`ARG1`，否则为`ARG2`。

`ARG1 & ARG2`

如果两个参数都不为空或为 0，则为`0`。

`ARG1 < ARG2`

`ARG1`小于`ARG2`。

`ARG1 <= ARG2`

`ARG1`小于或等于`ARG2`。

`ARG1 = ARG2`

`ARG1`等于`ARG2`。

`ARG1 != ARG2`

`ARG1`不等于`ARG2`。

`ARG1 >= ARG2`

`ARG1`大于或等于`ARG2`。

`ARG1 > ARG2`

`ARG1`大于`ARG2`。

`ARG1 + ARG2`

`ARG1`和`ARG2`的算术求和。

`ARG1 - ARG2`

`ARG1`和`ARG2`的算术差值。

`ARG1 * ARG2`

`ARG1`和`ARG2`的算术乘积。

`ARG1 / ARG2`

`ARG1`除以`ARG2`的算术商。

`ARG1 % ARG2`

`ARG1`除以`ARG2`的算术余数。

`STRING : REGEXP`

在`STRING`中对`REGEXP`进行锚定模式匹配。

`match STRING REGEXP`

与`STRING : REGEXP`相同。

`substr STRING POS LENGTH`

`STRING`的子字符串，`POS`从 1 开始计数。

`index STRING CHARS`

`STRING`中找到任何`CHARS`的索引，或为`0`。

`length STRING`

`STRING`的长度。

`+ TOKEN`

将`TOKEN`解析为字符串，即使它是像`'match'`的关键字或像`'/'`的运算符。

`( EXPRESSION )`

`EXPRESSION`的值。

注意，许多运算符在 shell 中需要转义或加引号。如果两个`ARGs`都是数字，则进行算术比较，否则进行字典序比较。模式匹配返回`\(`和`\)`之间的匹配字符串或空；如果没有使用`\(`和`\)`，它们返回匹配的字符数或`0`。

如果`EXPRESSION`既不为空为 0，则退出状态为`0`；如果`EXPRESSION`为空或 0，则为`1`；如果`EXPRESSION`语法无效则为`2`；如果发生错误则为`3`。

## 作者

由 Mike Parker、James Youngman 和 Paul Eggert 编写。

## 错误报告

GNU coreutils 在线帮助文档：<http://www.gnu.org/software/coreutils/>

将`expr`翻译错误报告至 <http://translationproject.org/team/>

## 版权

Copyright Š 2015 Free Software Foundation, Inc. 许可证 GPLv3+：GNU GPL 3 或更高版本 <http://gnu.org/licenses/gpl.html>。

这是免费软件：你可以自由地更改和分发它。在法律允许范围内，不提供任何担保。

## 参见

完整文档位于：<http://www.gnu.org/software/coreutils/expr>

或通过本地信息可用：`info '(coreutils) expr invocation'`

# extlinux

## 名称

`extlinux` - 在 ext2/ext3 文件系统上安装`SYSLINUX`引导程序

## 语法

`extlinux [options] directory`

## 描述

`EXTLINUX`是一个新的 syslinux 派生版本，从 Linux ext2/ext3 文件系统启动。它与`SYSLINUX`工作方式相同，但有细微修改。它旨在简化 Linux 的首次安装，并创建救援和其他特殊用途启动盘。

安装程序设计为在挂载的目录上运行。例如，如果你有一个 ext2 或 ext3 USB 闪盘挂载在`/mnt`，你可以运行以下命令：

```bash
extlinux --install /mnt
```

## 选项

`-H, --heads=#`

强制指定头部数。

`-i, --install`

在当前启动区安装。

`-O, --clear-once`

清除启动区的命令。

`-o, --once=command`

在启动时执行一次命令。

`-M, --menu-save=label`

将标签设置为默认。

`-r, --raid`

失败时回退到`EXTLINUX`。

`--reset`

重置辅助数据。

`-S, --sectors=#`

强制扇区数。

`-U, --update`

更新`EXTLINUX`。

`-z, --zip`

强制 zip 架构。

`--device=devename`

覆盖设备。

# 文件

`extlinux`配置需要命名为`syslinux.cfg`，参见`linux`。

## 错误

感谢听到`extlinux`的任何问题。如果你正在使用它，请向 majordomo@linux.org 发送消息：

`syslinux`文件。

## 参见

`syslinux(1)`

# FALLOCATE

## 名称

`fallocate` - 预分配或释放空间到

## 语法

`fallocate [-c] [-n] [-p] [-z] [-o offset] [-l length] filename`

`fallocate -d [-o offset] [-l length] filename`

## 描述

`fallocate`用于操作文件的已分配空间，无论是释放还是预分配它。对于支持`fallocate`系统调用的系统，通过分配块并将其标记为未初始化来快速进行预分配。这比创建一个零文件快得多。

`fallocate`返回的退出代码成功时为`0`，失败时为`1`。

### 选项

`length`和`offset`参数可以后跟倍数后缀 KiB（=1024）、MiB（=1024*1024），以及 GiB、TiB、PiB、EiB、ZiB 和 YiB（“iB”是可选的，例如“K”与“KiB”含义相同）或后缀 KB（=1000）、MB（=1000*1000），以及 GB、TB、PB、EB、ZB 和 YB（“iB”是可选的）。

选项`--collapse-range`、`--dig-holes`、`--punch-hole`和`--zero-range`是互斥的。

`-c, --collapse-range`

`-d, --dig-holes`

检测并挖掘空洞。这使文件原地稀疏化，而不使用额外的磁盘空间。空洞的最小尺寸取决于文件系统的 I/O 块大小（通常为 4096 字节）。此外，使用此选项时，隐含`--keep-size`。如果通过`--offset`和`--length`指定范围，则对整个文件进行空洞分析。

`-c, --collapse-range`

从文件中删除字节范围，而不留空洞。要压缩的字节范围从`offset`开始，持续`length`字节。在操作完成后，从`offset`+`length`开始的文件内容将附加到位置`offset`，文件将减小`length`字节。`--keep-size`选项可能用于压缩范围。自 Linux 3.15 起适用于 ext4（仅针对基于范围的文件）和 XFS。

你可以将此选项理解为执行`cp --sparse`然后将目标文件重命名为原始文件，而不需要额外的磁盘空间。

查看`--punch-hole`获取支持的文件系统列表。

`-l, --length` `长度`

指定范围的长度，单位为字节。

`-n, --keep-size`

不修改文件的显示长度。这可能会在 EOF（文件结束符）之后有效分配块，这些可以通过`truncate`移除。

`-o, --offset` `偏移量`

指定范围的起始偏移量，单位为字节。

`-p, --punch-hole`

在从`offset`开始并持续`length`字节的字节范围内释放空间（即创建一个空洞）。在指定的范围内，部分文件系统块将被置零，整个文件系统块将从文件中移除。调用成功后，对该范围的后续读取将返回零。此选项可能与`--zero-range`选项同时指定。此外，使用此选项时，隐含了`--keep-size`。

支持 XFS（自 Linux 2.6.38 起）、ext4（自 Linux 3.0 起）、Btrfs（自 Linux 3.7 起）和 tmpfs（自 Linux 3.5 起）。

`-v, --verbose`

启用详细模式。

`-z, --zero-range`

将从`offset`开始并持续`length`字节的字节范围内的空间置零。在指定的范围内，跨越文件空洞的区域将预分配块。调用成功后，对该范围的后续读取将返回零。

置零操作在文件系统内部完成，优选通过将范围转换为未写入的范围区（unwritten extents）。这种方法意味着指定的范围不会在设备上进行物理置零（范围两端的部分块除外），在其他情况下 I/O 只需要更新元数据。

可以指定`--keep-size`选项以防止文件长度被修改。

自 Linux 3.14 起适用于 ext4（仅针对基于范围区的文件）和 XFS。

`-V, --version`

显示版本信息并退出。

`-h, --help`

显示帮助文本并退出。

## AUTHORS

Eric Sandeen

Karel Zak

## SEE ALSO

`fallocate(2)`、`posix_fallocate(3)`、`truncate(1)`

## AVAILABILITY

`fallocate`命令是 util-linux 软件包的一部分，可在 Linux Kernel Archive 获取。

# FC-CACHE

## NAME

`fc-cache` - 构建字体信息缓存文件

## SYNOPSIS

`fc-cache` [`-EfrsvVh`] [`--error-on-no-fonts`] [`--force`] [`--really-force`] [[`-y` `dir`] [`--sysroot` `dir`]] [`--system-only`] [`--verbose`] [`--version`] [`--help`] [`dir...`]

## DESCRIPTION

`fc-cache`扫描系统上的字体目录，并为使用 fontconfig 处理字体的应用程序构建字体信息缓存文件。

如果没有提供目录参数，`fc-cache`将使用当前字体配置中的每个目录。对每个目录进行扫描以寻找 FreeType 可读的字体文件。将创建一个包含每个字体属性及其关联文件名的缓存。该缓存用于在运行 fontconfig 库时加速应用程序的启动。

注意，`fc-cache`必须每种架构执行一次，以生成针对该架构定制的字体信息。

## OPTIONS

此程序遵循标准的 GNU 命令行语法，长选项以两个横杠（`--`）开头。下包含了选项摘要。

`-E`



如果`dir`中没有字体，或者在未提供目录时配置中没有目录，则报错。

`-f`

强制重新生成看似最新的缓存文件，覆盖时间戳检查。

`-r`

删除所有现有缓存文件并重新扫描。

`-s`

仅扫描系统级目录，忽略位于用户主目录下的位置。

`-v`

在忙碌时显示状态信息。

`-y`

在所有扫描路径前加上`dir`。

`-h`

显示选项摘要。

`-V`

显示程序版本并退出。

`dir`

用于扫描字体的目录。

## RETURN CODES

如果缓存成功生成，`fc-cache`返回 0；否则返回非零值值。

## FILES

`%cachedir%/*-%arch%.cache-%version%`

这些文件由`fc-cache`生成，包含从文件名到字体属性的映射。`fontconfig`库在应用程序启动时读取这些文件以定位合适的字体。

## SEE ALSO

`fc-cat`(1)、`fc-list`(1)、`fc-match`(1)、`fc-pattern`(1)、`fc-query`(1)、`fc-scan`(1)

`fontconfig`用户指南，HTML 格式：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

此手册页由 Keith Packard <keithp@keithp.com> 和 Josselin Mouette <joss@debian.org> 编写。

# FC-CAT

## NAME

`fc-cat` - 读取字体信息缓存文件

## SYNOPSIS

`fc-cat` [`-rvVh`] [`--recurse`] [`--verbose`] [`--version`] [`--help`]

[`fonts-cache-%version%-files`] [`dirs`] ...

## DESCRIPTION

`fc-cat`从缓存文件或字体目录读取字体信息并以 ASCII 形式输出。

## OPTIONS

此程序遵循标准的 GNU 命令行语法，长选项以两个横杠（`--`）开头。下包含了选项摘要。

`-r`

递归进入子目录。

`-v`

详细输出。

`-h`

显示选项摘要。

`-V`

显示程序版本并退出。

## SEE ALSO

`fc-cache`(1)、`fc-list`(1)、`fc-match`(1)、`fc-pattern`(1)、`fc-query`(1)、`fc-scan`(1)

`fontconfig`用户指南，HTML 格式：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

此手册页由 Patrick Lam <plam@mit.edu> 编写。

# FC-LIST

## NAME

`fc-list` - 列出字体

## SYNOPSIS

`fc-list` [`-vVh`] [`--verbose`] [`-f` `format`] [`--format` `format`] [`-q`]

## DESCRIPTION

`fc-list`列出系统中可字体。如果指定了元素，则打印这些元素。否则打印族和样式，除非请求详细输出。

## OPTIONS

此程序遵循标准的 GNU 命令行语法，长选项以两个横杠（`--`）开头。下包含了选项摘要。

`-v`

打印每个匹配的完整字体模式的详细输出，如果提供了`element`。

`-f`

根据格式规范`format`格式化输出。

`-q`

抑制所有普通输出。如果没有匹配的字体，返回错误码 1。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`pattern`

如果设置了此参数，则只显示匹配`pattern`的字体。

`element`

如果设置，则显示`element`属性。

## EXAMPLES

`fc-list`

列出所有字体。

`fc-list :lang=hi`

列出印地语的字体。

`fc-list : family style spacing`

列出每个字体的文件名和间距。“'是匹配所有字体的空模式。

## SEE ALSO

`fc-match`(1)、`FcFontList`(3)、`FcPatternFormat`(3)、`fc-cat`(1)、`fc-cache`(1)、`fc-pattern`(1)、`fc-query`(1)、`fc-scan`(1)

`fc-match`使用标准的`fontconfig`匹配规则匹配`pattern`（默认的空模式）以找到可用的最佳字体。如果给出`--sort`，则显示最佳匹配字体的排序列表。`--all`选项的作用与`--sort`类似，但它不会对字体列表进行任何裁剪。

如果指定了任何元素，则只打印这些元素。否则，将打印短文件名、族和样式，除非请求了详细输出。

## OPTIONS

本程序遵循通常的 GNU 命令行语法，长选项以两个横杠（`-`）开头。下文包含了选项的摘要。

`-a`

显示最佳匹配字体的排序列表，但不对该列表进行任何裁剪。

`-s`

显示最佳匹配字体的排序列表。

`-v`

为每个匹配项打印整个字体模式的详细输出，或者如果提供了`element`，则打印该元素。

`-f`

根据格式指定符`format`格式化输出。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`pattern`

显示匹配`pattern`的字体（默认使用空模式）。

`element`

如果设置，则为匹配的字体显示`element`属性。

## SEE ALSO

`fc-list`(1)、`FcFontMatch`(3)、`FcFontSort`(3)、`FcPatternFormat`(3)、`fc-cat`(1)、`fc-cache`(1)、`fc-pattern`(1)、`fc-query`(1)、`fc-scan`(1)

## DESCRIPTION

HTML 格式的`fontconfig`用户指南：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

本手册页由 Patrick Lam <plam@csail.mit.edu> 更新。

# FC-PATTERN

## NAME

`fc-pattern` - 解析并显示模式

## SYNOPSIS

`fc-pattern` [`-cdVh`] [`--config`] [`--default`] [[`-f` `format`] [`--format` `format`]] [`--version`] [`--help`]

`pattern` [`element...`]

## DESCRIPTION

`fc-pattern`解析`pattern`（默认的空模式）并显示解析结果。如果给出`--config`，则在显示之前对模式进行配置替换。如果给出`--default`，则在显示之前对模式进行默认替换。

如果指定了任何元素，则只打印这些元素。

## OPTIONS

本程序遵循通常的 GNU 命令行语法，长选项以两个横杠（`-`）开头。下文包含了选项的摘要。

`-c`

对模式执行配置替换。

`-d`

对模式执行默认替换。

`-f`

根据格式指定符`format`格式化输出。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`pattern`

解析并显示`pattern`（默认使用空模式）。

`element`

如果设置，则为解析后的模式显示`element`属性。

## SEE ALSO

`FcNameParse`(3)、`FcConfigSubstitute`(3)、`FcDefaultSubstitute`(3)、`FcPatternPrint`(3)、`FcPatternFormat`(3)、`fc-cat`(1)、`fc-cache`(1)、`fc-list`(1)、`fc-match`(1)、`fc-query`(1)、`fc-scan`(1)

## DESCRIPTION

HTML 格式的`fontconfig`用户指南：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

# FC-QUERY

## NAME

`fc-query` - 查询字体文件

## SYNOPSIS

`fc-query` [`-Vh`] [[`-b`] [`--ignore-blanks`]] [[`-i` `index`] [`--index` `index`]] [[`-f` `format`] [`--format` `format`]] [`--version`] [`--help`] `font-file...`

## DESCRIPTION

`fc-query`使用标准的`fontconfig`规则查询`font-file`，并为找到的每个字面打印字体模式。如果给出`--index`，则查询每个文件的一个字面，否则查询所有字面。

## OPTIONS

本程序遵循通常的 GNU 命令行语法，长选项以两个横杠（`-`）开头。下文包含了选项的摘要。

`-b`

忽略空格以计算语言。

`-i`

仅查询每个文件中索引为`index`的字面。

`-f`

根据格式指定符`format`格式化输出。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`font-file`

查询`font-file`的字面。

## RETURN CODES

`fc-query`成功解析返回错误代码 0，如果至少有一个字体字面无法打开，则返回 1。

## SEE ALSO

`fc-scan`(1)、`FcTypeQuery`(3)、`FcPatternFormat`(3)、`fc-cat`(1)、`fc-cache`(1)、`fc-list`(1)、`fc-match`(1)、`fc-pattern`(1)

## DESCRIPTION

HTML 格式的`fontconfig`用户指南：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

# FC-SCAN

## NAME

`fc-scan` - 扫描字体文件或目录

## SYNOPSIS

`fc-scan` [`-Vbh`] [`-b`] [`--ignore-blanks`] [`-f` `format`] [`--format` `format`] [`--version`] [`--help`] `file...`

## DESCRIPTION

`fc-scan`递归扫描`file`并为找到每个字面打印字体模式。

## OPTIONS

本程序遵循通常的 GNU 命令行语法，长选项以两个横杠（`-`）开头。下文包含了选项的摘要。

`-b`

忽略空格以计算语言。

`-f`

根据格式指定符`format`格式化输出。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`file`

递归扫描`file`的字面。

## RETURN CODES

`fc-scan`如果找到字面则返回 0，否则返回 1。

## SEE ALSO

`fc-query`(1)、`FcFileQuery`(3)、`FcPatternFormat`(3)、`fc-cat`(1)、`fc-cache`(1)、`fc-list`(1)、`fc-match`(1)、`fc-pattern`(1)

HTML 格式的`fontconfig`用户指南：`/usr/share/doc/fontconfig/fontconfig-user.html`。

## AUTHOR

本手册页由 Akira TAGOH <akira@tagoh.org> 更新。

# FC-VALIDATE

## NAME

`fc-validate` - 验证字体文件

## SYNOPSIS

`fc-validate` [`-Vhv`] [`-i` `index`] [`--index` `index`] [`-l` `lang`] [`--lang` `lang`] [`--verbose`] [`--version`] [`--help`] `font-file...`

## DESCRIPTION

`fc-validate`根据`fontconfig`文件验证`font-file`是否满足语言覆盖。如果给出`--index`，则验证每个文件的一个字面，否则验证所有字面。

## OPTIONS

本程序遵循通常的 GNU 命令行语法，长选项以两个横杠（`-`）开头。下文包含了选项的摘要。

`-i`

仅查询每个文件中索引为`index`的字面。

`-l`

设置`lang`为语言而非当前区域。这用于`-m`。

`-v`

显示更详细的信息。

`-V`

显示程序版本并退出。

`-h`

显示选项摘要。

`font-file`

查询`font-file`的字面。

## RETURN CODES

`fc-validate`成功解析返回错误代码 0，如果至少有一个字体字面无法打开，则返回 1。

## AUTHOR

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

# FGCONSOLE

## NAME

`fgconsole` - 打印活动 VT 的编号

## SYNOPSIS

`fgconsole` [`--help`|`--version`|`--next-available`]

## DESCRIPTION

如果活动虚拟终端是`/dev/ttyN`，则在标准输出上打印`N`。

如果控制台是串口控制台，则打印 `"serial"`。

`--next-available`

显示未分配的虚拟终端。通常分配 6 个虚拟终端，数字 7 用于 X；在这种情况下将返回 `"8"`。

### NOTES

在`devfs`下，控制台位于`/dev/vc/N`。`devfsd`可能会为了兼容性维护软链接。

## SEE ALSO

`chvt`(1)。

# GREP

## NAME

`grep`、`egrep`、`fgrep` - 打印匹配模式的行

## SYNOPSIS

`grep` [`OPTIONS`] `PATTERN` [`FILE`...]

`grep` [`OPTIONS`] [`-e` `PATTERN` | `-f` `FILE`] [`FILE`...]

## DESCRIPTION

`grep`在指定的输入文件`FILE`中搜索包含给定`PATTERN`匹配项的行。如果没有指定文件，或者提供了文件`-`，`grep`将搜索标准输入。默认情况下，`grep`会打印匹配的行。

此外，变体程序`egrep`和`fgrep`分别相当于`grep -E`和`grep -F`。这些变体已弃用，但为了向后兼容仍然提供。

## OPTIONS

### 通用程序信息

`--help`

输出用法信息并退出。

`-V`、`--version`

输出`grep`的版本号并退出。

### 匹配器选择

`-E`、`--extended-regexp`

将`PATTERN`解释为扩展正则表达式（ERE，见下文）。

`-F`、`--fixed-strings`

将`PATTERN`解释为由换行符分隔的固定字符串列表，其中任何一个字符串都将被匹配。

`-G`、`--basic-regexp`

将`PATTERN`解释为基础正则表达式（BRE，见下文）。这是默认选项。

`-P`、`--perl-regexp`

将`PATTERN`解释为 Perl 正则表达式。这是高度实验性的，`grep -P`可能会对未实现的功能警告。

### 匹配控制

`-e` `PATTERN`、`--regexp=PATTERN`

使用`PATTERN`作为模式。这可以指定多个搜索模式，或用于保护以连字符（`-`）开头的模式。

`-f` `FILE`、`--file=FILE`

从`FILE`获取模式，每行一个。空文件包含零模式，因此不匹配任何内容。

`-i`、`--ignore-case`

忽略`PATTERN`和输入文件中的大小写区别。

`-v`、`--invert-match`

反转匹配意义，选择不匹配的行。

`-w`、`--word-regexp`

仅选择包含完整单词匹配项的行。测试标准是匹配的字符串必须位于行首，或者由一个非单词组成字符引导。同样，它必须位于行尾，或者由一个非单词组成字符跟随。单词组成字符是字母、数字和下划线。

`-x`、`--line-regexp`

仅选择完全匹配整行的匹配项。

`-y`

`-i`的过时同义词。

### 通用输出控制

`-c`、`--count`

抑制正常输出；而是打印每个输入文件的匹配行数。配合`-v`、`--invert-match`选项（见下文），则计算不匹配行数。

`--color`[`=WHEN`]、`--colour`[`=WHEN`]

在匹配的（非空）字符串、匹配行、上下文行、文件名、行号、字节偏移和分隔符（针对字段和上下文行组）周围加上转义序列，以便在终端上以颜色显示。颜色由环境变量`GREP_COLORS`定义。已弃用的环境变量`GREP_COLOR`仍然受支持，但其设置没有优先级。`WHEN`为`never`、`always`或`auto`。

`-L`、`--files-without-match`

抑制正常输出；而是打印通常不会输出内容的每个输入文件的名称。扫描将在第一个匹配项处停止。

`-l`、`--files-with-matches`

抑制正常输出；而是打印通常输出内容的每个输入文件的名称。扫描将在第一个匹配项处停止。



`-m` `NUM`, `--max-count=NUM`

在读取 `NUM` 行匹配行后停止文件。如果输入是来自普通文件的标准输入，且输出了 `NUM` 行匹配行，`grep` 确保标准输入定位在最后一条匹配行之后再退出，无论是否存在后续上下文行。这允许调用进程恢复搜索。当 `grep` 在输出 `NUM` 行匹配行后停止时，它会输出任何后续上下文行。当同时使用 `-c` 或 `--count` 选项时，`grep` 输出的计数不会大于 `NUM`。当同时使用 `-v` 或 `--invert-match` 选项时，`grep` 在输出 `NUM` 行不匹配行后停止。

`-o`, `--only-matching`

仅打印匹配行中的匹配（非空）部分，每个部分单独占一个输出行。

`-q`, `--quiet`, `--silent`

静静模式；不向标准输出写入任何内容。如果发现任何匹配，则立即以零状态退出，即使检测到错误。另见 `-s` 或 `--no-messages` 选项。

`-s`, `--no-messages`

抑制关于不存在或不可读文件的错误信息。

### 输出行前缀控制

`-b`, `--byte-offset`

在输出的每一行之前打印从 0 开始的字节偏移。如果指定了 `-o`（`--only-matching`），则打印匹配部分本身的偏移。

`-H`, `--with-filename`

为每个匹配打印文件名。当有多个文件需要搜索时，这是默认值。

`-h`, `--no-filename`

抑制输出上的文件名前缀。当只有一个文件（或只有标准输入）需要搜索时，这是默认值。

`--label=LABEL`

将实际来自标准输入的内容显示为来自 `LABEL`。这对于像 `gzip -cd foo | grep --label=foo -H something` 的工具很有用。

`-n`, `--line-number`

在每个输出行前加上从 1 开始的号。

`-T`, `--initial-tab`

确保内容的第一个字符位于制表位上，以便制表符对齐看起来正常。这对于输出前带有最小尺寸字段的选项有用。

`-u`, `--unix-byte-offsets`

报告 Unix 风格的偏移。此开关使 `grep` 像文件是 Unix 风格文本文件一样报告字节偏移，即删掉 CR。除非也使用 `-b` 选项，否则此选项不起作用；在 MS-DOS 和 MS-Windows 以外的平台上不起作用。

`-Z`, `--null`

输出零字节（ASCII `NUL` 字符）而不是通常跟随文件名的字符。例如，`grep -lZ` 在每个文件后输出一个零字节。此选项使得输出在文件名包含换行符的情况下无歧义。此选项可以配合 `find -print0`、`perl -0`、`sort -z` 和 `xargs -0` 等命令处理任意文件名，即使是包含换行符的文件。

### 上下行控制

`-A` `NUM`, `--after-context=NUM`

在匹配行之后打印 `NUM` 行后续上下文。在连续匹配组之间放置包含组分隔符（在 `--group-separator` 下描述）的行。在使用 `-o` 或 `--only-matching` 选项时，此不起作用并给出警告。

`-B` `NUM`, `--before-context=NUM`

在匹配行之前打印 `NUM` 行前上下文。在连续匹配组之间放置包含组分隔符（在 `--group-separator` 下描述）的行。在使用 `-o` 或 `--only-matching` 选项时，此不起作用并给出警告。

`-C` `NUM`, `-NUM`, `--context=NUM`

打印 `NUM` 行输出上下文。在连续匹配组之间放置包含组分隔符（在 `--group-separator` 下描述）的行。在使用 `-o` 或 `--only-matching` 选项时，此不起作用并给出警告。

`--group-separator=SEP`

使用 `SEP` 作为组分隔符。默认情况下 `SEP` 为双连字符（`--`）。

`--no-group-separator`

使用空字符串作为组分隔符。

### 文件和目录选择

`-a`, `--text`

将二进制文件作为文本处理；这等同于 `--binary-files=text` 选项。

### `--binary-files=TYPE`

如果文件的前几个字节指示该文件包含二进制数据，则假设文件类型为 `TYPE`。默认情况下，`TYPE` 为 `binary`，`grep` 通常会输出一条消息显示二进制文件已匹配，或者在没有匹配项时不输出任何消息。如果 `TYPE` 为 `without-match`，`grep` 假设二进制文件不匹配；这等同于 `-I` 选项。如果 `TYPE` 为 `text`，`grep` 将二进制文件视为文本处理；这等同于 `-a` 选项。警告：`grep --binary-files=text` 可能会输出二进制垃圾，如果输出到终端且终端驱动程序将某些内容解释为命令，可能会产生严重的副作用。

### `-D ACTION`, `--devices=ACTION`

如果输入文件是设备、FIFO 或套接字，则使用 `ACTION` 来处理它。默认情况下，`ACTION` 为 `read`，这意味着像读取普通文件一样读取设备。如果 `ACTION` 为 `skip`，则静默跳过设备。

### `-d ACTION`, `--directories=ACTION`

如果输入文件是目录，则使用 `ACTION` 来处理它。默认情况下，`ACTION` 为 `read`，即像读取普通文件一样读取目录。如果 `ACTION` 为 `skip`，则静默跳过目录。如果 `ACTION` 为 `recurse`，则递归读取每个目录下的所有文件，仅当符号链接位于命令行上时才遵循该链接。这等同于 `-r` 选项。

### `--exclude=GLOB`

跳过文件名匹配 `GLOB`（使用通配符匹配）的文件。文件名 glob 可以使用 `*`、`?` 和 `[...]` 作为通配符，并使用 `\` 来转义通配符或反斜符字符。

### `--exclude-from=FILE`

跳过文件名匹配从 `FILE` 读取的任何文件名 glob 的文件（使用 `--exclude` 中描述的通配符匹配）。

### `--exclude-dir=DIR`

在递归搜索中排除匹配模式 `DIR` 的目录。

### `-I`

像处理不包含匹配数据的二进制文件一样处理二进制文件；这等同于 `--binary-files=without-match` 选项。

### `--include=GLOB`

仅搜索文件名匹配 `GLOB` 的文件（使用 `--exclude` 中描述的通配符匹配）。

### `-r`, `--recursive`

递归读取每个目录下的所有文件，仅当符号链接位于命令行上时才遵循该链接。注意，如果没有给出文件操作数，`grep` 将搜索工作目录。这等同于 `-d recurse` 选项。

### `-R`, `--dereference-recursive`

递归读取每个目录下的所有文件。与 `-r` 不同，它遵循所有的符号链接。

### 其他选项

### `--line-buffered`

在输出上使用行缓冲。这可能会导致性能损失。

### `-U`, `--binary`

将文件视为二进制文件。默认情况下，在 MS-DOS 和 MS-Windows 下，`grep` 通过查看从文件中读取的前 32KB 内容来猜测文件类型。如果 `grep` 认为文件是文本文件，它将剥离原始文件内容中的 CR 字符（以便带有 `^` 和 `$` 的正则表达式能够正常工作）。指定 `-U` 将覆盖此猜测，导致所有文件按原样读取并传递给匹配机制；如果文件是每行末尾带有 CR/LF 对的文本文件，这将导致某些正则表达式失效。此选项对 MS-DOS 和 MS-Windows 以外的平台无效。

### `-z`, `--null-data`

将输入视为一组行，每行由零字节（ASCII `NUL` 字符）而不是换行符结束。类似于 `-Z` 或 `--null` 选项，此选项可配合 `sort -z` 等命令处理任意文件名。

## 正则表达式

正则表达式是描述字符串集合的模式。正则表达式的构造类似于算术表达式，通过使用各种运算符组合较小的表达式。

`grep` 理解三种不同的正则表达式语法：`basic`（基础）、`extended`（扩展）和 `perl`。在 GNU `grep` 中，基础语法和扩展语法在可用功能上没有区别。在其他实现中，基础正则表达式的功能较弱。以下描述适用于扩展正则表达式；基础正则表达式的差异在后文总结。Perl 正则表达式提供了额外功能，并在 `pcresyntax(3)` 和 `pcrepattern(3)` 中记录，但在每个系统上可能可用。

基础构建块是匹配单个字符的正则表达式。大多数字符（包括所有字母和数字）都是匹配自身的正则表达式。任何具有特殊含义的元字符都可以通过在其前面加反斜杠来转义。

点 `.` 匹配任何单个字符。

### 字符类和括号表达式

括号表达式（bracket expression）是位于 `[` 和 `]` 包围的字符列表。它匹配列表中的任何单个字符；如果列表的第一个字符是脱字符 `^`，则匹配列表中不在的任何字符。例如，正则表达式 `[0123456789]` 匹配任何单个数字。

在括号表达式内部，范围表达式（range expression）由由连字符分隔的两个字符组成。它匹配两个字符之间排序的任何单个字符（包含边界），使用本地化（locale）的排序序列和字符集。例如，在默认的 C 语言设置中，`[a-z]` 匹配任何小写字母。

### 括号表达式细节

大多数元字符在括号表达式内部会失去它们的特殊含义。要包含字面量 `]`，请将其放在列表的第一位。同样，要包含字面量 `^`，请将其放在非首位置。最后，要包含字面量 `-`，请将其放在最后。

### 锚定

脱字符 `^` 和美元符号 `$` 是元字符，分别匹配行开头和结尾的空字符串。

### 反斜符字符和特殊表达式

符号 `\<` 和 `\>` 分别匹配单词开头和结尾的空字符串。符号 `\b` 匹配单词边缘的空字符串，而 `\B` 则在不是单词边缘时匹配空字符串。符号 `\w` 是 `[:alnum:]` 的同义词，`\W` 是 `[^[:alnum:]]` 的同义词。

### 重复

正则表达式可以跟随几种重复运算符之一：

`?`

前面的项是可选的，最多匹配一次。

`*`

前面的项将被匹配零次或多次。

`+`

前面的项将被匹配一次或多次。

`{n}`

前面的项恰好匹配 `n` 次。

`{n,}`

前面的项将匹配 `n` 次或更多。

`{,m}`

前面的项最多匹配 `m` 次。这是 GNU 的扩展功能。

`{n,m}`

前面的项将至少匹配 `n` 次，但不超过 `m` 次。

### 拼接

两个正则表达式可以拼接；生成的正则表达式匹配由两个子字符串拼接而成的任何字符串，这两个子字符串分别匹配所拼接的表达式。

### 选替

两个正则表达式可以通过中缀运算符 `|` 组合；生成的正则表达式匹配匹配任一交替表达式的任何字符串。

### 优先级

重复的优先级高于拼接，而拼接的优先级高于交替。整个表达式可以用括号括起来以覆盖这些优先级规则并形成一个子表达式。

### 反引用和子表达式

反引用 `\n`（其中 `n` 是单个数字）匹配正则表达式中之前匹配的第 `n` 个括号子表达式的子字符串。

### 基础正则表达式与扩展正则表达式

在基础正则表达式中，元字符 `?`、`+`、`{`、`|`、`(` 和 `)` 失去它们的特殊含义；相反应使用反斜杠版本 `\?`、`\+`、`\{`、`\|`、`\(` 和 `\)`。

## 环境变量

`grep` 的行为受到环境变量的影响。

类别 `LC_*foo` 的语言区域（locale）通过按顺序检查三个环境变量 `LC_ALL`、`LC_*foo` 和 `LANG` 来指定。这些变量中第一个设置的变量指定语言区域。例如，如果 `LC_ALL` 未设置，但 `LC_MESSAGES` 被设置为 `pt_BR`，则 `LC_MESSAGES` 类别使用巴西葡萄牙语语言区域。如果这些环境变量都没有设置、语言区域目录未安装，或者 `grep` 编译时没有启用语言支持（NLS），则使用 C 语言区域。

### `GREP_OPTIONS`

此变量指定了放在任何显式选项之前的默认选项。由于这在编写可移植脚本时会导致问题，此功能将在未来的 `grep` 版本中移除，`grep` 在使用时会警告。请使用别名或脚本。

### `GREP_COLOR`

此变量指定用于高亮匹配（非空）文本的颜色。它已被弃用并由 `GREP_COLORS` 代替，但仍然受支持。`GREP_COLORS` 的 `mt`、`ms` 和 `mc` 功能优先级高于它。它只能指定高亮任何匹配行中匹配非空文本的颜色（当省略 `-v` 命令行选项时为选定行，当指定 `-v` 时为上下文行）。默认值为 `01;31`，意味着在终端的默认背景上显示粗体红色前景文本。

### `GREP_COLORS`

指定用于高亮输出不同部分的颜色和其他属性。其值是一个由冒号分隔的功能列表，默认值是 `ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36`，其中省略了 `rv` 和 `ne` 布尔功能（即为 false）。支持的功能如下。

#### `sl=`

针对整个选定行的 SGR 子字符串（即当省略 `-v` 命令行选项时为匹配行，当指定 `-v` 时为非匹配行）。然而，如果同时指定了布尔功能 `rv` 和 `-v` 命令行选项，它将应用于匹配的上下文行。默认值为空（即终端的默认颜色对）。

#### `cx=`

针对整个上下文行的 SGR 子字符串（即当省略 `-v` 命令行选项时为非匹配行，当指定 `-v` 时为匹配行）。然而，如果同时指定了布尔功能 `rv` 和 `-v` 命令行选项，它将应用于选定的非匹配行。默认值为空（即终端的默认颜色对）。

#### `rv`

布尔值，在指定 `-v` 命令行选项时反转（交换）`sl=` 和 `cx=` 功能的含义。默认 false（即省略该功能）。

#### `mt=01;31`

针对任何匹配行中匹配非空文本的 SGR 子字符串（即当省略 `-v` 命令行选项时为选定行，当指定 `-v` 时为上下文行）。设置此项等于同时将 `ms=` 和 `mc=` 设置为相同的值。默认值是在当前行背景上的粗体红色文本前景。

#### `ms=01;31`

针对选定行中匹配非空文本的 SGR 子字符串。（这仅在省略 `-v` 命令行选项时使用）。当此项生效时，`sl=`（或如果 `rv` 则为 `cx=`）的功能保持激活。默认值是在当前行背景上的粗体红色文本前景。

#### `mc=01;31`

针对上下文行中匹配非空文本的 SGR 子字符串。（这仅在指定 `-v` 命令行选项时使用）。当此项生效时，`cx=`（或如果 `rv` 则为 `sl=`）的功能保持激活。默认值是在当前行背景上的粗体红色文本前景。

#### `fn=35`

位于任何内容行之前的文件名 SGR 子字符串。默认值是在终端默认背景上的洋红色文本前景。

#### `ln=32`

位于任何内容行之前的行号 SGR 子字符串。默认值是在终端默认背景上的绿色文本前景。

#### `bn=32`

位于任何内容行之前的字节偏移 SGR 子字符串。默认值是在终端默认背景上的绿色文本前景。

#### `se=36`

针对选定行字段之间（`:`）、上下文行字段之间（`-`）以及当指定非零上下文（`--`）时相邻行之间的分隔符的 SGR 子字符串。默认是在终端背景上的青色文本前景。

#### `ne`

布尔值，在每次颜色项目结束时使用行尾清除（EL，`\33[K`）来防止清空。这对于不支持 EL 的终端是需要的。否则，对于没有 `back_color_erase`（`bce`）terminfo 属性、所选高亮颜色不影响背景或 EL 速度过慢导致过多闪烁的终端是有用的。默认值为 false（即省略该功能）。

注意布尔功能没有 `=` 部分。它们默认被省略（即为 false），在指定时变为 true。

请参所用文本终端文档中的选择图形渲染（SGR）章节，了解允许的值及其作为字符属性的含义。这些子字符串值为十进制表示的整数，并可以用分号连接。`grep` 负责将结果组成为完整的 SGR 序列（`\33[...m`）。常用的连接值包括 `1`（粗体）、`4`（下划线）、`5`（闪烁）、`7`（反色）、`39`（默认前景色）、`30` 到 `37`（前景色）、`90` 到 `97`（16 色模式）、`38;5;0` 到 `38;5;255`（88 色和 256 色模式）、`49`（默认背景色）、`40` 到 `47`（背景色）、`100` 到 `107`（16 色模式背景色）以及 `48;5;0` 到 `48;5;255`（88 色和 256 色模式背景色）。



`LC_ALL`、`LC_COLLATE`、`LANG` 这些变量指定 `LC_COLLATE` 类的区域设置，该设置决定了用于解释如 `[a-z]` 等范围表达式的排序顺序。

`LC_ALL`、`LC_CTYPE`、`LANG` 这些变量指定 `LC_CTYPE` 类的区域设置，它决定了字符类型，例如哪些字符是空白字符。

`LC_ALL`、`LC_MESSAGES`、`LANG` 这些变量指定 `LC_MESSAGES` 类的区域设置，决定了 `grep` 用于消息的语言。默认的 C locale 使用美国英语消息。

`POSIXLY_CORRECT` 如果设置，`grep` 将按照 POSIX 要求运行；否则，`grep` 的行为更像其他 GNU 程序。POSIX 要求跟在文件名后面的选项必须视为文件名；默认情况下，此类选项会被移动到操作列表的前端并被视为选项。此外，POSIX 要求将未识别的选项诊断为“非法的”（illegal），但由于它们并没有违反法律，默认是将它们诊断为“无效的”（invalid）。`POSIXLY_CORRECT` 还会禁用下文描述的 `N_GNU_nonoption_argv_flags_`。

`N_GNU_nonoption_argv_flags_`（此处 `N` 是 `grep` 的数字进程 ID）。如果此环境变量值的第 `i` 个字符为 `1`，则不将 `grep` 的第 `i` 个操作视为选项，即使它看起来像选项。shell 可以在运行每个命令时设置此变量，指定哪些操作是文件名通配符扩展的结果，因此不应被视为选项。此行为仅适用于 GNU C，且仅在未设置 `POSIXLY_CORRECT` 时可用。

## 退出状态

通常情况下，如果选择了行，退出状态为 0；如果没有选中行，状态为 1；如果发生错误，状态为 2。然而，如果使用了 `-q`、`--quiet` 或 `--silent` 且选择了行，即使发生了错误，退出状态也为 0。

## 版权

Copyright 1998-2000, 2002, 2005-2014 Free Software Foundation, Inc.

这是一个自由软件；请查看源代码以获取复制条件。不提供任何担保，即使是针对商业性或针对特定用途的担保。

## 缺陷

### 报告缺陷

将错误报告发送电子邮件至错误报告地址 `<email: bug-grep@gnu.org >`。提供邮件存档 `<URL: http://lists.gnu.org/mailman/listinfo/bug-grep >` 和缺陷跟踪器 `<URL: http://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep >`。

### 已知缺陷

`{n,m}` 结构中大量的重复计数可能会导致 `grep` 使用大量内存。此外，某些其他晦涩的正则表达式需要指数级的时间空间，可能会导致 `grep` 内存耗尽。后向引用非常慢，可能需要指数级的时间。

## 相关

### 常规手册页

`awk(1)`、`cmp(1)`、`diff(1)`、`find(1)`、`gzip(1)`、`perl(1)`、`sed(1)`、`sort(1)`、`xargs(1)`、`zgrep(1)`、`read(2)`、`pcre(3)`、`pcresyntax(3)`、`pcrepattern(3)`、`terminfo(5)`、`glob(7)`、`regex(7)`。

### POSIX 程序员手册页

`grep(1p)`。

### 完整文档

提供完整的手册 `<URL: http://www.gnu.org/software/grep/manual/ >`。如果你的站点正确安装了 `info` 和 `grep` 程序，执行命令：

`info grep`

应该可以让你访问完整手册。

## 注意事项

本 man 手页的维护并不频繁；完整文档通常更新更新。

***

# 文件

## 名称

`file` - 确定文件类型

## 语法概要

- `words [-bcEhiklLNnprsvz0] [--apple] [--mime-encoding] [--mime-type] [-e testname] [-F separator] [-f namefile] [-m magicfiles] [-P name=value] file ...`
- `-C [-m magicfiles] [--help]`

## 描述

本手册页记录了该命令的 5.22 版本。

尝试对每个参数进行分类。有三组测试按此顺序执行：文件系统测试、魔数测试（magic tests）和语言测试。第一个通过的测试将打印文件类型。

打印的类型通常包含以下词之一：`text`（文件仅包含打印字符和一些常见的控制字符，可能在 `ASCII` 终端上读取是安全的）、`executable`（文件包含以某些 `UNIX` 内核或其他可理解的形式编译的程序结果）或 `data`（意味着其他任何内容，数据通常是“二进制的”或不可打印的）。异常情况是常见的已知格式（核心文件、tar 存档），它们已知包含二进制数据。在修改魔数文件或程序本身时，请确保保留这些关键字。用户依赖此点。

文件系统测试基于 `stat(2)` 系统调用。程序会检查其是否为空、符号链接或管道（FIFOs）。

魔数测试用于检查特定类型的文件。识别这些文件的信息从编译后的文件 `/usr/share/misc/magic.mgc` 中读取。此外，如果存在 `$HOME/.magic.mgc`，它将优先于系统魔数文件。如果文件不匹配魔数文件中的任何项，则将检查其是否为文本文件。ASCII、ISO-8859-x、UTF-8、扩展 ASCII 和 EBCDIC 字符集可以通过构成打印文本的不同字节范围和序列来区分。如果文件通过了这些任何一个测试，将报告其字符集。ASCII、ISO-8859-x、UTF-8 和扩展 ASCII 文件被识别为“文本”，因为它们在几乎任何终端上都是可读的；UTF-16 和 EBCDIC 仅识别为“字符数据”，因为虽然它们包含文本，但文本需要翻译后才能读取。此外，尝试确定文本类型文件的其他特征。如果文件的行以 CR、CRLF 或 NEL 终止而不是 Unix 标准的 LF，将会被报告。包含转义序列或叠印的文件也将被识别。

一旦确定了文本类型文件中使用的字符集，将尝试确定文件是用什么语言编写的。语言测试寻找特定的字符串（参见 `names.h`），这些字符串可以出现在文件开头几块的任何位置。例如，关键字 `.br` 表示该文件可能是一个 `troff(1)` 输入文件，就像关键字 `struct` 表明这是一个 C 程序一样。这些测试比前两组不可靠，因此最后执行。语言测试例程还会测试一些杂项（如 `tar(1)` 存档）。

### 选项

#### `--apple`

使 `file` 命令输出旧版本 MacOS 中使用的文件类型和创建者代码。该代码由八个字母组成，第一个字母描述文件类型，后几个描述创建者。

#### `-b`、`--brief`

不在输出行前置文件名（简短模式）。

#### `-C`、`--compile`

写入一个 `magic.mgc` 输出文件，包含 magic 文件或目录的预解析版本。

#### `-c`、`--checking-printout`

对 magic 文件的解析形式进行输出。这通常与 `-m` 标志配合使用，在安装新的 magic 文件之前进行调试。

#### `-E`

发生文件系统错误（如文件未找到）时，不再按照 POSIX 强制将错误作为普通输出处理并继续，而是输出错误信息并退出。

#### `-e`、`--exclude testname`

在确定文件类型的测试列表中，排除名为 `testname` 的测试。有效的测试名称有：

##### `apptype`

`EMX` 类型（仅在 EMX 上可用）。

##### `ascii`

各种类型的文本文件（此测试将尝试猜测文本编码，无论 `encoding` 选项如何设置）。

##### `encoding`

用于软 magic 测试的不同文本编码。

##### `tokens`

为了向后兼容而被忽略。

##### `cdf`

打印复合文档文件（Compound Document Files）的细节。

##### `compress`

检查并查看压缩文件内部。

##### `elf`

打印 ELF 文件细节。

##### `soft`

查询 magic 文件。

##### `tar`

检查 tar 文件。

#### `-F`、`--separator separator`

使用指定的字符串作为文件名与返回的文件结果之间的分隔符。默认为 `:`。

#### `-f`、`--files-from namefile`

在参数列表之前，从 `namefile`（每行一个）读取要检查的文件名。必须存在 `namefile` 或至少一个文件名参数；要测试标准输入，请使用 `-` 作为文件名参数。请注意，当遇到此选项时，会解包 `namefile` 并处理其中包含的文件名，且在任何后续选项处理之前完成。这允许在同一次调用中使用不同的命令行参数处理多个文件列表。因此，如果你想设置分隔符，需要在指定文件列表之前进行设置，例如：`-F *@ -f namefile` 而不是：`-f namefile -F file ...`

#### `-h`、`--no-dereference`

该选项导致不跟随符号链接（在支持符号链接的系统上）。如果环境变量 `POSIXLY_CORRECT` 未定义，则这是默认值。

#### `-i`、`--mime`

使 `file` 命令输出 MIME 类型字符串，而不是传统的人类可读字符串。因此，它可能会输出 `text/plain; charset=us-ascii` 而不是 `ASCII text`。

#### `--mime-type`、`--mime-encoding`

类似于 `-i`，但仅打印指定的元素。

#### `-k`、`--keep-going`

不要在第一个匹配处停止，继续执行。后续匹配将带有前缀字符串 `\012-`。（如果你需要换行符，请参见 `-r` 选项）。强度最高的 magic 模式（参见 `-l` 选项）在前。

#### `-l`、`--list`

显示模式列表及其强度，按 magic(4) 强度降序排序，该强度用于匹配（另参见 `-k` 选项）。

#### `-L`、`--dereference`

该选项导致跟随符号链接，类似于 `ls(1)` 中的同名选项（在支持符号链接的系统上）。如果环境变量 `POSIXLY_CORRECT` 已定义，则默认如此。

#### `-m`、`--magic-file magicfiles`

指定包含 magic 的替代文件和目录列表。这可以是单个项目，也可以是冒号分隔的列表。如果在文件或目录旁边找到编译过的 magic 文件，则将使用它。

#### `-N`、`--no-pad`

不对文件名进行填充以便在输出中对齐。

#### `-n`、`--no-buffer`

强制在检查每个文件后刷新 stdout。这仅在检查文件列表时有用。适用于希望从管道获取文件类型输出的程序。

#### `-p`、`--preserve-date`

在支持 `utime(3)` 或 `utimes(2)` 的系统上，尝试保留所分析文件的访问时间，假装从未读取过它们。

#### `-P`、`--parameter name=value`

设置各种参数限制。

| 名称 | 默认值 | 说明 |
| :--- | ---: | :--- |
| `indir` | 15 | 间接 magic 的递归限制 |
| `name` | 30 | 名称/使用 magic 的计数限制 |
| `elf_notes` | 256 | 处理的 ELF note 最大值 |
| `elf_phnum` | 128 | 处理的 ELF 段最大值 |
| `elf_shnum` | 32768 | 处理的 ELF section 最大值 |

#### `-r`、`--raw`

不要将不可打印字符转换为 `\ooo`。通常情况下会将不可打印字符转换为其八进制表示。

#### `-s`、`--special-files`

通常，只尝试读取并确定 `stat(2)` 报告为普通文件的参数文件。这可以防止问题，因为读取特殊文件可能会产生特殊的后果。指定 `-s` 选项会导致也读取块或字符特殊文件的参数文件。这对于确定原始磁盘分区的数据文件系统类型有用。此选项还会忽略 `stat(2)` 报告的文件大小。

#### `-v`、`--version`

打印程序版本并退出。

#### `-z`、`--uncompress`

尝试查看压缩文件内部。

#### `-0`、`--print0`

文件名结束后输出空字符 `\0`。

#### `--help`

打印帮助信息并退出。

## FILES

`/usr/share/misc/magic.mgc`

默认编译 magic 列表。

`/usr/share/misc/magic`

包含 magic 文件的目录。

## ENVIRONMENT

环境变量 `MAGIC` 可用于设置默认 magic 文件。如果设置了该变量，会在其值后添加 `.mgc`。但文件必须存在才能被考虑。环境变量 `POSIXLY_CORRECT` 控制（在支持符号链接的系统上）是否尝试跟随符号链接。如果设置，则跟随，否则不。这也由 `-L` 和 `-h` 选项控制。

## SEE ALSO

`magic(5)`、`hexdump(1)`、`od(1)`、`strings(1)`

## STANDARDS CONFORMANCE

认为此程序超过了 System V 接口定义的 FILE(CMD)，根据其中包含的模糊语言所能确定的程度。它的行为与同名的 System V 程序基本兼容。然而，此版本知道更多 magic，因此在许多情况下会产生不同的（尽管更准确）输出。

此版本与 System V 的一个显著区别是，此版本将任何空白视为分隔符，因此模式字符串中的空格必须经过转义。例如，现有 magic 文件中的：

`>10 string language impress (imPRESS data)`

必须更改为：

`>10 string language\ impress (imPRESS data)`

此外，在此版本中，如果模式字符串包含反斜杠，则必须经过转义。例如，现有 magic 文件中的：

`0 string \begindata Andrew Toolkit document`

必须更改为：

`0 string \\begindata Andrew Toolkit document`

## MAGIC DIRECTORY

magic 文件条目收集自各种来源（主要是 USENET），由各作者贡献。Christos Zoulas（地址见下方）将收集额外的或修正的 magic 文件条目。定期发布 magic 文件条目的汇总。

magic 文件中条目的顺序非常重要。取决于你所使用的系统，它们组合的顺序可能是错误的。如果你的旧命令使用了 magic 文件，请保留旧的 magic 文件以备对比（将其重命名为 `/usr/share/misc/magic.orig`）。

## 示例

```text
$ file file.c file /dev/{wd0a,hda}
file.c: C program text
file: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), stripped
/dev/wd0a: block special (0/0)
/dev/hda: block special (3/0)

$ file -s /dev/wd0{b,d}
/dev/wd0b: data
/dev/wd0d: x86 boot sector

$ file -s /dev/hda{,1,2,3,4,5,6,7,8,9,10}
/dev/hda: x86 boot sector
/dev/hda1: Linux/i386 ext2 filesystem
/dev/hda2: x86 boot sector
/dev/hda3: x86 boot sector, extended partition table
/dev/hda4: Linux/i386 ext2 filesystem
/dev/hda5: Linux/i386 swap file
/dev/hda6: Linux/i386 swap file
/dev/hda7: Linux/i386 swap file
/dev/hda8: Linux/i386 swap file
/dev/hda9: empty
/dev/hda10: empty

$ file -i file.c file /dev/{wd0a,hda}
file.c: text/x-c
file: application/x-executable
/dev/hda: application/x-not-regular-file
/dev/wd0a: application/x-not-regular-file
```

## 历史

至少从研究版本 4 以来，每个 UNIX 系统都有这个命令（man 手页日期为 1973 年 11 月）。System V 版本引入了一个重大的主要变化：magic 类型的外部列表。这让程序运行稍微变慢，但使其变得灵活得多。

该程序基于 System V 版本，由 Ian Darwin (`aq@darwinsys.com`) 在没有查看任何其他人源代码的情况下编写。

John Gilmore 对代码进行了大量修订，使其比第一个版本更好。Geoff Collyer 发现了几处缺陷并提供了一些 magic 文件条目。Rob McMahon 对 `&` 运算符的贡献（`aq cudcv@warwick.ac.uk`，1989 年）。

Guy Harris (`aq guy@netapp.com`) 从 1993 年至今进行了许多更改。1989 年。

从 1990 年至今由 Christos Zoulas (`aq christos@astron.com`) 进行主要的开发和维护。



Chris Lowth (`chris@lowth.com`) 于 2000 年修改：处理 `-i` 选项以输出 MIME 类型字符串，使用了备用的 magic 文件和内部逻辑。

Eric Fischer (`enf@pobox.com`) 于 2000 年 7 月修改，用于识别字符编码并尝试识别非 ASCII 文件的语言。

Reuben Thomas (`rrt@sc3d.org`) 于 2007-2011 年修改：改进 MIME 支持，合并 MIME 和非 MIME magic，支持目录以及 magic 文件，应用了许多错误修复，更新并修复了许多 magic，改进构建系统，改进文档，并用纯 Python 重写了 Python 绑定。

`magic` 目录（magic 文件）的贡献者列表太长，无法在此列出。你知道你们是谁；感谢。源文件中列出了许多贡献者。

## 法律声明

版权所有 (c) Ian F. Darwin, Toronto, Canada, 1986-1999。受标准伯克利软件发行版版权保护；请参源码发行包中的 `COPYING` 文件。

`tar.h` 和 `is_tar.c` 文件由 John Gilmore 根据其公有领域 `tar(1)` 程序编写，不受上述许可证的保护。

## 返回码

成功时返回 0，错误时返回非零。

如果 `file` 操作数指定的文件不存在、不可读取，或无法确定 `file` 操作数指定的文件类型，这不被视为影响退出状态的错误。

## Bug

请通过 http://bugs.gw.com/ 上的错误跟踪器报告 bug 并发送补丁，或通过邮件列表 `file@mx.gw.com`（先访问 http://mx.gw.com/mailman/list/file 订阅）。

## 待办

修复输出，使得 MIME 和 APPLE 标志的测试不需要到处都是，且实际输出只在一个地方完成。这需要一个设计。建议：将可能的输出推入列表，然后在最后选择最后一个推入的（人们希望是最具体的）值，或者在列表为空时使用默认值。这不应该减慢评估速度。

继续消除所有 magic bug。参阅 Debian BTS 以获取良好的来源。

存储任意长度的字符串（例如用于 `%s` 模式），以便它们可以打印出来。修复了 Debian bug #271672。需要在 apprentice 中更复杂的存储/加载代码。

添加当前层之后相对偏移的语法（Debian bug #466037）。

让 `file -ki` 工作，即提供多个 MIME 类型。

添加 zip 库以便我们可以查看内部内容。

## 可用

你可以通过 ftp.astron.com 的 `/pub/file-X.gz` 获取作者的最新版本。

---

# FIND-JAR

## 名称

find-jar - 查找 JAR 或目录

## 语法

`find-jar` JAR 或目录

## 描述

`find-jar` 命令测试指定的元素。如果成功，它将返回 JAR 或目录。此命令专门用于测试，不应用于脚本。

## 依赖

使用 `find-jar` 需要 `mvn-resolve` 可用。`find-jar` 的用户负责使其可用。

## 示例

`find-jar xpp3` 将输出 `/usr/share/java/xpp3.jar`。

`find-jar javamail` 将输出 `/usr/share/java/javail`。

## 报告 Bug

应通过 Red Hat Bugzilla http://bugzilla.redhat.com/ 报告。

## 参见

`build-classpath`(1), `build-jar-repository`(1), `mvn-resolve`(1)。

---

# FIND

## 名称

find - 在目录中搜索文件

## 语法

`find` [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...] [expression]

## 描述

本手册页文档 GNU 版本的 **find**。GNU **find** 搜索每个起始点的根目录树，从左到右评估给定的表达式（优先级规则见 OPERATORS 部分），直到结果已知（*and* 操作的左侧为假，*or* 操作为真），此时 **find** 继续处理下一个文件名。如果没有指定起始点，则假设为 `.`。

如果你在安全重要的环境中使用 **find**（例如，用它搜索其他用户可写入的目录），你应该阅读 findutils 文档中的“安全考虑”章节。该文档包含比本手册页更多的细节和讨论，因此你可能会发现它是更有用的来源。

### 选项

`-H`, `-L` 和 `-P` 选项控制符号链接的处理。这些选项之后的命令行参数被视为要检查的文件或目录名称，直到第一个以 `-` 开头的参数，或参数 `(` 或 `!`。该参数及其后的任何参数被视为描述搜索内容的表达式。如果没有提供路径，则使用当前目录。如果未提供表达式，则使用表达式 `-print`（但你可能应该考虑使用 `-print0`，无论如何）。

本手册页介绍了表达式列表中的 `options`。这些选项控制 `find` 的行为，但它们紧跟在最后一个路径名称之后指定。五个“真实”选项 `-H`、`-L`、`-P`、`-D` 和 `-O` 必须出现在第一个路径名称之前（如果存在的话）。也可以使用双横线 `--` 来指示任何剩余参数都不是选项（尽管如果你在起始点列表中使用通配符，确保所有起始点都以 `./` 或 `/` 开头通常更安全）。

#### `-P`

从不跟随符号链接。这是默认行为。当 `find` 检查或打印文件信息时，如果该文件是符号链接，所使用的信息应从符号链接本身的属性获取。

#### `-L`

跟随符号链接。当 `find` 检查或打印文件信息时，所使用的信息应从链接指向的文件的属性获取，而不是来自链接本身（除非链接是断开的符号链接或 `find` 无法检查链接所指向的文件）。使用此选项意味着隐含 `-noleaf`。如果你之后使用 `-P` 选项，`-noleaf` 仍然有效。如果 `-L` 效且 `find` 在搜索过程中发现指向子目录的符号链接，将搜索该符号链接指向的目录。

当 `-L` 选项有效时，`-type` 谓词将始终匹配符号链接指向的文件类型，而不是链接本身（除非符号链接是断开的）。使用 `-L` 会导致 `-lname` 和 `-ilname` 谓词始终返回假。

#### `-H`

不跟随符号链接，但在处理命令行参数除外。当 `find` 检查或打印文件信息时，所使用的信息应从符号链接本身的属性获取。此行为的唯一例外是当命令行上指定的文件是符号链接，且该链接可以解析。对于该情况，所使用的信息取自链接指向的任何内容（即跟随链接）。如果符号链接指向的文件无法检查，则使用链接本身的信息作为备选。如果 `-H` 有效且命令行上指定的路径之一指向目录的符号链接，则将检查该目录的内容（尽管当然，`-maxdepth 0` 会防止这种情况）。

如果指定了 `-H`、`-L` 和 `-P` 中的多个选项，每个选项都会覆盖其他；最后一个在命令行上出现的选项生效。由于 `-P` 是默认选项，除非指定了 `-H` 或 `-L`，否则应认为 `-P` 有效。

GNU `find` 在开始任何搜索之前，经常在处理命令行本身期间对文件进行统计。这些选项也会影响这些参数的处理方式。具体来说，有许多测试会将命令行上列出的文件与我们当前考虑的文件进行比较。在每情况下，命令行上指定的文件都将被检查，并且其某些属性将被保存。如果命名文件实际上是符号链接，且 `-P` 选项有效（或者既未指定 `-H` 也未指定 `-L`），则用于比较的信息将来自符号链接的属性。否则，将来自链接指向的文件属性。如果 `find` 无法跟随链接（例如因为权限不足或链接指向不存在的文件），则将使用链接本身的属性。

当 `-H` 或 `-L` 选项有效时，任何作为 `-newer` 参数列出的符号链接都将被引用，且时间戳将从符号链接指向的文件获取。同样的考虑也适用于 `-newerXY`、`-anewer` 和 `-cnewer`。

`-follow` 选项的效果与 `-L` 类似，但它在出现的地方生效（也就是说，如果没有使用 `-L` 但使用了 `-follow`，则命令行中 `-follow` 之后出现的任何符号链接将被引用，而在它之前的则不会）。

#### `-D debugoptions`

打印诊断信息；这有助于诊断为什么 `find` 没有按照你预期的方式运行。调试选项列表之间应用逗号隔开。findutils 版本之间不保证调试选项的兼容性。有关有效调试选项的完整列表，请参见 `find -D help` 的输出。有效的调试选项包括：

- `help`: 解释调试选项。

- `tree`: 显示原始形式和优化形式的表达式树。

- `stat`: 在使用 `stat` 和 `lstat` 系统调用检查文件时打印消息。`find` 程序会尽力减少此类调用。

- `opt`: 打印与表达式树优化相关的诊断信息；详见请参见 `-O` 选项。

- `rates`: 打印摘要，指示每个谓词成功或失败的频率。

#### `-Olevel`

启用查询优化。`find` 程序会重新排列测试以加快执行速度，同时保留整体效果；也就是说，具有副作用的谓词彼此之间不会被重排序。在每个优化级别执行的优化如下：

- `0`: 等同于优化级别 1。

- `1`: 这是默认优化级别，对应于传统行为。重新排列表达式，使得仅基于文件名的测试（例如 `-name` 和 `-regex`）首先执行。

- `2`: 任何 `-type` 或 `-xtype` 测试将在任何仅基于文件名的测试之后执行，但在任何需要 inode 的测试之前执行。在许多现代 Unix 版本中，文件类型由 `readdir()` 返回，因此这些谓词的评估速度比需要 stat 的谓词要快。如果你使用 `-fstype` *FOO* 谓词并指定了一个在 `find` 启动时未知（即不在 `/etc/mtab` 中）的文件类型，该谓词等同于 `-false`。

- `3`: 在此优化级别，启用完整的基于成本的优化器。测试顺序将被修改，使得廉价（即快速）的测试首先执行，昂贵的稍后执行。在每个成本区间内，根据谓词是否可能成功来决定早评估或后评估。对于 `-o`，可能成功的谓词更早评估；对于 `-a`，可能失败的谓词更早评估。

基于成本的优化器对任何给定测试成功的概率有一个固定的想法。在某些情况下，概率会考虑到测试的特定性质（例如，`-type f` 被认为比 `-type c` 更可能成功）。基于成本的优化器目前正在评估中。如果它没有提高 `find` 的性能，将被再次移除。相反，证明可靠、稳健且有效的优化可能会随着推移在较低的优化级别启用。然而，在 4.3.x 系列中默认行为（即优化级别 1）将不会改变。findutils 测试套会在每个优化级别运行 `find` 的所有测试，并确保结果一致。

## 表达式

表达式由选项（影响整体操作而非特定文件的处理，且始终返回真）、测试（返回真或假值）和动作（具有副作用并返回真或假值）组成，所有部分由运算符分隔。如果省略运算符，则假设为 `-and`。

如果表达式包含除 `-prune` 以外的动作，则对所有表达式为真的文件执行 `-print`。

所有选项始终返回 true。除 `-daystart`、`-follow` 和 `-regextype` 之外，选项会影响所有测试，包括在这些选项之前指定的测试。这是因为选项是在解析命令行时处理的，而测试在检查文件之前不会执行任何操作。`-daystart`、`-follow` 和 `-regextype` 选项在这方面有所不同，它们只对命令行中后出现的测试产生影响。因此，为了清晰起见，最好将它们放在表达式的开头。如果不这样做，系统会发出警告。

### -d

`-depth` 的同义词，为了兼容 FreeBSD、NetBSD、MacOS X 和 OpenBSD。

### -daystart

从今天开始测量时间（针对 `-amin`、`-atime`、`-cmin`、`-ctime`、`-mmin` 和 `-mtime`），而不是 24 小时前。此选项仅影响命令行中后出现的测试。

### -depth

在处理目录本身之前处理每个目录的内容。`-delete` 动作也隐含 `-depth`。

### -follow

已废弃；请改用 `-L` 选项。解析符号链接。隐含 `-noleaf`。`-follow` 选项仅影响命令行中在其之后的测试。除非指定了 `-H` 或 `-L` 选项，否则 `-follow` 选项的位置会改变 `-newer` 谓词的行为；如果作为 `-newer` 参数列出的文件是符号链接，它们将被解析。同样的考虑也适用于 `-newerXY`、`-anewer` 和 `-cnewer`。同样，`-type` 谓词将始终与符号链接指向的文件类型进行匹配，而不是链接本身。使用 `-follow` 会导致 `-lname` 和 `-ilname` 谓词始终返回 false。

### -help, --help

打印 `find` 命令行用法的摘要并退出。

### -ignore_readdir_race

通常情况下，当 `find` 无法 `stat` 一个文件时会输出错误消息。如果你提供此选项，并且文件在 `find` 从目录读取文件名到它尝试 `stat` 该文件之间之间被删除，则不会输出错误消息。这也适用于在命令行上指定的文件或目录。此选项在读取命令行时生效，这意味着你不能在开启此选项的情况下搜索文件系统的部分，而在关闭此选项的情况下搜索另一部分（如果你需要这样做，你需要执行两个 `find` 命令，一个带选项，一个不带）。

### -maxdepth *levels*

从起点向下最多进入 *levels*（一个非负整数）层目录。`-maxdepth 0` 意味着仅对起点本身应用测试和动作。

### -mindepth *levels*

对于小于 *levels*（一个非负整数）的层不应用任何测试或动作。`-mindepth 1` 意味着处理起点以外的所有文件。

### -mount

不要进入其他文件系统上的目录。`-xdev` 的替代名称，为了兼容某些其他版本的 `find`。

### -noignore_readdir_race

关闭 `-ignore_readdir_race` 的影响。

### -noleaf

不通过假设目录包含的子目录比其硬链接数少 2 个来优化。在搜索不遵循 Unix 目录链接标准的的文件系统时（例如 CD-ROM 或 MS-DOS 文件系统或 AFS 卷载挂载点），需要此选项。普通 Unix 文件系统上的每个目录至少有 2 个硬链接：它的名称和它的 `.` 条目。此外，它的子目录（如果有）每个都有一个链接该目录的 `..` 条目。当 `find` 检查目录时，在 `stat` 了比目录链接数少 2 个子目录后，它知道目录中剩余的条目是非目录（目录树中的 `leaf` 文件）。如果只需要检查文件名，则无需对它们进行 `stat`；这会显著提高搜索速度。

### -regextype *type*

更改命令行中稍后出现的 `-regex` 和 `-iregex` 测试所理解的正则表达式语法。目前实现的类型有：emacs（这是默认值）、posix-awk、posix-basic、posix-egrep 和 posix-extended。

### -version, --version

打印 `find` 的版本号并退出。

### -warn, -nowarn

开启或关闭警告消息。这些警告仅适用于命令行用法，不适用于 `find` 在搜索目录时可能遇到的任何条件。如果标准输入是 tty，默认行为对应于 `-warn`，否则对应于 `-nowarn`。

### -xautofs

不要进入 autofs 文件系统上的目录。

### -xdev

不要进入其他文件系统上的目录。

### TESTS

某些测试（例如 `-newerXY` 和 `-samefile`）允许当前正在检查的文件与命令行上指定的某些参考文件进行比较。当使用这些测试时，参考文件的解释由选项 `-H`、`-L` 和 `-P` 以及任何之前的 `-follow` 决定，但参考文件只在解析命令行时检查一次。如果无法检查参考文件（例如，`stat`(2) 系统调用对其失败），则会输出错误消息，`find` 以非零状态退出。数字参数可以指定为：

- `+n` 表示大于 `n`，

- `-n` 表示小于 `n`，

- `n` 表示正好等于 `n`。

#### -amin *n*

文件在 *n* 分前被访问。

#### -anewer *file*

文件访问的时间比 *file* 修改的时间晚。如果 *file* 是符号链接且 `-H` 选项或 `-L` 选项生效，则始终使用其指向的文件的访问时间。

#### -atime *n*

文件最后一次访问是在 *n*24 小时前。当 `find` 计算文件是在多少个 24 小时前被访问的，任何小数部分都会被忽略，因此为了匹配 `-atime +1`，文件必须至少在两天前被访问过。

#### -cmin *n*

文件的状态最后一次更改是在 *n* 分前。

#### -cnewer *file*

文件的状态更改的时间比 *file* 修改的时间晚。如果 *file* 是符号链接且 `-H` 选项或 `-L` 选项生效，则始终使用其指向的文件的状态更改时间。

#### -ctime *n*

文件的状态最后一次更改是在 *n*24 小时前。查看 `-atime` 的注释以理解舍入如何影响文件时间的解释。

#### -empty

文件为空且是普通文件或目录。

#### -executable

匹配可执行的文件和可搜索的目录（从文件名角度而言）。这考虑了访问控制列表以及 `-perm` 测试忽略的权限属性。

#### -false

始终为 false。

#### -fstype *type*



文件位于`type`类型的文件系统上。有效的文件系统类型在不同的 Unix 版本之间不同；在某些 Unix 版本上接受的文件系统类型的不完整列表：`ufs`、`4.2`、`4.3`、`nfs`、`tmp`、`mfs`、`S51K`、`S52K`。你可以使用`-printf`配合`%F`指令来查看文件系统的类型。

#### `-gid n`

文件的数字组 ID 为`n`。

#### `-group gname`

文件属于组`gname`（允许数字组 ID）。

#### `-ilname pattern`

类似于`-lname`，但匹配不区分大小写。如果`-L`选项或`-follow`选项生效，除非符号链接断开，否则此测试返回 false。

#### `-iname pattern`

类似于`-name`，但匹配时不区分大小写。例如，模式`'fo*'`和`'F??'`会匹配文件名`'Foo'`、`'FOO'`、`'foo'`、`'fOo'`等。模式`'*foo*'`也会匹配名为`fofoobar`的文件。

#### `-inum n`

文件的 inode 编号为`n`。通常使用`-samefile`测试会更方便。

#### `-ipath pattern`

类似于`-path`，但匹配时不区分大小写。

#### `-iregex pattern`

类似于`-regex`，但匹配时不区分大小写。

#### `-iwholename pattern`

参见`-ipath`。这种替代方案的移植性不如`-ipath`。

#### `-links n`

文件有`n`个链接。

#### `-lname pattern`

文件是一个符号链接，其内容匹配 shell 模式`pattern`。元字符不特殊处理`/`或`.`。如果生效了`-L`选项或`-follow`选项，除非符号链接损坏，否则此测试返回假。

#### `-mmin n`

文件数据最后修改于`n`分钟前。

#### `-mtime n`

文件数据最后修改于`n`个 24 小时前。参见`-atime`的注释以理解舍入如何影响对文件修改时间的解释。

#### `-name pattern`

文件名的基础（删除前导目录后的路径）匹配 shell 模式`pattern`。由于删除了前导目录，用于`-name`匹配的文件名永远不会包含斜杠，因此`-name 'a/b'`永远不会匹配任何内容（你可能需要使用`-path`）。

元字符（`*`、`?`和`[]`）会匹配基础名开头的`.`（这是 findutils-4.2.2 中的更改；参见下文的“标准符合性”章节）。若要忽略某个目录及其下的文件，请使用`-prune`；参见`-path`描述中的示例。

大括号不被视为特殊字符，尽管包括 Bash 在内的某些 shell 在 shell 模式中赋予了大括号特殊含义。文件名匹配是使用`fnmatch(3)`库函数实现的。不要忘记将模式包含在引号中以防止其被 shell 扩展。

#### `-newer file`

文件修改时间比`file`更新。如果`file`是符号链接且生效了`-H`选项或`-L`选项，则始终使用其指向的文件修改时间。

#### `-newerXY reference`

将当前文件的时间戳与`reference`进行比较。`reference`参数通常是文件名（使用其一个时间戳进行比较），但也可以是描述绝对时间的字符串。`X`和`Y`是其他字母的占位符，这些字母决定了使用`reference`的哪个时间进行比较。

| 标识 | 含义 |
| :--- | :--- |
| `a` | 文件`reference`的访问时间 |
| `B` | 文件`reference`的创建时间 |
| `c` | `reference`的 inode 状态改变时间 |
| `m` | 文件`reference`的修改时间 |
| `t` | `reference`直接被解释为时间 |

某些组合是无效的；例如，`X`为`t`是无效的。某些组合在所有系统上都没有实现；例如，并非所有系统都支持`B`。如果指定的`XY`组合无效或不受支持，将导致致命错误。

时间的解释方式类似于 GNU `date`的`-d`选项参数。如果你尝试使用引用文件的创建时间，且无法确定创建时间，将产生致命错误消息。如果你指定的测试引用了正在检查的文件创建时间，则该测试对于任何创建时间未知的文件将失败。

#### `-nogroup`

没有组与文件的数字组 ID 对应。

#### `-nouser`

没有用户与文件的数字用户 ID 对应。

#### `-path pattern`

文件名匹配 shell 模式`pattern`。元字符不特殊处理`/`或`.`；例如：

```bash
find . -path "./sr*sc"
```

将为一个名为`./src/misc`的目录打印条目（如果它存在）。

若要忽略整个目录树，请使用`-prune`而不是检查树中的每个文件。例如，要跳过目录`src/emacs`及其下的所有文件和目录，并打印找到的其他文件的名称，可以执行如下操作：

```bash
find . -path ./src/emacs -prune -o -print
```

注意，模式匹配测试适用于整个文件名，从命令行上指定的某个起点开始。只有当相关的起点也是绝对路径时，在此处使用绝对路径名才有意义。这意味着此命令将永远不会匹配任何内容：

```bash
find bar -path /foo/bar/myfile -print
```

`find`将`-path`参数与正在检查的目录名和文件基础名的拼接进行比较。由于拼接永远不会以斜杠结尾，以斜杠结尾的`-path`参数将匹配任何内容（除非是命令行上指定的起点）。HP-UX `find`也支持`-path`谓词，并将出现在未来的 POSIX 标准中。

#### `-perm mode`

文件的权限位完全等于`mode`（八进制或符号）。由于需要精确匹配，如果你想在此形式下使用符号模式，可能需要指定一个相当复杂的模式。例如，`-perm g=w`只匹配设置了组权限的文件。

你可能更想使用`/`或`-`形式，例如`-perm -g=w`，它匹配任何具有组写权限的文件。参见“示例”章节以获取一些说明性示例。

#### `-perm -mode`

文件所有权限位`mode`都已设置。此形式接受符号模式，且这通常是你想要使用它们的方式。如果你使用符号模式，必须指定`u`、`g`或`o`。参见“示例”章节以获取一些说明性示例。

#### `-perm /mode`

文件的任何权限位`mode`都已设置。此形式接受符号模式。如果你使用符号模式，必须指定`u`、`g`或`o`。参见“示例”章节以获取一些说明性示例。

如果`mode`中没有权限位被设置，此测试将匹配任何文件（此处的目的是与`-perm -000`的行为保持一致）。

#### `-perm +mode`

这不再被支持（已自 2005 年起弃用）。请改用`-perm /mode`。

#### `-readable`

匹配可读的文件。这考虑了访问控制列表以及`-perm`测试忽略的其它权限属性。此测试使用了`access(2)`系统调用，因此可能会被进行 UID 映射（或根抑制）的 NFS 服务器欺骗，因为许多系统在内核中实现`access(2)`，因此无法利用服务器上的 UID 映射信息。

#### `-regex pattern`

文件名匹配正则表达式`pattern`。这是对整个路径的匹配，而不是搜索。例如，要匹配名为`./fubar3`的文件，可以使用正则表达式`.*bar.`或`.*b.*3`，但不是`f.*r3`。`find`理解的正则表达式默认是 Emacs 正则表达式，但可以通过`-regextype`选项更改。

#### `-samefile name`

文件与`name`指向同一个 inode。当`-L`生效时，这包含符号链接。

#### `-size n[cwbkMG]`

文件使用`n`单位的空间，并向上取整。可以使用以下后缀：

- `b`：512 字节块（如果未使用后缀，则默认为此值）。
- `c`：字节。
- `w`：双字节字。
- `k`：千字节（1024 字节为单位）。
- `M`：兆字节（1048576 字节为单位）。
- `G`：吉字节（1073741824 字节为单位）。

大小不计算间接块，但会计算稀疏文件中未实际分配的块。请记住，`-printf`的`%k`和`%b`格式指定符处理稀疏文件的方式不同。`b`后缀始终表示 512 字节块，而绝不是 1 千字节（KB）块，这与`-ls`的行为不同。

`+`和`-`前缀像通常一样表示大于和小于，但请注意大小会向上舍入到下一个单位（因此一个 1 字节的文件不会被`-size -1M`匹配）。`-true`始终为真。

#### `-type c`

文件类型为`c`：

- `b`：块（有缓冲）特殊文件。
- `c`：字符（无缓冲）特殊文件。
- `d`：目录。
- `p`：命名管道（FIFO）。
- `f`：目录文件。
- `l`：符号链接；如果生效了`-L`或`-follow`选项，则永远为假，除非符号链接是断开的。如果你想在`-L`生效时搜索符号链接，请使用`-xtype`。
- `s`：套接字。
- `D`：门（Solaris）。

#### `-uid n`

文件的数字用户 ID 为`n`。

#### `-used n`

文件在状态最后一次更改后访问了`n`天。

#### `-user uname`

文件由用户`uname`所有（允许数字用户 ID）。

#### `-wholename pattern`

参见`-path`。这种替代方案比`-path`的移植性较差。

#### `-writable`

匹配可写的文件。这考虑了访问控制列表（ACL）以及其他`-perm`测试忽略的权限伪迹。此测试使用了`access(2)`系统调用，因此可能会被进行 UID 映射（或根用户抑制）的 NFS 服务器所欺骗，因为许多系统在客户端内核中实现`access(2)`，因此无法利用服务器上持有的 UID 映射信息。

#### `-xtype c`

与`-type`相同，除非文件是符号链接。对于符号链接：如果指定了`-H`或`-P`选项，当文件指向类型为`c`的文件时，则为真；如果给了`-L`选项，当`c`为`l`时，为真。

换句话说，对于符号链接，`-xtype`检查`-type`不检查的文件类型。

#### `-context pattern`

（仅限 SELinux）文件的安全上下文匹配 glob 模式`pattern`。

### 操作

- `-delete`：删除文件；如果删除成功则为真。如果删除失败，将发出错误消息。如果`-delete`失败，`find`的退出状态将是非零（当它最终退出时）。使用`-delete`会开启`-depth`选项。

  **警告**：不要忘记`find`命令行作为表达式求值，因此将`-delete`放在第一个将使`find`尝试删除你指定的起始点以下的所有内容。在测试以后打算配合`-delete`使用的`find`命令行时，你应该显式指定`-depth`以避免日后的意外。由于`-delete`意味着`-depth`，你无法同时有效使用`-prune`和`-delete`。

- `-exec command ;`：执行`command`；如果返回状态为 0 则为真。`find`的所有后续参数都将被视为命令的参数，直到遇到由`';'`组成的参数为止。字符串`'{}'`在命令参数的每个出现处都会被替换为正在处理的文件名，而不像某些版本的`find`那样只在单独的参数中替换。

  这两种构造都可能需要转义（使用`\'`）或加引号，以防止它们被 shell 扩展。参见“示例”部分获取使用`-exec`选项的示例。指定的命令会为每个匹配的文件运行一次。命令在起始目录中执行。使用`-exec`操作存在不可避免的安全问题；你应该使用`-execdir`选项。

- `-exec command {} +`：`-exec`操作的这种变体在所选文件上运行指定的命令，但命令行是通过在末尾追加每个选定的文件名来构建的；命令的调用总数将远少于匹配的文件数。命令行的构建方式与`xargs`构建其命令行非常相似。

  命令中只允许出现一个`'{}'`。命令在起始目录中执行。如果`find`遇到错误，有时会导致立即退出，因此某些待处理命令可能完全不会运行。这种`-exec`变体始终返回真。

- `-execdir command ;`
- `-execdir command {} +`

  类似于`-exec`，但指定的命令从匹配文件所在的子目录运行，该目录通常不是你启动`find`的目录。这是一种调用命令更安全的方法，因为避免了在解析指向匹配文件的路径时的竞态条件。

  与`-exec`操作一样，`-execdir`的`+`形式将构建一个处理多个匹配文件的命令行，但任何给定的`command`调用只会列出存在于相同子目录中的文件。

  如果你使用此选项，必须确保你的`$PATH`环境变量不引用`.`；否则，攻击者可以在你运行`-execdir`的目录中留下一个命名恰当的文件，从而运行他们喜欢的任何命令。对于`$PATH`中存在空条目或非绝对目录名的情况也是如此。

  如果`find`遇到错误，有时会导致立即退出，因此某些待处理命令可能完全不会运行。操作的结果取决于使用的是`+`还是`;`变体；`-execdir command +`始终返回真，而`-execdir command ;`仅在`command`返回 0 时返回真。

- `-fls file`：类似于`-ls`，但写入到`file`。块计数为 1K 块，除非设置了环境变量`POSIXLY_CORRECT`，此时使用 512 字节块。参见“特殊文件名”章节了解如何处理文件名中的特殊字符。

- `-fprint file`：为真；将完整文件名打印到`file`。如果在`find`运行时`file`不存在，则创建它；如果已存在，则将其截断。文件名`/dev/stdout`和`/dev/stderr`被特殊处理；它们分别引用标准输出和标准错误。即使谓词不匹配，输出文件也会创建。参见“特殊文件名”章节了解如何处理文件名中的特殊字符。

- `-fprint0 file`：为真；类似于`-print0`，但写入到`file`，类似于`-fprint`。即使谓词不匹配，输出文件也会创建。参见“特殊文件名”章节了解如何处理文件名中的特殊字符。

- `-fprintf file format`：为真；类似于`-printf`，但写入到`file`，类似于`-fprint`。即使谓词不匹配，输出文件也会创建。参见“特殊文件名”章节了解如何处理文件名中的特殊字符。

- `-ls`：为真；在标准输出上以`ls -dils`格式列出当前文件。参见“特殊文件名”章节了解如何处理文件名中的特殊字符。

- `-ok command ;`：类似于`-exec`，但先询问用户。如果用户同意，则执行命令；否则返回假。如果执行命令，其标准输入将重定向自`/dev/null`。

  提示的响应将与一对正则表达式匹配，以确定其是否为肯定或否定响应。该正则表达式在`POSIXLY_CORRECT`环境变量设置时从系统获取，否则从`find`的消息翻译中获取。如果系统没有合适的定义，将使用`find`自己的定义。

  在任何情况下，正则表达式本身的解释都会受到环境变量`LC_CTYPE`（字符类）和`LC_COLLATE`（字符范围和等价类）的影响。

- `-okdir command ;`

  类似于`-execdir`，但会像`-ok`一样先询问用户。如果用户不同意，则返回假。如果执行了命令，其标准输入将重定向自`/dev/null`。

#### `-print`

真；在标准输出上打印完整文件名，并在后跟一个换行符。如果你正将`find`的输出管道到另一个程序，并且极有可能你正在搜索的文件可能包含换行符，那么你应该认真考虑使用`-print0`选项而不是`-print`。有关如何处理文件名中的特殊字符的信息，请参阅“UNUSUAL FILENAMES（异常文件名）”部分。

#### `-print0`

真；在标准输出上打印完整文件名，并在后跟一个空字符（而不是`-print`使用的换行符）。这允许包含换行符或其他类型空白的文件名被处理`find`输出的程序正确解释。此选项对应`xargs`的`-0`选项。

#### `-printf format`

真；在标准输出上打印`%`，并解释`\'`转义字符和`%'`指令。字段宽度精度可以像 C 语言的`printf`函数一样指定。

请注意，许多字段是以`%s`而不是`%d`打印的，这可能意味着标志的作用不像你预期的那样工作。这也意味着`-`标志是有效的（它强制字段左对齐）。与`-print`不同，`-printf`不会在字符串末尾添加换行符。

转义和指令如下：



# 转义序列与格式指令

## 转义序列

- `\a`：警铃声。
- `\b`：退格键。
- `\c`：立即停止打印此格式并刷新输出。
- `\f`：分页符。
- `\n`：换行符。
- `\r`：回车。
- `\t`：水平制表符。
- `\v`：垂直制表符。
- `\0`：ASCII NUL。
- `\\`：字面上的反斜杠（`\`）。
- `\NNN`：ASCII 代码为 `NNN`（八进制）的字符。
- `\'` 字符后跟任何其他字符被视为普通字符，因此它们都会被打印。
- `%%`：字面上的百分号。

## 时间格式指令

### 访问时间

- `%a`：文件的最后访问时间，格式由 C 语言的 `ctime` 函数返回。
- `%A*k*`：文件的最后访问时间，格式由 `k` 指定，`k` 可能是 `@` 或 C 语言 `strftime` 函数的指令。`k` 的可能值列如下；由于系统之间 `strftime` 的差异，某些值可能在所有系统上不可用。
  - `@`：自 1970 年 1 月 1 日 00:00 GMT 以来的秒，带有小数部分。

### 时间字段

- `H`：小时 (00..23)
- `I`：小时 (01..12)
- `k`：小时 ( 0..23)
- `l`：小时 ( 1..12)
- `M`：分钟 (00..59)
- `p`：本地的 AM 或 PM
- `r`：12 小时制时间 (hh:mm:ss [AP]M)
- `S`：秒 (00.00 .. 61.00)。带有小数部分。
- `T`：24 小时制时间 (hh:mm:ss)
- `+`：日期和时间，用 `+` 分隔，例如 `2004-04-28+22:22:05.0`。这是一个 GNU 扩展。时间以当前时区给出（可能会受环境变量 `TZ` 的影响）。秒字段包含小数部分。
- `X`：本地的时间表示 (H:M:S)
- `Z`：时区（例如 EDT），如果无法确定时区，则为空。

### 日期字段

- `a`：本地的缩写星期名称 (Sun..Sat)
- `A`：本地的完整星期名称，长度可 (Sunday..Saturday)
- `b`：本地的缩写月份名称 (Jan..Dec)
- `B`：本地的完整月份名称，长度可 (January..December)
- `c`：本地的日期和时间 (Sat Nov 04 12:02:33 EST 1989)。格式与 `ctime(3)` 相同，为了与该格式保持兼容，秒字段中没有小数部分。
- `d`：一个月中的几 (01..31)
- `D`：日期 (mm/dd/yy)
- `h`：与 `b` 相同
- `j`：一年中的天数 (001..366)
- `m`：月份 (01..12)
- `U`：以周日为周的第一天的周数 (00..53)
- `w`：星期几 (0..6)
- `W`：以周一为周的第一天的周数 (00..53)
- `x`：本地的日期表示 (mm/dd/yy)
- `y`：年份的最后两位 (00..99)
- `Y`：年份 (1970...)

## 文件信息格式指令

- `%b`：该文件使用的 512 字节块磁盘空间量。由于磁盘空间按文件系统块大小的倍数分配，这通常大于 `%s/512`，但如果文件是稀疏文件，也可能更。
- `%c`：文件的最后状态更改时间，格式由 C 语言的 `ctime` 函数返回。
- `%C*k*`：文件的最后状态更改时间，格式由 `k` 指定，与 `%A` 相同。
- `%d`：文件在目录树中的深度；0 表示文件是起点。
- `%D`：文件所在的设备号 (`st_dev`)。
- `%f`：该文件使用的 512 字节块磁盘空间量。由于磁盘空间按文件系统块大小的倍数分配，这通常大于 `%s/512`，但如果文件是稀疏文件，也可能更。
- `%g`：文件的最后状态更改时间，格式由 C 语言的 `ctime` 函数返回。
- `%H`：文件的最后状态更改时间，格式由 `k` 指定，与 `%A` 相同。
- `%i`：文件的 inode 节点号。
- `%j`：文件使用的 512 字节块磁盘空间量。由于磁盘空间按文件系统块大小的倍数分配，这通常大于 `%s/512`，但如果文件是稀疏文件，也可能更。
- `%k`：文件的最后状态更改时间，格式由 C 语言的 `ctime` 函数返回。
- `%l`：文件的最后状态更改时间，格式由 `k` 指定，与 `%A` 相同。
- `%m`：权限（八进制）。
- `%n`：文件的硬链接数。
- `%p`：文件名。
- `%P`：文件名。
- `%s`：以字节计算的文件大小。
- `%S`：稀疏度。
- `%t`：文件的最后修改时间，格式由 C 语言的 `ctime` 函数返回。
- `%T*k*`：文件的最后修改时间，格式由 `k` 指定，与 `%A` 相同。
- `%u`：文件的用户名，如果用户没有名称则显示数字用户 ID。
- `%U`：文件的数字用户 ID。
- `%y`：文件类型（如 `ls -l`），U=未知类型（不应发生）
- `%Y`：文件类型（如 `%y`），加上跟踪符号链接：L=循环，N=不存在
- `%Z`：（仅限 SELinux）文件的安全上下文。
- `%{`、`%(`：留供以后使用。

## 操作选项

- `-prune True;` 如果文件是一个目录，则不进入其中。如果给出了 `-depth`，则为假；无影响。由于 `-delete` 包含了 `-depth`，因此你无法有效地结合 `-prune` 和 `-delete` 使用。
- `-quit` 立即退出。不会留下子进程继续运行，但将不再处理命令行上指定的后续路径。例如，`find /tmp/foo /tmp/bar -print -quit` 只打印 `/tmp/foo`。任何通过 `-execdir ... {} +` 构建的命令行都将在 `find` 退出之前被调用。退出状态可能为 0 也可能不为 0，取决于是否已经发生了错误。

## 特殊文件名

`find` 的许多操作都会导致输出其他用户控制的数据。这包括文件名、大小、修改时间等。文件名是一个潜在问题，因为它们可以包含除 `\0` 和 `/` 之外的任何字符。文件名中的非常规字符会对你的终端产生意料之外且通常是不人意的结果（例如，在某些终端上更改你功能键的设置）。不同的操作对非常规字符的处理方式不同，下文所述。

### `-print0, -fprint0`

始终原样打印精确的文件名，即使输出目标是终端。

### `-ls, -fls`

非常规字符始终会被转义。空格、反斜杠和双引号字符使用 C 风格的转义打印（例如 `\f`、`\"`）。其他非常规字符使用八进制转义打印。其他可打印字符（对于 `-ls` 和 `-fls`，这些是八进制 041 到 0176 之间的字符）按原样打印。

### `-printf, -fprintf`

如果输出不是终端，则按原样打印。否则，结果取决于使用的是哪个指令。指令 `%D`、`%F`、`%g`、`%G`、`%H`、`%Y` 和 `%y` 的值不受文件所有者的控制，因此原样打印。指令 `%a`、`%b`、`%c`、`%d`、`%i`、`%k`、`%m`、`%M`、`%n`、`%s`、`%t`、`%u` 和 `%U` 的值受文件所有者的控制，但不能用于向终端发送任意数据，因此这些按原样打印。指令 `%f`、`%h`、`%l`、`%p` 和 `%P` 会被引用。这种引用方式与 GNU `ls` 的方式相同。如果你能够决定 `find` 输出的格式，通常使用 `\0` 作为终止符比使用换行符更好，因为文件名可以包含空格和换行符。`LC_CTYPE` 环境变量的设置用于确定哪些字符需要被引用。

### `-print, -fprint`

引的处理方式与 `-printf` 和 `-fprintf` 相同。如果你在脚本中使用 `find`，或者在匹配到的文件可能具有任意名称的情况下，你应该考虑使用 `-print0` 代替 `-print`。

`-ok` 和 `-okdir` 操作按原样打印当前文件名。这在未来的发布中可能会发生。

## 运算符

按优先级从高到低列出：

- `( *expr* )`：强制优先级。由于括号在 shell 中有特殊含义，你通常需要对它们加引号。此手册页中的许多示例使用反斜杠来实现此目的：用 `\(...\)` 代替 `(...)`。
- `! *expr*`：如果 `*expr` 为假则为真。该字符通常也需要防止被 shell 解释。
- `-not *expr*`：与 `! *expr*` 相同，但不符合 POSIX 标准。
- `*expr1 expr2*`：连续两个表达式被视为隐含的“与”连接；如果 `expr1` 为假，则不对 `expr2` 求值。
- `*expr1* -a *expr2*`：与 `expr1 expr2` 相同。
- `*expr1* -and *expr2*`：与 `expr1 expr2` 相同，但不符合 POSIX 标准。
- `*expr1* -o *expr2*`：或；如果 `expr1` 为真，则不对 `expr2` 求值。
- `*expr1* -or *expr2*`：与 `expr1 -o *expr2` 相同，但不符合 POSIX 标准。
- `*expr1* , *expr2*`：列表；`expr1` 和 `expr2` 始终会被求值。`expr1` 的值被丢弃；列表的值是 `expr2` 的值。逗号运算符对于搜索多种不同类型的内容非常有用，但只需遍历一次文件系统层次。`-fprintf` 操作可以将各种匹配项列出到多个不同的输出文件中。

## 标准遵循性

为了尽可能符合 POSIX 标准，你应该设置 `POSIXLY_CORRECT` 环境变量。POSIX 标准（IEEE Std 1003.1, 2003 版）中指定了以下选项：

- `-H`：支持此选项。
- `-L`：支持此选项。
- `-name`：支持此选项，但 POSIX 遵循性取决于系统系统的 `fnmatch(3)` 库函数的 POSIX 遵循性。从 findutils-4.2.2 开始，shell 元字符（例如 `*`、`?` 或 `[]`）将匹配 `.`。
- `-type`：支持此选项。POSIX 规定了 `b`、`c`、`d`、`l`、`p`、`f` 和 `s`。GNU find 还支持 `D`。
- `-ok`：支持。响应的解释根据设置 `LC_MESSAGES` 环境变量的“是”和“否”模式进行。当设置 `POSIXLY_CORRECT` 环境变量时，这些模式取决于系统的肯定（是）或否定（否）响应。当未设置 `POSIXLY_CORRECT` 时，模式取自 find 自身的目录。
- `-newer`：支持。如果指定的文件是符号链接，则始终会被引用。这是以前行为的改变，以前从符号链接获取相关时间；见下文历史部分。
- `-perm`：支持。如果未设置 `POSIXLY_CORRECT` 环境变量，某些在 POSIX 中无效的模式参数（例如 `+a+x`）也将被支持。

### 其他谓词

谓词 `-atime`、`-ctime`、`-depth`、`-group`、`-links`、`-mtime`、`-nogroup`、`-nouser`、`-print`、`-prune`、`-size`、`-user` 和 `-xdev` 均受支持。

POSIX 标准规定了括号 `(`、`)`、否定 `!` 以及 `and` 和 `or` 运算符（`-a`, `-o`）。

所有其他选项、谓词、表达式等都是超出 POSIX 标准的扩展。然而，这些扩展许多并非 GNU find 特有。

POSIX 标准要求 **find** 检测循环：

**find** 实用程序应检测无限循环；即进入一个之前访问过的、作为最后一个文件的祖先的目录。当检测到无限循环时，find 应向标准错误写入一条诊断消息，并在层次结构中恢复位置或终止。

GNU `find` 遵循这些要求。包含指向祖先目录硬链接项的目录，其链接计数通常会比本应有的值低。这意味着 GNU `find` 有时会优化掉对实际上指向祖先目录的子目录的访问。由于 `find` 并没有实际进入该子目录，因此允许不输出诊断信息。尽管这种行为可能让人有些困惑，但不太可能有人实际上依赖于这种行为。如果通过 `-noleaf` 关闭了叶子节点优化，则目录项将始终被检查，并在适当的情况下发布诊断信息。符号链接本身不能创建文件系统循环，但如果使用了 `-L` 选项或 `-follow` 选项，当 `find` 遇到符号链接循环时，会发布诊断信息。与包含硬链接的循环一样，叶子节点优化通常意味着 `find` 知道它不需要对符号链接调用 `stat()` 或 `chdir()`，因此这种诊断通常是没的。

为了与各种 BSD 系统兼容，`find` 支持 `-d` 选项，但你应该使用符合 POSIX 标准的选项 `-depth`。

`POSIXLY_CORRECT` 环境变量不会影响 `-regex` 或 `-iregex` 测试的行为，因为这些测试未在 POSIX 标准中规定。

## 环境变量

### `LANG`

为未设置或为空的国际化变量提供默认值。

### `LC_ALL`

如果设置为非空字符串值，则覆盖所有其他国际化变量的值。

### `LC_COLLATE`

POSIX 标准规定该变量影响用于 `-name` 选项的模式匹配。GNU find 使用 `fnmatch(3)` 库函数，因此对 `LC_COLLATE` 的支持取决于系统库。该变量还影响对 `-ok` 响应的解释，而 `LC_MESSAGES` 变量选择了用于解释 `-ok` 响应的实际模式，模式中任何括号表达式的解释将受到 `LC_COLLATE` 的影响。

### `LC_CTYPE`

该变量影响正则表达式中字符类的处理，以及 `-name` 测试中的处理（如果系统的 `fnmatch(3)` 库支持此项）。该变量还影响解释由 `-ok` 提示响应时使用的正则表达式中任何字符类的解释。`LC_CTYPE` 环境变量还会影响打印文件名时哪些字符被视为不可打印字符；请参见“异常文件名”（UNUSUAL FILENAMES）章节。

### `LC_MESSAGES`

确定用于国际化消息的区域（locale）。如果设置了 `POSIXLY_CORRECT` 环境变量，它还决定了 `-ok` 操作提示响应的解释。

### `NLSPATH`

确定国际化消息目录的位置。

### `PATH`

影响搜索以查找由 `-exec`、`-execdir`、`-ok` 和 `-okdir` 调执行文件的目录。

### `POSIXLY_CORRECT`

确定 `-ls` 和 `-fls` 使用的块大小。如果设置了 `POSIXLY_CORRECT`，块的单位为 512 字节。否则单位为 1024 字节。

设置此变量默认还会关闭警告消息（即意味着 `-nowarn`），因为 POSIX 要求除了 `-ok` 的输出外，打印在 stderr 上的所有都是都是诊断，并且必须导致非零退出状态。

当未设置 `POSIXLY_CORRECT` 时，如果 `+zzz` 不是有效的符号模式，则 `-perm +zzz` 被处理为与 `-perm /zzz` 相同。当设置 `POSIXLY_CORRECT` 时，此类结构被视为错误。

当设置 `POSIXLY_CORRECT` 时，对 `-ok` 操作提示的响应将根据系统的消息目录进行解释，而不是根据 `find` 自身的消息翻译。

### `TZ`

影响 `-printf` 和 `-fprintf` 中某些时间相关格式指令使用的时区。

## 二进制文件

findutils 源码发行包含两种不同的 `find` 实现。旧的实现递归遍历文件系统，而新的实现使用 `fts(3)`。两者通常都会安装。

如果在执行 `configure` 时传递了 `--without-fts` 选项，则递归实现被安装为 `find`，基于 fts 的实现安装为 `ftsfind`。否则，基于 fts 的实现被安装为 `find`，递归实现安装为 `oldfind`。

## 示例

```bash
find /tmp -name core -type f -print | xargs /bin/rm -f
```

在 `/tmp` 目录或以下查找名为 `core` 的文件并删除它们。注意，如果文件名包含换行符、单引号、双引号或空格，此操作将无法正常工作。

```bash
find /tmp -name core -type f -print0 | xargs -0 /bin/rm -f
```

在 `/tmp` 目录或以下查找名为 `core` 的文件并删除它们，处理文件名的方式可以正确处理包含单引号、双引号、空格或换行符的文件或目录名。`-name` 测试在 `-type` 测试之前，以避免对每个文件都调用 `stat(2)`。

```bash
find . -type f -exec file '{}' \;
```

对当前目录及以下的每个文件运行 `file` 命令。注意，花括号被包含在单引号中，以防止它们被解释为 shell 脚本标点符号。

```bash
find . -type f -exec file '{}' \;
```

遍历一次文件系统，将 setuid 文件列出 `/root/suid.txt`，将大文件列出 `/root/big.txt`。

```bash
find $HOME -mtime 0
```

在你的主目录下查找过去 24 小时内修改过的文件。此命令之所以这样工作，是因为每个文件最后修改的时间除以 24 小时并丢弃余数。这意味着要匹配 `-mtime 0`，文件的修改时间必须少于 24 小时。

```bash
find /sbin /usr/sbin -executable ! -readable -print
```

查找可执行但不可读的文件。

```bash
find . -perm 664
```

查找所有者和组具有读写权限，且其他用户仅可读不可写的文件。符合这些标准但设置了其他权限（例如有人可以执行该文件）的文件将不会匹配。

```bash
find . -perm -664
```

查找所有者和组具有读写权限，且其他用户可读的文件，而不考虑任何其他权限位是否存在（例如执行位）。这将匹配模式为 0777 的文件等。

```bash
find . -perm /222
```

查找对某些可写的文件（其所有者、其组或任何人）。

```bash
find . -perm -444 -perm /222 ! -perm /111
find . -perm -a+r -perm /a+w ! -perm /a+x
```

这两条命令都用于搜索所有人均可读（`-perm -444` 或 `-perm -a+r`）、至少设置了一个写位（`-perm /222` 或 `-perm /a+w`）但任何人都不可执行（分别对应 `! -perm /111` 和 `! -perm /a+x`）的文件。

```bash
cd /source-dir
find . -name .snapshot -prune -o \( \! -name *~ -print0 \)|-
cpio -pmd0 /dest-dir
```



该命令将`/source-dir`的内容复制到`/dest-dir`，但跳过名为`.snapshot`的文件和目录（及其包含的所有内容）。它还会跳过以`~`结尾的文件或目录，但保留其内容。`-prune -o \( ... -print0 \)`结构非常常见。这里的思路是`-prune`之前的表达式匹配了要剪掉的对象。然而，`-prune`本身返回真，因此随后的`-o`确保仅对那些没有被剪掉的目录评估右侧部分（被剪掉目录的内容甚至不会被访问，因此其内容无关）。`-o`右侧的表达式使用括号仅是为了清晰起见。它强调了`-print0`操作仅针对未应用`-prune`的对象执行。由于测试之间默认`and`条件的绑定优先级比`-o`更紧密，这在默认情况下也是如此，但括号有助于展示执行逻辑。

```bash
find repo/ -exec test -d {}/.svn \; -or -exec test -d {}/.git \; -or -exec test -d {}/CVS \; -print -prune
```

给定以下项目目录及其关联的 SCM 管理目录，请对项目根目录进行高效搜索：

```text
repo/project1/CVS
repo/gnu/project2/.svn
repo/gnu/project3/.svn
repo/gnu/project3/src/.svn
repo/project4/.git
```

在此示例中，`-prune`防止了进入已经发现的目录进行必要的递归（例如，我们不会搜索`project3/src`，因为我们已经找到了`project3/.svn`），但确保了兄弟目录（`project2`和`project3`）被找到。

## EXIT STATUS

如果所有文件都成功处理，`find`以状态 0 退出；发生错误时状态大于 0。这是一个故意非常宽泛的描述，但如果返回值为非零，你不应该依赖`find`结果的正确性。

当发生某些错误时，`find`可能会立即停止，而不完成所有指定的操作。例如，某些起点可能未被检查，或者某些等待中的`-exec ... {} +`或`-execdir ... {} +`程序调用可能未执行。

## SEE ALSO

`locate(1)`、`locatedb(5)`、`updatedb(1)`、`xargs(1)`、`chmod(1)`、`fnmatch(3)`、`regex(7)`、`stat(2)`、`lstat(2)`、`ls(1)`、`printf(3)`、`strftime(3)`、`ctime(3)`

`find`的完整文档作为 Texinfo 手册维护。如果你的站点环境中正确安装了`info`和`find`程序，执行命令`info find`应该可以访问完整手册。

## HISTORY

从 findutils-4.2.2 开始，文件名模式中使用的 shell 元字符（例如`*`、`?`或`[]`）将匹配开头的`.`，因为 IEEE POSIX 解释 126 条有此项要求。

从 findutils-4.3.3 开始，`-perm /000`现在匹配所有文件而不是没有任何文件。

findutils-4.3.3 中实现了纳秒级分辨率的时间戳。

从 findutils-4.3.11 开始，`-delete`操作在失败时会将`find`的退出状态设置为非零值。然而，`find`不会立即退出。在此之前，`find`的退出状态不受`-delete`失败的影响。

| 特性 | 引入版本 | 同样出现在 |
| :--- | :--- | :--- |
| `-newerXY` | 4.3.3 | BSD |
| `-D` | 4.3.1 | |
| `-O` | 4.3.1 | |
| `-readable` | 4.3.0 | |
| `-writable` | 4.3.0 | |
| `-executable` | 4.3.0 | |
| `-regextype` | 4.2.24 | |
| `-exec ... +` | 4.2.12 | POSIX |
| `-execdir` | 4.2.12 | BSD |
| `-okdir` | 4.2.12 | |
| `-samefile` | 4.2.11 | |
| `-H` | 4.2.5 | POSIX |
| `-L` | 4.2.5 | POSIX |
| `-P` | 4.2.5 | BSD |
| `-delete` | 4.2.3 | |

- `-preferences`

  打开偏好设置框。

- `-private`

  以私有浏览模式启动`firefox`。

- `-private-toggle`

  切换私有浏览模式。

- `-setDefaultBrowser`

  将`firefox`设置为默认网络浏览器。

- `-search` `term`

  使用你的默认搜索引擎搜索`term`。

- `-migration`

  启动迁移向导。

- `-new-instance`

  打开新实例，而不是在运行中的实例中打开新窗口。

## FILES

`/usr/bin/firefox` - 封装`firefox`的 shell 脚本

`/usr/lib/mozilla/firefox-bin` - `firefox`可执行文件

## VERSION

1.0

## BUGS

如需报告 bug，请访问`http://bugzilla.mozilla.org/`。

## SEE ALSO

`mozilla(1)`

## AUTHORS

`The Mozilla Organization`

`http://www.mozilla.org/about.html`

---

# FIREWALL-CMD

## NAME

`firewall-cmd` - firewalld 命令行客户端

## SYNOPSIS

`firewall-cmd` `[OPTIONS...]`

## DESCRIPTION

`firewall-cmd`是 firewalld 守护进程的命令行客户端。它提供了管理运行时和永久配置的接口。

firewalld 中的运行时配置与永久配置是分离的。这意味着可以在运行时配置或永久配置中进行更改。

## OPTIONS

支持以下选项：

### General Options

`-h`、`--help`

打印简短的帮助文本并退出。

`-V`、`--version`

打印 firewalld 的版本字符串。此选项不能与其他选项组合。

`-q`、`--quiet`

不打印状态消息。

### Status Options

`--state`

检查 firewalld 守护进程是否处于活动（即正在运行）。如果活动，则返回退出码 0，否则返回`NOT_RUNNING`（参见“EXIT CODES”部分）。这会将状态打印到`STDOUT`。

`--reload`

重载防火墙规则并保留状态信息。当前的永久配置将成为新的运行时配置，即在重载之前完成的所有仅运行时的更改，如果没有包含在永久配置中，则将在重载时丢失。

`--complete-reload`

完全重载防火墙，甚至是 netfilter 内核模块。这极可能会终止活动连接，因为状态信息丢失了。此选项应在出现严重的防火墙问题时使用。例如，由于状态信息问题导致无法通过正确的防火墙规则建立连接。

`--runtime-to-permanent`

保存活跃的运行时配置并用其覆盖永久配置。预期的工作方式是：在配置 firewalld 时仅进行运行时更改，一旦你对配置满意并测试其已按预期方式运行，就将配置保存到磁盘。

### Permanent Options

永久选项`--permanent`可用于永久设置选项。这些更改不会立即生效，只有在服务重启/重载或系统重启后才会生效。如果没有`--permanent`选项，更改将仅作为运行时配置的一部分。

如果你要在运行时和永久配置中进行更改，请分别使用带有和不带`--permanent`选项的相同调用。

`--permanent`选项可以可选添加到后续所有支持的选项中。

### Zone Options

`--get-default-zone`

打印连接和接口的默认区域。

`--set-default-zone`=`zone`

为未选择区域的连接和接口设置默认区域。设置默认区域将更改使用默认区域的连接或接口的区域。

这是一个运行时和永久性的更改。

`--get-active-zones`

打印当前活动的所有区域，以及这些区域使用的接口和源。活动区域是指绑定到接口或源的区域。输出格式为：

`zone1 interfaces: interface1 interface2 .. sources: source1 .. zone2 interfaces: interface3 .. zone3 sources: source2 ..`

如果区域没有绑定的接口或源，则相应的行将被省略。

`--permanent` `--get-zones`

以空格分隔的列表打印定义的区域。

`--permanent` `--get-services`

以空格分隔的列表打印定义的服务。

`--permanent` `--get-icmptypes`

以空格分隔的列表打印定义的 icmptypes。

`--permanent` `--get-zone-of-interface`=`interface`

打印`interface`绑定的区域名称或显示`no zone`。

`--permanent` `--get-zone-of-source`=`source`[`mask`]

打印`source`[`mask`]绑定的区域名称或显示`no zone`。

`--permanent` `--list-all-zones`

列出在所有区域中添加或启用的所有内容。输出格式为：

`zone1 interfaces: interface1 .. sources: source1 .. services: service1 .. ports: port1 .. forward-ports: forward-port1 .. icmp-blocks: icmp-type1 .. rich rules: rich-rule1 .. ..`

`--permanent` `--new-zone`=`zone`

添加新区域。

`--permanent` `--delete-zone`=`zone`

删除已存在的区域。

`--permanent` `--zone` `--get-target`

获取永久区域的目标（target）。

`--permanent` `--zone` `--set-target`=`target`

设置永久区域的目标（target）。`target`为：`ACCEPT`、`DROP`、`REJECT`。

### Options to Adapt and Query Zones

这些选项影响特定的区域。如果与`--zone`=`zone`使用，它们将影响该区域。

`--permanent` `--zone` `--list-all`

列出所有区域中添加或启用的内容。如果省略区域，将使用默认区域。

`--permanent` `--zone` `--list-services`

以空格分隔的列表列出区域的服务。如果省略区域，将使用默认区域。

`--permanent` `--zone` `--add-service`=`service` [`timeout`=`timeval`]

为区域添加服务。如果省略区域，将使用默认区域。此选项可以多次指定。如果提供了超时（timeout），规则将在指定时间内有效，并在之后移除。`timeval`是数字（秒）或数字后带有`s`（秒）、`m`（分钟）、`h`（小时）之一的字符，例如`20m`或`1h`。

服务是 firewalld 提供的服务。要获取支持的服务列表，请使用`firewall-cmd --get-services`。

`--timeout`选项不能与`--permanent`选项组合。

`--permanent` `--zone` `--remove-service`=`service`

从区域删除服务。此选项可以多次指定。如果省略区域，将使用默认区域。

`--permanent` `--zone` `--query-service`=`service`

返回服务是否已添加到区域。如果省略区域，将使用默认区域。如果为真返回 0，否则返回 1。

`--permanent` `--zone` `--list-ports`

以空格分隔的列表列出区域端口。端口格式为`portid`[-`portid`]/`protocol`，它可以是端口和协议对，也可以是带有协议的端口范围。如果省略区域，将使用默认区域。

`--permanent` `--zone` `--add-port`=`portid`[-`portid`]/`protocol` [`timeout`=`timeval`]

为区域添加端口。如果省略区域，将使用默认区域。此选项可以多次指定。如果提供了超时（timeout），规则将在指定时间内有效，并在之后移除。`timeval`是数字（秒）或数字后带有`s`（秒）、`m`（分钟）、`h`（小时）之一的字符，例如`20m`或`1h`。

端口可以是单个端口号或端口范围`portid`-`portid`。协议可以是`tcp`或`udp`。

`--timeout`选项不能与`--permanent`选项组合。

`[--permanent]` `[--zone`=`zone`]` `--remove-port`=`portid`[-`portid`]/`protocol`

从`zone`移除端口。如果省略了`zone`，将使用默认区域。此选项可以多次指定。

`[--permanent]` `[--zone`=`zone`]` `--query-port`=`portid`[-`portid`]/`protocol`

返回`zone`是否已添加该端口。如果省略了`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

`[--permanent]` `[--zone`=`zone`]` `--list-icmp-blocks`

以空格分隔的列表列出为`zone`添加的控制消息协议（ICMP）类型块。如果省略了`zone`，将使用默认区域。

`[--permanent]` `[--zone`=`zone`]` `--add-icmp-block`=`icmptype` `[--timeout`=`timeval`]`

为`zone`为`icmptype`添加一个 ICMP 块。如果省略了`zone`，将使用默认区域。此选项可以多次指定。如果提供了超时时间，该规则将在指定时间内生效，并在之后自动删除。`timeval`是数字（秒）或数字后跟以下字符之一：`s`（秒）、`m`（分钟）、`h`（小时），例如`20m`或`1h`。

`icmptype`是 firewalld 支持的 icmp 类型之一。获取支持 icmp 类型列表：`firewall-cmd --get-icmptypes`。

`--timeout`选项不能与`--permanent`选项结合使用。

`[--permanent]` `[--zone`=`zone`]` `--remove-icmp-block`=`icmptype`

从`zone`移除针对`icmptype`的 ICMP 块。如果省略了`zone`，将使用默认区域。此选项可以多次指定。

`[--permanent]` `[--zone`=`zone`]` `--query-icmp-block`=`icmptype`

返回`zone`是否已添加针对`icmptype`的 ICMP 块。如果省略了`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

`[--permanent]` `[--zone`=`zone`]` `--list-forward-ports`

以空格分隔的列表列出为`zone`添加的`IPv4`转发端口。如果省略了`zone`，将使用默认区域。

对于`IPv6`转发端口，请使用富规则（rich language）。

`[--permanent]` `[--zone`=`zone`]` `--add-forward-port`=`port`=`portid`[-`portid`]:proto=`protocol`

`[:toport=`portid`[-`portid`]][:toaddr=`address`[/`mask`]]` `[--timeout`=`timeval`]`

为`zone`添加`IPv4`转发端口。如果省略了`zone`，将使用默认区域。此选项可以多次指定。如果提供了超时时间，该规则将在指定时间内生效，并在之后自动删除。`timeval`是数字（秒）或数字后跟以下字符之一：`s`（秒）、`m`（分钟）、`h`（小时），例如`20m`或`1h`。

端口可以是单个端口号`portid`或端口范围`portid`-`portid`。协议可以是`tcp`或`udp`。目标地址是一个简单的 IP 地址。

`--timeout`选项不能与`--permanent`选项结合使用。

对于`IPv6`转发端口，请使用富规则。

`[--permanent]` `[--zone`=`zone`]` `--remove-forward-port`=`port`=`portid`[-`portid`]:proto=`



## 转发端口选项

`protocol[:toport=portid[-portid]][:toaddr=address[/mask]]`

从`zone`移除`IPv4`转发端口。如果省略了`zone`，将使用默认区域。此选项可以多次指定。

对于`IPv6`转发端口，请使用富规则。

`[--permanent]` `[--zone=zone]` `--query-forward-port=port=portid[-portid]:proto=`

`protocol[:toport=portid[-portid]][:toaddr=address[/mask]]`

返回`zone`是否已添加`IPv4`转发端口。如果省略了`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

对于`IPv6`转发端口，请使用富规则。

## 伪装选项

`[--permanent]` `[--zone=zone]` `--add-masquerade` `[--timeout=timeval]`

为`zone`启用`IPv4`伪装。如果省略了`zone`，将使用默认区域。如果提供了超时时间，伪装将在指定时间内生效。`timeval`是数字（秒）或数字后跟以下字符之一：`s`（秒）、`m`（分钟）、`h`（小时），例如`20m`或`1h`。该选项不能与`--permanent`选项结合使用。对于`IPv6`伪装，请使用富规则。

`[--permanent]` `[--zone=zone]` `--remove-masquerade`

禁用`zone`的`IPv4`伪装。如果省略了`zone`，将使用默认区域。如果伪装是带有超时时间启用的，将被禁用。对于`IPv6`伪装，请使用富规则。

`[--permanent]` `[--zone=zone]` `--query-masquerade`

返回`zone`是否启用了`IPv4`伪装。如果省略了`zone`，将使用默认区域。如果为真返回 0，否则返回 1。对于`IPv6`伪装，请使用富规则。

## 富规则选项

`[--permanent]` `[--zone=zone]` `--list-rich-rules`

以换行分隔的列表列出为`zone`添加的富规则。如果省略了`zone`，将使用默认区域。

`[--permanent]` `[--zone=zone]` `--add-rich-rule=rule'` `[--timeout=timeval]`

为`zone`添加带有超时时间的富规则`'rule'`。`timeval`是数字（秒）或数字后跟以下字符之一：`s`（秒）、`m`（分钟）、`h`（小时），例如`20m`或`1h`。

`[--permanent]` `[--zone=zone]` `--remove-rich-rule=rule'`

从`zone`移除富规则`'rule'`。如果省略了`zone`，将使用默认区域。此选项可以多次指定。

`[--permanent]` `[--zone=zone]` `--query-rich-rule=rule'`

返回`zone`是否已添加了富规则`'rule'`。如果省略了`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

## 处理接口绑定的选项

将接口绑定到区域意味着该区域的设置将用于限制流量。

此部分的选项仅影响特定区域。如果与`--zone`选项配合使用，将影响区域`zone`。如果省略该选项，将影响默认区域（参见`--get-default-zone`）。

获取预定义区域列表使用`firewall-cmd --get-zones`。

接口名称是最多 16 字符的字符串，可以包含`/`、`!`和`*`。

`[--permanent]` `[--zone=zone]` `--list-interfaces`

以空格分隔的列表列出绑定到区域`zone`的接口。如果省略了`zone`，将使用默认区域。

`[--permanent]` `[--zone=zone]` `--add-interface=interface`

将接口`interface`绑定到区域`zone`。如果省略了`zone`，将使用默认区域。

作为终端用户，大多数情况下不需要此操作，因为NetworkManager（或旧网络服务）会自动将接口添加到区域（根据`ifcfg-interface`文件中的`ZONE=`选项）。只有在没有`/etc/sysconfig/network-scripts/ifcfg-interface`文件时才需要这样做。如果存在此类文件且您使用此`--add-interface`选项添加接口，请确保两种情况下的区域相同，否则将将定义。关于接口与区域的永久关联，请参见`firewalld.zones`(5)中的“如何设置或更改连接的区域?”。

`[--zone=zone]` `--change-interface=interface`

更改接口`interface`绑定的区域为`zone`。这基本上先执行`--remove-interface`后执行`--add-interface`。如果接口之前未绑定到任何区域，则其行为类似于`--add-interface`。如果省略了区域，将使用默认区域。

`[--permanent]` `[--zone=zone]` `--query-interface=interface`

查询接口`interface`是否绑定到区域`zone`。如果是，则返回 0；否则返回 1。

`[--permanent]` `--remove-interface=interface`

从之前添加的区域中移除接口`interface`的绑定。

## 处理源绑定的选项

将源绑定到区域意味着该区域的设置将用于限制来自该源的流量。

源地址或地址范围可以是一个 IP 地址，也可以带有掩码的`ipv4`或`ipv6`网络 IP 地址。对于`ipv4`，掩码可以是网络子网掩码或纯数字。对于`ipv6`，掩码为纯数字。不支持主机名。

此节中的选项仅影响一个特定的区域。如果与`--zone=zone`选项配合使用，它们将影响区域`zone`。如果省略该选项，它们将影响默认区域（参见`--get-default-zone`）。

获取预定义区域列表，请使用`firewall-cmd` `[--permanent]` `--get-zones`。

`[--permanent]` `[--zone=zone]` `--list-sources`

以空格分隔列表的形式列出绑定到区域`zone`的源。如果省略了区域，将使用默认区域。

`[--permanent]` `[--zone=zone]` `--add-source=source[/mask]`

将源`source[/mask]`绑定到区域`zone`。如果省略了区域，将使用默认区域。

`--zone=zone` `--change-source=source[/mask]`

更改源`source[/mask]`绑定的区域为`zone`。这基本上先执行`--remove-source`后执行`--add-source`。如果源之前未绑定到任何区域，则其行为类似于`--add-source`。如果省略了区域，将使用默认区域。

`[--permanent]` `[--zone=zone]` `--query-source=source[/mask]`

查询源`source[/mask]`是否绑定到区域`zone`。如果是，则返回 0；否则返回 1。

`[--permanent]` `--remove-source=source[/mask]`

从之前添加的区域中移除源`source[/mask]`的绑定。

## 服务选项

`--permanent` `--new-service=service`

添加一个新的永久服务。

`--permanent` `--delete-service=service`

删除现有的永久服务。

## 互联网控制消息报协议 (ICMP) 类型选项

`--permanent` `--new-icmptype=icmptype`

添加一个新的永久 icmptype。

`--permanent` `--delete-icmptype=icmptype`

删除现有的永久 icmptype。

## 直接选项 (Direct Options)

直接选项提供了对防火墙更直接的访问。这些选项要求用户了解基本的 iptables 概念，例如`table`(filter/mangle/nat/...)、`chain`(INPUT/OUTPUT/FORWARD/...)、`commands`(-A/-D/-I/...)、`parameters`(-p/-s/-d/-j/...)以及`targets`(ACCEPT/DROP/REJECT/...)。

当无法使用`--add-service=service`或`--add-rich-rule='rule'`时，直接选项应作为最后的手段。

每个选项的第一个参数必须是`ipv4`、`ipv6`或`eb`。使用`ipv4`用于IPv4（`iptables`(8)），使用`ipv6`用于IPv6（`ip6tables`(8)），使用`eb`用于以太网桥接（`ebtables`(8)）。

`[--permanent]` `--direct` `--get-all-chains`

获取所有到所有表中的链。此选项仅涉及之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--get-chains` { `ipv4` | `ipv6` | `eb` } `table`

以空格分隔列表的形式获取添加到表`table`中的所有链。此选项仅涉及之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--add-chain` { `ipv4` | `ipv6` | `eb` } `table` `chain`

向表`table`添加一个名为`chain`的新链。确保已没有其他同名的链。

已经存在可以与直接选项使用的基础链，例如`INPUT_direct`链（参见`iptables-save | grep direct`的输出以查看所有链）。这些链在区域链之前被跳转，也就是说，放入`INPUT_direct`的每个规则将在区域中的规则之前被检查。

`[--permanent]` `--direct` `--remove-chain` { `ipv4` | `ipv6` | `eb` } `table` `chain`

从表`table`中移除名为`chain`的链。只有通过这种方式移除之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--query-chain` { `ipv4` | `ipv6` | `eb` } `table`

返回表`table`中是否存在名为`chain`的链。此选项仅涉及之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--get-all-chains`

获取所有到所有表中的链。此选项仅涉及之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--get-chains` { `ipv4` | `ipv6` | `eb` } `table`

以空格分隔列表的形式获取添加到表`table`中的所有链。此选项仅涉及之前通过`--direct --add-chain`添加的链。

`[--permanent]` `--direct` `--add-chain` { `ipv4` | `ipv6` | `eb` } `table` `chain`

向表`table`添加一个名为`chain`的新链。确保已没有其他同名的链。

本地应用程序或服务如果以 root 身份运行（例如`libvirt`）或使用 PolicyKit 进行身份验证，则能够更改防火墙配置。通过此功能，管理员可以锁定防火墙配置，使得只有锁定白名单上的应用程序才能请求更改防火墙。

锁定（lockdown）访问检查限制了修改防火墙规则的 D-Bus 方法。查询、列表和获取方法不受限制。

锁定功能是 firewalld 用户和应用策略的轻量级版本，默认关闭状态。

`--lockdown-on`

启用锁定。请小心——如果你在启用锁定时，`firewall-cmd`不在锁定白名单中，你将无法通过`firewall-cmd`再次禁用它，而是需要编辑`firewalld.conf`。

这是一个运行时且永久的更改。

`--lockdown-off`

禁用锁定。

这是一个运行时且永久的更改。

`--query-lockdown`

查询是否已启用锁定。如果已锁定则返回 0，否则返回 1。

## 锁定白名单选项

锁定白名单可以包含`commands`（命令）、`contexts`（上下文）、`users`（用户）和`user ids`（用户 ID）。

如果白名单上的命令项以星号`*`结尾，则所有以该命令开头的命令行都将匹配。如果没有`*`，则必须匹配包含参数的绝对命令。

root 用户和其他用户的命令并不总是相同的。例如：在 Fedora 上，作为 root 身份使用`/bin/firewall-cmd`，而作为普通用户则使用`/usr/bin/firewall-cmd`。

上下文是运行的应用程序或服务的安全（SELinux）上下文。要获取运行应用程序的上下文，请使用`ps -e --context`。

**警告：** 如果上下文未受限制（unconfined），这将为目标应用程序之外的程序开放访问。

锁定白名单项按以下顺序检查：

1. `context`
2. `uid`
3. `user`
4. `command`

`--permanent` `--list-lockdown-whitelist-commands`

列出所有在白名单上的命令行。

`--permanent` `--add-lockdown-whitelist-command=command`

将`command`添加到白名单。

`--permanent` `--remove-lockdown-whitelist-command=command`

从白名单中移除`command`。

`--permanent` `--query-lockdown-whitelist-command=command`

查询`command`是否在白名单中。如果为真返回 0，否则返回 1。

`--permanent` `--list-lockdown-whitelist-contexts`

列出所有在白名单上的上下文。

`--permanent` `--add-lockdown-whitelist-context=context`

将上下文`context`添加到白名单。

`--permanent` `--remove-lockdown-whitelist-context=context`

从白名单中移除上下文`context`。

`--permanent` `--query-lockdown-whitelist-context=context`

查询上下文`context`是否在白名单中。如果为真返回 0，否则返回 1。

`--permanent` `--list-lockdown-whitelist-uids`

列出所有在白名单上的用户 ID。

`--permanent` `--add-lockdown-whitelist-uid=uid`

将用户 ID`uid`添加到白名单。

`--permanent` `--remove-lockdown-whitelist-uid=uid`

从白名单中移除用户 ID`uid`。

`--permanent` `--query-lockdown-whitelist-uid=uid`

查询用户 ID`uid`是否在白名单中。如果为真返回 0，否则返回 1。

`--permanent` `--list-lockdown-whitelist-users`

列出所有在白名单上的用户名。

`--permanent` `--add-lockdown-whitelist-user=user`

将用户名`user`添加到白名单。

`--permanent` `--remove-lockdown-whitelist-user=user`

从白名单中移除用户名`user`。

`--permanent` `--query-lockdown-whitelist-user=user`

查询用户名`user`是否在白名单中。如果为真返回 0，否则返回 1。

## 恐慌（Panic）选项

`--panic-on`

启用恐慌模式。所有入站和出站数据包将被丢弃，活动连接将超时。仅当网络环境出现严重问题时启用，例如机器正在被攻击。

这是一个运行时更改。

`--panic-off`

禁用恐慌模式。禁用恐慌模式后，如果恐慌模式仅开启了短时间，已建立的连接可能会恢复工作。

这是一个运行时更改。



`--query-panic`

如果启用了恐慌模式返回 0，否则返回 1。

## 示例

更多示例请参见`http://fedoraproject.org/wiki/FirewallD`。

### 示例 1

在默认区域中启用`http`服务。这仅是运行时更改，即生效直到重启。

```bash
firewall-cmd --add-service=http
```

### 示例 2

在默认区域中立即并永久地启用端口`443/tcp`。为了使更改立即生效并在重启后依然有效，我们需要两条命令。第一条命令在运行时配置中进行更改，即立即生效，直到重启。第二条命令在永久配置中进行更改，即重启后生效。

```bash
firewall-cmd --add-port=443/tcp
firewall-cmd --permanent --add-port=443/tcp
```

## 退出码

| 字符串 | 代码 |
| :--- | :--- |
| 0 | success |
| 1 | 失败 |
| 2 | 命令行用法错误 |
| 3 | 未运行 |
| 4 | 未授权 |
| 5 | 未知错误 |
| 6 | 无效族 |
| 7 | 审计类型 |
| 8 | 区域冲突 |
| 9 | 内置 |
| 10 | 无效 |
| 11 | 已启用 |
| 12 | 未启用 |
| 13 | 命令失败 |
| 14 | `ipv6` |
| 15 | 恐慌 |
| 16 | 已设置 |
| 17 | 接口 |
| 18 | 冲突 |
| 19 | 内置 |
| 20 | 转发 |
| 21 | 可加载 |
| 22 | 默认值 |
| 23 | 内置 |
| 24 | 内置 |
| 25 | `icmp`类型 |
| 26 | 上下文 |
| 27 | 不匹配 |
| 28 | 解析 |
| 29 | 访问拒绝 |
| 30 | 运行时到永久 |

`firewall-offline-cmd`是`firewalld`守护进程的离线命令行客户端。它应仅在`firewalld`服务未运行时使用。例如，从`system-config-firewall/lokkit`迁移，或者在安装环境中使用 kickstart 配置防火墙设置。

某些`lokkit`选项无法自动转换为`firewalld`，它们会导致错误或警告信息。此工具尝试尽可能进行转换，但在自定义规则、模块和地址伪装（masquerading）方面存在局限性。

在使用此工具后检查防火墙配置。

## 选项

如果没有提供选项，将从`/etc/sysconfig/system-config-firewall`配置配置。

支持以下选项。

### 帮助选项

`-h`、`--help`

打印简短帮助文本并退出。

### 状态选项

`--enabled`

启用防火墙。这是一个默认选项，只要没有给出`--disabled`选项，它将在防火墙尚未启用时激活防火墙。

`--disabled`

通过禁用`firewalld`服务来禁用防火墙。

### Lokkit 兼容性选项

这些选项与`lokkit`的选项几乎相同。

`--addmodule=*module`

此选项将导致警告信息并被忽略。

netfilter helpers 的处理已完全合并到服务中。因此，不再需要在服务外部添加或删除 netfilter helpers。有关如何在服务中处理 netfilter helpers 的更多信息，请参阅`firewalld.zone`(5)。

`--removemodule`

此选项将导致警告信息并被忽略。

netfilter helpers 的处理已完全合并到服务中。因此，不再需要在服务外部添加或删除 netfilter helpers。有关如何在服务中处理 netfilter helpers 的更多信息，请参阅`firewalld.zone`(5)。

`--remove-service=*service`

从默认区域中移除一个服务。此选项可以指定多次。

该服务是`firewalld`提供的服务之一。要获取支持的服务列表，请使用`firewall-cmd --get-services`。

`-s service`、`--service=*service`

向默认区域添加一个服务。此选项可以指定多次。

该服务是`firewalld`提供的服务之一。要获取支持的服务列表，请使用`firewall-cmd --get-services`。

`-p portid[-*portid*]:protocol`、`--port=*portid[-*portid*]:protocol`

向默认区域添加端口。此选项可以指定多次。

端口可以是单个端口号或端口范围`portid-portid`。协议可以是`tcp`或`udp`。

`-t interface`、`--trust=*interface`

此选项将导致警告信息。

将接口标记为受信任。此选项可以指定多次。该接口将绑定到信任区域。

如果该接口在 NetworkManager 管理的连接中使用，或者如果该接口有 ifcfg 文件，则该接口一旦被激活，其区域将更改为配置中定义的区域。要更改连接的区域，请使用`nm-connection-editor`并将区域设置为`trusted`；对于 ifcfg 文件，请使用编辑器并添加`ZONE=trusted`。如果 ifcfg 文件中未定义区域，则将使用`firewalld`默认区域。

`-m interface`、`--masq=*interface`

此选项将导致警告信息。

将在默认区域中启用内部地址伪装。接口参数将被忽略。这仅适用于`IPv4`。

`--custom-rules=[type:][[table:]*filename`

此选项将导致警告信息并被忽略。

`firewalld`不支持自定义规则文件。

`--forward-port=if=*interface*:port=*port*:proto=*protocol*[:toport=*destination port*][:toaddr=*destination address*]`

此选项将导致警告信息。

在默认区域中添加`IPv4`端口转发。此选项可以指定多次。

端口可以是单个端口号`portid`或端口范围`portid-portid`。协议可以是`tcp`或`udp`。目标地址是一个 IP 地址。

`--block-icmp=*icmptype`

此选项将导致警告信息。

在默认区域中为`icmptype`添加 ICMP 阻塞。此选项可以指定多次。

`icmptype`是`firewalld`支持的 icmp 类型之一。要获取支持的 icmp 类型列表，请使用`firewall-cmd --get-icmptypes`。

## 区域选项

`--get-default-zone`

打印连接和接口的默认区域。

`--set-default-zone=*zone`

为未选择区域的连接和接口设置默认区域。设置默认区域将更改使用默认区域的连接或接口的区域。

`--get-zones`

以空格隔开的列表形式打印预定义的区域。

`--get-services`

以空格隔开的列表形式打印预定义的服务。

`--get-icmptypes`

以空格隔开的列表形式打印预定义的 icmp 类型。

`--get-zone-of-interface=*interface`

打印`interface`绑定的区域名称或输出`no zone`。

`--get-zone-of-source=*interface`

打印`interface`绑定的区域名称或输出`no zone`。

`--list-all`

列出区域中添加或启用的所有内容。输出格式为：`interfaces:` `sources:` `services:` `ports:` `forward-ports:` `icmp-blocks:` `rich-rules:`。

`--new-zone=*zone`

添加一个新的永久区域。

`--delete-zone=*zone`

删除一个永久区域。

`--get-target=*zone`

获取永久区域的策略。

`--set-target=*zone`

设置永久区域的策略。

## 适配和查询区域的选项

此类选项仅影响特定区域。如果配合`--zone=*zone`使用，它们将影响`zone`。如果省略该选项，它们将影响默认区域（参见`--get-default-zone`）。

`--list-all`

列出区域中添加或启用的所有内容。如果省略区域，将使用默认区域。

`--list-services`

以空格隔开的列表打印`zone`添加的服务。如果省略区域，将使用默认区域。

`--add-service=*service`

为`zone`添加服务。如果省略区域，将使用默认区域。此选项可以指定多次。

该服务是`firewalld`提供的服务之一。要获取支持的服务列表，请使用`firewall-cmd --get-services`。

`--remove-service-from-zone=*service`

从`zone`移除服务。此选项可以指定多次。如果省略区域，将使用默认区域。

`--query-service=*service`

查询`service`是否已添加到`zone`。如果省略区域，将查询默认区域。真则返回 0，否则返回 1。

`--list-ports`

以空格隔开的列表打印`zone`添加的端口。端口格式为`portid[-portid]/protocol`，可以是端口协议对或带有协议的端口范围。如果省略区域，将使用默认区域。

`--add-port=*portid[-*portid*]/protocol`

为`zone`添加端口。如果省略区域，将使用默认区域。此选项可以指定多次。

`--remove-port=*portid[-*portid*]/protocol`

从`zone`移除端口。如果省略区域，将使用默认区域。此选项可以指定多次。

`--query-port=*portid[-*portid*]/protocol`

查询端口是否已添加到`zone`。如果省略区域，将查询默认区域。真则返回 0，否则返回 1。

返回`zone`是否已添加该端口。如果省略`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

`--zone=*zone`、`--list-icmp-blocks`

以空格分隔的列表形式列出`zone`添加的互联网控制消息协议（ICMP）类型块。如果省略`zone`，将使用默认区域。

`--zone=*zone`、`--add-icmp-block=*icmptype`

为`zone`添加针对`icmptype`的 ICMP 块。如果省略`zone`，将使用默认区域。此选项可以指定多次。

`icmptype`是`firewalld`支持的 icmp 类型之一。要获取支持的 icmp 类型列表，请执行：`firewall-cmd --get-icmptypes`。

`--zone=*zone`、`--remove-icmp-block=*icmptype`

从`zone`中移除针对`icmptype`的 ICMP 块。如果省略`zone`，将使用默认区域。此选项可以指定多次。

`--zone=*zone`、`--query-icmp-block=*icmptype`

返回`zone`是否已添加针对`icmptype`的 ICMP 块。如果省略`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

`--zone=*zone`、`--list-forward-ports`

以空格分隔的列表列出`zone`添加的`IPv4`转发端口。如果省略`zone`，将使用默认区域。

对于`IPv6`转发端口，请使用富规则（rich language）。

`--zone=*zone`、`--add-forward-port=port=*portid*[-*portid*]:proto=*protocol*[:toport=*portid*[-*portid*]][:toaddr=*address*[/*mask*]]`

为`zone`添加`IPv4`转发端口。如果省略`zone`，将使用默认区域。此选项可以指定多次。

端口可以是单个端口号`portid`或端口范围`portid-portid`。协议可以是`tcp`或`udp`。目标地址是一个简单的 IP 地址。

对于`IPv6`转发端口，请使用富规则（rich language）。

`--zone=*zone`、`--remove-forward-port=port=*portid*[-*portid*]:proto=*protocol*[:toport=*portid*[-*portid*]][:toaddr=*address*[/*mask*]]`

从`zone`中移除`IPv4`转发端口。如果省略`zone`，将使用默认区域。此选项可以指定多次。

对于`IPv6`转发端口，请使用富规则（rich language）。

`--zone=*zone`、`--query-forward-port=port=*portid*[-*portid*]:proto=*protocol*[:toport=*portid*[-*portid*]][:toaddr=*address*[/*mask*]]`

返回`zone`是否已添加`IPv4`转发端口。如果省略`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

对于`IPv6`转发端口，请使用富规则（rich language）。

`--zone=*zone`、`--add-masquerade`

启用`zone`的`IPv4`伪装（masquerade）。如果省略`zone`，将使用默认区域。如果该机器是路由器，且连接到另一个区域接口的机器应该能够使用第一个连接，则伪装非常有用。

对于`IPv6`伪装，请使用富规则（rich language）。

`--zone=*zone`、`--remove-masquerade`

禁用`zone`的`IPv4`伪装。如果省略`zone`，将使用默认区域。

对于`IPv6`伪装，请使用富规则（rich language）。

`--zone=*zone`、`--query-masquerade`

返回`zone`是否已启用`IPv4`伪装。如果省略`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

对于`IPv6`伪装，请使用富规则（rich language）。

`--zone=*zone`、`--list-rich-rules`

以换行符分隔的列表列出`zone`添加的富规则。如果省略`zone`，将使用默认区域。

`--zone=*zone`、`--add-rich-rule='*rule*'`

为`zone`添加富规则`rule`。此选项可以指定多次。如果省略`zone`，将使用默认区域。

关于富规则的语法，请参阅`firewalld.richlanguage`(5)。

`--zone=*zone`、`--remove-rich-rule='*rule*'`

从`zone`中移除富规则`rule`。此选项可以指定多次。如果省略`zone`，将使用默认区域。

关于富规则的语法，请参阅`firewalld.richlanguage`(5)。

`--zone=*zone`、`--query-rich-rule='*rule*'`

返回`zone`是否已添加富规则`rule`。如果省略`zone`，将使用默认区域。如果为真返回 0，否则返回 1。

关于富规则的语法，请参阅`firewalld.richlanguage`(5)。

## 处理接口绑定的选项

将接口绑定到区域意味着将使用该区域设置。（注：源文件文本似乎是碎片化的，但保持了结构。）

## 处理源绑定的选项

将源（source）绑定到区域意味着将使用该区域设置来限制流量。源地址或地址范围对于 IPv4 是 IP 地址或带有掩码的网络 IP 地址。对于 IPv6，掩码是一个纯数字。不支持主机名。

本节中的选项仅影响一个特定的区域。如果配合`--zone`选项使用，它们将影响该区域。如果省略该选项，它们将影响默认区域。

直接选项提供了对防火墙的更直接访问。这些选项要求用户了解基本的`iptables`概念，即`table`（filter/mangle/nat/...）、`chain`（INPUT/OUTPUT/FORWARD/...）、`commands`（-A/-D/-I/...）、`parameters`（-p/-s/-d/-j/...）以及`targets`（ACCEPT/DROP/REJECT/...）。

只有在无法使用例如`--add-service=*service*`或`--add-rich-rule='*rule*'`的情况下，才应将直接选项作为最后的手段。

每个选项的第一个参数必须是`ipv4`、`ipv6`或`eb`。使用`ipv4`时针对 IPv4（`iptables`(8)），使用`ipv6`时针对 IPv6（`ip6tables`(8)），使用`eb`时针对以太网桥接（`ebtables`(8)）。

### `--direct --get-all-chains`

获取所有到所有表中的链（chains）。

此选项仅涉及之前通过`--direct --add-chain`添加的链。

### `--direct --get-chains` { `ipv4` | `ipv6` | `eb` } `table`

以空格分隔的列表形式获取所有添加到表`table`中的链。

此选项仅涉及之前通过`--direct --add-chain`添加的链。



### `--direct --add-chain` {`ipv4` | `ipv6` | `eb`} `table` `chain`

在表 `table` 中添加一个名为 `chain` 的新链。

已经存在一些用于直接选项的基础链，例如 `INPUT_direct` 链（查看 `iptables-save | grep direct` 输出以获取所有链）。这些链在区域（zones）链之前被跳转，这意味着放入 `INPUT_direct` 的每条规则都将在区域规则之前被检查。

### `--direct --remove-chain` {`ipv4` | `ipv6` | `eb`} `table` `chain`

从表 `table` 中删除名为 `chain` 的链。

### `--direct --query-chain` {`ipv4` | `ipv6` | `eb`} `table` `chain`

返回表 `table` 中是否存在名为 `chain` 的链。如果为真返回 0，否则返回 1。

此选项仅涉及之前通过 `--direct --add-chain` 添加的链。

### `--direct --get-all-rules`

以优先级和参数的换行分隔列表形式，获取添加到所有表中所有链中的所有规则。

### `--direct --get-rules` {`ipv4` | `ipv6` | `eb`} `table` `chain`

以优先级和参数的换行分隔列表形式，获取添加到表 `table` 中链 `chain` 中的所有规则。

### `--direct --add-rule` {`ipv4` | `ipv6` | `eb`} `table` `chain` `priority` `args`

在表 `table` 的链 `chain` 中以优先级 `priority` 添加带有参数 `args` 的规则。

`priority` 用于对规则进行排序。优先级 0 表示将规则添加到链的顶部，优先级越高，规则添加的位置越靠后。相同优先级的规则处于同一层，这些规则的顺序是不固定的并且可能会发生。如果你想确保某条规则在另一条规则之后添加，请为第一条规则使用低优先级，为后续规则使用高优先级。

### `--direct --remove-rule` {`ipv4` | `ipv6` | `eb`} `table` `chain` `priority` `args`

从表 `table` 的链 `chain` 中删除具有优先级 `priority` 和参数 `args` 的规则。

### `--direct --remove-rules` {`ipv4` | `ipv6` | `eb`} `table` `chain`

删除表 `table` 中名为 `chain` 的链中的所有规则。

此选项仅涉及之前在此链中通过 `--direct --add-rule` 添加的规则。

### `--direct --query-rule` {`ipv4` | `ipv6` | `eb`} `table` `chain` `priority` `args`

返回表 `table` 的链 `chain` 中是否存在具有优先级 `priority` 和参数 `args` 的规则。如果为真返回 0，否则返回 1。

### `--direct --get-all-passthroughs`

以 `ipv` 值和参数的换行分隔列表形式，获取所有永久直通（passthroughs）。

### `--direct --get-passthroughs` {`ipv4` | `ipv6` | `eb`}

以优先级和参数的换行分隔列表形式，获取对应 `ipv` 值的永久直通规则。

### `--direct --add-passthrough` {`ipv4` | `ipv6` | `eb`} `args`

为 `ipv` 值添加带有参数 `args` 的永久直通规则。

### `--direct --remove-passthrough` {`ipv4` | `ipv6` | `eb`} `args`

为 `ipv` 值删除带有参数 `args` 的永久直通规则。

### `--direct --query-passthrough` {`ipv4` | `ipv6` | `eb`} `args`

返回是否存在对应 `ipv` 值的参数 `args` 的永久直通规则。如果为真返回 0，否则返回 1。

## 锁定选项（Lockdown Options）

本地应用程序或服务如果以 root 运行（例如：`libvirt`）或使用 PolicyKit 验证，则能够更改防火墙配置。通过此功能，管理员可以锁定防火墙配置，使得只有白名单上的应用程序能够请求防火墙更改。

锁定访问检查限制了更改防火墙规则的 D-Bus 方法。

### 锁定（Lockdown）

开启锁定。请小心——锁定后 `firewall-cmd` 将无法更改防火墙配置。通过此功能，管理员可以锁定防火墙配置，使得只有白名单上的应用程序能够请求防火墙更改。

查询是否锁定。如果为真返回 0，否则返回 1。

### 锁定白名单选项（Lockdown Whitelist Options）

锁定白名单可以包含命令（commands）、上下文（contexts）和用户（users）。

锁定项按以下顺序检查：

1. `context`
2. `uid`
3. `user`
4. `command`

### `--list-lockdown-commands`

列出白名单中的所有命令。

### `--add-lockdown-whitelist-command`=`command`

向白名单添加命令 `command`。

### `--remove-lockdown-whitelist-command`=`command`

从白名单中删除命令 `command`。

### `--query-lockdown-whitelist-command`=`command`

查询命令 `command` 是否在白名单中。如果为真返回 0，否则返回 1。

### `--list-lockdown-contexts`

列出白名单中的所有上下文。

### `--add-lockdown-whitelist-context`=`context`

向白名单添加上下文 `context`。

### `--remove-lockdown-whitelist-context`=`context`

从白名单中删除上下文 `context`。

### `--query-lockdown-whitelist-context`=`context`

查询上下文 `context` 是否在白名单中。如果为真返回 0，否则返回 1。

### `--list-lockdown-uids`

列出白名单中的所有用户 ID。

### `--add-lockdown-whitelist-uid`=`uid`

向白名单添加用户 ID `uid`。

### `--remove-lockdown-whitelist-uid`=`uid`

从白名单中删除用户 ID `uid`。

### `--query-lockdown-whitelist-uid`=`uid`

查询用户 ID `uid` 是否在白名单中。如果为真返回 0，否则返回 1。

### `--list-lockdown-users`

列出白名单中的所有用户名。

**警告：** 如果上下文是未限制的（unconfined），这将开放比目标应用程序更多的访问权限。

### `--add-lockdown-whitelist-user`=`user`

向白名单添加用户名 `user`。

### `--remove-lockdown-whitelist-user`=`user`

从白名单中删除用户名 `user`。

### `--query-lockdown-whitelist-user`=`user`

查询用户名 `user` 是否在白名单中。如果为真返回 0，否则返回 1。

## 策略选项（Policy Options）

`--policy-server`

将 PolicyKit 策略更改为“server”（更严格）。

`--policy-desktop`

将 PolicyKit 策略更改为“desktop”（较宽松）。

## 参见

`firewall-applet`(1)、`firewalld`(1)、`firewall-cmd`(1)、`firewall-config`(1)、`firewalld.conf`(5)、`firewalld.direct`(5)、`firewalld.icmptype`(5)、`firewalld.lockdown-whitelist`(5)、`firewall-offline-cmd`(1)、`firewalld.richlanguage`(5)、`firewalld.service`(5)、`firewalld.zone`(5)、`firewalld.zones`(5)

## Notes

firewalld 主页：

`http://www.firewalld.org`

更多带有示例的文档：

`http://fedoraproject.org/wiki/FirewallD`

## 作者

**Thomas Woerner** <twoerner@redhat.com>

开发者

**Jiri Popelka** <jpopelka@redhat.com>

开发者

# FIREWALLD

## 名称

`firewalld` - 动态防火墙管理器

## 概要

`firewalld` `[OPTIONS...]`

## 描述

`firewalld` 提供了一个动态管理的防火墙，支持通过网络/防火墙区域（zones）来定义网络连接或接口的信任级别。它支持 IPv4、IPv6 防火墙设置以及以太网桥接，并将运行时配置和永久配置选项分离。它还支持服务或应用程序直接添加防火墙规则的接口。

### 选项

这些是 `firewalld` 的命令行选项：

`-h`、`--help`

打印简短帮助文本并退出。

`--debug`=`level`

将 `firewalld` 的调试级别设置为 `level`。调试级别的范围从 1（最低级别）到 10（最高级别）。调试输出将被写入 `firewalld` 日志文件 `/var/log/firewalld`。

`--debug-gc`

打印垃圾回收器泄漏信息。收集器每 10 秒运行一次，如果有泄漏，将打印有关泄漏的信息。

`--nofork`

关闭守护进程派叉。强制 `firewalld` 作为前台进程运行，而不是作为后台守护进程。

`--nopid`

禁用写入 pid 文件。默认情况下，程序会写入 pid 文件。如果使用此选项调用程序，它将不会检查已存在的服务器进程。

## 概念

`firewalld` 有一个 D-Bus 接口用于服务和应用程序的防火墙配置。它还为用户提供命令行客户端。已使用 D-Bus 的服务或应用程序可以通过 D-Bus 接口直接请求防火墙。有关 `firewalld` D-Bus 接口的更多信息，请参阅 `firewalld.dbus`(5)。

`firewalld` 支持区域、预定义服务和 ICMP 类型，并将运行时和永久配置选项分离。永久配置从 `/usr/lib/firewalld` 或 `/etc/firewalld` 中的 XML 文件加载（参见“目录”章节）。

如果没有使用 NetworkManager，则存在一些局限性：`firewalld` 将无法获取网络设备重名的通知。如果 `firewalld` 在网络启动后启动，连接和手动创建的接口将不会绑定到区域。你可以通过 `firewall-cmd [--permanent] --zone=zone --add-interface=interface` 将它们添加到区域，但请确保如果存在 `/etc/sysconfig/network-scripts/ifcfg-*interface`，其中指定的 `ZONE=zone` 区域是相同的（或者默认区域都为空/缺失），否则行为将未定义。

### 区域（Zones）

网络或防火墙区域定义了用于连接的接口的信任级别。`firewalld` 提供了多个预定义区域。区域配置选项和关于区域的通用信息在 `firewalld.zone`(5) 中描述。

### 服务（Services）

可以是本地端口和目的地的列表，此外当启用服务时自动加载的防火墙辅助模块列表。服务配置选项和关于服务的通用信息在 `firewalld.service`(5) 中描述。使用预定义服务使用户更容易启用和禁用对某个服务的访问。

### ICMP 类型（ICMP types）

互联网控制消息协议（ICMP）用于在互联网协议（IP）中交换信息和错误消息。ICMP 类型可用于 `firewalld` 以限制此类消息的交换。欲了解更多信息，请参阅 `firewalld.icmptype`(5)。

### 运行时配置（Runtime configuration）

运行时配置是实际生效的配置，不是永久的。在服务加载、重启或系统重启后，如果运行时设置未包含永久配置中，它们将会消失。

### 永久配置（Permanent configuration）

永久配置存储在配置文件中，并在每次机器启动或服务加载、重启时加载并成为新的运行时配置。

### 直接接口（Direct interface）

直接接口主要用于服务或应用程序添加特定的防火墙规则。它需要具备 `ip(6)tables` 的基本知识（表、链、命令、参数、目标）。

## 目录（DIRECTORIES）

`firewalld` 支持两个配置目录：

### `/usr/lib/firewalld` 中的默认/回备配置

此目录包含 `firewalld` 为 `icmptypes`、服务和区域提供的默认和回备配置。`firewalld` 包提供的文件不应被更改，更改在更新 `firewalld` 包后将消失。可以提供额外的 `icmptypes`、`services` 和 `zones`。

### `/etc/firewalld` 中的系统配置

存储在此处的系统配置由系统管理员或用户创建。这些文件将覆盖默认配置。

## 信号（SIGNALS）

目前仅支持 `SIGHUP`。

### `SIGHUP`

重新加载完整配置。你也可以使用 `firewall-cmd --reload`。所有运行时设置将根据配置文件定义的选项进行恢复。

## 参见（SEE ALSO）



# 概述

`firewall-applet`(1), `firewalld`(1), `firewall-cmd`(1), `firewall-config`(1), `firewalld.conf`(5), `firewalld.direct`(5), `firewalld.icmptype`(5), `firewalld.lockdown-whitelist`(5), `firewall-offline-cmd`(1), `firewalld.richlanguage`(5), `firewalld.service`(5), `firewalld.zone`(5), `firewalld.zones`(5)

当使用 `-n` 选项且存在冲突锁，或使用 `-w` 选项且达到超时时间时所使用的退出码。默认值为 `1`。

# 选项

`-e`, `-x`, `--exclusive`

获取排他锁，有时也称为写锁。这是默认选项。

`-n`, `--nb`, `--nonblock`

如果无法立即获取锁，则失败而不是等待。查看 `-E` 选项了解使用的退出码。

`-o`, `--close`

在执行 `command` 之前关闭持有锁的文件描述符。如果 `command` 产生了一个不应持有锁的子进程，则此用非常有用。

`-s`, `--shared`

获取共享锁，有时也称为读锁。

`-u`, `--unlock`

释放锁。这通常不需要，因为锁在文件关闭时会自动释放。然而，在特殊情况下可能需要这样做，例如，如果包含的命令组可能派生了一个不应持有锁的后台进程。

`-w`, `--wait`, `--timeout` `seconds`

如果在 `seconds` 内无法获取锁，则失败。允许使用小数分值。查看 `-E` 选项了解使用的退出码。`seconds` 的数字 0 被解释为 `--nonblock`。

`--verbose`

报告获取锁所需的时间，或者为什么无法获取锁。

`-V`, `--version`

显示版本信息并退出。

`-h`, `--help`

显示帮助文本并退出。

# 示例

```
shell1> flock /tmp -c cat
```

```
shell2> flock -w .007 /tmp -c echo; /bin/echo $? 为目录 /tmp 设置了排他锁，第二个命令将失败。
```

```
shell1> flock -s /tmp -c cat
```

```
shell2> flock -s -w .007 /tmp -c echo; /bin/echo $? 为目录 /tmp 设置了共享锁，第二个命令不会失败。注意，尝试用第二个命令获取排他锁将失败。
```

```
shell> flock -x local-lock-file echo 'a b c'
```

在运行带有 'a b c' 的 `echo` 之前，获取排他锁 `local-lock-file`。

```
(
  flock -n 9 || exit 1
  # ... 在锁下执行的命令 ... ) 9>/var/lock/mylockfile
```

这种形式在 shell 脚本内部非常方便。打开文件的模式对 `flock` 来说并不重要；使用 `>` 或 `>>` 允许在锁文件不存在时创建它，然而，这需要写权限。使用 `<` 则要求文件已存在，但只需要读权限。

```
[ "${FLOCKER}" != "$0" ] && exec env FLOCKER="$0" flock -en "$0" "$0" "$@" || :
```

这是 shell 脚本中非常有用的样板代码。将其置于想要锁定的 shell 脚本的顶部，它将在首次运行时自动锁定自己。如果环境变 `$FLOCKER` 未被设置为正在运行的 shell 脚本，则执行 `flock` 并获取一个排他非阻塞锁（使用脚本本身作为锁文件），然后使用正确的参数重新执行自身。它还会将 `FLOCKER` 环境变量设置为正确的值，以确保它不会再次运行。

# 退出状态

该命令对所有情况都使用 `sysexits.h` 返回值，但使用选项 `-n` 或 `-w` 时除外，它们会通过 `-E` 选项提供的返回值报告获取锁失败，默认值为 `1`。

当使用 `command` 变体且执行子命令成功时，退出状态即为子命令的退出状态。

# 作者

H. Peter Anvin

# 版权

Copyright Š 2003-2006 H. Peter Anvin.

这是一项免费软件；复制条件请参见源代码。本没有任何保证；即使对于商品性或特定用途的适用性。

# 参见

`flock`(2)

# 可用性

`flock` 命令是 util-linux 软件包的一部分，可从 Linux 内核存档获取。

---

# FMT

## 名称

fmt - 简单的最优文本格式化工具

## 用法简述

`fmt` `[-WIDTH]` `[*OPTION]`... `[*FILE]`...

## 描述

重新格式化 `FILE(s)` 中的每个段落，并写入标准输出。选项 `-WIDTH` 是 `--width=*DIGITS` 的缩写。

在无 `FILE` 或当 `FILE` 为 `-` 时，读取标准输入。

长选项的强制性参数对于短选项也是强制性的。

`-c`, `--crown-margin`

保留前两行的缩进

`-p`, `--prefix=*STRING`

仅重新格式化以 `STRING` 开头的行，并将前缀重新到重新格式化的行上。

`-s`, `--split-only`

拆分长行，但不重新填充内容。

`-t`, `--tagged-paragraph`

第一行的缩进与第二行不同

`-u`, `--uniform-spacing`

单词之间留一个空格，句末后留两个空格

`-w`, `--width=*WIDTH`

最大行宽（默认为 75 列）

`-g`, `--goal=*WIDTH`

目标宽度（默认为 75）

`--help`

显示帮助并退出

`--version`

输出版本

## 作者

由 Ross Paterson 编写

## 缺陷

向 <http://gnu.org/bugzilla/> 报告缺陷；...

## 版权

Copyright Š 2015-2023 Free Foundation, Inc。这是一项免费软件；根据自由通用许可证发布。您可以在更多信息中查阅许可证（http://gnu.org/licenses/）。

## 参见

`fmt`

## 可用性

`fmt` 命令是 GNU Coreutils 的一部分。

## 版权

Copyright Š 2015-2023 Free Foundation, Inc。这是一项免费软件；根据自由通用许可证发布。您可以在更多信息中查阅许可证（http://gnu.org/licenses/）。

---

# FONT2C

## 名称

font2c - 将 PostScript Type 0 字体转换为 C

## 用法简述

**font2c** *font*

## 描述

该脚本调用 `gs`(1) 并传入以下参数：

`-q -dWRITESY`

随后是命令行。

## 参见

`gs`(1)

## 版本

本文最后修订于 Ghostscript 9.16。

## 作者

Artifex Software, Inc. 是 Ghostscript 的主要维护者。

---

# FONTTOSNT

## 名称

fonttosnt - 将位图字体封装为 sfnt (TrueType)

## 用法简述

**fonttosnt** [ *options* ] `-o` *file.ttf* [ **** ] *font*

## 描述

将位图字体或一组位图字体封装为 sfnt (TrueType)。

## 选项

`-v`

详细模式

`-c`

不裁剪。通常会增加文件大小，但对于终端字体有时可以稍微缩小文件大小。

`-b`

写入字节对齐字形。默认写入未对齐的数据。

`-r`

不重新编码字体。默认尽可能重新编码。

`-g` *n*

设置我们写入的可缩放字体类型。如果 *n* 为 0，则不写入可缩放字体；这是合法的，但会让大多数软件困惑。如果 *n* 为 1，则写入单个可缩放字体（未定义字体），对其他字体仅写入左边距值。如果 *n* 为 2（默认），则写入所有可缩放字体，这会增加文件大小且不建议这样做。

`-m` *n*

设置我们写入的可缩放指标。如果 *n* 为 0，则不写入可缩放指标，这可能合法也可能非法。如果 *n* 为 1，则写入单个字体的完整指标，对其他字体仅写入左边距。如果 *n* 为 2，则写入所有字体的缩放指标，这会增加文件大小且不建议这样做。默认值为 1。

`--`

选项结束。

## 缺陷

某些字体级值，特别是上下标标位置，是虚拟值。

## 参见

X(7), Xserver(1), Xft(3x). *X11 中的字体.*

## 作者

包含在此 X.Org Foundation 发布中的 **Fontftsnt** 版本最初由 Juliusz Chroboczek <jch@freedesktop.org> 为 XFree86 项目编写。

---

`foomatic-cleanupdrivers` 命令会删除所有命令行为空的驱动 XML 文件。

该命令不 intended 供用户直接调用。

# FOOMATIC-COMBO-XML

## 名称

`foomatic-combo-xml` - <在此处输入简短描述>

## 概要

`foomatic-combo-xml` `[OPTION]`...

## 描述

这是由用 C 语言编写的 Foomatic 加速引擎，它可以计算打印机/驱动组合 XML 文件以及打印机概览 XML 文件。

## 退出状态

`foomatic-combo-xml` 返回 ???

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 为 foomatic 项目，使用了关联二进制文件的输出。

## 缺陷

此帮助页面需要编辑。

请在以下地址发布错误报告：

http://lists.freestandards.org/mailman/listinfo/printing-foomatic

# FOOMATIC-COMPILEDB

## 名称

`foomatic-compiledb` - 编译 Foomatic 打印机/驱动数据库

## 概要

`foomatic-compiledb` `[-t type]` `[-f]` `[-j n]` `[driver ...]`

## 描述

`foomatic-compiledb` 为所有可能的打印机/驱动组合生成所有 PPD 文件或 Foomatic 组合 XML 文件，或仅为选定的驱动范围生成。除非想要生成一组用于分发的 Foomatic 数据文件，否则通常不需要。对于配置单台打印机，`foomatic-ppdfile(1)` 尤其是 `foomatic-configure(1)` 会自动计算它们所需的内容。

### 选项

`-t type`

输出文件类型，ppd 或 xml。

`-f`

强制：即使目标目录已存在也写入其中。

`-j n`

n = 运行的工作进程数量

`driver ...`

仅为这些驱动生成数据文件

## 另参

`foomatic-ppdfile(1)`, `foomatic-configure(1)`

## 退出状态

除非发生意外情况，否则 `foomatic-compiledb` 返回 0。

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 和 Till Kamppeter `<till.kamppeter@gmail.com>` 为 foomatic 项目，使用了关联二进制文件的输出。

## 缺陷

现有文件始终会被保留，而不是覆盖旧文件。因此建议删除目标目录（`rm -rf dir`）并在不带 `-f` 选项的情况下调用 `foomatic-compiledb`。

请在以下地址发布错误报告：

http://lists.freestandards.org/mailman/listinfo/printing-foomatic

# FOOMATIC-CONFIGURE

## 名称

`foomatic-configure` - foomatic 打印系统的的主配置程序。

## 概要

`foomatic-configure` `[OPTION]`...

`foomatic-configure -n queuename` `[-N description]` `[-L location]` `[-c connect]` `[-d driver]` `[-p printer]` `[ppd ppdfile]` `[-s spooler]` `[-C [sourcespooler] sourcequeue]` `[-o option1=value1 -o...]` `[-q]` `foomatic-configure -D -n queuename` `[-s spooler]` `[-q]`

`foomatic-configure -R -n queuename` `[-s spooler]` `[-q]`

`foomatic-configure -Q [-s spooler]` `[-n queuename]` `[-r]`

`foomatic-configure -P [-s spooler]` `[-n queuename]` `[-d driver]` `[-p printer]` `[--ppd ppdfile]` `[index]`

`foomatic-configure -p printer | -d driver | -p printer -d driver*`

`foomatic-configure -O`

`foomatic-configure -h`

`foomatic-configure --help`

## 描述

`foomatic-configure` 是一个用于为每个已知的后台（CUPS, LPRng, LPD, PPR, PDQ, direct）以及 Foomatic 数据库中的每个打印机/驱动组合或每个 PostScript PPD 文件设置和配置打印队列的程序。由于 RIP 过滤器（光栅图像处理器，从 PostScript 到打印机原生语言的转换）始终使用 `foomatic-rip(1)`，除了 CUPS 或 PPR 下的 PostScript 打印机的 PPD 文件外，它们将在不使用 RIP 过滤器的情况下使用。它还包含了用户工具的一半 API：你可以学习并控制关于打印队列静态属性的所有信息。配合兄弟程序 `foomatic-printjob(1)`，你可以执行与打印队列动态状态相关的一切：提交作业、查询、取消、重新排序和重定向。

### 选项

`-n queuename`

配置此打印队列

`-N Name/Description`

使用此可读的名称/描述

`-L Location`

描述此打印机位置的短语

`-c connection`

打印机连接至 `/dev/lp`

`-d driver`

所需驱动的 Foomatic 数据库名称

`-p printer`

打印机的 Foomatic ID

`--ppd ppdfile`

PPD 文件，例如由 PostScript 打印机制造商提供的文件

`-s spooler`

显式后台类型（cups, lpd, prng, pdq, ppr, direct）

`-o option=value`

将选项的默认 own 值

`-o option`

默认开启

`-D`

将此队列设置为默认队列（只需提供 `-n`）

`-R`

完全移除此队列（只需提供 `-n`）

`-C [sourcespooler] sourcequeue`

从后台复制源队列（如果未提供后台，则使用当前的）

`-Q`

查询现有配置（提供 XML）

`-r`

列出定义的队列（仅限 CUPS）

`-P [index]`

获取当前配置的 Perl dump（如果未提供 index，则显示所有）

`-O`

打印已知打印机/驱动的 XML 概览（这显示打印机的 ID）

`-X`

打印 `-p printer` 或 `-d driver` 的数据

`-q`

静默运行

### 命令

无命令，仅选项

## 另参

`foomatic-printjob(1)`, `foomatic-rip(1)`

## 退出状态

如果没有发生错误，`foomatic-configure` 返回 0。

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 为 foomatic 项目，使用了源文件。

## 缺陷

`foomatic-configure` 目前无法处理 `lprng` 风格的 printcap 文件。由于 `lprng` 使用 BSD 风格的 printcaps，只要不使用 GUI 打印管理器 `lprngtool`，这并不是太大的问题。这些格式之间的区别在于，BSD 风格要求打印定义中的延续行以冒号结尾，并用反斜杠转义换行符。`pr` 没有这种限制。



在使用 `lprngtool` 生成或编辑的 `printcap` 文件配合 `foomatic-configure` 时，需要在每个打印定义的最后一行末尾添加 `:\`，如下所示：

`#comment # primary printer name lp #alternate names |lp2|lp3 |Example of a printer :sd=/usr/spool/LPD/lp :rw=/dev/lp:mx#100 :`

必须转换为：

`#comment # primary printer name lp\ |lp2|lp3\ |Example of a printer\ :sd=/usr/spool/LPD/lp:\ :rw=/dev/lp:mx#100:`

此帮助页面可能已过期。

# FOOMATIC-PPDFILE

## 名称

`foomatic-ppdfile` - 为指定的打印机/驱动组合生成 PPD 文件

## 概要

`foomatic-ppdfile [-w] [-d <driver>] -p <printerid>`

`foomatic-ppdfile [-A] [-P pattern]`

`foomatic-ppdfile -h`

## 描述

`foomatic-ppdfile` 的第一形式用于为 Foomatic 数据库中任何有效的打印机/驱动组合计算与后台无关的 Foomatic PPD 文件，既可用于 `foomatic-rip(1)` 打印，也可用于应用程序/客户端访问打印机选项。PPD 文件在标准输出上返回。如果未指定驱动，则使用默认驱动。

`foomatic-ppdfile` 程序的第二形式将搜索打印机数据库并返回所有打印机条目，或名称和/或模型信息匹配正则表达式的条目。

最后一种形式打印帮助信息并退出。

### 选项

`-d drivername`

要使用的可选驱动程序名称。如果未提供驱动名称，则使用打印机兼容驱动列表中的默认或第一个驱动。

`-p`

`printer id` 打印机 ID。

`-w`

返回符合 Microsoft Windows 格式限制的 PPD 文件。

`-A`

返回数据库中所有的打印机条目。

`-P pattern`

返回数据库中匹配正则表达式的所有打印机条目。

## 参见

`foomatic-rip(1)`

## 退出状态

`foomatic-ppdfile` 成功时返回 0，否则返回 1。

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 为 foomatic 项目编写，使用了相关二进制文件的输出。

由 Patrick Powell `<papowell at astart.com>` 修改和更新。

## 缺陷

目前为止没有。

请在以下地址发布 Bug 报告：

`http://lists.freestandards.org/mailman/listinfo/printing-foomatic`

# FOOMATIC-EXTRACT-TEXT

## 名称

`foomatic-extract-text` - 从 Foomatic UI 字符串生成 `.po` 文件

## 概要

`foomatic-extract-text`

## 描述

`foomatic-extract-text` 命令从当前安装的 Foomatic 数据库中的 UI 字符串生成 `.po` 文件。

它不供用户直接调用。

# FOOMATIC-FIX-XML

## 名称

`foomatic-fix-xml` - 删除 Foomatic 数据库开头的空行

## 概要

`foomatic-fix-xml` `[DBDIR]`

## 描述

如果你针对 `libxml` 1.x 编译了 `foomatic-perl-data`，并且拥有带有开头空行的旧数据库条目，请使用 `foomatic-fix-xml` 命令。

# FOOMATIC-NONUMERICALIDS

## 名称

`foomatic-nonumericalids` - 将数字型打印机 ID 转换为文本 ID

## 概要

`foomatic-nonumericalids`

## 描述

此脚本将已安装的 Foomatic 数据库中所有旧的加密数字打印机 ID 转换为明文打印机 ID。

你可能不需要执行此操作。

# FOOMATIC-PERL-DATA

## 名称

`foomatic-perl-data` - 从 XML 生成 Perl 数据结构

## 概要

`foomatic-perl-data [-O] [-C] [-P] [-D] [-o option=setting] [-o ...] [-v] [filename]`

### 选项

`-O`

解析概述 XML 数据。

`-C`

解析打印机/驱动组合 XML 数据（默认）。

`-P`

解析打印机条目 XML 数据。

`-D`

解析驱动条目 XML 数据。

`-o option=setting`

生成的 Perl 数据的默认选项设置（仅限组合）。

`-v`

详细（调试）模式。

`filename`

从文件而非标准输入读取输入。

## 退出状态

`foomatic-perl-data` 返回 ...

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 为 foomatic 项目编写，使用了相关二进制文件的输出。

## 缺陷

此帮助手册页需要编辑。

# FOOMATIC-PPD-OPTIONS

## 名称

`foomatic-ppd-options` - 显示 PPD 选项

## 概要

`foomatic-ppd-options [-d=debuglevel] [ ppdfiles]`

## 描述

`foomatic-ppd-options` 程序读取指定的 PPD 文件或 `stdin` 并解码 PPD 文件以生成选项列表。这实际上只是其他打印配置工具的文本版本。

输出格式由一组行组成，每行都以一个关键字开头，后跟一组选项和默认值。例如：

`makemodel = Tektronix Phaser 350 Foomatic/Postscript (recommended) name=PageSize; default=Letter; options=Letter (US Letter), \ A4 (A4), 11x17 (11x17), A3 (A3), A5 (A5), B5 (B5 \(JIS\)),... name=PageRegion; default=Letter; options=Letter (US Letter), A4 (A4), ...`

每个选项都以 `name` 标签开头，后跟一个默认值（如果有），然后是选项和描述它们的注释。注释中的符号已转义。

### 选项

`-d debuglevel`

设置调试级别。0 禁用调试消息。

`[ files ]`

用于读取选项的 PPD 文件列表。`-` 导致读取 `STDIN`。

## 退出状态

`foomatic-ppd-options` 成功后以 0 退出，错误时返回非零。错误消息也会打印在标准错误（`STDERR`）上。

## 作者

Patrick Powell `<papowell at astart.com>`

## 缺陷

可能有。但已经过测试。

# FOOMATIC-PPD-TO-XML

## 名称

`foomatic-ppd-to-xml` - 从 PPD 生成 Foomatic 打印机 XML

## 概要

`foomatic-ppd-to-xml [OPTIONS] DRIVER:]PPD*`

`foomatic-ppd-to-xml -h`

## 描述

`foomatic-ppd-to-xml` 的第一形式从 PPD 创建 Foomatic 打印机 XML。

如果指定了 `DRIVER`，则使用该 `PPD`。如果没有提供，则使用第一个驱动。

`foomatic-ppd-to-xml` 的第二形式打印帮助信息。

### 选项

`-d DRIVERS`

驱动程序的逗号分隔列表。

`-r DRIVER`

推荐的驱动。

`-p PDLS`

打印机支持的页面语言（PDLs）逗号分隔列表。

`-l`

为 XML 文件添加链接。

`-b DIRECTORY`

PPD 的基础目录。

`-c COMMENT`

将注释添加到 XML 文件的注释字段。

`-C`

抑制默认注释（纸宽、每分钟页）。

`-f DIRECTORY`

写入 XML 文件的目录。文件名将为带有 `.xml` 扩展名的打印机 ID。

`-n`

不修改现有 XML 文件，仅为没有 XML 文件的打印机创建文件。

`-x`

无论是否存在 XML 文件都创建 XML 文件。如果你有不在 Foomatic 数据库中的打印机的 PPD 文件，这将极大加快进程。

## 退出状态

`foomatic-ppd-to-xml` 成功时返回 0，否则返回 1。

## 缺陷

目前为止没有。

请在以下地址发布 Bug 报告：

`http://lists.freestandards.org/mailman/listinfo/printing-foomatic`

# FOOMATIC-PPDFILE

## 名称

`foomatic-ppdfile` - 为指定的打印机/驱动组合生成 PPD 文件

## 概要

`foomatic-ppdfile [-w] [-d <driver>] -p <printerid>`

`foomatic-ppdfile [-A] [-P pattern]`

`foomatic-ppdfile -h`

## 描述

`foomatic-ppdfile` 的第一形式为 Foomatic 数据库中任何有效的打印机/驱动组合计算独立于打印程序的 Foomatic PPD 文件，用于 `foomatic-rip(1)` 打印以及应用程序/客户端访问打印机选项。PPD 文件返回到标准输出。如果未指定驱动，则使用默认驱动。

`foomatic-ppdfile` 程序的第二形式搜索打印机数据库并返回所有的打印机条目，或名称和/或模型信息匹配正则表达式的条目。

最后一种形式打印帮助信息并退出。

### 选项

`-d drivername`

（可选）要使用的驱动程序名称。如果未提供驱动程序名称，将使用打印机兼容驱动程序列表中的默认或第一个驱动程序。

`-p`

`printer id` 打印机 ID。

`-w`

返回符合 Microsoft Windows 格式限制的 PPD 文件。

`-A`

返回数据库中的所有打印机条目。

`-P pattern`

返回数据库中匹配正则表达式的所有打印机条目。

## 另请

`foomatic-rip(1)`

## 退出状态

`foomatic-ppdfile` 成功时返回 0，否则返回 1。

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 为 foomatic 项目编写，使用了关联二进制文件的输出。

由 Patrick Powell `<papowell at astart.com>` 修改和更新。

## 缺陷

目前暂无。

请在以下地址发布缺陷报告：

`http://lists.freestandards.org/mailman/listinfo/printing-foomatic`

# FOOMATIC-PRINTERMAP-TO-GUTENPRINT-XML

## 名称

`foomatic-printermap-to-gutenprint-xml` - 更新 Gutenprint 驱动 XML 文件

## 摘要

`foomatic-printermap-to-gutenprint-xml`

## 描述

此命令将 Gutenprint 驱动程序的 XML 文件更新为 Gutenprint 源码树中 `foomatic-printermap` 文件的状态。用于更新 OpenPrinting 数据库中 Gutenprint 的驱动 XML 文件。

你极可能不需要此操作。

# FOOMATIC-PRINTJOB

## 名称

`foomatic-printjob` - 以独立于打印队列的方式管理打印作业

## 摘要

`foomatic-printjob [ -s spooler ] [ -P queuename ] [ -o option1=value1 -o option2 ... ] [ -i ] [ file1 file2 ... ]`

`foomatic-printjob -Q [ -s spooler ] [ -P queuename ] [ -i ] [ -a ] [ user1 user2 ... ]`

`foomatic-printjob -R [ -s spooler ] [ -P queuename ] [ -i ] [ - | jobid1 jobid2 ... ]`

`foomatic-printjob -C [ -s spooler ] [ -i ] command [ arguments ]`

`foomatic-printjob -S [ -s spooler ] [ -i ]`

`foomatic-printjob -h [ -s spooler ] [ -P queuename ] [ -i ]`

## 描述

`foomatic-printjob` 提供了一个独立于打印队列的接口，用于创建和管理打印作业以及打印队列。注意第一个参数会改变命令的模式，因为它结合了多个 System V 风格打印命令的功能。

### 选项

`-s spooler`

显式打印队列类型。

`-P queuename`

指定的任何命令都应应用于此队列而非默认队列。

`-o option=value`

将选项设置为值。

`-o option`

设置开关选项。

`-#n`

打印 `n` 份副本。

`file1 file2 ...`

要打印的文件，当未给出文件时，将打印标准输入。

`-Q`

查询队列中的作业。如果指定了用户列表，则只查询这些用户的作业。

`-Q -a`

查询所有队列中的作业。如果指定了用户列表，则只查询这些用户的作业。

`-R [ - | jobid1 jobid2 ... ]`

从队列中删除作业。使用 `-` 将删除所有作业。

`-C command [ arguments ]`

执行用于队列/作业操作的控制命令。命令是 BSD `lpc` 工具的命令。使用控制命令 `help` 获取支持的命令列表。注意：命令的数量随打印队列而异，但在不同打印队列下提供的相同命令功能相同。

`-i`

交互模式：当 `foomatic-printjob` 对某些内容有疑问时会询问你。否则 `foomatic-printjob` 将使用自动检测或报错退出。

`-S`

将选定的打印队列保存为默认。

`-h`

显示此消息，或如果指定了队列，则显示可用选项列表。

## 另请

`foomatic-configure(1)` 以及你的打印队列的文档。

## 作者

Manfred Wassmann `<manolo@NCC-1701.B.Shuttle.de>` 和 Chris Lawrence `<lawrencc@debian.org>` 为 foomatic 项目编写，使用了关联二进制文件的输出。

## 缺陷

此帮助页仍需编辑。

# FOOMATIC-REPLACEOLDINTERIDS

## 名称

`foomatic-replaceoldprinterids` - 替换对旧打印机 ID 的引用

## 摘要

`foomatic-replaceoldprinterids`

## 描述

替换任意文件中旧数字或废弃打印机 ID 的引用。默认情况下，它使用当前 Foomatic 数据库的 `db/oldprinterids` 文件作为翻译表，但你可以使用任意的翻译表。

你极可能不需要此操作。

# FOOMATIC-RIP

## 名称

`foomatic-rip` - 通用打印过滤器/RIP 包装器

## 摘要

### 通用选项

`foomatic-rip [-v] [-q]` 模式特定选项

### 无队列打印过滤器

`foomatic-rip [-P printer | --ppd printerfile] [-J jobtitle] [-o option=value] [...] files]`

### CUPS 过滤器

`foomatic-rip jobid user jobtitle options]`

## 描述

`foomatic-rip` 是一个通用打印过滤器，可以作为 CUPS 过滤器或无队列的直接打印使用。它具有以下功能：

它将标准输入或文件的 PostScript 和 PDF 转换为打印机的原生语言。

翻译通过外部渲染器 `gs(1)` 完成。如果不需要翻译（PostScript 打印机），渲染器变为 `cat(1)`。

打印机功能、如何处理选项以及如何构建渲染器命令行由 PPD 文件描述。PPD 文件通常来自 Foomatic，也可以由 PostScript 制造商提供。`foomatic-rip` 支持 CUPS 和直接打印（无队列），后者通过命令行选项和环境变量选择。

`foomatic-rip` 不仅应用用户通过命令行提供的选项设置，还会搜索整个作业中的嵌入选项设置（仅限 PostScript 作业）。不仅考虑了影响整个作业的设置，还考虑了页头设置，这些设置仅对发现它们的页面有效，因此产生页面特定打印设置的应用程序得到了完全支持。

## 直接、无队列打印

### 选项

`-v`

用于调试的详细模式。警告：将在 `/tmp` 中创建一个包含调试信息的文件。这开启了安全漏洞，在生产环境中不应使用。

`-q`

静静模式 - 最少信息输出。

`-P printer`

`printer` 是用于此作业的配置打印机。

`--ppd printerfile`



处理此作业时应用 PPD 文件 `printerfile`。

`-o option=value`

此作业的选项设置。

`files`

要打印的文件。

如果命令行没有指定至少一个文件，`foomatic-rip` 将从标准输入打印。如果你的打印机 PPD 文件存储在 `/etc/direct/<printer>.ppd` 或 `~/.foomatic/direct/<printer>.ppd`，只需指定 `-P <printer>` 即可使用。

在 PPD 文件中插入：

```
FoomaticRIPPostPipe: "|command"
```

位于 `PPD-Adobe: "4.3"` 之后，其中 `command` 是你希望重定向输出数据的命令。由于 PPD 文件的限制 `command` 中不允许 `<>` 和 `"`，请按以下方式替换：

**字符替换** **`---------------------`**

通过这种方式你可以直接打印到打印机，使用：

```
FoomaticRIPPostPipe: "| cat > /dev/lp0"
```

或

```
FoomaticRIPPostPipe: "| cat > /dev/usb/lp0"
```

用于本地并行或 USB 打印机。为了让普通用户能够以这种方式打印，将他们加入 `lp` 组，并确保相应的打印机设备文件 `/dev/...` 对 `lp` 组是可写的。

对于主机名为 `printer` 且在端口 `9100` 上监听的 TCP/Socket/JetDirect 打印机，你需要以下配置：

```
FoomaticRIPPostPipe: "| /usr/bin/nc -w 1  printer 9100"
```

注意 `nc` 命令命令行中的 `-w 1`，它会让 `nc` 在数据传输到打印机后立即退出。

```
FoomaticRIPPostPipe: "| rlpr -Plp@printserver"
```

将你的作业调度到名为 `printserver` 的机器上的 LPD 打印机队列 `lp` 上。

参阅 [直接打印 direct-doc.html](http://www.openprinting.org/direct-doc.html)

# 使用打印程序打印

参阅 OpenPrinting 网站上的文档：http://www.openprinting.org/

# 配置文件

文件 `/etc/foomatic/filter.conf` 会在每次执行 `foomatic-rip` 时被读取。它允许按照如下方式配置 `foomatic-rip` 的行为（以 `#` 开头的行是注释，会被忽略）：

`debug: 0|1`

开启 (`1`) 或关闭 (`0`) 调试模式。这等于提供 `--debug` 命令行选项。默认设置为 `0`。

`ps_accounting: 0|1`

开启 (`1`) 或关闭 (`0`) 在 PostScript 作业中插入用于页面计数的代码。插入的 PostScript 代码会让 Ghostscript 在 stderr 上生成计数输出，CUPS 借此可以记录打印的每一页。只有当 CUPS 是打印程序时，才会插入该代码。默认设置为 `1`。

`echo: [<path>/]<executable>*`

设置支持 `-n` 的 `echo(1)` 可执行文件的路径。

`gspath: [<path>/]<executable>*`

设置 Ghostscript `gs(1)` 可执行文件的路径。当 Ghostscript 位于非标准位置或应使用备用 Ghostscript 使用。

`execpath: <path>[:<path>]...`

设置 `foomatic-rip` 使用的 `$PATH` 变量。

`cupsfilterpath: <path>[:<path>]...`

设置 `foomatic-rip` 搜索 CUPS 滤波器的目录（用冒号分隔）。

`preferred_shell: [<path>/]<executable>*`

设置执行 `FoomaticRIPCommandLine` 及其相关命令时使用的首选 shell。某些 PPD 文件使用了需要现代 shell（如 `bash`、`zsh` 或 `ksh`）的 shell 构造。

# 文件

`/etc/cups/ppd/<printer>.ppd`

`/etc/direct/<printer>.ppd`

当前定义打印机的 PPD 文件

`/etc/foomatic/filter.conf`

`foomatic-rip` 的配置文件

## 退出状态

除非发生意外，否则 `foomatic-rip` 返回 0。

## 作者

Till Kamppeter `<till.kamppeter@gmail.com>`，参考了 Manfred Wassmanns `<manolo@NCC-1701.B.Shuttle.de>` 关于 Foomatic 2.0.x 过滤器的 man 页面。

## 缺陷

目前暂无。

请向 OpenPrinting 缺陷跟踪器发送缺陷报告：

http://bugs.linuxfoundation.org/

使用 "OpenPrinting" 作为产品，使用 "cups-filters" 作为组件。

# FOOMATIC-SEARCHPRINTER

## 名称

`foomatic-searchprinter` - 搜索 Foomatic 数据库

## 摘要

```
foomatic-searchprinter [-mM] [-dFID] SEARCHTERM
```

```
foomatic-searchprinter -h
```

## 描述

此命令显示匹配 `SEARCHTERM` 的 Foomatic 数据库项。

### 选项

`-mM`

搜索模式：

`M = 0`

匹配所有（默认值）

`M = 1`

仅对制造商不匹配

`M = 2`

仅对制造商或仅对型号不匹配

`M = 3`

设备 ID、品牌/型号或 Foomatic ID 的精确匹配，并将设备 ID 中的页面描述语言匹配到相应的"通用(Generic)"打印机

`M = 4`

仅精确匹配设备 ID、品牌/型号或 Foomatic ID

`-dD`

显示结果：

`D = 0`

所有内容

`D = 1`

仅显示最佳匹配类（默认值）

`D = 2`

仅显示最佳匹配

`-h`

显示帮助信息并退出。

## 缺陷

目前暂无。

请在下方发布缺陷报告：

http://lists.freestandards.org/mailman/listinfo/printing-foomatic

# fpaste

## 名称

`fpaste` - fpaste.org 剪贴板的命令行界面

## 摘要

```
fpaste [OPTION]... [FILE]...
```

## 描述

能够方便地将文本粘贴到 http://fpaste.org 的 Fedora Pastebin 通常很有用，这个简单的实用程序就可以此操作并返回生成的 URL，以便人们可以检查输出。这希望能够帮助那些由于某些原因没有 X 环境、远程工作或任何其他无法通过网络浏览器将内容粘贴到剪贴板的人。

### 选项

`--version`

显示程序版本号并退出

`-h, --help`

显示帮助信息并退出

`-n "NICKNAME"`

你的昵称；默认值

`-d "PASSWORD"`

`password="PASSWORD"`

密码；默认值为 "password"

`-l "LANGUAGE"`

内容的语言；默认值为 "language"

`-x "EXPIRES"`

过期前时间；默认值为 "expires"

`-U "URL"`

URL；默认值为 "url"

`-P "PRIVATE"`

私有；默认值为 "private"

`-i "IN"`

从输入读取；默认值为 "input"

`-o "OUT"`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

### 选项

`fpaste -n NICKNAME`

你的昵称；默认值

`fpaste -d PASSWORD`

`password="PASSWORD"`

密码；默认值为 "password"

`fpaste -l LANGUAGE`

内容的语言；默认值为 "language"

`fpaste -x EXPIRES`

过期前时间；默认值为 "expires"

`fpaste -U URL`

URL；默认值为 "url"

`fpaste -P PRIVATE`

私有；默认值为 "private"

`fpaste -i IN`

从输入读取；默认值为 "input"

`fpaste -o OUT`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

## 示例

`fpaste -n NICKNAME`

你的昵称；默认值

`fpaste -n "NICKNAME"`

你的昵称；默认值

`fpaste -d PASSWORD`

`password="PASSWORD"`

密码；默认值为 "password"

`fpaste -l LANGUAGE`

内容的语言；默认值为 "language"

`fpaste -x EXPIRES`

过期前时间；默认值为 "expires"

`fpaste -U URL`

URL；默认值为 "url"

`fpaste -P PRIVATE`

私有；默认值为 "private"

`fpaste -i IN`

从输入读取；默认值为 "input"

`fpaste -o OUT`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

## 示例

`fpaste -n NICKNAME`

你的昵称；默认值

`fpaste -n "NICKNAME"`

你的昵称；默认值

`fpaste -d PASSWORD`

`password="PASSWORD"`

密码；默认值为 "password"

`fpaste -l LANGUAGE`

内容的语言；默认值为 "language"

`fpaste -x EXPIRES`

过期前时间；默认值为 "expires"

`fpaste -U URL`

URL；默认值为 "url"

`fpaste -P PRIVATE`

私有；默认值为 "private"

`fpaste -i IN`

从输入读取；默认值为 "input"

`fpaste -o OUT`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

## 示例

`fpaste -n NICKNAME`

你的昵称；默认值

`fpaste -n "NICKNAME"`

你的昵称；默认值

`fpaste -d PASSWORD`

`password="PASSWORD"`

密码；默认值为 "password"

`fpaste -l LANGUAGE`

内容的语言；默认值为 "language"

`fpaste -x EXPIRES`

过期前时间；默认值为 "expires"

`fpaste -U URL`

URL；默认值为 "url"

`fpaste -P PRIVATE`

私有；默认值为 "private"

`fpaste -i IN`

从输入读取；默认值为 "input"

`fpaste -o OUT`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

## 示例

`fpaste -n NICKNAME`

你的昵称；默认值

`fpaste -n "NICKNAME"`

你的昵称；默认值

`fpaste -d PASSWORD`

`password="PASSWORD"`

密码；默认值为 "password"

`fpaste -l LANGUAGE`

内容的语言；默认值为 "language"

`fpaste -x EXPIRES`

过期前时间；默认值为 "expires"

`fpaste -U URL`

URL；默认值为 "url"

`fpaste -P PRIVATE`

私有；默认值为 "private"

`fpaste -i IN`

从输入读取；默认值为 "input"

`fpaste -o OUT`

保存到输出；默认值为 "out"

`--CLIPBOARD`

剪贴板选择；默认值为 "clipboard"

`--FULLPATH`

全路径；默认值为 "fullpath"

`--ITSELF`

其本身；默认值为 "itself"

`--SYSINFO`

系统信息；默认值为 "sysinfo"

`--PRINTONLY`

仅打印；默认值为 "printonly"

`--CONFIRM`

确认；默认值为 "confirm"

`left-thumb`, `left-index-finger`, `left-middle-finger`, `left-ring-finger`, `left-little-finger`, `right-thumb`, `right-index-finger`, `right-middle-finger`, `right-ring-finger`, `right-little-finger`。

默认为自动，对于滑动设备选择第一个可用手指，对于压力设备则选择所有录入的手指。

## 测试应用程序

### fprintd-enroll

将用户的右手食指录入数据库。

### fprintd-list

列出用户已录入的指纹。

### fprintd-verify

将用户的右手食指录入数据库。

### fprintd-enroll

将用户的右手食指录入数据库。

## 属性

`fprintd` 由 Bastien Nocera 和 Daniel Drake 编写。

## 目录

默认情况下，`fprintd` 将指纹存储在 `/var/lib/fprint/`。

## 参见

`dbus-daemon`, `gnome-about-me`

---

# FREE

## 名称

`free` - 显示系统中空闲和已使用的内存量

## 语法

```
free [-options]
```

## 描述

`free` 显示系统中空闲和已使用的物理及交换内存总量，以及内核使用的缓冲区（buffers）和缓存（caches）。这些信息通过解析 `/proc/meminfo` 获取。显示的列如下：

**total**

已安装的内存总量（`/proc/meminfo` 中的 `MemTotal` 和 `SwapTotal`）

**used**

已使用的内存（计算方式为 `total` - `free` - `buffers` - `cache`）

**free**

未使用的内存（`/proc/meminfo` 中的 `MemFree` 和 `SwapFree`）

**shared**

（主要）由 `tmpfs` 使用的内存（`/proc/meminfo` 中的 `Shmem`，内核 2.6.32 及以上版本可用，不可用时显示为零）

**buffers**

内核缓冲区使用的内存（`/proc/meminfo` 中的 `Buffers`）

**cache**

页缓存（page cache）和插槽缓存（slabs）使用的内存（`/proc/meminfo` 中的 `Cached` 和 `Slab`）

**buff/cache**

`buffers` 和 `cache` 的总和

**available**



估计启动新应用程序时在无需交换的情况下可用内存量。与`cache`或`free`字段的数据不同，此字段考虑了页缓存，并且考虑到并非所有可回收的内存slabs会因为项目正在使用而无法回收（`/proc/meminfo`中的`MemAvailable`，内核3.14及以上版本可用，2.6.27+版本进行模拟，否则等同于`free`）

### 选项

`-b`, `--bytes`

以字节（bytes）显示内存量。

`-k`, `--kilo`

以千字节（kilobytes）显示内存量。这是默认值。

`-m`, `--mega`

以兆字节（megabytes）显示内存量。

`-g`, `--giga`

以吉字节（gigabytes）显示内存量。

`--tera`

以字节显示内存量。

所有输出字段自动缩放至最短的三位单位，并显示输出单位。使用以下单位：

`B = bytes K = kilos M = megas G = gigas T = teras`

如果单位缺失，且你有拍字节级的RAM或交换内存，数字将以TB计算，且列可能与表头不对齐。

`-w`, `--wide`

切换到宽模式。宽模式产生的行长度超过80个字符。在此模式下，`buffers`和`cache`在两个独立的列报告。

`-c`, `--count` *count*

显示结果*count*次。需要`-s`选项。

`-l`, `--lohi`

显示详细的低、高内存统计信息。

`-s`, `--seconds` *seconds*

每隔*seconds*连续显示结果。你可以为*delay*指定任何浮点数，使用`usleep(3)`用于微秒级延迟时间。

`--si`

使用1000的幂而非1024。

`-t`, `--total`

显示显示列总计的行。

`--help`

打印帮助信息。

`-V`, `--version`

显示版本信息。

# 文件

`/proc/meminfo`

内存信息

## 参见

`ps`(1), `slabtop`(1), `top`(1), `vmstat`(8)。

## 作者

由Brian Edmonds编写。

## 报告Bug

请将错误报告发送至

* *

# fros

## 名称

`fros` - 通用屏幕共享前端，支持多种后端的插件化

## 语法

`fros [-h] [--v] [--is-available]`

## 描述

`fros`通用屏幕共享前端，支持多种后端的插件化。目标是为尽可能多的屏幕共享后端提供统一访问，同时保持相同的用户界面，以便使用户在不同桌面和屏幕共享程序之间的体验是无缝的。

### 选项

`-h`, `--help`

显示帮助信息并退出

`-v`, `--verbose`

使输出更详细/话多

`--is-available`

检查当前环境是否支持屏幕共享（0:可用，1: 不可用）

## 属性

Jiri Moskovc <jmoskovc at redhat dot com>

## 参见

`mydesktop`(1)

* *

# FUNZIP

## 名称

`funzip` - 从ZIP存档中提取的过滤器

## 语法

`funzip [-password] [input.gz]`

## 参数

`[-password]`

如果ZIP存档加密，所需的密码。参见描述。

`[input.gz]`

可选输入文件。参见描述。

## 描述

`funzip`不带文件参数作为过滤器；即它假设ZIP存档（或`gzip`(1)文件）被管道到stdin，并将第一个成员提取到stdout。当stdin来自终端时，*funzip*假设这不是一个二进制数据流。如果存在文件参数，*funzip*从指定的文件读取。

加密文件的密码可以在命令行指定。注意这在许多系统上存在安全风险；当前运行的进程可以通过`ps`(1)查看。

## 示例

使用*funzip*提取test.zip的第一个成员并管道到`more`(1)：

```
funzip test.zip | more
```

使用*funzip*测试test.zip的第一个成员（任何错误将报告到标准错误）：

```
funzip test.zip > /dev/null
```

使用*zip*和*funzip*代替*compress*(1)和*zcat*(1)（或*gzip*(1L)和*gzcat*(1L)）进行磁带备份：

```
tar cf - . | zip -7 | dd of=/dev/nrst0 obs=8k dd if=/dev/nrst0 ibs=8k | funzip | tar xf -
```

（例如，nrst0是SCSI磁带驱动器）。

BUG

当管道一个加密文件并允许*funzip*提示密码时，终端有时会被重置为无显示模式。这显然由于两个程序之间的竞态条件引起的；*funzip*在*more*读取状态之前更改了终端模式，然后*more*将恢复到该模式。要恢复，对同一文件运行*funzip*但重定向到/dev/null而不是管道到more；在再次提示密码后，*funzip*将正确重置终端。

目前无法从ZIP存档中提取第一个以外的任何成员。这在ZIP存档包含在另一个存档的情况下有用。如果第一个成员是目录，*funzip*只创建该目录并退出。

*funzip*的功能应整合到*unzip*get中（未来版本）。

## 参见

`gzip`(1L), `unzip`(1L), `unzipsfx`(1L), `zip`(1L), `zipcloak`(1L), `zipinfo`(1L), `zipnote`(1L), `zipsplit`(1L)

Info-ZIP的主页目前位于`http://www.info-zip.org/pub/infozip/`或`ftp://ftp.info-zip.org/pub/infozip/`。

## 作者

Mark Adler (Info-ZIP)

***

# FUSER

## 名称

`fuser` - 识别使用文件或套接字的进程

## 语法

`fuser` [`-fuv`] [`-a`|`-s`] [`-4`|`-6`] [`-c`|`-m`|`-n` *space*] [` -k` [`-i`] [`-M`] [`-w`] [`-*SIGNAL*] ] *name* ...

`fuser` -l

`fuser` -V 

## 描述

`fuser`显示使用指定文件或文件系统的PID。在默认显示模式下，每个文件名后面都会跟着一个表示访问类型的字母：

`c`

当前目录。

`e`

正在运行的可执行文件。

`f`

打开的文件。在默认显示模式下省略`f`。

`F`

用于写入的打开文件。在默认显示模式下省略`F`。

`r`

根目录。

`m`

mmap映射的文件或共享库。

如果没有访问任何指定的文件，或者发生致命错误，`fuser`将返回非零状态码。如果发现至少一次访问，`fuser`返回零。

为了查找使用TCP和UDP套接字的进程，必须使用`-n`选项选择相应的命名空间。默认情况下，`fuser`会同时查找IPv6和IPv4套接字。如需更改默认行为，请使用`-4`和`-6`选项。可以通过本地和远程端口以及远程地址来指定套接字。所有字段均为可选，但缺失字段前的逗号必须存在：

`[`lcl_port`][,`[`rmt_host`][,`[`rmt_port`]]]`

**用作IP地址和端口号可以使用符号值或数值值。**

`fuser`仅将PID输出到stdout，其他所有内容发送到stderr。

### 选项

`-a`, `--all`

显示命令行上指定的所有文件。默认情况下，只显示至少一个进程访问的文件。

`-c`

与`-m`选项相同，用于POSIX兼容性。

`-f`

静默忽略，用于POSIX兼容性。

`-k`, `--kill`

杀死访问文件的进程。除非通过`-SIGNAL*`更改，否则发送SIGKILL。`fuser`进程永远不会杀死自己，但可能会杀死其他`fuser`进程。在尝试杀死之前，执行`fuser`的进程的有效用户ID设置为真实用户ID。

`-i`, `--interactive`

在杀死进程之前询问用户确认。如果没有`-k`，此选项将被静默忽略。

`-l`, `--list-signals`

列出所有已知信号名称。

`-m` *NAME*, `--mount` *NAME*

*NAME*指定挂载文件系统上的文件或挂载的块设备。列出访问该文件系统文件的所有进程。如果指定了目录文件，它会自动变为*NAME*/，以便使用可能挂载在该目录上的任何文件系统。

`-M`, `--ismountpoint`

仅当*NAME*指定挂载点时，请求才会执行。这是一个无价的安全带，可以防止在*NAME*恰好不是文件系统时杀掉机器。

`-w`

只杀死具有写权限的进程。如果没有`-k`，此选项将被静默忽略。

`-n` *SPACE*, `--namespace` *SPACE*

选择不同的命名空间。支持`file`（文件名，默认）、`udp`（本地UDP端口）和`tcp`（本地TCP端口）命名空间。对于端口，可以使用端口号或符号名称。如果没有歧义，可以使用快捷记法*name*/***space*（例如*80*/***tcp*）。

`-s`, `--silent`

静默操作。在此模式下将忽略`-u`和`-v`。`-a`不能与`-s`一起使用。

`-SIGNAL*`

在杀死进程时使用指定的信号代替SIGKILL。可以通过名称（例如`-HUP`）或数字（例如`-1`）指定信号。如果没有使用`-k`选项，此选项将被静默忽略。

`-u`, `--user`

在每个PID后附加进程所有者的用户名。

`-v`, `--verbose`

详细模式。以类似`ps`的样式显示进程。PID、USER和COMMAND字段与`ps`类似。ACCESS显示进程如何访问文件。详细模式还会显示特定文件何时作为挂载点、nfs导出或交换文件被访问。在这种情况下，显示`kernel`而不是PID。

`-V`, `--version`

显示版本信息。

`-4`, `--ipv4`

仅搜索IPv4套接字。此选项不能与`-6`选项一起使用，且仅对tcp和udp命名空间有效。

`-6`, `--ipv6`

仅搜索IPv6套接字。此选项不能与`-4`选项一起使用，且仅对tcp和udp命名空间有效。

`-`

重置所有选项并将信号恢复SIGKILL。

# 文件

`/proc`

proc文件系统的位置

## 示例

`fuser -km /home`

杀死所有访问`/home`文件系统的进程。

`if fuser -s /dev/tty1; then something; else fi`

如果没有使用`/dev/tty1`的进程，调用`something`。

`fuser telnet/tcp`

显示所有使用TELNET端口的进程。

## 限制

访问相同文件或文件系统的进程只会显示一次。如果在命令行上指定了多个相同的文件，其中某些可能会被忽略。`fuser`可能只能在具有权限的情况下获取部分信息。结果是，其他用户打开的文件可能不会列出，可执行文件可能会被归类为此。（注：由于原文中存在大量重复的段落，此处已根据“不要重复输出原文”原则进行了处理）。

此程序遵循标准的GNU命令行语法，长选项以两个横杠（`-`）开头。以下包含了选项摘要。

`--help`

显示选项摘要。

`--verbose`

显示额外的调试信息。

`--allow-reinstall`

允许重新安装现有的固件版本。

`--allow-older`

允许将固件版本降级。

`--offline`

在可能的情况下离线执行。

## Commands

此程序接受带有可变参数的命令。

**get-details**

获取固件文件的详细信息。

**get-devices**

获取支持固件更新的硬件列表。

**get-updates**

获取连接硬件的更新列表。

**update**

将所有固件更新到最新的可用版本。

**install**

在此硬件上安装固件文件。

**install-prepared**

现在安装已准备就的更新。

**clear-results**

清除上一次更新的结果。

**refresh**

从远程服务器刷新元数据。

**get-results**

获取上一次更新的结果。

## Author

本手册页由Richard Hughes `<richard@hughsie.com>`编写。

***

# GAWK

## Name

`gawk` - 模式扫描和处理语言

## Synopsis

`gawk` [ POSIX或GNU风格选项 ] `-f` *program-file* [ `--` ] file ...

`gawk` [ POSIX或GNU风格选项 ] [ `--` ] *program-text* file ...

## Description

`gawk`是GNU项目对AWK语言的实现。它符合POSIX 1003.1标准中对语言的定义。此版本基于Aho、Kernighan和Weinberger所著*The AWK Programming Language*中的描述。`gawk`提供了Brian Kernighan的`awk`当前版本中的额外功能以及许多GNU特有的扩展。

命令行由`gawk`自身的选项、AWK程序文本（如果未通过`-f`或`--file`选项提供）以及要在预定义AWK变量`ARGC`和`ARGV`中使用的值组成。

使用`--profile`选项调用`gawk`时，它开始从程序执行中收集分析统计数据。`gawk`在此模式下运行较慢，并在完成后自动在`awkprof.out`文件中生成执行分析报告。参见下文的`--profile`选项。

`gawk`还拥有一个集成调试器。通过向命令行提供`--debug`选项可以启动交互式调试会。在此执行模式下，`gawk`加载AWK源代码并提示调试命令。`gawk`只能对通过`-f`选项提供的AWK程序源码进行调试。调试器在*GAWK: Effective AWK Programming*中有介绍。

## Option Format

`gawk`选项可以是传统的POSIX风格单字母选项，也可以GNU风格的长选项。POSIX选项以单个`-`开头，而长选项以`--`开头。长选项既用于GNU特有的功能，也用于POSIX强制的功能。

`gawk`特有的选项通常以长选项的形式使用。长选项的参数可以通过`=`号与选项连接（中间没有空格），或者也可以作为下一个命令行参数提供。长选项可以缩写，只要该缩写保持唯一性。

此外，每个长选项都有一个对应的短选项，因此可以在`#!`可执行脚本内部使用该选项的功能。

## Options

`gawk`接受以下选项。标准选项列在前面，随后是`gawk`扩展选项，按短选项的字母顺序排序。

`-f *program-file*

`--file *program-file*` 从文件*program-file*读取AWK程序源码，而不是从第一个命令行参数。可以使用多个`-f`（或`--file`）选项。

`-F *fs*

`--field-separator *fs*` 使用`fs`作为输入字段分隔符（预定义变量`FS`的值）。

`-v *var*=*val*

`--assign *var*=*val*` 在程序开始执行前将值`val`赋值给变量`var`。此类变量对于AWK程序的`BEGIN`规则可用。

`-b

`--characters-as-bytes` 将所有输入数据视为单字节字符。换句话说，在尝试将字符串处理多字节字符时，不要关注任何本地化信息。`--posix`选项会覆盖此选项。

`-c

`--traditional` 在兼容模式下运行。在兼容模式下，`gawk`的行为与Brian Kernighan的`awk`完全相同；不会识别GNU特有的扩展。更多信息请参见下文的**GNU EXTENSIONS**。

`-C

`--copyright` 在标准输出上打印简短版本的GNU版权信息并成功退出。

`-d[*file*]

`--dump-variables[=*file*]` 将全局变量列表、其类型和最终值打印到*file*。如果没有提供`file`，`gawk`将使用当前目录下的`awkvars.out`文件。

列出所有全局变量是查找程序中拼写错误的好方法。

`-D[*file*]

`--debug[=*file*]` 启用AWK程序的调试。默认情况下，调试器从键盘（标准输入）交互式读取命令。可选的`file`参数指定了一个包含命令列表的文件供调试器非交互式执行。

`-e *program-text*

`--source *program-text*` 使用*program-text*作为AWK程序代码。此选项允许将库函数（通过`-f`和`--file`选项使用）与命令行输入的源码轻松混合。

`-E *file*

`--exec *file*` 与`-f`类似，但此选项是最后一个处理的。这应该用于`#!`脚本，特别是CGI，以避免从URL在命令行传递选项或源码。此选项禁用命令行赋值。

`-g

`--gen-pot` 扫描并解析AWK程序，并在标准输出上生成一个`.pot`（便对象模板）格式文件，包含程序中所有可本地化的字符串。程序本身不执行。有关`.pot`文件的更多信息请参见GNU *gettext*分发。

`-h



`--help` 在标准输出上打印可用选项的相对摘要。（根据 *GNU Coding Standards*，这些选项会导致立即成功退出。）

`-i include-file`

`--include include-file` 加载 AWK 源码库。使用环境变量 `AWKPATH` 搜索库。如果初始搜索失败，在添加 `.awk` 后缀后将再次尝试。文件将被加载一次（即消除重复），且代码不构成主程序源码。

`-l lib`

`--load lib` 加载共享库 `lib`。使用环境变量 `AWKLIBPATH` 搜索库。如果初始搜索失败，在添加平台默认共享库后缀后将再次尝试。预计初始化例程为 `dl_load()`。

`-L [value]`

- `--lint[=value]` 对可疑或无法移植到其他 AWK 实现的结构提供警告。带有可选参数 `fatal` 时，lint 警告将变为致命错误。这可能非常剧烈，但它的使用无疑会鼓励编写更整洁的 AWK 程序。带有可选参数 `invalid` 时，仅对实际上无效的内容发出警告。（目前尚未完全实现。）
- `-M`
- `--bignum` 强制对数字使用任意精度算术。如果 `gawk` 编译时没有使用 GNU MPFR 和 MP 库，则此选项无效。
- `-n`
- `--non-decimal-data` 识别输入数据中的八进制和十六进制值。*谨慎使用此选项！*
- `-N`
- `--use-lc-numeric` 强制 `gawk` 在解析输入数据时使用本地化（locale）小数点字符。虽然 POSIX 标准要求这种行为，且 `gawk` 在启用 `--posix` 时会这样做，但默认行为是遵循传统习惯使用句号作为小数点，即使在这些区域中句号并不是小数点字符。

  此选项覆盖了默认行为，但没有像 `--posix` 选项那样完全严苛严格。
- `-o[file]`
- `--pretty-print[=file]` 将程序的格式化版本输出到 `file`。如果没有提供 `file`，`gawk` 将使用当前目录下名为 `awkprof.out` 的文件。
- `-O`
- `--optimize` 针对程序的内部表示启用优化。目前，这包括简单的常量折叠和递归函数的尾调用消除。`gawk` 维护者希望随着时间的推移添加额外的优化。
- `-p[prof-file]`
- `--profile[=prof-file]` 启动分析会话，并将分析数据发送到 `prof-file`。默认值为 `awkprof.out`。配置文件在左侧边缘包含程序中每个语句的执行次数，以及每个用户定义函数的调用次数。
- `-P`
- `--posix` 开启*兼容*模式，并带有以下额外限制：

  - 不识别 `\x` 转义序列。
  - 当 `FS` 设置为单个空格时，只有空格和制表符作为字段分隔符，换行符不是。
  - 不能在 `?` 和 `:` 之后延续行。
  - 不识别关键字 `function` 的别名 `func`。
  - 运算符 `~` 和 `~=` 不能代替 `^` 和 `^=`。

- `-r --re-interval` 在正则表达式匹配中使用*区间表达式*（参见下下文的**正则表达式**）。区间表达式在传统的 AWK 语言中并不可用。POSIX 标准增加了它们，以使 `awk` 和 `egrep` 彼此保持一致。它们默认启用，但此选项仍保留以供配合 `--traditional` 使用。
- `-S --sandbox` 在沙箱模式下运行 `gawk`，禁用 `system()` 函数、通过 `getline` 进行输入重定向、通过 `print` 和 `printf` 进行输出重定向以及加载动态扩展。命令执行（通过管道）也被禁用。这有效地阻止了脚本访问本地资源（命令行中指定的文件除外）。
- `-t --lint-old` 对无法移植到原始版本 UNIX *awk* 版本的结构提供警告。
- `-V --version` 在标准输出上打印此特定 `gawk` 的版本信息。这主要用于判断你系统上的当前 `gawk` 版本是否与自由软件基金分发的版本保持同步。在报告 bug 时也很有用。（根据 *GNU 编码规范*，这些选项会导致程序立即成功退出。）
- `--` 标记选项的结束。这允许后续参数以 `-` 开头，包括 AWK 程序本身的参数。这与大多数其他 POSIX 程序所使用的参数解析约定保持一致。

在兼容模式下，任何其他选项都会被标记为无效，但在其他情况下会被忽略。在正常操作下，只要提供了程序文本，未知选项将传递给 AWK 程序的 `ARGV` 数组进行处理。这对于通过 `#!` 可执行文件解释器机制运行 AWK 程序特别有用。

对于 POSIX 兼容性，可以使用 `-W` 选项，后跟一个长选项的名称。

## AWK 程序执行

一个 AWK 程序由一系列模式-动作语句和可选的函数定义组成。

```awk
@include "filename*"
@load "filename*" pattern { action statements }
function name(parameter list) { statements }
```

`gawk` 首先从 `program-file(s)`、`--source` 参数或命令行上的第一个非选项参数读取程序源码（如果指定）。`-f` 和 `--source` 选项可以在命令行上多次使用。`gawk` 读取程序文本，就像所有的 `program-file` 和命令行源文本已经连接在一起一样。这对于构建 AWK 函数库非常有用，而无需在每个使用它们的新 AWK 程序中包含它们。它还提供了将库函数与命令行程序混合的能力。

此外，以 `@include` 开头的行可以将其他源文件包含到程序中，使库的使用更加简单。这等同于使用 `-i` 选项。

以 `@load` 开头的行可以将共享库加载到程序中。这等同于使用 `-l` 选项。

环境变量 `AWKPATH` 指定了查找使用 `-f` 和 `-i` 选项命名的源文件时使用的搜索路径。如果该变量不存在，默认路径为 `.:/usr/local/share/awk`。（实际路径取决于 `gawk` 的构建和安装。）如果给 `-f` 的文件名包含 `/` 字符，则不进行路径搜索。

环境变量 `AWKLIBPATH` 指定了查找使用 `-l` 选项命名的源文件时使用的搜索路径。如果该变量不存在，默认路径为 `/usr/local/lib/gawk`。（实际路径取决于 `gawk` 的构建和安装。）

*Gawk* 执行 AWK 程序的顺序如下：

1. 首先通过 `-v` 选项执行变量赋值。
2. 接下来，`gawk` 将程序编译为内部形式。
3. 然后，`gawk` 执行 `BEGIN` 规则（如果有），然后读取 `ARGV` 数组中的每个文件（直到 `ARGC`）。如果命令行没有命名文件，`gawk` 读取标准输入。

如果命令行上的文件名形式为 `var=val`，则被视为变量赋值。变量 `var` 将被赋值 `val`。（这发生在任何 `BEGIN` 规则运行之后。）命令行变量赋值对于动态分配 AWK 用于控制输入如何分解字段和记录的变量非常有用。对于需要对单个数据文件进行多次处理时控制状态也有用。

如果 `ARGV` 中特定元素的值为空 `()`，`gawk` 将跳过它。

对于每个输入文件，如果存在 `BEGINFILE` 规则，`gawk` 在处理文件内容之前执行相关代码。同样，`gawk` 在处理文件后执行与 `ENDFILE` 关联的代码。

对于输入中的每个记录，`gawk` 测试其是否匹配 AWK 程序中的任何*模式*。对于记录匹配的每个模式，`gawk` 执行相应的动作。模式按照它们在程序中的顺序进行测试。

最后，在所有输入耗尽后，`gawk` 执行 `END` 规则（如果有）。

根据 POSIX 标准，`awk` 命令行中指定的文件必须是文本文件。如果不是，其行为是“未定义”的。大多数 `awk` 版本会将命令行上的目录视为致命错误。

从 `gawk` 4.0 版本开始，命令行上的目录会产生警告，但在其他情况下会被跳过。如果给出 `--posix` 或 `--traditional` 选项，则 `gawk` 将恢复将命令行上的目录视为致命错误。

## 变量、记录与字段

AWK 变量是动态的；它们在第一次使用时产生。它们的值可以是浮点数、字符串或两者兼有，取决于如何使用它们。AWK 仅支持一维数组；多维数组可以通过模拟。`gawk` 提供了真正的数组数组；参见下文的**数组**。在程序运行时，会设置几个预定义变量；这些变量将在需要时进行描述并在下方进行总结。

### 记录

通常情况下，记录由换行符分隔。你可以通过为内置变量 `RS` 赋值来控制记录的分隔符。如果 `RS` 是任何单个字符，则用该字符分隔记录。否则，`RS` 是一个正则表达式。输入中匹配此正则表达式的文本将分隔记录。然而，在兼容模式下，仅使用其字符串值的第一个字符来分隔记录。如果将 `RS` 设置为空字符串，则通过空行分隔记录。当 `RS` 设置为空字符串时，换行符始终作为字段分隔符，无论 `FS` 的值是什么（无论如此）。

### 字段

在读取每个输入记录时，`gawk` 使用 `FS` 变量的值作为字段分隔符将记录拆分为*字段*。如果 `FS` 是单个字符，则由该字符分隔字段。如果 `FS` 为空字符串，则每个单独字符都成为一个单独字段。否则，期望 `FS` 为完整的正则表达式。在 `FS` 为单个空格的特殊情况下，字段由连续的空格和/或制表符和/或换行符分隔。（但请参见下方的**POSIX 兼容性**章节。）

**注意**：`IGNORECASE` 的值（见下文）也会影响 `FS` 为正则表达式时字段的划分方式，以及 `RS` 为正则表达式时记录的分隔方式。

如果 `FIELDWIDTHS` 变量设置为由空格分隔的数字列表，则每个字段预计具有固定宽度，`gawk` 使用指定的宽度拆分记录。此时忽略 `FS` 的值。为 `FS` 或 `FPAT` 赋新值将覆盖对 `FIELDWIDTHS` 的使用。

同样，如果 `FPAT` 变量设置为代表正则表达式的字符串，则每个字段由匹配该正则表达式的文本组成。在这种情况下，正则表达式描述的是字段本身，而不是分隔字段的文本。为 `FS` 或 `FIELDWIDTHS` 赋新值将覆盖对 `FPAT` 的使用。

输入记录中的每个字段可以通过其位置引用：`$1`、`$2` 等。`$0` 是整个记录。字段不需要通过常量引用：

```awk
n = 5
print $n
```

打印输入记录中的第五个字段。

变量 `NF` 被设置为输入记录中的字段总数。

对不存在的字段进行引用（即 `$NF` 之后的字段）会产生空字符串。然而，给不存在的字段赋值（例如 `$(NF+2) = 5`）会增加 `NF` 的值，创建任何中间的字段并以空字符串作为其值，并导致 `$0` 的值被重新计算，字段通过 `OFS` 的值进行分隔。对负编号字段引用会导致致命错误。递减 `NF` 会导致新值之后的字段值丢失，并重新计算 `$0` 的值，字段通过 `OFS` 的值进行分隔。

给现有的字段赋值会在引用 `$0` 时重新构建整个记录。同样，给 `$0` 赋值会导致记录重新拆分，从而为字段创建新值。

### 内置变量

`gawk` 的内置变量有：

#### `ARGC`

命令行参数的数目（不包括传递给 `gawk` 的选项或程序源码）。

#### `ARGIND`

当前处理的文件在 `ARGV` 中的索引。

#### `ARGV`

命令行参数数组。该数组从 0 到 `ARGC - 1` 索引。动态更改 `ARGV` 的内容可以控制用于数据的文件。

#### `BINMODE`

在非 POSIX 系统上，指定所有文件 I/O 使用“二进制”模式。数值值 1、2 或 3 分别指定输入文件、输出文件或所有文件使用二进制 I/O。字符串值 `r` 或 `w` 分别指定输入文件或输出文件使用二进制 I/O。字符串值 `rw` 或 `wr` 指定所有文件使用二进制 I/O。任何其他字符串值被视为 `rw`，但会生成警告消息。

#### `CONVFMT`

数字的转换格式，默认为 `%.6g`。

#### `ENVIRON`

包含当前环境值的数组。该数组由环境变量索引，每个元素是该变量的值。

#### `ERRNO`

如果在执行重定向、读取 `getline` 或执行 `close()` 期间发生系统错误，则 `ERRNO` 将包含描述该错误的字符串。

#### `FIELDWIDTHS`

一个由空格分隔的宽度列表。设置后，`gawk` 使用固定宽度拆分输入，而不是使用 `FS` 的值作为字段分隔符。见**字段**章节。

#### `FILENAME`

当前输入文件的文件名。如果在命令行上没有指定文件，`FILENAME` 在 **BEGIN** 规则内是未定义的（除非由 `getline` 设置）。

#### `FNR`

当前输入文件中的输入记录号。

#### `FPAT`

描述记录字段内容的正则表达式。设置后，`gawk` 将输入拆分为字段，其中字段匹配正则表达式，而不是使用 `FS` 的值作为字段分隔符。见**字段**章节。

#### `FS`

输入字段分隔符，默认为空格。见**字段**章节。

#### `FUNCTAB`

一个数组，其索引和对应的值是程序中所有自定义或扩展函数的名称。**注意**：你不能对 `FUNCTAB` 数组使用 `delete` 语句。

#### `IGNORECASE`

控制所有正则表达式和字符串操作的大小写敏感性。如果 `IGNORECASE` 非零，规则中的字符串比较和模式匹配、使用 `FS` 和 `FPAT` 的字段划分、使用 `RS` 的记录分隔、使用 `~` 和 `!~` 的正则表达式匹配，以及内置函数 `gensub()`、`gsub()`、`index()`、`match()`、`patsplit()`、`split()` 和 `sub()` 在执行正则表达式操作时忽略大小写。

**注意**：数组下标不受影响。然而，`asort()` 和 `asorti()` 函数受影响。因此，如果 `IGNORECASE` 不等于零，`/aB/` 将匹配所有字符串 `ab`、`aB`、`Ab` 和 `AB`。与所有 AWK 变量一样，`IGNORECASE` 的初始值为零，因此所有正则表达式和字符串操作通常是大小写敏感的。

#### `LINT`

从 AWK 程序内部动态控制 `--lint` 选项。当为 true 时，`gawk` 打印 lint 警告。当为 false 时，不打印。当赋值字符串值 `fatal` 时，lint 警告变为致命错误，与 `--lint=fatal` 完全相同。任何其他真值仅打印警告。

#### `NF`

当前输入记录中的字段数量。

#### `NR`

为止可见的输入记录总数。

#### `OFMT`

数字的输出格式，默认为 `%.6g`。

#### `OFS`

输出字段的分隔符，默认为空格。

#### `ORS`

输出记录分隔符，默认为换行符。

#### `PREC`

任意精度浮点数的工作精度，默认为 53。

#### `PROCINFO`

此数组的元素提供了对正在运行的 AWK 程序信息的访问。在某些系统上，数组中可能存在从 `group1` 到 `groupn` 的元素（其中 `n` 是某个整数），这表示该进程拥有的辅助组数量。使用 `in` 运算符来测试这些元素的存在。以下元素保证可用：

- `PROCINFO["egid"]`

  `getegid(2)` 系统调用的值。

- `PROCINFO["strftime"]`

  `strftime()` 的默认时间格式字符串。

- `PROCINFO["euid"]`

  `geteuid(2)` 系统调用的值。

- `PROCINFO["FS"]`

  如果正在使用 `FS` 进行字段分割，则为 `FS`；如果正在使用 `FPAT` 进行字段分割，则为 `FPAT`；如果正在使用 `FIELDWIDTHS` 进行字段分割，则为 `FIELDWIDTHS`。

- `PROCINFO["identifiers"]`

  一个子数组，通过 AWK 程序文本中使用的所有标识符名称进行索引。值表示 `gawk` 在完成程序解析后关于这些标识符的信息；它们在程序运行期间*不会*被更新。对于每个标识符，该元素的值为以下值之一：

  - `array`

    该标识符是一个数组。

  - `builtin`

    该标识符是一个内置函数。

  - `extension`

    通过 `@load` 或 `-l` 加载的扩展函数。

  - `scalar`

    该标识符是一个标量。

  - `untyped`

    该标识符未定义类型（可以作为标量或数组使用，`gawk` 尚不知道）。

  - `user`

    该标识符是用户定义的函数。

- `PROCINFO["gid"]`

  `getgid(2)` 系统调用的值。

- `PROCINFO["pgrpid"]`

  当前进程的进程组 ID。

- `PROCINFO["pid"]`

  当前进程的 ID。

- `PROCINFO["ppid"]`

  当前进程的父进程 ID。

- `PROCINFO["uid"]`

  `getuid(2)` 系统调用的值。

- `PROCINFO["sorted_in"]`

  如果此元素存在于 `PROCINFO` 中，则其值控制 `for` 循环中遍历数组元素的顺序。支持的值有 `@ind_str_asc`、`@ind_num_asc`、`@val_type_asc`、`@val_str_asc`、`@val_num_asc`、`@ind_str_desc`、`@ind_num_desc`、`@val_type_desc`、`@val_str_desc`、`@val_num_desc` 和 `@unsorted`。

  该值也可以是如下定义的比较函数的名称：

  ```awk
  function cmp_func(i1, v1, i2, v2)
  ```

  其中 `i1` 和 `i2` 是索引，`v1` 和 `v2` 是两个比较元素的对应值。它应该返回小于、等于或大于 0 的数字，取决于数组元素的排序方式。



`PROCINFO["input", "READ_TIMEOUT"]`：从`input`读取数据的毫秒超时时间，其中`input`是重定向字符串或文件名。值为 0 或小于 0 表示无超时。

`PROCINFO["mpfr_version"]`：`gawk`用于支持任意精度数的 GNU MPFR 库版本。如果未在`gawk`中编译 MPFR 支持，则不存在此条目。

`PROCINFO["gmp_version"]`：`gawk`用于支持任意精度数的 GNU MP 库版本。如果未在`gawk`中编译 MPFR 支持，则不存在此条目。

`PROCINFO["prec_max"]`：GNU MPFR 库支持的任意精度浮点数的最大精度。如果未在`gawk`中编译 MPFR 支持，则不存在此条目。

`PROCINFO["prec_min"]`：GNU MPFR 库允许的任意精度浮点数的最小精度。如果未在`gawk`中编译 MPFR 支持，则不存在此条目。

`PROCINFO["api_major"]`：扩展 API 的主版本。如果无法加载动态扩展，则不存在此条目。

`PROCINFO["api_minor"]`：扩展 API 的次版本。如果无法加载动态扩展，则不存在此条目。

`PROCINFO["version"]`：`gawk`的版本。

`ROUNDMODE`：数字任意精度算术时使用的舍入模式，默认为`N`（IEEE-754 舍入到偶模式）。接受的值为`N`或`n`（舍入到偶）、`U`或`u`（向正舍入）、`D`或`d`（向负舍入）、`Z`或`z`（向零舍入），以及如果你的 GNU MPFR 库版本支持，`A`或`a`（舍入到远离）。

`RS`：输入记录分隔符，默认为换行符。

`RT`：记录终止符。`gawk`将`RT`设置为匹配的输入文本。

`RSTART`：`match()`匹配到的第一个字符的索引；无匹配则为 0。

`RLENGTH`：`match()`匹配的字符串长度；无匹配则为 -1。

`SUBSEP`：用于分隔多个下标的字符。

## 数组

数组使用方括号`[`和`]`之间的表达式进行索引。如果表达式是一个列表，则下标是由`SUBSEP`连接而成的字符串。AWK 中的数组都是关联数组，即通过字符串值索引。

特殊运算符`in`可用于测试数组是否存在某个索引：

```
if (val in array) print array[val]
```

如果数组有多个下标，使用`(i, j) in array`。`in`结构也可以用于`for`循环遍历数组的所有元素。然而，`(i, j) in array`仅适用于测试，不适用于`for`循环。

可以使用`delete`语句从数组中删除元素。通过指定数组名而不带下标也可以删除整个数组的内容。

`gawk`支持真正的多维数组。它不需要像 C 或 C++ 那样要求此类数组是“矩形的”。例如：

```
a[1] = 5
a[2][1] = 6
a[2][2] = 7
```

**注意**：你可能需要告诉`gawk`数组元素实际上是一个子数组，以便在需要数组的地方（如`split()`的第二个参数）中使用它。可以通过在子数组中创建一个元素并将其删除来实现。

变量和字段可以是（浮点）数字、字符串或两者兼有。变量值的解释方式取决于其语境。如果在数字表达式中使用它，它将被视为数字；如果作为字符串使用，它将被视为字符串。

要强制将变量视为数字，请给它加上 0；要强制视为字符串，请将其与空字符串连接。

未初始变量具有数值值 0 和字符串值""（空字符串）。

当必须将字符串转换为数字时，使用`strtod`(3)完成转换。将数字转换为字符串则使用`CONVFMT`的值作为`sprintf`(3)的格式化字符串，并将变量的数值值作为参数。然而，尽管 AWK 中的所有数字都是浮点数，但整数值*总是*被转换为整数。因此，给定

```
CONVFMT = "%2.2f"
a = 12
b = a ""
```

变量`b`的字符串值为`12`而不是`12.00`。

**注意**：在 POSIX 模式下运行时（例如使用`--posix`选项），请注意区域设置（locale）可能会影响处理数字的方式：传递给`gawk`的数字的小数符必须符合你的区域设置预期，无论是逗号（,）还是点（.）。

`gawk`执行比较如下：如果两个变量都是数字，则进行数值比较。如果其中一个值是数字而另一个具有“数值字符串”字符串值，则也以数值方式进行比较。否则，将数值值转换为字符串并进行字符串比较。当然，两个字符串是作为字符串进行比较的。

注意，字符串常量（如`57`）*不是*数值字符串，而是字符串常量。“数值字符串”的概念仅适用于字段、`getline`输入、`FILENAME`、`ARGV`元素、`ENVIRON`元素以及由`split()`或`patsplit()`创建的数组元素的值。基本思想是，只有*用户输入*中看起来像数字的部分应该被那样处理。

### 八进制和十六进制常量

你可以在 AWK 程序源代码中使用 C 风格的八进制和十六进制常量。例如，八进制值`011`等于十进制`9`，十六进制值`0x11`等于十进制 17。

### 字符串常量

AWK 中的字符串常量是双引号之间的字符序列（如`value`）。在字符串内部，可以识别某些类似于 C 的*转义序列*。这些是：

`\\`

字面反斜杠。

`\a`

“警告”字符；通常是 ASCII BEL 字符。

`\b`

退格符。

`\f`

分页符。

`\n`

换行符。

`\r`

回车符。

`\t`

水平制表符。

`\v`

垂直制表符。

`\x*hex digits*`

由`\x`后跟的十六进制数字字符串表示的字符。与 ISO C 一样，所有后续十六进制数字都被视为转义序列的一部分。（这一特征应该告诉我们关于委员会化语言设计的一些信息。）例如，`\x1B`是 ASCII ESC（转义）字符。

`\*ddd*`

由 1、2 或 3 位八进制数字序列表示的字符。例如，`\033`是 ASCII ESC（转义）字符。

`\*c*`

字面字符`c`。

转义序列也可以用在常量正则表达式内部（例如，`/[ \t\f\n\r\v]/`匹配空白字符）。

在兼容模式下，八进制和十六进制转义序列表示的字符在用于正则表达式常量时被视为字面量。因此，`/a\52b/`等同于`/a\*b/`。

## 模式与动作

AWK 是一种行导向的语言。模式在先，动作在后。动作语句被包含在`{`和`}`之间。模式可以缺失，动作也可以缺失，但两者不能同时缺失。如果模式缺失，则对每一条输入记录执行动作。缺失的动作等同于

```
{ print }
```

这打印整个记录。

注释以`#`字符开始，持续到行尾。可以使用空行来分隔语句。通常，语句以换行符结束，但以逗号、`{`、`?`、`:`、`&&`或`||`结尾的行除外。以`do`或`else`结尾的行其语句也会自动延续到下一行。在其他情况下，可以通过以`\`结尾来延续行，在这种情况下，换行符会被忽略。

可以通过`;`分隔符将多个语句放在同一行中。这既适用于模式-动作对中动作部分内的语句（通常情况），也适用于模式-动作语句本身。

### 模式

AWK 模式可以是以下内容之一：

`BEGIN`
`END`
`BEGINFILE`
`ENDFILE`
`/*regular expression*`
`/*relational expression*`
`pattern && pattern`
`pattern || pattern`
`pattern ? pattern : pattern`
`(pattern)`
`!pattern`
`pattern1, pattern2`

`BEGIN`和`END`是两种特殊的模式，不对输入进行测试。所有`BEGIN`模式的动作部分都会合并，就像所有语句都写在一个`BEGIN`规则中一样。这些动作在读取任何输入之前执行。同样，所有的`END`规则都会合并，并在读取所有输入后执行。

## 正则表达式

正则表达式是 *egrep* 中找到的扩展类型。它们由以下字符组成：

其中`r`、`n`、`m`是正则表达式或数字。大括号内的一个或两个数字表示*区间表达式*。如果括号内有一个数字，则前面的正则表达式`r`将重复`n`次。如果有两个用逗号隔开的数字，则`r`将重复`n`到`m`次。如果一个数字后面跟着一个逗号，则`r`将至少重复`n`次。

`\y`

匹配单词开头或结尾的空字符串。

`\B`

匹配单词内部的空字符串。

`\<`

匹配单词开头的空字符串。

`\>`

匹配单词结尾的空字符串。

`\s`

匹配任何空白字符。

`\S`

匹配任何非空白字符。

`\w`

匹配任何单词组成字符（字母、数字或下划线）。

`\W`

匹配任何非单词字符的字符。

`\``

匹配缓冲区（字符串）开头的空字符串。

`\'`

匹配缓冲区结尾的空字符串。

在字符串常量中有效的转义序列（参见**字符串常量**）在正则表达式中同样有效。

## 字符类

字符类是 POSIX 标准引入的一项特性。字符类是描述具有特定属性的字符列表的特殊表示法，但字符本身可以根据国家和/或字符集的不同而异。例如，字母的定义在各地是不一样的。

字符类仅在正则表达式的字符列表的括号*内部*时才有效。字符类由`[:`、表示该类的关键字以及`:]`组成。POSIX 标准定义的字符类包括：

`[:alnum:]`

字母数字字符。

`[:alpha:]`

字母。

`[:blank:]`

空格或制表符字符。

`[:cntrl:]`

控制字符。

`[:digit:]`

数字字符。

`[:graph:]`

既可打印又可见的字符。（空格是可打印的，但不可见，而`a`两者都是。）

`[:lower:]`

小写字母。

`[:print:]`

可打印字符（不是控制字符的字符）。

`[:punct:]`

标点符号（不是字母、数字、控制字符或空格字符的字符）。

`[:space:]`

空白字符（例如空格、制表符和换页符等）。

`[:upper:]`

大写字母。

`[:xdigit:]`

十六进制数字字符。

例如，在 POSIX 标准之前，为了匹配字母数字字符，你必须编写`/[A-Za-z0-9]/`。如果你的字符集包含其他字母，它将无法匹配这些字符；如果你的字符集排序方式与 ASCII 不同，它甚至无法匹配 ASCII 字母数字字符。使用 POSIX 字符类，你可以编写`/[[:alnum:]]/`，这会匹配你字符集中的字母和数字字符，无论它是什么。

字符列表中还可以有两个额外的特殊序列。这些序列适用于非 ASCII 字符集，这些字符集可能包含由多个字符表示的单个符号（称为*排序元素*），也包含多个在*排序*（即排序）目的上等价的字符。（例如，在法语中，普通的`e`和带有重音符号的`e`是等价的。）

### 排序符号

排序符号是封装在`[`和`.]]`之间的多字符排序元素。例如，如果`ch`是一个排序元素，那么`[[.ch.]]`就是一个匹配该排序元素的正则表达式，而`[ch]`是一个匹配`c`或`h`的正则表达式。

### 等价类

等价类是等价字符列表的特定区域名称。该名称封装在`[=`和`=]`之间。例如，名称`e`可能用于表示所有的`e`、`e'`和`e``。在这种情况下，`[[=e=]]`是一个匹配`e`、`e'`或`e``中任意一个的正则表达式。

这些特性在非英语区域非常有价值。`gawk`用于正则表达式匹配的库函数目前仅识别 POSIX 字符类；它们不识别排序符号或等价类。

`\y`、`\B`、`\<`、`\>`、`\s`、`\S`、`\w`、`\W`、`\``和`\'`运算符是`gawk`特有的；它们是基于 GNU 正则表达式库功能的扩展。

各种命令行选项控制 `gawk` 如何解释正则表达式中的字符。

### 选项

在默认情况下，`gawk`提供 POSIX 正则表达式的所有功能以及上述的 GNU 正则表达式操作符。

`--posix`

仅支持 POSIX 正则表达式，GNU 操作符不再特殊。（例如，`\w`匹配字面量`w`）。

`--traditional`

匹配传统的 UNIX *awk* 正则表达式。GNU 操作符不再特殊，且不可用区间表达式。由八进制和十六进制转义序列描述的字符被视为字面量，即使它们代表正则表达式的元字符。

`--re-interval`

允许在正则表达式中使用区间表达式，即使提供了`--traditional`。

## 动作

动作语句封装在大括号`{}`中。动作语句由 C 语言中赋值、条件和循环语句组成。

### 运算符

AWK 中的运算符按优先级从高到低排序如下：

`(...)`

分组。

`$`

字段引用。

`++ --`

递增和递减，前缀和后缀。

`^`

幂（也可用于赋值）。

`+ - !`

一元加、一元减和逻辑取反。

`* / %`

乘法、除法和取模。

`+ -`

加法和减法。

`*`

字符串拼接。

`| &`

用于`getline`、`print`和`printf`的管道输出。

`< > ==`

关系运算符。

`~ !~`

正则表达式匹配、否定匹配。**注意**：不要在`~`或`!~`的左侧使用正则表达式`/foo/`。仅使用右侧。表达式`/foo/ ~ exp`等同于`($0 ~ //)`。这通常不是你想要的。

`in`

数组成员关系。

`&&`

逻辑与。

`||`

逻辑或。

`?:`

C 条件表达式。其形式为`expr1 ? expr2 : expr3`。如果`expr1`为真，表达式的值为`expr2`，否则为`expr3`。只有`expr2`或`expr3`会求值。

`= += -= *= /= ^=`

赋值。支持绝对赋值`var = value`和运算符赋值（其他形式）。

## 控制语句

控制语句如下所示：

`if (condition) statement [else statement]`

`while (condition) statement`

`do statement while (condition)`

`for (expr1; expr2; expr3) statement`

`for (var in array) statement`

`break`
`continue`
`delete array[index]`
`exit`

`switch (expression) { case value|regex: statement ... [default: statement] }`

## I/O 语句

输入输出语句如下：

`close(file [, how])`

关闭文件、管道或协进程。可选的`how`只应在关闭指向协进程的双向管道的一端时使用。它必须是一个字符串，`to`或`from`。

`getline`

从下一个输入记录设置`$0`；设置`NF`、`NR`、`FNR`、`RT`。

`getline < file`

从`file`的下一条记录设置`$0`；设置`NF`、`RT`。

`getline var`

从下一个输入记录设置`var`；设置`NR`、`FNR`、`RT`。

`getline var < file`

从`file`的下一条记录设置`var`、`RT`。

`command | getline [var]`

运行`command`并将其输出管道到`$0`或`var`（如上所示），以及设置`RT`。

`command |& getline [var]`

将`command`作为协进程运行，并将其输出管道到`$0`或`var`（如上所示），以及设置`RT`。协进程是`gawk`的一个扩展。（`command`也可以是一个 socket。参见**特殊文件名**节。）

`next`

停止处理当前输入记录。读取下一个输入记录，并从 AWK 程序中的第一个模式重新开始处理。当到达输入数据的末尾时，`gawk`会执行任何`END`规则。

`nextfile`

停止处理当前输入文件。读取的下一个输入记录将来自下一个输入文件。`FILENAME`和`ARGIND`会更新，`FNR`重置为 1，并从 AWK 程序中的第一个模式重新开始处理。当到达输入数据的末尾时，`gawk`会执行任何`END`规则。

`print`

打印当前记录。输出记录以`ORS`的值终止。

`print expr-list`

打印表达式。每个表达式之间用`OFS`的值分隔。输出记录以`ORS`的值终止。

`print expr-list > file`

在`file`上打印表达式。每个表达式之间用`OFS`的值分隔。输出记录以`ORS`的值终止。

`printf fmt, expr-list`

格式化并打印。参见**printf 语句**。

`printf fmt, expr-list > file`

在`file`上进行格式化并打印。

`system(cmd-line)`

执行命令`cmd-line`，并返回退出状态。（这在非 POSIX 系统上可能无效。）

`fflush([file])`

刷新与打开的输出文件或管道`file`关联的任何缓冲区。如果`file`缺失或为空字符串，则刷新所有打开的输出文件和管道。

`print`和`printf`允许额外的输出重定向。

`print ... >> file`

将输出追加到`file`。

`print ... | command`

将输出管道到`command`。



## 写入管道

`print ... |& command`

将数据发送到协进程或 socket。（另见下文的“特殊文件名”节。）

`getline` 命令在成功时返回 1，在文件末尾返回 0，在错误时返回 -1。发生错误时，`ERRNO` 被设置为描述该问题的字符串。

**注意**：打开双向 socket 失败会导致向调用函数返回非致命错误。在使用管道、协进程或 socket 进行 `getline`，或在循环内 `print` 或 `printf` 时，你必须使用 `close()` 创建命令或 socket 的新实例。AWK 在它们返回 EOF 时不会自动关闭管道、socket 或协进程。

### `printf` 语句

AWK 版本的 `printf` 语句和 `sprintf()` 函数（见下文）接受以下转换规范格式：

`%c`

单个字符。如果用于 `%c` 的参数是数字，则将其视为字符并打印。否则，假设参数是字符串，并仅打印该字符串的首字符。

`%d`、`%i`

十进制数字（整数部分）。

`%e`、`%E`

形式为 `[-]*d.dddddde[+-]*dd` 的浮点数。`%E` 格式使用 `E` 代替 `e`。

`%f`、`%F`

形式为 `[-]*d.ddddd` 的浮点数。`%F` 格式使用大写字母。

`%g`、`%G`

短格式的浮点数。`%G` 格式使用 `G` 代替 `g`。

`%o`

八进制数字。

`%u`

无符号十进制数字。

`%s`

字符串。

`%x`、`%X`

十六进制数字。`%X` 格式使用大写。

`%%`

单个 `%` 字符；可选的参数位于 `%` 之间：

- `count$`

  位置参数符，主要用于格式化字符串中。

- `-`

  左对齐。

- `+`

  在数字转换时始终显示符号标志，即使数值为正。

- `#`

  某些字母的替代形式。

- `0`

  该标志表示应用 0 填充而不是空格。

- `width`

  字段填充宽度。

- `.prec`

  指定精度。对于 `%e`、`%E`、`%f` 和 `%F` 格式，它指定小数点右侧的位数。对于 `%g` 和 `%G` 格式，它指定有效数字数。对于 `%s`，它指定要打印字符串的最大字符数。

- `*`

  ISO C `printf` 方案支持的动态宽度和精度。在宽度或精度规范处使用 `*` 会导致其值从 `printf` 或 `sprintf()` 的参数列表中获取。要在位置参数符中使用动态宽度或精度，在格式字符串的 `*` 之后提供 `count$`。例如，`%3$*$.1$s`。

- `'`

  单引号标志，表示数字转换时始终显示符号，即使数值为正。

#### 特殊文件名

当从 `print` 或 `printf` 将输出重定向到文件，或者通过 `getline` 从文件读取时，`gawk` 内部识别某些特殊文件名。这些文件名允许访问从 `gawk` 的父进程（通常是 shell）继承的文件描述符。这些文件名也可以在命令行用于命名数据文件。文件名如下：

`-`

标准输入。

`/dev/stdin`

标准输入。

`/dev/stdout`

标准输出。

`/dev/stderr`

标准错误输出。

`/dev/fd/*n*`

与打开的文件描述符 `n` 关联的文件。这些对于错误消息特别有用。例如：

```awk
print "You blew it!" > "/dev/stderr"
```

否则你可能需要使用：

```awk
print "You blew it!" | "cat 1>&2"
```

以下特殊文件名可以配合 `|&` 协进程运算符创建 TCP/IP 网络连接：

`/inet/tcp/*lport*/*rhost*/*rport*`

`/inet4/tcp/*lport*/*rhost*/*rport*`

`/inet6/tcp/*lport*/*rhost*/*rport*`

用于从本地端口 `lport` 到远程主机 `rhost` 远程端口 `rport` 的 TCP/IP 连接。使用端口 `0` 由系统自动选择端口。使用 `/inet4` 强制使用 IPv4 连接，使用 `/inet6` 强制使用 IPv6 连接。普通的 `/inet` 使用系统默认值（极率是 IPv4）。

`/inet/udp/*lport*/*rhost*/*rport*`

`/inet4/udp/*lport*/*rhost*/*rport*`

`/inet6/udp/*lport*/*rhost*/*rport*`

类似，但使用 UDP/IP 代替 TCP/IP。

### 数值函数

AWK 具有以下内置算术函数：

`atan2(y, x)`

以弧度返回 `y/x` 的反正切值。

`cos(expr)`

返回 `expr` 的余弦值，单位为弧度。

`exp(expr)`

指数函数。

`int(expr)`

截断为整数。

`log(expr)`

自然对数函数。

`rand()`

返回一个在 0 到 1 之间的随机数 `N`，使得 `0 ≤ N < 1`。

`sin(expr)`

返回 `expr` 的正弦值，单位为弧度。

`sqrt(expr)`

返回 `expr` 的平方根。

`srand([expr])`

使用 `expr` 作为随机数生成器的种子。如果没有提供 `expr`，则使用当天时间。返回随机数生成器的上一个种子。

### 字符串函数

`Gawk` 具有以下内置字符串函数：

`asort(s [, d [, how]])`

返回源数组 `s` 中的元素个数。使用 `gawk` 比较值的标准规则对 `s` 的内容进行排序，并将排序后的值 `s` 的索引替换为从 1 开始的连续整数。如果指定了可选的目标数组 `d`，则先将 `s` 复制到 `d`，然后对 `d` 进行排序，保持源数组 `s` 的索引不变。可选字符串 `how` 控制方向和比较模式。`how` 的有效值可以是 `PROCINFO["sorted_in"]` 中任何合法的字符串。它也可以是 `PROCINFO["sorted_in"]` 中描述的自定义定义比较函数名。

`asorti(s [, d [, how]])`

返回源数组 `s` 中的元素个数。行为与 `asort()` 相同，但使用数组 `indices` 进行排序，而不是数组值。完成后，数组按数字进行索引，而其值是原始索引的值。原始值将丢失；因此，如果你想保留原始值，请提供第二个数组。可选字符串 `how` 的目的与上述 `asort()` 的描述相同。

`gensub(r, s, h [, t])`

在目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果 `h` 是以 `g` 或 `G` 开头的字符串，则将所有 `r` 的匹配项替换为 `s`。否则，`h` 是一个数字，表示替换 `r` 的第几个匹配项。如果提供 `t`，则改用 `$0`。在替换文本 `s` 中，可以使用序列 `\n`（其中 `n` 是 1 到 9 的数字）表示匹配第 `n` 个括号子表达式的文本。序列 `\0` 代表整个匹配文本，字符 `&` 也是如此。与 `sub()` 和 `gsub()` 不同，修改后的字符串作为函数的返回结果，原始目标字符串不会改变。

`gsub(r, s [, t])`

对于字符串 `t` 中每个匹配正则表达式 `r` 的子字符串，替换字符串 `s`，并返回替换次数。如果未提供 `t`，则使用 `$0`。替换文本中的 `&` 被替换为实际匹配的文本。使用 `\&` 获取字面量上的 `&`。（这必须写为 `\\&`；请参阅 *GAWK: Effective AWK Programming* 以详细讨论关于 `sub()`、`gsub()` 和 `gensub()` 替换文本中 `&` 和反斜杠的规则。）

`index(s, t)`

返回字符串 `t` 在字符串 `s` 中的索引，如果 `t` 不存在则返回 0。（这意味着字符索引从 1 开始）。使用正则表达式常量作为 `t` 是致命错误。

`length([s])`

返回字符串 `s` 的长度，如果未提供 `s`，则返回 `$0` 的长度。作为非标准扩展，带有数组参数时，`length()` 返回数组中的元素个数。

`match(s, r [, a])`

返回正则表达式 `r` 在 `s` 中出现的位置，如果 `r` 不存在则返回 0，并设置 `RSTART` 和 `RLENGTH` 的值。

`patsplit(s, a [, r])`

将字符串 `s` 拆分为数组 `a` 和基于正则表达式 `r` 的分隔符 `seps`。如果省略 `r`，则使用 `FPAT`。`seps[i]` 是 `a[i]` 和 `a[i+1]` 之间匹配的内容。

`split(s, a [, r])`

将字符串 `s` 拆分为数组 `a` 和基于正则表达式 `r` 的分隔符 `seps`，返回字段数。如果省略 `r`，则使用 `FS`。首先清除数组 `a` 和 `seps`。

`sprintf(fmt, expr-list)`

根据 `fmt` 打印 `expr-list` 并返回生成的字符串。

`substr(s, i [, n])`

返回 `s` 从 `i` 开始的最多 `n` 个字符的子字符串。如果省略 `n`，则使用 `s` 的剩余部分。

`sub(r, s [, t])`

与 `gsub()` 类似，但仅替换第一个匹配项。

`tolower(str)`

返回 `str` 的副本，将其所有大写字母转换为对应的小写字母。非字母保持不变。

`toupper(str)`

返回 `str` 的副本，将其所有小写字母转换为对应的大写字母。非字母保持不变。

`strtonum(str)`

检查 `str` 并返回其数值值。如果 `str` 以 `0` 开头，则将其视为八进制数。如果 `str` 以 `0x` 或 `0X` 开头，则将其视为十六进制数。否则假设它是十进制数。

### 时间函数

由于 AWK 程序的一个主要用途之一是处理包含时间戳信息的日志文件，`gawk` 提供了以下函数用于获取时间戳并格式化它们。

`mktime(datespec)`

将 `datespec` 转换为与 `systime()` 返回格式相同的时间戳，并返回结果。`datespec` 是格式为 `YYYY MM DD HH MM SS[ DST]` 的字符串。该字符串包含六或七个数字，分别代表：包含世纪的完整年份、1 到 12 的月份、1 到 31 的日期、0 到 23 的小时、0 到 59 的分钟、0 到 60 的秒，以及一个可选的夏令标志。这些数字的值不需要在指定的范围内；例如，小时为 `-1` 表示在午夜前 1 小时。假设使用零起始的格里历历，年份 0 在于年份 1 前，年份 -1 在于年份 0 前。假设时间为本地时区时间。如果夏令标志为正数，则假设时间为夏令时；如果为零，则假设为标准时间；如果为负（默认值），`mktime()` 尝试确定指定时间是否处于夏令时。如果 `datespec` 不包含足够的元素，或者结果的时间超出范围，则 `mktime()` 返回 -1。

`strftime(format [, timestamp [, utc-flag]])`

根据 `format` 中的规范格式化 `timestamp`。如果 `utc-flag` 存在且非零或非空，则结果为 UTC，否则结果为本地时间。`timestamp` 应具有与 `systime()` 返回的相同格式。如果 `timestamp` 缺失，则使用当前时间。如果 `format` 缺失，则使用等同于 `date(1)` 输出的默认格式。默认格式在 `PROCINFO[strftime]` 中可用。请参考 ISO C 中 `strftime()` 函数的规范以获取保证可用的格式转换。

`systime()`

返回当前时间，单位为自 Epoch 以来的秒数（POSIX 系统上为 1970-01-01 00:00:00 UTC）。

### 位操作函数

`Gawk` 提供了以下位操作函数。这些函数通过将双精度浮点值转换为 `uintmax_t` 整数，执行操作，然后将结果转换回浮点数。这些函数是：

`and(v1, v2 [, ...])`

返回参数列表中提供的值的按位与（AND）结果。必须至少有两个值。

`compl(val)`

返回 `val` 的按位取反（补）。

`lshift(val, count)`

返回 `val` 向左移动 `count` 位后的值。

`or(v1, v2 [, ...])`

返回参数列表中提供的值的按位或（OR）结果。必须至少有两个值。

`rshift(val, count)`

返回 `val` 向右移动 `count` 位后的值。

`xor(v1, v2 [, ...])`

返回参数列表中提供的值的按位异或（XOR）结果。必须至少有两个值。

### 类型函数

以下函数用于多维数组。

`isarray(x)`

如果 `x` 是数组，则返回 true，否则返回 false。

### 国际化函数

在 AWK 程序内部可以使用以下函数在运行时翻译字符串。有关更多详细信息，请参阅 *GAWK: Effective AWK Programming*。

`bindtextdomain(directory [, domain])`

指定 `gawk` 查找 `.gmo` 文件的目录，以防它们未或无法放置在“标准”位置（例如在测试期间）。它返回 `domain` 被“绑定”的目录。

默认 `domain` 是 `TEXTDOMAIN` 的值。如果 `directory` 为空字符串 `()`，则 `bindtextdomain()` 返回给定 `domain` 的当前绑定关系。

`dcgettext(string [, domain [, category]])`

返回在文本域 `domain` 中针对区域类别 `category` 的 `string` 翻译。`domain` 的默认值为 `TEXTDOMAIN` 的当前值。`category` 的默认值为 `LC_MESSAGES`。

如果你提供了 `category` 的值，它必须是一个等于 *GAWK: Effective AWK Programming* 中描述的已知区域类别之一的字符串。你必须提供一个文本域。如果你想使用当前域，请使用 `TEXTDOMAIN`。

`dcngettext(string1, string2, number [, domain [, category]])`

返回在文本域 `domain` 中针对区域类别 `category` 的 `string1` 和 `string2` 在 `number` 时的复数形式翻译。`domain` 的默认值为 `TEXTDOMAIN` 的当前值。`category` 的默认值为 `LC_MESSAGES`。

如果你提供了 `category` 的值，它必须是一个等于 *GAWK: Effective AWK Programming* 中描述的已知区域类别之一的字符串。你必须提供一个文本域。如果你想使用当前域，请使用 `TEXTDOMAIN`。

## 用户定义函数

AWK 中的函数定义如下：

```awk
function name(parameter list) {statements}
```

函数从模式（patterns）或动作（actions）执行。实际参数通过引用传递，其他变量通过值传递。由于函数最初并不是 AWK 的一部分，因此局部变量的规定相当笨拙：它们被声明为参数列表中的额外参数。例如：

```awk
function f(p, q, a, b) { ... }
```

函数调用中的左括号必须紧跟在函数名之后，中间不能有任何空白字符。此限制不适用于内置函数。

函数可以相互调用，也可以是递归的。用作局部变量的函数参数在函数调用时初始化为空字符串和数字零。使用 `return expr` 从函数返回一个值。如果没有提供值，或者函数通过运行到末尾返回，则返回值是未定义的。

作为 `gawk` 的扩展，函数可以被间接调用。要做到这一点，将要调用的函数名作为字符串赋值给变量。然后使用该变量并在前面加上 `@` 符号，就像函数名一样，如下：

```awk
function myfunc() { print "myfunc called" }
{ thefunc = "myfunc"; @thefunc() }
```

从 4.1.2 开始，这适用于用户定义函数、内置函数和扩展函数。

如果提供了 `--lint`，`gawk` 在解析时会对未定义的函数调用警告，而不是在运行时。在运行时调用未定义的函数是致命错误。

单词 `func` 可以代替 `function`，尽管这已过时。

## 动态加载新函数

你可以使用 `@load` 语句向运行中的 `gawk` 解释器动态添加新的内置函数。详细信息超出了本手册的范围；请参阅 *GAWK: Effective AWK Programming*。

## 信号

`gawk` 分析器接受两个信号。`SIGUSR1` 使其将配置文件和函数堆栈转储到配置文件（即 `awkprof.out` 或通过 `--profile` 指定的任何文件名），然后继续运行。`SIGHUP` 使 `gawk` 转储配置文件和函数堆栈然后退出。

## 国际化

字符串常量是封装在双引号中的字符序列。在非英语环境中，可以标记 AWK 程序中的字符串需要翻译成本地自然语言。此类字符串在 AWK 程序中用前导下划线（`_`）标记。例如，



```bash
gawk 'BEGIN { print "hello, world" }'
```

始终打印`hello, world`。但是，

```bash
gawk 'BEGIN { print _"hello, world" }'
```

在法国可能会打印`bonjour, monde`。

制作和运行一个本地化的 AWK 程序涉及以下几个步骤：

1. 添加一个`BEGIN`动作来为`TEXTDOMAIN`变量赋值，以便将文本域设置为与你的程序关联的名称：

   ```awk
   BEGIN { TEXTDOMAIN = "myprog" }
   ```

   这允许`gawk`找到与你的程序相关的`.gmo`文件。如果没有这一步，`gawk`将使用`messages`文本域，该域可能不包含你程序的翻译。

2. 在所有需要翻译的字符串开头加上下划线标记。

3. 如有必要，在程序中适当地使用`dcgettext()`和/或`bindtextdomain()`函数。

4. 运行`gawk --gen-pot -f myprog.awk > myprog.pot`为你的程序生成`.pot`文件。

5. 提供相应的翻译，并构建和安装相应的`.gmo`文件。

国际化特性在`GAWK: Effective AWK Programming`中有详细的描述。

## POSIX 兼容性

`gawk`的主要目标是与 POSIX 标准兼容，并与 Brian Kernighan 的最新版本`awk`。为此，`gawk`整合了以下用户可见特性，这些特性在 AWK 书中没有描述，但是 Brian Kernighan 版本`awk`的一部分，也是 POSIX 标准的一部分。

书中指出，命令行变量赋值发生在`awk`原本应将参数作为文件打开时，这是在`BEGIN`规则执行之后。然而，在较早的实现中，当这种赋值出现在任何文件名之前时，该赋值会在`BEGIN`规则运行之前发生。应用程序开始依赖这种“特性”。当`awk`更改以与其文档一致时，为了适应依赖旧行为的应用程序，添加了`-v`选项用于在程序执行前分配变量。（该特性已获得贝尔实验室和 GNU 开发者的共识。）

在处理参数时，`gawk`使用特殊选项`''`来指示参数的结束。在兼容模式下，它会对未定义的选项发出警告，但在其他情况下忽略它们。在正常操作中，这些参数会被传递给 AWK 程序处理。

AWK 书没有定义`srand()`的返回值。POSIX 标准规定它返回其正在使用的种子，以便跟踪随机数序列。因此，`gawk`中的`srand()`也返回其当前种子。

其他新特性包括：使用多个`-f`选项（来自 MKS `awk`）；`ENVIRON`数组；`\a`和`\v`转义序列（最初在`gawk`中实现并反馈到贝尔实验室版本）；`tolower()`和`toupper()`内置函数（来自贝尔实验室版本）；以及`printf`中的 ISO C 转换规范（首次在贝尔实验室版本中实现）。

## 历史特性

`gawk`支持历史 AWK 实现中的一个特性：调用内置函数`length()`时不仅可以不带参数，甚至可以不带括号！因此，

```awk
a = length# Holy Algol 60, Batman!
```

等同于以下：

```awk
a = length()
a = length($0)
```

使用这种特性是一种不良做法，如果在命令行上指定了`--lint`，`gawk`会对其使用发出警告。

## GNU 扩展

`Gawk`对 POSIX `awk`拥有极其大量的扩展。这些特性在本节中进行了描述。通过在调用`gawk`时使用`--traditional`或`--posix`选项，禁用此处描述的所有扩展。

以下`gawk`特性在 POSIX `awk`中不可用：

- 不对通过`-f`选项命名的文件进行路径搜索。因此`AWKPATH`环境变量不是特殊的。
- 没有文件包含机制（`gawk`的`@include`机制）。
- 没有动态添加用 C 编写的新函数的机制（`gawk`的`@load`机制）。
- `\x`转义序列。（使用`--posix`禁用。）
- 在`?`和`:`之后继续行的能力。（使用`--posix`禁用。）
- AWK 程序中的八进制和十六进制常量。
- `ARGIND`、`BINMODE`、`ERRNO`、`LINT`、`RT`和`TEXTDOMAIN`变量不是特殊的。
- `IGNORECASE`变量及其副作用无效。
- `FIELDWIDTHS`变量和固定宽度字段分割。
- `FPAT`变量和基于字段值的字段分割。
- `PROCINFO`数组无效。
- 将`RS`作为正则表达式使用。
- 用于 I/O 重定向的特殊文件名不被识别。
- 用于创建协进程的`|&`运算符。
- `BEGINFILE`和`ENDFILE`特殊模式无效。
- 使用空字符串作为`FS`的值以及`split()`的第三参数来分割单个字符的能力。
- `split()`的可选第四个参数，用于接收分隔符文本。
- `close()`函数的可选第二个参数。
- `match()`函数的可选第三个参数。
- 在`printf`和`sprintf()`中使用位置标识符的能力。
- 向`length()`传递数组的能力。
- `and()`、`asort()`、`asorti()`、`bindtextdomain()`、`dcgettext()`、`dcntext()`、`gensub()`、`lshift()`、`mktime()`、`or()`、`patsplit()`、`rshift()`、`strtonum()`、`systime()`和`xor()`函数。

## 环境变量

`AWKPATH`环境变量可以提供目录列表，`gawk`将搜索通过`-f`、`-i`和`--include`选项命名的文件。如果初始搜索失败，则在文件名后添加`.awk`再次搜索路径。

`AWLIBPATH`环境变量可以提供目录列表，`gawk`将搜索通过`-l`和`--load`选项命名的文件。

`GAWK_READ_TIMEOUT`环境变量可以指定从终端、管道或包括套接字的双向通信中读取输入时的毫秒级超时。

对于通过 socket 连接到远程主机，`GAWK_SOCK_RETRIES`控制重试次数，`GAWK_MSEC_SLEEP`控制重试之间的间隔。间隔以毫秒为单位。在不支持`usleep(3)`的系统上，该值将向上取整为整数秒。

如果环境中存在`POSIXLY_CORRECT`，则`gawk`的行为将与指定了`--posix`完全一样。如果指定了`--lint`，`gawk`会为此发出警告消息。

## 退出状态

如果带值使用`exit`语句，则`gawk`将以给定的数值退出。

否则，如果执行过程中没有问题，`gawk`将以 C 常量`EXIT_SUCCESS`的值退出。这通常为 0。

如果发生错误，`gawk`将以 C 常量`EXIT_FAILURE`的值退出。这通常为 1。

如果`gawk`因为致命错误退出，则退出状态为 2。在非 POSIX 系统上，该值可能映射到`EXIT_FAILURE`。

## 版本信息

本帮助页文档了`gawk`，版本 4.1。

## 作者

原始的 UNIX `awk`版本由贝尔实验室的 Alfred Aho、Peter Weinberger 和 Brian Kernighan 设计并实现。Brian Kernighan 继续对其进行维护和增强。

来自自由软件基金会的 Paul Rubin 和 Jay Fenlason 编写了`gawk`，以确保与第七版 UNIX 中分发的原始`awk`版本兼容。John Woods 贡献了许多错误修复工作。David Trueman 在 Arnold Robbins 的贡献下，使`gawk`与新版本的 UNIX `awk`兼容。Arnold Robbins 是目前的维护者。

请参阅`GAWK: Effective AWK Programming`以获取`gawk`及其文档贡献者的完整列表。

请查看`gawk`分发中的`README`文件，获取有关维护者以及当前支持哪些端口的最新信息。

## 错误报告

如果您在`gawk`中发现了错误，请向`bug-gawk@gnu.org`发送电子邮件。请包含您的操作系统及其修订版本、`gawk`的版本（通过`gawk --version`获取）、您用于编译它的 C 编译器，以及一个尽可能小的重现问题的测试程序和数据。

在发送错误报告之前，请执行以下操作。首先，验证您是否拥有最新版本的`gawk`。许多错误（通常是微妙的错误）在每个发布版本中都会修复，如果您的版本过旧，问题可能已经解决。其次，请查看将环境变量`LC_ALL`设置为`LC_ALL=C`是否会导致行为符合您的预期。如果是，则这是一个区域设置（locale）问题，可能可能不是真正的错误。最后，请仔细阅读本帮助页和参考手册，以确保您认为的错误确实是错误，而不是仅仅语言的特性。

无论您做什么，都不要在`comp.lang.awk`中发布错误报告。虽然`gawk`开发者偶尔会阅读这个新闻组，但在那里发布错误报告是报告错误的不可靠方法。相反，请使用上面提供的电子邮件地址。真的。

如果您正在使用 GNU/Linux 或基于 BSD 的系统，您可能希望向您发行版的供应商提交错误报告。这是可以的，但请也向官方电子邮件地址发送副本，因为无法保证错误报告会被转发给`gawk`维护者。

## 缺陷

考虑到命令行变量赋值功能，`-F`选项并非必要；它仅保留用于向后兼容。

## 另另

`egrep(1)`、`sed(1)`、`getpid(2)`、`getppid(2)`、`getpgrp(2)`、`getuid(2)`、`geteuid(2)`、`getgid(2)`、`getegid(2)`、`getgroups(2)`、`usleep(3)`

`The AWK Programming Language`，Alfred V. Aho、Brian W. Kernighan、Peter J. Weinberger，Addison-Wesley，1988。ISBN 0-201-07981-X。

`GAWK: Effective AWK Programming`，第 4.1 版，随`gawk`源码提供。该文档的当前版本可以在`http://www.gnu.org/software/gawk/manual`在线获取。

## 示例

```awk
打印并排序所有用户的登录名：BEGIN { FS = ":" } { print $1 | "sort" }
```

```awk
统计文件行数：{ nlines++ } END { print nlines }
```

```awk
在每行前加上其在文件中的编号：{ print FNR, $0 }
```

```awk
连接并行号（主题的一种变体）：{ print NR, $0 }
```

```awk
对特定数据行运行外部命令：tail -f access_log | awk '/myhome.html/ { system("nmap " $1 ">> logdir/myhome.html") }'
```

## 致谢

Brian Kernighan 在测试和调试期间提供了宝贵的帮助。我们感谢他。

## 拷贝许可

Copyright Š 1989, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999, 2001, 2002, 2003, 2004, 2005, 2007, 2009, 2010, 2011, 2012, 2013, 2014 Free Software Foundation, Inc.

许可制作并分发本帮助页的逐字副本，前提是所有副本上均保留版权声明和本许可声明。

在满足逐字拷贝条件的情况下，许可复制并分发本帮助页的修改版本，前提是整个派生作品必须按照与本声明相同的许可声明条款进行分发。

在满足上述修改版本条件下，许可将本帮助页翻译成另一种语言并复制分发，但许可声明可以在基金会批准的翻译文中说明。

* * *

# GCCCMD

## 名称

`gawkmd` - 一个控制台计算器

## 概要

`gawk`

## 描述

`gcawkmd`是`gawk`的控制台版本。

## 另另

`gawk`

# GCORE

## 名称

`gcore` - 生成核心文件

## 概要

`gcore [-o filename] pid`

## 描述

`gcore`产生运行中进程的核心转储。

### 选项

`-o filename`指定存放核心文件的文件名。

# GDB-ADD-INDEX

## 名称

`gdb-add-index` - 添加索引文件以加速 GDB

## 概要

`gdb-add-index filename`

## 描述

当 GDB 找到符号文件时，它会扫描文件符号以构建内部符号表。

GDB 提供了一种构建索引的方法，可以加快启动速度。

要确定文件是否包含此类索引，使用命令`readelf -S filename`：索引存储在名为`.gdb_index`的节。注意，对于不包含 DWARF 调试信息（名为`.debug_*`的节）的文件，不会生成索引。

更多信息请参阅 GDB 手册中的`Index Files`节点 —— shell 命令`info -f gdb -n 'Index Files'`。

根据 GNU 自由文档许可证 1.3 版本或由自由软件基金发布的任何更高版本的条款，允许复制、分发和/或修改此本文档；其中不变部分为“自由软件”和“自由软件需要自由文档”，前封面文本为“GNU 手册”，封底文本如下文 (a) 所示。

(a) FSF 的封底文本为：“你可以自由复制和修改本 GNU 手册。从 GNU Press 购买副本支持 FSF 开发 GNU 并促进软件自由。”

* * *

# GDB

## 名称

`gdb` - The GNU 调试器

## 语法概览

```text
gdb [-help] [-nh] [-nx] [-q] [-batch] [-cd=dir] [-f] [-b bps]
     [-tty=dev] [-s symfile] [-e prog] [-se prog] [-c core] [-p procID]
     [-x cmds] [-d dir] [prog|prog procID|prog core]
```

## 描述

像 GDB 这样的调试器的目的是让你看到另一个程序在执行时“内部”发生了什么——或者另一个程序在崩溃瞬间正在做什么。

GDB 可以执行四种主要功能（以及支持这些功能的其他功能），帮助你现场捕获 bug：

- 启动你的程序，并指定任何可能影响其行为的参数。
- 让你的程序在特定条件下停止。
- 在程序停止时，检查发生了什么。
- 修改你程序中的内容，以便你可以尝试修复某个 bug 的影响并继续学习另一个 bug。

你可以使用 GDB 调试用 C、C++、Fortran 和 Modula-2 编写的程序。

通过 shell 命令`gdb`启动 GDB。一旦启动，它将从终端读取命令，直到你通过 GDB 命令`quit`使其退出。你可以使用`help`命令从 GDB 自身获取在线帮助。

你可以在不带任何参数或选项的情况下运行`gdb`；但启动 GDB 最常用的方法是带一个或两个参数，指定一个可执行程序作为参数：

```text
gdb program
```

你也可以同时指定可执行程序和一个 core 文件启动：

```text
gdb program core
```

如果你想调试一个正在运行的进程，可以将进程 ID 作为第二个参数：

```text
gdb program 1234
gdb -p 1234
```

会将 GDB 挂载到进程`1234`（除非你也有一个名为`1234`的文件；GDB 会先检查 core 文件）。使用选项`-p`时，你可以省略`program`文件名。

这里是一些最频繁使用的 GDB 命令：

- `break [file:]function`：在`function`（在`file`中）设置断点。
- `run [arglist]`：启动你的程序（如果指定了则带有`arglist`）。
- `bt`：回溯（Backtrace）：显示程序堆栈。
- `print expr`：显示表达式的值。
- `c`：继续运行你的程序（在停止后，例如在断点处）。
- `next`：执行下一行程序（在停止后）；跳过行中的任何函数调用。
- `edit [file:]function`：查看程序当前停止的所在行。
- `list [file:]function`：打印程序当前停止位置附近的程序文本。
- `step`：执行下一行程序（在停止后）；进入行中的任何函数调用。
- `help [name]`：显示关于 GDB 命令`name`的信息，或关于使用 GDB 的通用信息。
- `quit`：退出 GDB。

关于 GDB 的完整细节，请参阅 Richard M. Stallman 和 Roland H. Pesch 写的《Using GDB: A Guide to the GNU Source-Level Debugger》。该文本可以通过`info`程序中的`gdb`条目在线获取。

### 选项



选项之外的任何参数都指定可执行文件和 `core` 文件（或进程 ID）；也就是说，遇到的第一个没有关联选项标志的参数等同于 `-se` 选项，第二个（如果有）如果是文件名，则等同于 `-c` 选项。许多选项都有长短形式；这里显示了这两种形式。如果你截断长形式，只要保留的选项足够足以消除歧义，它也能被识别。（如果需要的话，可以使用`+`而不是`-`来标记选项参数，尽管我们演示的是更常用的习惯。）

你提供的所有选项和命令行参数都是按顺序处理的。当使用`-x`选项时，顺序会产生影响。

- `-help`, `-h`: 列出所有选项并带简要说明。
- `-symbols=file`, `-s file`: 从文件`file`读取符号表。
- `-write`: 启用写入可执行文件和 `core` 文件。
- `-exec=file`, `-e file`: 使用`file`作为可执行文件。
- `-se=file`: 从`file`读取符号表。
- `-core=file`, `-c file`: 使用`file`作为 `core`。
- `-command=file`, `-x file`: 从`file`执行命令。
- `-directory=dir`, `-d dir`: 将`dir`添加到搜索文件的路径。
- `-nh`, `-n`: 不执行来自`~/.gdb`的命令。
- `-quiet`, `-q`: 不打印介绍和版权信息。
- `-batch`: 以批处理模式运行。
- `-cd=dir`: 使用`dir`作为工作目录运行 `GDB`。

# GDBM_DUMP

## 名称

`gdbm_dump` - 将 GDBM 数据库导出到文件

## 语法概览

```
gdbm_dump [-H FMT] [--format=FMT] DB_FILE [FILE]
```

`gdbm_dump`[`-Vh`] [`--help`] [`--usage`] [`--version`]

## 描述

`gdbm_dump` 工具为指定的 (3) 数据库文件创建转储。输出转储文件名由第二个参数`FILE`提供。如果未指定，输出将重定向到标准错误。

创建的转储文件可以作为参数传递给 (1) 工具，以便重新创建`DB_FILE`的精确副本。

### 选项

`-H`, `--format`=`FMT`

选择转储格式。值`binary`（或`0`）指示`gdbm_dump`生成二进制转储，与早期版本的`gdbm`（最高到 1.9 版本）兼容。值`ascii`（或`1`）指示其创建 ASCII 转储（这是默认值）。后者更优，因为除了实际数据外，它还包含元信息，允许 (1) 重新创建文件的精确副本。

`-h`, `--help`

打印简短的用法摘要。

`--usage`

打印可用选项列表。

`-V`, `--version`

打印程序版本

## 参见

(1), (1), (3)。

欲需有关`gdbm_dump`和其他`gdbm`工具的详细说明，请参考 Texinfo 格式提供的`GDBM Manual`。运行如下：

```
info gdbm
```

## 错误报告

请将错误报告至 <>。

## 版权

Copyright Š 2013 Free Software Foundation, Inc

许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>

这是自由软件：你可以自由地更改和分发它。在法律允许的范围内，不提供任何保证。

***

# GDBM_LOAD

## 名称

`gdbm_load` - 从转储文件重建 GDBM 数据库。

## 语法

`gdbm_load`[`-Mnr`] [`-b` `NUM`] [`-c` `NUM`]

[`-m` `MODE`] [`-u` `NAME`|`UID`[:`NAME`|`GID`]]

[`--block-size`=`NUM`] [`--cache-size`=`NUM`] [`--mmap`=`NUM`]

[`--mode`=`MODE`] [`--no-meta`] [`--replace`]

[`--user`=`NAME`|`UID`[:`NAME`|`GID`]] `FILE` [`DB_FILE`]

`gdbm_load`[`-Vh`] [`--help`] [`--usage`] [`--version`]

## 描述

从转储文件`FILE`创建`gdbm`数据库文件`DB_FILE`。如果没有提供`FILE`参数，则将创建的数据库输出到标准错误。

如果输入文件为 ASCII 转储格式，创建的数据库的模式和所有权将从转储信息中恢复。可以使用命令行选项覆盖（见下文）。

### 选项

`-b`, `--block-size`=`NUM`

设置块大小。

`-c`, `--cache-size`=`NUM`

设置缓存大小。

`-M`, `--mmap`

使用内存映射`-m`, `--mode`=`MODE`

设置数据库文件模式（八进制）。

`-n`, `--no-meta`

不尝试恢复数据库元数据（模式和所有权）。

`-r`, `--replace`

如果数据库存在，则替换其中的记录。

`-u`, `--user`=`NAME`|`UID`[:`NAME`|`GID`]

设置文件所有权。

`-h`, `--help`

打印简短的用法摘要。

`--usage`

打印可用选项列表。

`-V`, `--version`

打印程序版本

## 参见

(1), (1), (3)。

欲需有关`gdbm_load`和其他`gdbm`工具的详细说明，请参考 Texinfo 格式提供的`GDBM Manual`。运行如下：

```
info gdbm
```

## 错误报告

请将错误报告至 <>。

## 版权

Copyright Š 2013 Free Software Foundation, Inc

许可证 GPLv3+: GNU GPL 版本 3 或更高版本 <>

这是自由软件：你可以自由地更改和分发它。在法律允许的范围内，不提供任何保证。

***

# Gdbmtool

## 名称

`gdbmtool` - 检查和修改 GDBM 数据库

## 语法

`gdbmtool`[`-lmNnqrs`] [`-b` `SIZE`] [`-c` `SIZE`]

[`-f` `FILE`] [`--block-size`=`SIZE`]

[`--cache-size`=`SIZE`] [`--file`=`FILE`]

[`--block-size`=`SIZE`] [`--cache-size`=`SIZE`] [`--file`=`FILE`]

[`no-c`] [`--mmap`] [`--newdb`] [`no-lock`] [`--quiet`] [`--read-only`] [`--synchronize`]

`gdbmtool`[`-Vh`] [`--help`] [`--usage`] [`--version`]

## 描述

`gdbmtool` 工具允许你查看现有的 GDBM 数据库或创建一个。`FILE`参数指定要打开的数据库名称。如果未指定，将创建一个新数据库。

程序提供了一种交互模式，可以在其中向数据库输入命令。可用命令见下表。

如果数据库为 ASCII 转储格式，程序将对其解压并显示。如果数据库为二进制格式，程序将直接显示。

`gdbmtool` 还可以用于修改数据库。例如，你可以删除记录、添加新记录或更改数据库元数据。

`avail` - 打印可用列表

`bucket` `NUM` - 打印桶号`NUM`并将其设为当前

`cache` - 打印桶缓存

`close` - 关闭当前打开的数据库

`count` - 打印数据库中的条数

`current` - 打印当前桶

`delete` `KEY` - 删除具有指定`KEY`的记录

`dir` - 打印哈希目录

`fetch` `KEY` - 获取并显示具有指定`KEY`的记录

`first` - 获取并显示数据库中的第一条记录。后续记录可以使用 `next` 命令获取。

`hash` `KEY` - 计算并显示指定`KEY`的哈希值

`header` - 打印文件头。

`help` 或`?` - 打印简洁的命令摘要，显示每个命令字母、动词及其参数以及功能的简短描述。可选参数括在方括号中。

### 选项

`-b`, `--block-size`=`SIZE`

设置块大小。

`-c`, `--cache-size`=`SIZE`

设置缓存大小。

`-f`, `--file`=`FILE`

从`FILE`读取命令，而不是标准输入。

`-l`, `--no-lock`

禁用文件锁定。

`-m`, `--mmap`

不使用 (2)。

`-n`, `--newdb`

创建数据库，如果已存在则将其截断。

`-q`, `--quiet`

不打印初始横幅。

`-r`, `--read-only`

以只读模式打开数据库。

`-s`, `--synchronize`

每次写入后同步到磁盘。

`-h`, `--help`

打印简短的用法摘要。

`--usage`

打印可用选项列表。

`-V`, `--version`

打印程序版本

## Shell 命令

`avail` - 打印可用列表

`bucket` `NUM` - 打印桶号`NUM`并将其设为当前

`cache` - 打印桶缓存

`close` - 关闭当前打开的数据库

`count` - 打印数据库中的条数

`current` - 打印当前桶

`delete` `KEY` - 删除具有指定`KEY`的记录

`dir` - 打印哈希目录

`fetch` `KEY` - 获取并显示具有指定`KEY`的记录

`first` - 获取并显示数据库中的第一条记录。后续记录可以使用 `next` 命令获取。

`hash` `KEY` - 计算并显示指定`KEY`的哈希值

`header` - 打印文件头。

`help` 或`?` - 打印简洁的命令摘要，显示每个命令字母、动词及其参数以及功能的简短描述。可选参数括在方括号中。

`import` *FILE-NAME* [`replace`] [`nometa`]

从扁平转储文件 *FILE-NAME* 导入数据。如果提供了`replace`参数，则与现有记录具有相同键的任何记录将被替换。`nometa`参数将关闭从转储文件中恢复元信息。

`list`

列出数据库的内容。

`next` [*KEY*]

顺序访问：获取并显示下一条记录。如果提供了 *KEY*，则将获取该键记录之后的下一条记录。

`open` *FILE*

打开数据库文件 *FILE*。如果成功，将关闭任何之前打开的数据库。否则，如果操作失败，则当前打开的数据库将保持不变。

此命令从变量`open`、`lock`、`mmap`和`sync`中获取额外信息。详细描述这些变量请参见 `VARIABLES` 。

`quit`

关闭数据库并退出实用程序。

`reorganize`

重组数据库。`set` [*VAR*=*VALUE*...]。如果不带参数，则列出变量及其值。如果指定了参数，则设置变量。布尔变量可以通过指定变量名（可选前缀为`no`）来设置为`false`。

`source` *FILE*

从给定的 *FILE* 读取命令。

`status`

打印当前程序状态。

`store` *KEY* *DATA*

在数据库中根据给定的 *KEY* 存储 *DATA*。如果 *KEY* 已经存在，其数据将被替换。

`unset` *VARIABLE*...

取消列出的变量。

`version`

打印`gdbm`的版本。

## 数据定义

`define` 语句提供了一种定义键或内容结构的机制。它类似于`C`语言的`struct`声明：

```
`define``key`|`content`{`defnlist`}
```

*defnlist* 是成员声明的逗分隔列表。在 *defnlist* 中，换行符丢失了作为命令终止符的特殊含义，因此每个声明可以单独出现，并且可以插入任意数量的注释来记录该定义。

每个声明具有以下格式之一：

*`type``name``type``name`[`[`N`]`

其中 *type* 是数据类型，*name* 是成员名。第二种格式将成员 *name* 定义为由 *N* 个 *type* 元素组成的数组。

支持的类型有：

`type meaning char 单字节（有符号）short 有符号短整数 ushort 无符号短整数 int 有符号整数 unsigned 无符号整数 uint 同上 long 有符号长整数 ulong 无符号长整数 llong 有符号长长整数 ullong 无符号长整数 float 浮点数 double 双精度浮点数 string 字符数组（见下文 `NOTE`）stringz 零终止字符字符串`

在 *defnlist* 中可以使用以下对齐声明：

`offset` *N*

下一个成员从偏移量 *N* 开始。

`pad` *N*

在上一个成员后添加 *N* 字节的填充。

例如：

```
`define content { int status, pad 8, char id[3], stringz name }`
```

要定义一个由单个数据成员组成的数据，可以使用以下简化的构造：

```
`define``key`|`content`*type*
```

其中 *type* 是上述类型之一。

**NOTE**：只有当`string`类型是数据结构的最后一个或唯一成员时，才能合理地使用。因为没有提供关于数组中元素数量的信息，因此被解释为包含到数据项结束的所有字节。

## 变量

`confirm`，布尔值

在执行某些破坏性操作（如截断现有数据库）之前是否请求确认。默认值为`true`。

`ps1`，字符串

主提示符字符串。其值可以包含*转换规范符*，由`%`字符后跟另一个字符组成。这些规范符在生成的提示符中的展开方式如下：

```
序列扩展 %f (数据库文件名) %p (程序名) %P (包名 (gdbm)) %_ (水平空格 (ASCII 32)) %v (程序版本) %%
```

默认提示符为`%p>%_`。

`ps2`，字符串

次要提示符。关于其值的描述请参见`ps1`。此提示符会在读取多行命令的第二行及后续行之前显示。

默认值为`%_>%_`。

`delim1`，字符串

用于在输出时分隔结构化数据字段的字符串（参见 `DATA DEFINITIONS` 节）。默认是`,`（逗号）。此变量无法取消。

`delim2`，字符串

在打印结构化数据时用于分隔数组项的字符串。默认是`,`（逗号）。此变量无法取消。

`pager`，字符串

将输出管道到分页器程序的名称和命令行。当估计的输出行数大于屏幕行数时，在交互模式使用此程序。

默认值继承自环境变量`PAGER`。取消此变量将禁用分页。

`quiet`，布尔值

启动时是否显示欢迎横幅。此变量应设置在启动脚本文件中。

以下变量控制数据库的运行方式：

`cachesize`，数值

设置缓存大小。默认未设置。

`blocksize`，数值

设置块大小。

`open`，字符串

打开模式。允许以下值：

`newdb`

截断数据库或创建一个新数据库。以读写模式打开它。

`wrcreat` 或 `rw`

以读写模式打开数据库。如果不存在则创建它。

`reader` 或 `readonly`

以只读模式打开数据库。如果不存在则产生错误。

`lock`，布尔值

锁定数据库。这是默认值。`mmap`，布尔值

使用内存映射。这是默认值。

## 参见

(1), (3)。

### 报告缺陷

向 <> 报告错误。

## 版权

Copyright 2013 Free Software Foundation

许可 GPLv3+: GNU GPL 版本 3 它是自由软件：你可以自由地更改和分发它。在法律允许范围内不提供任何保证。

***

# GDBUS

## 名称

`gdbus` - 用于 D-Bus 对象的工具

## 语法

`gdbus` introspect [--system | --session | --address*] --dest*bus_name* --object-path*/path/to/object* [--xml] [--recurse] [--only-properties]

`gdbus` monitor [--system | --session | --address*] --dest*bus_name* --object-path*/path/to/object*]

`gdbus` call [--system | --session | --address*] --dest*bus_name* --object-path*/path/to/object* --method*org.project.InterfaceName.MethodName* [--timeout*seconds*] ARG1 ARG2...

`gdbus` emit [--system | --session | --address*] --object-path*/path/to/object* --signal*org.project.InterfaceName.SignalName* [--dest*unique_bus_name*] ARG1 ARG2...

`gdbus` help

## 描述

`gdbus` 是一个用于 D-Bus 对象的简单工具。

## 命令

`introspect`

`monitor`

`call`

`emit`

`help`




`introspect` 打印远程对象的接口和属性值。要使此功能工作，所有者需要实现 `org.freedesktop.DBus.Introspectable` 接口。如果使用了 `--xml` 选项，则打印返回的探测 XML，否则打印解析后的精美表示。`--recurse` 选项可以用于探测子对象（及其子对象等），`--only-properties` 选项可以打印带有属性的接口。

`monitor` 监控 `bus_name` 拥有的一个或所有对象。

`call` 调用远程对象的方法。传递给方法的每个参数都必须指定为序列化的 `GVariant`，但字符串不需要显式引号。返回值将作为序列化的 `GVariant` 值打印出来。

`emit` 发射信号。包含在信号中的每个参数都必须指定为序列化的 `GVariant`，但字符串不需要显式引号。

`help` 显示帮助。

## GDBM

### 命令

`version`

打印 `gdbm` 的版本。

## 数据定义

`define` 语句提供了一种定义键或内容结构的机制。它类似于 `C` 语言的 `struct` 声明：

```text
define key|content { defnlist }
```

`defnlist` 是成员声明的逗号分隔列表。在 `defnlist` 中，换行符失去了作为命令终止符的特殊含义，因此每个声明可以单独出现，并且可以插入任意数量的注释来记录该定义。

每个声明具有以下格式之一：

```text
type name
type name[N]
```

其中 `type` 是数据类型，`name` 是成员名。第二种格式将成员 `name` 定义为由 `N` 个 `type` 元素组成的数组。

支持的类型有：

| 类型 | 含义 |
| --- | --- |
| `char` | 单字节（有符号） |
| `short` | 有符号短整数 |
| `ushort` | 无符号短整数 |
| `int` | 有符号整数 |
| `unsigned` | 无符号整数 |
| `uint` | 同上 |
| `long` | 有符号长整数 |
| `ulong` | 无符号长整数 |
| `llong` | 有符号长长整数 |
| `ullong` | 无符号长长整数 |
| `float` | 浮点数 |
| `double` | 双精度浮点数 |
| `string` | 字符数组（见下文 `NOTE`） |
| `stringz` | 零终止字符字符串 |

在 `defnlist` 中可以使用以下对齐声明：

`offset N`

下一个成员从偏移量 `N` 开始。

`pad N`

在上一个成员后添加 `N` 字节的填充。

例如：

```text
define content { int status, pad 8, char id[3], stringz name }
```

要定义一个由单个数据成员组成的数据，可以使用以下简化的构造：

```text
define key|content type
```

其中 `type` 是上述类型之一。

**NOTE**：只有当 `string` 类型是数据结构的最后一个或唯一成员时，才能合理地使用它。因为没有提供关于数组中元素数量的信息，因此被解释为包含到数据项结束的所有字节。

## 变量

`confirm`，布尔值

在执行某些破坏性操作（如截断现有数据库）之前是否请求确认。默认值为 `true`。

`ps1`，字符串

主提示符字符串。其值可以包含转换规范符，由 `%` 字符后跟另一个字符组成。这些规范符在生成的提示符中的展开方式如下：

```text
序列    扩展
%f      数据库文件名
%p      程序名
%P      包名（gdbm）
%_      水平空格（ASCII 32）
%v      程序版本
%%      %
```

默认提示符为 `%p>%_`。

`ps2`，字符串

次要提示符。关于其值的描述请参见 `ps1`。此提示符会在读取多行命令的第二行及后续行之前显示。

默认值为 `%_>%_`。

`delim1`，字符串

用于在输出时分隔结构化数据字段的字符串（参见 `DATA DEFINITIONS` 节）。默认是 `,`（逗号）。此变量无法取消。

`delim2`，字符串

在打印结构化数据时用于分隔数组项的字符串。默认是 `,`（逗号）。此变量无法取消。

`pager`，字符串

将输出管道到分页器程序的名称和命令行。当估计的输出行数大于屏幕行数时，在交互模式使用此程序。

默认值继承自环境变量 `PAGER`。取消此变量将禁用分页。

`quiet`，布尔值

启动时是否显示欢迎横幅。此变量应设置在启动脚本文件中。

以下变量控制数据库的运行方式：

`cachesize`，数值

设置缓存大小。默认未设置。

`blocksize`，数值

设置块大小。

`open`，字符串

打开模式。允许以下值：

`newdb`

截断数据库或创建一个新数据库。以读写模式打开它。

`wrcreat` 或 `rw`

以读写模式打开数据库。如果不存在则创建它。

`reader` 或 `readonly`

以只读模式打开数据库。如果不存在则产生错误。

`lock`，布尔值

锁定数据库。这是默认值。

`mmap`，布尔值

使用内存映射。这是默认值。

## 参见

`gdbm(1)`、`gdbm(3)`。

### 报告缺陷

向 <> 报告错误。

## 版权

Copyright 2013 Free Software Foundation

许可 GPLv3+：GNU GPL 版本 3。它是自由软件：你可以自由地更改和分发它。在法律允许范围内不提供任何保证。

# GDBUS

## 名称

`gdbus` - 用于 D-Bus 对象的工具

## 语法

```text
gdbus introspect [--system | --session | --address ADDRESS] --dest BUS_NAME --object-path /path/to/object [--xml] [--recurse] [--only-properties]

gdbus monitor [--system | --session | --address ADDRESS] --dest BUS_NAME --object-path /path/to/object

gdbus call [--system | --session | --address ADDRESS] --dest BUS_NAME --object-path /path/to/object --method org.project.InterfaceName.MethodName [--timeout SECONDS] ARG1 ARG2...

gdbus emit [--system | --session | --address ADDRESS] --object-path /path/to/object --signal org.project.InterfaceName.SignalName [--dest UNIQUE_BUS_NAME] ARG1 ARG2...

gdbus help
```

## 描述

`gdbus` 是一个用于 D-Bus 对象的简单工具。

## 命令

### `introspect`

打印远程对象的接口和属性值。要使此功能工作，所有者需要实现 `org.freedesktop.DBus.Introspectable` 接口。如果使用了 `--xml` 选项，则打印返回的探测 XML，否则打印解析后的精美表示。`--recurse` 选项可以用于探测子对象（及其子对象等），`--only-properties` 选项可以只打印带有属性的接口。

### `monitor`

监控 `bus_name` 拥有的一个或所有对象。

### `call`

调用远程对象的方法。传递给方法的每个参数都必须指定为序列化的 `GVariant`，但字符串不需要显式引号。返回值将作为序列化的 `GVariant` 值打印出来。

### `emit`

发射信号。包含在信号中的每个参数都必须指定为序列化的 `GVariant`，但字符串不需要显式引号。

### `help`

显示帮助并退出。

## BASH 填充

`gdbus` 自带一个 Bash 填充脚本，用于完成命令、目的地、总线名称、对象路径以及接口和方法名称。

## 示例

这展示了如何对对象进行自省。注意，每个属性的值都会被显示：

```bash
$ gdbus introspect --system \
    --dest org.freedesktop.NetworkManager \
    --object-path /org/freedesktop/NetworkManager/Devices/0

node /org/freedesktop/NetworkManager/Devices/0 {
  interface org.freedesktop.DBus.Introspectable {
    methods:
      Introspect(out s data);
  };

  interface org.freedesktop.DBus.Properties {
    methods:
      Get(in s interface, in s propname, out v value);
      Set(in s interface, in s propname, in v value);
      GetAll(in s interface, out a{sv} props);
  };

  interface org.freedesktop.NetworkManager.Device.Wired {
    signals:
      PropertiesChanged(a{sv} arg_0);

    properties:
      readonly b Carrier = false;
      readonly u Speed = 0;
      readonly s HwAddress = '00:1D:72:88:BE:97';
  };

  interface org.freedesktop.NetworkManager.Device {
    methods:
      Disconnect();

    signals:
      StateChanged(u arg_0, u arg_1, u arg_2);

    properties:
      readonly u DeviceType = 1;
      readonly b Managed = true;
      readwrite o Ip6Config = '/';
      readwrite o Dhcp4Config = '/';
      readwrite o Ip4Config = '/';
      readonly u State = 2;
      readwrite u Ip4Address = 0;
      readonly u Capabilities = 3;
      readonly s Driver = 'e1000e';
      readwrite s Interface = 'eth0';
      readonly s Udi = '/sys/devices/pci0000:00/0000:00-19.0/net/eth0';
  };
};
```

当想要检查特定进程拥有的所有对象时，`--recurse` 和 `--only-properties` 选项非常有用：

```bash
$ gdbus introspect --system \
    --dest org.freedesktop.UPower \
    --object-path / \
    --recurse \
    --only-properties

node / {
  node /org {
    node /org/freedesktop {
      node /org/freedesktop/UPower {
        interface org.freedesktop.UPower {
          properties:
            readonly b IsDocked = true;
            readonly b LidForceSleep = false;
            readonly b LidIsPresent = false;
            readonly b LidIsClosed = false;
            readonly b OnLowBattery = false;
            readonly b OnBattery = false;
            readonly b CanHibernate = true;
            readonly b CanSuspend = true;
            readonly s DaemonVersion = '0.9.10';
        };

        node /org/freedesktop/UPower/Policy {
        };

        node /org/freedesktop/UPower/Wakeups {
          interface org.freedesktop.UPower.Wakeups {
            properties:
              readonly b HasCapability = true;
          };
        };
      };
    };
  };
};
```

同样，可以使用 `introspect` 命令来学习关于 `Notify` 方法的细节：

```text
[...] interface org.freedesktop.Notifications {
  methods:
    GetServerInformation(
      out s return_name,
      out s return_vendor,
      out s return_version,
      out s return_spec_version
    );

    GetCapabilities(out as return_caps);

    CloseNotification(in u id);

    Notify(
      in s app_name,
      in u id,
      in s icon,
      in s summary,
      in s body,
      in as actions,
      in a{sv} hints,
      in i timeout,
      out u return_id
    );
}; [...]
```

有了这些信息，很容易使用 `call` 命令来显示通知：

```bash
$ gdbus call --session \
    --dest org.freedesktop.Notifications \
    --object-path /org/freedesktop/Notifications \
    --method org.freedesktop.Notifications.Notify \
    my_app_name \
    42 \
    gtk-dialog-info \
    "The Summary" \
    "Here's the body of the notification" \
    [] \
    {} \
    5000

(uint32 12,)
```

监控服务上的所有对象：



```text
$ gdbus monitor --system --dest org.freedesktop.ConsoleKit Monitoring signals from all objects owned by org.freedesktop.ConsoleKit The name org.freedesktop.ConsoleKit is owned by :1.15 /org/freedesktop/ConsoleKit/Session2: org.freedesktop.ConsoleKit.Session.ActiveChanged (false,) /org/freedesktop/ConsoleKit/Seat1: org.freedesktop.ConsoleKit.Seat.ActiveSessionChanged ('',) /org/freedesktop/ConsoleKit/Session2: org.freedesktop.ConsoleKit.Session.ActiveChanged (true,) /org/freedesktop/ConsoleKit/Seat1: org.freedesktop.ConsoleKit.Seat.ActiveSessionChanged ('/org/freedesktop/ConsoleKit/Session2',)
```

## 监控服务上的单个对象

```text
$ gdbus monitor --system --dest org.freedesktop.NetworkManager --object-path /org/freedesktop/NetworkManager/AccessPoint/4141 Monitoring signals on object /org/freedesktop/NetworkManager/AccessPoint/4141 owned by org.freedesktop.NetworkManager The name org.freedesktop.NetworkManager is owned by :1.5 /org/freedesktop/NetworkManager/AccessPoint/4141
```

这些选项在输出私钥之前使用指定的加密算法对私钥进行加密。系统会提示输入密码。如果未指定这些选项，则不使用加密。

`-rand file(s)`

一个包含随机数据的文件或多个文件，用于初始化随机数生成器，或者一个 EGD 套字（见 (3)）。可以使用依赖于系统的字符分隔多个文件。MS-Windows 使用 `;` 作为分隔符，OpenVMS 使用 `,`，其他所有系统使用 `:`。

`-engine id`

指定一个引擎（通过其唯一的 `id` 字符串）将使 `gendsa` 尝试获取指定引擎的功能引用，从而在需要时对其进行初始化。随后，该引擎将设置为所有可用算法的默认引擎。

`paramfile`

此选项指定要使用的 DSA 参数文件。文件中的参数决定了私钥的大小。可以使用 `openssl dsaparam` 命令生成和检查 DSA 参数。

## Notes

DSA 密钥的生成仅仅是些随机数生成，因此比 RSA 密钥的生成快得多。

## 另参

(1), (1), (1), (1)

***

# GENHOSTID

## 名称

`genhostid` - 为当前主机生成并设置主机 ID (`hostid`)

## 语法

`genhostid`

## 描述

`genhostid` 生成随机主机 ID，如果 `/etc/hostid` 不存在，则将其存储在 `/etc/hostid`。

## 另参

(1), (2), (2)

***

# GENISOIMAGE

## 名称

`genisoimage` - 创建带有可选 Rock Ridge 属性的 ISO9660/Joliet/HFS 文件系统

## 语法

`genisoimage` [-options] [-o filename] `pathspec` [`pathspec ...`]

## 描述

`genisoimage` 是一个用于生成 ISO9660/Joliet/HFS 混合文件系统的预制程序。

`genisoimage` 能够生成 `Rock Ridge 交换协议` 指定的 `系统使用共享协议记录 (SUSP)`。这被用于向 Unix 主机进一步描述 ISO9660 文件系统中的文件，并提供如长文件名、UID/GID、POSIX 权限、符号链接以及块和字符设备文件等信息。

如果指定了 Joliet 或 HFS 混合命令行选项，`genisoimage` 将为 Joliet 或 HFS 创建额外的文件系统元数据。否则，`genisoimage` 将生成一个纯 ISO9660 文件系统。

`genisoimage` 可以生成真实的（或共享的）HFS 混合文件系统。当从 Macintosh 访问时，相同的文件视为 HFS 文件；从其他机器访问时则视为 ISO9660 文件。HFS 代表 `Hierarchical File System`（分级文件系统），是 Macintosh 上使用的原生文件系统。

作为替代，`genisoimage` 可以为每个文件生成 `ISO9660 Apple 扩展`。这些扩展在 Macintosh 上访问时为每个文件提供 CREATOR、TYPE 和某些 Finder 标志。见下文的 `HFS MACINTOSH FILE FORMATS` 节。

`genisoimage` 对给定的目录树进行快照，并生成二进制镜像，该镜像在写入块设备时将对应于 ISO9660 和/或 HFS 文件系统。

写入 ISO9660 文件系统的每个文件必须具有 8.3 格式的文件名（最多 8 个字符、点号、最多 3 个字符，全部大写），即使在使用 Rock Ridge 的如此。此文件名用于无法利用 Rock Ridge 扩展的系统（如 MS-DOS），且每个目录中的每个文件名必须与该目录的其他文件名不同。`genisoimage` 通常会尝试通过强制将 Unix 文件名转换为大写并根据需要截断来形成正确的名称，但当截断后的名称不完全唯一时，通常会产生不人意的结果。`genisoimage` 为每个文件名分配权重，如果发现两个其他情况下相同的名称，则将优先级较低的名称重命名为包含一个 3 位数的名称（保证是唯一的）。例如，两个文件 `foo.bar` 和 `foo.bar.~1~` 可能会被渲染为 `FOO.BAR;1` 和 `FOO000.BAR;1`。

当配合各种 HFS 选项使用时，`genisoimage` 将尝试识别存储在多种 Apple/Unix 文件格式中的文件，并复制数据、资源叉以及任何相关的 Finder 信息。关于 `genisoimage` 支持的格式的更多信息，请见下文的 `HFS MACINTOSH FILE FORMATS` 节。

注意 `genisoimage` 设计并不是为了直接与写入器通信。大多数写入器具有随制造商而不同的专有指令集，你需要专门的工具来实际刻录光盘。`wodim` 是此类工具之一。最新版本的 `wodim` 可从 获取。

`pathspec` 是要拷贝到 ISO9660 文件系统的目录树路径。可以指定多个路径，`genisoimage` 将合并所有指定路径组件中找到的文件以形成文件系统镜像。

如果指定了 `-graft-points` 选项，则可以在根目录以外的点上嫁接路径，并以与源文件系统不同的名称将文件或目录嫁接到 CD-ROM 镜像上。用几个例子来说明最为简单。假设本地文件 `../old.lis` 存在，你想包含它。

`../old.lis`

```text
foo/bar=../old.lis
```

将包含 `old.lis`。

```text
foo/bar=../old.lis
```

将 `old.lis` 包含在光盘镜像中。`genisoimage` 将嫁接点在光盘镜像上创建目录。默认情况下，创建的目录权限为 0555，所有者为运行 `genisoimage` 的用户。如果你希望其他权限或所有者，请见 `-uid`、`-gid`、`-dir-mode`、`-file-mode` 和 `-new-dir-mode`。在 Windows 上编译的 `genisoimage` 也可以在 Windows 上运行。因此此手册中大多数对 Unix 的引用可以替换为 *。

### 选项

多个选项可以作为默认指定 `.genisoimagerc` 配置文件，也可以位于命令行。如果在两个地方都指定了参数，则使用命令行的设置。有关此文件的格式和可能的位置，请见 (5)。

`-abstract file`

指定抽象文件名。空间为 37 个字符。等于 `.genisoimagerc` 中的 `ABST`。

`-A application_id`

`-appid application_id`

指定写入卷头的文本字符串。这应该描述将位于光盘上的应用程序。空间为 128 个字符。等于 `.genisoimagerc` 中的 `APPI`。

`-allow-limited-size`

当处理大于 2GiB 且无法在 ISO9660 中轻松表示的文件时，以缩小的可见文件大小添加到 ISO9660，并以正确的可见文件大小添加到 UDF 系统。结果是不一致的文件系统，用户需要确保他们确实使用 UDF 而不是 ISO9660 驱动程序来读取此类磁盘。意味着启用 `-udf`。

`-allow-leading-dots`

`-ldots`

允许 ISO9660 文件名以点开头。通常，领先点会被替换为下划线以保持与 MS-DOS 的兼容性。

`-allow-lowercase`

此选项允许在 ISO9660 文件名中出现小写字母。这违反了 ISO9660 标准，但在某些系统上有效。请谨慎使用。

`-allow-multidot`

此选项允许 ISO9660 文件名中出现多个点。领先点不受此选项影响，它可以单独通过 `-allow-leading-dots` 允许。

这违反了 ISO9660 标准，但在许多系统上恰好有效。请谨慎使用。

### `-biblio file`

指定参考文献文件名。有 37 个字符的空间。等同于 `.genisoimagerc` 文件中的 `BIBL`。

### `-cache-inodes`

### `-no-cache-inodes`

启用或禁用缓存索引节点（inode）和设备号，以查找文件的硬链接。如果 `genisoimage` 发现硬链接（具有多个名称的文件），则该文件在 CD 上也会被硬链接，因此文件内容只会出现一次。这有助于节省空间。在 Unix 类操作系统上，`-cache-inodes` 是默认选项，但在某些其他系统（如 Cygwin）上，`-no-cache-inodes` 是默认选项，因为假设这些系统上的 inode 节点号是唯一的是不安全的。（某些 Cygwin 版本使用弱哈希算法创建伪造 inode 节点号，这可能会产生重复。）如果两个文件的 inode 节点号相同但它们不是指向同一个文件的硬链接，则 `genisoimage -cache-inodes` 的行为将不正确。`-no-cache-inodes` 在所有情况下都是安全的，但在那种情况下 `genisoimage` 无法检测硬链接，因此生成的 CD 镜像可能比需要的大。

### `-alpha-boot alpha_boot_image`

指定在制作 Alpha/SRM 可引导 CD 时使用的引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。

### `-hppa-bootloader hppa_bootloader_image`

指定在制作 HPPA 可引导 CD 时使用的引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。还需要其他选项，至少需要一个内核文件名和一个引导命令行。更多信息请参阅下方的 `HPPA NOTES` 章节。

### `-hppa-cmdline hppa_boot_command_line`

指定在制作可引导 CD 时传递给 HPPA 引导加载程序的命令行。使用空格或逗号分隔参数。必须向 `genisoimage` 传递更多选项，至少需要一个内核文件名和一个引导加载程序文件名。更多信息请参阅下方的 `HPPA NOTES` 章节。

### `-hppa-kernel-32 hppa_kernel_32`

### `-hppa-kernel-64 hppa_kernel_64`

指定在制作 HPPA 可引导 CD 时使用的 32 位和/或 64 位内核镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。还需要其他选项，至少需要引导加载程序文件名和引导命令行。更多信息请参阅下方的 `HPPA NOTES` 章节。

### `-hppa-ramdisk hppa_ramdisk_image`

指定在制作 HPPA 可引导 CD 时使用的内存盘（ramdisk）镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。此参数是可选的。还需要其他选项，至少需要一个内核文件名和一个引导命令行。更多信息请参阅下方的 `HPPA NOTES` 章节。

### `-mips-boot mips_boot_image`

指定在制作 SGI/大端序 MIPS 可引导 CD 时使用的引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。此选项可以指定多次，以存储多达 15 个引导镜像。

### `-mipsel-boot mipsel_boot_image`

指定在制作 DEC/小端序 MIPS 可引导 CD 时使用的引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。

### `-B img_sun4,img_sun4c,img_sun4m,img_sun4d,img_sun4e`

### `-sparc-boot img_sun4,img_sun4c,img_sun4m,img_sun4d,img_sun4e`

指定用于制作 SPARC 系统可引导 CD 的引导镜像列表，并用逗号分隔。分区 0 用于 ISO9660 镜像，第一个镜像文件映射到分区 1。逗号分隔的列表最多可以有 7 个字段，包括空字段。制作 Sun SPARC 的可引导 CD 需要此选项。如果指定了 `-B` 或 `-sparc-boot`，生成的镜像的第一个扇区将包含一个 Sun 磁盘标签。该磁盘标签为 ISO9660 镜像指定分区 0，并为此选项指定的引导镜像指定分区 1 到 7。每个附加引导镜像内的 512 到 8191 字节偏移处必须包含适用于相应 SPARC 架构的主引导程序。镜像的其余部分通常包含用于主内核引导阶段的 UFS 文件系统。

所实现的引导方法是 SunOS 4.x 和 SunOS 5.x 中的方法。然而，它不依赖于 SunOS 内部实现，而仅取决于 Open Boot prom 的属性，因此它适用于任何 SPARC 系统的操作系统。更多信息请参阅下方的 `NOTES` 章节。

如果使用特殊文件名 `...`，实际分区及所有后续引导分区将映射到上一个分区。如果调用 `genisoimage` 时带有 `-G ...`。

### `-G generic_boot_image`

指定在制作引导 CD 时使用的通用引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。此参数是可选的。还需要其他选项，至少需要一个内核文件名和引导命令行。更多信息请参阅下方的 `HPPA NOTES` 章节。

### `-b eltorito_image`

### `-eltorito-boot eltorito_image`

指定在为 x86 PC 制作引导 CD 时使用的引导镜像的路径和文件名。路径名必须相对于为 `genisoimage` 指定的源路径。制作可引导 CD 需要此选项。引导镜像必须恰为 1200 KB、1440 KB 或 2880 KB，`genisoimage` 在创建 ISO9660 文件系统时使用此大小。如果不是 4 的倍数，某些 BIOS 可能会有问题。如果引导镜像不是磁盘，你需要添加 `-hard-disk-boot` 或 `-no-emul-boot`。如果系统不应从模拟磁盘启动，请使用 `-no-boot`。

如果没有指定 `-sort`，引导镜像将以低优先级 (+2) 排在开头。如果你不喜欢这样，需要指定排序权重 0。

### `-eltorito-alt-boot`

使用一组新的 El Torito 引导参数。单个 CD 上可以存储多 63 个 El Torito 引导项。

### `-hard-disk-boot`

指定制作 El Torito 可引导 CD 时使用的引导镜像为硬盘镜像。该镜像必须以包含单个分区的主引导记录（MBR）开头。

### `-no-emul-boot`

指定制作 El Torito 可引导 CD 时使用的引导镜像为“无模拟”镜像。系统将在不进行磁盘模拟的情况下加载并执行此镜像。

### `-no-boot`

指定创建的 El Torito CD 应标记为不可引导。系统将为镜像提供一个模拟驱动器，但从标准引导设备启动。

### `-boot-load-seg segment_address`

指定无模拟 El Torito CD 引导镜像的加载段地址。

### `-boot-load-size load_sectors`

指定在无模拟模式下加载的“虚拟”（512 字节）扇区数量。默认是加载整个引导文件。如果不是 4 的倍数，某些 BIOS 可能会有问题。

### `-boot-info-table`

指定将包含 CD-ROM 布局信息的 56 字节表补丁在引导文件的偏移 8 处。如果给出了此选项，引导文件会在源文件系统中被修改，因此如果该文件无法重新生成，请备份一份！请参阅 `EL TORITO BOOT INFO TABLE` 章节以获取该表的描述。

### `-C last_sess_start,next_sess_start`

### `-cdrecord-params last_sess_start,next_sess_start`



此选项用于创建 CD Extra 或多会话光盘的第二个会话或更高级别的会话镜像。`-C` 需要两个由逗号分隔的数字。第一个数字是光盘上最后一个会话中应追加的内容的第一个扇区。第二个数字是新会话的起始扇区号。可以通过调用 `wodim -msinfo ...` 获取正确的数字。如果 `-C` 与 `-M` 一起使用，`genisoimage` 将创建一个旨在作为上一个会话延续的文件系统镜像。如果在未使用 `-M` 的情况下使用 `-C`，`genisoimage` 将创建一个用于 CD Extra 第二个会话的文件系统镜像。这是一个多会话 CD，第一个会话包含音频数据，第二个会话包含 ISO9660 文件系统。

## `-c` `boot_catalog`

## `-eltorito-catalog` `boot_catalog`

指定引导目录（boot catalog）的路径和文件名，这是 El Torito 可启动光盘所要求的。路径名必须相对于指定 `genisoimage` 的源路径。该文件将被插入到输出树中，而不会在源文件中创建，因此请确保指定的文件名不会与现有文件冲突，否则它将被排除。通常选择类似 `boot.catalog` 的名称。

如果未指定 `-sort`，引导目录将以低优先级 (+1) 排序到介质开头。如果你不喜欢这样，需要为引导目录指定排序权重 0。

## `-check-oldnames`

检查从旧会话（old session）导入的所有文件名是否符合 ISO9660 文件命名规则。如果不使用此选项，则仅检查长度超过 31 个字符的名字，因为这些文件严重违反了 ISO9660 标准。

## `-check-session` `file`

检查所有旧会话是否符合实际的 `genisoimage` ISO9660 文件命名规则。这是一个高级选项，结合了 `-M file`、`-C 0,0` 和 `-check-oldnames`。对于参数 `file`，请参阅 `-M` 的描述。

## `-checksum_algorithm_iso` `alg1,alg2,...`

指定输出镜像所需的校验和类型。

## `-checksum_algorithm_template` `alg1,alg2,...`

指定输出 jigdo 模板所需的校验和类型。

## `-copyright` `file`

指定版权信息，通常是光盘上的文件名。有 37 个字符的空间。等同于 `*.genisoimagerc` 文件中的 `COPY`。

## `-d`

## `-omit-period`

不在没有点号的文件末尾添加点号。这违反了 ISO9660 标准，但在许多系统中确实可以工作。请谨慎使用。

## `-D`

## `-disable-deep-relocation`

不使用深度目录重定位（deep directory relocation），而是按照我们看到的方式对其进行打包。如果没有选择 ISO9660:1999，这违反了 ISO9660 标准，但在许多系统中确实可以工作。请谨慎使用。

## `-debug`

设置调试标记。

## `-dir-mode` `mode`

将用于创建镜像的目录模式覆盖为 `mode`，指定为如 (1) 中的 4 位权限位。此选项会自动启用 Rock Ridge 扩展。

## `-dvd-video`

生成符合 DVD-Video 标准的 UDF 文件系统。这是通过对适当文件的内容进行排序并在文件之间添加填充来实现。请注意，只有当 DVD-Video 文件名仅包含大写字母时，排序才有效。

注意，为了获得符合 DVD-Video 标准的文件系统镜像，你需要准备一个符合 DVD-Video 标准的目录树。这需要在生成的 DVD 根目录下有一个 `VIDEO_TS` 目录（全大写），通常还有另一个 `AUDIO_TS` 目录。`VIDEO_TS` 需要包含符合 DVD-Video 文件系统所需文件（文件名必须全大写）。

## `-e` `efi_boot_file`

## `-efi-boot` `efi_boot_file`

设置 EFI 引导镜像名称。

## `-f`

## `-follow-links`

在生成文件系统时遵循符号链接。当未使用此选项时，如果启用了 Rock Ridge，则将进入符号链接，否则将忽略它们。

## `-file-mode` `mode`

将用于创建镜像的普通文件模式覆盖为 `mode`，指定为如 (1) 中的 4 位权限位。此选项会自动启用 Rock Ridge 扩展。

## `-gid` `gid`

将从源文件读取的组 ID 覆盖为 `gid` 值。指定此选项会自动启用 Rock Ridge 扩展。

## `-gui`

切换为 GUI 行为。目前这使输出更详细，但未来可能会有其他影响。

## `-graft-points`

允许文件名使用嫁接点（graft points）。如果使用此选项，将检查所有文件名的嫁接点。文件名在第一个未转义的等号处分割。如果指定了 `-graft-points`，所有 `\'` 和 `=` 字符都必须使用 `\'` 进行转义。

## `-hide` `glob`

隐藏匹配 `glob`（shell 通配符模式）的任何文件，使其在 ISO9660 或 Rock Ridge 目录中不可见。`glob` 可以匹配文件名或路径的任何部分。如果 `glob` 匹配目录，则该目录的内容将被隐藏。

## `-hide-list` `file`

一个包含要从目录隐藏的 shell 通配符的文件。

## `-hidden` `glob`

为匹配 `glob`（shell 通配符模式）的文件和目录添加 ISO9660 隐藏（existence）属性。此属性将防止文件在 MS-DOS 中显示。参见 `NOTES` 章节。此选项可以使用多次。

## `-hide-joliet` `glob`

在 Joliet 目录中隐藏匹配 `glob`（shell 通配符模式）的文件和目录。`glob` 可以匹配文件名或路径的任何部分。如果 `glob` 匹配目录，则该目录的内容将被隐藏。为了匹配目录名，请确保路径不包含结尾字符。所有隐藏的文件仍将写入输出镜像。此选项通常与 `-hide` 一起使用。参见 `README`。此选项可以使用多次。

## `-hide-joliet-list` `file`

一个包含要从 Joliet 树隐藏的 shell 通配符的文件。参见 `-hide-joliet`。

## `-hide-joliet-trans-tbl`

在 Joliet 树中隐藏 `TRANS.TBL` 文件。这些文件在 Joliet 世界中没有意义，因为它们列出了真实名称和 ISO9660 名称，后者可能与 Joliet 名称不同。

## `-hide-rr-moved`

在 Rock Ridge 树中将 `RR_MOVED` 目录重命名为 `.rr_moved`。似乎无法在 Rock Ridge 树中完全隐藏 `RR_MOVED` 目录。此选项仅让那些不知道该目录用途的人看到的可见树不那么困惑。如果你不需要 `RR_MOVED` 目录，应该使用 `-D`。注意，如果指定了 `-D`，生成的文件系统不符合 ISO9660 第一级，且无法在 MS-DOS 上读取。参见 `NOTES` 章节。

## `-input-charset` `charset`

定义本地文件名使用的字符的输入字符集。要获取有效字符集名称列表，请调用 `genisoimage -input-charset help`。获取一对映射，可以使用 `default` 作为字符集名称。默认初始值在基于 DOS 的系统上为 `cp437`，在所有其他系统上为 `iso8859-1`。更多信息请参见下文的**字符集**章节。

## `-output-charset` `charset`

定义 Rock Ridge 文件名中使用的字符输出字符集。默认为输入字符集。更多信息请参阅下文 `CHARACTER SETS` 章节。

## `-iso-level` *level*

设置 ISO9660 兼容性级别。有效数字为 1 到 4。

使用级别 1 时，文件可能只包含一个分区，且文件名限制为 8.3 字符。

使用级别 2 时，文件可能只包含一个分区。

使用级别 3 时，没有其他限制（`ISO-9660:1988` 除外）。

在从 1 到 3 的所有 ISO9660 级别中，所有文件名都限制为大写字母、数字和下划线（`_`）。文件名限制为 31 个字符，目录嵌套限制为 8 层，路径名限制为 255 个字符。

级别 4 官方上不存在，但 `genisoimage` 将其映射到 `ISO-9660:1999`，即 `ISO9660` 版本 2。

使用级别 4 时，将输出一个版本号和文件结构版本号设置为 2 的增强卷描述符。目录嵌套不再限制为 8 层，文件不需要包含点，且点没有特殊含义，文件名不包含版本号，且文件名长度可达 207 个字符，如果使用 Rock Ridge 则可达 197 个字符。

在创建版本 2 镜像时，`genisoimage` 会输出一个增强卷描述符，它与主卷描述符相似但并不相同。请注意不要使用损坏的软件通过假设存在第二个 PVD 副本并对该假设的 PVD 副本进行补丁到 El Torito VD 来使 ISO9660 镜像可启动。

## `-J`

除了常规的 ISO9660 文件名外，还生成 Joliet 目录记录。这在光盘要在 Windows 机器上使用时尤为有用。Joliet 文件名使用 Unicode 指定，每个路径组件的长度可达 64 个 Unicode 字符。注意 Joliet 并不是标准 --- 只有 Microsoft Windows 和 Linux 系统可以读取 Joliet 扩展。为了更好的移植性，请考虑同时使用 Joliet 和 Rock Ridge 扩展。

## `-joliet-long`

允许 Joliet 文件名长达 103 个 Unicode 字符，而不是 64 个。这破坏了 Joliet 规范，但似乎有效。请谨慎使用。

## `-jcharset` *charset*

`-J -input-charset charset` 的组合。更多信息请参阅下文 `CHARACTER SETS` 章节。

## `-l`

## `-full-iso9660-filenames`

允许使用完整的 31 字符文件名。通常 ISO9660 文件名将采用 8.3 格式，这与 MS-DOS 兼容，尽管 ISO9660 标准允许最多 31 个字符的文件名。如果你使用此选项，该光盘在 MS-DOS 系统上可能难以使用，但在大多数其他系统上可以工作。请谨慎使用。

## `-L`

过时的选项；请用 `-allow-leading-dots` 代替。

## `-jigdo-jigdo` *jigdo_file*

生成文件系统镜像的同时生成一个 jigdo `*.jigdo` 元数据文件。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-template` *template_file*

生成文件系统镜像的同时生成一个 jigdo `*.template` 文件。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-min-file-size` *size*

指定在 `*.jigdo` 文件列表中文件的最小大小。默认（以及允许的最小值）为 1KB。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-force-md5` *path*

指定一个文件模式，其中的文件*必须*包含在 `-md5-list` 提供的外部 MD5 列表中。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-exclude` *path*

指定一个文件模式，其中的文件将不会列在 `*.jigdo` 文件中。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-map` *path*

为 jigdo 文件指定模式映射（例如 `Debian=/mirror/debian`）。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-md5-list` *md5_file*

指定一个包含包含在 `*.jigdo` 文件中的文件的 MD5 和、大小和路径名的文件。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-jigdo-template-compress` *algorithm*

指定用于模板数据的压缩算法。目前支持 `gzip` 和 `bzip2`，其中 `gzip` 是默认值。更多信息请参阅下文 `JIGDO NOTES` 章节。

## `-log-file` *log_file*

将所有错误、警告和信息性消息重定向到 `log_file` 而不是标准错误输出。

## `-m` *glob*

排除匹配 `glob`（一种 shell 通配符模式）的文件不写入 CD-ROM。`glob` 可以匹配文件名部分，也可以匹配完整路径。此选项可以多次使用。例如：

```
genisoimage -o rom -m '*.o' -m core -m foobar
```

这将从镜像中排除所有以 `.o` 结尾、或名为 `core` 或 `foobar` 的文件。注意，如果你有一个名为 `foobar` 的目录，它（以及所有后代目录）也会被排除。

## `-exclude-list` *file*

一个包含要排除的 shell 通配符列表的文件。参见 `-m`。

## `-max-iso9660-filenames`

允许 ISO9660 文件名长达 37 个字符。此选项启用 `-N`，因为额外的空间是从版本号中留出的。

这违反了 ISO9660 标准，但在许多系统中是有效的。使用此选项可能会导致读取系统的缓冲区溢出。请极其小心。

## `-M` *path*

## `-M` *device*

## `-dev` *device*

指定要合并的现有 ISO9660 镜像。另一种形式是设备指定符，其格式与 `wodim` 的 `dev=` 参数相同。`genisoimage` 的输出将是 `-M` 指定的新会话。这通常需要刻录机支持多会话。此选项可以与 `-C` 结合使用。

## `-N`

## `-omit-version-number`

在 ISO9660 文件名中省略版本号。

这违反了 ISO9660 标准，但实际上没人使用版本号。请谨慎使用。

## `-new-dir-mode` *mode*

指定在文件系统镜像中创建新目录时使用的模式（四位数，如 1）。默认为 0555。

## `-nobak`

## `-no-bak`

排除 ISO9660 文件系统上的备份文件；即包含 `~` 或 `#` 或以 `*.bak` 结尾的文件。这些通常是 Unix 编辑器的备份文件。

## `-force-rr`

不对之前的会话使用自动 Rock Ridge 属性识别。这可以解决 NERO Burning ROM 等产生的问题。

## `-no-rr`

不要使用之前会话的 Rock Ridge 属性。这有助于避免 `genisoimage` 在旧会话中发现非法 Rock Ridge 签名。

在整个镜像的末尾填充 150 个扇区（300 kB）。此选项默认启用。如果与 `-B` 结合使用，将在 ISO9660 分区和启动分区之间插入填充，使得第一个启动分区从 16 的倍数扇区编号开始起始。

这种填充是必要的，因为许多操作系统（例如 Linux）在它们的文件系统 I/O 中实现了预读 Bug。这些 Bug 会导致对位于轨道末尾的文件产生读取错误，特别是当磁盘以“一次性轨道”（Track At Once）模式写入时，或者 CD 音频轨道紧随数据轨道之后。

不要在末尾填充 150 个扇区（300 kB），也不要让启动分区起始于 16 个扇区的倍数上。

`file`

一个包含 `pathspec` 目录和文件名列表的文件，用于将这些内容添加到 ISO9660 文件系统中。该 pathspecs 列表将在命令行中出现的任何其他 pathspec 之后进行处理。如果参数为 `--`，则从标准输入读取列表。

过时的选项；请改用 `-publisher`。

`publisher_id`

指定一个将写入卷标头的文本字符串。这应该描述 CD-ROM 的发行者，通常包含邮寄地址和电话号码。空间足够容纳 128 个字符。等同于 `.genisoimagerc` 文件中的 `PUBL`。

`preparer_id`

指定一个将写入卷标头的文本字符串。这应该描述 CD-ROM 的制备者，通常包含邮寄地址和电话号码。空间足够容纳 128 个字符。等同于 `.genisoimagerc` 文件中的 `PREP`。

以扇区大小（2048 字节）的倍数估计文件系统大小并退出。此选项在“一次性磁盘”（Disk At Once）模式以及配合某些 CD-R 驱动器直接管道传输到 `wodim` 时是必要的，在这种情况下 `wodim` 需要提前知道文件系统镜像的大小。旧版本的 `mkisofs` 将此信息（以及其他信息）写入 `stderr`。由于这被证明很难解析，现在不带任何其他信息的数字也会打印到 `stdout` 上。如果你想写一个简单的 shell 脚本，可以重定向 `stderr` 并从 `stdout` 获取该数字。可以通过以下方式实现：

```
cdblocks=`genisoimage -print-size -quiet ...`
genisoimage ... | wodim ... tsize=${cdblocks}s -
```

这使得 `genisoimage` 更加简洁。将不会提供进度输出。

## `-R`

## `-rock`

使用 Rock Ridge 协议生成 SUSP 和 RR 记录，以进一步描述 ISO9660 文件系统上的文件。

## `-r`

## `-rational-rock`



此类似于`-R`选项，但文件所有和模式被设置为更有用的值。`uid`和`gid`被设置为`0`，因为它们通常只对作者的系统有用，对客户端没用。所有文件的读取位都设置为真，以便文件和目录在客户端上全局可读。如果某个文件设置了任何执行位，则设置所有执行位，以便可执行文件在客户端上全局可执行。如果目录设置了任何搜索位，则设置所有搜索位，以便目录在客户端上全局可搜索。所有写入位都被清除，因为文件系统在任何情况下都会以只读模式挂载。如果设置了任何特殊模式位，则将其清除，因为文件锁在只读文件系统上没有用，且`uid 0`或`gid 0`不希望set-id位。在`Win32`上使用时，所有文件都会设置执行位。这是由于`Win32`缺少文件权限以及`Cygwin POSIX`仿真层导致的。参见`-uid`, `-gid`, `-dir-mode`, `-file-mode`和`-new-dir-mode`。

允许`ISO9660`文件名包含除小写字母以外的所有`7`位`ASCII`字符。

这违反了`ISO9660`标准，但在许多系统中恰好有效。请谨慎使用。

`dir`

将镜像中的所有文件和目录移动到`dir`中。这本质上与使用`-graft-points`并在每个pathspec前添加`dir`，但更容易使用。`dir`实际上可以是几层深。它与其他挂载点具有相同的权限。

`dir`

当写入多会话镜像且之前的（甚至更早的）会话是使用`-root dir`写入时，此选项是必要的。使用之前的会话中未找到的目录名会导致`genisoimage`报错并终止。如果没有此选项，`genisoimage`将无法找到未修改的文件，并将被迫再次将它们的数据写入镜像。`-root`和`-old-root`旨在配合使用以进行增量备份。初始会话例如使用：`genisoimage -root backup_1 dirs`。下次使用`genisoimage -root backup_1 dirs -old-root backup_1`进行增量备份将允许增量备份。生成的输出镜像将命名为：`backup_00`，`backup_01`，`backup_02`....

`sector type`

`sector type`

`-s`

`sectype`

将输出类型设置为`xa1`。

`sort_file`

排序`ISO9660`中文件名的顺序。它排序数据写入`CD`的顺序，这对于优化`CD`上的数据布局有用。更多细节参见`README.sort`。

`img_sun4,img_sun4c,img_sun4m,img_sun4d,img_sun4e`

见上述`-B`。

`label`

为使用`-sparc-boot`创建的`Sun`标签设置Sun标签名称。

将输出镜像拆分为若干个约`1 GB`文件。这有助于在不支持大文件的操作系统上创建`DVD`尺寸的`ISO9660`镜像。在写入`DVD`时，`wodim`将多个文件合并到一个轨道。为了使`-split-output`起作用，必须指定`-o` `filename`。生成的输出镜像将命名为：`filename_00`，`filename_01`，`filename_02`....

`#`

选择流操作并将大小设置为`#`个扇区。这允许你将（1）程序的输出管道到`genisoimage`，并在不需要中间存档的情况下创建`ISO9660`文件系统。如果指定了此选项，`genisoimage`从`stdin`读取并创建一个名为`STREAM.IMG`的文件。文件的大小（包含填充）比指定的大小小`200`个扇区。如果指定了`-no-pad`，文件大小比指定的大小小`50`个扇区。如果文件较小，`genisoimage`将写入填充。这可能需要一段时间。

选项`-stream-media-size`仅创建简单的`ISO9660`文件系统，且不能与多会话或混合文件系统选项一起使用。

`name`

留供未来使用。

# `-sunx86-boot` `UFS_img,,,AUX1_img`

指定一个逗号分隔的文件系统镜像列表，用于为`Solaris x86`系统制作可引导的`CD`。

请注意，分区`1`用于`ISO9660`镜像，分区`2`是整个磁盘，因此分区`1`和`2`可能无法被外部分区数据使用。第一个镜像文件映射到分区`0`。逗号分隔列表中可能存在空字段，且分区`1`和`2`的列表项必须为空。支持的分区最大数量为`8`（尽管`Solaris x86`分区表支持多达`16`个分区），因此无法指定超过`6`个分区镜像。这是为`Solaris x86`系统制作可引导`CD`所必需的选项。

如果指定了`-sunx86-boot`，生成的镜像第一个扇区将包含一个`PC fdisk`标签，其中包含一个`Solaris`类型`0x82`fdisk分区，它从偏移`512`开始并跨整个`CD`。此外，对于`Solaris`类型`0x82`fdisk分区，在`CD`第一个扇区的偏移`1024`处有一个`SVr4`磁盘标签。该磁盘标签指定用于引导`PC`的第一个（通常是`UFS`类型）文件系统镜像使用slice`0`，为`ISO9660`镜像使用slice`1`。slice`2`跨越整个`CD`，slice`3`...slice`7`可用于通过此选项指定的其他文件系统镜像。

`Solaris x86`引导`CD`使用一个`1024`字节大小的主引导，该引导使用`El-Torito` no-emulation引导模式，以及一个位于`CD`扇区`1..15`的次级通用引导。由于原因，必须指定`-b` `bootimage` `-no-emul-boot`和`-G` `genboot`。

# `-sunx86-label` `label`

为使用`-sunx86-boot`创建的`SVr4`磁盘标签设置`SVr4`磁盘标签名称。

# `-sysid` `ID`

指定系统`ID`。有`32`个字符的空间。等同于`.genisoimagerc`文件中的`SYSI`。

# `-T`

# `-translation-table`

在`CD-ROM`上的每个目录中生成文件`TRANS.TBL`，该文件用于不支持`Rock Ridge`的系统以帮助建立正确的文件。文件中还包含指示块设备和字符设备的主号和次号的信息，并且每个符号链接都有给定的链接文件名为。

# `-table-name` `table_name`

备用翻译表文件名（见上文）。隐含`-T`。如果你正在创建多会话镜像，必须使用与上一个会话相同的名称。

# `-ucs-level` `level`

在`Joliet SVD`中设置`Unicode`兼容性级别。默认级别为`3`。可以使用此选项将其设置为`1..3`。

# `-udf`

在生成的文件系统镜像中包含`UDF`文件系统支持。`UDF`支持目前处于alpha（测试）阶段，因此无法创建仅包含`UDF`的镜像。`UDF`数据结构目前与`Joliet`结构耦合，因此当前的实现中存在许多陷阱。没有`UID/GID`支持，没有`POSIX`权限支持，不支持符号链接。请注意，`UDF`除了实际`UDF`数据结构所需的空间外，还浪费了磁盘开头从扇区`~20`到扇区`256`的空间。

# `-uid` `uid`

将从源文件读取的`uid`覆盖为`uid`值。指定此选项会自动启用`Rock Ridge`扩展。

# `-use-fileversion`

选项`-use-fileversion`允许`genisoimage`使用文件系统中的版本号。如果未指定该选项，`genisoimage`为所有文件创建版本号`1`。文件版本是`;1`到`;32767`范围内的字符串。该选项在`VMS`上是默认的。

# `-U`

# `-untranslated-filenames`

允许“未翻译”的文件名，完全违反上述的`ISO9660`标准。启用以下标志：`-d`，`-l`，`-N`，`-allow-leading-dots`，`-relaxed-filenames`，`-allow-lowercase`，`-allow-multidot`，`-no-iso-translate`。允许文件名中出现多个`.`字符，以及混合大小写的文件名。这在`HP-UX`上很有用，因为内置的`cdfs`文件系统不识别任何扩展。请极其谨慎使用。

# `-no-iso-translate`

不要翻译对于`ISO9660`文件名无效的字符`#`和`~`。虽然无效，但这些字符经常被微软系统使用。

这违反了`ISO9660`标准，但在许多系统上可行。请谨慎使用。

# `-V` `volid`

指定写入主块的卷`ID`（卷名或标签）。有`32`个字符的空间。等同于`.genisoimagerc`文件中的`VOLI`。卷`ID`被`Solaris`卷管理器用作挂载点，并作为分配给`Windows`和`Apple Mac OS`等其他各种平台上磁盘的标签。

# `-volset` `ID`

指定卷集`ID`。有`128`个字符的空间。等同于`.genisoimagerc`文件中的`VOLS`。

# `-volset-size` `#`

将卷集大小设置为`#`。卷集大小是卷中`CD`的数量。`genisoimage`目前不支持大于`1`的`-volset-size`。

选项`-volset-size`必须在每行命令行中位于`-volset-seqno`之前。

# `-volset-seqno` `#`

将卷集序列设置为`#`。卷集序列号是当前`CD`在卷集中的索引数字。选项`-volset-size`必须在每行命令行中位于`-volset-seqno`之前。

# `-v`

# `-verbose`

详细执行。如果在命令行中给出两次，将打印额外的调试信息。

# `-x` `glob`

相同于`-m` `glob`。

# `-XA`

生成`XA`属性。

# `-xa`

生成合理化的`XA`属性。

# `-z`

# `-transparent-compression`

为透明压缩文件生成特殊的`RRIP`记录。这对于支持透明解压的主机，例如`Linux 2.4.14`或更高版本。你必须指定`-R`或`-r`来启用`Rock Ridge`，并在运行`genisoimage`之前使用`mkzftree`工具生成压缩文件。注意透明压缩是非标准的`Rock Ridge`扩展。生成的磁盘仅在`Linux`上可以透明读取。在其他操作系统上，你将需要调用`mkzftree`来解压文件。

## HFS 选项

# `-hfs`

创建一个`ISO9660/HFS`混合`CD`。此选项应结合`-map`、`-magic`和/或下文提供的各种双杠选项使用。

# `-apple`

创建一个带有`Apple`扩展的`ISO9660`CD。与`-hfs`类似，只是添加了`Apple ISO9660`扩展而不是创建`HFS`混合卷。`genisoimage`版本在指定`-apple`时默认包含`Rock Ridge`属性。此版本的`genisoimage`不再这样做。如果你想要`Rock Ridge`属性，你需要单独指定。

# `-map` `mapping_file`

使用`mapping_file`根据文件名的扩展名为文件设置`CREATOR`和`TYPE`信息。只有当文件名不是已知的`Apple/Unix`文件格式时，才会进行映射。见下文**HFS CREATOR/TYPE**章节。

# `-magic` `magic_file`

`CREATOR`和`TYPE`信息是通过使用文件的`magic number`（通常是文件的前几个字节）设置的。`magic_file`仅当文件不是已知`Apple/Unix`文件格式之一，或者文件扩展名未通过`-map`映射时才使用。详情请参见下方的`HFS CREATOR/TYPE`章节。

### `-hfs-creator` `creator`

为所有文件设置默认`CREATOR`。必须恰好为`4`个字符。详情请参见下方的`HFS CREATOR/TYPE`章节。

### `-hfs-type` `type`

为所有文件设置默认`TYPE`。必须恰好为`4`个字符。详情请参见下方的`HFS CREATOR/TYPE`章节。

### `-probe`

搜索文件内容以查找所有已`Apple/Unix`文件格式。关于这些格式的更多信息，请参见下方的`HFS MACINTOSH FILE FORMATS`。然而，检查`MacBinary`和`AppleSingle`文件的唯一方法是打开并读取它们，因此此选项可能会增加处理时间。如果已知使用的`Apple/Unix`格式，最好使用下面给出的一个或多个`double dash`。

### `-no-desktop`

不创建（空的）`Desktop`文件。在`Macintosh`上使用`CD`时，将创建新的`HFS Desktop`文件（并存储在系统文件夹中）。默认情况下，空的`Desktop`文件会被添加到`HFS`卷中。

### `-mac-name`

使用`HFS`文件名作为`ISO9660`、`Joliet`和`Rock Ridge`文件名的起始点。更多信息请参见下方的`HFS MACINTOSH FILENAMES`章节。

### `-boot-hfs-file` `driver_file`

安装`driver_file`，该文件`may`使`CD`在`Macintosh`上可启动。详情请参见下方的`HFS BOOT DRIVER`章节。（Alpha）。

### `-part`

生成`HFS`分区表。默认情况下不生成分区表，但某些旧的`Macintosh CD-ROM`驱动程序需要`CD-ROM`上有`HFS`分区才能混合`CD-ROM`。

### `-auto` `AutoStart_file`

使`HFS`CD使用`QuickTime 2.0 Autostart`功能来启动应用程序或文档。给定的文件名必须是位于`CD`顶目录的文档或应用程序。文件名必须少于`12`个字符。（Alpha）。

### `-cluster-size` `size`

设置`PC Exchange`文件簇或分配单元的字节大小。这隐含了`--exchange`。详情请参见下方的`HFS MACINTOSH FILE FORMATS`章节。

### `-hide-hfs` `glob`

从`HFS`卷中隐藏`glob`（这是一个shell通配符模式）。该文件或目录仍存在于`ISO9660`和/或`Joliet`目录中。`glob`可以匹配文件名的任何部分。可以排除多个globs。示例：

```
genisoimage -o rom -hfs -hide-hfs '*.o' --hide-hfs foobar
```

这将从`HFS`卷中排除所有以`.o`结尾或名为`foobar`的文件。注意，如果你有一个名为`foobar`的目录，它（以及所有的后代目录）也会被排除。`glob`也可以相对于命令行指定的源目录的路径名。示例：

```
genisoimage -o rom -hfs -hide-hfs src/html src
```

这将仅从`src`目录中排除名为`html`的文件或目录。树中任何其他名为`html`的文件或目录都不会排除。应与`-hide`和/或`-hide-joliet`使用。为了匹配目录名，请确保模式不包含末尾字符`/`。详情请参见`README.hide`。

### `-hide-hfs-list` `file`

指定一个包含通配符模式列表的文件，隐藏方式与`-hide-hfs`相同。

### `-hfs-volid` `hfs_volid`

`HFS`分区的卷名。这是分配给`Macintosh`上磁盘的名称，并替换了与`-V`使用的`volid`。

### `-icon-position`

如果`Apple/Unix`文件存在图标位置信息，则使用它。图标将出现在与在`Macintosh`桌面上相同的位置。屏幕上的文件夹位置和大小、滚动位置、文件夹视图（以图标显示、小图标显示等）也会被保留。（Alpha）。

### `-root-info` `file`

设置`HFS`卷根目录的`Location`、屏幕上大小、滚动位置、文件夹视图等。更多信息请参见`README.rootinfo`。（Alpha）。

### `-prep-boot` `file`

`PReP`启动镜像文件。允许最多`4`个。详情请参见`README.prep_boot`。（Alpha）。

### `-chrp-boot`

添加`CHRP`启动头。

### `-input-hfs-charset` `charset`

当配合`-mac-name`使用，定义`HFS`文件名中使用字符的输入字符集。默认字符集为`cp10000`（`Mac Roman`）。详情请参见下方的`CHARACTER SETS`和`HFS MACINTOSH FILENAMES`章节。

### `-output-hfs-charset` `charset`

当配合`-mac-name`使用，定义`HFS`文件名中使用字符的输出字符集。默认字符集为`cp10000`（`Mac Roman`）。详情请参见下方的`CHARACTER SETS`和`HFS MACINTOSH FILENAMES`章节。

### `-hfs-unlock`

默认情况下，`genisoimage`将创建锁定的`HFS`。

### `-hfs-bless` `folder_name`

“Bless”（加持）给定的`folder_name`。

### `-hfs-parms` `parameters`

覆盖用于`HFS`的某些参数。详情请参见`libhfs_iso`。

## CHARACTER SETS



`genisoimage`以符合 POSIX 标准的方式以 8 位字符字符串的形式处理文件名。为了表示所有语言的所有编码，8 位字符是不够的。Unicode 或 ISO-10646 定义了至少需要 21 位来表示所有语言的字符编码。它们可以用 `UTF-32`、`UTF-16` 或 `UTF-8` 编码来表示。

现代 Unix 操作系统对文件名使用 UTF-8 编码。每个 32 位字符由一个或多个 8 位字符表示。如果一个字符使用 `ISO-8859-1` 编码（用于中欧和北美），则它将 1:1 映射到 `UTF-32` 或 `UTF-16` 编码的 Unicode 字符。如果一个字符使用 `7-Bit ASCII` 编码（用于美国和其他字符集有限的国家），则它将 1:1 映射到 `UTF-32`、`UTF-16` 或 `UTF-8` 编码的 Unicode 字符。无法在 UTF-8 中用单字节表示的字符码（如果值 > 0x7F）使用映射到多个 8 位字符的转义序列。

如果所有操作系统都使用 UTF-8，`genisoimage` 就不需要重新编码文件名中的字符。遗憾的是，Apple 使用完全非标准的编码，而微软使用与 POSIX 文件名接口不兼容的 Unicode 编码。

对于所有非 UTF-8 编码的操作系统，每个字节代表的实际字符取决于本地操作系统使用的 `character set`（字符集）或 `codepage`（微软使用的术语）——字符集中的字符将反映用户设置的区域或自然语言。

通常，字符代码 `0x00-0x1f` 是控制字符，代码 `0x20-0x7f` 是 7 位 ASCII 字符（在 PC 和 Mac 上），`0x80-0xff` 用于其他字符。

由于使用的字符/符号远多于 256 个，字符集中仅由一小部分子集来表示。因此，相同的字符代码在不同的字符集中可能代表不同的字符。例如，在中欧生成的文件名，在（例如）东欧的机器上查看时，可能不会显示相同的字符。

让情况变得复杂的是，不同的操作系统对不同的区域或语言使用不同的字符集。例如，`ĂŠ`（带锐音符号的小写 e）的字符代码在 PC 上可能是代码 `0x82`，在 Macintosh 上是代码 `0x8e`，在西欧的 Unix 系统上是代码 `0xe9`，在 Unicode 中是代码 `0x000e9`。

只要不是所有的操作系统和应用程序使用相同的字符集作为文件名的基础，就有可能指定你的文件名使用什么字符集，以及文件名在 CD 上应该显示什么字符集。

有四个选项可以指定你想使用的字符集：

### `-input-charset`

定义你在主机机器上使用的本地字符集。任何发生的字符集转换将使用此字符集作为起点。默认输入字符集在基于 MS-DOS 的系统上为 `cp437`，在所有其他系统上为 `iso8859-1`。如果给出 `-J`，则 Joliet 目录将使用输入字符集的 Unicode 等效字符。`-jcharset` 与 `-input-charset -J` 相同。

### `-output-charset`

定义在 CD 上用于 Rock Ridge 名称将使用的字符集。默认使用输入字符集。

### `-input-hfs-charset`

定义用于从任何各种 Apple/Unix 文件格式解码出的 HFS 文件名中的 HFS 字符集。仅在配合 `-mac-name` 使用时有用。更多信息请参阅 `HFS MACINTOSH FILENAMES`。默认值为 `cp10000` (Mac Roman)。

### `-output-hfs-charset`

定义从当前使用的输入字符集创建 HFS 文件名时使用的 HFS 字符集。在大多数情况下，这将来自 `-input-charset` 提供的字符集。默认使用输入 HFS 字符集。

`genisoimage` 内置了许多字符集。要获取列表，请使用 `-input-charset help`。如果 `genisoimage` 编译时支持 `iconv`，则此列表将不包含从当前 locale 派生的字符集。

可以通过提供文件名作为任何字符集选项的参数，从文件中读取额外的字符集。只有当给定的文件名与内置字符集不匹配时，才会读取该文件。

字符集文件的格式与 . 提供的映射文件相同。该格式为：

第 1 列是输入字节代码（十六进制格式为 `0xXX`）

第 2 列是 Unicode（十六进制格式为 `0xXXXX`）

该行的其余部分将被忽略。

任何空行、符合上述格式但缺少两（或更多）列的行或注释行（以 `#` 字符开头）均会被忽略且无警告。任何缺失的输入代码映射到 Unicode 字符 `0x0000`。

注意，虽然支持 UTF-8，但不支持 UCS-2/UTF-16 和 UCS-4/UTF-32 等其他 Unicode 编码，因为 POSIX 操作系统无法原生处理它们。

可以使用关键字 `default` 作为任何字符集选项的参数定义 1:1 的字符集映射。这是旧版本 `mkisofs` 的行为。

从输入文件名生成的 ISO9660 文件名不会从输入字符集转换。ISO9660 字符集是 ASCII 字符的一个非常有限的子集，因此任何转换都没有意义。

`genisoimage` 无法转换的字符将被替换为字符 `_`。

## HFS CREATOR/TYPE

Mac 文件有两个与之相关的属性，定义了哪个应用程序创建了文件（`CREATOR`）以及文件包含什么数据（`TYPE`）。两者都是（恰好）4 个字母字符串。通常这允许 Macintosh 用户双击文件并启动正确的应用程序等。可以在 Macintosh 上使用类似 ResEdit（或类似工具）找到特定文件的 `CREATOR` 和 `TYPE`。

`CREATOR` 和 `TYPE` 信息存储在所有各种 Apple/Unix 编码文件中。对于其他文件，可以使用 `mapping` 文件（通过 `-map`）和/或使用文件的 `magic number`（通常是前几个字节中的 `signature`，通过 `-magic`）基于文件扩展名来确定 `CREATOR` 和 `TYPE`。如果同时给出这两个选项，它们在命令行上的顺序是重要的。如果先给出 `-map`，则会在尝试魔数匹配之前尝试文件名扩展名匹配。然而，如果先给出 `-magic`，则会在尝试文件名扩展名匹配之前尝试魔数匹配。

如果不使用映射文件或魔数文件，文件的默认 `CREATOR` 和 `TYPE` 可以通过 `-hfs-creator` 和/或 `-hfs-type` 设置，否则可能为 `????`。

`mapping` 文件的格式与 `afp` 使用的相同。该文件有五列：`extension`、`translation`、`CREATOR`、`TYPE` 和 `Comment`。以 `#` 开头的行会被忽略。示例文件如下：

```
| # Example file  |
|  |
| # EXTN | XLate | CREATOR | TYPE | Comment  |
| .tif | Raw | 8BIM | TIFF | Photoshop image  |
| .hqx | Ascii | BnHq | TEXT | BinHex file  |
| .doc | Raw | MSWD | WDBN | Word file  |
| .mov | Raw | TVOD | MooV | QuickTime Movie  |
| * | Ascii | ttxt | TEXT |
```

第一列 `EXTN` 定义了要映射的 Unix 文件名扩展名。`XLate` 列定义了 Unix 和 Macintosh 文件之间的文本转换，`genisoimage` 会忽略它，但为了兼容 `auf` 需要保留。`CREATOR` 和 `TYPE` 关键字必须是 4 个字符并用单引号括起来。注释字段用双引号括——`genisoimage` 会忽略它，但为了兼容 `aufs`。

`magic` 文件的格式与 `file` 命令使用的 `magic` 文件几乎相同。此文件有四个制表符分隔的列，分别是 `byte offset`、`type`、`test` 和 `message`。以 `#` 字符开头的行是注释行并会被忽略。示例文件如下：

```
| # Example magic file  |
|  |
| # off | type | test | message  |
| 0 | string | GIF8 | 8BIM GIF image  |
| 0 | beshort | 0xffd8 | 8BIM JPEG image data  |
| 0 | string | SIT! | SIT! StuffIt Archive  |
| 0 | string | \037\235 | LZIV ZIVU standard Unix compress  |
| 0 | string | \037\213 | GNUz ZIVU gzip compressed data  |
| 0 | string | %! | ASPS TEXT Postscript  |
| 0 | string | \004%! | ASPS TEXT PC Postscript with a ^D to start  |
| 4 | string | moov | txtt MooV QuickTime movie file (moov)  |
| 4 | string | mdat | txtt MooV QuickTime movie file (mdat)  |
```

文件的格式在 `magic`(5) 中描述。这里唯一的区别是，对于魔法文件中的每个条目，初始偏移的 `message` 必须是 4 个字符的 `CREATOR`，后跟 4 个字符的 `TYPE` --- 它们之间的空格可选。该行上的任何其他字符都会被忽略。续接行（以 `>` 开头）也会被忽略，即：只使用初始偏移行。

使用 `-magic` 可能会显著增加处理时间，因为每个文件都必须打开并读取以找到其魔数（magic number）。

总结，对于所有文件，默认的 `CREATOR` 为 `Unix`，默认的 `TYPE` 为 `TEXT`。可以通过使用 `.genisoimagerc` 文件中的条目，或使用 `-hfs-creator` 和/或 `-hfs-type` 来更改它们。

如果文件属于已知的 Apple/Unix 格式之一（并且已选择该格式），则 `CREATOR` 和 `TYPE` 取自存储在 Apple/Unix 文件中的值。

其他文件可以通过文件名扩展名（使用 `-map`）设置其 `CREATOR` 和 `TYPE`，或者通过其魔数（使用 `-magic`）设置。如果在 `mapping` 文件中使用了默认匹配，这些值将覆盖默认的 `CREATOR` 和 `TYPE`。

可以在 `ftp://ftp.apple.com/` 找到完整的 `CREATOR/TYPE` 数据库。

## HFS MACINTOSH 文件格式

Macintosh 文件有两个部分，称为 `Data`（数据）分叉和 `Resource`（资源）分叉。任何一个部分都可以为空。Unix（以及许多其他操作系统）只能处理只有一个部分（或分叉）的文件。此外，Macintosh 文件具有若干与之相关的属性 --- 最重要的可能是 `TYPE` 和 `CREATOR`。同样，Unix 没有这些类型属性的概念。

例如，一个 Macintosh 文件可能是一个 JPEG 图像，其中图像存储在 `Data` 分叉中，而桌面缩略图存储在 `Resource` 分叉中。通常数据分叉中的信息在跨平台使用时是有用的。

因此，要在 Unix 文件系统上存储 Macintosh 文件，就必须找到一种方法来处理这两个分叉和额外的属性（称为 `Finder info`）。遗憾的是，似乎每个在 Unix 上存储 Macintosh 文件的软件包都选择了完全不同的存储方法。

`genisoimage`（部分）支持的 Apple/Unix 格式包括：

### CAP AUFS 格式

数据分叉存储在一个文件中。资源分叉存储在子目录 `.resource` 中，与数据分叉相同。Finder info 存储在子目录 `.finderinfo` 中，文件名相同。

### AppleDouble/Netatalk

数据分叉存储在一个文件中。资源分叉存储在以 `%` 为前缀的相同文件中。Finder info 也存储在同一个 `%` 文件中。Netatalk 使用相同的格式，但资源分叉/Finder info 存储在子目录 `.AppleDouble` 中，与数据分叉相同。

### AppleSingle

数据结构类似于上述，但两个分叉和 Finder info 都存储在一个文件中。

### Helios EtherShare

数据分叉存储在一个文件中。资源分叉和 Finder info 共同存储在子目录 `.rsrc` 中，与数据分叉相同。

### IPT UShare

类似于 EtherShare 格式，但 Finder info 的存储方式略有不同。

### MacBinary

两个分叉和 Finder info 都存储在一个文件中。

### Apple PC Exchange

Macintosh 用于在 DOS (FAT) 磁盘上存储 Apple 文件。数据分叉存储在一个文件中。资源分叉存储在子目录 `resource.frk` (或 `RESOURCE.FRK`) 中。Finder info 作为文件 `finder.dat` (或 `FINDER.DAT`) 中的一条记录。每个数据分叉目录对应独立的 `finder.dat`。

注意：`genisoimage` 需要知道 PC Exchange 文件所在（或拷贝自）磁盘的本地 FAT 簇大小。此大小由 `-cluster-size` 给出。簇或分配大小可以通过使用 DOS 工具 `chkdsk` 找到。

可能无法配合 PC Exchange v2.2 或更高版本的文件（MacOS 8.1 可用）。使用 Linux 时，包含 PC Exchange 文件的 DOS 介质应挂载为类型 `msdos`（而不是 `vfat`）。

### SGI/XINET

SGI 机器在挂载 HFS 磁盘时使用。数据分叉存储在一个文件中。资源分叉存储在子目录 `.HSResource` 中，文件名相同。Finder info 作为文件 `.HSancillary` 中的一条记录。每个数据分叉目录对应的 `.HSancillary`。

### Thursby Software Systems DAVE

允许 Macintosh 在 SMB 服务器上存储 Apple 文件。数据分叉存储在一个文件中。资源分叉存储在子目录 `resource.frk` 中。使用 AppleDouble 格式存储资源分叉。

### Services for Macintosh

NT 服务器在 NTFS 文件系统上存储的文件格式。数据分叉存储为 `filename`。资源分叉存储为名为 `filename:AFP_Resource` 的 NTFS 流。Finder info 存储为名为 `filename:Afp_AfpInfo` 的 NTFS 流。NTFS 流通常对用户不可见。

警告：`genisoimage` 部分支持 SFM 格式。如果存储在 NT 服务器上的 HFS 文件或文件夹名称中包含非法的 NT 字符，NT 会将这些字符转换为 `Private Use Unicode` 字符。这些字符是：`" * / < > ? \ |` 以及作为文件名最后一个字符的空格或点，字符代码 0x01 到 0x1f（控制字符）以及 Apple 的苹果标志。

遗憾的是，这些专用 Unicode 字符无法被 `genisoimage` NT 可执行文件读取。因此，任何包含这些字符的文件或目录都被忽略 --- 包括任何此类目录的内容。

### Mac OS X AppleDouble

当 Mac OS X 将 HFS/HFS+ 文件复制或保存到非 HFS 文件系统（如 UFS, NFS 等）时，使用 AppleDouble 格式。数据分叉存储在以 `._` 开头的相同文件中。

### Mac OS X HFS (Alpha)

并非真正的 Apple/Unix 编码，但在 Mac OS 系统上的 HFS/HFS+ 文件。数据分叉存储在一个文件中。资源分叉存储在后缀为 `.rsrc` 的相同文件中。Finder info 仅通过 Mac OS 调用可用。

另见 `README.macosx`。仅在 Mac OS X 上有效。如果发现资源分叉长度为零且 finderinfo 为空，则假设没有 Apple/Unix 编码 --- 因此可以使用其他方法设置 `CREATOR` 和 `TYPE`。

`genisoimage` 将尝试从 finder info 设置 `CREATOR`、`TYPE` 和日期以及可能的其他标志。此外，如果存在，Macintosh 文件名将从 finder info 设置，否则基于 Unix 文件名 --- 参见下文的 **HFS MACINTOSH FILENAMES** 部分。

使用 `-apple` 时，`TYPE` 和 `CREATOR` 存储在 ISO9660 目录记录的可选系统使用 `SUSP` 字段中 --- 方式与 Rock Ridge 属性非常相似。事实上，为了方便，Apple 扩展被添加在现有的 Rock Ridge 属性之前（即：获取 Apple 扩展时也能获得 Rock Ridge 扩展）。

Apple 扩展要求资源分叉存储为 ISO9660 关联（associated）文件。这与 ISO9660 文件系统中的任何普通文件类似，只是目录记录中设置了关联标记（第 2 位）。该文件与数据分叉同名（非 Apple 看到的文件）。关联文件通常被其他操作系统忽略。

使用 `-hfs` 时，`TYPE` 和 `CREATOR` 以及其他 finder info 存储在单独 HFS 目录中，在 ISO9660 卷上不可见。HFS 目录引用上述数据和资源分叉文件。在大多数情况下，使用 `-hfs` 而不是 `-apple` 更好，因为后者限制了文件名允许的 ISO9660 字符。然而，Apple 扩展确实提供了文件在磁盘上打包更高效的优势，可能在 CD 上容纳更多文件。



在可能的情况下，将与 Apple/Unix 文件一起存储的 HFS 文件名用于 CD 的 HFS 部分。然而，并非所有的 Apple/Unix 编码都会通过`finderinfo`存储 HFS 文件名。在这些情况下，将使用 Unix 文件名，并对特殊字符进行转义。特殊字符包括`'/'`和代码大于 127 的字符。

AUFS 使用`:'`后跟两个十六进制数字的字符代码来转义这些字符。Netatalk 和 EtherShare 采用类似的方案，但使用的是`%'`而不是`:`。

如果`genisoimage`无法找到 HFS 文件名，它将使用 Unix 名称，并将任何`%xx`或`*:xx`字符（`xx`为两个十六进制数字）转换为单个字符代码。如果`xx`不是十六进制数字（`[0-9a-fA-F]`），则将其保持原样——尽管任何剩余的`:'`会转换为`%'`，因为`:'`是 HFS 的目录分隔符。必须小心，因为带有`%xx`或`*:xx`的普通 Unix 文件也会被转换。例如：

| 原始名称 | 转换结果 |
| --- | --- |
| `This:2fFile` | `This/File` |
| `This:File` | `This%File` |
| `This:t7File` | `This%t7File` |

尽管 HFS 文件名似乎支持大写和小写字母，但该文件系统是不区分大小写的，即文件名`aBc`和`AbC`是相同的。如果在目录中找到具有相同 HFS 名称的文件，`genisoimage`将尝试通过在其中一个文件名后添加`_`字符来创建一个唯一名称。

如果文件存在 HFS 文件名，`genisoimage`可以使用`-mac-name`将此名称作为 ISO9660、Joliet 和 Rock Ridge 文件名的起始点。没有 HFS 名称的普通 Unix 文件仍将使用其 Unix 名称。例如：

如果一个 MacBinary（或 PC Exchange）文件以`someimage.gif.bin`存储在 Unix 文件系统上，但它包含一个名为`someimage.gif`的 HFS 文件，则这将出现在 CD 的 HFS 部分的名称中。然而，由于`genisoimage`使用 Unix 名称作为其他名称的起始点，生成的 ISO9660 名称可能是`SOMEIMAG.BIN`，而 Joliet/Rock Ridge 将是`someimage.gif.bin`。此选项将使用 HFS 文件名作为起始点，ISO9660 名称可能是`SOMEIMAG.GIF`，而 Joliet/Rock Ridge 将是`someimage.gif`。

`-mac-name`目前无法与`-T`配合使用——`TRANS.TBL`文件中使用 Unix 名称，而不是 Macintosh 名称。

用于将任何 HFS 文件名转换为 Joliet/Rock Ridge 文件名的字符集默认为`cp10000`（Mac Roman）。可以使用`-input-hfs-charset`指定使用的字符集。其他内置的 HFS 字符集包括：`cp10006`（MacGreek）、`cp10007`（MacCyrillic）、`cp10029`（MacLatin2）、`cp10079`（MacIcelandandic）和`cp10081`（MacTurkish）。

注意：来自各种 Apple/Unix 格式的 HFS 文件名使用的字符代码将不会转换，因为它们被假设处于正确的 Apple 字符集中。只有从 HFS 文件名派生的 Joliet/Rock Ridge 名称会被转换。

现有的`genisoimage`代码将过滤掉 ISO9660 和 Joliet 文件名的任何非法字符，但由于`genisoimage`期望直接处理 Unix 名称，它让 Rock Ridge 名称保持不变。但由于`'/'`是合法的 HFS 文件名字符，`-mac-name`在 Rock Ridge 文件名中将`'/'`转换为`_`。

如果使用了 Apple 扩展，只有 ISO9660 文件名会出现在 Macintosh 上。然而，由于 Macintosh ISO9660 驱动可以使用`Level 2`文件名，你可以在 Macintosh 上无问题地使用`-allow-multidot`等选项——但仍需小心名称，例如，`this.file.name`将转换为`THIS.FILE`（即只有一个`.`），同样文件名`abcdefgh`将被视为`ABCDEFGH`，但`abcdefghi`将被视为`ABCDEFGHI.`（即末尾有一个`.`）——不知道这是 Macintosh 的问题还是`genisoimage`/`mkhybrid`的问题。在 Macintosh 上查看时，所有文件名都将是大写的。当然，DOS/Win.3.X 机器将无法看到 Level 2 文件。

## HFS 自定义卷/文件夹图标

若要为 HFS CD 提供自定义图标，请确保根（顶层）文件夹包含一个标准的 Macintosh 卷图标文件。在 Macintosh 上为卷提供自定义图标，必须在卷的“Get Info”框中将图标粘贴到卷图标上。这会在根目录中创建一个名为`Icon\r`的不可见文件（`\r`是回车字符）。

自定义文件夹图标非常相似——文件夹本身存在一个名为`Icon\r`的不可见文件。

创建一个`genisoimage`可以使用的自定义图标，可能最简单的方法是在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到它的“Get Info”框中。如果使用安装了 HFS 模块的 Linux，则在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到其“Get Info”框中。

若要在 Macintosh 上为卷提供自定义图标，必须在卷的“Get Info”框中将图标粘贴到卷图标上。这会在根目录中创建一个名为`Icon\r`的不可见文件（`\r`是回车字符）。

自定义文件夹图标非常相似——文件夹本身存在一个名为`Icon\r`的不可见文件。

创建一个`genisoimage`可以使用的自定义图标，可能最简单的方法是在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到它的“Get Info”框中。如果使用安装了 HFS 模块的 Linux，则在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到其“Get Info”框中。

## HFS 字符集与文件名处理

内置的 HFS 字符集包括：`cp10006`（MacGreek）、`cp10007`（MacCyrillic）、`cp10029`（MacLatin2）、`cp10079`（MacIcelandandic）和`cp10081`（MacTurkish）。

注意：来自各种 Apple/Unix 格式的 HFS 文件名使用的字符代码将不会转换，因为它们被假设处于正确的 Apple 字符集中。只有从 HFS 文件名派生的 Joliet/Rock Ridge 名称会被转换。

现有的`genisoimage`代码将过滤掉 ISO9660 和 Joliet 文件名的任何非法字符，但由于`genisoimage`期望直接处理 Unix 名称，它让 Rock Ridge 名称保持不变。但由于`'/'`是合法的 HFS 文件名字符，`-mac-name`在 Rock Ridge 文件名中将`'/'`转换为`_`。

如果使用了 Apple 扩展，只有 ISO9660 文件名会出现在 Macintosh 上。然而，由于 Macintosh ISO9660 驱动可以使用`Level 2`文件名，你可以在 Macintosh 上无问题地使用`-allow-multidot`等选项——但仍需小心名称，例如，`this.file.name`将转换为`THIS.FILE`（即只有一个`.`），同样文件名`abcdefgh`将被视为`ABCDEFGH`，但`abcdefghi`将被视为`ABCDEFGHI.`（即末尾有一个`.`）——不知道这是 Macintosh 的问题还是`genisoimage`/`mkhybrid`的问题。在 Macintosh 上查看时，所有文件名都将是大写的。当然，DOS/Win.3.X 机器将无法看到 Level 2 文件。

若要为 HFS CD 提供自定义图标，请确保根（顶层）文件夹包含一个标准的 Macintosh 卷图标文件。在 Macintosh 上为卷提供自定义图标，必须在卷的“Get Info”框中将图标粘贴到卷图标上。这会在根目录中创建一个名为`Icon\r`的不可见文件（`\r`是回车字符）。

自定义文件夹图标非常相似——文件夹本身存在一个名为`Icon\r`的不可见文件。

创建一个`genisoimage`可以使用的自定义图标，可能最简单的方法是在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到它的“Get Info”框中。如果使用安装了 HFS 模块的 Linux，则在 Mac 上格式化一张空白的 HFS 软盘，并将图标粘贴到其“Get Info”框中。

```bash
mount -t hfs /dev/fd0
```

## EL TORITO 启动信息表

当给出`-boot-info-table`时，`genisoimage`将在`-b`指定的文件偏移 8 处插入一个 56 字节的启动信息表。此修改是在源文件系统中进行的，因此如果此文件无法重新创建，请确保使用副本！此文件包含在启动时可能无法或无法可靠获取的指针。

此表的格式如下；所有整数均采用节 7.3.1（小端）格式。

| 偏移 | 名称 | 大小 | 含义 |
| :--- | :--- | :--- | :--- |
| 8 | `bi_pvd` | 4 字节 | 主卷描述符的 LBA |
| 12 | `bi_file` | 4 字节 | 启动文件的 LBA |
| 16 | `bi_length` | 4 字节 | 以字节为单位的启动长度 |
| 20 | `bi_csum` | 4 字节 | 32 位校验和 |
| 24 | `bi_reserved` | 40 字节 | 预留 |

32 位校验和是从字节偏移 64 开始的所有 32 位字之和。所有线性块地址（LBA）均以 CD 扇区（通常为 2048 字节）给出。

要为 HPPA 创建一个可启动 CD，至少必须指定一个引导程序文件（`-hppa-bootloader`）、一个内核镜像文件（取决于硬件的 32 位、64 位或两者兼有）以及启动命令行（`-hppa-cmdline`）。某些系统可以启动 32 位或 64 位的内核，如果两者都存在，固件将选择其中一个。可选地，可以使用`-hppa-cmdline`使用`ramdisk`作为根文件系统。

# JIGDO 说明

Jigdo 是一种帮助分发 CD 和 DVD 镜像等大文件的工具；详情请参见相关说明。Debian CD 和 DVD ISO 镜像以 jigdo 格式发布在网络上，以便终端用户更高效地下载。

要在使用`genisoimage`创建 ISO 镜像的同时创建 jigdo 和模板文件，你必须首先生成一个将要使用的文件列表，格式如下：

`MD5sum File size Path 32 chars 12 chars to end of line`

`MD5sum`必须以标准十六进制格式写入，文件大小必须列出以字节为单位的大小，路径必须列出文件的绝对路径。例如：

```text
00006dcd58ff0756c36d2efae21be376 14736 /mirror/debian/file1
000635c69b254a1be8badcec3a8d05c1 211822 /mirror/debian/file2
00083436a3899a09633fc1026ef1e66e 22762 /mirror/debian/file3
```

一旦你有了这个文件，请带上所有常规命令行参数调用`genisoimage`。使用`-jigdo-jigdo`和`-jigdo-template`指定 jigdo 和模板文件的输出文件名，并通过`-md5-list`传入你的 MD5 列表的位置。

如果有你不希望加入 jigdo 文件中的文件（例如，它们可能经常变化），请使用`-jigdo-exclude`指定这些文件。如果你想在文件写入镜像时验证某些文件，请使用`-jigdo-force-md5`指定它们。如果任何文件不匹配，`genisoimage`将中止执行。这两个选项都接受正则表达式作为输入。还可以根据大小进一步限制将要使用的文件集——使用`-jigdo-min-file-size`选项。

最后，jigdo 代码需要知道如何将给定的文件映射到镜像风格配置上。使用`-jigdo-map`指定如何映射路径。使用`Debian=/mirror/debian`将导致所有以`/mirror/debian`开头的路径映射到输出 jigdo 文件中的`Debian:<file>*`。

## 示例

要在文件`cd.iso`中创建一个纯的 ISO9660 文件系统镜像，其中目录`cd_dir`将成为 CD 的根目录，请调用：

```bash
genisoimage -o cd.iso cd_dir
```

创建一个带有源目录`cd_dir` Rock Ridge 扩展的 CD：

```bash
genisoimage -o cd.iso -R cd_dir
```

创建一个带有源目录`cd_dir` Rock Ridge 扩展的 CD，其中所有文件至少具有读权限且所有文件的所有者均为`root`，调用：

```bash
genisoimage -o cd.iso -r cd_dir
```

将 tar 归档直接写入 CD，该 CD 之后将包含带有该 tar 归档的简单 ISO9660 文件系统：

```bash
tar cf - . | genisoimage -stream-media-size 333000 | \
    wodim dev=b,t,l -dao tsize=333000s -
```

创建一个带有源目录`cd_dir` Joliet 和 Rock Ridge 扩展的 HFS 混合 CD：

```bash
genisoimage -o cd.iso -R -J -hfs cd_dir
```

从源目录`cd_dir`创建一个包含 Netatalk Apple/Unix 文件的 HFS 混合 CD：

```bash
genisoimage -o cd.iso --netatalk cd_dir
```

从源目录`cd_dir`创建一个 HFS 混合 CD，仅根据文件`mapping`中列出的文件名扩展名为所有文件赋予`CREATOR`和`TYPES`：

```bash
genisoimage -o cd.iso -map mapping cd_dir
```

从源目录`cd_dir`和`another_dir`创建带有 Apple 扩展的 ISO9660 CD。所有已知的 Apple/Unix 格式的文件都会解码，任何其他文件将根据文件`magic`提供的魔数（magic number）赋予`CREATOR`和`TYPE`：

```bash
genisoimage -o cd.iso -apple -magic magic -probe \
    cd_dir another_dir
```

以下示例将不同的文件放在 CD 上，这些文件都名为 README，但在被视为 ISO9660/Rock Ridge、Joliet 或 HFS CD 时，它们的内容不同。

当前目录包含：

```text
ls -F
README.hfs README.joliet README.Unix cd_dir/
```

以下命令将`cd_dir`目录的内容放在 CD 上，并带有 Rock Ridge、Joliet 和 HFS 扩展：

```bash
genisoimage -o cd.iso -R -J -hfs cd_dir
```

在使用多会话选项`-M`和`-C`创建 HFS 卷时，只有最后一个会话中的文件会位于 HFS 卷中。也就是说，`genisoimage`无法添加来自之前会话的现有文件到 HFS 卷。

然而，如果每个会话都使用`-part`创建，则每个会话在 Mac 上挂载时将显示为独立的卷。在这种情况下，建议使用`-V`或`-hfs-volid`为每个会话指定一个唯一的卷名称，否则每个“卷”将以相同的名称出现在桌面上。

符号链接（与所有其他非普通文件一样）不会被添加到 HFS 目录中。

混合卷可能比包含相同数据的纯 ISO9660 卷大。在某些情况下（例如 DVD 尺寸的卷），这种差异可能是显著的。随着 HFS 卷的变大，分配块大小（文件可以占据的最小空间单位）也会随之增大。对于 650MB 的 CD，分配块为 10kB；对于 4.7GB 的 DVD，它约为 70kB。

HFS 卷中的文件最大数量约为 65500——尽管实际限制会比此小。

可以使用`hfsutils`常程在 Unix 机器上访问生成的混合卷。然而，无法对卷进行任何更改，因为它被设置为锁定状态。`-hfs-unlock`选项将创建一个未锁定的输出镜像——但是，不应对卷的内容进行任何更改（除非你真的知道自己在做什么），因为它不是一个“真正的”HFS 卷。

`-mac-name`目前无法与`-T`配合使用——`TRANS.TBL`文件将使用 Unix 名称，而不是 Macintosh 名称。

尽管`genisoimage`不会修改文件内容，但如果二进制文件的`TYPE`设置为`TEXT`，在 Macintosh 上可能被错误地读取。因此，默认`TYPE`更好的选择可能是`????`。

`-mac-boot-file`可能完全不起作用……

可能无法与 PC Exchange v2.2 或更高版本的文件配合（MacOS 8.1 提供）。在使用 Linux 时，包含 PC Exchange 文件的 DOS 介质应挂载为`msdos`类型（而不是`vfat`）。

SFM 格式仅得到部分支持——请参见上文 **HFS MACINTOSH FILE FORMATS** 章节。



无法结合 `-boot-hfs-file` 或 `-prep-boot` 使用 `-sparc-boot` 或 `-generic-boot`。

`genisoimage` 应该能够创建超过 4Gb 的 HFS 混合镜像，尽管尚未经过充分测试。

## 参见

(5)、(1)、(8)、(5)。

## 作者

`genisoimage` 衍生自 2006 年 5 月 `cdrtools 2.01.01a08` 包中的 `mkisofs`，提取了来自 2007 年 3 月 `cdrtools 2.01.01a24` 的少量更新，来自 .IR，但现在是 `cdrkit` 工具套件的一部分，由 Joerg Jaspert、Eduard Bloch、Steve McIntyre、Peter Samuelson、Christian Fromme、Ben Hutchings 以及其他贡献者维护。可以通过以下方式联系维护者，或访问 `cdrkit` 项目网站。

Eric Youngdale 编写了 `mkisofs` 的早期版本（1993—1998）。Jörg Schilling 编写了 SCSI 传输库及其接口，并自 1999 年以来维护了 `mkisofs`。James Pearson 编写了 HFS 混合代码，使用了 Robert Leslie 的 `libhfs`。Pearson、Schilling、Jungshik Shin 和 Jaakko Heinonen 为字符集转换代码做出了贡献。`cdrkit` 维护者自 2006 年以来维护了 `genisoimage`。

```
Copyright 1993-2007 The Authors.
All rights reserved.
```

GOST R 34.10 算法参数文件是可选的。可以在密钥密钥期间指定参数，也可以在生成参数文件时指定。

`paramset:name`

根据 RFC 4357 指定 GOST R 34.10-2001 参数集。可以使用缩写名称、对象短名称或数字 OID 来指定参数集。支持以下参数集：

| 参数集 | OID | 用途 |
|---|---|---|
| A | `1.2.643.2.2.35.1` | Signature |
| B | `1.2.643.2.2.35.2` | Signature |
| C | `1.2.643.2.2.35.3` | Signature |
| XA | `1.2.643.2.2.36.0` | Key exchange |
| XB | `1.2.643.2.2.36.1` | Key exchange test |
| Test | `1.2.643.2.2.35.0` | Test purposes |

## 注意事项

建议使用 `genpkey` 程序而非特定算法工具，因为可以使用额外的算法选项和 ENGINE 提供的算法。

## 示例

使用默认参数生成 RSA 私钥：

```
openssl genpkey -algorithm RSA -out key.pem
```

使用 128 位 AES 和密码 `hello` 加密输出私钥：

```bash
openssl genpkey -algorithm RSA -out key.pem -aes-128-cbc -pass pass:hello
```

使用 3 作为公指数生成 2048 位 RSA 密钥：

```bash
openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:2048 \
-pkeyopt rsa_keygen_pubexp:3
```

生成 1024 位 DSA 参数：

```bash
openssl genpkey -genparam -algorithm DSA -out dsap.pem \
-pkeyopt dsa_paramgen_bits:1024
```

从参数生成 DSA 密钥：

```bash
openssl genpkey -paramfile dsap.pem -out dsakey.pem
```

生成 1024 位 DH 参数：

```bash
openssl genpkey -genparam -algorithm DH -out dhp.pem \
-pkeyopt dh_paramgen_prime_len:1024
```

输出带有 224 位子群的 RFC5114 2048 位 DH 参数：

```bash
openssl genpkey -genparam -algorithm DH -out dhp.pem \
-pkeyopt dh_rfc5114:2
```

从参数生成 DH 密钥：

```bash
openssl genpkey -paramfile dhp.pem -out dhkey.pem
```

# GENRSA

## 名称

`genrsa` — 生成 RSA 私钥

## 语法

`openssl genrsa [-out filename] [-passout arg] [-aes128] [-aes128] [-aes192] [-aes256] [-camellia128] [-camellia192] [-camellia256] [-aes192] [-aes256] [-camellia128] [-camellia192] [-camellia256] [-des] [-des3] [-idea] [-f4] [-3] [-rand file(s)] [-engine id] [numbits]`

## 描述

`genrsa` 命令生成 RSA 私钥。

### 选项

#### `-out filename`

输出文件名。如果未指定此参数，则使用标准输出。

#### `-passout arg`

输出文件的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

#### `-aes128|-aes192|-aes256|-camellia128|-camellia192|-camellia256|-des|-des3|-idea`

这些选项在输出私钥之前使用指定的加密算法对私钥进行加密。如果未指定其中任何一个选项，则不使用加密。如果使用了加密，且未通过 `-passout` 参数提供密码，则会提示输入。

#### `-F4|-3`

使用的公指数，可以是 65537 或 3。默认值为 65537。

#### `-rand file(s)`

包含随机数据的文件或多个文件，用于随机数生成器的种子，或者是 EGD 套接字（参见 (3)）。可以使用依赖系统的字符分隔多个文件。MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他系统使用 `:`。

#### `-engine id`

指定引擎。通过其唯一的 `id` 字符串将导致 `genrsa` 尝试获取指定引擎的功能引用，并在需要时对其初始化。该引擎将被设置为所有可用算法的默认引擎。

#### `numbits`

要生成的私钥大小（位）。这必须是最后一个选项。默认值为 512。

## 注意事项

RSA 私钥的生成本质上涉及两个质数。在生成私钥时，将输出各种符号以指示生成进度。`.` 代表通过初始筛选测试的数字，`+` 表示数字通过了单轮 Miller-Rabin 质性测试。



`-out filename`

输出文件名。如果未指定此参数，则使用标准输出。

`-passout arg`

输出文件的密码源。有关 `arg` 格式的更多信息，请参见 (1) 中的 `PASS PHRASE ARGUMENTS` 部分。

`-aes128|-aes192|-aes256|-camellia128|-camellia192|-camellia256|-des|-des3|-idea`

这些选项在输出私钥之前使用指定的加密算法对私钥进行加密。如果未指定其中任何一个选项，则不使用加密。如果使用了加密，且未通过 `-passout` 参数提供密码，则会提示输入。

`-F4|-3`

使用的公指数，可以是 65537 或 3。默认值为 65537。

`-rand file(s)`

包含随机数据的文件或多个文件，用于随机数生成器的种子，或者是 EGD 套接字（参见 (3)）。可以使用依赖系统的字符分隔多个文件。MS-Windows 使用 `;`，OpenVMS 使用 `,`，其他系统使用 `:`。

`-engine id`

指定引擎（通过其唯一的 `id` 字符串）将导致 `genrsa` 尝试获取指定引擎的功能引用，并在需要时对其初始化。该引擎将被设置为所有可用算法的默认引擎。

`numbits`

要生成的私钥大小（位）。这必须是最后一个选项。默认值为 512。

## 注意事项

RSA 私钥的生成本质上涉及两个质数。在生成私钥时，将输出各种符号以指示生成进度。`.` 代表通过初始筛选测试的数字，`+` 表示数字通过了单轮 Miller-Rabin 质性测试。

# 名称

`eqn` - 为 troff 或 MathML 格式化方程

# 语法

`[-rvCNR]` `[-d xy]` `[-T name]` `[-M dir]` `[-f F]` `[-s n]` `[-p n]` `[-m n]` `[*files...]`

# 描述

本手册页描述 **eqn** 的 GNU 版本，它是 groff 文档格式系统的一部分。**eqn** 将嵌入在 **troff** 输入文件中方程描述编译为 **troff** 理解的命令。通常，应该使用 groff 的 `-e` 选项调用它。语法与 Unix eqn 高度兼容。GNU **eqn** 的输出无法用 Unix troff 处理；必须用 GNU troff 处理。如果命令行上没有提供文件，则读取标准输入。

**eqn** 首先在 `-M` 选项指定的目录中搜索 **eqnrc** 文件，然后在 **/etc/groff/site-tmac**、**/etc/groff/site-tmac**，最后在标准宏目录 **/usr/share/groff/1.22.3/tmac** 中搜索。如果该文件存在，**eqn** 在其他输入文件之前处理它。`-R` 选项可以防止此操作。

GNU **eqn** 不提供 neqn 的功能：它不支持低分辨率的打字机设备（尽管对于非常简单的输入，效果可能良好）。

## 选项

命令行选项与其参数之间可以存在空格。

`-dxy`

分别指定行内公式左侧和右侧的分隔符 `x` 和 `~y`。源文件中任何 `delim` 语句都会覆盖此设置。

`-C`

即使在后面跟着非空格或换行符的字符时，也能识别 `.EQ` 和 `.EN`。此外，不会特殊处理语句 `'delim on'`。

`-N`

不允许在分隔符内换行。此选项允许 `eqn` 在缺少结束分隔符时能更好地恢复。

`-v`

打印版本号。

`-r`

仅进行一次尺寸缩小。

`-mn`

最小点号字体为 `~n`。`eqn` 不会将下标或上标的大小缩小到比 `~n` 更小。

`-Tname`

输出针对设备 `name`。通常情况下，此选项的作用是定义一个值为 `~1` 的宏 `name`；`eqnrc` 使用此为输出设备提供相应的定义。然而，如果指定的设备是 "MathML"，则输出将为 MathML 标记而非 troff 命令，且完全不会加载 `eqnrc`。默认输出设备为 `ps`。

`-Mdir`

在默认目录之前在 `dir` 中搜索 `eqnrc`。

`-R`

不加载 `eqnrc`。

`-fF`

这等同于 `gfont F` 命令。

`-sn`

这等同于 `gsize n` 命令。此选项已废用。`eqn` 通常在遇到公式时，按当前的点号字体大小设置公式。

`-pn`

这表示下标和上标应比周围文本小 `n~points`。此选项已废用。通常 `eqn` 将下标和上标的大小设置为周围文本大小的 70%。

# USAGE

此处仅描述 GNU `eqn` 与 Unix `eqn` 之间的差异。

## GNU eqn vs. Unix eqn

GNU `eqn` 在使用 `-T~MathML` 选项调用时会生成演示型 MathML 输出。

GNU `eqn` 将输入标记 `...` 设置为三个点或低点，而不是经典 `eqn` 的三个居中点。要获得三个居中点，请写 `cdots` 或 `cdot cdot cdot.`。

GNU `eqn` 输入语言的大多数新功能基于 TeX。下文提到了一些 TeX 与 GNU `eqn` 之间的差异；如果你不知道 TeX，可以安全地忽略这些。

## 控制分隔符

如果不在兼容模式下，`eqn` 识别

`delim on`

用于恢复之前通过 `delim off` 禁用的分隔符。如果未指定分隔符，则该调用不起作用。

## 自动间距

`eqn` 为公式的每个组件分配一个类型，并根据该类型调整组件之间的间距。可能的类型有：

- ordinary（普通）：普通字符，如 '1' 或 'x'；
- operator（运算符）：大型运算符，如 'ÎŁ`；
- binary（二元）：二元运算符，如 `+`；
- relation（关系）：关系如 `=`；
- opening（左）：如 `(`；
- closing（右）：如 `)`；
- punctuation（标点）：标点符号如 `,cl;`；
- inner（内部）：括号内的子公式；
- suppress spacing（抑制间距）：抑制自动间距调整。

公式组件通过两种方式之一获取类型。

`type te`

这产生一个包含 `e` 的公式组件，但其类型为 `t`，其中 `t` 是上述类型之一。例如，`times` 定义为：

```
type "binary" \(mu
```

类型的名称不需要引号，但加引号可以防止宏展开。`chartype t text` 未加引号的字符组会被拆分成单个字符，并查找每个字符的类型；这会更改存储的每个字符的类型；它表示从现在起 `text` 中的字符类型为 `~t`。例如，

```
chartype "punctuation" .,;:
```

将使得字符 `'.,;:` 在此后出现在公式中都具有标点类型。类型 `t` 也可以是 `letter` 或 `digit`；在这些情况下，`chartype` 会改变字符的字体类型。参见 `Fonts` 节。

## 新原语

`big e`

放大其修改的表达式；意在具有类似于 CSS 'large' 的语义。在 troff 输出中，点号字体增加了~5；在 MathML 输出中，表达式使用：

```xml
<mstyle mathsize='big'>
```

`e1 smallover e2` 这类似于 `over`；`smallover` 减小 `e1` 和 `e2` 的尺寸；它还在 `e1` 或 `e2` 与分线之间留更少的垂直空间。`over` 原语对应于显示样式中的 TeX `\over` 原语；`smallover` 对应于非显示样式中的 `\over`。`vcenter e` 将 `e` 绕着数学轴垂直居中。数学轴是 `+cq` 和 `-` 等字符居中的垂直位置；它也是用于分数分线的垂直位置。例如，`sum` 定义为：

```latex
{ type "operator" vcenter size +5 \(*S }
```

（注意在生成 MathML 时，vcenter 被静忽略。）

`special text e` 这使用一个名为 `text` 的 (1) 宏从 `e` 构建一个新对象。（实际上，查看提供的文本，我将格式化最后的特定块）。

```latex
.EQ
define box 'special Bx'
.EN
.de Bx
.���ds 0s \
\Z'\h'1n'\\*(0s'\
\Z'\
```

```
\D'l 0 \\n(0hu+\\n(0du+2n'
\h'\\n(0wu+2n'
```

- `nr 0w +2n`

- `nr 0d +1n`

- `nr 0h +1n`

`space n` 整数 `n` 的正值（单位为 em 的百分分之一）用于设置公式前的垂直间距，负值用于设置公式后的间距，并替换默认值。该原语为 `groff` 的 `\x` 转义字符提供了一个接口（但符号符号相反）。如果公式是 `pic` 图像的一部分，则该关键字不起作用。

## 扩展原语

`col n {...}` `ccol n {...}` `lcol n {...}` `rcol n {...}` `pile n {...}` `cpile n {...}` `lpile n {...}` `rpile n {...}` 整数值 `n`（单位为 em 的百分分之一）增加行之间的垂直间距，使用 `groff` 的 `\x` 转义字符（该值在 MathML 模式下无效）。可以是负值，但无效。如果矩阵中给出多个值，则使用最大的一个。

## 定制化

当 `eqn` 生成 troff 标记时，公式的外观由大量参数控制。在生成 MathML 模式时，这些参数无效，因为该模式将排版和微调交给了下游的 MathML 渲染引擎。可以使用 `set` 命令设置这些参数。

`set p n`

这会将参数 `p` 设置为值 `n`；`n` 是一个整数。例如，

```
set x_height 45
```

表示 `eqn` 应该假设 x 高为 0.45 em。

可能的参数如下。除非另有说明，值的单位均为 em 的百分之一。这些描述旨在阐释，而非给出确定性定义。

`minimum_size`

`eqn` 不会对小于此值的点字号设置任何内容。值的单位是磅（points）。

`fat_offset`

`fat` 原语通过覆盖水平偏移此距离的两个公式副本来使公式加粗。此参数在 MathML 模式下不使用；相反，粗体使用：

```
<mstyle mathvariant='double-struck'>
```



`over_hang`：分数线比分子和分母宽度最大值长两倍此数值；换句话说，它至少超出分子和分母此数值长度。

`accent_width`：当 `bar` 或 `under` 应用于单个字符时，线条长度为此。通常情况下，`bar` 或 `under` 产生的线条长度等于所应用对象的宽度；对于单个字符，这往往会产生一条看起来太宽的线。

`delimiter_factor`：使用 `left` 和 `right` 原语生成的扩展分隔符，其总高度和深度至少为被分隔符包围的子方程离轴最大距离的两倍的若干几千分之一。

`delimiter_shortfall`：使用 `left` 和 `right` 原语生成的扩展分隔符，其总高度和深度不小于被分隔符包围的子方程离轴最大距离的两倍与此值之差。

`null_delimiter_space`：在分数的每侧插入此宽的水平空间。

`script_space`：下标和上标的宽度增加此数值。

`thin_space`：在标点符号字符后自动会自动插入此数量的空间。

`medium_space`：在二元运算符的两侧自动插入此数量的空间。

`thick_space`：在关系符号的两侧自动插入此数量的空间。

`x_height`：不带升部字母的小写字母（如 `x`）的高度。

`axis_height`：字符 `+` 和 `-` 等字符中心相对于基线的高度。对于你正在使用的字体，该值的正确至关重要。

`default_rule_thickness`：这应设置为 `\(ru` 字符的厚度，或使用 `\D` 转义序列产生的水平线的厚度。

`num1`：`over` 命令将分子向上移动至少此距离。

`num2`：`smallover` 命令将分子向上移动至少此距离。

`denom1`：`over` 命令将分母向下移动至少此距离。

`denom2`：`smallover` 命令将分母向下移动至少此距离。

`sup1`：通常情况下，上标被向上移动至少此距离。

`sup2`：上标内部的上标、上限或 `smallover` 分式分子中的上标被向上移动至少此距离。这通常小于 `sup1`。

`sup3`：分母、根号、下标或下限内部的上标向上移动至少此距离。这通常小于 `sup2`。

`sub1`：下标通常被向下移动至少此距离。

`sub2`：当同时存在下标和上标时，下标被向下移动此距离。

`sup_drop`：上标的基线不低于其所在物体下方的此距离。

`sub_drop`：下标的基线至少位于其所在物体的下方此距离。

`big_spacing_1`：上限的基线至少在其所在的物体上方此距离。

`big_spacing_2`：下限的基线至少在其所在的物体下方此距离。

`big_spacing_3`：上限的顶部至少在其所在的物体上方此距离。

`big_spacing_4`：下限的底部至少在其所在的物体下方此距离。

`big_spacing_5`：在限制的上下下方添加此垂直空间。

`baseline_sep`：`pile` 中行之间的基线间隔通常为此距离。

`shift_down`：矩阵中顶基线和底基线相对于轴向下偏移此距离。

`column_sep`：矩阵列之间添加此宽的空间。

`matrix_side_sep`：在矩阵每侧添加此宽的空间。

`draw_lines`：若此非零，则使用 `\D` 转义序列绘制线条，而不是使用 `\l` 转义序列和 `\(ru` 字符。

`body_height`：公式高度超过此值将作为公式前的额外间距（使用 `\x`）。默认值为 85。

`body_depth`：公式深度超过此值的深度将作为公式后的额外间距（使用 `\x`）。默认值为 35。

`nroff`：若此非零，则 `ndefine` 行为如 `define` 且忽略 `tdefine`；否则 `tdefine` 行为如 `define` 且忽略 `ndefine`。默认值为 0（这通常由 `eqnrc` 文件为 `ascii`、`latin1`、`utf8` 和 `cp1047` 设备改为 1）。

关于这些许多参数作用的更精确描述可见 *The TeXbook* 的附录 H。

## 宏

宏可以接受参数。在宏主体中，`n`（`n` 在 1 到 9 之间）在带参数调用宏时，会被替换为第 n 个参数；如果参数少于 n 个，则被替换为空。

包含左括号的单词，如果左括号前的部分已使用 `define` 命令定义，则会被识别为带参数的宏调用；左括号到匹配右括号之间的字符被视为逗号分隔的参数；嵌套括号内的逗号不会终止参数。

`sdefine name anything`

这类似于 `define` 命令，但 `name` 在带参数调用时不会被识别。

`include files`

`copy files` 包含 `file` 的内容（`include` 和 `copy` 是同义词）。以 `.EQ` 或 `.EN` 开头的 `file` 行将被忽略。

`ifdef name X anything X`

如果 `name` 已通过 `define` 定义（或因为 `name` 是输出设备而自动定义），则处理 `anything`；否则忽略 `anything`。`X` 可以是任意未出现在 `anything` 中的字符。

`undef name`

移除 `name` 的定义，使其变为未定义。

除了上述宏外，可以使用以下定义：`Alpha`、`Beta`、……`Omega`（这与 `ALPHA`、`BETA`……`OMEGA` 相同）、`ldots`（基线上的三个点）和 `dollar`。

## 字体

`eqn` 通常使用至少两种字体来设置公式：用于字母的斜体字体和用于其他内容的正字体。现有的 `gfont` 命令更改用作斜体的字体。默认情况下是 `~I`。用作正体的字体可以使用新的 `grfont` 命令进行更改。

`grfont f`

将正字体设置为 `~f`。

`italic` 原语使用由 `gfont` 设置的当前斜字体；`roman` 原语使用由 `grfont` 设置的当前正字体。还有一个新的 `gbfont` 命令，更改 `bold` 原语使用的字体。

如果你只使用 `roman`、`italic` 和 `bold` 原语在公式内更改字体，你可以通过使用 `gfont`、`grfont` 和 `gbfont` 命令更改公式中使用的所有字体。

你可以通过上述描述的 `chartype` 命令控制哪些字符被视为字母（并因此以斜体设置）。`letter` 类型会导致字符被设置为斜体类型。`digit` 类型会导致字符被设置为正体类型。

# 文件

`u+2n`

`/usr/share/groff/1.22.3/tmac/eqnrc` 初始化文件。

## MathML 模式限制

MathML 的设计假设是，它无法获知渲染媒体和设备的精确物理特性。它对动作和大小的控制无法达到像 `troff` 那样的精细程度。因此：

- `eqn` 参数对生成的 MathML 没有影响。
- `special`、`up`、`down`、`fwd` 和 `back` 操作无法实现，而是产生 MathML `<merror>` 消息。
- `vcenter` 关键字被静默忽略，因为在数学轴上居中是 MathML 的默认设置。
- `eqn` 比 `troff` 设置得更大的字符（特别是积分号）可能看起来太小，需要手动调整它们的 `<mstyle>` 包装器。

与其 `troff` 模式一样，MathML 模式下的 `eqn` 为显示公式保留 `.EQ` 和 `.EN` 分隔符，但不对内联公式发射显式分隔符。然而，它们可以识别为以 `<math>` 开头并 `</math>` 结尾且不跨越行的字符串。

参见 `BUGS` 部分关于 `eqn` 的特定翻译限制。

## 缺陷

内联公式按输入行开始时的当前字号设置。

在 MathML 模式下，`mark` 和 `lineup` 功能不起作用。理论上，可以使用 `<maligngroup>` 元素实现。

在 MathML 模式下，数字字面量的每个数字都获得一个单独的 `<mn>:</mn>` 对，小数点被标记为 `<mo>:</mo>`。规范允许这样做，但效率低下。

## 另参

`(1)`、`(1)`、`(1)`、`(5)`、*The TeXbook*

## 复制

版权所有 © 1989-2014 Free Software Foundation, Inc.

允许制作并分发本手册的逐字副本，前提是所有副本上必须保留版权声明和此许可声明。

允许在逐字复制条件下复制和分发本手册的修改版本，前提是整个生成的派生作品必须按照与此相同的许可声明条款进行分发。

允许在上述修改版本的条件下将本手册翻译成另一种语言，但例外是此许可声明可以包含在由自由软件基金会批准的翻译中，而不是在原始英文中。

# GETCIFSACL

## 节点

`getcifsacl` - 用于显示通用互联网文件系统（CIFS）安全描述符中 ACL（访问控制列表）的用户空间辅助程序

## 语法概要

`getcifsacl [-v|-r] {file system object}`

## 描述

此工具是 `cifs-utils` 套件的一部分。

`getcifsacl` 是 Linux CIFS 客户端文件系统的用户空间辅助程序。它用于显示包含文件系统对象 ACL 的描述符。

该程序使用插件处理 SID 到用户和组名的映射。`/etc/cifs-utils/idmap-plugin` 应该是一个指向要用插件的符号链接。

ACE 的字段如 `SID`、类型、标志和掩码用 `/` 分隔显示。类型、标志和掩码的数值以十六进制格式显示。

## 选项

- `-v`：打印版本号并退出。
- `-r`：以原始模式显示安全描述符。类型和标志等值以十六进制格式显示，`SID` 不映射为名称。

## 注意

内核对 `getcifsacl/setcifsacl` 的支持最初在 2.6 中引入。

## 另参

`(8)`、`(1)`

## 作者

Shirish Pargakar 写了 `getcifsacl` 程序。Linux CIFS 邮件列表是询问这些问题的首选。

# GETENT

## 节点

`getent` - 从名称切换获取条目

## 语法概要

`getent [option] [database] [key]`

## 描述

`getent` 命令从名称切换库显示条目，这些库配置在 `/etc/nsswitch.conf` 中。如果提供了多个 `key` 参数，将显示匹配键的条目。否则，如果没有提供 `key`，将显示所有条目（除非数据库不支持枚举）。

`database` 可以是 GNU C 支持的数据库：

### hosts

在未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 hosts 数据库。这与 `hosts` 相同。当提供了多个 `key` 参数时，将每个 `key` 传递给 `(3)` 并枚举返回的套字结构。

### ahsv4

与 `ahosts` 相同，但使用地址族 `AF_INET`。

### ahostsv6

与 `ahosts` 相同，但使用地址族 `AF_INET6`。在这种情况下对 `(3)` 的调用包含了 `AI_V4MAPPED` 标志。

### aliases

在未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 aliases 数据库。当提供了多个 `key` 参数时，将每个 `key` 连续传递给 `(3)` 并显示结果。

### ethers

当提供了多个 `key` 参数时，将每个 `key` 连续传递给 `(3)` 和 `(3)` 直到获得结果并显示结果。`ethers` 不支持，因此必须提供 `key`。

### group

在未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 group 数据库。当提供了多个 `key` 参数时，将每个数值 `key` 传递给 `(3)`，将非数值 `key` 传递给 `(3)` 并显示结果。

### gshadow

在未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 gshadow 数据库。当提供了多个 `key` 参数时，将每个 `key` 连续传递给 `(3)` 并显示结果。

### hosts

在未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 hosts 数据库。当提供了多个 `key` 参数时，根据对 `(3)` 的调用指示 `key` 是否为 IPv6 或 IPv4 地址，将 `key` 传递给 `(3)` 或 `(3)`，并显示结果。

当提供一个或多个 `key` 参数时，将每个 `key` 连续传递给 `(3)` 并显示结果。`initgroups` 不支持枚举，因此必须提供 `key`。

### netgroup

当提供一个 `key` 时，将该 `key` 传递给 `(3)` 并使用 `(3)` 显示生成的字符串三元组（`hostname`、`username`、`domainname`）。

或者，也可以提供三个 `key`，它们被解释为 `hostname`、`username` 和 `domainname`，通过 `(3)` 匹配 netgroup 名称。`netgroup` 不支持枚举，因此必须提供一个或三个 `key`。

### networks

当未提供 `key` 时，使用 `(3)`、`(3)` 和 `(3)` 穷举 networks 数据库。当提供一个或多个 `key` 参数时，将每个数字 `key` 传递给 `(3)`，将每个非数字 `key` 传递给 `(3)` 并显示结果。

### passwd

当未提供 `key` 时，使用 `(3)`、`(3)` 和 `(3)` 穷举 passwd 数据库。当提供一个或多个 `key` 参数时，将每个数字 `key` 传递给 `(3)`，将每个非数字 `key` 传递给 `(3)` 并显示结果。

### protocols

当未提供 `key` 时，使用 `(3)`、`(3)` 和 `(3)` 穷举 protocols 数据库。当提供一个或多个 `key` 参数时，将每个数字 `key` 传递给 `(3)`，将每个非数字 `key` 传递给 `(3)` 并显示结果。

### rpc

当未提供 `key` 时，使用 `(3)`、`(3)` 和 `(3)` 穷举 rpc 数据库。当提供一个或多个 `key` 参数时，将每个数字 `key` 传递给 `(3)`，将每个非数字 `key` 传递给 `(3)` 并显示结果。

### services

当未提供 `key` 时，使用 `(3)`、`(3)` 和 `(3)` 穷举 services 数据库。当提供一个或多个 `key` 参数时，将每个数字 `key` 传递给 `(3)`，将每个非数字 `key` 传递给 `(3)` 并显示结果。

### shadow

当未提供 `key` 时，使用 `(3)`、`(3)`、`(3)` 列举 shadow 数据库。当提供了多个 `key` 参数时，将每个 `key` 连续传递给 `(3)` 并显示结果。

## OPTIONS

`-s service, --service service`

用指定的服务覆盖所有数据库。（自 glibc 2.2.5 起支持）

`-s database:service, --service database:service`

仅用指定的服务覆盖指定的数据库。该选项可以使用多次，但每个数据库将仅使用最后一个服务。（自 glibc 2.4 起支持）

`-i`、`--no-idn`

在 `ahosts`/`(3)` 的查找中禁用 IDN 编码。（自 glibc-2.13 起支持）

`-?`、`--help`

打印用法摘要并退出。

`--usage`

打印简短的用法摘要并退出。

`-V`、`--version`

打印 `getent` 的版本号、许可协议和免责声明。

## EXIT STATUS

`getent` 可以返回以下退出值之一：

### `0`

命令成功完成。

### `1`

缺少参数或 `database` 未知。

### `2`

在 `database` 中未找到一个或多个提供的 `key`。

### `3`

该 `database` 不支持枚举。

## SEE ALSO

`(5)`

## COLOPHON

本页面是 Linux *man-pages* 项目发布 4.00 的。关于项目的描述、报告错误的信息以及本页面的最新版本可以在此处找到：

* *

# GETFACL

## NAME

`getfacl` - 获取文件访问控制列表

## SYNOPSIS

```text
getfacl [-aceEsRLPtpndvh] file ...
getfacl [-aceEsRLPtpndvh] -
```

## DESCRIPTION

对于每个文件，`getfacl` 会显示文件名、所有者、组以及访问控制列表（ACL）。如果目录有默认 ACL，`getfacl` 还会显示默认 ACL。非目录不能有默认 ACL。

如果在不支持 ACL 的文件系统上使用 `getfacl`，`getfacl` 将显示传统文件模式权限位定义的访问权限。

`getfacl` 的输出格式如下：

```text
1: # file: somedir/
2: # owner: lisa
3: # group: staff
4: # flags: -s-
5: user::rwx
6: user:joe:rwx #effective:r-x
7: group::rwx #effective:r-x
8: group:cool:r-x
9: mask::r-x
10: other::r-x
11: default:user::rwx
12: default:user:joe:rwx #effective:r-x
13: default:group::r-x
14: default:mask::r-x
15: default:other:---
```

第 1--3 行指示文件名、所有者和所属组。

第 4 行指示 `setuid`（`s`）、`setgid`（`s`）和 `sticky`（`t`）位：代表该位的字母，否则为横杠（`-`）。如果任何一个位被设置，则包含此行。

（注：由于原文存在大量重复内容，此处已根据要求清理并保留核心信息）



# GETFACL

如果定义了环境变量 `POSIXLY_CORRECT`，`getfacl` 的默认行为将发生以下变化：除非另有指定，否则只打印 ACL。只有给出 `-d` 选项时才会打印默认 ACL。如果未给出命令行参数，`getfacl` 的行为将同于调用了 `getfacl -`。不会生成指示 `setuid`、`setgid` 和 `sticky` 位的标志注释。

## 作者

Andreas Gruenbacher, `<>`。

请向上述地址发送您的错误报告和注释。

## 参见

(1), (5)

***

# GETFATTR

## 名称

`getfattr` - 获取文件系统对象的扩展属性

## 语法

```text
getfattr [-hRLP] -n name [-e en] pathname...
getfattr [-hRLP] -d [-e en] [-m pattern] pathname...
```

## 描述

对于每个文件，`getfattr` 会显示文件名以及与该文件关联的扩展属性名称（以及可选的值）。

`getfattr -d` 的输出格式如下：

```text
1: # file: somedir/
2: user.name0="value0"
3: user.name1="value1"
4: user.name2="value2"
5: ...
```

第 1 行标识后续行报告的文件名。其余行（上述第 2 到 4 行）显示与指定文件关联的 `name` 和 `value` 对。

## 选项

`-n name`、`--name=name`

导出指定命名扩展属性的值。

`-d`、`--dump`

导出与 `pathname` 关联的所有扩展属性的值。

`-e en`、`--encoding=en`

在检索值后对其进行编码。`en` 的有效值为 `"text"`、`"hex"` 和 `"base64"`。以文本字符串编码的值用双引号（`"`）包围，而以十六进制和 base64 格式编码的字符串分别带有 `0x` 和 `0s` 前缀。

`-h`、`--no-dereference`

不解引用符号链接。与其符号链接指向的文件，而是检查符号链接本身。除非进行逻辑（`-L`）遍历，否则不遍历指向目录的符号链接。

`-m pattern`、`--match=pattern`

仅包含名称匹配正则表达式 `pattern` 的属性。`pattern` 的默认值为 `^user\\.`，它包含了用户命名空间中的所有属性。指定 `-` 以包含所有属性。关于命名空间的详细讨论，请参阅 (5)。

`--absolute-names`

不剥离开头的斜杠字符（`/`）。默认行为是剥离开头的斜杠字符。

`--only-values`

导出原始扩展属性值而不进行编码。

`-R`、`--recursive`

递归列出所有文件和目录的属性。

`-L`、`--logical`

逻辑遍历，跟随指向目录的符号链接。默认行为是在给出 `--no-dereference` 的情况下跟随符号链接参数，并跳过子目录中遇到的符号链接。仅在结合 `-R` 使用时有效。

`-P`、`--physical`

物理遍历，不跟随指向目录的符号链接。也会跳过符号链接参数。仅在结合 `-R` 使用时有效。

`--version`

打印 `getfattr` 的版本并退出。

`--help`

打印解释命令行选项的帮助信息。

`--`

命令行选项的结束。所有剩余参数都将被解释为文件名，即使它们以横杠开头。

## 作者

Andreas Gruenbacher, `<>` 和 SGI XFS 开发团队, `<>`。

请向这些地址发送您的错误报告或注释。

## 参见

(1) 和 (5)。

***

# GETHOSTIP

## 名称

`gethostip` --- 将 IP 地址转换为各种格式

## 语法

```text
gethostip [-dxnf] [HOSTNAME|IP]
```

## 描述

本手册页简要说明了 `gethostip` 命令。

`gethostip` 工具将给定的主机名或 IP 地址转换为多种格式。它由 syslinux 包提供，以便更容易地为 pxelinux 配置文件计算适当名称。这些文件名可以是给定 IP 地址的完整十六进制表示，也可以是匹配一组 IP 地址范围的局部十六进制表示。

## 选项

下方包含了选项的摘要。

`-d`

以十进制格式输出 IP 地址。

`-x`

以十六进制格式输出 IP 地址。

`-n`

输出主机的规范名称（canonical name）。

`-f`

完整输出。以所有支持的格式输出 IP 地址。等同于 `-xdn`。

## 参见

(1)

更多细节可以在 pxelinux 文档中找到，该文档位于 `Debian GNU/Linux` 系统的 `/usr/share/doc/syslinux/pxelinux.doc.gz`。

## 作者

本手册页由 dann frazier `<>` 为 `Debian GNU/Linux` 系统编译（但也供其他人使用）。

***

# GETOPT

## 名称

`getopt` - 解析命令行选项（增强版）

## 语法

```text
getopt optstring
getopt [options] [--] optstring
getopt [options] -o|--options optstring [--] parameters
```

## 描述

`getopt` 用于拆分（解析）命令行中的选项以便 shell 轻松解析，并检查合法选项。它使用 (3) 程来实现此功能。

调用 `getopt` 的参数可以分为两部分：修改 `getopt` 解析方式的选项（`options` 和 `optstring`），以及要解析的参数（`parameters`）。第二部分从第一个非选项开始，或者在第一个 `--` 之后。如果在第一部分没有找到 `-o` 或 `--options` 选项，则使用第二部分的参数作为选项字符串。

如果设置了环境变量 `GETOPT_COMPATIBLE`，或者第一个参数不是选项（不以 `-` 开头），`getopt` 将生成与其他版本 (1) 的输出。它仍然执行重排并识别可选参数（详见兼容性章节）。

传统的 (1) 实现无法处理参数和非选项参数中的空格和其他 shell 特有的特殊字符。为了解决这个问题，此实现可以生成引号输出，这些输出必须再次由 shell 解释（通常使用 `eval` 命令）。这具有保留那些字符的效果，但你必须以不再与其他版本兼容的方式调用 `getopt`（即语法中的第二种或第三种格式）。要确定是否安装了此增强版的 (1)，可以使用特殊的测试选项（`-T`）。

## 选项

`-a`、`--alternative`

允许长选项以单个 `-` 开头。

`-h`、`--help`

显示帮助文本并退出。不产生其他输出。

`-l`、`--longoptions longopts`

要识别的长（多字符）选项。可以通过逗号分隔名称来一次指定多个选项名称。此选项可以多次给出，`longopts` 是累积的。`longopts` 中的每个长选项名称后面可以跟一个冒号表示其有一个必需参数，或者跟两个冒号表示其有一个可选参数。

`-n`、`--name progname`

(3) 程在报告错误时使用的名称。注意，(1) 的错误仍被报告为来自 `getopt`。

`-o`、`--options shortopts`

要被识别的短（单字符）选项。如果未找到此选项，则 `getopt` 的第一个不以 `-` 开头（且不是选项参数）的参数将用作短选项字符串。`shortopts` 中的每个短选项字符后面可以跟一个冒号，表示它带有一个必需的参数；也可以跟两个冒号，表示它带有一个可选的参数。`shortopts` 的第一个字符可以是 `+` 或 `-`，以影响选项的解析方式和输出的生成（详情请参见 **SCANNING MODES** 章节）。

`-q`、`--quiet`

禁用 (3) 中的错误报告。

`-Q`、`--quiet-output`

不生成普通输出。错误仍由 (3) 报告，除非你同时也使用了 `-q`。

`-s`、`--shell shell`

将引用约定设置为 `shell` 的约定。如果没有给出 `-s` 选项，则使用 BASH 约定。目前有效的参数有 `sh`、`bash`、`csh` 和 `tcsh`。

`-T`、`--test`

测试你的 (1) 是此增强版本还是旧版本。这不会产生任何输出，并将错误状态设置为 4。其他 (1) 的实现，以及设置了环境变量 `GETOPT_COMPATIBLE` 的此版本，将返回 `--` 和错误状态 0。

`-u`、`--unquoted`

不对输出进行加引号。注意，空格和特殊（取决于 shell）字符在这种模式下可能会导致混乱（就像在其他 (1) 实现中一样）。

`-V`、`--version`

显示版本信息并退出。不生成其他输出。

## PARSING

本节指定了 `getopt` 参数中第二个部分的格式（即 **SYNOPSIS** 中的 `parameters`）。下一节（**OUTPUT**）描述了所生成的输出。这些参数通常是调用 shell 函数时传入的参数。必须确保调用 shell 函数时传入的每个参数与 `getopt` 参数列表中的某一个参数一一对应（参见 **EXAMPLES**）。所有的解析工作都由 GNU (3) 例程完成。

参数从左到右进行解析。每个参数被归类为短选项、长选项、选项的参数或非选项参数。

简单的短选项是一个 `-` 后面跟一个短选项字符。如果该选项有一个必需参数，可以直接写在选项字符之后，或者作为下一个参数（即在命令行上通过空格分隔）。如果该选项有一个可选参数，则如果存在，它必须直接写在选项字符之后。

可以在一个 `-` 之后指定多个短选项，只要所有选项（可能除最后一个外）都不具有必需或可选参数即可。

长选项通常以 `--` 开头，后跟长选项名称。如果该选项有一个必需参数，可以直接写在长选项名称之后并用 `=` 分隔，或者作为下一个参数（即在命令行上通过空格分隔）。如果该选项有一个可选参数，则如果存在，它必须直接写在长选项名称之后并用 `=` 分隔（如果你添加了 `=` 但后面什么都没有，它被解释为没有参数存在；这是一个轻小的 bug，参见 **BUGS**）。长选项可以缩写，只要缩写不产生歧义。

每个不以 `-` 开头且不是前一个选项的必需参数的参数都是非选项参数。`--` 参数之后的每个参数始终被解释为非选项参数。如果环境变量 `POSIXLY_CORRECT` 被设置，或者短选项字符串以 `+` 开头，则一旦发现第一个非选项参数（即不以 `-` 开头的参数），所有剩余参数都将被解释为非选项参数。

## OUTPUT

为前一节描述的每个元素生成输出。输出顺序与输入中指定的元素顺序相同，非选项参数除外。输出可以在兼容（未加引号，unquoted）模式下进行，也可以以保留参数和非选项参数内的空格和其他特殊字符的方式进行（参见 **QUOTING**）。当在 shell 脚本中处理输出时，它似乎由不同的元素组成，可以逐个处理（通过使用大多数 shell 语言中的 `shift` 命令）。这在未加引号模式下是不完美的，因为如果元素包含空格或特殊字符，可能会在意想不到的地方被拆分。

如果在解析参数时出现问题，例如未找到必需参数或未识别选项，将在 stderr 上报告错误，出错的元素将没有输出，并返回一个非零错误状态。

对于短选项，将一个单个 `-` 和选项字符生成为一个参数。如果该选项带有参数，则下一个参数将是该参数。如果选项带有可选参数但未找到，则将生成下一个参数，但在引用模式下为空，而在未加引号（兼容）模式下则不会生成第二个参数。注意许多其他 (1) 实现不支持可选参数。

如果在单个 `-` 之后指定了多个短选项，每个选项都将作为一个独立的参数出现在输出中。

对于长选项，`--` 和完整的选项名称被生成为一个参数。无论该选项在输入中是缩写的还是用单个 `-` 指定的都是如此。参数的处理方式与短选项相同。

通常，在所有选项及其参数生成之前，不会生成非选项参数输出。随后，生成 `--` 作为单个参数，其之后按照发现它们的顺序生成非选项参数，每个参数作为一个独立的参数。只有当短选项字符串的第一个字符为 `-` 时，才会在发现它们的地方生成非选项参数输出（如果使用的是 **SYNOPSIS** 的第一格式，则不支持；在这种情况下，所有之前出现的 `-` 和 `+` 都会被忽略）。

## QUOTING

在兼容模式下，参数或非选项参数中的空格或“特殊”字符无法被正确处理。当输出传递给 shell 脚本时，脚本不知道应该如何将输出拆分为不同的参数。为了解决这个问题，此实现提供了引用（quoting）功能。其思想是在生成输出时为每个参数加上引号。当此输出再次传递给 shell（通常通过 `eval` 命令）时，它会被正确拆分为不同的参数。

如果环境变量 `GETOPT_COMPATIBLE` 被设置、使用了 **SYNOPSIS** 的第一形式或发现了选项 `-u`，则不启用引用。

不同的 shell 使用不同的引用约定。你可以使用 `-s` 选项来选择你正在使用的 shell。目前支持以下 shell：`sh`、`bash`、`csh` 和 `tcsh`。实际上，只区分两种“风格”：sh 类的引用约定和 csh 类的引用约定。如果你使用另一种 shell 脚本语言，可能可以使用其中一种风格。

## SCANNING MODES

短选项字符串的第一个字符可以是 `-` 或 `+`，用于指示特殊的扫描模式。如果使用了 **SYNOPSIS** 中的第一个调用形式，它们将被忽略；尽管仍会检查环境变量 `POSIXLY_CORRECT`。

如果第一个字符是 `+`，或者环境变量 `POSIXLY_CORRECT` 被设置，则一旦发现第一个不是选项参数的非选项参数（即不以 `-` 开头的参数），解析就会停止。剩余参数都将被解释为非选项参数。

如果第一个字符是 `-`，则非选项参数将在它们出现的地方输出；在正常操作下，它们都会在生成 `--` 参数后被收集在输出的末尾。注意，此 `--` 参数仍然会被生成，但在这种模式下它始终是最后一个参数。

## 兼容性（COMPATIBILITY）

此版本的 (1) 编写时尽可能与其他版本兼容。通常，你可以直接用此版本替换它们，而无需进行任何修改，并且具有某些优势。

如果 `getopt` 第一个参数的第一个字符不是 `-`，`getopt` 将进入兼容模式。它将把第一个参数解释为短选项字符串，并解析所有其他参数。它仍然会进行参数重排（即所有非选项参数都输出在末尾），除非设置了环境变量 `POSIXLY_CORRECT`。

环境变量 `GETOPT_COMPATIBLE` 强制 `getopt` 进入兼容模式。同时设置此环境变量和 `POSIXLY_CORRECT` 可以为“困难”的程序提供 100% 的兼容性。但通常，这两者都不需要。

在兼容模式下，短选项字符串开头的 `-` 和 `+` 字符会被忽略。

## 返回码（RETURN CODES）

`getopt` 成功解析返回错误代码 `0`；如果 (3) 返回错误则返回 `1`；如果不理解自己的参数则返回 `2`；如果发生如内存不足等内部错误则返回 `3`；如果使用 `-T` 调用返回 `4`。

## 示例（EXAMPLES）

(1) 分发提供了 (ba)sh 和 (t)csh 的示例脚本，并可选安装在 `/usr/share/getopt/` 或 `/usr/share/doc/` 下的 util-linux 子目录下。

## 环境变量（ENVIRONMENT）

### POSIXLY_CORRECT

(3) 程会检查此环境变量。如果设置了它，一旦发现不是选项也不是选项参数的参数，解析将停止。所有剩余参数都被解释为非选项参数，无论它们是否以 `-` 开头。

### GETOPT_COMPATIBLE

强制 `getopt` 使用概要（SYNOPSIS）中指定的第一个调用格式。

## 缺陷（BUGS）

(3) 可以解析带有可选参数的长选项，该可选参数可以为空（但对短选项无法这样做）。此 (1) 将空的可选参数视为不存在。

如果你完全不想要任何短选项变量，这种语法并不直观（你必须显式地将它们设置为空字符串）。

## 作者（AUTHOR）

Frodo Looijaard

## 参见（SEE ALSO）

(3), (1), (1)。

## 可用性（AVAILABILITY）

`getopt` 命令是 util-linux 软件包的一部分，可从 Linux 内核存档获取。

***

# GETTEXT

## 名称（NAME）

`gettext` - 翻译消息

## 概要（SYNOPSIS）

```text
gettext [OPTION] [[TEXTDOMAIN] MSGID]
gettext [OPTION] -s [MSGID]...
```

## 描述（DESCRIPTION）

`gettext` 程序通过在消息目录查找查找，将自然语言消息翻译成用户的语言。

显示文本消息的本地语言翻译。

`-d`、`--domain=TEXTDOMAIN`

从 `TEXTDOMAIN` 获取翻译后的消息。

`-e`

启用某些转义序列的扩展。

`-E`

（为了兼容性被忽略。）

`-h`、`--help`

显示此帮助并退出。

`-n`

抑制末尾换行。

`-V`、`--version`

显示版本信息并退出。

`[TEXTDOMAIN] MSGID`

从 `TEXTDOMAIN` 获取与 `MSGID` 对应的翻译消息。

如果没有给出 `TEXTDOMAIN` 参数，则域将由环境变量 `TEXTDOMAIN` 确定。如果在常规目录下未找到消息目录，可以通过环境变量 `TEXTDOMAINDIR` 指定另一个位置。与 `-s` 选项配合使用时程序行为类似于 `echo` 命令。但它并不是简单地将参数复制到标准输出。相反，在所选目录中找到的消息将被翻译。标准搜索目录：`/usr/share/locale`

## 作者（AUTHOR）

由 Ulrich Drepper 编写。



# 报告缺陷 (REPORTING BUGS)

向`<>`报告缺陷。

# 版权 (COPYRIGHT)

版权所有 1995-1997, 2000-2007 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 版本 3 或更高版本`<https://www.gnu.org/licenses/gpl->`

这是自由软件：你可以自由地更改和重新发布它。在法律允许的范围内，不提供担保。

# 参见 (SEE ALSO)

`gettext`的完整文档作为 Texinfo 手册维护。如果你的站点正确安装了`info`和`gettext`程序，那么命令

`info gettext`

应该让你能够访问完整手册。

---

# GIT-ADD

## 名称 (NAME)

`git-add` - 将文件内容添加到索引

## 概要 (SYNOPSIS)

`git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p] [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]] [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--] [<pathspec>...]`

## 描述 (DESCRIPTION)

此命令使用工作树中找到的当前更新索引，为下一次提交准备暂存内容。它通常将现有路径的当前内容作为一个整体添加，但通过某些选项，它可以用于添加更改的一部分。

索引持有工作树内容的快照，通过某些选项，它可以用于添加更改的一部分。索引持有工作树内容的快照，并且该快照将作为下一次提交。`git status`命令可以用于获取哪些文件有更改的摘要。

索引持有工作树内容的快照，并且该快照将作为下一次提交。`git add`命令可以用于添加不存在或修改的文件。注意旧版本的 Git 会忽略删除的文件；使用`--no-all`选项来添加修改或新文件但忽略删除的文件。

`git add`命令默认不会添加忽略的文件。如果显式指定了忽略的文件，`git add`将带有忽略文件列表失败。通过目录递归或文件名通配执行（在 shell 前加上通配符）到达忽略的文件将被忽略。`git add`命令可以使用`-f`选项添加忽略的文件。

请参见 (1) 获取将内容添加到提交的替代方法。

## 选项 (OPTIONS)

`<pathspec>...`

要添加的文件。可以提供通配符（例如`*.c`）以添加所有匹配的文件。提供前导目录名（例如`dir`以添加`dir/file1`和`dir/file2`）可以更新索引以匹配目录的整体状态（例如指定`dir`将不仅记录在工作树中修改的`dir/file1`、添加到工作树的`dir/file2`，还记录从工作树中删除的`dir/file3`）。注意旧版本的 Git 会忽略删除的文件；使用`--no-all`选项来添加修改或新文件但忽略删除的文件。

`-n`, `--dry-run`

不实际添加文件，仅显示它们是否存在以及是否会被忽略。

`-v`, `--verbose`

详细输出。

`-f`, `--force`

允许添加其他忽略的文件。

`-i`, `--interactive`

交互地将工作树中的修改内容添加到索引。可以提供可选路径参数以限制操作到工作树的子集。详情请参见"交互模式"。

`-p`, `--patch`

交互地选择索引和工作树之间的补丁块并添加到索引。这让用户在将修改内容添加到索引之前有机会查看差异。

这实际上运行`add --interactive`，但跳过了初始命令菜单直接跳转到补丁子命令。详情请参见"交互模式"。

`-e`, `--edit`

在编辑器中打开与索引的差异并让用户编辑。在编辑器关闭后，调整块头并将补丁应用到索引。

此选项的目的是选择要应用的补丁行，或者甚至可以修改待暂存行的内容。这比使用交互式代码分块选择器（hunk selector）更快、更灵活。然而，这很容易混淆并创建一个无法应用于索引（index）的补丁。请参见下文的`EDITING PATCHES`。

### `-u`, `--update`

仅对已存在匹配`<pathspec>`条目的地方更新索引。这将删除或修改索引条目以匹配工作树，但不会添加新文件。

在使用`-u`选项时如果未给出`<pathspec>`，则将更新整个工作树中的所有跟踪文件（旧版本的 Git 会将更新限制在当前目录及其子目录）。

### `-A`, `--all`, `--no-ignore-removal`

不仅在工作树具有匹配`<pathspec>`的文件的地方更新索引，在索引已存在条目的地方也进行更新。这将添加、修改和删除索引条目以匹配工作树。

在使用`-A`选项时如果未给出`<pathspec>`，则更新整个工作树中的所有文件（旧版本的 Git 会将更新限制在当前目录及其子目录）。

### `--no-all`, `--ignore-removal`

通过添加索引未知的新文件和工作树中修改的文件来更新索引，但忽略已从工作树中删除的文件。当未使用`<pathspec>`时，此选项不起作用（no-op）。

此选项主要用于习惯旧版本 Git 的用户，在旧版本中，`git add <pathspec>...`是`git add --no-all <pathspec>...`的同义词，即忽略已删除的文件。

### `-N`, `--intent-to-add`

仅记录以后将添加该路径的事。在索引中放置该路径的条目但不包含内容。这通常用于通过`git diff`显示此类文件的未暂存内容，并通过`git commit -a`提交它们。

### `--refresh`

不添加文件，仅在索引中刷新它们的`stat()`信息。

### `--ignore-errors`

如果某些文件因为索引错误而无法添加，不要中止操作，而是继续添加其他文件。命令仍将以非零状态退出。可以将配置变量`add.ignoreErrors`设置为 true 以使其成为默认行为。

### `--ignore-missing`

此选项只能与`--dry-run`配合使用。通过使用此选项，用户可以检查给定文件是否会被忽略，无论它们是否已存在于工作树中。

### `--`

此选项用于将命令行选项与文件列表分开（当文件名可能误认为是命令行选项时有用）。

## 配置 (CONFIGURATION)

可选的配置变量`core.excludesFile`指向一个文件路径，该文件包含要从`git-add`中排除的文件名模式，类似于`$GIT_DIR/info/exclude`。排除文件中的模式将在`info/exclude`中的模式之外额外使用。参见 (5)。

## 示例 (EXAMPLES)

添加 `Documentation` 目录及其子目录下所有`*.txt`文件的内容：

```bash
git add Documentation/*.txt
```

注意，在此示例中星号`*`是从 shell 中加了引号；这允许命令包含`Documentation/`目录子目录下的文件。

考虑添加所有`git-*.sh`脚本的内容：

```bash
git add git-*.sh
```

由于此示例允许 shell 扩展星号（即你显式地列出了文件），因此它不会考虑`subdir/git-foo.sh`。

## 交互模式 (INTERACTIVE MODE)

当命令进入交互模式时，它会显示`status`子命令的输出，然后进入交互式命令循环。

命令循环显示可用的子命令列表，并给出提示`"What now> "`。通常，当提示以单个`*>`结束时，你可以从给出的选项中选择一个并回车，如下：

```text
*** Commands *** 1: status 2: update 3: revert 4: add untracked 5: patch 6: diff 7: quit 8: help What now> 1
```

只要选择是唯一的，你也可以在上面说 `s` 或 `sta` 或 `status`。

主命令循环有 6 个子命令（加上 `help` 和 `quit`）。

### `status`

这显示了每个路径`HEAD`与索引之间的差异（即如果你执行`git commit`将要提交的内容），以及索引与工作树文件之间的差异（即在执行`git commit`之前可以使用`git add`进一步暂存的内容）。示例输出如下所示：

```text
staged unstaged path 1: binary nothing foo.png 2: +403/-35 +1/-1 git-add--interactive.perl
```

它显示`foo.png`与`HEAD`有差异（但它是二进制文件，因此无法显示行数），并且索引副本与工作树版本之间没有差异（如果工作树版本也不同，将用`binary`替换`nothing`）。另一个文件`git-add--interactive.perl`如果提交索引中的内容将增加 403 行并删除 35 行，但工作树文件有进一步的修改（一次添加和一次删除）。

### `update`

这显示状态信息并发出`"Update>>"`提示。当提示以双`>>`结束时，你可以进行多个选择，并用空格或逗号连接。你也可以说范围。例如`"2-5 7,9"`选择 2,3,4,5,7,9。如果省略了范围中的第二个数字，则选取剩余所有项。例如`"7-"`选择 7 之后。选中的内容将被显示：

```text
staged unstaged path 1: binary nothing foo.png 2: +403/-35 +1/-1 git-add--interactive.perl
```

在决定了所有分块的命运后，如果有选中的分块，索引将用这些分块进行更新。要移除选择，可以在输入前加`-`，如下：

```text
Update>> -2
```

### `revert`

界面与`update`非常相似，暂存的信息将还原为`HEAD`。还原新路径使其变为未跟踪。

### `add untracked`

界面与`update`和`revert`非常相似，并让你将未跟踪路径添加到索引中。

### `patch`

这让你从`status`中选择一个路径。选择路径后，它会索引与工作树文件之间的差异，并询问你是否暂存每个分块的变化。你可以选择以下选项并回车：

```text
y - 暂存此分块
n - 不暂存此分块
q - 退出；不暂存此分块或任何后续分块
a - 暂存此分块及文件中后续的分块
d - 不暂存此分块或文件中后续的分块
g - 跳到一个分块
/ - 搜索匹配给定正则表达式的分块 j - 留此分块未决定，查看下一个未决定分块
J - 留此分块未决定，查看下一个分块
k - 留此分块未决定，查看上一个未决定分块
K - 留此分块未决定，查看上一个分块
s - 将当前分块拆分为更小的分块
e - 手动编辑当前分块
? - 打印帮助
```

通过将配置变量`interactive.singleKey`设置为 true，你可以省略此处的回车。

### `diff`

这让你查看将提交的内容（即`HEAD`与索引之间的内容）。

## 编辑补丁 (EDITING PATCHES)

调用`git add -e`或在交互式分块选择器中选择`e`会用编辑器打开补丁；编辑器退出后，结果将应用于索引。你可以自由对补丁进行任意更改，但请注意某些更改可能会产生混乱的结果，甚至导致补丁无法应用。如果你想完全中止操作（即在索引中不暂存任何新内容），只需删除补丁的所有行。下列表描述了补丁中可能看到的某些常见情况，以及对它们进行哪些编辑操作是合理的。

**添加的内容**

添加的内容由以"+"开头的行表示。你可以通过删除这些行来防止暂存任何添加行。

**移除的内容**

被删除的内容用以以"-"开头的行表示。你可以通过将`-`转换为`" "`（空格）来防止这些删除操作被加入暂存（staging）。

### 修改后的内容

修改的内容用`"-"`行（移除旧内容）后紧跟`"+"`行（添加替换内容）来表示。你可以通过将`"-"`行转换为`" "`并删除`"+"`行来防止将该修改加入暂存。请注意，仅修改配对中的半部分可能会给索引引入混乱的更改。

还可以执行一些更复杂的操作。但请注意，由于补丁（patch）仅应用于索引（index）而不应用于工作树（working tree），工作树看起来将会"撤销"索引中的更改。例如，在索引中引入了一行既不在`HEAD`中也不在工作树中的新行，会将该行加入暂存以进行提交，但该行在工作树中看起来又被还原了。

请避免使用这些结构，或者在使用时要极其谨慎。

### 移除未触动的内容

索引和工作树之间没有差异的内容可能会作为上下文行显示，以`" "`（空格）开头。你可以通过将空格转换为`"-"`来将上下文行加入暂存移除。结果工作树文件看起来将重新添加了这些内容。

### 修改现有内容

人们也可以通过将上下文行加入暂存移除（将`" "`转换为`"-"`）并添加一个带有新内容的`"+"`行来修改上下文行。同样，也可以对现有的添加或修改修改`"+"`行。在所有情况下，新的修改在工作树中看起来都将还原了。

### 新内容

你也可以添加补丁中不存在的新内容；只需添加每行以`"+"`开头的新行即可。该添加在工作树中看起来将是还原的。

还有几种操作应该完全避免的，因为它们会使补丁无法应用：

- 添加上下文（`" "`）或删除（`"-"`）行

- 删除上下文行或删除行

- 修改上下文或删除行的内容

---

# GIT-AM

## 名称 (NAME)

`git-am` - 从邮箱（mailbox）应用一系列补丁

## 概要用法说明 (SYNOPSIS)

```text
`git am` [--signoff] [--keep] [--[no-]keep-cr] [--[no-]utf8] [--3way] [--interactive] [--committer-date-is-author-date] [--ignore-date] [--ignore-space-change | --ignore-whitespace] [--whitespace=<option>] [-C<n>] [-p<n>] [--directory=<dir>] [--exclude=<path>] [--include=<path>] [--reject] [-q | --quiet] [--[no-]scissors] [-S[<keyid>]] [--patch-format=<format>] [(<mbox> | <Maildir>)...] `git am` (--continue | --skip | --abort)
```

## 描述 (DESCRIPTION)

将邮箱中的邮件消息拆分为提交日志消息、作者信息和补丁，并将它们应用于当前分支。

### 选项 (OPTIONS)

`<mbox>|<Maildir>)...`

要从中读取补丁的邮箱文件列表。如果你不提供此参数，命令将从标准输入读取。如果你提供了目录，它们将被视为 Maildir 。

- `-s, --signoff`

在提交消息中添加`Signed-off-by:`行，使用你自己的提交者身份。

- `-k, --keep`

将`-k`标记传递给`git mailinfo`（见 (1)）。

- `--keep-non-patch`

将`-b`标记传递给`git mailinfo`（见 (1)）。

- `--[no-]keep-cr`

使用`--keep-cr`时，带有相同的选项调用`git mailsplit`（见 (1)），以防止其去除行尾的 CR（回车符）。可以使用`am.keepcr`配置变量来指定默认行为。`--no-keep-cr`有助于覆盖`am.keepcr`。

- `-c, --scissors`

移除剪刀行（scissors line）之前之前的所有内容（见 (1)）。可以通过`mailinfo.scissors`配置变量默认激活。

- `--no-scissors`

忽略剪刀行（见 (1)）。

- `-m, --message-id`

将`-m`标记传递给`git mailinfo`（见 (1)），以便将 Message-ID 头部添加到提交消息中。可以使用`am.messageid`配置变量来指定默认行为。

- `--no-message-id`

不要向提交消息中添加 Message-ID 头部。`no-message-id`有助于覆盖`am.messageid`。

- `-q, --quiet`

保持安静。只打印错误信息。

- `-u, --utf8`

将`-u`标记传递给`git mailinfo`（见 (1)）。从电子邮件中提取的提交日志消息被重新编码为 UTF-8 编码（如果不是 UTF-8，可以使用配置变量`i18n.commitencoding`指定项目首选编码）。

这在之前的 git 版本中是可选的，但现在是默认。你可以使用`--no-utf8`来覆盖此。

- `--no-utf8`

将`-n`标记传递给`git mailinfo`（见 (1)）。

- `-3, --3way`

当补丁无法顺利应用时，如果补丁记录了它应该应用的 blob 标识，并且我们在本地拥有这些 blob，则回退到 3way 合并。

- `--ignore-space-change, --ignore-whitespace, --whitespace=<option>, -C<n>, -p<n>, --directory=<dir>, --exclude=<path>, --include=<path>, --reject`

这些标记被传递给`git apply`（见 (1)）。

- `--patch-format`

默认情况下命令将尝试检测补丁格式。此选项允许用户指定补丁（es）应该解释的格式。有效的格式有 mbox, stgit, hg。



- `-i, --interactive`

交互式运行。

- `--committer-date-is-author-date`

默认情况下命令记录邮件日期作为作者日期，并将创建时间作为提交者日期。这允许用户使用相同的值来覆盖提交者日期。

- `--ignore-date`

默认情况下命令记录邮件日期作为作者日期，并创建创建时间作为提交者日期。这允许用户使用相同的值来覆盖提交者日期。

- `--skip`

跳过当前补丁。这在重启中断的补丁时才有意义。

- `-S[<keyid>], --gpg-sign[=<keyid>]`

GPG 签名提交。

- `--continue, -r, --resolved`

补丁失败后（例如尝试应用冲突补丁），用户已手动应用，且索引文件存储了结果。使用从电子邮件中提取的作者信息和提交日志以及当前索引文件进行提交并继续。

- `--resolvemsg=<msg>`

当补丁失败时，`<msg>` 将打印到屏幕并退出。这覆盖了提示你使用 `--continue` 或 `--skip` 的标准消息。这仅供 `git rebase` 和 `git am` 之间的内部使用。

- `--abort`

恢复原始分支并中止补丁操作。

## 邮件格式

作者名称从消息的 `"From: "` 行获取，提交作者日期从消息的 `"Date: "` 行获取。`"Subject: "` 行被用作标题，在去掉常见前缀 `[PATCH <anything>]` 后。`"Subject: "` 行应该用一行文本简洁描述提交的内容。

正文开头的 `"From: "` 和 `"Subject: "` 行会覆盖从头部获取的相应提交作者名称和标题值。

提交消息由从 `"Subject: "` 获取的标题、一个空行以及到补丁开始之前的正文组成。每行末尾的多余空格会被自动删除。

补丁预计是内联的，紧接消息之后。任何形式如下的内容：

- 三个横杠和行尾；
- 以 `"diff -"` 开头的行；
- 以 `"Index: "` 开头的行。

都被视为补丁的开始，提交日志消息在首次此类行出现之前终止。

## 冲突处理

手动解决工作目录中的冲突，并更新索引文件，使其进入补丁应该产生的状态。然后带有 `--continue` 选项运行该命令。

该命令在当前操作完成之前将拒绝处理新的邮箱箱，因此，如果你决定从头开始，请在运行带有邮箱箱名称的命令之前运行 `git am --abort`。

在应用任何补丁之前，`ORIG_HEAD` 被设置为当前分支的顶端。如果你在多个提交时遇到问题，这非常有用，例如在错误的分支上运行了 `git am`，或者提交中的错误可以通过更改邮箱箱更容易修复（例如 `"From:"` 行中的错误）。

## 钩子（HOOKS）

此命令可以运行 `applypatch-msg`、`pre-applypatch` 和 `post-applypatch` 钩子。更多信息请参见 (5)。

# GIT-APPLY

## 名字

`git-apply` - 将补丁应用于文件和/或索引

## 概要

`git apply [--stat] [--numstat] [--summary] [--check] [--index] [--3way] [--apply] [--no-add] [--build-fake-ancestor=<file>] [-R | --reverse] [--allow-binary-replacement | --binary] [--reject] [-z] [-p<n>] [-C<n>] [--inaccurate-eof] [--recount] [--cached] [--ignore-space-change | --ignore-whitespace] [--whitespace=(nowarn|warn|fix|error|error-all)] [--exclude=<path>] [--include=<path>] [--directory=<root>] [--verbose] [--unsafe-paths] [<patch>...]`

## 描述

读取提供的 diff 输出（即“补丁”）并将其应用于文件。使用 `--index` 选项时，补丁也会应用于索引；使用 `--cached` 选项时补丁仅应用于索引。如果不使用这些选项，命令将仅补丁应用于文件，且不要求它们位于 Git 仓库中。

此命令应用补丁但不会创建提交。使用 (1) 从由 (1) 生成和或通过电子邮件接收的补丁创建提交。

### 选项

`<patch>...`

从中读取补丁的文件。`-` 可从标准输入读取。

`--stat`

不应用补丁，而是为输入输出 diffstat。关闭 `apply`。

`--numstat`

与 `--stat` 类似，但以十进制符号显示添加和删除的行数，以及不缩短的路径名，使其对机器友好。对于二进制文件，输出两个 `-`，而不是说 `0 0`。关闭 `apply`。

`--summary`

不应用补丁，而是输出从 git diff 扩展头中获取的压缩摘要，例如创建、重命名和模式更改。关闭 `apply`。

`--check`

不应用补丁，而是检查补丁是否适用于当前的工作树和/或索引文件，并检测错误。关闭 `apply`。

`--index`

当 `--check` 生效时，或者在应用补丁时（当没有任何禁用它的选项生效时，这是默认设置），请确保补丁适用于当前索引文件记录的内容。如果工作树中要应用补丁的文件不是最新的，则会被标记为错误。此标记也会导致索引文件被更新。

`--cached`

在不接触工作树的情况下应用补丁。相反，获取缓存数据，应用补丁并将结果存储在索引中，而不使用工作树。这意味着包含了 `--index`。

`-3, --3way`

当补丁无法整洁应用时，如果补丁记录了它应该应用的 blob 标识，且我们在本地拥有这些 blob，则回退到三路合并，并可能在工作树的文件中留下冲突标记供用户解决。此选项包含了 `--index` 选项，并且与 `--reject` 和 `--cached` 选项不兼容。

`--build-fake-ancestor=<file>`

较新的 `git diff` 输出为每个 blob 嵌入了 `index information` 以帮助识别补丁应用的原始版本。当给出此标志时，如果 blob 的原始版本本地可用，则构建一个包含这些 blob 的临时索引。

当遇到纯模式更改（其没有索引信息）时，将从当前索引中读取信息。

`-R, --reverse`

反向应用补丁。

`--reject`

为了原子性，当某些块（hunks）无法应用时，`git apply` 默认会失败整个补丁且不接触工作树。此选项使其应用补丁中可用的部分，并将被拒绝的块留存在对应的 `.rej` 文件中。

`-z`

当给出 `--numstat` 时，不要处理路径名，而是使用以 NUL 终止的机器读格式。

如果不使用此选项，每个输出的路径名的 TAB、LF、双引号和反斜杠字符分别替换为 `\t`、`\n`、`\"` 和 `\\`。如果发生了任何此类替换，路径名将被双引号包围。

`-p<n>`

从传统的 diff 路径中删除 `<n>` 个领先斜杠。默认是 1。

`-C<n>`

确保每个更改前后至少有 `<n>` 行周围上下文匹配。如果周围上下文行较少，则它们必须全部匹配。默认情况下不会忽略任何上下文。

`--unidiff-zero`

默认情况下，`git apply` 期望正在应用的补丁是具有至少一行上下文的统一差异（unified diff）。这提供了良好的安全措施，但在应用使用 `--unified=0` 生成的 diff 时失效。要绕过这些检查，使用 `--unidiff-zero`。

`--apply`

如果你使用任何标记为“关闭 `apply`”的选项，`git apply` 读取并输出所需的信息而不实际应用补丁。在这些标志后给出此标志以应用补丁。

`--no-add`

当应用补丁时，忽略补丁中的添加。这可以通过先对两个文件运行 diff 并使用此选项应用其结果来提取共同部分。

`--allow-binary-replacement, --binary`

过去我们在没有用户显式许可的情况下不允许二进制补丁，而此标志是这样做的方法。目前我们总是允许二进制补丁，因此这是一个空操作。

`--exclude=<path>`

不应用匹配给定路径的文件更改。这在导入补集时非常有用，你想排除某些文件或目录。

`--include=<path>`

应用匹配给定路径的文件更改。这在导入补集时非常有用，你想包含某些文件或目录。

当使用 `--exclude` 和 `--include` 模式时，按照它们在命令行出现的顺序进行检查，第一个匹配决定是否使用每个路径的补丁。如果命令行上没有包含模式，默认使用未匹配任何包含/排除模式的路径补丁；如果有则忽略。

`--ignore-space-change, --ignore-whitespace`

应用补丁时，必要时忽略上下文行的空格更改。上下文行将保留其空格，无论 `--whitespace` 选项的值如何，都不会进行空格修复。不过，新行仍然会被修复。

`--whitespace=<action>`

应用补丁时，检测具有空格错误的新行或修改行。什么是空格错误由 `core.whitespace` 配置控制。默认情况下，尾随空格（包括仅由空格组成的行）以及初始缩进内紧随制表符的空格字符被认为是空格错误。

默认情况下，命令输出警告消息但应用补丁。当 `git-apply` 用于统计且不应用补丁时，它默认为 `nowarn`。

你可以使用不同的 `<action>` 值来控制这种行为：

`nowarn` 关闭尾随空格警告。

`warn` 对少数此类错误输出警告，但按原样应用补丁（默认值）。

`fix` 针对少数此类错误输出警告，并在修复它们后应用补丁（`strip` 是一个同义词——该工具仅将末尾空白字符视为错误，修复方法涉及 `stripping`（剥离）它们，但现代 Git 会执行更多操作）。

`error` 针对少数此类错误输出错误信息，并拒绝应用补丁。

`error-all` 类似于 `error`，但会显示所有错误。

`--inaccurate-eof`

在某些情况下，某些版本的 `diff` 无法正确检测文件末尾缺少换行符。因此，由此类 `diff` 程序创建补丁无法正确记录不完整的行。此选项通过绕过此 bug 提供了应用此类补丁的支持。

`-v, --verbose`

向 `stderr` 报告进度。默认情况下，只会打印关于正在应用的当前补丁的消息。此选项将报告额外信息。

`--recount`

不要信任 hunk 头部（块头部）中的行数，而是通过检查补丁来推断它们（例如在编辑补丁后未相应调整 hunk 头部的情况下）。

`--directory=<root>`

在所有文件名前加上 `<root>`。如果也传递了 `-p` 参数，则会在加上新根目录之前应用它。

例如，一个关于更新 `a/git-gui.sh` 到 `b/git-gui.sh` 的补丁，可以通过运行 `git apply --directory=modules/git-gui` 应用到工作树中的文件 `modules/git-gui/git-gui.sh`。

`--unsafe-paths`

默认情况下，影响工作区之外（无论是 Git 控制的工作树，还是当使用 `git apply` 替换 GNU patch 的当前工作目录）的补丁会被视为错误（或恶意行为）。

当将 `git apply` 用作“更好的 GNU patch”时，用户可以传递 `--unsafe-paths` 选项来覆盖此安全检查。当使用 `--index` 或 `--cached` 时，此选项无效。

## 配置

`apply.ignoreWhitespace`

如果您希望默认忽略空白字符的变化，请将其设置为 `change`。如果您希望空白字符的变化具有重要性，请设置为 `no`、`none`、`never` 或 `false` 之一。

`apply.whitespace`

当命令行没有给出 `--whitespace` 标志时，将使用此配置项作为默认。

## 子模块

如果补丁包含对子模块的任何更改，`git apply` 将如下方式处理这些更改。

如果指定了 `--index`（显式或隐式），子模块提交必须与索引完全匹配才能应用补丁。如果任何子模块已检出（checked-out），则这些检出状态将被完全忽略，即它们不需要是最新的或整洁的，也不会被更新。

如果没有指定 `--index`，则补丁中的子模块提交将被忽略，仅检查相应的子目录是否存在并（在可能的情况下）进行更新。

---

# GIT-ARCHIVE

## 名称

`git-archive` - 为命名的树创建文件归档

## 语法

`git archive [--format=<fmt>] [--list] [--prefix=<prefix>/] [<extra>] [-o <file> | --output=<file>] [--worktree-attributes] [--remote=<repo> [--exec=<git-upload-archive>]] <tree-ish> [<path>...]`

## 描述

创建一个指定格式的归档，其中包含命名树的树结构，并将其写入标准输出。如果指定了 `<prefix>`，它将加在归档中文件名的前面。

`git archive` 在给定树 ID 与给定提交 ID 或标签 ID 时的行为不同。在第一种情况下，使用当前时间作为归档中每个文件的修改时间。在后一种情况下，使用在引用提交对象中记录的提交时间。此外，如果使用 tar 格式，提交 ID 将存储在全局扩展 pax 头部中；可以使用 `git get-tar-commit-id` 提取它。在 ZIP 文件中，它被存储为文件注释。

### 选项

`--format=<fmt>`

结果归档的格式：`tar` 或 `zip`。如果未给出此选项且指定了输出文件，则在可能的情况下从文件名推断格式（例如，写入 `"foo.zip"` 会使输出为 zip 格式）。否则，输出格式为 `tar`。

`-l, --list`

显示所有可用格式。

`-v, --verbose`

向 `stderr` 报告进度。

`--prefix=<prefix>/`

在归档中的每个文件名前加上 `<prefix>/`。

`-o <file>, --output=<file>`

将归档写入 `<file>` 而不是 `stdout`。

`--worktree-attributes`

同时在工作树的 `.gitattributes` 文件中查找属性（参见“ATTRIBUTES”部分）。

`<extra>`

这可以是归档后端理解的任何选项。详见下一节。

`--remote=<repo>`

不是从本地仓库创建 tar 归档，而是从远程仓库检索 tar 归档。注意远程仓库可能对 `<tree-ish>` 中允许的 `sha1` 表达式进行限制。详见 (1)。

`--exec=<git-upload-archive>`

配合 `--remote` 使用，指定远程侧 `git-upload-archive` 的路径。

`<tree-ish>`

产生归档的树或提交。

`<path>`

如果没有路径参数，当前工作目录的所有文件和子目录都包含在归档中。如果指定了一个或多个路径，则仅包含这些路径。

## 后端选项

### zip

`-0`

存储文件而不是压缩。

`-9`

最高且最慢的压缩级别。你可以指定 1 到 9 任何数字。

## 配置

`tar.umask`

此变量用于限制 tar 条目的权限。默认值为 `002`，这关闭了世界写权限。`user` 特值表示使用用户的 umask。详见 (2)。

`tar.<format>.command`

此变量指定通过 `git archive` 生成的 tar 输出的 shell 命令。通过标准输入执行命令并产生标准输出。`tar.gz` 和 `tgz` 格式会自动定义。可以使用自定义命令覆盖它们。

`tar.<format>.remote`

如果为 `true`，通过 (1) 为远程启用 `<format>`。对于用户定义的 `<format>` 默认为 `false`。

## 属性

`export-ignore`

具有 `export-ignore` 属性的文件和目录不会被添加到归档。详见 (5)。

`export-subst`

如果文件设置了 `export-subst` 属性，则 Git 在将此文件添加到归档时展开多个占位符。详见 (5)。

注意属性默认从树的 `.gitattributes` 文件获取。如果你想在之后调整生成方式（例如，在提交 `.gitattributes` 时没有添加相应的 `export-ignore`），请调整检出的 `.gitattributes` 文件并使用 `--worktree-attributes` 选项。或者，你可以在 `$GIT_DIR/info/attributes` 文件中保留归档时所需的属性。

## 示例

```bash
git archive --format=tar --prefix=junk/ HEAD | (cd /var/tmp/ && tar xf -)
```

创建一个包含当前分支最新提交内容的 tar 归档，并将其解压到 `/var/tmp/junk` 目录。

```bash
git archive --format=tar --prefix=git-1.4.0/ v1.4.0 | gzip >git-1.4.0.tar.gz
```

为 `v1.4.0` 创建压缩 tar 包。

```bash
git archive --format=tar.gz --prefix=git-1.4.0/ v1.4.0 >git-1.4.0.tar.gz
```

与上述相同，但使用内置的 tar.gz 处理。

```bash
git archive --prefix=git-1.4.0/ -o git-1.4.0.tar.gz v1.4.0
```

与上述相同，但格式从输出文件推断。

```bash
git archive --format=tar --prefix=git-1.4.0/ v1.4.0^{tree} | gzip >git-1.4.0.tar.gz
```



为 `v1.4.0` 发布创建一个压缩的 `tar` 包，但不包含全局扩展 `pax` 头部。

```bash
git archive --format=zip --prefix=git-docs/ HEAD:Documentation/ > git-1.4.0-docs.zip
```

将当前 `HEAD` 的 `Documentation/` 目录下的所有内容放入 `git-1.4.0-docs.zip` 中，并使用前缀 `git-docs/`。

```bash
git archive -o latest.zip HEAD
```

创建一个包含当前分支最新提交内容的 `Zip` 归档。注意，输出格式由输出文件的扩展名推断。

```bash
git config tar.tar.xz.command "xz -c"
```

配置 `tar.xz` 格式以创建经过 `LZMA` 压缩的 `tar` 文件。你可以通过指定 `--format=tar.xz` 或通过创建输出文件如 `-o foo.tar.xz` 来使用它。

***

# GIT-BISECT

## 名称

`git-bisect` - 通过二分查找引入 bug 的更改

## 语法

`git bisect <subcommand> <options>`

## 描述

该命令接受不同的子命令，根据子命令有不同的选项：

```bash
git bisect help
git bisect start [--no-checkout] [<bad> [<good>...]] [--] [<paths>...]
git bisect bad [<rev>]
git bisect good [<rev>...]
git bisect skip [(<rev>|<range>)...]
git bisect reset [<commit>]
git bisect visualize
git bisect replay <logfile>
git bisect log
git bisect run <cmd>...
```

该命令使用 `git rev-list --bisect` 来帮助驱动二分查找过程，在给定旧的“good”提交对象名称和较后的“bad”提交对象名称的情况下，找到哪个更改引入了 bug。

### 获取帮助

使用 `git bisect` 获取简短的用法说明，使用 `git bisect help` 或 `git bisect -h` 获取详细的用法说明。

### 基础二分命令：`start`、`bad`、`good`

以 Linux 内核树为例，`bisect` 命令的基本用法如下：

```bash
$ git bisect start
$ git bisect bad # 当前版本是坏的
$ git bisect good v2.6.13-rc2 # v2.6.13-rc2 是最后一个测试过的良好版本
```

当你指定了至少一个 bad 和一个 good 版本时，命令会对修订版本树进行二分，并输出类似下面的内容：

```text
Bisecting: 675 revisions left to test after this
```

然后会检出修订集中间的状态。你现在可以编译该内核并启动。如果启动的内核运行正常，你只需执行以下命令：

```bash
$ git bisect good # 这个是好的
```

该命令的输出类似于下面的内容：

```text
Bisecting: 337 revisions left to test after this
```

你不断重复这个过程：编译树、测试它，并根据是好是坏发布 `git bisect good` 或 `git bisect bad` 命令以请求下一次二分。

最终将不再有更多可二分的修订版本，你将在 `refs/bisect/bad` 中留下第一个坏的内核修订版本。

### `Bisect reset`（重置）

在二分会结束后，为了清理二分状态并返回原始的 `HEAD`（即退出二分），请执行以下命令：

```bash
$ git bisect reset
```

默认情况下，这会将你的树恢复到 `git bisect start` 之前检出的提交。（一个新的 `git bisect start` 也会这样做，因为它会清理旧的二分状态。）

可以通过可选参数返回不同的提交：

```bash
$ git bisect reset <commit>
```

例如，`git bisect reset HEAD` 将让你留在当前的二分提交上且完全不切换，而 `git bisect reset bisect/bad` 将检出第一个坏的修订版本。

### `Bisect visualize`（可视化）

要在 `gitk` 中查看当前剩余的怀疑对象，请在二分过程中执行以下命令：

```bash
$ git bisect visualize
```

`view` 也可以作为 `visualize` 的同义词。

如果没有设置 `DISPLAY` 环境变量，则将使用 `git log`。你也可以提供 `-p` 和 `--stat` 等命令行选项。

```bash
$ git bisect view --stat
```

### `Bisect log` 和 `bisect replay`（日志与重放）

在标记修订版本为 good 或 bad 后，执行以下命令显示到目前为止的操作：

```bash
$ git bisect log
```

如果你发现指定修订版本状态时犯了错误，可以将此命令的输出保存到文件中，编辑它移除错误的条目，然后执行以下命令返回更正的状态：

```bash
$ git bisect reset
$ git bisect replay that-file
```

### Avoiding testing a commit（避免测试某个提交）

如果在二分会话期间，你知道下一个建议的修订版本不是一个好的测试版本（例如，已知该提交引入的更改在你的环境中不起作用，且你知道它与你正在追踪的 bug 无关），你可能想要寻找一个附近的提交并尝试测试那个。

例如：

```bash
$ git bisect good/bad # 上一轮是好是坏。正在二分：337 revisions left to test after this
$ git bisect visualize # 哎，那个没意思。
$ git reset --hard HEAD~3 # 3 revisions before what suggested
```

然后编译并测试选定的版本，之后将该版本标记为 good 或 bad。

### `Bisect skip`（跳过）

与其自己选择一个附近的提交，不如通过执行命令让 Git 来完成：

```bash
$ git bisect skip # 当前版本无法测试
```

但如果你也想跳过一个提交范围而不仅仅是一个，使用 `<commit1>..<commit2>` 符号。例如：

```bash
$ git bisect skip v2.5..v2.6
```

这告诉二分过程 `v2.5` 到 `v2.6` 之间的提交应该被跳过。

### Cutting down bisection（缩小二分范围）

如果你知道树的哪个部分涉及正在追踪的问题，可以在执行 `bisect start` 时指定路径参数来进一步减少尝试次数：

```bash
$ git bisect start arch/i86 include/asm-i8
```

如果你提前知道多个 good 提交，可以在 bad 提交之后指定所有的 good 提交来缩小二分空间：

```bash
$ git bisect start v2.6.0-rc6 v2.6.0-rc4 v2.6.0-rc1 -- v2.6.0-rc6 is bad # rc-4 and rc1 are good
```

### `Bisect run`（运行）

如果你有一个可以判断当前源码是好是坏的脚本，可以通过执行以下命令进行二分：

```bash
$ git bisect run my_script arguments
```

注意，如果当前源码是好的，脚本应以代码 0 退出；如果当前源码是坏的，应以 1 到 127（包含）之间的代码退出，125 除外。

任何其他退出码将中止二分过程。应该注意到，通过 `exit(-1)` 终止的程序会留下 `$? = 255`（参见 (3) 手页），因为该值被与 `0377` 取模。特殊的退出码 125 用于当前源码无法测试的情况。如果脚本以此代码退出，当前修订版本将被跳过（参见上文的 `bisect skip`）。选择 125 作为此目的的最高合理值，是因为 126 和 127 被 POSIX Shell 用于表示特定的错误状态（127 表示未找到命令，126 表示找到命令但不可执行——对于“bisect run”而言，这些细节是脚本中的正常错误）。

你经常可能会发现在二分会话期间，希望对被测试的版本应用临时修改（例如，在头文件中将 `#define DEBUG 0` 修改为 `#define DEBUG 1`，或者“没有该提交的版本需要应用此补丁来绕过另一个二分不感兴趣的问题”）。

为了应对这种情况，在内部 `git bisect` 找到下一个要测试的版本后，脚本可以在编译前应用补丁，运行真实测试，然后判断该版本（可能包含所需的补丁）是否通过测试，最后将工作树回溯到原始状态。最后，脚本应以真实测试的状态退出，让 `git bisect run` 命令通过循环来确定二分会话的最终结果。

### 选项

#### `--no-checkout`

在二分过程的每次迭代中，不要检出新的工作树。相反，仅需更新一个名为 `BISECT_HEAD` 的特殊引用，使其指向应该测试的提交。

当你要在每一步中执行的测试不需要检出的工作树时，此选项可能很有用。

如果仓库是裸仓库（bare），则假设使用了 `--no-checkout`。

## 示例

在 `v1.2` 和 `HEAD` 之间对损坏的构建进行自动二分：

```bash
$ git bisect start HEAD v1.2 -- # HEAD 是错误的，v1.2 是正确的
$ git bisect run make # "make" 构建应用程序
$ git bisect reset # 退出二分会话
```

在 `origin` 和 `HEAD` 之间对测试失败进行自动二分：

```bash
$ git bisect start HEAD origin -- # HEAD 是错误的，origin 是正确的
$ git bisect run make test # "make test" 构建并测试
$ git bisect reset # 退出二分会话
```

对损坏的测试用例进行自动二分：

```bash
$ cat ~/test.sh
#!/bin/sh
make || exit 125 # 这跳过损坏的构建

~/check_test_case.sh # 测试用例通过了吗？

$ git bisect start HEAD HEAD~10 -- # 罪祸首在最后 10 个提交中
$ git bisect run ~/test.sh
$ git bisect reset # 退出二分会话
```

在这里我们使用了自定义脚本 `test.sh`。在脚本中，如果 `make` 失败，我们将跳过当前提交。如果测试用例通过，`check_test_case.sh` 应该 `exit 0`，否则 `exit 1`。

如果 `test.sh` 和 `check_test_case.sh` 都在仓库之外，会更安全，以防止二分、`make`、测试进程与脚本之间的相互作用。

使用临时修改（热修复）进行自动二分：

```bash
$ cat ~/test.sh
#!/bin/sh

# 通过合并热修复分支来调整工作树
# 然后尝试进行构建，如果 git merge --no-commit hot-fix && make
then
    # 运行项目特定的测试并报告其状态
    ~/check_test_case.sh
    status=$?
else
    # 告诉调用者此状态不可测试
    status=125
fi

# 撤销修改以允许干净地切换到下一个提交
git reset --hard

# 返回控制权
exit $status
```

这在每次测试运行之前应用来自热修复分支的修改，例如，如果你的构建或测试环境发生了变化，旧版本可能需要修复，而新版本已经修复了。（确保热修复分支基于你正在二分的所有版本中所包含的提交，这样合并时就不会引入过多的内容，或者使用 `git cherry-pick` 代替 `git merge`。）

对损坏的测试用例进行自动二分：

```bash
$ git bisect start HEAD HEAD~10 -- # 罪祸首在最后 10 个提交中
$ git bisect run sh -c "make || exit 125; ~/check_test_case.sh"
$ git bisect reset # 退出二分会话
```

这表明如果你在单行中编写测试，可以不需要运行脚本。

在损坏的仓库中定位对象图中良好的区域：

```bash
$ git bisect start HEAD <known-good-commit> [ <boundary-commit> ... ] --no-checkout

$ git bisect run sh -c '
    GOOD=$(git for-each-ref "--format=%(objectname)" refs/bisect/good-*) &&
    git rev-list --objects BISECT_HEAD --not $GOOD >tmp.$$ &&
    git pack-objects --stdout >/dev/null <tmp.$$
    rc=$?
    rm -f tmp.$$
    test $rc = 0
'

$ git bisect reset # 退出二分会话
```

在这种情况下，当 `git bisect run` 完成时，`bisect/bad` 将指向一个至少有一个父提交的提交，该提交的可达图在 `git pack objects` 所要求的范围内是完全可遍历的。

## 参见

使用 `git bisect` 对抗回归 `m[][1]`，(1)。

## 注意事项

1. 使用 `git bisect` 对抗回归

***

# GIT-BRANCH

## 名称

`git-branch` - 列出、创建或删除分支

## 语法

```text
git branch [--color[=<when>] | --no-color] [-r | -a] [--list]
    [-v [--abbrev=<length> | --no-abbrev]]
    [--column[=<options>] | --no-column]
    [(--merged | --no-merged | --contains) [<commit>]]
    [--] [<pattern>...]

git branch [--set-upstream | --track | --no-track] [-l] [-f]
    <branchname> [<start-point>]

git branch (--set-upstream-to=<upstream> | -u <upstream>)
    [<branchname>]

git branch --unset-upstream [<branchname>]

git branch (-m | -M) [<oldbranch>] <newbranch>

git branch (-d | -D) [-r] <branchname>...

git branch --edit-description [<branchname>]
```

## 描述

如果给了 `--list`，或者如果没有参数，则列出现有分支；当前分支将用星号标记。使用 `-r` 显示远程跟踪分支。如果给了 `<pattern>`，它将作为通配符限制输出的分支。

命令的第二种形式创建一个名为 `<branchname>` 的新分支，它指向 `HEAD`，或者指向 `<start-point>`。注意这将创建新分支，但不会切换工作树；使用 `git checkout <newbranch>` 来切换到新分支。

当从跟踪分支启动本地分支时，Git 会设置分支（特别是 `branch.<name>.remote` 和 `branch.<name>.merge` 配置），以便 `git pull` 能够相应合并跟踪分支。此行为可以通过全局配置 `branch.autoSetupMerge` 修改。使用 `--track` 和 `--no-track` 选项可以覆盖该设置，并在之后通过 `git branch --set-upstream` 修改。

带有 `-m` 或 `-M` 选项，将重命名 `<oldbranch>`。如果 `<oldbranch>` 有对应的 reflog，将被重命名以匹配 `<newbranch>`，并创建一个 reflog 条目记录分支重命名。如果 `<newbranch>` 已存在，必须使用 `-M` 来强制重命名。

带有 `-d` 或 `-D` 选项，将删除 `<branchname>`。你可以指定多个分支进行删除。如果该分支当前有 reflog，则 reflog 也将被删除。

将 `-r` 与 `-d` 配合使用以删除远程跟踪分支。注意，只有当它们在远程仓库不存在或 `git fetch` 配置为不再获取它们时，删除远程跟踪分支才有意义。参见 (1) 中的 `prune` 子命令以清理所有过时的远程跟踪分支。

### 选项

#### `-d`、`--delete`

删除分支。分支必须在其上游分支中完全合并，或者如果没有通过 `--track` 设置上游，则必须在 `HEAD` 中合并。

#### `-D`

`--delete --force` 的快捷方式。

#### `-l`、`--create-reflog`

创建分支的 reflog。这将激活对分支 ref 的所有更改记录，允许使用基于日期的 SHA-1 表达式如 `<branchname>@{yesterday}`。注意在非裸仓库中，reflog 通常通过 `coreconfig` 配置选项默认启用。

# 概述



如果`<branchname>`存在，则将其重置为`<startpoint>`。如果不使用`-f`，`git branch`将拒绝更改现有分支。与`-d`（或`--delete`）结合使用，无论分支是否合并都允许删除。与`-m`（或`--move`）结合使用，即使新分支名称已存在也可以重命名分支。

- `-m, --move`

  移动/重命名分支以及对应的 reflog。

- `-M`

  `--move --force`的快捷方式。

- `--color[=<when>]`

  为分支着色以突出当前分支、本地和远程跟踪分支。值必须为`always`（默认）、`never`或`auto`。

- `--no-color`

  关闭分支颜色，即使配置文件默认开启了颜色输出。等同于`--color=never`。

- `--column[=<options>], --no-column`

  以列的形式显示分支列表。选项语法参见配置变量`column.branch`。不带选项的`--column`和`--no-column`分别等于`always`和`never`。

  此选项仅适用于非详细模式。

- `-r, --remotes`

  列出或删除（如果与`-d`使用）远程跟踪分支。

- `-a, --all`

  列出远程跟踪分支和本地分支。

- `--list`

  激活列表模式。`git branch <pattern>`会尝试创建一个分支，使用`git branch --list <pattern>`来列出匹配的分支。

- `-v, -vv, --verbose`

  在列表模式下，显示每个头节点的 sha1 和提交主题行，以及与上游分支的关系（如果有）。如果给出两次，则也打印上游分支名称（参见`git remote show <remote>`）。

- `-q, --quiet`

  在创建或删除分支时保持更静默，抑制非错误消息。

- `--abbrev=<length>`

  更改输出列表中 sha1 的最小显示长度。默认值为 7，可以通过`core.abbrev`配置选项覆盖。

- `--no-abbrev`（注：原文为`--no-abbrev`）

  在输出列表中显示完整的 sha1，而不是进行缩写。

- `-t, --track`

  在创建新分支时，设置`branch.<name>.remote`和`branch.<name>.merge`配置项，将起始分支标记为新分支的“上游”。此配置将告诉 git 在`git status`和`git branch -v`中显示这两个分支之间的关系。此外，它还指导在检出新分支时，带参数的`git pull`从上游拉取。

  当起始点是远程跟踪分支时，这是默认行为。如果你希望`git checkout`和`git branch`的行为始终像给了`--no-track`一样，请将`branch.autoSetupMerge`配置变量设置为 false。如果你希望当起始点是本地或远程跟踪分支时具有此行为，请将其设置为 always。

- `--no-track`

  不设置“上游”配置，即使`branch.autoSetupMerge`配置变量为 true。

- `--set-upstream`

  如果指定的分支不存在或已给出`--force`，则行为与`--track`完全相同。否则，在创建分支时会设置类似于`--track`样的配置，但不会更改分支所指向的地方。

- `-u <upstream>, --set-upstream-to=<upstream>`

  设置`<branchname>`的跟踪信息，使`<upstream>`视为`<branchname>`的上游分支。如果没有指定`<branchname>`，则默认为当前分支。

- `--unset-upstream`

  移除`<branchname>`的上游信息。如果没有指定分支，则默认为当前分支。

- `--edit-description`

  打开编辑器并编辑说明分支用途的文本，供其他其他命令（例如`request-pull`）。

- `--contains [<commit>]`

  仅列出包含指定提交的分支（未指定则为 HEAD）。隐含`--list`。

- `--merged [<commit>]`

  仅列出 tip 从指定提交可达的分支（未指定则为 HEAD）。隐含`--list`。

- `--no-merged [<commit>]`

  仅列出 tip 从指定提交不可达的分支（未指定则为 HEAD）。隐含`--list`。

- `<branchname>`

  要创建或删除的分支名称。新分支名称必须通过由 (1) 定义的所有检查。其中某些检查可能会限制分支名称中允许的字符。

- `<start-point>`

  新分支的头将指向此提交。它可以作为分支名称、提交 ID 或标签给出。如果省略此选项，将使用当前的 HEAD。

- `<oldbranch>`

  要重命的现有分支名称。

- `<newbranch>`

  现有分支的新名称。适用与`<branchname>`相同的限制。

## 示例

### 从已知标签开始开发

```bash
$ git clone my2.6
$ cd my2.6
$ git branch my2.6.14 v2.6.14
$ git checkout my2.6.14
```

1. 这一步和下一步可以通过`checkout -b my2.6.14 v2.6.14`合并为单个步骤。

### 删除不需要的分支

```bash
$ git clone my.git
$ cd my.git
$ git branch -d -r origin/todo origin/html origin/man
$ git branch -D test
```

1. 删除远程跟踪分支`todo`、`html`和`man`。下次 fetch 或 pull 将再次创建它们，除非你配置了不创建。

2. 删除`test`分支，即使`master`分支（或当前检出的分支）。

## 注意事项

如果你正在创建一个想要立即检出的分支，使用 checkout 命令并配合其`-b`选项创建分支会更简单。

`--contains`、`--merged`和`--no-merged`选项具有相关但不同的用途：

- `--contains <commit>`用于找到所有如果`<commit>`被变基或修改时将需要特别处理的分支。

- `--merged`用于找到所有可以安全删除的分支，因为这些分支被 HEAD 完全包含。

- `--no-merged`用于找到可以合并到 HEAD 的候选分支，因为这些分支没有被 HEAD 完全包含。

将包中的对象传递给`git index-pack`以存储在仓库中，然后打印所有定义引用的名称。如果给出了引用列表，则只打印与列表中匹配的引用。此命令是一个底层的管道命令（plumbing），旨在仅供`git fetch`调用。

`<git-rev-list-args>`

一组`git rev-parse`和`git rev-list`可接受的参数列表（包含一个具名的引用，参见下文“指定引用”部分），用于指定要传输的特定对象和引用。例如，`master~10..master`会导致当前的`master`引用连同其第 10 代祖先提交以来添加的所有对象一起打包。可以打包的引用和对象数量没有显式限制。

`[<refname>...]`

一个引用列表，用于限制报告为可用的引用。这主要对`git fetch`有用，它期望只接收请求的引用，而不一定是 pack 包中的所有内容（在这种情况下，`git bundle`的作用类似于`git fetch-pack`）。

## 指定引用

`git bundle`只打包由`git show-ref`显示的引用：这包括头部（heads）、标签（tags）和远程头部（remote heads）。如`master~1`等引用无法被打包，但非常适合定义基准（basis）。可以打包多个引用，也可以指定多个基准。打包的对象是不包含在给定基准集中的对象。每个基准可以显式指定（例如`^master~10`），也可以隐式指定（例如`master~10..master`、`--since=10.days.ago master`）。

所使用的基准由目标端持有，这一点非常重要。采取保守态度，导致 bundle 文件包含目标端已有的对象是可以的，因为这些对象在目标端解包时会被忽略。

## 示例

假设你想将历史从机器 A 上的仓库 R1 传输到机器 B 上的另一个仓库 R2。由于某种原因，A 和 B 之间不允许直接连接，但我们可以通过某种机制（光盘、电子邮件等）将数据从 A 移动到 B。我们希望根据 R1 中`master`分支的开发内容来更新 R2。

为了启动该过程，你可以先创建一个没有任何基准的包。你可以使用标签来记录上次处理到哪个提交，以便以后用增量包更新另一个仓库：

```bash
machineA$ cd R1
machineA$ git bundle create file.bundle master
machineA$ git tag -f lastR2bundle master
```

然后你将`file.bundle`传输到目标机器 B。因为这个包不需要提取任何现有的对象，你可以通过克隆它在机器 B 上创建一个新仓库：

```bash
machineB$ git clone -b master /home/me/tmp/file.bundle R2
```

这将在生成的仓库中定义一个名为`origin`的远程，允许你从包中 fetch 和 pull。R2 中的`$GIT_DIR/config`文件将会有如下条目：

```ini
[remote "origin"]
    url = /home/me/tmp/file.bundle
    fetch = refs/heads/*:refs/remotes/origin/*
```

要更新生成的 mine.git 仓库，可以在将存储`/home/me/tmp/file.bundle`的包替换为增量更新后，执行 fetch 或 pull。

在原始仓库中继续工作一段时间后，你可以创建一个增量包来更新另一个仓库：

```bash
machineA$ cd R1
machineA$ git bundle create file.bundle lastR2bundle..master
machineA$ git tag -f lastR2bundle master
```

然后你将包传输到另一台机器并替换`/home/me/tmp/file.bundle`，然后进行 pull。

```bash
machineB$ cd R2
machineB$ git pull
```

如果你知道预期接收仓库应该拥有哪些提交所需的对象，你可以利用这一知识来指定基准，提供一个截止点来限制进入生成包的修订和对象。上一个示例使用了`lastR2bundle`标签来实现此目的，但可以使用任何其他提供给 (1) 命令的选项。这里是更多示例：

你可以使用在两者中都存在的标签：

```bash
$ git bundle create mybundle v1.0.0..master
```

你可以使用基于时间的基准：

```bash
$ git bundle create mybundle --since=10.days master
```

你可以使用提交数：

```bash
$ git bundle create mybundle -10 master
```

你可以运行`git-bundle verify`来检查是否可以从带有基准创建的包中提取内容：

```bash
$ git bundle verify mybundle
```

这将列出你为了从包中提取而必须拥有的提交，如果没有这些提交则会报错。

从接收仓库的角度来看，一个包就像一个它对其进行 fetch 或 pull 的普通仓库。例如，你可以在 fetch 时映射引用：

```bash
$ git fetch mybundle master:localRef
```

你还可以查看它提供了哪些引用：

```bash
$ git ls-remote mybundle
```

***

# GIT-CAT-FILE

## 名称

`git-cat-file` - 为仓库对象提供内容或类型及大小信息

## 概要

```text
git cat-file (-t [--allow-unknown-type] | -s [--allow-unknown-type] | -e | -p | <type> | --textconv) <object>

git cat-file (--batch | --batch-check) [--follow-symlinks] <list-of-objects>
```

## 描述

在第一种形式下，命令提供仓库对象的内容或类型（除非使用了`-t`或`-p`或`--textconv`）。在第二种形式下，从标准输入提供由换行符分隔的对象列表，并打印每个对象的 SHA-1、类型和大小。

## 参数

`<object>`

要显示的对象名称。有关更完整的对象命名列表，请参见“指定引用”章节。

`-t`

不显示内容，显示由`<object>`指定的对象类型。

`-s`

不显示内容，显示由`<object>`指定的大小。

`-e`

抑制所有输出；如果`<object>`存在且有效对象则以零状态退出。

`-p`

格式打印`<object>`内容。

`<type>`

通常匹配`<object>`的真实类型，但也可以请求可以从给定`<object>`解析的类型。例如，请求一个包含它的提交对象的“tree”，或者请求一个指向它的标签对象的“blob”。

`--textconv`

通过 textconv 过滤器转换显示内容。在这种情况下，`<object>`格式为`<tree-ish>:<path>`或`:<path>`，以便对索引中的`<path>`内容应用过滤器。

`--batch`, `--batch=<format>`

为标准输入提供的每个对象打印信息和内容。不能与其他任何选项或参数结合。详见下文“批量输出”。

`--batch-check`, `--batch-check=<format>`

为标准输入提供的每个对象打印信息。不能与其他任何选项或参数结合。详见下文“批量输出”。

`--allow-unknown-type`

允许`-s`或`-t`查询类型未知/损坏的对象。

`--follow-symlinks`

在使用`--batch`或`--batch-check`时，当请求格式为`tree-ish:path-in-tree`的扩展 SHA-1 表达式时遵循仓库内部链接。与其提供链接本身的输出，不如提供链接对象的输出。如果链接指向树外部（例如指向`/foo`或根目录下的`../foo`），链接中树外部的部分将被打印。

该选项目前在指定索引中的对象（例如`:link`而不是`HEAD:link`）而非树中的对象时无法正常工作。

该选项目前无法在未使用`--batch`或`--batch-check`时使用。

例如，考虑一个包含内容的 git 仓库：

- `f`：一个包含`"hello\n"`的文件
- `link`：指向`f`的符号链接
- `dir/link`：指向`../f`的符号链接
- `plink`：指向`../f`的符号链接
- `alink`：指向`/etc/passwd`的符号链接

对于普通文件`f`，`echo HEAD:f | git cat-file --batch`将打印：

```text
ce013625030ba8dba906f756967f9e9ca394464a blob 6
```

执行`echo HEAD:link | git cat-file --batch --follow-symlinks`会打印出相同的内容，`HEAD:dir/link`也是如此，因为它们都指向`HEAD:f`。

如果不使用`--follow-symlinks`，这些命令将打印关于符号链接本身的数据。在`HEAD:link`的情况下，你会看到：

```text
4d1ae35ba2c8ec712fa2a379db44ad639ca277bd blob 1
```

`plink`和`alink`都指向树之外，因此它们会分别打印：

```text
symlink 4 ../f
symlink 11 /etc/passwd
```

## 输出

如果指定了`-t`，则输出`<type>`之一。

如果指定了`-s`，则输出`<object>`的大小（字节）。

如果指定了`-e`，则无输出。

如果指定了`-p`，则对`<object>`的内容进行格式化打印。

如果指定了`<type>`，则返回`<object>`的原始（尽管未压缩）内容。

## 批量输出

如果给出了`--batch`或`--batch-check`，`cat-file`将从`stdin`读取对象（每行一个），并打印它们的相关信息。默认情况下，整行被视为一个对象，就像输入到`(1)`一样。

你可以通过自定义的`<format>`来指定每个对象显示的信息。`<format>`会原样复制到`stdout`，其中形式如`%(atom)`的占位符会被展开，随后是一个换行符。可用的原子项有：

`objectname`

对象的 40 位十六进制名称。

`objecttype`

对象的类型（与`cat-file -t`报告相同）。

`objectsize`

对象的大小（字节）（与`cat-file -s`报告相同）。

`objectsize:disk`

对象在磁盘上占用的空间（字节）。请参见下文 CAVEATS 部分中关于磁盘大小的说明。

`deltabase`

如果对象在磁盘上以增量（delta）形式存储，则此展开为增量基础对象的 40 位十六进制 sha1。否则，展开为空 sha1（40 个零）。请参见下文 CAVEATS。

`rest`



如果在输出字符串中使用此原子项，输入行将在第一个空白边界处拆分。该空白之前的所有字符被视为对象名称；该连续空白之后的所有字符（即行的“剩余”部分）将替换 `%(rest)` 原子项输出。

如果未指定格式，默认格式为 `%(objectname) %(objecttype) %(objectsize)`。

如果指定了 `--batch`，对象信息后将跟随对象内容（由 `%(objectsize)` 字节组成），随后是一个换行符。

例如，不带自定义格式的 `--batch` 会产生：

`<sha1> SP <type> SP <size> LF <contents> LF`

而 `--batch-check='%(objectname) %(objecttype)'` 会产生：

`<sha1> SP <type> LF`

如果在 `stdin` 上指定的名称无法解析为仓库中的对象，则 `cat-file` 将忽略任何自定义格式并打印：

`<object> SP missing LF`

如果使用了 `--follow-symlinks`，且仓库中的符号链接指向仓库外部，则 `cat-file` 将忽略任何自定义格式并打印：

`symlink SP <size> LF <symlink> LF`

符号链接将是绝对路径（以 `/` 开头），或者是相对于树根的。例如，如果 `dir/link` 指向 `../../foo`，那么 `<symlink>` 将是 `../foo`。`<size>` 是符号链接的大小（字节）。

如果使用了 `--follow-symlinks`，将显示以下错误信息：

`<object> SP missing LF`

当请求的符号链接不存在时打印。

`dangling SP <size> LF <object> LF`

当初始符号链接存在，但其（或其链）指向的对象不存在时打印。

`loop SP <size> LF <object> LF`

用于符号链接循环（或任何需要超过 40 次解析的符号链接）。

`notdir SP <size> LF <object> LF`

在解析符号链接过程中，将文件用作目录名时打印。

## 注意事项

注意，磁盘上对象的大小报告是准确的，但在得出关于哪些引用（refs）或对象导致了磁盘占用的结论时应小心。打包后的非增量对象的大小可能比对其进行增量的对象大得多，但选择哪个对象作为基础、哪一个作为增量是任意的，并且在重打包（repack）期间可能会发生。

同样注意，对象数据库中可能存在对象的多个副本；在这种情况下，报告哪个副本的大小或增量基础是未定义的。

***

# GIT-CHECK-ATTR

## 名称

`git-check-attr` - 显示 `gitattributes` 信息

## 语法概要

`git check-attr [-a | --all | attr...] [--] pathname...`

`git check-attr --stdin [-z] [-a | --all | attr...] < <list-of-paths>`

## 描述

对于每个路径，此命令将列出该路径上的每个属性是 unspecified（未指定）、set（已设置）还是 unset（未设置）。

### 选项

- `-a, --all`：列出所有属性。如果使用此选项，将不包含 unspecified 属性。
- `--cached`：考虑索引，忽略工作树。
- `--stdin`：从标准输入读取文件名而非从命令行。
- `-z`：输出格式修改为机器可解析。如果给了 `--stdin`，输入路径用 NUL 字符分隔。
- `--`：将之前的所有参数视为属性，将之后的所有参数视为路径。

## 输出

输出格式为 `<path> SP <attribute> SP <info>`，除非生效 `-z`，此时使用 NUL 作为分隔符：`<path>` 是文件路径，`<attribute>` 是查询的属性，`<info>` 可以：

- `unspecified`：属性对该路径未定义。
- `unset`：属性定义为 false。
- `set`：属性定义为 true。
- `<value>`：为该属性分配了值。

## 示例

在示例中，使用了以下 `.gitattributes` 文件：

`*.java diff=java`

`!myAttr README caveat=unspecified`

列出单个属性：

`$ git check-attr diff org/example/MyClass.java`

`org/example/MyClass.java: diff: java`

为文件列出多个属性：

`$ git check-attr crlf myAttr org/example/MyClass.java`

`org/example/MyClass.java: crlf: unset`

`org/example/MyClass.java: diff: java`

为文件列出所有属性：

`$ git check-attr --all -- org/example/MyClass.java`

`org/example/MyClass.java: crlf: unset`

`org/example/MyClass.java: diff: java`

`org/example/MyClass.java: myAttr: set`

为多个文件列出属性：

`$ git check-attr myAttr -- org/example/MyClass.java org/example/NoMyAttr.java`

`org/example/MyClass.java: myAttr: set`

`org/example/NoMyAttr.java: myAttr: unspecified`

并不是所有的值都同样明确：

`$ git check-attr caveat README`

`README: caveat: unspecified`

输出格式已修改为机器可解析（见下文）。如果同时提供了 `--stdin`，输入路径之间将用 NUL 字符而非换行符分隔。

### `-n, --non-matching`

显示不匹配任何模式的给定路径。这仅在启用 `--verbose` 时才有意义，否则将无法区分匹配模式的路径和不匹配模式的路径。

### `--no-index`

在执行检查时不查找索引。这可以用于调试为什么某个路径被例如通过 `git add .` 跟踪，并且没有按照用户预期地被规则忽略，或者在开发包含否定匹配的模式时，用于匹配之前已通过 `git add -f` 添加的路径。

## 输出

默认情况下，任何匹配忽略模式的给定路径都将被输出，每行一个。如果没有模式匹配给定的路径，则该路径将不会输出任何内容；这意味着该路径将不会被忽略。

如果指定了 `--verbose`，输出将是一系列格式如下的内容：

`<source> <COLON> <linenum> <COLON> <pattern> <HT> <pathname>`

`<pathname>` 是被查询的文件路径，`<pattern>` 是匹配模式，`<source>` 是模式的源文件，`<linenum>` 是模式在该源文件中的行号。如果模式包含 `!` 前缀或 `/` 后缀，它们将在输出中保留。当引用由 `core.excludesFile` 配置的文件时，`<source>` 为绝对路径；当引用 `.git/info/exclude` 或按目录排除的文件时，为相对于仓库根目录的路径。

如果指定了 `-z`，输出中的路径由空字符分隔；如果同时指定了 `--verbose`，则也使用空字符代替冒号和制表符（tab）：

`<source> <NULL> <linenum> <NULL> <pattern> <NULL> <pathname> <NULL>`

如果指定了 `-n` 或 `--non-matching`，也将输出不匹配的路径，在这种情况下，每个输出记录中除 `<pathname>` 之外的所有字段都将为空。这在运行非交互式运行时非常有用，以便文件可以增量地流到长时间运行的 `check-ignore` 进程的 `STDIN` 中，并且对于这些每个文件，`STDOUT` 将指示该文件是否匹配了模式。（如果没有此选项，将无法判断给定文件的输出缺失意味着它没有匹配任何模式，还是输出尚未生成。）

缓冲处理如 (1) 中 `GIT_FLUSH` 选项下的文档说明所示。调用者负责避免因输入缓冲区溢出或从空输出缓冲区读取导致的死锁。

## 退出状态

### 0

提供的一个或多个路径被忽略。

### 1

所有提供的路径均未被忽略。

### 128

遇到了致命错误。

# GIT-CHECK-MAILMAP

## 别名

`git-check-mailmap` - 显示联系人的标准名称和邮箱地址

## 概要

`git check-mailmap [options] <contact>...`

## 描述

对于命令行或标准输入（使用 `--stdin` 时）中的每个 `"Name <>"` 或 `"<>`，查找该人的标准名称和邮箱地址（见下文“映射作者”）。如果找到，则打印它们；否则原样打印输入。

### 选项

`--stdin`

在耗尽命令行提供的联系人后，从标准输入每行读取一个联系人。

## 输出

对每个联系人输出单行并以换行符结束。如果提供了名称或该名称在 `mailmap` 中已知，则打印 `"Name <>"`；否则只打印 `"<>`。

## 映射作者

如果 `.mailmap` 文件存在于仓库顶层，或者存在 `mailmap.file` 或 `mailmap.blob` 配置选项所指的位置，则使用它来将作者和提交者的名称及邮箱地址映射到标准的真实姓名和邮箱地址。

在简单形式下，文件中的每行由作者的标准真实姓名、空白以及提交中使用的邮箱地址（用 `<` 和 `>` 包围）组成，用于映射。例如：

`Proper Name <>`

更复杂的形式有：

`<> <>`

这允许 `mailmap` 仅替换提交的邮箱部分，以及：

`Proper Name <> <>`

这允许 `mailmap` 替换匹配指定提交邮箱地址的提交的名称和邮箱，以及：

`Proper Name <> Commit Name <>`

这允许 `mailmap` 替换同时匹配指定提交名称和邮箱地址的提交的名称和邮箱。

### 示例 1

你的历史包含两个作者 Jane 和 Joe 的提交，他们的名字在仓库中以多种形式出现：

`Joe Developer <> Joe R. Developer <> Jane Doe <> Jane Doe <.(none)> Jane D. <.(none)>`

现在假设 Joe 想使用他的中间名首字母，而 Jane 喜欢完整拼写她的姓。一个正确的 `.mailmap` 文件看起来如下：

`Jane Doe <.(none)> Joe R. Developer <>`

注意，不需要为 `<.(none)>` 创建条目，因为该作者的真实姓名已经是正确的。

### 示例 2

你的仓库包含来自以下作者的提交：

`nick1 <> nick2 <> nick2 <> santa <> claus <> CTO <>`

你可能想要一个这样的 `.mailmap` 文件：

`<> <> Some Dude <> nick1 <> Other Author <> Santa Claus <> Other Author <> <>`

使用 `#` 作为其行尾或邮箱地址后的注释。

# GIT-CHECK-REF-FORMAT

## 别名

`git-check-ref-format` - 确保引用格式正确

## 概要

`git check-ref-format [--normalize] [--no-]allow-level] [--refspec-pattern] <refname>`

## 描述

检查 `refname` 是否接受，如果不接受以非零状态退出。

引用在 Git 中用于分支和标签。分支存储在 `refs/heads`，而标签存储在 `refs/tags`。

Git 对引用命名有以下规则：

1. 允许包含 `/` 用于分层分组，但任何斜杠分隔的部分不能以 `.` 开头或以 `.lock` 结尾。
2. 必须包含至少一个 `/`。这强制要求类似 `heads/` 的类别，但实际名称不受限制。如果使用了 `--allow-level` 选项，则忽略此规则。
3. 不能有两个连续的点 `..`。
4. 任何地方不能有 ASCII 控制字符（即值小于 040 或 177 DEL）、空格、波浪号 `~`、脱号 `^` 或冒号 `:`。
5. 不能有 `?`、星号 `*` 或左括号 `[`。见下文 `--refspec-pattern` 选项。
6. 不能以斜杠 `/` 开头或结尾，或包含多个斜杠（见下文 `--normalize` 选项）。
7. 不能以点 `..` 结尾。
8. 不能包含序列 `@{`。
9. 不能是单个字符 `@`。
10. 不能包含 `\`。

这些规则使得基于 shell 的工具易于解析引用名称，避免了 shell 在错误未引用引用名称时进行路径扩展，同时也避免了引用表达式中的歧义：

1. 双点 `..` 经常用于 `ref1..ref2`，在某些上下文中这种符号表示 `^ref1 ref2`。
2. 波浪号 `~` 和脱号 `^` 用于引入后缀 *n 个父节点* 和 *剥壳* 操作。
3. 冒号 `:` 用于 `srcref:dstref`，表示在 fetch 和 push 操作中“使用 `srcref` 的值并将其存储在 `dstref`”。也可以用于选择特定对象，例如使用 `git cat-file` 时：`git cat-file blob v1.3.3:refs.c`。
4. 大大括号 `@{` 用作访问 reflog 条目的符号。

使用 `--branch` 选项，它可以扩展“上一个分支语法”`@{-n}`。例如，`@{-1}` 是引用之前所在分支的方法。瓷化程序（porcelains）应该在任何预期分支名称的地方使用此选项，以便它们可以像你输入了分支名称一样操作。

### 选项

#### `--[no-]allow-onelevel`

控制是否接受单级引用名（refnames）（即不包含多个由 `/-` 分隔组件的引用名）。默认为 `--no-allow-onelevel`。

#### `--refspec-pattern`

将 `<refname>` 解释为引用规格（refspec）的引用名模式（常用于远程仓库）。如果启用此选项，`<refname>` 允许包含单个 `*` 来替换一个完整的路径组件（例如 `foo/*/bar`，但不是 `foo/bar*`）。

#### `--normalize`

通过移除任何前头的斜杠（`/`）并将名称组件之间连续的斜杠合并为单个斜杠来归一化 `refname`。如果归一化后的 `refname` 有效，则将其打印到标准输出并以状态码 `0` 退出（`--print` 是 `--normalize` 的过时写法）。

## 示例

打印上一个分支的名称：

```bash
$ git check-ref-format --branch @{-1}
```

确定用于新分支的引用名：

```bash
$ ref=$(git check-ref-format --normalize "refs/heads/$newbranch") || die "we do not like '$newbranch' as a branch name."
```

***

# GIT-CHECKOUT-INDEX

## 名称

`git-checkout-index` - 从索引（index）复制文件到工作树

## 概要

`git checkout-index [-u] [-q] [-a] [-f] [-n] [--prefix=<string>] [--stage=<number>|all] [--temp] [-z] [--stdin] [--] [<file>...]`

## 描述

将索引列出的所有文件复制到工作目录（不覆盖现有文件）。

### 选项

- `-u, --index`：更新索引文件中已检出条目的统计信息。
- `-q, --quiet`：如果文件存在或不在索引中，则保持安静。
- `-f, --force`：强制覆盖现有文件。
- `-a, --all`：检出索引中的所有文件。不能与显式文件名一起使用。
- `-n, --no-create`：不检出新文件，只刷新已检出的文件。
- `--prefix=<string>`：在创建文件时，在前面加上 `<string>`（通常是一个包含末尾 `/` 的目录）。
- `--stage=<number>|all`：不再检出未合并的条目，而是从命名的阶段复制文件。`<number>` 必须在 1 到 3 之间。注意：`--stage=all` 自动意味着 `--temp`。
- `--temp`：不将文件复制到工作目录，而是将内容写入临时文件。临时文件名称关联将写入标准输出。
- `--stdin`：不再从命令行获取路径列表，而是从标准输入读取路径列表。默认情况下，路径由 LF 分隔（即每行一个路径）。
- `-z`：仅对 `--stdin` 有意义；路径用 NUL 字符而非 LF 分隔。
- `--`：不再将任何后续参数解释为选项。

所使用的标志顺序曾经很重要，但现在不再了。

仅仅执行 `git checkout-index` 什么都不会做。你可能想执行 `git checkout-index -a`。如果你想强制执行，你应该执行 `git checkout-index -f -a`。

直观性不是这里的目标。可重复性才是。“无参数意味着无操作”行为的原因是，在脚本中，你应该能够执行以下操作：

```bash
$ find . -name '*.h' -print0 | xargs -0 git checkout-index -f --
```



这将强制将所有存在的`*.h`文件替换为它们的缓存副本。如果空命令行意味着“全部”，那么这将强制刷新索引中的所有内容，而这并不是目的。但由于`git checkout-index`接受`--stdin`，使用以下命令会更快：

```bash
$ find . -name '*.h' -print0 | git checkout-index -f -z --stdin
```

`--`在你知道后面是文件名时是一个很好的主意；它可以防止因诸如`-a`这样的文件名引起的问题。在脚本中使用`--`可能是一个通用的策略。

## 使用`--TEMP`或`--STAGE=ALL`

当使用`--temp`（或由`--stage=all`隐含）时，`git checkout-index`将为每个检出的索引条目创建一个临时文件。索引不会更新统计信息。如果调用者需要所有未合并条目的所有阶段，以便由外部合并工具处理未合并的文件，这些选项将有用。

标准输出将写入一个列表，提供临时文件名与跟踪路径名的关联。列表格式有两种变体：

1. `tempname TAB path RS`

   当省略`--stage`或其不是`--stage=all`时使用这种格式。`tempname`字段是持有文件内容的临时文件名，`path`是索引中的跟踪路径名。仅输出请求的条目。

2. `stage1temp SP stage2temp SP stage3tmp TAB path RS`

   当使用`--stage=all`时使用这种格式。三个阶段临时字段（`stage1temp`、`stage2temp`、`stage3temp`）在索引中存在阶段条目时列出临时文件名，如果没有则显示`.`。只有阶段 0 的路径将始终从输出中排除。

在两种格式中，`RS`（记录分隔符）默认为换行符，但如果使用了`-z`，则为空字节。

# GIT-CHECKOUT

## 名称

`git-checkout` - 切换分支或恢复工作树

## 概要

`git checkout [-q] [-f] [-m] [<branch>]`

`git checkout [-q] [-f] [-m] --detach [<branch>]`

`git checkout [-q] [-f] [-m] --detach <commit>`

`git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]`

`git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <paths>...`

`git checkout [-p|--patch] [<tree-ish>] [--] [<paths>]`

## 描述

更新工作树中的文件以匹配索引或指定树的版本。如果没有路径，`git checkout`将并将指定的分支设置为当前分支。

`git checkout <branch>`

为了在`<branch>`上工作做准备，通过更新索引和工作树中的文件并将`HEAD`指向该分支来切换。工作树中文件的本地修改将被保留，以便将其提交到`<branch>`。

如果未找到`<branch>`但恰好一个远程仓库（称为`<remote>`）中存在具有匹配名称的跟踪分支，则将其视为等同于：

```bash
$ git checkout -b <branch> --track <remote>/<branch>
```

你可以省略`<branch>`，此时命令将退化为“检出当前分支”，这只是一个带有昂贵副作用的无操作，仅显示当前分支的跟踪信息（如果存在的话）。

`git checkout -b|-B|--orphan <new_branch> [<start_point>]`

指定`-b`会导致创建一个新分支，就像调用了`(1)`并对其进行了检出。在这种情况下，你可以使用`--track`或`--no-track`选项，这些选项将传递给`git branch`。为了方便起见，在不使用`-b`的情况下`--track`意味着创建分支；参见下文对`--track`的描述。

如果给出`-B`，如果`<new_branch>`不存在则创建它；否则，对其进行重置。这在事务上等同于：

```bash
$ git branch -f <branch> [<start point>] $ git checkout <branch>
```

也就是说，除非`git checkout`执行成功，否则不会对分支进行重置/创建。

```bash
git checkout --detach [<branch>]
git checkout [--detach] <commit>
```

准备在`<commit>`之上工作，通过将`HEAD`挂离到该提交上（参见“DETACHED HEAD”章节），并更新索引和工作树中的文件。工作树中文件的本地修改将被保留，因此生成的工作树将是提交中记录的状态加上本地修改。

当`<commit>`参数是分支名时，可以使用`--detach`选项将`HEAD`挂离到分支的顶端（`git checkout <branch>`将检出该分支而不挂离`HEAD`）。

省略`<branch>`则将`HEAD`挂离到当前分支的顶端。

```bash
git checkout [-p|--patch] [<tree-ish>] [--] <pathspec>...
```

当给出`<paths>`或`--patch`时，`git checkout`不切换分支。它从索引文件或命名的`<tree-ish>`（通常是提交）更新工作树中命名的路径。在这种情况下，`-b`和`--track`选项是没有意义的，提供其中任何一个都会导致错误。`<tree-ish>`参数用于在更新工作树之前，为指定的路径指定一个特定的 tree-ish（即提交、标签或树）以更新索引。

配合`<paths>`或`--patch`使用的`git checkout`用于从索引将已修改或已删除的路径恢复到其原始内容，或用来自命名的`<tree-ish>`（通常是提交对象）的内容替换路径。

索引可能由于之前的合并失败而包含未合并的条目。默认情况下，如果你尝试从索引检出此类条目，检出操作将失败且什么都不会被检出。使用`-f`将忽略这些未合并的条目。可以通过`--ours`或`--theirs`从索引中检出合并特定侧的内容。使用`-m`，可以丢弃对工作树文件所更改，以重建原始的冲突合并结果。

### 选项

- `-q, --quiet`：静默模式，抑制反馈消息。
- `-f, --force`：在切换分支时，即使索引或工作树与`HEAD`不同也继续执行。这用于丢弃本地更改。当从索引检出路径时，不会因未合并的条目而失败；相反将忽略未合并的条目。
- `--ours, --theirs`：从索引检出路径时，为未合并的路径检出阶段 #2（`--ours`）或 #3（`--theirs`）。
- `-b <new_branch>`：创建名为`<new_branch>`的新分支并从`<start_point>`开始它；详情请见`(1)`。
- `-B <new_branch>`：创建分支`<new_branch>`并从`<start_point>`开始它；如果它已存在，则将其重置为`<start_point>`。这等同于带有`-f`运行`git branch`；详情请见`(1)`。
- `-t, --track`：创建新分支时，设置“上游”配置。详情见`(1)`中的`--track`。如果没有给出`-b`选项，新分支名称将从远程跟踪分支派生，通过查看为对应远程配置的 refspec 的本地部分，然后剥离到`*`的初始部分。这将告诉我们在从`origin/hack`（或`remotes/origin/hack`，甚至`refs/remotes/origin/hack`）派生时使用`hack`作为本地分支。如果给定的名称没有斜杠，或者上述猜测结果为空名称，则取消猜测。在这种情况下，你可以通过`-b`显式给出名称。
- `--no-track`：不设置“上游”配置，即使`branch.autoSetupMerge`配置变量为 true。
- `-l`：创建新分支的引用日志（reflog）；详情请见`(1)`。
- `--detach`：与检出分支分支进行工作不同，而是检出一个提交用于检查和可丢弃的实验。这是当`<commit>`不是分支名时`git checkout <commit>`的默认行为。详情见下文的“DETACHED HEAD”章节。
- `--orphan <new_branch>`：创建名为`<new_branch>`的孤立分支，从`<start_point>`开始并切换到它。在该分支上进行的第一个提交将没有父节点，它将成为与所有其他分支和提交完全分离的新历史的根。索引和工作树的调整就像你之前运行了`git checkout <start_point>`一样。这允许你启动一个记录类似于`<start_point>`的路径集的新历史，通过轻松运行`git commit -a`来创建根提交。这在你想要从某个提交发布树而不暴露其完整历史时非常有用。你可能想通过此操作发布一个项目的开源分支。
- `--ignore-skip-worktree`：在稀疏检出模式下，`git checkout -- <paths>`只更新由`<paths>`和稀疏模式匹配的条目。
- `--ignore-other-worktrees`：当所需的引用已被另一个工作树检出时，`git checkout`会拒绝。此选项强制检出该引用。换句话说，该引用可以被多个工作树持有。
- `-m, --merge`：在切换分支时，如果当前分支与要切换的分支之间存在本地修改，命令将拒绝切换。然而，使用此选项将在当前分支、你的树内容和新分支之间执行三路合并，并将进入新分支。当发生合并冲突时，冲突路径的索引条目保持未合并状态，你需要解析冲突并使用`git add`标记路径（如果合并导致删除则使用`git rm`）。从索引检出路径时，此选项允许在指定路径中重建冲突。
- `--conflict=<style>`：与上述`--merge`选项相同，但更改冲突块呈现的方式，覆盖`merge.conflictStyle`配置变量。可能值为`merge`（默认）和`diff3`（在合并样式的基础上显示原始内容）。
- `-p, --patch`：交互式选择`<tree-ish>`（未指定则为索引）与工作树之间的差异块。选中的块随后将反向应用于工作树（如果指定了`<tree-ish>`，则应用于索引）。这意味着你可以使用`git checkout -p`选择性丢弃当前工作树中的编辑。参见`(1)`的“交互模式”章节了解如何操作`--patch`模式。
- `<branch>`：要检出的分支；如果它引用一个分支（即在名称前加上`refs/heads/`后是有效引用），则检出该分支。否则，如果它引用一个有效的提交，你的`HEAD`将处于“游离”状态，且不再处于任何分支上（详情见下文）。

作为一种特殊情况，`@{-N}`语法用于检查倒数第 N 个分支/提交（而不是分离头指针状态）。你也可以指定`-`，它与`@{-1}`等价。

另一个特殊情况是，如果`A`和`B`恰好有一个合并基底，你可以使用`A...B`作为它们合并基底的快捷方式。你可以省略`A`和`B`中的最多一个，在这种情况下，它将默认为`HEAD`。

`<new_branch>`

新分支的名称。

`<start_point>`

开始创建新分支的提交名称；详请见`(1)`。默认为`HEAD`。

`<tree-ish>`

要从此处检出的树（当给出了路径时）。如果未指定，则将使用索引（index）。

## 分离头指针（DETACHED HEAD）

`HEAD`通常指向一个具名的分支（例如`master`）。同时，每个分支指向一个特定的提交。让我们来看一个包含三个提交的仓库，其中一个被标记了标签，并且检出了`master`分支：

```text
HEAD (指向分支 'master') | v a---b---c branch 'master' (指向提交 'c') ^ | tag 'v2.0' (指向提交 'b')
```

当在此状态下创建提交时，分支将更新为指向新提交。具体来说，`git commit`会创建一个新提交`d`，其父提交是提交`c`，然后更新分支`master`指向新提交`d`。`HEAD`仍然指向分支`master`，因此现在间接地指向了提交`d`：

```text
$ edit; git add; git commit HEAD (指向分支 'master') | v a---b---c---d branch 'master' (指向提交 'd') ^ | tag 'v2.0' (指向提交 'b')
```

有时，能够检出一个不在任何具名分支顶端的提交，甚至创建一个不被任何具名分支引用的新提交，是非常有用的。让我们看看检出提交`b`时会发生什么（这里展示了两种可能的实现方式）：

```text
$ git checkout v2.0 # 或 $ git checkout master^^ HEAD (指向提交 'b') | v a---b---c---d branch 'master' (指向提交 'd') ^ | tag 'v2.0' (指向提交 'b')
```

注意，无论我们使用哪种 checkout 命令，`HEAD`现在都直接指向提交`b`。这被称为处于“分离头指针”状态。这简单意味着`HEAD`指向一个特定的提交，而不是指向一个具名分支。让我们看看当我们创建一个提交时会发生什么：

```text
$ edit; git add; git commit HEAD (指向提交 'e') | v e / a---b---c---d branch 'master' (指向提交 'd') ^ | tag 'v2.0' (指向提交 'b')
```

现在有一个新提交`e`，但它只被`HEAD`引用。当然，我们可以在这种状态下再添加另一个提交：

```text
$ edit; git add; git commit HEAD (指向提交 'f') | v e---f / a---b---c---d branch 'master' (指向提交 'd') ^ | tag 'v2.0' (指向提交 'b')
```

事实上，我们可以执行所有的正常的 Git 操作。但是，让我们看看如果我们随后检出`master`会发生什么：

```text
$ git checkout master HEAD (指向分支 'master') e---f | / v a---b---c---d branch 'master' (指向提交 'd') ^ | tag 'v2.0' (指向提交 'b')
```

重要的是，要意识到在此时没有任何东西指向提交`f`。

在记录 commit 时，在原始 commit 消息末尾添加一行`(cherry picked from commit ...)`，以指示该更改是从哪个 commit 拾取（cherry pick）的。这仅适用于没有冲突的 cherry-pick。如果你是从自己的私有分支进行 cherry-pick，请勿使用此选项，因为这些信息对接收者是没用的。相反，如果你在两个公开分支之间进行 cherry-pick（例如从开发分支将修复程序回移植到旧版本的维护分支），添加这些信息可以是很有用的。

`-r`

该命令以前默认执行上述的`-x`，而`-r`则用于禁用它。现在默认不执行`-x`，因此此选项是一个空操作。

`-m parent-number, --mainline parent-number`

通常你无法 cherry-pick 一个合并 commit，因为你不知道合并的哪侧应该被视为主线。此选项指定主线的父节点编号（从 1 开始），允许 cherry-pick 相指定的父节点重放更改。

`-n, --no-commit`

通常该命令会自动创建一系列 commit。此标志会将 cherry-pick 每个命名 commit 所需的更改应用到你的工作树和索引中，而不创建任何 commit。此外，当使用此选项时，你的索引不需要与`HEAD`commit 匹配。cherry-pick 是针对你索引的初始状态进行的。

这在你连续向索引 cherry-pick 多个 commit 的效果时非常有用。

`-s, --signoff`

在 commit 消息末尾添加 Signed-off-by 行。

`-S[<key-id>], --gpg-sign[=<key-id>]`

对 commit 进行 GPG 签名。

`--ff`

如果当前的`HEAD`与被 cherry-pick commit 的父节点相同，则执行该 commit 的快进（fast forward）。

`--allow-empty`

默认情况下，cherry-pick 一个空 commit 将失败，表示需要显式调用`git commit --allow-empty`。此选项将覆盖该行为，允许在 cherry-pick 中自动保留空 commit。注意，当`--ff`生效时，满足“快进”要求的空 commit 即使没有此选项也会保留。另请注意，使用此选项仅保留最初为空的 commit（即该 commit 记录的树与其父节点相同的树）。由于之前的 commit 导致变为空的 commit 将被丢弃。要强制包含这些 commit，请使用`--keep-redundant-commits`。

`--allow-empty-message`

默认情况下，cherry-pick 一个消息为空的 commit 将失败。此选项覆盖该行为，允许对空消息的 commit 进行 cherry-pick。

`--keep-redundant-commits`



如果正在 `cherry-pick` 的 `commit` 与当前历史中的某个 `commit` 重复，它将为空。默认情况下，这些冗余 `commit` 会导致 `cherry-pick` 停止，以便用户检查该 `commit`。此选项覆盖该行为并创建一个空 `commit` 对象。隐含 `--allow-empty`。

`--strategy=<strategy>`

使用指定的合并策略。应仅使用一次。详情见 (1) 中的 `MERGE STRATEGIES` 章节。

`-X<option>, --strategy-option=<option>`

将合并策略特定的选项传递给合并策略。详情见 (1)。

## 序列化器子命令

`--continue`

使用 `*.git/sequencer` 中的信息继续正在进行的操作。可用于解决失败的 `cherry-pick` 或 `revert` 中的冲突后继续执行。

`--quit`

忘记正在进行的操作。用于失败的 `cherry-pick` 或 `revert` 后清除序列化器状态。

`--abort`

取消操作并返回到序列化之前的状态。

## 示例

```bash
git cherry-pick master
```

应用 `master` 分支端 `commit` 所引入的更改，并用此更改创建一个新 `commit`。

```bash
git cherry-pick ..master, git cherry-pick ^HEAD master
```

应用所有 `master` 的祖先但不是 `HEAD` 的 `commit` 所引入的更改，以产生新 `commit`。

```bash
git cherry-pick maint next ^master, git cherry-pick maint master..next
```

应用所有 `maint` 或 `next` 的祖先但不是 `master` 或其任何祖先的 `commit` 所引入的更改。注意，后者并不是指 `maint` 以及 `master` 和 `next` 之间的所有内容；具体来说，如果 `maint` 在 `master` 中，则不会使用 `maint`。

```bash
git cherry-pick master~4 master~2
```

应用 `master` 指向的倒第五和倒第三 `commit` 所引入的更改，并用这些更改创建 2 个新 `commit`。

```bash
git cherry-pick -n master~1 next
```

将 `master` 指向的倒第二个 `commit` 以及 `next` 指向的最后一个 `commit` 所引入的更改应用到工作树和索引，但不要用这些更改创建任何 `commit`。

```bash
git cherry-pick --ff ..next
```

如果历史是线性的且 `HEAD` 是 `next` 的祖先，则更新工作树并将 `HEAD` 指针移动到 `next`。否则，将 `next` 中但 `HEAD` 中没有的 `commit` 的更改应用于当前分支，为每个新更改创建一个新 `commit`。

```bash
git rev-list --reverse master -- README | git cherry-pick -n --stdin
```

将 `master` 分支上所有修改 `README` 的 `commit` 所引入的更改应用到工作树和索引，以便检查结果并在并在的情况下合并为一个新 `commit`。

以下序列尝试回移植一个补丁，由于补丁应用的代码变化太大而退出，然后再次尝试，这次在匹配上下文行时会更加小心。

```bash
$ git cherry-pick topic^
```

**(1)**

```bash
$ git diff
```

**(2)**

```bash
$ git reset --merge ORIG_HEAD
```

**(3)**

```bash
$ git cherry-pick topic^
```

**(4)**

```bash
$ git cherry-pick -Xpatience topic^
```

**1.** 应用 `git show topic^` 显示的更改。在例例中，补丁没有整洁地应用，因此冲突信息被写入索引，且没有产生新 `commit`。

**2.** 总结需要调和的更改

**3.** 取消 `cherry-pick`。换句话说，返回到 `cherry-pick` 之前的状态，保留你之前的任何本地修改。

**4.** 再次尝试应用 `topic^` 引入的更改，花费额外时间以避免因上下文行匹配错误导致的错误。

## 另另

(1)

```bash
$ git log --graph --oneline --decorate --boundary origin/master...topic * 7654321 (origin/master) upstream tip commit [... snip some other commits ...] * cccc111 cherry-pick of C * aaaa111 cherry-pick of A [... snip a lot more that has happened ...] | * cccc000 (topic) commit C | * bbbb000 commit B | * aaaa000 commit A |/ o 1234567 branch point
```

在这些情况下，`git-cherry` 显示了尚未应用的提交的简要摘要：

```bash
$ git cherry origin/master topic - cccc000... commit C + bbbb000... commit B - aaaa000... commit A
```

在这里，我们看到提交 `A` 和 `C`（标记为 `-`）可以在您将 `topic` 分支变基到 `origin/master` 之上时从您的 `topic` 分支中删除，而提交 `B`（标记为 `+`）仍然需要保留，以便将其发送并应用到 `origin/master`。

### 使用限制

可选的 `<limit>` 在您的 `topic` 基于上游中不存在的其他工作时非常有用。扩展之前的示例，它看起来可能像这样：

```bash
$ git log --graph --oneline --decorate --boundary origin/master...topic * 7654321 (origin/master) upstream tip commit [... snip some other commits ...] * cccc111 cherry-pick of C * aaaa111 cherry-pick of A [... snip a lot more that has happened ...] | * cccc000 (topic) commit C | * bbbb000 commit B | * aaaa000 commit A | * 0000fff (base) unpublished stuff F [... snip ...] | * 0000aaa unpublished stuff A |/ o 1234567 merge-base between upstream and topic
```

通过指定 `base` 为限制条件，您可以避免列出 `base` 和 `topic` 之间的提交：

```bash
$ git cherry origin/master topic base - cccc000... commit C + bbbb000... commit B - aaaa000... commit A
```

## 参见

(1)

---

# GIT-CLEAN

## 名称

`git-clean` - 从工作树中删除未跟踪的文件

## 概要用法说明

`git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] <path>...`

## 描述

通过从当前目录开始递归删除不受版本控制的文件来清理工作树。

通常情况下，只有 `Git` 未知的文件会被删除，但如果指定了 `-x` 选项，忽略的文件也会被删除。这对于删除所有构建产物非常有用。

如果给了任何可选的 `<path>...` 参数，则只有这些路径受影响。

### 选项

`-d`

除了未跟踪的文件外也删除未跟踪的目录。如果未跟踪的目录由另一个 `Git` 仓库管理，默认情况下不会删除。如果您真的想删除此类目录，请使用两次 `-f` 选项。

`-f, --force`

如果 `Git` 配置变量 `clean.requireForce` 未设置为 `false`，则在没有给出 `-f`、`-n` 或 `-i` 的情况下，`git clean` 将拒绝删除文件或目录。除非给出第二个 `-f`，否则 `Git` 将拒绝删除带有 `.git` 子目录或文件的目录。也会影响 `git` 子模块，被删除子模块在 `.git/modules/` 下的存储区域在给出两次 `-f` 之前不会被删除。

`-i, --interactive`

显示将要执行的操作并以交互方式清理文件。详情请参见“交互模式”。

`-n, --dry-run`

不实际删除任何内容，只显示将要的操作。

`-q, --quiet`

保持安静，只报告错误，不报告成功删除的文件。

`-e <pattern>, --exclude=<pattern>`

除了在 `.gitignore`（按目录）和 `$GIT_DIR/info/exclude` 中找到的模式外，还考虑将这些模式纳入生效的忽略规则集中。

`-x`

不使用从 `.gitignore`（按目录）和 `$GIT_DIR/info/exclude` 读取的默认忽略规则，但仍使用通过 `-e` 选项提供的忽略规则。这允许删除所有未跟踪的文件，包括构建产物。这可以用于（可能结合 `git reset`）创建一个纯净的工作目录以测试干净的构建。

`-X`

仅删除被 `Git` 忽略的文件。这对于从头开始重建一切可能有用，但保留手动创建的文件。

## 交互模式

当命令进入交互模式时，它会显示要清理的文件和目录，并进入交互式命令循环。

命令循环显示可用的子命令列表，并提示“What now> ”。通常，当提示以单个 `*` 结束时，您可以只选择给出的选项之一并按回车，如下：

```
*** Commands *** 1: clean 2: filter by pattern 3: select by numbers 4: ask each 5: quit 6: help What now> 1
```

只要选择是唯一的，您也可以上方说 `c` 或 `clean`。

主命令循环有 6 个子命令。

### `clean`

开始清理文件和目录，然后退出。

### `filter by pattern`

按模式过滤。这将显示要删除的文件和目录，并给出“What now> ”的提示。通常，当提示以单个 `*` 结束时，您可以只选择给出的选项之一并按回车，如下：

### `select by numbers`

按数字选择。这将显示要删除的文件和目录，并给出“What now> ”的提示。通常，当提示以单个 `*` 结束时，您可以只选择给出的选项之一并按回车，如下：

### `ask each`

逐询问。这将显示要删除的文件和目录，并给出“What now> ”的提示。通常，当提示以单个 `*` 结束时，您可以只选择给出的选项之一并按回车，如下：

### `quit`

退出。

### `help`

显示 `git-clean` 的简要用法。

## 参见

(5)

---

# GIT-CLONE

## 名称

`git-clone` - 将仓库克隆到新目录

## 概要用法说明

`git clone [--template=<template_directory>] [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror] [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>] [--dissociate] [--separate-git-dir <git dir>] [--depth <depth>] [--[no-]single-branch] [--recursive | --recurse-submodules] [--] <repository> [<directory>]`

## 描述

将仓库克隆到新目录，为每个分支创建远程跟踪分支（使用 `git branch -r` 可），并检出一个从克隆仓库活动分支分支初始分支。

克隆后，普通的 `git fetch` 将更新所有远程跟踪分支，`git pull` 将额外将远程主分支合并到当前主分支（在给出 `--single-branch` 时不如此；见下文）。

此默认配置通过在 `refs/remotes/origin` 下创建远程分支引用以及初始化 `remote.origin.url` 和 `remote.origin.fetch` 配置变量来实现。

### 选项

`--local, -l`

当要克隆的仓库位于本地机器时，此标志跳过正常的“感知 Git”传输机制，通过复制 `HEAD` 以及 `objects` 和 `refs` 目录下的内容来克隆仓库。`.git/objects/` 目录下的文件尽可能使用硬链接以节省空间。

如果指定为本地路径（例如 `/path/to/repo`），这是默认设置，且 `--local` 实际上不起作用。如果指定为 URL，则忽略此标志（此时我们从不使用本地优化）。指定 `--no-local` 将在给出 `/path/to/repo` 时覆盖默认设置，使用常规 `Git` 传输。

`--no-hardlinks`

强制从本地文件系统上的仓库进行克隆时复制 `.git/objects` 目录下的文件，而不是使用硬链接。当您尝试备份仓库时这可能是需要的。

`--shared, -s`

当要克隆的仓库位于本地机器时，将不再使用硬链接，而是自动设置 `.git/objects/info/alternates` 来与源仓库共享对象。生成的仓库初始时不包含任何自己的对象。

**注意**：这是一个可能带有危险的操作；除非你理解它的作用，否则**切勿**使用它。如果你使用此选项克隆仓库，然后在源仓库中删除分支（或使用任何其他导致现有提交未引用的 `Git` 命令），某些对象可能会变成未被引用的（或悬空的）。这些对象可能会被正常的 `Git` 操作（如 `git commit`）移除，这些操作会自动调用 `git gc --auto`。（参见 (1)）。）如果这些对象被移除了，且它们曾被克隆的仓库所引用，那么克隆的仓库将会损坏。

请注意，在通过 `-s` 克隆的仓库中如果不带 `-l` 选项运行 `git repack`，会将对象从源仓库复制到克隆仓库的包中，从而失去了 `clone -s` 节省磁盘空间的效果。不过，运行 `git gc` 是安全的，因为它默认使用 `-l` 选项。

如果你想断开通过 `-s` 克隆的仓库对源仓库的依赖，可以简单运行 `git repack -a` 将所有对象从源仓库复制到克隆仓库的包中。

### `--reference <repository>`

如果引用仓库位于本地机器上，将自动设置 `.git/objects/info/alternates` 以从引用仓库获取对象。使用已存在的仓库作为替代方案可以减少从被克隆仓库中复制的对象数量，降低网络和本地存储成本。

**注意**：请参见 `--shared` 选项的注意事项，以及 `--dissociate` 选项。

### `--dissociate`

仅从通过 `--reference` 选项指定的引用仓库借用对象以减少网络传输，并在克隆完成后，通过为借用的对象创建必要的本地副本来停止从那里借用。

### `--quiet, -q`

静默运行。进度不会向标准错误流报告。在给定的此标志时，它也会被传递给 `rsync` 命令。

### `--verbose, -v`

详细模式运行。不影响向标准错误流报告进度状态。

### `--progress`

默认情况下，当标准错误流连接到终端时，会在标准错误流上报告进度状态，除非指定了 `-q`。此标志即使在标准错误流未定向到终端也会强制报告进度状态。

### `--no-checkout, -n`

克隆完成后不执行 `HEAD` 的检出。

### `--bare`

创建一个裸（bare）`Git` 仓库。也就是说，而不是创建 `<directory>` 并将管理文件放在 `<directory>/.git` 中，而是让 `<directory>` 本身成为 `$GIT_DIR`。这显然意味着 `-n`，因为没有地方可以检出工作树。此外，远程分支头将直接复制到对应的本地分支头，而不会将其映射到 `refs/remotes/origin/`。当使用此选项时，不会创建远程跟踪分支或相关的配置变量。

### `--mirror`

设置源仓库的镜像。这意味着 `--bare`。与 `--bare` 相比，`--mirror` 不仅将源的本地分支映射到目标的本地分支，还映射所有的引用（包括远程跟踪分支、注释等等），并设置 `refspec` 配置，使得所有这些引用在目标仓库的 `git remote update` 中被覆盖。

### `--origin <name>, -o <name>`

使用 `<name>` 代替使用远程名称 `origin` 来跟踪上游仓库。

### `--branch <name>, -b <name>`

不再将新创建的 `HEAD` 指向克隆仓库 `HEAD` 所指向的分，而是指向 `<name>` 分支。在非裸仓库中，这将是将被检出的分支。`--branch` 也可以接受标签，并在生成的仓库中分离到该提交的 `HEAD`。

### `--upload-pack <upload-pack>, -u <upload-pack>`

当给定此参数且通过 `ssh` 访问要克隆的仓库时，它指定了在另一端运行的命令的非默认路径。

### `--template=<template_directory>`



指定从哪个目录使用模板文件；（参见 (1) 的“TEMPLATE DIRECTORY”部分。）

### `--config <key>=<value>, -c <key>=<value>`

在新创建的仓库中设置配置变量；该设置在仓库初始化后立即生效，但在获取远程历史或检出任何文件之前生效。键的格式与 (1) 预期的格式相同（例如 `core.eol=true`）。如果为同一个键给出多个值，每个值都将写入配置文件。这使得（例如）向 `origin` 远程添加额外的 fetch refspecs 是安全的。

### `--depth <depth>`

创建一个浅层克隆，其历史被截断到指定的修订数量。

### `--[no-]single-branch`

只克隆通向单个分支末端的历史，该分支由 `--branch` 选项指定，或者由主分支远程的 `HEAD` 指向。在使用 `--depth` 选项创建浅层克隆时，这是默认设置，除非给出 `--no-single-branch` 来获取所有分支末端附近的历史。对生成的仓库进行后续获取将只会更新用于初始克隆的该分支的远程跟踪分支。如果在执行 `--single-branch` 克隆时，远端的 `HEAD` 没有指向任何分支，则不会创建远程跟踪分支。

### `--recursive, --recurse-submodules`

克隆创建后，初始化所有的子模块，使用它们的默认设置。这等同于克隆完成后立即运行 `git submodule update --init --recursive`。如果给出了 `--no-checkout/-n` 或 `--bare`，则此选项被忽略。

### `--separate-git-dir=<git dir>`

不再将克隆仓库放在它应该所在的位置，而是将克隆仓库放在指定的目录，然后在那里创建一个文件系统相关的符号链接。结果是 Git 仓库可以与工作树分离。

### `<repository>`

要克隆的（可能是远程）仓库。有关指定仓库的更多信息请参见下文 URL。

### `<directory>`

目标目录名称。如果没有显式给出目录，则使用源仓库的“人类”部分。克隆到已存在的目录仅在目录为空时允许。

## URLS

通常，URL 包含传输协议、远程服务器的地址以及仓库的路径。取决于传输协议，这些信息可能会缺失。

Git 支持 `ssh`、`git`、`http` 和 `https` 协议（此外，`ftp` 和 `ftps` 可用于获取，`rsync` 可用于获取和推送，但这些效率低下；不要使用它们）。

原生传输（即 `git://` URL）不进行身份验证，在不安全的网络上应谨慎使用。

以下语法适用于它们：

`http[s]://host.xz[:port]/path/to/repo.git/`

`ftp[s]://host.xz[:port]/path/to/repo.git/`

另一种类似于 scp 的语法也可适用于 `ssh` 协议：

`[user@]host.xz:path/to/repo.git/`

此语法只有在第一个冒号之前没有斜线时才被识别。有助于区分包含冒号的本地路径。例如，本地路径 `foo:bar` 可以指定为绝对路径或 `./foo:bar` 以避免被误认为是 ssh url。

`ssh` 和 `git` 协议额外支持 `~username` 扩展：

`[user@]host.xz:/~[user]/path/to/repo.git/`

对于本地仓库（Git 原生支持），可以使用以下语法：

`/path/to/repo.git/`

这两种语法大部分等价，前者隐含 `--local` 选项。

当 `Git` 不知道如何处理某种传输协议时，它会尝试使用 `remote-<transport>` 远程助手（如果存在的话）。要显式请求远程助手，可以使用以下语法：

`<transport>::<address>`

其中 `<address>` 可能是一个路径、服务器和路径，或者是由调用的特定远程助手所识别的任意 URL 字符串。详情请参见 (1)。

如果存在大量命名相似的远程仓库，且你希望为它们使用不同的格式（使得你使用的 URL 将被重写为可以工作的 URL），你可以创建一个如下形式的配置节：

`[url "<actual url base>"] insteadOf = <other url base>`

例如，使用以下配置：

`[url ""] insteadOf = host.xz:/path/to/ insteadOf = work:`

像 `"work:repo.git"` 或 `"host.xz:/path/to/repo.git"` 这样的 URL 在任何接受 `""` 作为 URL 的环境中会被重写。

如果你只想针对推送（push）重写 URL，可以创建一个如下形式的配置节：

`[url "<actual url base>"] pushInsteadOf = <other url base>`

例如，使用以下配置：

`[url ""] pushInsteadOf =`

像 `" "` 的 URL 在推送时会被重写为 `" "`，但拉取（pull）仍将使用原始 URL。

## 示例

从上游克隆：

```shell
$ git clone my-linux
$ cd my-linux
$ make
```

创建一个引用当前目录的本地克隆，但不检出文件：

```shell
$ git clone -l -s -n . ../copy
$ cd ../copy
$ git show-branch
```

在从现有本地目录借鉴的同时从上游克隆：

```shell
$ git clone --reference /git/linux.git \
  my-linux
$ cd my-linux
```

创建一个裸仓库（bare repository）以向公共发布你的更改：

```shell
$ git clone --bare -l /home/proj/.git /pub/scm/proj.git
```

***

# GIT-COLUMN

## 名称

`git-column` - 以列格式显示数据

## 概要

`git column [--command=<name>] [--[raw-]mode=<mode>] [--width=<width>] [--indent=<string>] [--nl=<string>] [--padding=<n>]`

## 描述

此命令将输入格式化为多列。

### 选项

#### `--command=<name>`

使用配置变量 `column.<name>` 和 `column.ui` 查找布局模式。

#### `--mode=<mode>`

指定布局模式。选项语法参见配置变量 `column.ui`。

#### `--raw-mode=<n>`

与 `--mode` 相同，但接受数字编码的模式。主要用于已解析布局模式的其他命令。

#### `--width=<width>`

指定终端宽度。默认情况下，`git column` 将检测终端宽度，如果无法检测则回退到 80。

#### `--indent=<string>`

在每行开头打印的字符串。

#### `--nl=<N>`

在每行结尾打印的字符串，包括换行符。

#### `--padding=<N>`

列之间的空格数。默认一个空格。

***

# GIT-COMMIT-TREE

## 名称

`git-commit-tree` - 创建一个新的提交对象

## 概要

```text
git commit-tree <tree> [(-p <parent>)...] < changelog

git commit-tree [(-p <parent>)...] [-S[<keyid>]] [(-m <message>)...] [(-F <file>)...] <tree>
```

## 描述

这通常不是最终用户想要直接运行的。请改看 (1)。

基于提供的 tree 对象创建一个新的提交对象，并在标准输出输出新的提交对象 ID。除非给了 `-m` 或 `-F` 选项，否则日志消息将从标准输入读取。

提交对象可以有任意数量的父对象。如果只有一个父对象，它是一个普通的提交。如果有多个父对象，该提交是几条历史之间的合并。初始（根）提交没有父对象。

虽然 tree 代表工作目录的特定目录状态，但 commit 代表该状态在“时间”上的位置，并解释了如何到达那里。

通常一个提交会标识一个新的 `"HEAD"` 状态，虽然 Git 不关心你将关于该状态的记录存在哪里，但在实践中我们倾向于将结果写入 `.git/HEAD` 指向的文件，这样我们始终能看到最后提交的状态。

### 选项

#### `<tree>`

一个存在的 tree 对象。

#### `-p <parent>`

每个 `-p` 表示父提交对象的 ID。

#### `-m <message>`

提交日志消息中的段落。可以多次给出，每个 `<message>` 变成自己的段落。

#### `-F <file>`

从给定文件读取提交日志消息。使用 `-` 从标准输入读取。

#### `-S[<keyid>], --gpg-sign[=<keyid>]`

GPG 签名提交。

#### `--no-gpg-sign`

取消 `commit.gpgSign` 配置变量，该变量用于强制每个提交进行签名。

## 提交信息

一个提交封装了：

- 所有父对象 ID
- 作者姓名、邮箱和日期
- 提交者姓名、邮箱和提交时间

虽然父对象 ID 在命令行中提供，但如果设置了，作者和提交者信息将从以下环境变量获取：

`GIT_AUTHOR_NAME GIT_AUTHOR_EMAIL GIT_AUTHOR_DATE GIT_COMMITTER_NAME GIT_COMMITTER_EMAIL GIT_COMMITTER_DATE`

如果你没有此配置变量，将使用 `i18n.commitencoding` 的值。

注意，我们特意选择在进行提交时不重新编码提交日志消息，以强制在提交对象级别使用 UTF-8，因为重新编码为 UTF-8 并不一定是一个可逆的操作。

## 文件

`/etc/mailname`

## 相关参见

(1)

***

# GIT-COMMIT

## 名称

`git-commit` - 记录仓库的更改

## 概要

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend] [--dry-run] [(-c | -C | --fixup | --squash) <commit>] [-F <file> | -m <msg>] [--reset-author] [--allow-empty] [--allow-empty-message] [--no-verify] [-e] [--author=<author>] [--date=<date>] [--cleanup=<mode>] [--[no-]status] [-i | -o] [-S[<key-id>]] [--] [<file>...]
```

## 描述

将索引（index）的当前内容存储在一个新的提交中，并带上用户描述更改的日志消息。

要添加的内容可以通过多种方式指定：

1. 通过使用 `git add` 在使用 `commit` 命令之前将更改增量“添加”到索引中（注意：即使是修改过的文件也必须“添加”）；
2. 在使用 `commit` 命令之前，通过 `git rm` 从工作树和索引中删除文件；
3. 通过将文件作为 `commit` 命令的参数列出，在这种情况下，提交将忽略索引中暂存的更改，而是在记录列出的文件的当前内容（这些文件必须是 Git 已知的）；
4. 通过使用 `commit` 命令的 `-a` 切换来自动“添加”所有已知文件的更改（即所有已列在索引中的文件），并自动“删除”索引中已从工作树中删除的文件，然后执行实际的提交；
5. 通过使用 `commit` 命令的 `--interactive` 或 `--patch` 切换，在最终完成操作之前，逐个决定哪些文件或代码块（hunks）应该是提交的一部分。请参见 (1) 的“交互模式”部分以了解如何操作这些模式。

`--dry-run` 选项可以通过提供相同的参数 set（选项和路径），获取上述任何操作在下一次提交中将包含内容的摘要。

如果你进行了提交，并在之后立即发现错误，可以使用 `git reset` 从中恢复。

### 选项

#### `-a, --all`

告诉命令自动暂存已修改和删除的文件，但你尚未告知 Git 的新文件不会受影响。

#### `-p, --patch`

使用交互式补丁选择界面来选择要提交的更改。详情参见 (1)。

#### `-C <commit>, --reuse-message=<commit>`

取一个现有的提交对象，并在创建提交时复用其日志消息和作者信息（包括时间戳）。

#### `-c <commit>, --reedit-message=<commit>`

与 `-C` 类似，但使用 `-c` 会调用编辑器，以便用户可以进一步编辑提交消息。

#### `--fixup=<commit>`

构建一个用于 `rebase --autosquash` 的提交消息。提交消息将是指定提交的主题行，并带有“fixup! ”前缀。详情参见 (1)。

#### `--squash=<commit>`

构建一个用于 `rebase --autosquash` 的提交消息。提交消息的主题取自指定提交，并带有“squash! ”前缀。可以配合额外的提交消息选项（`-m/-c/-C/-F`）。详情参见 (1)。

#### `--reset-author`

与 `-C/-c/--amend` 选项配合使用，或在冲突的 cherry-pick 后进行提交时，声明结果提交的作者现在属于提交者。这也刷新作者时间戳。

#### `--short`

在进行运行（dry-run）时，以短格式输出。详情参见 (1)。隐含 `--dry-run`。

#### `--branch`

即使在短格式下，也显示分支和跟踪信息。

#### `--porcelain`

在进行运行时，以便于解析的 porcelain-ready 格式输出。详情参见 (1)。隐含 `--dry-run`。

#### `--long`

在进行运行时，以长格式输出。隐含 `--dry-run`。

#### `-z, --null`

在显示短格式或 porcelain 状态输出时，用 NUL 代替 LF 终止状态输出项。如果没有给出格式，则隐含 `--porcelain` 输出格式。

#### `-F <file>, --file=<file>`

从给定文件获取提交消息。使用 `-` 从标准输入读取消息。

#### `--author=<author>`

覆盖提交作者。使用标准的 A U Thor <> 格式指定显式作者。否则，`<author>` 被视为模式，并用于搜索该作者的现有提交（即 `rev-list --all -i --author=<author>`）；然后从找到的第一个此类提交中复制提交作者。

#### `--date=<date>`

覆盖提交中使用的作者日期。

#### `-m <msg>, --message=<msg>`

使用给定的 `<msg>` 作为提交消息。如果给出多个 `-m` 选项，它们的值将合并为独立的段落。

#### `-t <file>, --template=<file>`

编辑提交消息时，使用指定文件的启动编辑器。`commit.template` 变量通常用于提示。如果用户退出编辑器且未编辑消息，则取消提交。

#### `-s, --signoff`

在消息末尾添加 Signoff-by 行。

#### `-n, --no-verify`

跳过 pre-commit 和 commit-msg 钩子。另见 (5)。

#### `--allow-empty`

通常记录一个与其父节点树相同的提交是错误的，该命令会阻止你进行此类提交。此选项主要用于外部脚本。

#### `--allow-empty-message`

类似于 `--allow-empty`，该命令主要用于外部脚本。它允许创建一个空消息的提交。

#### `--cleanup=<mode>`

此选项决定在提交前如何对提供的提交消息进行清理。`<mode>` 可以是 `strip`、`whitespace`、`verbatim` 或 `default`。

##### `strip`

删除首尾行、行尾空格、注释并合并连续空行。

##### `whitespace`

与 `strip` 相同，但不移除注释。

##### `verbatim`

完全不更改消息。

##### `scissors`

与 `whitespace` 相同，但如果编辑消息，从“# ------------------------ >------------------------”开始的所有内容将被截断。“#”可以通过 `core.commentChar` 自定义。

##### `default`

如果编辑消息，则与 `strip` 相同。否则为 `whitespace`。可以通过 `commit.cleanup` 变量更改（参见 (1)）。

#### `-e, --edit`

从文件 `-F`、命令行 `-m` 和从提交对象 `-C` 获取的消息通常作为未修改的提交日志消息。此选项让你进一步编辑从这些来源获取的消息。

#### `--no-edit`

在不启动编辑器的情况下使用选定的提交消息。例如，`git commit --amend --no-edit` 在不更改提交消息的情况下修订提交。

#### `--amend`

创建一个新提交来替换当前分支的顶点。按通常记录树（包括 `-i` 和 `-o` 选项以及显式路径规范的影响），如果未通过命令行选项 `-m/-F/-c` 等指定其他消息，则使用原始提交的消息作为起始点，而不是空消息。新提交与当前提交具有相同的父节点和作者（`--reset-author` 选项可以取消此限制）。它大致相当于：

```shell
$ git reset --soft HEAD^
... 执行其他操作以获得正确的树 ...
$ git commit -c ORIG_HEAD
```

但也可以用于修订合并提交。

如果你修改了已经发布的提交，你应该理解重写历史所可能产生的影响。（请参见 (1) 中的“RECOVERING FROM UPSTREAM REBASE”章节。）

#### `--no-post-rewrite`



跳过重写后的钩子（hook）。

`-i, --include`

在对目前暂存的内容进行提交之前，也将命令行中给出的路径的内容进行暂存。除非你正在完成一个冲突合并，否则通常不是你想要的操作。

`-o, --only`

通过获取命令行指定路径的更新后的工作树内容来创建提交，忽略任何已暂存其他路径的内容。如果命令行上提供了任何路径，这是 `git commit` 的默认操作模式，在这种情况下可以省略此选项。如果此选项与 `--amend` 一起指定，则不需要指定路径，这可以用于修改上一次提交，而不提交已经暂存的更改。

`-u[<mode>], --untracked-files[=<mode>]`

显示未跟踪的文件。

`mode` 参数是可选的（默认为 `all`），用于指定处理未跟踪文件的方式；当不使用 `-u` 时，默认值为 `normal`，即显示未跟踪的文件和目录。

可能的选项有：

- `no` - 不显示未跟踪的文件

- `normal` - 显示未跟踪的文件和目录

- `all` - 也显示未跟踪目录中的单个文件。

默认值可以使用 (1) 中记录的 `status.showUntrackedFiles` 配置变量进行更改。

`-v, --verbose`

在 HEAD 提交与提交消息模板底部将提交的内容之间显示统一差异（unified diff），以帮助用户通过提醒提交包含了哪些更改来描述提交。请注意，此差异输出的行开头没有 `#` 前缀。此差异不会成为提交消息的一部分。

如果指定两次，则额外显示将要提交的内容与工作树文件之间的统一差异，即已跟踪文件的未暂存更改。

`-q, --quiet`

静默输出提交摘要消息。

`--dry-run`

不创建提交，但显示将要提交的路径列表、将未提交且带有本地更改的路径以及未跟踪的路径。

`--status`

当使用编辑器准备提交消息时，在提交消息模板中包含 (1) 的输出。默认开启，但可用于覆盖配置变量 `commit.status`。

`--no-status`

当使用编辑器准备默认提交消息时，不在提交消息模板中包含 (1) 的输出。

`-S[<keyid>], --gpg-sign[=<keyid>]`

对提交进行 GPG 签名。

`--no-gpg-sign`

取消 `commit.gpgSign` 配置变量，该变量强制对每个提交进行签名。

`--`

不再将任何参数解释为选项。

`<file>...`

当命令行上给出文件时，命令将提交命名文件的内容，而不记录已暂存的更改。这些文件的内容也被暂存到在之前暂存内容的基础上，用于下一次提交。

## 日期格式

`GIT_AUTHOR_DATE`、`GIT_COMMITTER_DATE` 环境变量和 `--date` 选项支持以下日期格式：

### Git 内部格式

格式为 `<unix timestamp> <time zone offset>`，其中 `<unix timestamp>` 是自 Unix 纪元以来的秒数，`<time zone offset>` 是相对于 UTC 的正负偏移量。例如，CET（比 UTC 早 2 小时）为 `+0200`。

### RFC 2822

RFC 2822 描述的标准邮件格式，例如 `Thu, 07 Apr 2005 22:13:13 +0200`。

### ISO 8601

ISO 8601 标准指定的时间日期，例如 `2005-04-07T22:13:13`。解析器也接受空格代替 `T` 字符。

**注意**

此外，日期部分也接受以下格式：`YYYY.MM.DD`、`MM/DD/YYYY` 和 `DD.MM.YYYY`。

## 示例

在记录你自己的工作时，工作树中修改文件的内容会通过 `git add` 临时存储在名为“索引（index）”的暂存区。可以通过 `git reset HEAD -- <file>` 将文件恢复到上一次提交的状态，但仅在索引中恢复而不在工作树中，这实际上撤销了 `git add` 并防止该文件的更改参与下一次提交。在用这些命令增量构建好待提交的状态后，使用 `git commit`（不带任何路径参数）来记录目前为止已暂存的内容。这是该命令最基本的形式。示例：

```
$ edit hello.c $ git rm goodbye.c $ git add hello.c $ git commit
```

与其在每次单独更改后暂存文件，你可以告诉 `git commit` 注意你工作树中被跟踪内容的文件的更改，并为你执行相应的 `git add` 和 `git rm`。也就是说，如果你的工作树中没有其他更改，此示例与之前的示例相同：

```
$ edit hello.c $ rm goodbye.c $ git commit -a
```

`git commit -a` 命令首先查看你的工作树，注意到你修改了 `hello.c` 并删除了 `goodbye.c`，然后为你执行必要的 `git add` 和 `git rm`。

在暂存许多文件的更改后，你可以通过向 `git commit` 传递路径来更改记录更改的顺序。给出路径时，命令创建一个记录以下内容的提交：

```
$ edit hello.c hello.h $ git add hello.c hello.h $ git commit Makefile
```

这将创建一个记录 `Makefile` 更改的提交。`hello.c` 和 `hello.h` 的更改未包含在生成的提交中。然而，它们仍然处于暂存状态，只是被留下了。在上述序列之后，如果你执行 `git commit`

## 讨论

虽然不是强制的，但最好用一个简短的（少于 50 个字符）行概述更改，后面跟着一个空行，然后是更详细的描述。提交消息中第一个空行之前的文本被视为提交标题，该标题在整个 Git 中都会使用。例如，(1) 将提交转换为邮件，它使用主题行作为标题，并将提交的其他部分作为正文。

在核心层面，Git 与字符编码无关。

在索引和树对象中记录的路径名被视为未解释的非空字节序列。(2) 返回的内容是用于记录并与 Git 跟踪的数据进行比较的内容，而这些数据预期是 (2) 和 (2) 接受的内容。不存在路径名编码转换。

尽管我们鼓励提交日志信息使用 UTF-8 编码，但核心部分和 Git Porcelain 工具（Porcelain）在设计上并未强制项目使用 UTF-8。如果某个项目的所有参与者认为使用遗留编码更方便，Git 并不禁止。然而，有几点需要注意。

1. 如果提供的提交日志信息看起来不像是有效的 UTF-8 字符串，`git commit` 和 `git commit-tree` 会发出警告，除非你显式说明你的项目使用遗留编码。这种方法是在 `.git/config` 文件中设置 `i18n.commitencoding`，如下：

```
[i18n] commitencoding = ISO-8859-1
```

使用上述设置创建的提交对象会在其编码头部中记录 `i18n.commitencoding` 的值。为了之后查看的人，缺少此头部意味着提交日志信息是用 UTF-8 编码的。

2. `git log`、`git show`、`git blame` 等命令会查看提交对象的编码头部，除非另有指定，否则会尝试将日志信息重新编码为 UTF-8。你可以通过 `.git/config` 文件中的 `i18n.logoutputencoding` 来指定所需的输出编码，如下：

```
[i18n] logoutputencoding = ISO-8859-1
```

如果你没有此配置变量，将使用 `i18n.commitencoding` 的值。

请注意，我们刻意选择在执行提交时不重新编码提交日志信息，以便在提交对象级别强制使用 UTF-8，因为重新编码为 UTF-8 并不一定是一个可逆的操作。

## 环境与配置变量

用于编辑提交日志信息的编辑器将从 `GIT_EDITOR` 环境变量、`core.editor` 配置变量、`VISUAL` 环境变量或 `EDITOR` 环境变量中选择（按此顺序）。详情请见 (1)。

## 钩子 (HOOKS)

此命令可以运行 `commit-msg`、`prepare-commit-msg`、`pre-commit` 和 `post-commit` 钩子。更多信息请见 (5)。

## 文件 (FILES)

`$GIT_DIR/COMMIT_EDITMSG`

该文件包含正在进行提交的提交信息。如果 `git commit` 在创建提交之前由于错误退出，用户提供的任何提交信息（例如在编辑器会话中）将在此文件中可用，但会被下一次调用 `git commit` 时覆盖。

## 参见 (SEE ALSO)

(1), (1), (1), (1), (1)

---

# GIT-CONFIG

## 名称

`git-config` - 获取和设置仓库或全局选项

## 概要

```
git config [<file-option>] [type] [-z|--null] name [value [value_regex]]
git config [<file-option>] [type] --add name value
git config [<file-option>] [type] --replace-all name value [value_regex]
git config [<file-option>] [type] [-z|--null] --get name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-all name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-regexp name_regex [value_regex]
git config [<file-option>] [type] [-z|--null] --get-urlmatch name URL
git config [<file-option>] --unset name [value_regex]
git config [<file-option>] --unset-all name [value_regex]
git config [<file-option>] --rename-section old_name new_name
git config [<file-option>] --remove-section name
git config [<file-option>] [-z|--null] -l | --list
git config [<file-option>] --get-color name [default]
git config [<file-option>] --get-colorbool name [stdout-is-tty]
git config [<file-option>] -e | --edit
```

## 描述

你可以使用此命令查询/设置/替换/取消选项。名称实际上是由点分隔的节（section）和键（key），值将被转义。

可以使用 `--add` 选项向选项中添加多行。如果你想更新或取消一个可能出现在多行的选项，则提供一个 POSIX 正则表达式 `value_regex`。只有匹配正则表达式的现有值会被更新或取消。如果你想处理**不**匹配正则表达式的行，只需在前面加一个感叹号（参见“示例”部分）。

类型指定符可以是 `--int` 或 `--bool`，以使 `git config` 确保变量为给定的类型并将值转换为规范形式（`int` 为简单的数字，`bool` 为 "true" 或 "false" 字符串），或者是 `--path`，它会执行一些路径扩展（见下文 `--path`）。如果没有传递类型指定符，则不会对值进行任何检查或转换。

读取时，默认从系统、全局和仓库本地配置文件读取值，可以使用 `--system`、`--global`、`--local` 和 `--file <filename>` 选项告诉命令从该位置读取（参见“文件”部分）。

写入时，默认从系统、全局和仓库本地配置文件读取值，可以使用 `--system`、`--global`、`--local` 和 `--file <filename>` 选项告诉命令从该位置写入。

此命令在发生以下情况将失败并返回非零状态：

1. 节无效，
2. 未提供节或名称，
3. 配置文件无效，
4. 未找到键，
5. 尝试取消不存在的选项，
6. 尝试取消多行，
7. 使用了无效的正则表达式。

如果成功，命令返回退出代码 0。

### 选项

`--replace-all` 默认行为最多替换一行。这将替换匹配键的所有行。

`--add` 向选项添加新行，不更改任何现有值。

`--get` 获取给定键的值。如果未找到键则返回错误 1，如果找到多个值则返回最后一个。

`--get-all` 类似于 `get`，但如果值的数量不等于一个则不失败。

`--get-regexp` 类似于 `get-all`，但将名称解释为正则表达式并输出键名。正则表达式匹配目前是区分大小写的，并针对规范化后的键进行，其中节名会被小写，但子节名不会。

`--get-urlmatch name URL` 当给定双部分名称 `section.key` 时，返回 `<url>` 部分匹配给定 URL 的值（如果不存在此类键，则使用 `section.key` 作为备用）。当仅提供节作为名称时，对该节中的所有键执行操作。

`--global` 写入时：写入全局 `~/.gitconfig` 而不是仓库的 `.git/config`；如果 `$XDG_CONFIG_HOME/git/config` 文件存在而 `~/.gitconfig` 文件不存在，则写入该文件。读取时：仅从全局 `~/.gitconfig` 和 `$XDG_CONFIG_HOME/git/config` 读取，而不是所有可用文件。

`--system` 写入时：写入系统级 `$(prefix)/etc/gitconfig` 而不是仓库的 `.git/config`。读取时：仅从系统级 `$(prefix)/etc/gitconfig` 读取，而不是所有可用文件。

`--local` 写入时：写入仓库的 `.git/config` 文件。这是默认行为。读取时：仅从仓库的 `.git/config` 读取，而不是所有可用文件。

`-f config-file`, `--file config-file` 使用指定的配置文件代替 `GIT_CONFIG` 指定的文件。

`--blob blob` 类似于 `--file` 但使用指定的 blob 代替文件。例如，你可以使用 `master:.gitmodules` 从 `master` 分支的 `*.gitmodules` 文件读取值。参见 (7) 中的“指定修订”部分以获取更完整的 blob 名称拼写列表。

`--remove-section` 从配置文件中删除指定的节。

`--rename-section` 将给定的部分重命名为新名称。

`--unset` 从配置文件中删除匹配键的行。

`--unset-all` 从配置文件中删除所有匹配该键的行。

`-l, --list` 列出配置文件中设置的所有变量。

`--bool` `git config` 将确保输出为 "true" 或 "false"。

`--int` `git config` 将确保输出为一个简单的十进制数字。配置文件中可选的值后缀 `k`、`m` 或 `g` 会导致该值在输出前乘以 1024、1048576 或 1073741824。

`--bool-or-int` `git config` 将确保输出符合上述描述的 `--bool` 或 `--int` 格式之一。

`--path` `git-config` 将将开头的 `~` 展开为 `$HOME` 的值，并将将 `~user` 展开为指定用户的家目录。此选项在设置值时无效（但你可以从命令行使用 `git config bla ~/` 来让你的 shell 执行展开）。

`-z, --null` 对于所有输出值和/或键的选项，值始终以空字符结尾（而不是换行符）。使用换行符作为键和值之间的分隔符。这允许对输出进行安全解析，而不会因为值中包含换行符而产生混淆。

`--get-colorbool name [stdout-is-tty]` 查找 `name` 的颜色设置（例如 `color.diff`）并输出 "true" 或 "false"。`stdout-is-tty` 应该是 "true" 或 "false"，且在当配置说明为 "auto" 时会考虑它。如果缺少 `stdout-is-tty`，则检查命令本身的标准输出，如果需要使用颜色，则以状态 0 退出，否则以状态 1 退出。当 `name` 的颜色设置未定义时，命令将使用 `color.ui` 作为回备。

`--get-color name [default]` 查找为 `name` 配置的颜色（例如 `color.diff.new`）并将其作为 ANSI 颜色转义序列输出到标准输出。如果没有为 `name` 配置颜色，则改为使用可选的默认参数。

`-e, --edit` 打开编辑器修改指定的配置文件；可以是 `--system`、`--global` 或仓库（默认）。

`--[no-]includes` 在查找值时尊重配置文件中的 `include.*` 指令。默认开启。

## 文件 (FILES)

如果没有通过 `--file` 显式设置，有四个文件 `git config` 会在其中搜索配置选项：

`$(prefix)/etc/gitconfig`

系统级配置文件。

`$XDG_CONFIG_HOME/git/config`

第二个用户特定的配置文件。如果 `$XDG_CONFIG_HOME` 未设置或为空，则将使用 `$HOME/.config/git/config`。在此文件中设置的任何单值变量都将被 `~/.gitconfig` 中的内容覆盖。如果你有时使用旧版本的 Git，那么不创建此文件是一个好主意，因为对该文件的支持最近才添加的。

`~/.gitconfig`

用户特定的配置文件。也称为全局（global）配置文件。

`$GIT_DIR/config`

仓库特定的配置文件。



如果没有提供进一步的选项，所有读取选项将读取所有这些可用文件。如果全局或系统级配置文件不可，它们将被忽略。如果仓库配置文件不可或不可读，`git config` 将以非零错误代码退出。然而，在上述两种情况下都不会发布错误消息。

文件按照上述顺序读取，最后找到的值优于较早读取的值。当取多个值时，将使用来自所有文件中该键的所有值。

默认情况下，所有写入选项将写入仓库特定的配置文件。请注意，这也会影响如 `--replace-all` 和 `--unset` 等选项。`git config` 每次只会更改一个文件。

你可以通过命令行选项或环境变量来覆盖这些规则。`--global` 和 `--system` 选项将将使用的文件限制为全局或系统级文件。`GIT_CONFIG` 环境变量具有类似的效果，但你可以指定任何所需的文件名。

## 环境 (ENVIRONMENT)

`GIT_CONFIG`

从给定的文件而不是 `.git/config` 获取配置。使用 `--global` 选项将其强制指向 `~/.gitconfig`。使用 `--system` 选项将其强制指向 `$(prefix)/etc/gitconfig`。

`GIT_CONFIG_NOSYSTEM`

是否跳过从系统级 `$(prefix)/etc/gitconfig` 文件读取设置。详情请见 (1)。

另请参见“文件 (FILES)”章节。

## 示例 (EXAMPLES)

假设有一个如下 `.git/config`：

```
# # 这是配置文件，其中 # 字符 '#' 或 ';' 字符表示 # 注释 #
; 核心变量 [core] ; 不要信任文件模式 filemode = false
; 我们的差分算法 [diff] external = /usr/local/bin/diff-wrapper renames = true
; 代理设置 [core] gitproxy=proxy-command for kernel.org gitproxy=default-proxy ; 针对其余所有
; HTTP [http] sslVerify [http ""] sslVerify = false cookieFile = /tmp/cookie.txt
```

你可以通过以下命令将 `filemode` 设置为 `true`：

```
% git config core.filemode true
```

假设的代理命令条目实际上有一个后缀，用于区分它们适用于什么 URL。以下是更改 `name` 的方法：

（注：由于原文示例部分似乎被截断或重复，已按逻辑完整翻译）

该文件由节和变量组成。节以方括号中的节名称开始，并持续到下一个节开始。节名称不区分大小写。节名称中仅允许出现字母、数字、`-` 和 `.`。每个变量必须属于某个节，这意味着在变量的第一个设置之前必须有一个节头部。

节可以进一步划分为子节。要开始一个子节，请在节头部中将其名称放在双引号中，并与节名之间用空格隔开，如下例：

`[section "subsection"]`

子节名称区分大小写，并且可以包含换行符以外的任何字符（双引号 `"` 和反斜杠 `\` 可以通过转义为 `\"` 和 `\\` 来包含）。节头部不能跨多行。变量可以直接属于一个节，也可以属于给定的子节。如果你有了 `[section "subsection"]`，则你可以有 `[section]`，但没有必要这样做。

还有一个已弃用的 `[section.subsection]` 语法。在这种语法下，子节名称会被转换为小写，并且同样进行区分大小写的比较。这些子节名称遵循的限制与节名称相同。

所有其他行（以及节头部之后的行剩余部分）都被识别为设置变量，格式为 `name = value`（或仅为 `name`，这是变量为布尔值 `"true"` 的简写）。变量名不区分大小写，仅允许字母、数字和 `-`，并且必须以字母开头。

定义值的行可以通过以 `;` 结尾来延续到下一行，反引号（此处）和行结束符会被剥离。`name =` 之后的前导空格、第一个注释字符 `#` 或 `;` 之后的行剩余部分以及行的尾部空格会被丢弃，除非它们被包含在双引号内。值内部的空格将原样保留。

在双引号内部，双引号 `"` 和反斜杠 `\` 字符必须进行转义：使用 `\"` 表示 `"`，使用 `\\` 表示 `\`。

除了 `\"` 和 `\\` 之外，还识别以下转义序列：`\n` 表示换行符 (NL)，`\t` 表示水平制表符 (HT, TAB)，以及 `\b` 表示退格 (BS)。其他字符转义序列（包括八进制转义序列）都是无效的。

### Includes

你可以通过将特殊的 `include.path` 变量设置为要包含的文件名，从另一个文件中包含配置文件。被包含的文件立即展开，就像其内容在包含指令的位置被找到一样。如果 `include.path` 变量的值是相对路径，则该路径被认为相对于发现包含指令的配置文件。`include.path` 的值受波浪号扩展：`~/` 扩展为 `$HOME` 的值，`~user/` 扩展为指定用户的家目录。示例见下文。

### Example

```bash
# 核心变量 [core] ; 不要信任文件模式 filemode = false
# 我们的差异算法 [diff] external = /usr/local/bin/diff-wrapper renames = true
[branch "devel"] remote = origin merge = refs/heads/devel
# 代理设置 [core] gitProxy="ssh" 用于 "kernel.org" gitProxy=default-proxy ; 用于其他部分
[include] path = /path/to/foo.inc ; 通过绝对路径包含 path = foo ; 相对于当前文件路径扩展 "foo"
```

### Values

`include.path` 变量的值是一个相对路径，该路径被认为相对于发现包含指令的配置文件。`include.path` 的值受波浪号扩展：`~/` 扩展为 `$HOME` 的值，`~user/` 扩展为指定用户的家目录。

定义值的行可以通过以 `;` 结尾来延续到下一行，反引号和行结束符会被剥离。`name =` 之后的前导空格、第一个注释字符 `#` 或 `;` 之后的行剩余部分以及行的尾部空格会被丢弃，除非它们被包含在双引号内。值内部的空格将原样保留。

在双引号内部，双引号 `"` 和反斜杠 `\` 字符必须进行转义：使用 `\"` 表示 `"`，使用 `\\` 表示 `\`。

除了 `\"` 和 `\\` 之外，还识别以下转义序列：`\n` 表示换行符 (NL)，`\t` 表示水平制表符 (HT, TAB)，以及 `\b` 表示退格 (BS)。其他字符转义序列（包括八进制转义序列）都是无效的。

### Variables

注意此列表并不完整的。对于特定命令的变量，你将在手册页中找到更详细的描述。

其他 git 相关的工具可能并在使用自己的变量。在发明新变量时，请确保它们的名称与 Git 本身使用的冲突，并在文档中描述它们。

所有 `advice` 变量默认认为 `true`，你可以通过将这些变量设置为 `false` 来告诉 Git 你不需要帮助：

### updateRejected

如果你想将此变量设置为 `false`，则同时禁用 `pushNonCurrent`、`pushNonMatching`、`pushAlreadyExists`、`pushFetchFirst` 和 `pushNeedsForce`。

`pushNonCurrent`

当 `(1)` 由于当前分支的非快进更新（non-fastforward update）失败时显示的建议。

`pushNonMatching`

当你运行 `(1)` 并显式推送 `matching refs`（即你使用了不是你当前分支的 `refspec`）并导致非快进错误时显示的建议。

# core.fileMode

告知 Git 是否尊重工作区中文件的可执行位。

某些文件系统在检出被标记为可执行的文件时会丢失可执行位，或者在检出带有可执行位的非可执行文件时加上该执行位。(1) 或 (1) 会探测文件系统以查看其是否能正确处理执行位，并根据需要自动设置此变量。

然而，仓库可能位于一个能够正确处理文件模式的文件系统上，该变量在创建时被设置为 `true`，但随后可能会从另一个会丢失文件模式的环境访问（例如：通过 CIFS 挂载 ext4，或者使用 Git for Windows 或 Eclipse 访问由 Cygwin 创建的仓库）。在这种情况下，可能需要将此变量设置为 `false`。详见 (1)。

默认值为 `true`（当配置文件中未指定 `core.filemode` 时）。

# core.ignoreCase

如果为 `true`，此选项将启用各种变通方法，使 Git 在不支持大小敏感的文件系统（如 FAT）上运行得更好。例如，如果目录列表发现了 `makefile` 而 Git 期望 `Makefile`，Git 将假设它们实际上是同一个文件，并继续将其记录为 `Makefile`。

默认值为 `false`，但在创建仓库时，(1) 或 (1) 会探测并在适当的情况下将 `core.ignoreCase` 设置为 `true`。

# core.precomposeUnicode

此选项仅供 Mac OS 版本的 Git 实现使用。当 `core.precomposeUnicode=true` 时，Git 会撤销 Mac OS 对文件名进行的 Unicode 分解。这在在 Mac OS 与 Linux 或 Windows 之间共享仓库时非常有用。（需要 Git for Windows 1.7.10 或更高版本，或者 cygwin 1.7 下的 Git）。当为 `false` 时，Git 将完全透明地处理文件名，这与旧 Git 兼容。

# core.protectHFS

如果设置为 `true`，则不允许检出在 HFS+ 文件系统上被认为等同于 `.git` 的路径。在 Mac OS 上默认为 `true`，在其他地方默认为 `false`。

# core.protectNTFS

如果设置为 `true`，则不允许检出会导致 NTFS 文件系统出现问题的路径，例如与 8.3“短”名称的冲突。在 Windows 上默认为 `true`，在其他地方默认为 `false`。

# core.trustctime

如果为 `false`，则忽略索引和工作区之间的 ctime 差异；当 inode 修改时间经常被 Git 外部程序修改（如文件系统爬虫和某些备份系统）时非常有用。详见 (1)。默认认为 `True`。

# core.checkStat

确定索引和工作区之间匹配哪些 stat 字段。用户可以将其设置为 `default` 或 `minimal`。`Default`（或显式的 `default`）会检查所有字段，包括 `mtime` 和 `ctime` 的亚秒部分。

# core.quotePath

输出路径的命令（例如 `ls-files`, `diff`）在没有给出 `-z` 选项时，将通过双引号对包裹路径并使用反斜杠对路径中的“异常”字符进行引用，方式类似于 C 源代码中字符串的引用方式。如果此变量设置为 `false`，高于 `0x80` 的字节将不会被引用，而是原样输出。注意，无论此变量如何设置，双引号、反斜杠和控制字符在不使用 `-z` 的情况下始终会被引用。

# core.eol

设置工作目录中使用的行结束符类型。默认是 `auto`，使用平台的原生行结束符。替代方案有 `lf`、`crlf` 和 `native`。更多信息见 (5)。

# core.safecrlf

如果为 `true`，防止 Git 在检出文件时将 CRLF 转换为 LF。如果你希望工作区中使用 CRLF 行结束符而仓库中不是，这非常有用。默认值为 `false`。

# core.autocrlf

将此变量设置为 `true` 几乎与将所有文件的文本属性设置为 `auto` 相同，只是文本文件无法保证在仓库中被归一化。如果你希望目录中使用 CRLF 行结束符，请使用此设置。此变量可以设置为 `input`，在这种情况下不进行输出转换。

# core.symlinks

如果为 `false`，符号链接将被检出为包含链接文本的小纯文件。这对于 FAT 等不支持符号链接的文件系统非常有用。

默认值为 `true`，但在创建仓库时，(1) 或 (1) 会探测并在适当的情况下将 `core.symlinks` 设置为 `false`。

# core.gitProxy

一个“代理命令”，用于在使用 Git 协议获取数据时执行（如 `command host port`），而不是直接与远程服务器建立连接。如果变量值为 `COMMAND for DOMAIN` 格式，则该命令仅适用于以指定域名字符串结尾的主机。此变量可以设置多次，并按给定顺序进行匹配；第一个匹配获胜。

可以通过环境变量 `GIT_PROXY_COMMAND` 覆盖（其始终全局适用，没有特殊的 `for` 处理）。

可以使用特殊字符串 `none` 作为代理命令，以指定对特定的域名模式不使用代理。这对于排除防火墙内部服务器使用代理非常有用，同时对外部域名使用通用代理。

# core.ignoreStat

如果为 `true`，Git 将避免使用 `lstat()` 调用来检测文件是否更改，而是通过对那些在索引和工作区中更新完全相同的跟踪文件设置 `assume-unchanged` 位。当文件在 Git 外部被修改时，用户需要显式地暂存修改的文件（例如，参见 (1) 中的 *Examples* 部分）。Git 通常不会检测到这些文件的更改。这对于 `lstat()` 调用非常慢的系统（如 CIFS/Microsoft Windows）非常有用。

默认认为 `false`。

# core.preferSymlinkRefs

对于 `HEAD` 和其他符号引用文件，使用符号链接而不是默认的 `symref` 格式。这有时是为了与那些期望 `HEAD` 为符号链接的旧脚本工作。

### `core.bare`

如果为 `true`，则假设此仓库是 `bare`（裸仓库），并且没有与之关联的工作目录。如果是此类情况，许多需要工作目录的命令将被禁用，例如 `(1)` 或 `(1)`。

此设置在创建仓库时由 `(1)` 或 `(1)` 自动推断。默认情况下，以 `/.git` 结尾的仓库被认为不是裸仓库（`bare = false`），而所有其他仓库都被认为是裸仓库（`bare = true`）。

### `core.worktree`

设置工作树根目录的路径。如果设置了 `GIT_COMMON_DIR` 环境变量，则忽略 `core.worktree` 且不用于确定工作树的根目录。这可以通过 `GIT_WORK_TREE` 环境变量和 `--work-tree` 命令行选项覆盖。该值可以是绝对路径，也可以相对于 `.git` 目录的相对路径（该目录由 `--git-dir` 或 `GIT_DIR` 指定）。如果指定了 `--git-dir` 或 `GIT_DIR` 但未指定 `--work-tree`、`GIT_WORK_TREE` 和 `core.worktree`，则当前工作目录被视为工作树的顶层。

请注意，即使在该变量设置在目录的 `.git` 子目录的配置文件中时也会生效，且其值与后一个目录不同（例如，`/path/to/.git/config` 中的 `core.worktree` 被设置为 `/different/path`），这很可能是一个配置错误。在 `/path/to` 目录中运行 Git 命令仍将使用 `/different/path` 作为工作树的根目录，除非你清楚自己在做什么，否则可能会导致混惑（例如，你正在向不同于仓库通常工作树的位置创建相同索引的只读快照）。

### `core.logAllRefUpdates`

启用引用日志（reflog）。对引用 `<ref>` 的更新将记录到文件 `$GIT_DIR/logs/<ref>` 中，通过追加新的和旧 SHA-1、日期/时间以及更新原因，但仅在文件存在时进行。如果将此配置变量设置为 `true`，则会自动为分支头（即 `refs/heads/` 下）、远程引用（即 `refs/remotes/` 下）、备注引用（即 `refs/notes/` 下）以及符号引用 `HEAD` 创建缺失的 `$GIT_DIR/logs/<ref>` 文件。

此信息可以用于确定“2 天前”分支末端是哪个提交。

在关联了工作目录的仓库中，此值默认认为 `true`；在裸仓库中默认认为 `false`。

### `core.repositoryFormatVersion`

标识仓库格式和布局版本的内部变量。

### `core.sharedRepository`

当为 `group`（或 `true`）时，仓库可以在一个组内的多个用户之间共享（确保所有文件和对象对用户组可写）。当为 `all`（或 `world` 或 `everybody`）时，仓库除了对组共享外，对所有用户可读。当为 `umask`（或 `false`）时，Git 将使用由 `(2)` 报告的权限。当为 `0xxx`（其中 `0xxx` 为八进制数），仓库中的文件将具有此模式值。`0xxx` 将覆盖用户的 umask 值（而其他选项只会覆盖用户 umask 值的请求部分）。示例：`0660` 将使仓库对所有者和组可读写，但其他人不可（除非 umask 等于 `0022`，则相当于 `group`）。`0640` 是一个组可读但组不可写的仓库。参见 `(1)`。默认认为 `false`。

### `core.warnAmbiguousRefs`



如果为`true`，如果你传递的引用名称具有歧义并可能匹配仓库中的多个引用，Git 将向你发出。默认认为`true`。

### `core.compression`

一个`-1..9`的整数，表示默认压缩级别。`-1`是 zlib 默认值。0 表示不压缩，`1..9`是各种速度/大小的权衡，9 最慢。如果设置，它将为其他压缩变量提供默认值，例如`core.looseCompression`和`pack.compression`。

### `core.looseCompression`

一个`-1..9`的整数，表示未在包文件中对象的压缩级别。`-1`是 zlib 默认值。0 表示不压缩，`1..9`是各种速度/大小的权衡。如果未设置，默认为`core.compression`。如果仍未设置，则默认为 1（最佳速度）。

### `core.packedGitWindowSize`

单次映射操作中映射到内存的包文件字节数。较大的窗口大小可能允许你的系统更快速地处理较少的大型包文件。较小的窗口大小由于增加了对操作系统内存管理器的调用而对性能产生不利影响，但在访问大量大型包文件时可能会提高性能。

如果在编译时设置了`NO_MMAP`，默认值为 1 MiB；否则，在 32 位平台上为 32 MiB，在 64 位平台上为 1 GiB。这对于所有用户/操作系统都是合理的。你可能不需要调整此值。

支持单位后缀`k`、`m`或`g`。

### `core.packedGitLimit`

从包文件同时映射到内存的最大字节数。如果 Git 需要访问超过此数量的字节来完成操作，它将取消映射现有区域以释放虚拟空间。

在 32 位平台上默认值为 256 MiB，在 64 位平台上默认值为 8 GiB。这对于所有用户/操作系统都是合理的，最大的项目除外。你可能不需要调整此值。

支持单位后缀`k`、`m`或`g`。

### `core.deltaBaseLimit`

为可能被多个差异对象引用的基对象保留的最大字节数。通过缓存解压后的基对象，Git 能够避免多次解压基对象。

在所有平台上默认值为 96 MiB。这对于所有用户/操作系统都是合理的，最大的项目除外。你可能不需要调整此值。

支持单位后缀`k`、`m`或`g`。

### `core.bigFileThreshold`

大于此大小的文件将进行压缩，但不尝试增量压缩。存储大文件可以避免过度内存使用，但代价是增加磁盘占用。此外，大于此大小的文件始终被视为二进制。

在所有平台上默认值为 512 MiB。对于大多数项目是合理的，因为源代码和其他文本文件仍然可以增量压缩，但较大的二进制文件不会。

支持单位后缀`k`、`m`或`g`。

### `core.excludesFile`

除了`.gitignore`（每目录）和`.git/info/exclude`外，Git 还会在此文件中查找不跟踪的文件模式。`~/`扩展为`$HOME`的值，`~user/`扩展为指定用户的家目录。其默认值为`$XDG_CONFIG_HOME/git/ignore`。如果`$XDG_CONFIG_HOME`未设置或为空，则使用`$HOME/.config/git/ignore`。参见`(5)`。

### `core.askPass`

某些交互式询问密码的命令（例如 svn 和 http 接口）可以被告知使用此变量指定的外部程序。可以通过`GIT_ASKPASS`环境变量覆盖。如果未设置，则回退到`SSH_ASKPASS`环境变量的值，或者使用简单的密码提示。外部程序将获得一个合适的提示作为命令行参数，并在 STDOUT 上写入密码。

### `core.attributesFile`

除了`.gitattributes`（每目录）和`.git/info/attributes`外，Git 还会在此文件中查找属性（参见`(5)`）。路径扩展方式与`core.excludesFile`相同。其默认值为`$XDG_CONFIG_HOME/git/attributes`。如果`$XDG_CONFIG_HOME`未设置或为空，则使用`$HOME/.config/git/attributes`。

### `core.editor`

如`commit`和`tag`等允许通过启动编辑器来编辑消息的命令，当此变量被设置且环境变量`GIT_EDITOR`未设置时，将使用该变量的值。详见`(1)`。

### `core.commentChar`

如`commit`和`tag`等允许编辑消息的命令，在处理时会将以此字符开头的行视为注释，并在编辑器返回后将其删除（默认值为`*#`）。

如果设置为`"auto"`，`git-commit`将选择一个不起始于现有提交消息中任何一行的首字符的字符。

### `core.packedRefsTimeout`

在尝试锁定`packed-refs`文件时重试的时间，以毫秒为单位。值`0`表示不重试；`-1`表示无限次尝试。默认值为`1000`（即重试 1 秒）。

### `sequence.editor`

`git rebase -i`用于编辑 rebase 指令文件时所使用的文本编辑器。该值意图在使用时由 shell 解释。可以通过环境变量`GIT_SEQUENCE_EDITOR`进行覆盖。如果未配置，则使用默认的提交消息编辑器。

### `core.pager`

Git 命令使用的文本查看器（例如`less`）。该值意图由 shell 解释。优先级顺序为`$GIT_PAGER`环境变量、然后是`core.pager`配置、然后`$PAGER`、最后是编译时选择的默认值（通常为`less`）。

当`LESS`环境变量未设置时，Git 会将其设置为`FRX`（如果已设置`LESS`环境变量，Git 将完全不更改）。如果你想选择性地覆盖 Git 对`LESS`的默认设置，可以将`core.pager`设置为例如`less -S`。Git 将其传递给 shell，shell 将最终命令翻译为`LESS=FRX less -S`。环境没有设置`S`选项，但命令行设置了，指示`less`裁剪长行。同样，将`core.pager`设置为`less -+F`将从命令行禁用环境变量指定的`F`选项，从而禁用`less`的“一屏即退出”行为。可以为特定命令专门激活某些标志：例如，将`pager.blame`设置为`less -S`可仅为`git blame`启用行裁剪。

同样，当`LV`环境变量未设置时，Git 将其设置为`-c`。你可以通过导出带有另一个值的`LV`或将`core.pager`设置为`lv +c`来覆盖此设置。

### `core.whitespace`

一个用逗号分隔的需要注意的常见空格问题列表。`git diff`将使用`color.diff.whitespace`高亮这些问题，而`git apply --whitespace=error`将它们视为错误。你可以以前缀`-`来禁用其中任何一个（例如`-trailing-space`）：

- `blank-at-eol`将行尾的末随空格视为错误（默认启用）。
- `space-before-tab`将行初始缩进部分紧邻制表符之前的空格字符视为错误（默认启用）。
- `indent-with-non-tab`将使用空格字符而非等效 tab 缩进的视为错误（默认禁用）。
- `tab-in-indent`将行初始缩进部分中的 tab 字符视为错误（默认禁用）。
- `blank-at-eof`将文件末尾添加的空行视为错误（默认启用）。
- `trailing-space`是涵盖`blank-at-eol`和`blank-at-eof`的简写。
- `cr-at-eol`将行尾的回车符视为行终止符的一部分，即：如果该回车符之前的字符不是空格，则`trailing-space`不会触发（默认禁用）。
- `tabwidth=<n>`告诉 tab 占用多少个字符位置；这对于`indent-with-non-tab`以及 Git 修复`tab-in-indent`错误时是相关的。默认 tab 宽度为`8`。允许的值为 1 到 63。

### `core.fsyncObjectFiles`

此布尔值将在写入对象文件时启用`fsync()`。

对于能够正确排序数据写入的文件系统，这完全是浪费精力和时间，但对于不使用日志的文件系统（传统的 UNIX 文件系统）或仅记录元数据而非文件内容的系统（OS X 的 HFS+, 或开启了 "data=writeback" 的 Linux ext3）可能有用。

### `core.preloadIndex`

为`git diff`等操作启用并行索引预加载。

这可以加速`git diff`和`git status`等操作，特别是在像 NFS 这样具有弱缓存语义且 IO 延迟相对较高的文件系统上。启用后，Git 将并行执行索引与文件系统数据的比较，允许 IO 堆叠。默认值为 true。

### `core.createObject`

你可以将其设置为`link`，在这种情况下，将使用硬链接随后删除源文件，以确保对象的创建不会覆盖已存在的对象。

在某些文件系统/操作系统的组合上，这是不可靠的。在此处将此配置设置设置为`rename`；然而，这将移除确保现有对象不会被覆盖的检查。

### `core.notesRef`

在显示提交消息时，同时也显示存储在给定 ref 中的 notes。该 ref 必须是完全限定的。如果给定的 ref 不存在，这不是错误，意味着不应打印 notes。

此设置默认值为`"refs/notes/commits"`，可以通过环境变量`GIT_NOTES_REF`进行覆盖。详见`(1)`。

### `core.sparseCheckout`

启用“稀疏检出”功能。更多信息请参阅`(1)`。

### `core.abbrev`

设置对象缩写的长度。如果未指定，许多命令将缩写为 7 位十六，这可能不足以保持名称的唯一性。

### `add.ignoreErrors`, `add.ignore-errors`（已弃）

告知`git add`在某些文件因错误无法添加时继续添加。等于`(1)`中的`--ignore-errors`选项。`add.ignore-errors`已弃，因为它不符合变量的命名规范。

### `alias.*`

`(1)`命令的别名。例如定义`alias.last = cat-file HEAD`后，调用`git last`等于`cat-file HEAD`。如果别名扩展以叹号开头，则被视为 shell 命令。例如定义`alias.new = !gitk --all --not-HEAD`，调用`git new`等于执行 shell 命令`gitk --all --not-HEAD`。注意 shell 命令将在仓库顶层目录执行，不一定是当前目录。`GIT_PREFIX`设置为原始目录下运行`git-parse --show-prefix`的返回值。详见`(1)`。参数通过空格分割，支持标准的 shell 转义。可以使用引号或反斜杠进行引用。

### `am.keepcr`

如果为 true，`git-am`在处理 mbox 格式的补丁时将带参数`--keep-cr`调用`git-mailsplit`。在这种情况下，`git-mailsplit`不会从`\r\n`中移除`\r`。可以通过命令行提供`--no-keep-cr`来覆盖。详见`(1),(1)`。

### `apply.ignoreWhitespace`

设置为`change`时，告知`git apply`忽略空格变化，类似于`--ignore-space-change`选项。设置为 no, none, never, false 时，`git apply`将尊重所有空格差异。详见`(1)`。

### `apply.whitespace`

告知`git apply`如何处理空格，类似于`--whitespace`选项。详见`(1)`。

### `branch.autoSetupMerge`

告知`git branch`和`git checkout`设置新分支，以便`(1)`能够从起点分支正确合并。注意，即使未设置此选项，也可以通过`--track`和`--no-track`选项按分支选择此行为。有效设置为：false --- 不进行自动设置；true --- 当起点是远程跟踪分支时进行自动设置；always --- 当起点是本地分支或远程跟踪分支时均进行自动设置。此选项默认值为 true。

### `branch.autoSetupRebase`

当使用`git branch`或`git checkout`创建一个追踪另一个分支的新分支时，此变量告诉 Git 设置 pull 为 rebase 模式而非 merge 模式（参见`branch.<name>.rebase`）。设置为`never`时，rebase 永远不会自动设置为 true。设置为`local`时，对于其他本地分支的跟踪分支，rebase 为 true。设置为`remote`时，对于远程追踪分支的跟踪分支，rebase 为 true。设置为`always`时，所有跟踪分支的 rebase 都设置为 true。关于如何设置分支以跟踪另一个分支的详情，请参见`branch.autoSetupMerge`。此选项默认值为`never`。

### `branch.<name>.remote`

在分支`<name>`上时，它告诉`git fetch`和`git push`从哪个远程获取内容/推送到哪个远程。推送的远程可以通过`remote.pushDefault`（针对所有分支）覆盖。当前分支的推送远程可以被`branch.<name>.pushRemote`进一步覆盖。如果没有配置远程仓库，或者你不在任何分支上，则获取默认为`origin`，推送默认为`remote.pushDefault`。此外，`.`（点）表示当前本地仓库（点仓库），请参见下文`branch.<name>.merge`的最后说明。

### `branch.<name>.pushRemote`

在分支`<name>`上时，它会覆盖推送时的`branch.<name>.remote`。它还会覆盖从分支`<name>`推送`remote.pushDefault`。当你从一个地方（例如你的上游） pull 并送到另一个地方（例如你自己的发布仓库）时，你可能希望设置`remote.pushDefault`指定所有分支的推送远程，并使用此选项覆盖特定分支。

### `branch.<name>.merge`

与`branch.<name>.remote`共同定义给定分支的上游分支。它告诉`git fetch`/`git pull`/`git rebase`要合并哪个分支，并可能影响`git push`（参见`push.default`）。在分支`<name>`中时，它告诉`git fetch`默认的 refspec 将在`FETCH_HEAD`中标记为合并。该值的处理方式类似于 refspec 的远程部分，并且必须与从`branch.<name>.remote`指定的远程获取的 ref 匹配。合并信息供`git pull`（它首先调用`git fetch`）查找用于合并的默认分支。如果没有此选项，`git pull`默认合并第一个获取的 refspec。指定多个值可以实现章鱼合并（octopus merge）。如果你希望设置`git pull`使从本地仓库中的另一个分支合并到`<name>`，你可以将`branch.<name>.merge`指向目标分支，并使用相对路径设置`branch.<name>.remote`为点。

### `branch.<name>.mergeOptions`

设置合并到分支`<name>`的默认选项。语法和支持的选项与`(1)`相同，但目前不支持包含空白字符的选项值。

### `branch.<name>.rebase`

设置为`true`时，在运行`git pull`时，将分支`<name>` rebase 在已获取的分支之上，而不是合并默认远程的默认分支。参见`pull.rebase`以以非特定特定分支的方式进行此操作。

设置为`preserve`时，会将`--preserve-merges`传递给`git rebase`，使得本地提交的合并提交不会在运行`git pull`时被扁平化。

**注意**：这是一个可能危险的操作；除非你理解其影响，否则**不要**使用它（详情参见`(1)`）。

### `branch.<name>.description`

分支描述，可以使用`git branch --edit-description`进行编辑。分支描述会自动添加到 format-patch 封页或 request-pull 摘要中。

### `browser.<tool>.cmd`

指定调用指定浏览器的命令。指定的将在 shell 中评估，并将 URL 作为参数传递。（参见`(1)`。）

### `browser.<tool>.path`

覆盖给定工具的路径，该路径可能用于浏览 HTML 帮助（参见`(1)`中的`*-w*`选项）或 gitweb 中的工作仓库（参见`(1)`）。

### `clean.requireForce`

布尔值，除非给出`-f`、`-i`或`-n`，否则`git-clean`什么都不做。默认值为`true`。

### `color.branch`

布尔值，用于启用/禁用`(1)`输出中的颜色。可以设置为`always`、`false`（或`never`）或`auto`（或`true`），在这种情况下，只有输出到终端时才会使用颜色。默认值为`false`。

### `color.branch.<slot>`

使用自定义颜色进行分支着色。`<slot>`是当前（`current`当前分支）、`local`（本地分支）、`remote`（refs/remotes/ 中的远程追踪分支）、`upstream`（上游跟踪分支）、`plain`（其他 ref）之一。

### `color.diff`



是否使用 ANSI 转义序列为补丁添加颜色。如果设置为 `always`，(1)、(1) 和 (1) 将为所有补丁使用颜色。如果设置为 `true` 或 `auto`，这些命令仅在输出到终端时才使用颜色。默认值为 `false`。

这不影响 (1) 或 `git-diff-` 管道命令。可以通过命令行上的 `--color[=<when]` 选项进行覆盖。

## `color.diff.<slot>`

使用自定义颜色进行差异着色。`<slot>` 指定补丁的哪个部分使用指定的颜色，它是以下之一：`context`（上下文文本 - `plain` 是其历史同义词）、`meta`（元数据）、`frag`（块头）、`func`（块头中的函数）、`old`（删除的行）、`new`（添加的行）、`commit`（提交头）或 `whitespace`（空白字符高亮）。

## `color.decorate.<slot>`

为 `git log --decorate` 输出使用自定义颜色。`<slot>` 分别为 `branch`、`remoteBranch`、`tag`、`stash` 对应本地分支、标签和 HEAD。

## `color.grep`

设置为 `always` 时，始终高亮匹配项。设置为 `false`（或 `never`）时，永不。设置为 `true` 或 `auto` 时，仅在输出到终端时使用颜色。默认值为 `false`。

## `color.grep.<slot>`

使用自定义颜色进行 grep 着色。`<slot>` 指定行的哪个部分使用指定的颜色，它是以下之一：`context`（使用 `-A`、`-B` 或 `-C` 时的上下文文本）、`filename`（使用 `-h` 时的文件名头部）、`function`（使用 `-p` 时的函数名）、`number`（使用 `-n` 时的行号头部）、`match`（同于 `matchContext` 和 `matchSelected`）、`matchContext`（上下文中的匹配文本）、`matchSelected`（选中行中的匹配文本）、`selected`（选中行中的非匹配文本）、`separator`（行字段间的分隔符（`:`）以及块间的分隔符（`--`））。

## `color.interactive`

设置为 `always` 时，对交互式提示和显示（如 `git-add-interactive` 和 `git-clean-interactive` 使用的）使用颜色。设置为 `false`（或 `never`）时，永不。设置为 `true` 或 `auto` 时，仅在输出到终端时使用颜色。默认值为 `false`。

## `color.interactive.<slot>`

为 `git add --interactive` 和 `git clean --interactive` 输出使用自定义颜色。`<slot>` 对于交互式命令中四种不同类型的正常输出，其为 `prompt`、`header`、`help` 或 `error`。

## `color.pager`

布尔值，在使用分页器时启用/禁用彩色输出（默认值 `true`）。

## `color.showBranch`

布尔值，用于启用/禁用 (1) 输出中的颜色。可以设置为 `always`、`false`（或 `never`）或 `auto`（或 `true`），在这种情况下，只有输出到终端时才会使用颜色。默认值为 `false`。

## `color.status`

布尔值，用于启用/禁用 (1) 输出中的颜色。可以设置为 `always`、`false`（或 `never`）或 `auto`（或 `true`），在这种情况下，只有输出到终端时才会使用颜色。默认值为 `false`。

## `color.status.<slot>`

使用自定义颜色进行状态着色。`<slot>` 是以下之一：`header`（状态消息的头部）、`added or updated`（已添加但未提交的文件）、`changed`（已更改但未添加到索引的文件）、`untracked`（未被 Git 跟踪的文件）、`branch`（当前分支）、`nobranch`（显示无分支警告的颜色，默认红色）或 `unmerged`（具有未合并的文件）。

## `color.ui`

此变量决定了 `color.diff` 和 `color.grep` 等变量的默认值，这些变量控制每个命令族颜色的使用。随着更多命令学习设置 `--color` 选项的默认值，其作用范围将会扩大。如果你希望 Git 命令除非显式通过其他配置或 `--color` 选项启用，否则不使用颜色，请将其设置为 `false` 或 `never`。如果你希望所有非机器读取的输出都使用颜色，请将其设置为 `always`；如果你希望此类输出在写入终端时使用颜色，请设置为 `true` 或 `auto`（这是 Git 1.8.4 之后的默认值）。

## `column.ui`

指定支持的命令是否以列的形式输出。该变量由由空格或逗号分隔的标记列表组成：

这些选项控制何时启用该功能（默认为 `never`）：

- `always`: 始终列出显示

- `never`: 始终不列出显示

- `auto`: 如果输出到终端，则列出显示

这些选项控制布局（默认为 `column`）。如果未指定 `always`、`never` 或 `auto` 中的任何一个，设置其中任何一个都意味着 `always`：

- `column`: 先填充列再填充行

- `row`: 先填充行再填充列

- `plain`: 以单列形式显示

最后，这些选项可以与布局选项（默认为 `nodense`）结合：

- `dense`: 创建不等宽的列以利用更多空间

- `nodense`: 创建等宽的列

## `column.branch`

指定 `git branch` 中是否以列的形式输出分支列表。详情请见 `column.ui`。

## `column.clean`

指定 `git clean -i` 中列表项的布局，该命令始终以列的形式显示文件和目录。详情请见 `column.ui`。

## `column.status`

指定 `git status` 中是否以列的形式输出未跟踪的文件。详情请见 `column.ui`。

## `column.tag`

指定 `git tag` 中是否以列的形式输出标签列表。详情请见 `column.ui`。

## `commit.cleanup`

此设置覆盖了 `git commit` 中 `--cleanup` 选项的默认值。详情请见 (1)。当你始终希望在日志消息中保留以注释字符 `#` 开头的行时，更改默认值非常有用，在这种情况下你会执行 `git config commit.cleanup whitespace`（注意，如果你这样做，将必须手动删除提交日志模板中以 `#` 开头的帮助行）。

## `commit.gpgSign`

布尔值，指定是否对所有提交进行 GPG 签名。在执行 rebase 等操作时使用此选项可能会导致大量提交被签名。使用代理可以避免多次输入 GPG 口令。

## `commit.status`

布尔值，用于在使用编辑器准备提交消息时，是否在提交消息模板中启用/禁用包含状态信息。默认为 `true`。

## `commit.template`

指定一个文件作为新提交消息的模板。`~/` 会被扩展为 `$HOME` 的值，`~user/` 会扩展为指定用户的家目录。

## `credential.helper`

指定在需要用户名或密码凭据时调用的外部助手程序；助手程序可以查询外部存储以避免提示用户输入凭据。详情请见 (7)。

## `credential.useHttpPath`

在获取凭据时，认为 `http` 或 `https` URL 的“路径”部分是重要的。默认为 `false`。更多信息请见 (7)。

## `credential.username`

如果为网络认证没有设置用户名，则默认使用此用户名。见下文 `credential.<context>.*` 和 (7)。

## `credential.<url>.*`

上述任何 `credential.*` 选项都可以选择性地应用到某些凭据。例如，`credential.` 将仅为到 example.com 的 https 连接设置默认用户名。关于 URL 如何匹配的详情请见 (7)。

## `diff.autoRefreshIndex`

在使用 `git diff` 与工作树文件进行比较时，不要将仅有状态（stat-only）的更改视为已更改。相反，静默运行 `git update-index --refresh` 以更新工作树中内容与索引内容匹配的路径的缓存信息。此选项默认为 `true`。注意，这只影响 `git diff` 的 Porcelain 命令，而不影响更底层的 `diff` 命令（如 `git diff-files`）。

## `diff.dirstat`

一个逗号分隔的 `--dirstat` 参数列表，用于指定 `--dirstat` 选项的默认行为为 (1) 等。默认值可以在命令行上覆盖（使用 `--dirstat=<param1,param2,...>`）。回退默认值（当未被 `diff.dirstat` 更改时）为 `changes,noncumulative,3`。可用参数如下：

- `changes`: 通过计算从源删除或向目标添加的行数来计算 dirstat 数字。这忽略了文件内部纯代码的移动量。换句话说，在文件中重新排列行不会像其他更改那样被计算。这是未提供参数时的默认行为。

- `lines`: 通过进行常规基于行的 diff 分析并累加删除/添加的行数来计算 dirstat 数字。（对于二进制文件，改为计算 64 字节块，因为二进制文件没有自然的行概念）。这是比 `changes` 行为更消耗性能的 `--dirstat` 行为，但它会将文件内重新排列的行视为与其他更改相同。生成的输出与你从其他 `--*stat` 选项获得的结果一致。

- `files`: 通过计算更改的文件数来计算 dirstat 数字。每个更改的文件在 dirstat 分析中权重相等。这是计算开销最低的 `--dirstat` 行为，因为它不需要查看文件内容。

- `cumulative`: 也会计算父目录中子目录的更改。注意，使用 `cumulative` 时，报告的百分比总和可能会超过 100%。可以通过 `noncumulative` 参数指定默认行为。

- `<limit>`: 整数参数指定阈值百分比（默认为 3%）。贡献小于此百分比的目录不会显示。示例：以下将统计文件，同时忽略占比小于 10% 的目录：`files,10,cumulative`。

## `diff.statGraphWidth`

限制 `--stat` 输出中图形部分的宽度。如果设置，适用于除 format-patch 外的所有命令。

## `diff.context`

生成具有 `<n>` 行上下文的 diff，而不是默认的 3。此值由 `-U` 选项覆盖。

## `diff.external`

设置了此配置，则不使用内部机制生成 diff，而是使用给定的命令。可以通过环境变量 `GIT_EXTERNAL_DIFF` 覆盖。该命令按照 (1) 中“git Diffs”部分描述的参数调用。注意：如果你只想对部分文件使用外部 diff 程序，你可能需要使用 (5)。

## `diff.ignoreSubmodules`

设置 `--ignore-submodules` 的默认值。注意，这只影响 `git diff` 的 Porcelain 命令，而不影响更底层的 `diff` 命令（如 `git diff-files`）。`git checkout` 在报告未提交更改时也遵循此设置。将其设置为 `all` 会禁用 `status.submoduleSummary` 设置时 `git commit` 和 `git status` 通常显示的子模块摘要，除非使用 `--ignore-submodules` 命令行覆盖。`git submodule` 命令不受此设置影响。

## `diff.mnemonicPrefix`

如果设置，`git diff` 将根据比较的内容使用与标准 "a/" 和 "b/" 不同的前缀对。当此配置生效时，反向 diff 输出也会交换前缀顺序：

```
git diff
比较索引和工作树；
git diff HEAD
比较提交和工作树；
git diff --cached
比较提交和索引；
git diff HEAD:file1 file2
比较对象和工作树实体；
git diff --no-index a b
比较两个非 git 对象 (1) 和 (2)。
```

## `diff.noprefix`

如果设置，`git diff` 将不显示任何源或目标前缀。

## `diff.orderFile`

指示在 diff 中对文件进行排序的文件，每行使用一个 shell glob 通配符。可以通过 `-O` 选项被 (1) 覆盖。

## `diff.renameLimit`

在执行复制/重命名检测时考虑的文件数量；等同于 `git diff` 选项 `-l`。

## `diff.renames`

告诉 Git 检测重命名。如果设置为任何布尔值，它将启用基础重命名检测。如果设置为 `copies` 或 `copy`，则也会检测复制。

## `diff.suppressBlankEmpty`

一个布尔值，用于抑制在每个空输出行之前打印空格的标准行为。默认值为 `false`。

## `diff.submodule`

指定子模块差异的显示格式。`log` 格式列出范围内的提交，就像 (1) 中的 `summary` 一样。`short` 格式仅显示范围开头和结尾的提交名称。默认值为 `short`。

## `diff.wordRegex`

一个 POSIX 扩展正则表达式，用于在执行逐词差异计算时确定什么是“单词”。匹配正则表达式的字符序列为“单词”，所有其他字符均为可忽略的空白。

## `diff.<driver>.command`

自定义 diff 驱动器命令。详见 (5)。

## `diff.<driver>.xfuncname`

diff 驱动器用于识别块头（hunk header）的正则表达式。也可以使用内置模式。详见 (5)。

## `diff.<driver>.binary`

将此选项设置为 `true`，可使 diff 驱动器将文件视为二进制文件。详见 (5)。

## `diff.<driver>.textconv`

diff 驱动器调用的命令，用于生成文件的文本转换版本。转换结果用于生成人类可读的 diff。详见 (5)。

## `diff.<driver>.wordRegex`

diff 驱动器用于拆分行内单词的正则表达式。详见 (5)。

## `diff.<driver>.cachetextconv`

将此选项设置为 `true`，可让 diff 驱动器缓存文本转换输出。详见 (5)。

## `diff.tool`

控制 (1) 使用哪种 diff 工具。此变量会覆盖 `merge.tool` 中配置的值。下方列表显示了有效的内置值。

- `araxis`

- `bc`

- `bc3`

- `codecompare`

- `deltawalker`

- `diffmerge`

- `diffuse`

- `ecmerge`

- `emerge`

- `gvimdiff`

- `gvimdiff2`

- `gvimdiff3`

- `kdiff3`

- `kompare`

- `meld`

- `opendiff`

- `p4merge`

- `tkdiff`

- `vimdiff`

- `vimdiff2`

- `vimdiff3`

- `winmerge`

- `xxdiff`

## `diff.algorithm`

选择 diff 算法。变体如下：

- `default`, `myers`: 基础贪心 diff 算法。目前是默认值。

- `minimal`: 花费额外时间确保产生尽可能小的 diff。

- `patience`: 在生成补丁时使用 "patience diff" 算法。

- `histogram`: 该算法扩展了 patience 算法以“支持低频共同元素”。

## `difftool.<tool>.path`

覆盖给定工具的路径。当你的工具不在 `PATH` 中时非常有用。

## `difftool.<tool>.cmd`

指定调用指定 diff 工具的命令。指定的命令在 shell 中求值，以下变量可用：`LOCAL` 设置为包含 diff 预镜像（pre-image）内容的临时文件名，`REMOTE` 设置为包含 diff 后镜像（post-image）内容的临时文件名。

## `difftool.prompt`

在每次调用 diff 工具之前进行提示。

## `fetch.recurseSubmodules`

此选项可以设置为布尔值或 `on-demand`（按需）。设置为布尔值会改变 `fetch` 和 `pull` 的行为：设置为 `true` 时无条件递归进入子模块，设置为 `false` 时完全不递归。当设置为 `on-demand`（默认值）时，`fetch` 和 `pull` 仅当父项目获取了更新子模块引用的提交时，才会递归进入已填充的子模块。

## `fetch.fsckObjects`

如果设置为 `true`，`git-fetch-pack` 将检查所有获取的对象。如果遇到格式错误的对象或损坏的链接，将中止。中止的结果仅产生悬空对象。默认值为 `false`。如果未设置，则使用 `transfer.fsckObjects` 的值。

## `fetch.unpackLimit`

如果通过 Git 原生传输获取的对象数量低于此限制，则对象将解压为松散对象文件。然而，如果接收的对象数量等于或超过此限制，则收到的 pack 将以 pack 形式存储，并添加任何缺失的 delta 基础。存储 push 的 pack 可以让操作更快完成，特别是在慢文件系统上。如果未设置，则使用 `transfer.unpackLimit` 的值。

## `fetch.prune`

如果为 `true`，`fetch` 的行为将等同于命令行上提供了 `--prune` 选项。另参见 `remote.<name>.prune`。

## `format.attach`



在`format-patch`中默认启用多部分附件。该值也可以是一个双引号字符串，将作为边界。详见 (1) 中的选项。

`format.numbered`

一个布尔值，用于启用或禁用补丁主题中的编号。默认值为`"auto"`，即在存在多个补丁时启用。通过设置为`"true"`或`"false"`可全局控制。详见 (1)。

`format.headers`

包含在补丁中的额外邮件头。

`format.to`, `format.cc`

包含在补丁中的额外收件人。详见 (1)。

`format.subjectPrefix`

`format-patch`默认输出带有`[PATCH]`前缀的文件。使用此变量更改前缀。

`format.signature`

`format-patch`默认输出包含 Git 签名。使用此变量更改。将此变量设置为空字符串 (`""`) 以抑制签名生成。

`format.signatureFile`

功能类似于`format.signature`，但使用该变量指定的文件内容的签名。

`format.suffix`

`format-patch`默认输出后缀为`.patch`的文件。使用此变量更改后缀（确保包含点）。

`format.pretty`

`log/show/changed`命令的默认格式化格式，见 (1)。

`format.thread`

`format-patch`的默认线程样式。可以是布尔值、shallow 或 deep。shallow 线程让每封邮件回复序列头部，头部从封面信、`--reply-to`和第一个补丁邮件中选择。deep 线程让每封邮件回复前一个。布尔值 true 等同于 shallow，false 则禁用线程。

`format.signOff`

一个布尔值，允许默认启用`format-patch`的`-s/--signoff`选项。**注意：** 在补丁中添加 Signed-off-by: 行是有意识的行为，意味着你证明权利以相同的开源许可提交此工作。详情请参见 *SubmittingPatches* 文档。

`format.coverLetter`

控制在调用`format-patch`时是否生成封面信的布尔值，此外还可以设置为`"auto"`，即仅在存在多个补丁时生成。

`filter.<driver>.clean`

在提交（checkin）时将工作区文件内容转换为 blob 的命令。详见 (5)。

`filter.<driver>.smudge`

在检出（checkout）时将 blob 对象内容转换为工作区文件的命令。详见 (5)。

当仓库中的松散对象大约超过此数量时，`git gc --auto`将将它们打包。某些 Porcelain 命令（用户界面命令）会定期调用此命令执行轻量级垃圾回收。默认值为`6700`。将其设置为`0`可禁用此项功能。

`gc.autoPackLimit`

当仓库中未被`.keep`文件标记的包数量超过此值时，`git gc --auto`将将它们合并为一个更大的包。默认值为`50`。将其设置为`0`可禁用此项功能。

`gc.autoDetach`

如果系统支持，则让`git gc --auto`立即返回并在后台运行。默认值为`true`。

`gc.packRefs`

在仓库中运行`git pack-refs`会导致其无法被`1.5.1.2`之前的 Git 版本通过`HTTP`等哑（传输协议进行克隆。此变量决定了`git gc`是否运行`git pack-refs`。可以将其设置为`notbare`以在所有非裸仓库中启用它，也可以设置为一个布尔值。默认值为`true`。

`gc.pruneExpire`

当运行`git gc`时，它将调用`prune --expire 2.weeks.ago`。通过此配置变量覆盖宽限期。可以使用值`"now"`来禁用此宽限期并始终立即清理不可达的对象。

`gc.pruneWorktreesExpire`

当运行`git gc`时，它将调用`prune --worktrees --expire 3.months.ago`。通过此配置变量覆盖宽限期。可以使用值`"now"`来禁用此宽限期并立即清理`$GIT_DIR/worktrees`。

`gc.reflogExpire`, `gc.<pattern>.reflogExpire`

`git reflog expire`会移除早于此时间的 reflog 条目；默认值为`90`天。如果中间带有`<pattern>`（例如`"refs/stash"`），则该设置仅适用于匹配`<pattern>`的引用引用。

`gc.reflogExpireUnreachable`, `gc.<ref>.reflogExpireUnreachable`

`git reflog expire`会移除早于此时间且从当前提交末端不可达的 reflog 条目；默认值为`30`天。如果中间带有`<pattern>`（例如`"refs/stash"`），则该设置仅适用于匹配`<pattern>`的引用引用。

`gc.rerereResolved`

当运行`git rerere gc`时，你之前解决的冲突合并记录将保留此时长。默认值为`60`天。

`gc.rerereUnresolved`

当运行`git rerere gc`时，你尚未解决的冲突合并记录将保留此时长。默认值为`15`天。

`gitcvs.commitMsgAnnotation`

将此字符串附加到每个提交消息。设置为空字符串以禁用此功能。默认值为`"via git-CVS emulator"`。

`gitcvs.enabled`

是否为该仓库启用了 CVS 服务器接口。

`gitcvs.logFile`

CVS 服务器接口日志文件路径，该文件会……记录各种内容。

`gitcvs.usecrlfattr`

如果为`true`，服务器将查找文件的换行符转换属性以确定要使用的`*k`模式。如果属性强制 Git 将文件视为文本，则`*k`模式将留空，以便 CVS 客户端将其视为文本。如果它们禁用了文本转换，则文件将设置为`*kb`模式，这将抑制客户端可能执行的任何换行符处理。如果属性无法确定文件类型，则使用`gitcvs.allBinary`。

`gitcvs.allBinary`

当`gitcvs.usecrlfattr`无法解析出正确的`*kb`模式时将使用此项。如果为`true`，所有未解析的文件将以`*kb`模式发送给客户端。这会导致客户端将其视为二进制文件，从而抑制其可能执行的任何换行符处理。或者，如果设置为`"guess"`，则将检查文件内容以判断其是否为二进制文件，类似于`core.autocrlf`。

`gitcvs.dbName`

`git-cvsserver`用于缓存从 Git 仓库派生的修订信息的数据库。具体含义取决于所使用的数据库驱动程序，对于`SQLite`（默认驱动程序），这是一个文件名。支持变量替换。可能不包含分号（`;`）。默认值：`"%Ggitcvs.%m.sqlite"`。

`gitcvs.dbDriver`

使用的 Perl DBI 驱动。你可以在此处指定任何可用的驱动，但它可能不起。`git-cvsserver`已通过`DBD::SQLite`进行测试，据报告支持`DBD::Pg`，且据报告**不支持**`DBD::mysql`。实验性功能。可能不包含双冒号（`:`）。默认值：`SQLite`。

`gitcvs.dbUser`, `gitcvs.dbPass`

数据库用户和密码。仅在设置了`gitcvs.dbDriver`时有用，因为`SQLite`没有数据库用户和/或密码的概念。`gitcvs.dbUser`支持变量替换。

`gitcvs.dbTableNamePrefix`

数据库表名前缀。附加在任何使用的数据库表名之前，允许单个数据库用于多个仓库。支持变量替换。任何非字母字符将被替换为下划线。

所有`gitcvs`变量除`gitcvs.usecrlfattr`和`gitcvs.allBinary`外，也可以指定为`gitcvs.<access_method>.<varname>`（其中`access_method`为`"ext"`之一）。

指定`git gui blame`原始位置检测中使用的阈值，以字母和数字字符计数。有关复制检测的更多信息，请参阅 (1) 手册。

`gui.blamehistoryctx`

当从`git gui blame`中调用“显示历史上下文”菜单项时，指定在 (1) 中显示的对应提交的历史上下文半径（以天为单位）。如果此变量设置为零，则显示整个历史。

`guitool.<name>.cmd`

指定当调用 (1) 工具菜单中的对应项时要执行的 shell 命令行。此选项对于每个工具都是必选的。该命令从工作目录的根目录执行，并在环境中，它将接收工具名称作为`GIT_GUITOOL`，当前选定文件的名称作为`FILENAME`，以及当前分支名称作为`CUR_BRANCH`（如果处于分离头指针状态，则`CUR_BRANCH`为空）。

`guitool.<name>.needsFile`

仅当在 GUI 中选择了差异（diff）时才运行该工具。这保证了`FILENAME`不为空。

`guitool.<name>.noConsole`

静默运行命令，不创建显示其输出的窗口。

`guitool.<name>.noRescan`

在工具执行完成后，不要重新扫描工作目录的变化。

`guitool.<name>.confirm`

在实际运行工具之前显示确认对话框。

`guitool.<name>.argPrompt`

向用户请求一个字符串参数，并通过`ARGS`环境变量将其传递给工具。由于请求参数意味着确认，因此如果启用了此项，`confirm`选项将无效。如果该选项设置为`true`、`yes`或`1`，则对话框将使用内置的通用提示；否则使用变量的精确值。

`guitool.<name>.revPrompt`

向用户请求一个有效的修订版本（revision），并设置`REVISION`环境变量。在其他方面，此选项与`argPrompt`类似，并可以与其一起使用。

`guitool.<name>.revUnmerged`

在`revPrompt`子对话框中仅显示未合并的分支。这对于类似于合并（merge）或变基（rebase）的工具有用，但不适用于切换（checkout）或重置（reset）等操作。

`guitool.<name>.title`

指定用于提示对话框的标题。默认值是工具名称。

`guitool.<name>.prompt`

指定显示在对话框顶部的通用提示字符串，位于`argPrompt`和`revPrompt`子部分之前。默认值包含实际命令。

`help.browser`

指定用于以`web`格式显示帮助的浏览器。请参阅 (1)。

`help.format`

覆盖 (1) 使用的默认帮助格式。支持`man`、`info`、`web`和`html`值。默认为`man`。`web`和`html`相同。

`help.autoCorrect`

在等待指定的十分分之一秒（0.1 秒）后，自动纠正并执行输入错误的命令。如果从输入的文本中可以推断出多条命令，则不执行任何操作。如果此选项的值为负数，将立即执行纠正后的命令。如果值为 0，则将显示命令但不执行。这是默认值。

`help.htmlPath`

指定 HTML 文档所在的路径。支持文件系统路径和 URL。当在以`web`格式显示帮助时，HTML 页面将以前该路径开头。默认认为你的 Git 安装的文档路径。

`http.proxy`

覆盖 HTTP 代理，通常使用`http_proxy`、`https_proxy`和`all_proxy`环境变量配置（参见 (1)）。可以按远程进行覆盖；参见`remote.<name>.proxy`。

`http.cookieFile`

包含之前存储的 cookie 行的文件，如果它们与服务器匹配，则应在 Git http 会话中使用。读取 cookie 的文件格式应该是纯 HTTP 头部或 Netscape/Mozilla cookie 文件格式（参见 (1)）。**注意**，除非设置了`http.saveCookies`，否则通过`http.cookieFile`指定的文件仅作为输入使用。

`http.saveCookies`

如果设置，将请求期间收到的 cookie 存储在`http.cookieFile`指定的文件中。如果未设置`http.cookieFile`，则无效。

`http.sslCipherList`

在协商 SSL 连接时使用的 SSL 加密套列表。可用的加密套取决于 libcurl 是基于 NSS 还是 OpenSSL 编译的，以及所使用的加密库的特定配置。在内部，这设置了`CURLOPT_SSL_CIPHER_LIST`选项；有关此列表格式的更多信息请参见 libcurl 文档。

可以通过`GIT_SSL_CIPHER_LIST`环境变量覆盖。要强制 git 使用 libcurl 的默认加密套列表并忽略任何显式的`http.sslCipherList`选项，将`GIT_SSL_CIPHER_LIST`设置为空字符串。

`http.sslVerify`

在通过 HTTPS 获取或推送时，是否验证 SSL 证书。可以通过`GIT_SSL_NO_VERIFY`环境变量覆盖。

`http.sslCert`

在通过 HTTPS 获取或推送时，包含 SSL 证书的文件。可以通过`GIT_SSL_CERT`环境变量覆盖。

`http.sslKey`

在通过 HTTPS 获取或推送时，包含 SSL 私钥的文件。可以通过`GIT_SSL_KEY`环境变量覆盖。

`http.sslCertPasswordProtected`

启用 Git 对 SSL 证书的密码提示。否则，如果证书或私钥已加密，OpenSSL 将多次提示用户。可以通过`GIT_SSL_CERT_PASSWORD_PROTECTED`环境变量覆盖。

`http.sslCAInfo`

在通过 HTTPS 或推送时，用于验证对方证书的文件。可以通过`GIT_SSL_CAINFO`环境变量覆盖。

`http.sslCAPath`

在通过 HTTPS 获取或推送时，包含 CA 证书文件的路径。可以通过`GIT_SSL_CAPATH`环境变量覆盖。

`http.sslTry`

通过常规 FTP 协议连接时尝试使用 SSL/TLS 和加密。如果 FTP 服务器出于安全原因需要，或者你希望安全连接，则可能需要。默认认为 false，因为可能会在配置错误的服务器上触发证书错误。

`http.maxRequests`

并行启动的 HTTP 请求数。可以通过`GIT_HTTP_MAX_REQUESTS`环境变量覆盖。默认 5。

`http.minSessions`

跨请求保留的 curl 会话数（跨槽）。在调用`http_cleanup()`之前不会通过`curl_easy_cleanup()`结束。如果没有`USE_CURL_MULTI`，此值将被限制为 1。默认值为 1。

`http.postBuffer`

智能传输在推送数据到远程系统时使用的缓冲区最大字节。对于大于此缓冲器的请求，将使用 HTTP/1.1 和分块传输（Transfer-Encoding: chunked），以避免在本地创建巨大的包文件。默认为 1 MiB，对于大多数请求足够。

`http.lowSpeedLimit, http.lowSpeedTime`

如果 HTTP 传输速度低于`http.lowSpeedLimit`超过`http.lowSpeedTime`秒，则中止传输。可以通过`GIT_HTTP_LOW_SPEED_LIMIT`和`GIT_HTTP_LOW_SPEED_TIME`环境变量覆盖。

`http.noEPSV`

禁用 curl 使用 EPSV ftp 命令的布尔值。这对于不支持 EPSV 模式的某些糟糕 ftp 服务器有用。可以通过`GIT_CURL_FTP_NO_EPSV`环境变量覆盖。默认值为 false（curl 将使用 EPSV）。

`http.userAgent`

向 HTTP 服务器呈现的 HTTP USER_AGENT 字符串。默认代表代表 Git 版本，例如 git/1.7.1。此选项允许你将此值覆盖为常用值，例如 Mozilla/4.0。这可能是必要的，例如通过限制 HTTP 连接到一组常用 USER_AGENT 字符串（但不包含 git/1.7.1 等）的防火墙连接时。可以通过`GIT_HTTP_USER_AGENT`环境变量覆盖。

上述任何`http.*`选项都可以选择性地应用于某些 URL。为了使配置键（config key）匹配 URL，配置键的每个元素将按照以下顺序与 URL 的对应元素进行比较：

1. 协议（Scheme）（例如此的`https`）：此字段在配置键和 URL 之间必须完全匹配。

2. 主机名/域名（例如此的`example.com`）：此字段在配置键和 URL 之间必须完全匹配。

3. 端口号（例如此的`8080`）：此字段在配置键和 URL 之间必须完全匹配。省略的端口号在匹配前会自动转换为该协议的正确默认值。

4. 路径（Path）（例如此的`repo.git`）：配置键的路径字段必须与 URL 的路径字段完全匹配，或者作为斜杠分隔路径元素的前缀匹配。这意味着路径为`foo/`的配置键会匹配 URL 路径`foo/bar`。前缀只能在斜杠（`/`）边界上进行匹配。较长的匹配具有更高的优先级（因此，路径为`foo/bar`的配置键比仅路径为`foo/`的配置键更匹配 URL 路径`foo/bar`）。



5. 用户名（User name）（例如此的 `user`）：如果配置键包含用户名，则它必须与 URL 中的用户名完全匹配。如果配置键没有用户名，则该配置键将匹配任何用户名（包括无）的 URL，但其优先级低于带有用户名的配置键。

上述列表按优先级递减排序；匹配配置键路径的 URL 优于匹配其用户名的 URL。例如，如果 URL 匹配配置键的 `will`，则其优先级将高于配置键的 `of`。

在尝试任何匹配之前，所有 URL 都会经过归一化处理（如果嵌入 URL 中的密码部分，在匹配时将始终被忽略），以便让拼写不同但等效的 URL 能够正确匹配。环境变量设置始终覆盖任何匹配结果。用于匹配的 URL 是直接传递给 Git 命令的 URL。这意味着任何由于重定向而访问的 URL 都不参与匹配。

### `i18n.commitEncoding`

存储提交信息时使用的字符编码。Git 本身并不关心，但这些信息是必要的，例如当从邮件导入提交时，或在 `gitk` 图形历史浏览器中（以及可能在未来的其他地方或其他界面中）。参见例如 (1)。默认为 `utf-8`。

### `i18n.logOutputEncoding`

在运行 `git log` 及其命令时，提交信息转换到的字符编码。

### `imap`

`imap` 部分中的配置变量见 (1)。

### `index.version`

指定初始化新索引文件时应使用的版本。这不会影响现有仓库。

### `init.templateDir`

指定从哪个目录拷贝模板。（参见 (1) 中的 "TEMPLATE DIRECTORY" 节。）

### `instaweb.browser`

指定用于在 gitweb 中浏览你的工作仓库的程序。参见 (1)。

### `instaweb.httpd`

用于在你的工作仓库上启动 gitweb 的 HTTP 守护进程命令行。参见 (1)。

### `instaweb.local`

如果为 `true`，由 (1) 启动的 Web 服务器将绑定到本地 IP（`127.0.0.1`）。

### `instaweb.modulePath`

(1) 使用的默认模块路径，用于替代 `/usr/lib/apache2/modules`。仅当 httpd 是 Apache 时才使用。

### `instaweb.port`

绑定到 gitweb httpd 的端口号。参见 (1)。

### `interactive.singleKey`

在交互式命令中，允许用户通过单键提供单字母输入（即无需按回车键）。目前用于 (1) 的 `--patch` 模式、(1)、(1)、(1) 和 (1)。注意，如果不支持便携按键输入，此设置将被默默忽略；需要 Perl 模块 `Term::ReadKey`。

### `log.abbrevCommit`

如果为 `true`，则让 (1)、(1) 和 (1) 假设使用 `--abbrev-commit`。你可以通过 `--no-abbrev-commit` 覆盖此选项。

### `log.date`

设置 `log` 命令的默认日期时间模式。为 `log.date` 设置值类似于使用 `git log` 的 `--date` 选项。可能的值有 `relative`、`local`、`default`、`iso`、`rfc` 和 `short`；详见 (1)。

### `log.decorate`

打印 `log` 命令显示出的任何提交的引用名（ref names）。如果指定 `short`，则不打印 `refs/heads/*`、`refs/tags/*` 和 `refs/remotes/*` 前缀。如果指定 `full`，则打印完整的引用名（包括前缀）。这与 `log` 命令的 `--decorate` 选项相同。

### `log.showRoot`

如果为 `true`，初始提交将显示为一个大的创建事件。这等同于相对于空树的 diff。通常隐藏根提交的工具如 (1) 或 (1) 现在将显示它。默认 `true`。

### `log.mailmap`

如果为 `true`，则让 (1)、(1) 和 (1) 假设使用 `--use-mailmap`。

### `mailinfo.scissors`

如果为 `true`，则让 (1)（因此是 (1)）默认行为类似于在命令行上提供了 `--scissors` 选项。激活时，此功能在 `=======` 之前移除 `8`。

### `mailmap.file`

mailmap 文件的位置。仓库根目录的 mailmap 首先加载，然后是此变量指向的 mailmap。

### `mailmap.blob`

类似于 `mailmap.file`，但考虑仓库中的 blob 值。如果给了 `mailmap.file` 和 `mailmap.blob`，则以 `mailmap.file` 为优先。在裸仓库中默认为 `HEAD:.mailmap`。在非裸仓库中，默认为空。

### `man.viewer`

指定可能用于帮助的程序。参见 (1)。

### `man.<tool>.cmd`

指定调用指定 man 查看器的命令。指定的命令将在 shell 中作为参数执行。（参见 (1)。）

### `man.<tool>.path`

覆盖指定工具的路径。参见 (1)。

### `merge.conflictStyle`

指定合并时将冲突块写入工作树文件的样式。默认值为 `merge`，它显示 `<<<<` 冲突标记、一侧的更改、`=======` 标记、另一侧的更改，以及 `>>>>` 标记。另一种样式 `diff3` 在 `=======` 之前添加 `||||||` 标记和原始文本。

### `merge.ff`

默认情况下，Git 在合并当前提交的后代提交时不会创建额外的合并提交。相反，当前分支的末端将进行快进。当设置为 `false` 时，此变量告诉 Git 在这种情况下创建一个额外的合并提交（相当于从命令行提供 `--no-ff` 选项）。当设置为 `only` 时，仅允许此类快进合并（相当于从命令行提供 `--ff-only` 选项）。

### `merge.branchdesc`

除了分支名外，在日志中填充与之关联的分支描述文本。默认 `false`。

### `merge.log`

除了分支名外，在日志中填充最多指定数量的来自合并提交的单行描述。默认 `false`，`true` 是 20 的同义词。

### `merge.renameLimit`

合并时进行重命名检测时考虑的文件数；如果没有指定，默认为 `diff.renameLimit` 的值。

### `merge.renormalize`

告诉 Git 仓库中文件的标准表示形式随时间发生了变化（例如，早期的提交记录了 CRLF 换行的文本文件，而最近的提交使用 LF 换行）。在这样的仓库中，Git 可以在执行合并之前将提交记录的数据转换为标准形式，以减少不必要的冲突。更多信息请参阅 (5) 中的“合并具有不同检入/检出属性的分支”章节。

### `merge.stat`

在合并结束时，是否打印 `ORIG_HEAD` 与合并结果之间的 diffstat。默认 `true`。

### `merge.tool`

控制由 (1) 使用哪种合并工具。其下方的列表显示了所有有效的内置值。任何其他值都被视为自定义合并工具，并且需要定义相应的 `mergetool.<tool>.cmd` 变量。

- `araxis`
- `bc`
- `bc3`
- `codecompare`
- `deltawalker`
- `diffmerge`
- `diffuse`
- `ecmerge`
- `emerge`
- `gvimdiff`
- `gvimdiff2`
- `gvimdiff3`
- `kdiff3`
- `meld`
- `opendiff`
- `p4merge`
- `tkdiff`
- `tortoisemerge`
- `vimdiff`
- `vimdiff2`
- `vimdiff3`
- `winmerge`
- `xxdiff`

### `merge.verbosity`

控制递归合并策略显示的输出量。Level 0 除了检测到冲突时的最终错误消息外不输出任何内容。Level 1 只输出冲突，Level 2 输出冲突和文件更改。Level 5 及以上输出调试信息。默认是 Level 2。可以通过环境变量 `GIT_MERGE_VERBOSITY` 进行覆盖。

### `merge.<driver>.name`

为自定义低级合并驱动程序定义一个可读的名称。详情参阅 (5)。

### `merge.<driver>.driver`

定义实现自定义低级合并驱动程序的命令。详情参阅 (5)。

### `merge.<driver>.recursive`

指定在公共祖先之间执行内部合并时使用的低级合并驱动程序名称。详情参阅 (5)。

### `mergetool.<tool>.path`

覆盖指定工具的路径。当你的工具不在 `PATH` 中时，这非常有用。

### `mergetool.<tool>.cmd`

指定调用指定合并工具的命令。指定的命令在 shell 中求值，并提供以下变量：`BASE` 是包含待合并文件公共基的临时文件名称（如果可用）；`LOCAL` 是包含当前分支文件内容的临时文件名称；`REMOTE` 是包含被合并分支文件内容的临时文件名称；`MERGED` 包含合并工具应向其写入合并结果的文件名。

### `mergetool.<tool>.trustExitCode`

对于自定义合并命令，指定合并命令的退出码是否可以用于判断合并是否成功。如果未设置为 `true`，则会检查合并目标文件的时间戳，如果文件已更新，则假设合并成功，否则将提示用户指示合并是否成功。

### `mergetool.meld.hasOutput`

旧版本的 meld 不支持 `--output` 选项。Git 将尝试通过检查 `meld --help` 的输出来检测 meld 是否支持 `--output`。通过配置 `mergetool.meld.hasOutput` 将使 Git 跳过这些检查并改用配置的值。将 `mergetool.meld.hasOutput` 设置为 `true` 告诉 Git 无条件使用 `--output` 选项，设置为 `false` 则避免使用 `--output`。

### `mergetool.keepBackup`

执行合并后，带有冲突标记的原始文件可以保存为带有 `.orig` 扩展的文件。如果此变量设置为 `false`，则不保留此文件。默认是 `true`（即保留备份文件）。

### `mergetool.keepTemporaries`

在调用自定义合并工具时，Git 使用一组临时文件来传递给该工具。如果工具返回错误且此变量设置为 `true`，则这些临时文件将被保留，否则它们将在工具退出后被删除。默认是 `false`。

### `mergetool.writeToTemp`

Git 默认在工作树中写入冲突文件的临时 `BASE`、`LOCAL` 和 `REMOTE` 版本。当设置为 `true` 时，Git 将尝试使用临时目录来存放这些文件。默认是 `false`。

### `mergetool.prompt`

在每次调用合并解决程序之前提示。

### `notes.displayRef`

在显示提交消息时，从中显示注释的（完全限定的）引用名（refname）。该变量的值可以设置为通配符（glob），在这种情况下，将显示所有匹配 ref 的注释。你也可以多次指定此配置变量。对于不存在的 ref 将发出警告，但不匹配任何 ref 的通配符将被静默忽略。

此设置可以通过环境变量 `GIT_NOTES_DISPLAY_REF` 进行覆盖，该变量必须是由冒号分隔的 ref 或通配符列表。

`core.notesRef` 的有效值（可能被 `GIT_NOTES_REF` 覆盖）也会隐式添加到要显示的 ref 列表中。

### `notes.rewrite.<command>`

当使用 `<command>` 重写提交（目前为 amend 或 rebase）且此变量设置为 `true` 时，Git 会自动将你的注释从原始提交复制到重写提交。默认是 `true`，但请参见下文 "notes.rewriteRef"。

### `notes.rewriteMode`

在重写期间复制注释时（见 "notes.rewrite.<command>"），决定当目标提交已有注释时执行。必须是 `overwrite`、`concatenate` 或 `ignore` 之一。默认是 `concatenate`。

此设置可以通过环境变量 `GIT_NOTES_REWRITE_MODE` 进行覆盖。

### `notes.rewriteRef`

在重写期间复制注释时，指定应复制注释的（完全限定的）引用。引用可以是通配符，在这种情况下将复制所有匹配 ref 的注释。你也可以多次指定此配置变量。

没有默认值；你必须配置此变量以启用注释重写。设置为 `refs/notes/commits` 以对默认提交启用重写。

此设置可以通过环境变量 `GIT_NOTES_REWRITE_REF` 进行覆盖，该变量必须是冒号分隔的 ref 或通配符列表。

### `pack.window`

当未指定 own 时，(1) 使用的窗口。默认是 10。

### `pack.depth`

当未指定最大深度时，(1) 使用的最大差异深度。默认是 50。

### `pack.windowMemory`

当未指定限制时，(1) 中每个线程用于包窗口内存的最大内存。该值可以带有后缀 `"k"`、`"m"` 或 `"g"`。当未配置（或显式设置为 0）时，将没有限制。

### `pack.compression`

整数 -1..9，表示包文件中对象的压缩级别。-1 是 zlib 默认值。0 表示不压缩，1..9 是不同的速度/大小权衡，9 最慢。如果未设置，默认为 `core.compression`。如果也未设置，默认为 -1，即 zlib 默认值，它是“速度和压缩之间的默认折中（目前相当于级别 6）”。

注意，更改压缩级别不会自动重新压缩所有对象。你可以通过向 (1) 传递 `-F` 参数来强制重新压缩。

### `pack.deltaCacheSize`

(1) 在写入包之前用于缓存差异的最大内存（字节）。该缓存用于加速写入对象的阶段，以便在找到所有对象的最佳匹配后无需重新计算差异结果。在内存紧张的机器上重新打包大型仓库可能会受到此影响，特别是当此缓存导致系统进入交换分区时。值 0 表示没有限制。最小大小 1 字节可虚拟禁用此缓存。默认是 256 MiB。

### `pack.deltaCacheLimit`

(1) 缓存的差异的最大大小。该缓存用于加速写入对象的阶段，以便在找到所有对象的最佳匹配后无需重新计算差异结果。默认是 1000。

指定搜索最佳增量匹配（delta matches）时启动的线程数。这要求 (1) 编译时使用了 `pthreads`，否则该选项将被忽略并显示警告。这旨在减少多处理器机器上的打包时间。然而，增量搜索窗口所需的内存将是线程数的倍数。指定 0 将导致 Git 自动检测 CPU 数量并据此设置线程数。

### `pack.indexVersion`

指定默认的包索引版本。有效值为：1，表示 Git 1.5.2 之前的版本使用的旧版包索引；2，表示新的包索引，它具有支持大于 4 GB 的包的能力，并对损坏包的重新打包提供适当的保护。版本 2 是默认值。请注意，当相应的包大于 2 GB 时，将强制使用版本 2 并忽略此配置选项。

如果你使用的旧版 Git 无法识别版本 2 的 `*.idx` 文件，那么通过非原生协议（例如 `"http"` 和 `"rsync"`）进行克隆或获取（这会从对端拷贝 `*.pack` 文件和对应的 `*.idx` 文件），可能会导致得到的仓库无法用旧版本的 Git 访问。然而，如果 `*.pack` 文件小于 2 GB，你可以对 `*.pack` 文件使用 (1) 来重新生成 `*.idx` 文件。

### `pack.packSizeLimit`

包（pack）的最大大小。此设置仅影响重新打包到文件时，即 `git://` 协议不受影响。它可以通过 (1) 的 `--max-pack-size` 选项覆盖。允许的最小大小限制为 1 MiB。默认不受限制。支持常用的单位后缀 `k`、`m` 或 `g`。

### `pack.useBitmaps`

当为 `true` 时，Git 在打包到标准输出时（例如在 `fetch` 的服务端执行期间）将使用包位图（pack bitmaps，如果可用）。默认 `true`。除非你正在调试包位图，否则通常不需要关闭它。

### `pack.writeBitmaps`（已弃）

这是 `repack.writeBitmaps` 的已弃同义词。

### `pack.writeBitmapHashCache`

当为 `true` 时，Git 将在位图索引中包含一个“哈希缓存”部分（如果已了）。该缓存可用于为 Git 的增量启发式提供数据，可能在位图对象和非位图对象之间产生更好的增量（例如，当在旧的位图包和自上次 `gc` 之后推送的对象之间提供 `fetch` 时）。缺点是每个对象会消耗 4 字节磁盘空间，且 `JGit` 的位图实现不理解它，导致在同一仓库上使用 Git 和 JGit 时它会报错。默认 `false`。

### `pager.<cmd>`

如果值为布尔值，则在写入 tty 时开启或关闭特定 Git 子命令输出的分页。否则，将使用 `pager.<cmd>` 值指定的分页器对该子命令开启分页。如果在命令行上指定了 `--paginate` 或 `--no-pager`，则其优先级高于此选项。要禁用所有命令的分页，可以将 `core.pager` 或 `GIT_PAGER` 设置为 `cat`。

### `pretty.<name>`



指定`--pretty=`格式字符串的别名。在这里定义的任何别名都可以像内置格式化格式一样使用。例如，运行`git config pretty.changelog "format:* %H %s"`会导致调用`git log --pretty=changelog`等同于运行`git log "--pretty=format:* %H %s"`。注意，与内置格式同名的别名将被默默忽略。

## `pull.ff`

默认情况下，Git 在合并一个作为当前提交后代的提交时，不会创建额外的合并提交（merge commit）。相反，当前分支的末端将进行快进（fast-forward）。当设置为 false 时，此变量告诉 Git 在这种情况创建一个额外的合并提交（等同于在命令行中提供`--no-ff`选项）。当设置为 only 时，仅允许此类的快进合并（等同于在命令行中提供`--ff-only`选项）。此设置在 pull 时会覆盖`merge.ff`。

## `pull.rebase`

当为 true 时，运行`git pull`时，会将分支 rebase 到获取到的分支之上，而不是从默认远程仓库合并默认分支。按分支设置此项，请参见`branch.<name>.rebase`。

当设置为 preserve 时，还会将`--preserve-merges`传递给`git rebase`，这样本地提交的合并提交就不会在运行`git pull`时被扁平化。

**注意**：这是一个可能危险的操作；除非你理解其影响，否则**不要**使用它（详情请参见 (1)）。

## `pull.octopus`

一次性提取多个分支时使用的默认合并策略。

## `pull.twohead`

拉取单个分支时使用的默认合并策略。

## `push.default`

定义了如果没有显式给出引用规格（refspec），`git push`应该采取的动作。不同的值适用于特定的工作流；例如，在纯中心化工作流中（即 fetch 源等于 push 目的），`upstream`可能是你想要的。

- `nothing`：除非显式给出引用规格，否则不推送任何内容（报错）。这主要用于那些希望通过始终显式操作避免错误的人。
- `current`：将当前分支推送到接收端同名的分支。这在中心化和非中心化工作流中均有效。
- `upstream`：将当前分支推回通常集成到当前分支的分支（称为`@{upstream}`）。这种模式只有在你推送通常从其 pull 的仓库时才有意义（即中心化工作流）。
- `simple`：在中心化工作流中，其工作类似于`upstream`，但增加了一个安全性：如果上游分支名称与本地分支不同，则拒绝推送。这曾是默认值，但从 Git 2.0 开始不再是（simple 是新的默认值）。
- `matching`：推送两端具有同名的所有分支。这使得你推送到的仓库记住将被推送出的分支集。

## `push.followTags`

如果设置为 true，则默认启用`--follow-tags`选项。你可以在推送时通过指定`--no-follow-tags`来覆盖此配置。

将此变量设置为字符串时，`git receive-pack`将接受`git push --signed`，并使用该字符串作为密钥通过 HMAC 保护的“随机数”（nonce）进行验证。

## `receive.certNonceSlop`

当`git push --signed`发送的推送证书包含的“随机数”是在在指定的秒数内由服务同一仓库的`receive-pack`发的时，将证书中找到的“随机数”导出到`GIT_PUSH_CERT_NONCE`传递给钩（而不是`receive-pack`要求发送端包含的内容）。这可能使得在`pre-receive`和`post-receive`中编写检查逻辑变得更容易。钩无需通过检查记录随机数过期秒数的`GIT_PUSH_CERT_NONCE_SLOP`环境变量来决定是否接受证书，只需检查`GIT_PUSH_CERT_NONCE_STATUS`是否为`OK`。

## `receive.fsckObjects`

如果设置为`true`，`git-receive-pack`将检查所有收到的对象。如果遇到格式错误的对象或损坏的链接，将中止。中止的结果只会产生悬空对象。默认值为`false`。如果未设置，则使用`transfer.fsckObjects`的值。

## `receive.unpackLimit`

如果推送中收到的对象数量低于此限制，对象将被解压为松散对象文件。然而，如果收到的对象数量等于或超过此限制，收到的包将在添加任何缺失的增量基后，以包的形式存储。存储推送的包可以使推送操作完成更快，特别是在慢文件系统上。如果未设置，则使用`transfer.unpackLimit`的值。

## `receive.denyDeletes`

如果设置为`true`，`git-receive-pack`将拒绝删除引用（ref）的更新。使用此防止通过推送删除此类引用。

## `receive.denyDeleteCurrent`

如果设置为`true`，`git-receive-pack`将拒绝删除非裸仓库中当前检出分支的引用更新。

## `receive.denyCurrentBranch`

如果设置为`true`或`"refuse"`，`git-receive-pack`将拒绝对非裸仓库中当前检出分支的引用更新。这种推送具有潜在危险，因为它会导致`HEAD`与索引和工作树不同步。如果设置为`"warn"`，则向`stderr`打印此类推送的警告，但允许推送继续。如果设置为`false`或`"ignore"`，则允许此类推送且不发送消息。默认值为`"refuse"`。

另一个选项是`"updateInstead"`，当向当前分支推送内容时，它将更新工作树。此选项用于在一方无法通过交互式 ssh 轻松访问时同步工作目录（例如实时网站，因此要求工作目录必须是干净的）。这种模式在虚拟机内部开发以测试和修复不同操作系统上的代码时也非常好用。

默认情况下，如果工作树或索引与`HEAD`有任何任何差异，`"updateInstead"`将拒绝推送，但可以使用`push-to-checkout`钩来自定义此行为。见 (5)。

## `receive.denyNonFastForwards`

如果设置为`true`，`git-receive-pack`将拒绝非快进（not fast-forward）的引用更新。使用此防止通过推送此类更新，即使该推送是强制的。此配置变量在初始化共享仓库时设置。

## `receive.hideRefs`

`receive-pack`使用的字符串用于决定从其初始广告中省略哪些引用。使用多个定义可以指定多个前缀字符串。位于此变量值列出的层级下的引用将被排除，并在响应`git push`时被隐藏，且通过`git push`尝试更新或删除隐藏引用的尝试将被拒绝。

## `receive.updateServerInfo`

如果设置为`true`，`git-receive-pack`在接收来自`git-push`的数据并更新引用后，将运行`git-update-server-info`。

## `receive.shallowUpdate`

如果设置为`true`，当新引用需要新的浅层根时，`.git/shallow`可以被更新。否则，这些引用将被拒绝。

## `remote.pushDefault`

默认推送到的远程仓库。它覆盖所有分支的`branch.<name>.remote`，并被特定分支的`branch.<name>.pushRemote`覆盖。

## `remote.<name>.url`

远程仓库的 URL。见 (1) 或 (1)。

## `remote.<name>.pushurl`

远程仓库的推送 URL。见 (1)。

## `remote.<name>.proxy`

对于需要`curl`（http, https 和 ftp）的远程仓库，用于该远程仓库的代理 URL。设置为空字符串以禁用该远程仓库的代理。

## `remote.<name>.fetch`

用于 (1) 的默认 "refspec" 集合。见 (1)。

## `remote.<name>.push`

用于 (1) 的默认 "refspec" 集合。见 (1)。

## `remote.<name>.mirror`

如果为`true`，推送到此远程将自动表现为在命令行上提供了`--mirror`选项。

## `remote.<name>.skipDefaultUpdate`

如果为`true`，在使用 (1) 或 (1) 的更新子命令更新时，默认跳过此远程仓库。

## `remote.<name>.skipFetchAll`

如果为`true`，在使用 (1) 或 (1) 的更新子命令更新时，默认跳过此远程仓库。

## `remote.<name>.receivepack`

推送时在远程侧执行的默认程序。见 (1) 的选项`--receive-pack`。

## `remote.<name>.uploadpack`

获取时在远程侧执行的默认程序。见 (1) 的选项`--upload-pack`。

## `remote.<name>.tagOpt`

将此值设置为`--no-tags`可以在从远程`<name>`获取时禁用自动跟踪标签。将其设置为`--tags`将获取从远程`<name>`的每一个标签，即使它们从远程分支头无法到达。将这些标志直接传递给 (1)。

## `remote.<name>.vcs`

将此项设置为值`<vcs>`将导致 Git 与远程交互。

## `remote.<name>.prune`

当设置为`true`时，从此远程获取内容将还将删除远程上已不存在的任何远程跟踪引用（如同提供了`--prune`选项）。

## `remotes.<group>`

通过`git update <group>`获取的远程仓库列表。见 (1)。

## `repack.useDeltaOffset`

默认情况下，(1) 创建的包使用增量基偏移量。如果你需要与比 1.4.4 更老的 Git 共享仓库（直接或通过 http 等易易协议），则你需要将此选项设置为`"false"`并重新打包。旧版本的访问不受此选项影响。

## `repack.packObjects`

如果设置为`true`，使`git repack`行为类似于传递了`--kept-objects`。见 (1) 详情。通常默认值为`false`，但在写入位图索引时（通过`--bitmap-index`或`repack.writemaps`）为`true`。

## `repack.writemaps`

为`true`时，git 在打包所有对象到磁盘时写入位图索引（例如运行`git repack -a`时）。该索引可以加快后续克隆和获取的计数计数阶段，代价是额外的磁盘空间和初始打包花费的时间。默认值为`false`。

## `rerere.autoUpdate`

当设置为`true`时，`git-rerere`在使用之前记录的解析清理冲突后更新索引。默认值为`false`。

## `rerere.enabled`

激活对已解决冲突记录，以便再次遇到相同的冲突块时可以自动解决。默认情况下，如果`$GIT_DIR`下存在`rr-cache`目录，则启用（例如之前在仓库中使用过 "rerere"）。

## `sendemail.identity`

配置身份。给出后会导致`sendemail.<identity>`部分的值值优于`sendemail`部分的值。默认身份是`sendemail.identity`的值。

## `sendemail.smtpEncryption`

描述请见 (1)。注意，此设置不受 *identity* 机制的影响。

## `sendemail.smtpssl`（已弃用）

`sendemail.smtpEncryption = ssl`的已弃用别名。

## `sendemail.smtpsslcertpath`

ca 证书路径（目录或单个文件）。将其为空字符串以禁用证书验证。

## `sendemail.<identity>.*`

下方是`sendemail.*`参数的特定身份版本，当通过命令行或`sendemail.identity`选择该身份时，这些参数优先级高于其他设置。

`sendemail.aliasesFile`, `sendemail.aliasFileType`, `sendemail.annotate`, `sendemail.bcc`, `sendemail.cc`, `sendemail.ccCmd`, `sendemail.chainReplyTo`, `sendemail.confirm`, `sendemail.envelopeSender`, `sendemail.from`, `sendemail.multiEdit`, `sendemail.signedoffbycc`, `sendemail.smtpPass`, `sendemail.suppresscc`, `sendemail.suppressFrom`, `sendemail.to`, `sendemail.smtpDomain`, `sendemail.smtpServer`, `sendemail.smtpServerPort`, `sendemail.smtpServerOption`, `sendemail.smtpUser`, `sendemail.thread`, `sendemail.transferEncoding`, `sendemail.validate`, `sendemail.xmailer`

描述请参见 (1)。

## `sendemail.signedoffcc`（已弃用）

`sendemail.signedoffbycc`的弃用别名。

## `showbranch.default`

(1) 的默认分支集。请参见 (1)。

## `status.relativePaths`

默认情况下，(1) 显示相对于当前目录的路径。将此变量设置为`false`则显示相对于仓库根目录的路径（这是 Git v1.5.4 之前的默认设置）。

## `status.short`

设置为`true`可在 (1) 中默认启用`--short`。`--no-short`选项优先级高于此变量。

## `status.branch`

设置为`true`可在 (1) 中默认启用`--branch`。`--no-branch`选项优先级高于此变量。

## `status.displayCommentPrefix`

如果设置为`true`，(1)将在每行输出前插入一个注释前缀（以`core.commentChar`开头，默认为`#`）。这是 Git 1.8.4 及之前的版本的行为。默认值为`false`。

## `status.showUntrackedFiles`

默认情况下，(1) 和 (1) 显示当前未被 Git 跟踪的文件。对于仅包含未跟踪文件的目录，将仅显示目录名。显示未跟踪文件意味着 Git 需要对整个仓库中的文件执行`lstat()`，这在某些系统上可能会很慢。因此，此变量控制命令如何显示未跟踪文件。可能的值有：

- `no` - 不显示未跟踪的文件。
- `normal` - 显示未跟踪的文件目录。
- `all` - 同时显示未跟踪目录中的单个文件。

如果未指定此变量，默认为`normal`。可以通过 (1) 和 (1) 的`-u|--untracked-files`选项覆盖此变量。

## `status.submoduleSummary`

默认为`false`。如果设置为非零数字或`true`（等同于`-1`或无限数量），将启用子模块摘要并显示已修改子模块的提交摘要（参见 (1) 的`--summary-limit`选项）。请注意，当`diff.ignoreSubmodules`设置为`all`时，所有子模块的摘要输出命令将被抑制；或者仅针对设置了`submodule.<name>.ignore=all`的子模块。该规则的例外是`status`和`commit`将显示已暂存的子模块更改。若要查看被忽略子模块的摘要，可以使用`--ignore-submodules=dirty`命令行选项或`git submodule summary`命令，后者会显示类似的输出，但不遵循这些设置。

## `submodule.<name>.path`, `submodule.<name>.url`

子模块在项目中的路径和 URL。这些变量最初由`git submodule init`填充。详情参见 (1) 和 (5)。

## `submodule.<name>.update`

子模块的默认更新程序。此变量由`git submodule init`从 (5) 文件中填充。参见 (1) 中 `update` 命令的描述。

## `submodule.<name>.branch`

子模块的远程分支名，供`git submodule update --remote`使用。设置此选项以覆盖`.gitmodules`文件中的值。详情参见 (1) 和 (5)。

## `submodule.<name>.fetchRecurseSubmodules`

此选项可用于控制此子模块的递归获取。可以通过对`git fetch`和`git pull`使用`--[no-]recurse-submodules`命令行选项进行覆盖。

此设置将覆盖 (5) 文件中的设置。

## `submodule.<name>.ignore`



定义了在什么情况下 `git status` 和 `diff` 系列命令会将子模块显示为已修改。当设置为 `"all"` 时，它永远不会被视为已修改（但如果已暂存，仍会在 `status` 和 `commit` 的输出中出现）；`"dirty"` 会忽略子模块工作树的所有更改，仅考虑子模块的 `HEAD` 与主项目中记录的提交之间的差异；`"untracked"` 会额外让工作树中有已修改的跟踪文件的子模块显示出来。使用 `"none"`（未设置此选项时的默认值）也会将工作树中存在未跟踪文件的子模块显示为已更改。此设置将覆盖 `.gitmodules` 中对该子模块的任何设置，两种设置都可以在命令行上通过 `--ignore-submodules` 选项进行覆盖。`git submodule` 命令不受此设置影响。

# tag.sort

此变量控制标签在 (1) 中显示时的排序顺序。在没有提供 `--sort=<value>` 选项的情况下，将使用此变量的值。

# tar.umask

此变量用于限制 `tar` 归档项目的权限位。默认值为 `0002`，关闭 world 写位。特殊值 `"user"` 表示使用归档用户的 `umask`。参见 (2) 和 (1)。

# transfer.fsckObjects

当 `fetch.fsckObjects` 或 `receive.fsckObjects` 未设置时，将使用此变量的值。默认为 `false`。

# transfer.hideRefs

此变量可同时将 `receive.hideRefs` 和 `uploadpack.hideRefs` 设置为相同的值。参见这些其他变量的条目。

# transfer.unpackLimit

当 `fetch.unpackLimit` 或 `receive.unpackLimit` 未设置时，将使用此变量的值。默认值为 `100`。

# uploadarchive.allowUnreachable

如果为 `true`，允许客户端使用 `git archive --remote` 请求任何树，无论是否可。详情参见 (1) 安全部分。默认为 `false`。

# uploadpack.hideRefs

`upload-pack` 用于决定从初始广告中省略哪些引用的字符串列表。使用多个定义来指定多个前缀字符串。位于变量值列表层级的引用将被排除，并对 `git ls-remote`、`git fetch` 等隐藏。尝试通过 `git fetch` 获取隐藏引用将失败。参见 `uploadpack.allowTipSHA1InWant`。

# uploadpack.allowTipSHA1InWant

当 `uploadpack.hideRefs` 生效时，允许 `upload-pack` 接受请求隐藏引用端对象的获取请求（默认情况下，此类请求拒绝）。参见 `uploadpack.hideRefs`。

# uploadpack.allowReachableSHA1InWant

允许 `upload-pack` 接受请求任何引用端可达对象的获取请求。但请注意，计算对象可达性开销很大。默认为 `false`。

# uploadpack.keepAlive

当 `upload-pack` 开始 `pack-objects` 时，在 `pack-objects` 准备包期间可能会有一个静默期。通常会输出进度信息，但如果 `fetch` 使用了 `--quiet`，`pack-objects` 在包数据开始之前将没有任何输出。某些客户端和网络可能会认为服务器挂起并放弃。设置此选项指示 `upload-pack` 每隔 `uploadpack.keepAlive` 秒发送一个空心跳包。将此选项设置为 `0` 则完全禁用心跳包。默认值为 `5` 秒。

# url.<base>.insteadOf

任何以此值开头的 URL 都将被重写为以 `<base>` 开头。在某些站点提供大量仓库并提供多种访问方式的情况下，如果某些用户需要使用不同的访问方式，此功能允许用户指定任何一个等效的 URL，并让 Git 自动将 URL 重写为适用于特定用户的最佳替代，即使是该站点上从未见过的仓库也是。当多个 `insteadOf` 字符串匹配给定 URL 时，将使用最长的匹配项。

# url.<base>.pushInsteadOf

任何以此值开头的 URL 都不会被推送；相反，它将被重写为以 `<base>` 开头，并推送生成的 URL。在某些站点提供大量仓库并提供多种访问方式（其中某些方式不允许推送）的情况下，此功能允许用户指定一个仅限拉取的 URL，并让 Git 自动使用适当 URL 进行推送，即使是该站点上从未见过的仓库。当多个 `pushInsteadOf` 字符串匹配给定 URL 时，将使用最长的匹配项。如果远程仓库有显式的 `pushurl`，Git 将忽略该远程仓库的此设置。

# user.email

记录在任何新创建提交中的电子邮件地址。可以通过 `GIT_AUTHOR_EMAIL`、`GIT_COMMITTER_EMAIL` 和 `EMAIL` 环境变量覆盖。参见 (1)。

# user.name

记录在任何新创建提交中的你的全名。可以通过 `GIT_AUTHOR_NAME` 和 `GIT_COMMITTER_NAME` 环境变量覆盖。参见 (1)。

# user.signingKey

如果在创建签名标签或提交时，(1) 或 (1) 没有选择你想要自动使用的密钥，你可以通过此变量覆盖默认选择。此选项将原封不动传递给 `gpg` 的 `--local-user` 参数，因此你可以使用 `gpg` 支持的任何方法指定密钥。

# versionsort.prereleaseSuffix

当在 (1) 中使用版本排序时，预发布标签（例如 `"1.0-rc1"`）可能会出现在主发布版本 `"1.0"` 之后。通过在该变量中指定后缀 `"-rc"`，`1.0-rc1` 将出现在 `"1.0"` 之前。

此变量可以指定多次，每个后缀对应一次。配置文件中后缀的顺序决定了排序顺序（例如，如果 `"-pre"` 在配置文件中于 `"-rc"` 之前，则 `1.0-preXX` 将排在 `1.0-rcXX` 之前）。如果它们位于多个配置文件中，不同后缀之间的排序顺序是未定义的。

# web.browser

指定某些命令可能使用的网页浏览器。目前只有 (1) 和 (1) 可以使用它。

***

# GIT-COUNT-OBJECTS

## 名称

`git-count-objects` - 统计未解包对象的数量及其磁盘空间占用

## 概要

```
git count-objects [-v] [-H | --human-readable]
```

## 描述

计算未解包对象文件的数量以及它们占用的磁盘空间，帮助你判断何时重新重新打包（`repack`）。

### 选项

- `-v`, `--verbose`

详细详细报告：

- `count`: 松散对象的数量

- `size`: 松散对象占用磁盘空间，单位为 KiB（除非指定了 `-H`）

- `in-pack`: 包内对象的数量

- `size-pack`: 包占用的磁盘空间，单位为 KiB（除非指定了 `-H`）

- `prune-packable`: 同时存在于包中的松散对象数量。这些对象可以使用 `git prune-packed` 进行修剪。

- `garbage`: 对象数据库中既不是有效松散对象也不是有效包的文件数量

- `size-garbage`: 垃圾文件占用磁盘空间，单位为 KiB（除非指定了 `-H`）

- `-H`, `--human-readable`

以人类可读的格式打印大小

***

# GIT-CREDENTIAL-CACHE--DAEMON

## 名称

`git-credential-cache--daemon` - 在内存中临时存储用户凭证

## 概要

```
git credential-cache---daemon [--debug] <socket>
```

## 描述

**注意**

你可能不想自己调用此命令；它在你在使用 (1) 时会自动启动。

该命令在 `<socket>` 指定的 Unix 域接字上监听 `git-credential-cache` 客户端。客户端可以存储和检索凭证。每个凭证的有效期由客户端指定；一旦没有凭证，守护进程就会退出。

如果指定了 `--debug` 选项，守护进程不会关闭其 `stderr` 流，并且在开始监听客户端后也可能向其输出额外的诊断信息。

***

# GIT-CREDENTIAL-CACHE

## 名称

`git-credential-cache` - 在内存中临时存储密码的辅助程序

## 概要

```
git config credential.helper 'cache [options]'
```

## 描述

此命令在内存中缓存凭证以供未来的 Git 程序使用。存储的凭证永远不会接触磁盘，并在配置的超时后被忘记。缓存可以通过 Unix 域接字访问，并通过文件系统权限限制为当前用户。

你可能不想直接调用此命令；它旨在作为 Git 其他部分的凭据助手使用。参见下文的 (7) 或 示例。

### 选项

- `--timeout <seconds>`

缓存凭证的秒数（默认: `900`）。

- `--socket <path>`

使用 `<path>` 连接到运行的缓存守护进程（如果没有启动，则启动一个新的缓存守护进程）。默认为 `~/.git-credential-cache`。如果你的主目录在网络挂载的文件系统上，可能需要将其改为本地文件系统。

## 控制守护进程

如果你希望守护进程在超时之前退出并忘记所有凭证，可以执行此操作：

```
git credential-cache exit
```

## 示例

此辅助程序的目的是减少你输入用户名或密码的次数。例如：

```
git config credential.helper cache
git push Username: <你的用户名> Password: <你的密码>
```

你可以通过 `credential.helper` 配置变量提供选项（此示例将缓存时间降为 5 分钟）：

```
git config credential.helper 'cache --timeout=300'
```

***

# GIT-CREDENTIAL-STORE

## 名称

`git-credential-store` - 将凭据存储在磁盘上的辅助程序

## 概要

```
git config credential.helper 'store'
```

## 描述

**注意**

使用此助手会将你的密码明文存储在磁盘上，仅受文件系统权限保护。如果这不是可以接受的安全权，请尝试 (1)，或者寻找与系统提供的安全存储的助手。

此命令将凭证永久存储在磁盘上，供未来的 Git 程序使用。

你可能不想直接调用此命令；它旨在作为 Git 其他部分的凭据助手使用。参见下文的 (7) 或 示例。

### 选项

- `--file=<path>`

使用 `<path>` 查找和存储凭证。该文件的文件系统权限将设置为防止系统上的其他用户读取，但不会进行加密或其他保护。如果没有指定，系统将从 `~/.git-credentials` 和 `$XDG_CONFIG_HOME/git/credentials` 搜索凭证，如果前者不存在，则凭证将写入后者（如果后者存在）。请另参见“文件”部分。

# 文件

如果没有通过 `--file` 显式设置，`git-credential-store` 将按优先级在两个文件中搜索凭证：

`~/.git-credentials`

用户特定凭据文件。

`$XDG_CONFIG_HOME/git/credentials`

第二个用户特定凭据文件。如果 `$XDG_CONFIG_HOME` 未设置为空，将使用 `$HOME/.config/git/credentials`。如果 `~/.git-credentials` 有匹配的凭证，则该文件中任何凭证都不会被使用。如果你有时使用不支持它的旧版本 Git，不创建此文件是一个好主意。

对于凭据查找，将按照上述顺序读取文件，找到的第一个匹配凭证优先于列表中后续文件的凭证。

凭据存储默认将写入到列表中第一个存在的文件。如果这些文件都不存在，则将创建并写入 `~/.git-credentials`。

在删除凭据时，所有文件中匹配的凭据都将被删除。

## 示例

此辅助工具的作用点是减少你必须输入用户名或密码的次数。例如：

```bash
$ git config credential.helper store
$ git push Username: <输入你的用户名> Password: <输入你的密码>
[几天后]
$ git push [你的凭据将被自动使用]
```

## 存储格式

`.git-credentials` 文件以明文形式存储。每个凭据单独存储在一行，格式如下 URL：

当 Git 需要对特定的 URL 上下文进行身份验证时，`credential-store` 将该上下文视为一个模式，与凭据文件中的每个项目进行匹配。如果协议、主机名和用户名（如果已经有了的话）匹配，则会将密码返回给 Git。更多信息请参见 (7) 中关于配置的讨论。

***

# GIT-CREDENTIAL

## 名称

`git-credential` - 获取和存储用户凭据

## 概要

`git credential <fill|approve|reject>`

## 描述

Git 有一个内部接口用于从特定系统的辅助工具中存储和检索凭据，并提示用户用户名和密码。`git-credential` 命令将此接口暴露给脚本，这些脚本可能希望以 Git 以相同的方式获取、存储或提示凭据。该可脚本接口的设计模拟了内部的 C API；有关概念的更多背景信息，请参见 `the Git credential API`m[][1]。

`git-credential` 在命令行上接受一个“操作”选项（`fill`、`approve` 或 `reject` 之一），并从 `stdin` 读取凭据描述（参见 INPUT/OUTPUT FORMAT）。

如果操作是 `fill`，`git-credential` 将尝试通过读取配置文件、联系任何已配置的凭据辅助工具或提示用户，向描述中添加 `username` 和 `password` 属性。随后，将凭据描述的用户名和密码属性连同已提供的属性一起打印到 `stdout`（标准输出）。

如果操作是 `approve`，`git-credential` 将描述发送给任何已配置的凭据辅助工具，这些工具可能会存储凭据以供以后使用。

如果操作是 `reject`，`git-credential` 将描述发送给任何已配置的凭据辅助工具，这些工具可能会删除任何与描述匹配的存储凭据。

如果操作是 `approve` 或 `reject`，则不应产生输出。

## GIT CREDENTIAL 的典型用法

使用 `git-credential` 的应用程序通常按以下步骤使用 `git credential`：

1. 根据上下文生成凭据描述。

例如，如果我们想为某个请求获取密码，可能会生成如下凭据描述（不要忘记末最后的空行；它告诉 `git credential` 应用程序完成了所有其拥有的信息的输入）：

`protocol=https host=example.com path=foo.git`

2. 要求 `git-credential` 为此描述提供一个用户名和密码。这是通过运行 `git credential fill` 并将步骤 (1) 中的描述馈送给它的标准输入完成的。完整的凭据描述（包括凭据本身，即登录名和密码）将在标准输出上产生，如下：

`protocol=https host=example.com username=bob password=secr3t`

在大多数情况下，这意味着输入中给出的属性将在输出中重复，但 Git 可能会修改凭据描述，例如，当协议为 HTTP(s) 且 `credential.useHttpPath` 为 `false` 时，移除 `path` 属性。

如果 `git credential` 知道密码，那么此步骤在返回 `password=secr3t` 之前，可能并不涉及用户实际输入此密码（用户可能输入了密码来解锁钥匙串，或者如果钥匙串已经解锁则没有用户交互）。

3. 使用该凭据（例如，使用步骤 (2) 中的用户名和密码访问 URL），并查看是否被接受。

4. 报告密码的成功或失败。如果凭据允许操作成功完成，则可以将其标记为 `approve` 操作，告诉 `git credential` 在下一次调用中重用它。如果凭据在操作期间被拒绝，则使用 `reject` 操作，以便 `git credential` 在下一次调用时请求新密码。在任何情况下，都应向 `git credential` 供给从步骤 (2) 获取的凭据描述（该描述也包含了步骤 (1) 中提供的项）。

## 输入/输出格式

`git credential` 在其标准输入/输出中读取和或写入（取决于使用的操作）凭据信息。这些信息可以对应于 `git credential` 获取登录/密码信息的键（例如 `host`、`protocol`、`path`），也可以对应于获取的实际凭据数据（登录/密码）。

凭据被分为一组命名属性，每行一个属性。每个属性由一个键值对指定，用 `=`（等号）分隔，后跟一个换行符。凭据被拆分为一组命名属性，每行一个属性。每个属性由一个键值对指定，用 `=`（等号）分隔，后跟一个换行符。每个属性由一个键值对指定，用 `=`（等号）分隔，后跟一个换行符。凭据被拆分为一组命名属性，每行一个属性。每个属性由一个键值对指定，用 `=`（等号）分隔，后跟一个换行符。凭据被拆分为一组命名属性，每行一个属性。`git credential` 属性列表的结束。`git credential` 的属性列表以换行符结束。Git 理解以下属性：

`protocol`

用于该凭据的协议（e.g. `https`）。

`host`

远程凭据的主机名。

`path`

用于该凭据的路径。

`username`

凭据的用户名。

`password`

凭据的密码。

`url`

当此特殊属性被 `git credential` 读取时，将被视为 URL。

## 注意

1.



# 凭证 API

***

## GIT-DESCRIBE

### 名称

`git-describe` - 使用从提交到达的最早标签描述提交

### 概要

`git describe [--all] [--tags] [--contains] [--abbrev=<n>] <commit-ish>...`

`git describe [--all] [--tags] [--contains] [--abbrev=<n>] --dirty[=<mark>]`

### 描述

该命令找到从提交到达的最早标签。如果标签指向该提交，则仅显示标签。否则，将在标签名称后面加上标记对象的额外提交数以及最近提交的简短对象名。

默认情况下（不使用 `--all` 或 `--tags`），`git describe` 只显示注解标签。关于创建注解标签的更多信息请参见 (1) 中的 `-a` 和 `-s` 选项。

#### 选项

`<commit-ish>...`

要描述的提交对象。

`--dirty[=<mark>]`

描述工作树。这意味着描述 `HEAD` 并在工作树不干净时追加 `<mark>`（默认为 `-dirty`）。

`--all`

不再只使用注解标签，而是使用 `refs/` 命名空间中的任何引用。此选项允许匹配任何已知分支、远程跟踪分支或轻量级标签。

`--tags`

不再只使用注解标签，而是使用 `refs/tags` 命名空间中的任何标签。此选项允许匹配轻量级（非注解）标签。

`--contains`

不是找到在提交之前的标签，而是找到提交之后的标签，并因此包含它。自动隐含 `--tags`。

`--abbrev=<n>`

简短对象名的最大长度。

### `--abbrev=<n>`

不再使用默认的 7 位十六进制数字作为缩写对象名，而是使用 `<n>` 位数字，或形成唯一对象名所需的任意位数。`<n>` 设置为 `0` 将抑制长格式输出，仅显示最近的标签。

### `--candidates=<n>`

不再仅考虑最近的 10 个标签作为描述输入提交（`commit-ish`）的候选，而是考虑最多 `<n>` 个候选。将 `<n>` 增加到 10 以上会花费稍微长时间，但可能会产生更准确的结果。`<n>` 设置为 `0` 将仅输出精确匹配项。

### `--exact-match`

仅输出精确匹配项（标签直接引用所提供的提交）。这是 `--candidates=0` 的同义词。

### `--debug`

向标准错误流详细显示关于正在采用的搜索策略的策略。标签名称仍会打印到标准输出。

### `--long`

即使在匹配到标签时也始终输出长格式（标签、提交数量和缩写后的提交名）。当你想在 `describe` 输出中查看提交对象名的部分内容时非常有用，即使该提交恰好是一个标记过的版本。它不会仅仅输出标签名，而是会将此类提交描述为 `v1.2-0-gdeadbee`（自标签 `v1.2` 以来指向对象 `deadbee` 的第 0 个提交....）

### `--match <pattern>`

仅考虑匹配给定（7 位）模式的标签，排除 `refs/tags/` 前缀。这可以避免泄露仓库中的私有标签。

### `--always`

显示唯一的缩写提交对象作为备选。

### `--first-parent`

在遇到合并提交时，仅遵循第一个父提交。当你不想匹配目标提交历史中合并的分支上的标签时，这非常有用。

### 示例

在类似 `git.git` 的当前树中，我得到：

``` 
[torvalds@g5 git]$ git describe parent v1.0.4-14-g2414721 
```

即我的 `parent` 分支的当前 `HEAD` 是基于 `v1.0.4` 的，但由于其上有几次提交，`describe` 在末尾添加了额外提交的数量（`14`）以及提交本身的缩写对象名（`2414721`）。

额外提交的数量是 `git log v1.0.4..parent` 显示的提交数量。哈希后缀是 `-g` + `parent` 顶部提交的 7 位缩写（该提交为 `2414721b194453f058079d897d13c4e377f92dc6`）。`g` 前缀代表 `git`，用于根据软件所管理的 `SCM` 系统来描述软件版本。这在人们可能使用不同 `SCM` 的环境中非常有用。

对标签名执行 `git describe` 将仅显示标签名：

``` 
[torvalds@g5 git]$ git describe v1.0.4 v1.0.4 
```

使用 `--all` 时，命令可以使用分支头部作为引用，因此输出会显示引用路径：

``` 
[torvalds@g5 git]$ git describe --all --abbrev=4 v1.0.5² tags/v1.0.0-21-g975b 
[torvalds@g5 git]$ git describe --all --abbrev=4 HEAD^ heads/lt/describe-7-g975b 
```

将 `--abbrev` 设置为 `0` 时，命令可以找到没有任何后缀的最近标签名：

``` 
[torvalds@g5 git]$ git describe --abbrev=0 v1.0.5² tags/v1.0.0 
```

请注意，你今天输入这些命令得到的后缀可能比 Linus 之前运行这些命令时看到的要长，因为你的 Git 仓库可能有新的以 `975b` 开头的对象名的提交，而这些提交在当时并不存在，仅凭 `-g975b` 后缀可能不足以区分这些提交。

### 搜索策略

对于每个提供的提交（`commit-ish`），`git describe` 将首先查找精确标记该提交的标签。注记标签总是优于轻量标签，日期较新的标签总是优于日期较旧的标签。如果找到精确匹配，将输出其名称并停止搜索。

如果未找到精确匹配，`git describe` 将回溯提交历史以定位一个被标记过的祖先提交。将输出祖先的标签以及输入提交的 `SHA-1` 缩写。如果指定了 `--first-parent`，则回溯将仅考虑每个提交的第一个父提交。

如果在回溯期间找到多个标签，将选择并输出与输入提交差异提交最少的标签。这里“差异提交最少”定义为 `git log tag..input` 显示的提交数量是尽可能小的数字。

## GIT-DIFF-FILES

### 名称

`git-diff-files` - 比较工作树和索引中的文件

### 概要

`git diff-files [-q] [-0|-1|-2|-3|-c|--cc] [<common diff 选项>] [<path>...]`

### 描述

比较工作树和索引中的文件。当指定了路径时，仅比较这些命名的路径。否则，比较索引中的所有条目。

#### 选项

`-p`, `-u`, `--patch`

生成补丁（见下）。

`-s`, `--no-patch`

抑制差异输出。适用于 `show` 等命令。

`-U<n>`, `--unified=<n>`

使用 `<n>` 行上下文而不是通常的三行生成差异。

`--raw`

以原始格式生成差异。这是默认值。

`--patch-with-raw`

`-p` 的同义词。

`--minimal`

花费更多时间以确保产生可能的差异。

`--patience`

使用 `patience diff` 算法生成差异。

`--histogram`

使用 `histogram diff` 算法生成差异。

`--diff-algorithm={patience|minimal|histogram|myers}`

选择差异算法。变如下：

- `default`, `myers`：贪心差异算法。目前是默认值。
- `minimal`：花费更多时间以确保产生可能的差异。
- `patience`：在生成补丁时使用 `patience diff` 算法。
- `histogram`：该算法扩展了 `patience` 算法以“支持低频元素”。例如，如果你将 `diff.algorithm` 变量配置为非默认值并想使用默认值，必须使用 `--diff-algorithm=default`。

`--stat[=<width>,<name-width>[,<count]]]`

生成统计。默认情况下，文件名部分将尽可能使用空间，图形部分。最大宽度默认为终端宽度，如果没有连接终端则为 80 列，可以通过 `<width>` 覆盖。通过逗号给出另一个宽度 `<name-width>` 可以限制文件名部分的宽度。图形部分的宽度可以通过 `--stat-graph-width=<width>`（影响所有生成统计的命令）或设置 `diff.statGraphWidth=<width>`（不影响 `format-patch`）来限制。通过给出第三个参数 `<count>`，可以限制输出前 `<count>` 行，如果有更多则显示 ...

这些参数也可以单独设置：`--stat-width=<width>`、`--stat-name-width=<name-width>` 和 `--stat-count=<count>`。

`--numstat`

与 `--stat` 类似，但使用十进制显示添加和删除行的数量以及不缩写的路径，以便机器友好。对于二进制文件，输出两个 `-`。

`--shortstat`

仅输出 `stat` 格式的最后一行，包含修改文件的总数以及添加和删除行的数量。

`--dirstat[=<param1,param2,...>]`

输出每个子目录相对变化的分布。`--dirstat` 的行为可以通过逗号分隔的参数列表进行自定义。默认由 `diff.dirstat` 配置变量控制（见 (1)）。可用参数如下：

- `changes`：通过计算从源删除或向目标添加的行来计算 `dirstat` 数字。这忽略了文件内部纯代码移动。也就是说，重新排列文件中的行不会被像其他变化那样计数。这是未提供参数时的默认行为。

通过执行常规基于行的 `diff` 分析，并累加删除/添加的行数来计算 `dirstat` 数字。（对于二进制文件，改用计数 64 字节块，因为二进制文件没有天然的行概念）。这种 `--dirstat` 行为比 `changes` 行为开销更大，但它对文件内重排行的计数方式与其他更改相同。输出结果与其他 `--*stat` 选项获得的结果一致。

- `files`：通过统计已更改的文件数量来计算 `dirstat` 数字。在 `dirstat` 分析中，每个更改的文件计数权重相等。这是计算上开销最低的 `--dirstat` 行为，因为它完全不需要查看文件内容。

- `cumulative`：同时也为父目录统计子目录的变化。请注意，使用 `cumulative` 时，报告的百分比总和可能会超过 100%。可以使用 `noncumulative` 参数指定默认（非累计）行为。

- `<limit>`：一个整数参数，用于指定截断百分比（默认为 3%）。变化量低于此百分比的目录不会显示在输出中。

示例：以下命令将统计更改的文件，同时忽略更改文件总数少于 10% 的目录，并在父目录中累积子目录计数：`--dirstat=files,10,cumulative`。

`--summary`

输出扩展头部信息的压缩摘要，例如创建、重命名和模式更改。

`--patch-with-stat`

`-p` `--stat` 的同义词。

`-z`

当给出 `--raw`、`--numstat`、`--name-only` 或 `--name-status` 时，不对路径进行处理，并使用 `NUL` 作为输出字段分隔符。

如果没有此选项，每个输出的路径会将 `TAB`、`LF`、双引号和反斜杠字符替换为 `\t`、`\n`、`\"` 和 `\\`，如果发生了任何替换，路径将被双引号包围。

`--name-only`

仅显示更改的文件名。

`--name-status`

仅显示更改的文件名和状态。关于状态字母的含义，请参见 `--diff-filter` 选项的描述。

`--submodule[=<format>]`

指定子模块差异的显示方式。当给出 `--submodule` 或 `--submodule=log` 时，使用 `log` 格式。该格式像 (1)`summary` 一样列出范围内的提交。省略 `--submodule` 选项或指定 `--submodule=short` 则使用 `short` 格式。该格式仅显示范围开头和结尾的提交名称。可以通过 `diff.submodule` 配置变量进行调整。

`--color[=<when>]`

显示彩色的 diff。`--color`（即没有 `=<when>`）与 `--color=always` 相同。`<when>` 可以是 `always`、`never` 或 `auto` 之一。

`--no-color`

关闭彩色 diff。它与 `--color=never` 相同。

`--word-diff[=<mode>]`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

- `color`：仅使用颜色高亮更改的单词。隐含 `--color`。
- `plain`：将单词显示为 `[-removed-]` 和 `{+added+}`。如果出现分隔符，则不尝试进行转义。
- `porcelain`：输出扩展头部信息的压缩摘要，例如创建、重命名和模式更改。
- `none`：禁用单词 diff。

`--word-diff-regex`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-stat`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-fragment`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-regex=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-stat=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-fragment=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--diff-filter`

仅显示更改的文件名和状态。关于状态字母的含义，请参见 `--diff-filter` 选项的描述。

`--word-diff-regex`

`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-regex`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-stat`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-fragment`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-regex=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-stat=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

`--word-diff-fragment=<mode>`

显示单词 diff，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

### `--find-copies-harder`

出于性能考虑，默认情况下 `-C` 选项仅在副本的原始文件在同一变更（`changeset`）中被修改时才会查找副本。此标志位使命令检查未修改的文件作为复制源的候选文件。对于大型项目来说，这是一个非常昂贵的操作，请谨慎使用。提供多个 `-C` 选项的效果相同。

### `-D`, `--irreversible-delete`

省略删除操作的原始镜像（`preimage`），即只打印头信息，而不打印镜像与 `/dev/null` 之间的差异。生成的补丁并非用于通过 `patch` 或 `git apply` 应用；这仅适用于只想专注于在更改后查看文本的人。此外，输出显然缺乏反向应用此类补丁的信息（即使手动操作也无法），这也是该选项命名的由来。

与 `-B` 配合使用时，还会省略删除/创建对中删除部分的镜像。

### `-l<num>`



`-M` 和 `-C` 选项需要 `O(n²)` 处理时间，其中 `n` 是潜在重命名/复制目标的数量。当重命名/复制目标的数量超过指定数量时，此选项将防止重命名/复制检测运行。

## `--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]`

仅选择已添加 (`A`)、复制 (`C`)、删除 (`D`)、修改 (`M`)、重命名 (`R`)、类型发生变化 (`T`，即普通文件、符号链接、子模块等...)、未合并 (`U`)、未知 (`X`) 或配对损坏 (`B`)的文件。可以使用过滤器字符的任何组合（包括不包含）。当组合中添加 `*`（全有或全无）时，如果比较中有任何文件匹配其他标准，则选择所有路径；如果没有文件匹配其他标准，则不选择任何内容。

## `-S<string>`

查找文件中指定字符串出现次数发生变化（即添加/删除）的差异。该选项旨在供脚本编写人员使用。

当你正在寻找一个精确的代码块（如结构体），并想知道该块自诞生以来的历史时，它非常有用：迭代使用此功能，将镜像中感兴趣块馈回 `-S`，直到获取该块的最早版本。

## `-G<regex>`

查找补丁文本中包含匹配 `<regex>` 的添加/删除行的差异。

为了说明 `-S<regex> --pickaxe-regex` 与 `-G<regex>` 之间的区别，考虑同一文件中具有以下差异的提交：

```
+ return !regexec(regexp, two->ptr, 1, &regmatch, 0); ... - hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
```

虽然 `git log -G"regexec\(regexp"` 会显示此提交，但 `git log -S"regexec\(regexp" --pickaxe-regex` 则不会（因为该字符串的出现次数没有变化）。

更多信息见 `(7)` 中的 *pickaxe* 条目。

## `--pickaxe-all`

当 `-S` 或 `-G` 找到更改时，显示该变更中的所有更改，而不仅仅是包含 `<string>` 的文件。

## `--pickaxe-regex`

将传递给 `-S` 的 `<string>`视为扩展 POSIX 正则表达式进行匹配。

## `-O<orderfile>`

按照 `<orderfile>` 中指定的顺序输出补丁，该文件每行有一个 shell 通配符模式（glob pattern）。这会覆盖 `diff.orderFile` 配置变量（见 `(1)`）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

## `-R`

交换两个输入；即从索引或磁盘文件到树内容的差异。

## `--relative[=<path>]`

当从项目的子目录下运行时，可以通过此选项指示排除目录之外的更改，并显示相对于该目录的路径名。当你不在子目录中（例如在裸仓库中）时，可以通过提供 `<path>` 参数来指定相对于哪个子目录输出输出。

## `-a`, `--text`

将所有文件视为文本。

## `--ignore-space-at-eol`

忽略行尾（EOL）空白的变化。

## `-b`, `--ignore-space-change`

忽略空白数量的变化。这会忽略行尾的空白，并将所有其他一个或多个空白字符序列视为等效。

## `-w`, `--ignore-all-space`

在比较行时忽略空白。即使一行有空白而另一行没有，也会忽略这些差异。

## `--ignore-blank-lines`

忽略所有行均为空白更改。

## `--inter-hunk-context=<lines>`

显示差异块（hunks）之间的上下文，最多到指定的行数，从而合并相邻的块。

## `-W`, `--function-context`

显示更改周围的完整函数。

## `--exit-code`

使程序以类似于 `(1)` 的状态码退出。即，如果有差异则退出码为 `1`，`0` 表示没有差异。

## `--quiet`

禁用程序的所有输出。隐含 `--exit-code`。

## `--ext-diff`

允许执行外部 diff 助手。如果你通过 `(5)` 设置了外部 diff 驱动程序，则需要配合 `(1)` 等选项使用此选项。

## `--no-ext-diff`

不允许外部 diff 驱动程序。

## `--textconv`, `--no-textconv`

在比较二进制文件时允许（不允许）运行外部文本转换过滤器。详情见 `(5)`。由于 textconv 过滤器通常是单向转换，生成的差异适用于人类阅读，但无法被应用。由于原因，textconv 过滤器默认仅对 `(1)` 和 `(1)` 启用，而不用于 `(1)` 或 diff plumbing 命令。

## `--ignore-submodules[=<when>]`

在生成差异时忽略对子模块的更改。`<when>` 可以是 `"none"`、`"untracked"`、`"dirty"` 或 `"all"`，默认为 `all`。使用 `"none"` 时，当子模块包含未跟踪或修改的文件，或者其 HEAD 与父项目中记录的提交不同时，会将子模块视为已修改，并可覆盖 `(1)` 或 `(5)` 中 *ignore* 选项的任何设置。使用 `"untracked"` 时，如果子模块仅包含未跟踪的内容，则不将其视为脏（但仍对其修改内容进行扫描）。使用 `"dirty"` 会忽略对子模块工作树的所有更改，仅显示存储在父项目中的提交更改（这是 `1.7.0` 之前的行为）。使用 `"all"` 会隐藏对子模块的所有更改。

## `--src-prefix=<prefix>`

显示指定的源前缀代替 `"a/"`。

## `--dst-prefix=<prefix>`

显示指定的目标前缀代替 `"b/"`。

## `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的更详细解释，请见 `(7)`。

## `-1 --base`, `-2 --ours`, `-3 --theirs`, `-0`

分别与“基础”版本、“我们的分支”或“他们的分支”进行对比。使用这些选项时，不会显示合并条目的差异。

默认是与我们的分支 (`-2`) 以及清理解析的路径进行对比。可以提供 `-0` 选项来省略未合并条目的差异输出，仅显示“Unmerged”。

## `-c`, `--cc`

此比较阶段 `2`（我们的分支）、阶段 `3`（他们的分支）和工作树文件，并输出一个合并差异，类似于 *diff-tree* 使用这些标志显示合并提交的方式。

## `-q`

即使文件不存在也保持静默

## 原始输出格式

来自 `"git-diff-index"`、`"git-diff-tree"`、`"git-diff-files"` 和 `git diff --raw` 的原始输出格式非常相似。

这些命令都比较两组事物；但比较的对象有所不同：

```
git-diff-index <tree-ish>
```

比较 `<tree-ish>` 和文件系统上的文件。

```
git-diff-index --cached <tree-ish>
```

比较 `<tree-ish>` 和索引。

```
git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [<pattern>...]
```

比较由两个参数指定的树。

```
git-diff-files [<pattern>...]
```

比较索引和文件系统上的文件。

`"git-diff-tree"` 命令在输出开始时打印比较对象的哈希值。之后，所有命令都会为每个更改的文件打印一行输出。

输出行的格式化如下：

```
in-place edit :100644 100644 bcd1234... 0123456... M file0 copy-edit :100644 100644 abcd123... 1234567... C68 file1 file2 rename-edit :100644 100644 abcd123... 1234567... R86 file1 file3 create :000000 100644 0000000... 1234567... A file4 delete :100644 000000 1234567... 0000000... D file5 unmerged :000000 000000 0000000... 0000000... U file6
```

也就是说，从左到右：

1. 一个冒号。

2. `"src"` 的模式；如果是创建或未合并，则为 `000000`。

3. 一个空格。

4. `"dst"` 的模式；如果是删除或未合并，则为 `000000`。

5. 一个空格。

6. `"src"` 的 `sha1`；如果是创建或未合并，则为 `0{40}`。

7. 一个空格。

8. `"dst"` 的 `sha1`；如果是创建、未合并或“查看工作树”，则为 `0{40}`。

9. 一个空格。

10. 状态，后面跟一个可选的 `"score"` 数字。

11. 使用 `-z` 选项时为制表符（TAB）或 NUL 字符。

12. `"src"` 的路径。

13. 使用 `-z` 选项时为制表符或 NUL；仅存在于 C 或 R 类型。

14. `"dst"` 的路径；仅存在 C 或 R 类型。

15. 使用 `-z` 选项时为 LF 或 NUL，用于结束记录。

可能的状态字母有：

- `A`：添加文件

- `C`：将文件复制到新文件中

- `D`：删除文件

- `M`：修改文件的内容或模式

- `R`：重命名文件

- `T`：更改文件类型

- `U`：文件未合并（在提交之前，你必须完成合并）

- `X`：“未知”更改类型（极可能是一个 bug，请报告它）

状态字母 `C` 和 `R` 后面总是会跟上分数（表示移动或复制的源和目标之间的相似性百分比）。状态字母 `M` 后面在文件重写时可能会跟上一个分数（表示差异性百分比）。

如果文件在文件系统中是新的且与索引不同步，则 `<sha1>` 显示为全 `0`。

示例：

```
:100644 100644 5be4a4...... 000000...... M file.c
```

当不使用 `-z` 选项时，路径中的 TAB、LF 和反斜杠字符分别表示为 `\t`、`\n` 和 `\\`。

## 合并的差异格式

`git-diff-tree`、`git-diff-files` 和 `git diff --raw` 可以接受 `-c` 或 `--cc` 选项来为合并提交生成差异输出。输出与上述描述的格式不同之处：

1. 每个父节点都有一个冒号。

2. 有多个 `"src"` 模式和 `"src"` sha1。

3. 状态是每个父节点状态字符的拼接。

4. 没有可选的 `"score"` 数字。

5. 单路径，仅针对 `"dst"`。

示例：

```
::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c
```

注意，“合并差异”（combined diff）仅列出从所有父节点修改的文件。

## 使用 `-P` 生成补丁

当运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files` 并带有 `-p` 选项，不带 `--raw` 选项的 `git diff`，或带有 `-p` 选项的 `git log` 时，它们不会产生上述输出；而是产生一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量来自定义此类补丁的创建。

`-p` 选项产生的内容与传统的 diff 格式略有不同：

1. 前面有一个这样的 `"git diff"` 头部：

```
diff --git a/file1 b/file2
```

除非涉及重命名/复制，否则 `a/` 和 `b/` 文件名是相同的。具体来说，即使是创建或删除，也不会用 `/dev/null` 替代 `a/` 或 `b/` 文件名。当涉及重命名/复制时，`file1` 和 `file2` 分别显示重命名/复制的源以及重命名/复制产生的文件名。

2. 后面跟着一个或多个扩展头部行：

```
old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
```

文件模式以 6 位八进制数字打印，包括文件类型和文件权限位。扩展头部中的路径不包含 `a/` 和 `b/` 前缀。相似性索引是未更改行的百分比，差异性索引是更改行的百分比。这是一个向下取整的整数，后面跟着一个百分号。因此，`100%` 的相似性索引值留给两个相同的文件，而 `100%` 的差异意味着旧文件中没有某一行进入了新文件。索引行包含了更改前后的 SHA-1 校验和。如果文件模式没有变化，则包含 `<mode>`；否则，用单独的行指示旧模式。

3. 路径中的 TAB、LF、双引号和反斜杠字符分别表示为 `\t`、`\n`、`\"` 和 `\\`。如果需要此类替换，则整个路径将放在双引号中。

4. 所有 `file1` 文件引用提交前的文件，而 `file2` 文件引用提交后的文件。

## 合并差异格式

任何生成差异的命令都可以接受 `-c` 或 `--cc` 选项来产生合并的*差异*（combined diff）。这是为了审查合并更改。

1. 前面有一个这样的 `"git diff"` 头部（使用 `-c` 选项）：

```
diff --combined file
```

或者如下（使用 `--cc` 选项）：

```
diff --cc file
```

2. 后面跟着一个或多个扩展头部行（此示例显示两个父节点的合并）：

```
index <hash>..<hash> mode <mode>,<mode>
```

只有当至少一个 `<mode>` 不同时，才会出现 `mode <mode>,<mode>` 行。关于检测内容的扩展头部旨在用于两个 `<tree-ish>` 的差异，不用于合并差异格式。

3. 后面跟着两行的源文件/目标文件头部：

```
--- a/file
+++ b/file
```

类似于传统*统一*格式的双行头部，使用 `/dev/null` 来指示创建或删除的文件。

4. 块头部格式经过修改，以防止人们误将其传递给 `-p`：

```
@@@ <from-file-range> <from-file-range> <to-file-range> @@@
```

合并差异格式的块头部中有（父节点数量 + 1）个 `@` 字符。与传统的*统一*格式显示两个文件 A 和 B 并带有单列 `-`（表示 A 有但 B 无）、`+`（表示 A 无但 B 有）或 `" "`（表示未更改）不同，这种格式比较两个或多个文件 `file1, file2,...` 与一个文件 X，并显示 X 与每个文件的差异。每个 `fileN` 的一个列都置于输出行前面，以说明 X 的行与其不同之处。

第 `N` 列中的 `-` 意味着该行出现在 `fileN` 中但没有出现在结果中。第 `N` 列中的 `+` 意味着该行出现在结果中，而 `fileN` 没有该行（也就是说，从该父节点的角度来看，该行被添加了）。

在上面的示例输出中，函数签名在两个文件中都发生了变化（因此在 `file1` 和 `file2` 中都删除了两个部分，并加上 `++` 表示添加的一行代码既没有出现在 `file1` 中也没有出现在 `file2` 中）。此外，还有 8 行与 `file1` 相同但未出现在 `file2` 中（因此以 `+` 为前缀标记）。

当使用 `git diff-tree -c` 显示时，它会将合并提交的父节点与合并结果进行比较（即 `file1..fileN` 是父节点）。当使用 `git diff-files -c` 显示时，它会将两个未解析的合并父节点与工作树文件进行比较（即 `file1` 是阶段 2，亦“我们的版本”，`file2` 是阶段 3，亦“他们的版本”）。

## 其他 Diff 格式

`--summary` 选项描述新添加、删除、重命名和复制的文件。`--stat` 选项在输出中添加 `(1)` 图表。这些选项可以与其他选项（如 `-p`）结合使用，旨在供人类阅读。

当显示涉及重命名或复制的更改时，`--stat` 输出通过合并路径的公共前缀和后缀来紧凑地格式化路径。例如，将 `arch/i386/Makefile` 移动到 `arch/x86/Makefile` 同时修改 4 行的更改将显示如下：

`arch/{i386 => x86}/Makefile | 4 +--`

`--numstat` 选项提供 `(1)` 信息，但设计用于便于机器读取。`--numstat` 输出中的条目如下：

`1 2 README 3 1 arch/{i386 => x86}/Makefile`

即，从左到右：

1. 添加的行数；

2. 一个制表符；

3. 删除的行数；

4. 一个制表符；

5. 路径（可能包含重命名/复制信息）；

6. 换行符。

当 `-z` 输出选项生效时，输出格式如下：

`1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL`

即：

1. 添加的行数；

2. 一个制表符；

3. 删除的行数；

4. 一个制表符；

5. 一个 `NUL`（仅在重命名/复制时存在）；

6. 镜像前的路径；

7. 一个 `NUL`（仅在重命名/复制时存在）；

8. 镜像后的路径（仅在重命名/复制时存在）；

9. 一个 `NUL`。

在重命名情况下，镜像路径之前的额外 `NUL` 是为了让读取输出的脚本判断当前读取的记录是单路径记录还是重命名/复制记录，而无需预读。在读取添加和删除行后，读取到 `NUL` 即可获得路径，但如果它是 `NUL`，则该记录将显示两个路径。

# Git-Diff-Index

## 名称

`git-diff-index` - 比较树与工作树或索引

## 概要



# `git diff-index`

```text
git diff-index [-m] [--cached] [<common diff options>] <tree-ish> [<path>...]
```

## 描述

将树对象中找到 blob 内容和模式与工作树中对应的跟踪文件比较，或与索引中对应的路径比较。当存在 `<path>` 参数时，仅比较匹配这些模式的路径。否则，将比较所有跟踪文件。

## 选项

### `-p, -u, --patch`

生成补丁（参见生成补丁的章节）。

### `-s, --no-patch`

抑制 diff 输出。适用于像 `git show` 这样默认显示补丁的命令，或取消 `--patch` 的效果。

### `-U<n>, --unified=<n>`

生成具有 `<n>` 行上下文的 diff，而不是通常的三个行。隐含 `-p`。

### `--raw`

以原始格式生成 diff。这是默认设置。

### `--patch-with-raw`

`-p --raw` 的别名。

### `--minimal`

花费额外时间以确保产生尽可能小的 diff。

### `--patience`

使用“patience diff”算法生成 diff。

### `--histogram`

使用“histogram diff”算法生成 diff。

### `--diff-algorithm={patience|minimal|histogram|myers}`

选择一种 diff 算法。其变体如下：

- `default, myers`：基础贪婪 diff 算法。目前是默认值。
- `minimal`：花费额外时间确保产生尽可能小的 diff。
- `patience`：在生成补丁时使用“patience diff”算法。
- `histogram`：该算法扩展了 patience 算法以“支持低频公共元素”。

例如，如果你将 `diff.algorithm` 变量配置为默认值并并使用默认值，则必须使用 `--diff-algorithm=default` 选项。

### `--stat[=<width>[,<name-width>[,<count>]]]`

生成 diffstat。默认情况下，将使用尽可能的空间用于文件名部分，其余用于图表部分。最大宽度默认为终端宽度，如果没有连接到终端则为 80 列，并可以通过 `<width>` 覆盖。通过在逗号后提供另一个宽度 `<name-width>` 可以限制文件名部分的宽度。图部分的宽度可以通过使用 `--stat-graph-width=<width>`（影响所有生成统计图表的命令）或设置 `diff.statGraphWidth=<width>` 来限制。

### `--numstat`

类似于 `--stat`，但以十进制显示添加和删除的行数，且不缩写。

### `--shortstat`

仅输出 `--stat` 的最后一行，包含文件总数以及添加和删除的行数。

### `--dirstat[=<param1,param2,...>]`

输出每个子目录更改的分布。dirstat 的行为可以通过传递逗号分隔的参数列表进行自定义。默认由 `diff.dirstat` 配置控制（见 1）。可用参数如下：

- `changes`：通过计算从源删除或添加到目的地的行来计算 dirst 数字。这忽略文件内部的移动。也就是说，文件内的排序不被视为更改。这是未提供参数时的默认行为。
- `lines`：通过基于行的 diff 分析来计算 dirst 数字，并汇总删除/添加计数。（对于二进制文件，计算 64 字节块，因为二进制文件没有自然的行概念）。这比 `changes` 行为开销更大，但它会计算文件内的排序。输出结果与其他 `--stat` 选项一致。
- `files`：通过计算更改的文件数量来计算 dirst 数字。每个更改的文件在 dirstat 中计数相等。这是计算成本最低的 dirstat 行为，因为它无需查看文件内容。
- `cumulative`：同时为父目录计算子目录的更改。注意，使用累计时，报告的百分比总和可能会超过 100%。默认（非累计）行为可以通过 `noncumulative` 参数指定。
- `<limit>`：整数参数指定截止百分比（默认为 3%）。贡献小于此百分比的目录不会显示在输出中。

示例：以下命令将计算更改的文件，忽略占比小于 10% 的目录，并将子目录计数累计到父目录：`--dirstat=files,10,cumulative`。

### `--summary`

输出扩展头（如创建、重命名和模式更改）的压缩摘要。

### `--patch-with-stat`

`-p --stat` 的别名。

### `-z`

当给出 `--raw`、`--numstat`、`--name-only` 或 `--name-status` 时，不要处理路径并使用 NUL 作为输出字段终止符。如果没有此选项，每个输出的路径将 TAB、LF、双引号和反斜杠字符替换为 `\t`、`\n`、`\"` 和 `\\`，如果发生了其中任何替换，则路径将用双引号包围。

### `--name-only`

仅显示更改的文件名。

### `--name-status`

显示更改的文件名及其状态。

仅显示更改文件的名称和状态。查看 `--diff-filter` 选项的描述以了解状态字母的含义。

### `--submodule[=<format>]`

指定显示子模块差异的方式。当给出 `--submodule` 或 `--submodule=log` 时，使用 `log` 格式。该格式列出范围内的提交，类似于 `(1)summary` 的格式。省略 `--submodule` 选项或指定 `--submodule=short`，则使用 `short` 格式。该格式仅显示范围开头和结尾的提交名称。可以通过 `diff.submodule` 配置变量进行调整。

### `--color[=<when>]`

显示彩色差异。`--color`（即不带 `<when>`）与等同于 `--color=always`。`<when>` 可以是 `always`、`never` 或 `auto` 之一。

### `--no-color`

关闭彩色差异。它等同于 `--color=never`。

### `--word-diff[=<mode>]`

显示单词差异，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白字符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，且必须是以下之一：

- `color`：仅使用颜色突出显示更改的单词。隐含 `--color`。
- `plain`：将单词显示为 `[-removed-]` 和 `{+added+}`。如果分隔符出现在输入中，则不尝试对其进行转义，因此输出可能存在歧义。
- `porcelain`：使用一种专用于脚本读取的特殊行格式。添加/删除/未更改的运行将以标准的统一差异格式打印，行首以 `+`/`-`/` ` 字符开头并延伸到行尾。输入中的换行由单独占一行的波浪 `~` 表示。
- `none`：再次禁用单词差异。

注意，尽管第一个模式名为 `color`，但如果启用，`color` 将在所有模式下突出显示更改的部分。

### `--word-diff-regex=<regex>`

使用 `<regex>` 来决定什么是一个单词，而不是将连续的非空白字符视为单词。如果尚未启用，则也会隐含 `--word-diff`。

`<regex>` 的每个非重叠匹配项都被视为一个单词。这些匹配项之间的任何内容都被视为空白字符并在查找差异时被忽略！你可能想向你的正则表达式中添加 `|[^[:space:]]` 以确保它匹配所有非空白字符。包含换行符的匹配项会在换行处被静默截断！

正则也可以通过 diff 驱动程序或配置选项设置，见 `(1)` 或 `(1)`。显式提供它将覆盖任何 diff 驱动程序或配置设置。diff 驱动程序覆盖配置设置。

### `--color-words[=<regex>]`

等同于 `--word-diff=color` 加上（如果指定了正则）`--word-diff-regex=<regex>`。

### `--no-renames`

关闭重命名检测，即使配置文件默认执行该操作。

### `--check`

如果更改引入了空格错误则发出警告。什么被视为空格错误由 `core.whitespace` 配置控制。默认情况下，尾随空格（包括由空白组成的行）以及行初始缩进内紧跟在制表符后的空格字符被视为空格错误。如果发现问题，则以非零状态退出。与 `--exit-code` 不兼容。

### `--ws-error-highlight=<kind>`

以 `color.diff.whitespace` 指定颜色突出显示由 `<kind>` 指定行上的空格错误。`<kind>` 是旧的、新的、上下文的逗号分隔列表。当未给出此选项时，仅突出显示新行的空格错误。例如，`--ws-error-highlight=new,old` 会突出显示被删除和添加行的空格错误。`all` 可以作为 `old,new,context` 的简写。

### `--full-index`

在生成补丁格式输出时，在 `"index"` 行上显示完整的原始和后续 blob 对象名称，而不是前几个字符。

### `--binary`

除了 `--full-index` 之外，输出一个可以使用 `git-apply` 应用的二进制差异。

### `--abbrev[=<n>]`

在 `diff-raw` 格式输出和 `diff-tree` 行中，不显示完整的 40 字节十六进制对象名称，而是显示部分前缀。这与上述 `--full-index` 选项独立，后者控制 diff-patch 输出格式。可以通过 `--abbrev=<n>` 指定非默认数字位数。

### `-B[<n>][/<m>], --break-rewrites[=[<n>][/<m>]]`

将完全重写的更改拆分为删除和创建的对。此有两个作用：

1. 它影响等同于文件完全重写的更改的处理方式，使其不是一系列删除和插入与极少数在文本上匹配的上下文行混合在一起，而是作为所有旧内容的单个删除，随后是由于所有新内容的单个插入。数字 `m` 控制 `-B` 选项的这方面（默认为 60%）。`-B/70%` 指定如果结果中剩余少于 30% 的原始内容，则 Git 将其视为完全重写（否则生成的补丁将是一系列混合了上下文行的删除和插入）。
2. 当与 `-M` 一起使用时，完全重写的文件也被视为重名的源（通常 `-M` 只考虑消失的文件作为重名的源），且数字 `n` 控制 `-B` 选项的这方面（默认为 50%）。`-B20%` 指定与文件大小相比增加和删除达到 20% 或以上的更改有资格被 pick 选择为重命名到另一个文件的可能源。

### `-M[<n>], --find-renames[=<n>]`

检测重命名。如果指定了 `n`，它是相似性索引的阈值。例如，`-M90%` 意味着如果文件超过 90% 没有更改，Git 应该将一个删除/添加对视为重命名。如果没有 `%` 号，该数字被读作分值，前面有一个小数点。即 `-M5` 变为 `0.5`，因此等同于 `-M50%`。要将检测限制为精确重命名，请使用 `-M100%`。默认相似性索引为 50%。

### `-C[<n>], --find-copies[=<n>]`

检测复制以及复制。见 `--find-copies-harder`。如果指定了 `n`，它的含义与 `-M<n>` 相同。

### `--find-copies-harder`

出于性能考虑，默认情况下 `-C` 选项仅在复制的原始文件在同一更改集中被修改时才查找复制。此标志使命令检查未修改的文件作为候选源。对于大型项目，这是一个非常昂贵的操作，请谨慎使用。提供多个 `-C` 选项的效果相同。

### `-D, --irreversible-delete`

省略删除操作的镜像（preimage），即仅打印头信息，但不打印镜像与 `/dev/null` 之间的差异。生成的补丁不是用于 `patch` 或 `git apply`；这仅适用于只想关注更改后文本的人。此外，输出显然缺少反向应用此类补丁的信息，因此有了该选项的名称。与 `-B` 配合使用时，还会省略删除/创建对中删除部分的镜像。

### `-l<num>`

`-M` 和 `-C` 选项需要 `O(n²)` 处理时间，其中 `n` 是潜在重命名/复制目标的数量。此选项在重命名/复制目标超过指定数字时防止重命名/复制检测运行。

### `--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]`

仅选择新增（A）、复制（C）、删除（D）、修改（M）、重命名（R）、类型（例如普通文件、符号链接、子模块……）更改（T）、未合并（U）、未知（X）或配对损坏（B）的文件。可以使用过滤字符的任何组合（包括空组合）。当将 `*`（全有或无）添加到组合中时，如果比较中有任何一个符合其他标准的文件，则选择所有路径；如果没有符合其他标准的文件，则不选择任何内容。

### `-S<string>`

查找文件中更改了指定字符串出现次数（即添加/删除）的差异。旨在供脚本人员使用。

当你正在寻找某个特定的代码块（如结构体），并想知道该代码块自诞生以来的历史时，此功能非常有用：反复使用该功能，将感兴趣的代码块的镜像部分回馈给 `-S`，直到获取该代码块的最早版本。

### `-G<regex>`

查找补丁文本中包含匹配 `<regex>` 的新增/删除行的差异。

为了说明 `-S<regex> --pickaxe-regex` 和 `-G<regex>` 之间的区别，请考虑在同一文件中具有以下差异的提交：

```diff
+ return !regexec(regexp, two->ptr, 1, &regmatch, 0); ... - hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
```

虽然 `git log -G"regexec\(regexp"` 会显示此提交，但 `git log -S"regexec\(regexp" --pickaxe-regex` 则不会显示（因为该字符串出现的次数没有变化）。

更多信息请参阅 (7) 中的 `pickaxe` 条目。

### `--pickaxe-all`

当 `-S` 或 `-G` 发现变化时，显示该变更集中的所有更改，而不仅仅是包含 `<string>` 变化的文件。

### `--pickaxe-regex`

将传递给 `-S` 的 `<string>` 视为扩展 POSIX 正则表达式进行匹配。

### `-O<orderfile>`

按照 `<orderfile>` 指定的顺序输出补丁，该文件每行有一个 shell glob 通配模式。这会覆盖 `diff.orderFile` 配置变量（见 (1)）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

### `-R`

交换两个输入；即显示索引或磁盘文件到树内容的差异。

### `--relative[=<path>]`

当从项目的子目录下运行时，可以通过此选项忽略该目录之外的更改，并显示相对于该目录的路径。当你不在子目录中（例如在裸仓库中）时，可以通过提供参数 `<path>` 来指定哪个子目录的相对输出。

### `-a, --text`

将所有文件视为文本。

### `--ignore-space-at-eol`

忽略行尾（EOL）空白字符的变化。

### `-b, --ignore-space-change`

忽略空白字符数量的变化。这会忽略行尾的空白，并将所有其他一个或多个空白字符序列视为等效。

### `-w, --ignore-all-space`

在比较行时忽略空白字符。即使其中一行有空白而另一行没有，也会忽略这些差异。

### `--ignore-blank-lines`

忽略所有行都为空的更改。

### `--inter-hunk-context=<lines>`

显示差异块（diff hunks）之间的上下文，最多到指定的行数，从而合并相邻的差异块。

### `-W, --function-context`

显示更改周围的完整函数。

### `--exit-code`

使程序以类似于 (1) 的代码退出。即，如果存在差异则以 1 出，无差异则以 0 出。

### `--quiet`

禁用程序的所有输出。隐含 `--exit-code`。

### `--ext-diff`

允许执行外部 diff 助手。如果你通过 (5) 设置了外部 diff 驱动程序，则需要配合 (1) 等选项一起使用此选项。

### `--no-ext-diff`

不允许外部 diff 驱动程序。

### `--textconv, --no-textconv`

在比较二进制文件时允许（或不允许）运行外部文本转换过滤器。详情见 (5)。由于 `textconv` 过滤器通常是单向转换，生成的 diff 适用于人类阅读，但无法应用。因此，`textconv` 过滤器默认仅对 (1) 和 (1) 启用，而不适用于 (1) 或 diff 底层管道命令。

### `--ignore-submodules[=<when>]`

在生成差异时忽略子模块的更改。`<when>` 可以是 `"none"`、`"untracked"`、`"dirty"` 或 `"all"`，后者是默认值。使用 `"none"` 时，如果子模块包含未跟踪或修改的文件，或者其 HEAD 与主项目记录的提交不同，则认为子模块已修改，这可用于覆盖 (1) 或 (5) 中 `ignore` 选项的任何设置。使用 `"untracked"` 时，如果子模块仅包含未跟踪的内容，则不认为它是脏（但仍会对修改内容进行扫描）。使用 `"dirty"` 会忽略对子模块工作树的所有更改，仅显示存储在主项目中的提交的更改（这是 1.7.0 之前的行为）。使用 `"all"` 则隐藏对子模块的所有更改。

### `--src-prefix=<prefix>`

显示指定的源前缀代替 `"a/"`。

### `--dst-prefix=<prefix>`

显示指定的目标前缀代替 `"b/"`。

### `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的更详细解释，请参阅 (7)。

## `<tree-ish>`



用于对比的树对象的 ID。

`--cached`

完全不考虑磁盘文件。

`-m`

默认情况下，索引中记录但未检出的文件被报告为删除。此标记使 `git diff-index` 所有未检出的文件都是最新的。

## 原始输出格式

`git-diff-index`、`git-diff-tree`、`git-diff-files` 和 `git diff --raw` 的原始输出格式非常相似。

这些命令都比较两组东西；但比较的对象不同：

`git-diff-index <tree-ish>`

比较 `<tree-ish>` 和文件系统上的文件。

`git-diff-index --cached <tree-ish>`

比较 `<tree-ish>` 和索引。

`git-diff-tree [-r] <pattern>...]`

比较树。

`git-diff-files [<pattern>...]`

比较索引和文件系统。

当运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files` 并带有 `-p` 参数，或者不带 `--raw` 参数的 `git diff`，带有 `-p` 参数的 `git log` 时，它们不会产生上述输出；而是产生一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量自定义此类补丁的创建。

`-p` 参数产生的输出与传统的 diff 格式略有不同：

1. 它前面有一个如下所示的 `git diff` 头部：

```diff
diff --git a/file1 b/file2
```

除非涉及重命名/复制，否则 `a/` 和 `b/` 文件名是相同的。特别是，即使是创建或删除，也**没有**使用 `/dev/null` 来代替 `a/` 或 `b/` 文件名。

当涉及重命名/复制时，`file1` 和 `file2` 分别显示重命名/复制源文件名以及重命名/复制产生的文件名。

2. 它后面跟着一个或多个扩展头部行：

```text
old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
```

文件模式以 6 位八进制数字打印，包括文件类型和权限位。扩展头中的路径名不包含 `a/` 和 `b/` 前缀。

相似索引（similarity index）是未更改行的百分比，差异索引（dissimilarity index）是更改行的百分比。它是一个向下取整的整数，后跟一个百分号。因此，100% 的相似索引值留给两个相同的文件，而 100%差异意味着旧文件中没有一行进入新文件。

索引行包含了更改前后的 SHA-1 校验和。如果文件模式没有变化，则包含 `<mode>`；否则，用单独的行指示旧模式。

3. 路径中的 `TAB`、`LF`、双引号和反斜杠字符分别表示为 `\t`、`\n`、`\"` 和 `\\`。如果需要此类替换，则整个路径名会被放在双引号中。

4. 输出中所有的 `file1` 文件均指提交之前的文件，所有的 `file2` 文件均指提交之后的文件。将每个更改顺序应用到每个文件是错误的。例如，此补丁将交换 `a` 和 `b`：

```diff
diff --git a/a b/b rename from a rename to b diff --git a/b b/a rename from b rename to a
```

## 合并 diff 格式 (COMBINED DIFF FORMAT)

任何生成 diff 的命令都可以显示合并时都可以 `-c` 或 `--cc` 参数来产生“合并 diff”（combined diff）。这是显示带有 (1) 或 (11) 次合并时的默认格式。请注意，你也可以给这些命令中的任何一个提供 `-m` 参数，以强制生成合并单个父节点的 diff。

`合并 diff` 格式如下：

```diff
diff --combined describe.c index fabadb8,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) ++static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

1. 它前面有一个 `git diff` 头部，如下所示（当使用 `-c` 参数时）：

```diff
diff --combined file
```

或者如下所示（当使用 `--cc` 参数时）：

```diff
diff --cc file
```

2. 它后面跟着一个或多个扩展头部行（此示例显示了一个带有两个父节点的合并）：

```text
index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>
```

`<mode>,<mode>..<mode>` 行仅在至少有一个 `<mode>` 与其他模式不同时出现。带有有关检测到的内容移动（重命名和复制检测）信息的扩展头设计用于用于两个 `<tree-ish>` 之间的 diff，不用于合并 diff 格式。

3. 它后面跟着两行的源文件/目标文件头部

```diff
--- a/file ++++ b/file
```

与传统的 `unified` diff 格式的双行头部类似，使用 `/dev/null` 来指示已创建或删除的文件。

4. 块头部格式经过修改，以防止人们无意将其交给 `patch -p1`。合并 diff 格式是为了审查合并提交的更改而设计的，并非用于应用。更改与扩展 `index` 头部类似：

```diff
@@@ <from-file-range> <from-file-range> <to-file-range> @@@
```

合并 diff 格式是为了审查合并提交的更改而设计的，并非用于应用。更改与扩展 `index` 头部类似。

## 其他格式

`--summary` 参数描述新添加、删除、重命名和复制的文件。`--stat` 参数在输出中添加 (1) 图表。这些选项可以与其他参数（如 `-p`）组合，供人类阅读。

当显示涉及重命名或复制的更改时，`--stat` 输出通过组合路径名的公共前缀和后缀来格式化路径名。例如，将 `arch/i386/Makefile` 移动到 `arch/x86/Makefile` 同时修改 4 行的更改将显示为：

```text
arch/{i386 => x86}/Makefile | 4
```

`--numstat` 参数提供 (1) 信息，但旨在便于机器读取。`--numstat` 输出条目如下：

```text
1 2 README 3 1 arch/{i386 => x86}/Makefile
```

即，从左到右：

1. 添加的行数；

2. 一个制表符；

3. 删除的行数；

4. 一个制表符；

5. 路径名（可能带有重命名/复制信息）；

6. 换行符。

当 `-z` 输出选项生效时，输出格式如下：

```text
1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL
```

即：

1. 添加的行数；

2. 一个制表符；

3. 删除的行数；

4. 一个制表符；

5. 一个 `NUL`（仅在重命名/复制时存在）；

6. 镜像前的路径名；

7. 一个 `NUL`（仅在重命名/复制时存在）；

8. 后的路径名（仅在重命名/复制时存在）；

9. 一个 `NUL`。

重命名情况下镜像路径前的额外 `NUL` 是为了让读取输出的脚本判断当前读取的记录是单路径记录还是重命名/复制记录，而无需预读。在读取添加和删除行后，读取到 `NUL` 将得到路径名，但如果它是 `NUL`，则记录将显示两个路径。

你可以选择是完全信任索引文件（使用 `--cached` 标记），还是让 diff 逻辑将任何与状态（stat）状态不匹配的文件显示为“暂存更改”。这两种操作实际上非常有用。

## 缓存模式 (CACHED MODE)

如果指定了 `--cached`，它允许你询问：

`显示我 HEAD 和当前索引内容之间的差异（即我通过 'git write-tree' 写入的内容）`

例如，假设你在工作目录中进行了工作，更新了索引中的某些文件，并准备好提交。你想确切地看到你将提交**什么**，而无需编写一个新的树对象并并通过那种方式进行比较。为了做到，你只需要执行：

```
git diff-index --cached HEAD
```

示例：假设我将 `commit.c` 重命名为 `git-commit.c`，并执行了 `update-index` 使该更改在索引文件中生效。`git diff-files` 将不会显示任何内容，因为索引文件与我的工作目录匹配。但执行 `git diff-index` 就会显示：

```
:~/git> git diff-index --cached HEAD -100644 blob 4161aecc6700a2eb579e842af0b7f22b98443f74 commit.c +100644 blob 4161aecc6700a2eb579e842af0b7f22b98443f74 git-commit.c
```

你可以很容易地看到上面是一个重命名。

事实上，`git diff-index --cached` 应该完全等同于实际执行 `git write-tree` 并对其进行比较。只是在你只想检查自己所处位置时，这种方法要优雅得多。

所以，当你通过 `git diff-index --cached` 来询问“我已经标记了哪些内容要提交，它们与之前的树有什么区别”时，基本上是非常用的。

## 非缓存模式 (NON-CACHED MODE)

“非缓存”模式采取了不同的方法，在两种模式中可能更有用，因为它的功能无法通过 `git write-tree` + `git diff-tree` 来模拟。因此，这是默认模式。非缓存版本提出的问题是：

`显示 HEAD 与当前检出的树之间的差异 - 索引内容 _ 以及 _ 未更新的文件文件`

这显然也是一个非常有用的问题，因为它告诉了你**可以**提交什么。再次，其输出与 `git diff-tree -r` 的输出完全一致，但有一个转折。

这个转折在于，如果某些文件与索引不匹配，我们没有为它们提供底层存储，因此我们使用魔术“全零”sha1 来显示这一点。假设你编辑了 `kernel/sched.c`，但尚未对它实际执行 `git update-index` —— 新状态下没有与之关联的“对象”，你会得到：

```
:~/v2.6/linux> git diff-index --abbrev HEAD :100644 100664 7476bb... 000000... kernel/sched.c
```

即：它显示树已经发生了变化，且 `kernel/sched.c` 不是最新的，并可能包含新内容。全零的 sha1 意味着要获取真实的差异，你需要直接查看工作目录中的对象，而不是进行对象之间的差异比较。

## 注意事项

与其他此类类型的命令一样，`git diff-index` 实际上根本不查看文件内容。所以可能 `kernel/sched.c` 并没有实际变化，只是你触碰了它。无论何种情况，这提示你需要执行 `git update-index` 来使索引同步。

## 注意事项

你可以同时看到显示“已更新”和“在工作目录中仍为脏”的文件。你始终可以判断哪个文件处于哪种状态，因为“已更新”的文件显示的是有效的 sha1，而“与索引不同步”的文件将始终具有特殊的全零 sha1。

***

# GIT-DIFF-TREE

## 名称

`git-diff-tree` - 比较通过两个树对象找到 blob 的内容和模式

## 语法

`git diff-tree` [--stdin] [-m] [-s] [-v] [--no-commit-id] [--pretty] [-t] [-r] [-c | --cc] [--root] [<common diff options>] <tree-ish> [<tree-ish>] [<path>...]`

## 

比较通过两个树对象找到 blob 的内容和模式。

如果只给出一个 `<tree-ish>`，则将提交与其父提交进行比较（见下文 --stdin）。

注意 `git diff-tree` 可以使用提交对象封装的树。

### 选项

- `-p, -u, --patch`

  生成补丁（参见生成补丁的章节）。

- `-s, --no-patch`

  抑制 diff 输出。适用于像 `git show` 这样默认显示补丁的命令，或取消 `--patch` 的效果。

- `-U<n>, --unified=<n>`

  生成具有 `<n>` 行上下文的差异，而不是通常的三行。隐含了 `-p`。

- `--raw`

  以原始格式生成差异。这是默认设置。

- `--patch-with-raw`

  `-p` 的同义词。

- `--minimal`

  花费额外时间确保产生最小的差异。

- `--patience`

  使用“patience”算法生成差异。

- `--histogram`

  使用“histogram”算法生成差异。

- `--diff-algorithm={patience|minimal|histogram|myers}`

  选择一种差异 算法。变体有：

  - `myers`: 基础贪心算法。目前是默认值。

  - `minimal`: 花费额外时间确保产生最小的差异。

  - `patience`: 使用“patience”算法。

  - `histogram`: 该算法扩展了 patience 算法以支持公共元素。

- `--stat[=<width>,<name-width>,<count>]`

  生成统计。默认情况下，将使用尽可能的空间用于文件名，其余空间用于图表部分。最大宽度默认为终端，如果没有连接到终端则为 80 列，并可以通过 `<width>` 覆盖。通过提供第三参数 `<count>`，你可以将输出限制为前 `<count>` 行，如果更多，则显示 ...。这些参数也可以通过 `--stat-width=<width>`、`--stat-name-width=<name-width>` 和 `--stat-count=<count>` 单独设置。

- `--numstat`

  与 `--stat` 类似，但以十进制符号显示添加和删除的行数以及不带缩写的路径名，以便于机器处理。对于二进制文件，输出两个 `--` 而不是说 0。

- `--shortstat`

  仅输出 `--stat` 格式的最后一行，其中包含修改文件的总数，以及添加和删除的行数。

- `--dirstat[=<param1,param2,...>]`

  输出每个子目录相对变化量的分布。`--dirstat` 的行为可以通过传递逗号分隔的参数列表进行自定义。默认值由 `diff.dirstat` 配置变量控制（见 (1)）。可用参数如下：

  - `changes`: 通过计算从源删除的行或向目标添加的行数来计算 dirstat 数字。这忽略了文件内部纯代码移动量。换句话说，在文件内重新排列行的计算不像与其他变化那样多。这是未提供参数时的默认行为。

  - `lines`: 通过执行常规行的差异分析来计算 dirstat 数字，并累加删除/添加的行数。（对于二进制文件，计算 64 字节块，因为二进制文件没有自然的行概念）。这是比 `changes` 行为更耗资源的 dirstat 行为，但它将文件内重新排列行的计算与与其他变化一样多。

  - `files`: 通过计算更改的文件数量来计算 dirstat 数字。每个更改的文件在 dirstat 分析中权重相等。这是计算上最廉价的 dirstat 行为，因为它完全查看文件内容。

### 选项

将子目录的更改也计入父目录。注意，当使用 `cumulative` 时，报告的百分比总和可能会超过 100%。默认（非累积）行为可以通过 `noncumulative` 参数指定。

### `<limit>`

一个整数参数，用于指定截止百分比（默认为 3%）。变化小于此百分比的目录将不会显示在输出中。

示例：以下命令将统计更改的文件，同时忽略变化少于总文件数 10% 的目录，并在父目录中累积子目录计数：`--dirstat=files,10,cumulative`。

### `--summary`

输出扩展头部信息的简要摘要，例如创建、重命名和模式更改。



### `--patch-with-stat`

`-p`、`--stat` 的别名。

### `-z`

当给出 `--raw`、`--numstat`、`--name-only` 或 `--name-status` 时，不要处理路径名，并使用 `NUL` 作为输出字段分隔符。

如果没有此选项，每个输出的路径名将把 `TAB`、`LF`、双引号和反斜杠分别替换为 `\t`、`\n`、`\"` 和 `\\`。如果发生了其中任何替换，路径名将被包含在双引号中。

### `--name-only`

仅显示更改文件的名称。

### `--name-status`

仅显示更改文件的名称和状态。查看 `--diff-filter` 选项的描述以了解状态字母的含义。

### `--submodule[=<format>]`

指定子模块差异的显示方式。当给出 `--submodule` 或 `--submodule=log` 时，使用 `log` 格式。该格式列出范围内的提交，类似于 `(1)summary` 的。省略 `--submodule` 选项或指定 `--submodule=short` 则使用 `short` 格式。该格式仅显示范围开始和结束的提交名称。可以通过 `diff.submodule` 配置变量进行调整。

### `--color[=<when>]`

显示带颜色的差异。`--color`（即不带 `=<when>`）等同于 `--color=always`。`<when>` 可以是 `always`、`never` 或 `auto` 之一。

### `--no-color`

关闭彩色差异。它等同于 `--color=never`。

### `--word-diff[=<mode>]`

显示单词差异，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空格分隔；见下文 `--word-diff-regex`。`<mode>` 默认为 `plain`，必须是以下之一：

- `color`：仅使用颜色突出更改的单词。隐含 `--color`。
- `plain`：将单词显示为 `[-removed-]` 和 `{+added+}`。如果输入中出现分隔符，则不尝试转义，因此输出可能存在歧义。
- `porcelain`：使用一种专为脚本读取的特殊行格式。添加、删除、未更改的运行按通常的统一差异格式打印，每行以 `+`、`-` 或空格字符开头，并延伸到行尾。输入中的换行符由单独占一行的波浪号 `~` 表示。
- `none`：再次禁用单词差异。

请注意，尽管第一种模式名为 `color`，但如果启用了颜色，`color` 将用于突出所有模式下的更改部分。

### `--word-diff-regex=<regex>`

使用 `<regex>` 来决定什么是单词，而不是将连续的非空白字符视为单词。除非已启用，否则也隐含 `--word-diff`。

`<regex>` 的每个非重叠匹配都被视为一个单词。这些匹配之间的任何内容都被视为空格，并在查找差异时被忽略（`!`）。你可能想向正则表达式添加 `|[^[:space:]]`，以确保它匹配所有非空白字符。包含换行符的匹配会在换行处被静默截断（`!`）。

正则也可以通过 diff 驱动或配置选项设置，见 `(1)` 或 `(1)`。显式给出将覆盖任何 diff 驱动或配置设置。diff 驱动覆盖配置设置。

### `--color-words[=<regex>]`

等同于 `--word-diff=color` 以及（如果指定了正则）`--word-diff-regex=<regex>`。

### `--no-renames`

关闭重命名检测，即使配置文件默认开启了。

### `--check`

如果更改引入了空格错误则警告。什么被视为空格错误由 `core.whitespace` 配置控制。默认情况下，行尾空格（包括仅由空格组成的行）以及行初始缩进内紧随制表符的空格被视为空格错误。如果发现问题，则以非零状态退出。与 `--exit-code` 不兼容。

### `--ws-error-highlight=<kind>`

用 `color.diff.whitespace` 指定的颜色突出 `<kind>` 指定行上的空格错误。`<kind>` 是用逗号分隔的列表 `old`、`new`、`context`。当未给出此选项时，仅突出新行中的空格错误。例如，`--ws-error-highlight=new,old` 突出被删除和添加行的空格错误。所有都可以作为 `old,new,context` 的简写。

### `--full-index`

在生成补丁格式输出时，在“index”行上显示完整的前后镜像 blob 对象名称，而不是前几个字符。

### `--binary`

除了 `--full-index` 之外，输出可以使用 `git-apply` 应用的二进制差异。

### `--abbrev[=<n>]`

在 diff-raw 格式输出和 diff-tree 头部行中不再显示完整的 40 字节十六进制对象名称，而是显示部分前缀。这与上述控制 diff-patch 输出格式的 `--full-index` 选项独立。可以通过 `--abbrev=<n>` 指定非默认的位数。

### `-B[=<n>][/<m>], --break-rewrites[=<n>]]]]`

将完全重写的更改分解为删除和创建对。这有两个用途：

它影响将一个相当于文件完全重写的更改处理方式，视为一次删除所有旧内容，随后是一次插入所有新内容，只有极少数行在文本上匹配作为上下文；数字 `m` 控制 `-B` 选项的这方面（默认为 60%）。`-B70%` 指定当原始内容保留部分少于 30% 时，Git 才会将其考虑为完全重写（即否则生成的补丁将是一系列删除和插入的混合）。

当与 `-M` 使用时，完全重写的文件也被视为重命名源（通常 `-M` 只考虑消失的文件作为重命名源），数字 `n` 控制 `-B` 选项的这方面（默认为 50%）。`-B20%` 指定与文件大小相比，添加和删除达到 20% 或更多的更改有资格被选为重命名到另一个文件的可能源。

### `-M[=<n>], --find-renames[=<n>]`

检测重命名。如果指定了 `n`，它是相似性索引阈值（即与文件大小相比的添加/删除量）。例如，`-M90%` 意味着如果文件有超过 90% 未更改，Git 应该将一个删除/添加对视为重命名。如果没有 `%` 符号，该数字被读取为分数，前面带有小数点。即，`-M5` 变为 `0.5`，因此等于 `-M50%`。同样，`-M05` 等于 `-M5%`。要将检测限制为精确重命名，请使用 `-M100%`。默认相似性索引为 50%。

### `-C[=<n>], --find-copies[=<n>]`

检测拷贝以及重命名。见 `--find-copies-harder`。如果指定了 `n`，其含义与 `-M<n>` 相同。

### `--find-copies-harder`

出于性能考虑，默认 `-C` 选项仅在拷贝的原文件在同一更改集中被修改时才查找拷贝。此标志使命令检查未修改的文件作为拷贝源的候选。对于大型项目来说这是一个非常昂贵的操作，请谨慎使用。提供多个 `-C` 选项效果相同。

### `-D, --irreversible-delete`

在删除操作时省略原始文件（preimage），即只打印头部，而不打印原始文件与 `/dev/null` 之间的差异。生成的补丁并非用于通过 `patch` 或 `git apply` 应用；它仅适用于那些只想专注于查看更改后文本的人员。此外，输出内容显然缺乏足够反向应用此类补丁的信息（即使是手动操作），这也是该选项命名的由来。

与 `-B` 配合使用时，在删除/创建对的删除部分也省略原始文件。

### `-l<num>`

`-M` 和 `-C` 选项需要 `O(n²)` 处理时间，其中 `n` 是潜在重命名/复制目标的数量。如果重命名/复制目标的数量超过指定数量，此选项将防止重命名/复制检测运行。

### `--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]`

仅选择已添加（`A`）、复制（`C`）、删除（`D`）、修改（`M`）、重命名（`R`）、类型发生变化（即普通文件、符号链接、子模块等类型）（`T`）、未合并（`U`）、未知（`X`）或配对损坏（`B`）的文件。可以使用过滤器字符的任意组合（包括空组合）。当在组合中添加 `*`（全有全无）时，如果比较中存在任何符合其他标准的文件，则选择所有路径；如果没有符合其他标准的文件，则不选择任何内容。

### `-S<string>`

查找更改文件中指定字符串出现次数（即添加/删除）的差异。供脚本编写人员使用。

当你正在寻找一个精确的代码块（如 `struct`），并想知道该块自首次出现以来的历史时，此功能非常有用：迭代地使用该功能，将原始文件中的感兴趣的代码块馈回 `-S`，持续进行直到获得该代码块的最早版本。

### `-G<regex>`

查找补丁文本中包含匹配 `<regex>` 的添加/删除行的差异。

为了说明 `-S<regex> --pickaxe-regex` 与 `-G<regex>` 之间的区别，考虑一个在同一文件中具有以下差异的提交：

```text
+ return !regexec(regexp, two->ptr, 1, &regmatch, 0); ... - hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
```

虽然 `git log -G"regexec\(regexp"` 会显示此提交，但 `git log -S"regexec\(regexp" --pickaxe-regex` 则不会（因为该字符串的出现次数没有变化）。

更多信息请参见 `(7)` 中的 `pickaxe` 条。

### `--pickaxe-all`

当 `-S` 或 `-G` 找到更改时，显示该变更集中的所有更改，而不仅仅是包含 `<string>` 更改的文件。

### `--pickaxe-regex`

将传递给 `-S` 的 `<string>` 视为扩展 POSIX 正则表达式进行匹配。

### `-O<orderfile>`

按照 `<orderfile>` 中指定的顺序输出补丁，该文件每行有一个 shell glob 模式。这会覆盖 `diff.orderFile` 配置变量（见 `(1)`）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

### `-R`

交换两个输入；即显示索引或磁盘文件到树内容的差异。

### `--relative[=<path>]`

当从项目的子目录运行时，可以通过此选项告诉程序排除目录之外的更改，并显示相对于该目录的路径。当你不在子目录中（例如在裸仓库中）时，可以通过提供参数 `<path>` 来指定输出相对于哪个子目录。

### `-a, --text`

将所有文件视为文本。

### `--ignore-space-at-eol`

忽略行尾（EOL）空白的更改。

### `-b, --ignore-space-change`

忽略空白数量的变化。这会忽略行尾的空白，并将所有其他一个或多个空白字符序列视为等效。

### `-w, --ignore-all-space`

在比较行时忽略空白。即使某一行有空白而另一行没有，也会忽略差异。

### `--ignore-blank-lines`

忽略所有行均为空的更改。

### `--inter-hunk-context=<lines>`

显示差异块（hunks）之间的上下文，最多到指定的行数，从而合并距离彼此较近的块。

### `-W, --function-context`

显示更改周围的完整函数。

### `--exit-code`

使程序以类似于 `(1)` 的状态码退出。即，如果有差异则以 `1` 退出，无差异则以 `0` 退出。

### `--quiet`

禁用程序的所有输出。隐含 `--exit-code`。

### `--ext-diff`

允许执行外部 diff 助手。如果你通过 `(5)` 设置了外部 diff 驱动程序，则需要配合 `(1)` 等选项使用此选项。

### `--no-ext-diff`

不允许使用外部 diff 驱动程序。

### `--textconv, --no-textconv`

在比较二进制文件时允许（或禁止）运行外部文本转换过滤器。详情见 `(5)`。由于 textconv 过滤器通常是单向转换，生成的 diff 适用于人类阅读，但无法应用。出于此原因，textconv 过滤器默认对 `(1)` 和 `(1)` 启用，而不对 `(1)` 或 diff 工具命令启用。

### `--ignore-submodules[=<when>]`

在生成 diff 时忽略子模块。`<when>` 可以是 `"none"`、`"dirty"` 或 `"all"`，后者是默认值。使用 `"none"` 将考虑修改的子模块。使用 `"all"` 将隐藏所有子模块更改。

### `--src-prefix=<prefix>`

使用指定的源前缀代替 `a/`。

### `--dst-prefix=<prefix>`

使用指定的目标前缀代替 `b/`。

### `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的详细解释，请参见 `(7)`。

`<tree-ish>` 树的 ID。

`<path>...` 如果提供，结果将限于匹配这些字符串之一的文件子集。即文件匹配 `/pattern1|pattern2|.../`。

`-r` 递归进入树。

`-t` 显示树项本身以及子树。隐含 `-r`。

### `--root`

指定 `--root` 时，初始提交将作为一个事件显示。这等同于对比空树的 diff。

### `--stdin`

指定 `--stdin` 时，命令不从命令行获取 `<tree-ish>` 参数。相反，它从标准输入读取包含两个 `<tree>`、一个 `<commit>` 或一组 `<commit>` 的行。（使用单个空格作为分隔符。）

给出两个树时，比较第一个树和第二个树。给出一个提交时，比较该提交及其父提交。给出的剩余提交将被视为第一个提交的父提交。

当比较两个树时，在差异之前打印两个树的 ID（用空格分隔并换行终止）。当比较提交时，打印第一个（或唯一的）提交的 ID，后跟一个换行。

以下标志进一步影响比较提交（但不影响树）的行为：

- `-m`：默认情况下，`git diff-tree --stdin` 不显示合并提交的差异。使用此标志，将显示该提交相对于所有父提交的差异。参见 `-c`。
- `-s`：默认情况下，`git diff-tree --stdin` 显示差异，无论是机器可读格式（不带 `-p`）还是补丁格式（带 `-p`）。这种输出可以被抑制。它仅配合 `-v` 标志时有用。
- `-v`：此标志导致 `git diff-tree --stdin` 在差异之前还显示提交信息。

### `--pretty[=<format>], --format=<format>`

以指定的格式美化打印提交日志的内容，其中 `<format>` 可以是 `oneline`、`short`、`medium`、`full`、`fuller`、`email`、`raw`、`format:<string>` 和 `tformat:<string>` 之一。当 `<format>` 不是上述格式且包含 `%placeholder` 时，它的作用类似于指定了 `--pretty=tformat:<format>`。

请参见“PRETTY FORMATS”部分获取每个格式的更多详细信息。当省略 `=<format>` 部分时，默认为 `medium`。

注意：你可以在仓库配置中指定默认的美化格式（参见 `(1)`）。

### `--abbrev-commit`

此选项不再显示完整的 40 字节十六进制提交对象名称，而是仅显示部分前缀。可以使用 `--abbrev=<n>` 指定非默认的位数（如果显示了 diff 输出，也会修改该输出）。

这对于使用 80 列终端的用户来说，会让 `--pretty=oneline` 更具可读性。

### `--no-abbrev-commit`

显示完整的 40 字节十六进制提交对象名称。这会抵消 `--abbrev-commit` 以及隐含它的选项（如 `--oneline`）。它还会覆盖 `log.abbrevCommit` 变量。

### `--oneline`

这是 `--pretty=oneline --abbrev-commit` 结合使用的简写。

### `--encoding=<encoding>`

提交对象在它们的编码头中记录了用于日志消息的编码；此选项可用于命令按用户偏好的编码重新编码提交日志消息。对于非内部命令（plumbing commands），默认为 UTF-8。请注意，如果一个对象声称编码为 X 且我们正在输出 X，则我们将原样输出对象；这意味着原始提交中的无效序列可能会被复制到输出中。

### `--notes[=<ref>]`

在显示提交日志消息时，显示注释提交的注释（参见 `(1)`）。这是 `git log`、`git show` 和 `git whatchanged` 命令在命令行没有给出 `--pretty`、`--format` 或 `--oneline` 时的默认设置。

默认情况下，显示的注释来自 `core.notesRef` 和 `notes.displayRef` 变量列出的注释引用（或相应的环境变量覆盖）。参见 `(1)` 获取更多详细信息。

通过可选的 `<ref>` 参数，显示此注释引用而不是默认的注释引用。如果该引用未限定，则被认为位于 `refs/notes/` 下。

可以组合多个 `--notes` 选项来控制显示哪些注释。例如：`--notes=foo` 将仅显示来自 `refs/notes/foo` 的注释；`--notes=foo --notes` 将同时显示来自 `refs/notes/foo` 和默认注释引用的注释。

### `--no-notes`



不显示注释。这会抵消上述 `--notes` 选项，通过重置显示注释的注释引用列表来实现。选项按照命令行给出的顺序解析，例如，`--notes --notes=foo --no-notes --notes=bar` 只显示来自 `refs/notes/bar` 的注释。

### `--show-notes[=<ref>]`, `--[no-]standard-notes`

这些选项已弃用。请使用上述 `--notes/--no-notes` 选项。

### `--show-signature`

通过将签名传递给 `gpg --verify` 来检查签名提交对象的有效性并显示输出。

### `--no-commit-id`

`git diff-tree` 在适用时会输出一条带有提交 ID 的行。此标志抑制了提交 ID 的输出。

### `-c`

此标志更改合并提交的显示方式（这意味着它仅在给定一个 `<tree-ish>` 或 `--stdin` 时有用）。它同时显示每个父节点到合并结果的差异，而不是逐个显示父节点与结果之间的成对差异（这是 `-m` 选项的作用）。此外，它仅列出从所有父节点都被修改的文件。

### `--cc`

此标志更改合并提交补丁（patch）的显示方式，与 `-c` 选项类似。它隐含了 `-c` 和 `-p` 选项，并通过省略无趣的块（hunks）进一步压缩补丁输出，即这些块在父节点中的内容只有两种变体，且合并结果在未经修改的情况下选择了其中之一。当所有块都是无趣的时，不会显示提交本身和提交日志消息，就像任何其他“空差异”情况一样。

### `--always`

即使差异本身为空，也显示提交本身和提交日志消息。

## PRETTY FORMATS

如果提交是合并，且美化格式不是 `oneline`、`email` 或 `raw`，则在 `Author:` 行之前插入额外行。该行以 `"Merge: "` 开头，并打印祖先提交的 SHA-1，用空格分隔。请注意，如果你限制了历史视图，列出的提交不一定是直接父节点提交的列表：例如，如果你只对与特定目录或文件的更改感兴趣。

有几种内置格式，你可以通过将 `pretty.<name>` 配置选项设置为另一个格式名称或下文描述的 `format:` 字符串来定义附加格式（参见 (1)）。以下是内置格式的详细信息：

### `oneline`

```
<sha1> <title line>
```

此设计初衷是尽可能紧凑。

### `short`

```
commit <sha1> Author: <author>
<title line>
```

### `medium`

```
commit <sha1> Author: <author> Date: <author date>
<title line>
```

### `full`

```
commit <sha1> Author: <author> Date: <committer>
<title line>
```

### `fuller`

```
commit <sha1> Author: <author> Date: <committer date>
<title line>
<commit message>
```

### `email`

```
From <sha1> Author: <author> Date: <author date>

<title line>

<commit message>
```

### `raw`

`raw` 格式显示整个提交。特别是 SHA-1 是完整的，无论 `--abbrev` 如何，影响父节点。

### `format:<string>`

`format:<string>` 格式允许你指定想要显示的信息。它的用法类似于 `printf`，不同之处在于你会得到一个换行符 `%n`。例如，`format:"The author of %h was %s"` 会显示：

```
The author of fe6eee was Junio Hamano, 23 hours ago
```

占位符为：

- `%H`：提交哈希
- `%h`：短提交哈希
- `%T`：树哈希
- `%t`：短树哈希
- `%P`：父节点哈希
- `%p`：父节点哈希
- `%an`：作者名
- `%aN`：作者名（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%ae`：作者邮箱
- `%aE`：作者邮箱（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%ad`：作者日期（遵循 `--date=`）
- `%aD`：作者日期，RFC222 样式
- `%ar`：作者日期，相对日期
- `%at`：作者日期，Unix 时间戳
- `%ai`：作者日期，ISO 8601 格式
- `%aI`：作者日期，严格 ISO 8601 格式
- `%cn`：提交者名
- `%cN`：提交者名（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%ce`：提交者邮箱
- `%cE`：提交者邮箱（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%cd`：提交者日期（遵循 `--date=`）
- `%cD`：提交者日期，RFC222 样式
- `%cr`：提交者日期，相对日期
- `%ct`：提交者日期，Unix 时间戳
- `%ci`：提交者日期，ISO 8601 格式
- `%cI`：提交者日期，严格 ISO 8601 格式
- `%d`：引用名，类似于 (1) 的 `--decorate` 选项
- `%D`：引用名，无 `" (" ")"` 包裹
- `%e`：编码
- `%s`：主题
- `%f`：安全的主题行，适用于文件名
- `%b`：正文
- `%B`：正文（未解析的主题和正文）
- `%N`：提交注释
- `%GG`：签名提交的 GPG 原始验证消息
- `%G?`：签名良好显示“G”，签名错误显示“B”，良好但不可信的签名显示“U”，无签名显示“N”
- `%GS`：显示签名提交的签名者名称
- `%GK`：显示用于签名已提交的密钥
- `%gD`：reflog 选择器，例如 `refs/stash@{1}`
- `%gd`：简短的 reflog 选择器，例如 `stash@{1}`
- `%gn`：reflog 身份名称
- `%gN`：reflog 身份名称（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%ge`：reflog 身份邮箱
- `%gE`：reflog 身份邮箱（遵循 `.mailmap`，参见 (1) 或 (1)）
- `%gs`：reflog 主题
- `%Cred`：将颜色切换为红色
- `%Cgreen`：将颜色切换为绿色
- `%Cblue`：将颜色切换为蓝色
- `%Creset`：重置颜色
- `%C(...)`：规范，如 `color.branch.*` 配置选项所述；在开头添加 `auto` 将仅在日志输出启用了颜色时输出颜色（通过 `color.diff`、`color.ui` 或 `--color` 启用，并且如果目标是终端，则遵循前者的 `auto` 设置）。单独的 `auto`（即 `%C(auto)`）将在后续占位符处开启自动染色，直到颜色再次切换。
- `%m`：左、右或边界标记
- `%n`：换行符
- `%%`：原始 `%`
- `%x00`：从十六进制代码打印一个字节
- `%w([<w>[,<i1>[,<i2>]]])`：切换换行，类似于 (1) 的 `-w` 选项。
- `%<(<N>[,trunc|ltrunc|mtrunc])`：使下一个占位符至少占据 `N` 列，必要时在右侧填充空格。如果输出超过 `N` 列，可以选择在开头（`ltrunc`）、中间（`mtrunc`）或结尾（`trunc`）处截断。注意，截断仅在 `N >= 2` 时才能正常工作。
- `%<|(<N>)`：使下一个占位符至少占据到第 `N` 列，必要时在右侧填充空格。
- `%>(<N>)`、`%>|(<N>)`：分别类似于 `%<(<N>)` 和 `%<|(<N>)`，但在左侧填充空格。
- `%>>(<N>)`、`%>>|(<N>)`：分别类似于 `%>(<N>)` 和 `%>|(<N>)`，区别在于如果下一个占位符占据的空间比给定的多且其左侧有空格，则使用那些空格。
- `%><(<N>)`、`%><|(<N>)`：分别类似于 `%<(<N>)` 和 `%<|(<N>)`，但在两边都填充（即文本居中）。

**注意**

某些占位符可能取决于传递给修订遍历引擎的其他选项。例如，`%g*` reflog 选项除非我们正在遍历 reflog 条目（例如通过 `git log -g`），否则将插入空字符串。如果命令行上未提供 `--decorate`，`%d` 和 `%D` 占位符将使用“短”装饰格式。

如果你在占位符的 `%*` 之后添加 `+`（加号），则当且仅当占位符展开为非空字符串时，在展开之前插入一个换行符。

如果你在占位符的 `%*` 之后添加 `-`（减号），则当且仅当占位符展开为空字符串时，删除紧邻展开之前的换行符。

如果你在占位符的 `%*` 之后添加 ` `（空格），则当且仅当占位符展开为非空字符串时，在展开之前插入一个空格。

### `tformat:`

`tformat:` 格式的工作方式与 `format:` 完全相同，不同在于它提供“终止符”语义而不是“分隔符”语义。换句话说，每个提交都追加了消息终止符（通常是换行符），而不是在条目之间放置一个分隔符。这意味着单行格式的最后一个条目将用新行符正确终止，就像 `oneline` 格式一样。例如：

```
$ git log -2 --pretty=format:%h 4da45bef \
  | perl -pe '$_ .= " -- NO NEWLINE\n" unless /\n/'
4da45be 7134973 -- NO NEWLINE

$ git log -2 --pretty=tformat:%h 4da45bef \
  | perl -pe '$_ .= " -- NO NEWLINE\n" unless /\n/'
4da45be
7134973
```

此外，任何包含 `%` 的未识别字符串都被解释为其前面有 `tformat:`。例如，以下两者是等价的：

```
$ git log -2 --pretty=tformat:%h 4da45bef
$ git log -2 --pretty=%h 4da45bef
```

## 限制输出

如果你只对子集文件的差异感兴趣（例如某些特定架构的文件），你可以这样做：

```
git diff-tree -r <tree-ish> <tree-ish> arch/ia64 include/asm-ia64
```

它将向你显示那两个目录中变化的内容。

如果你只想搜索 `kernel/sched.c` 中发生了什么，只需执行：

```
git diff-tree -r <tree-ish> <tree-ish> kernel/sched.c
```

它将忽略所有其他文件的差异。

模式始终是前缀，并且是精确匹配。没有通配符。更严格的是，它必须匹配完整的路径组件。例如，“foo”不会匹配 `foobar.h`。“foo”会匹配 `foo/bar.h`，因此它可以用于命名子目录。

正常用法的示例是：

```
git diff-tree --abbrev 5319e4 :100664 ac348b... a01513... fs-objects.c
```

这告诉你最后一次提交只更改了一个文件。

## 原始输出

`git-diff-index`、`git-diff-tree`、`git-diff-files` 和 `git diff --raw` 的原始输出非常相似。这些命令都比较两个东西；不同在于：

`git diff-index <tree-ish>`

比较 `<tree-ish>` 和文件系统上的文件。

`git diff-index --cached <tree-ish>`

比较 `<tree-ish>` 和索引。

`git diff-tree [-r] <tree-ish-1> <tree-ish-2> [<pattern>...]`

比较由两个参数指定的树。

`git diff-files [<pattern>...]`

比较索引和文件系统上的文件。

`git-diff-tree` 命令通过打印正在比较内容的哈希值开始其输出。之后，所有命令为每个更改的文件打印一行输出。输出行的格式化方式如下：

```
:100644 100664 bcd1234... 0123456... M copy
:100644 100664 abcd123... 1234567... C rename
:100644 100664 abcd123... 1234567... R create
:000000 100664 000000... 1234567... A delete
:100644 000000... 1234567... D unmerged
:000000 000000... 000000... U file
```

也就是说，从左到右：

1. 一个冒号。
2. “源”的模式；如果是创建或未合并则为 `000000`。
3. 一个空格。
4. “目的”的模式；如果是删除或未合并则为 `000000`。
5. 一个空格。
6. “源”的 SHA-1；如果是创建或未合并则为 `0{40}`。
7. 一个空格。
8. “目的”的 SHA-1；如果是创建、未合并或“查看工作树”则为 `0{40}`。
9. 一个空格。
10. 状态，随后是可选的“分数”数字。
11. 使用 `-z` 选项时使用制表符或空。
12. “源”的路径。
13. 使用 `-z` 选项时使用制表符或空；仅存在 `C` 或 `R`。
14. “目的”的路径；仅存在于 `C` 或 `R`。
15. 使用 `-z` 选项时使用 LF 或空来结束记录。

可能的状态字母有：

- `A`：添加文件
- `C`：将文件复制到新文件
- `D`：删除文件
- `M`：修改文件内容或模式
- `R`：重命名文件
- `T`：文件类型更改
- `U`：文件未合并（必须在提交之前完成合并）
- `X`：“未知”更改类型（很可能是错误，请报告）

状态字母 `C` 和 `R` 总是跟随一个分数（表示移动或复制源与目标之间的相似性）。状态字母 `M` 对于文件重写可能会跟随一个分数（表示差异性）。

如果文件在文件系统中是新的且与索引不同，则 `<sha1>` 显示为全 0。

例如：

```
:100644 100664 5be4a4...... 000000...... M file.c
```

当未使用 `-z` 选项时，路径中的 TAB、LF 和反斜杠字符分别表示为 `\t`、`\n` 和 `\\`。

## 合并差异格式

`git-diff-tree`、`git-diff-files` 和 `git diff --raw` 可以带有 `-c` 或 `--cc` 选项为合并提交生成差异输出。输出与上述描述的格式不同之处在于：

1. 每个父节点有一个冒号。
2. 有更多的 `src` 模式和 `src` SHA-1。
3. `status` 是每个父节点状态字符的拼接。
4. 无可选的 `score` 数字。
5. 单一路径，仅用于 `dst`。

示例：

`::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c`

注意，`combined diff`（合并差异）仅列出从所有父节点都被修改的文件。

## 使用 `-P` 生成补丁

当运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files` 并带有 `-p` 选项，或者运行不带 `--raw` 选项的 `git diff` 或带有 `-p` 选项的 `git log` 时，它们不会产生上述输出；而是产生补丁文件（patch）。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量自定义此类补丁的创建。

`-p` 选项产生的内容与传统的 diff 格式略有不同：

1. 它以前一个类似于这样的 `"git diff"` 头部开头：

   `diff --git a/file1 b/file2`

   除非涉及重命名或复制，否则 `a/` 和 `b/` 文件名是相同的。特别是，即使是创建或删除，也不会用 `/dev/null` 代替 `a/` 或 `b/` 文件名。

   当涉及重命名或复制时，`file1` 和 `file2` 分别显示重命名或复制源文件名以及重命名或复制产生的文件。

2. 后面跟着一个或多个扩展头部行：

   `old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>`

   文件模式以 6 位八进制数字打印，包括文件类型和文件权限位。

   扩展头部中的路径名不包含 `a/` 和 `b/` 前缀。

   相似性索引（similarity index）是未更改行的百分比，差异性索引（dissimilarity index）是更改行的百分比。它是一个向下取整的整数，后跟一个百分号。因此，100% 的相似性索引值留给两个相同的文件，而 100% 的差异性意味着旧文件中没有行进入新文件。

   索引行包含了更改前后的 SHA-1 校验和。如果文件模式没有变化，则包含 `<mode>`；否则，用单独的行表示旧新模式。

3. 路径名中的 TAB、LF、双引号和反斜杠字符分别表示为 `\t`、`\n`、`\"` 和 `\\`。如果需要此类替换，整个路径名将放在双引号中。



## 4. 文件说明

输出中所有的 `file1` 文件都指提交之前的文件，所有的 `file2` 文件都指提交之后的文件。将每个更改按顺序应用到每个文件是错误的。例如，此补丁将交换 `a` 和 `b`：

```diff
diff --git a/a b/b
rename from a
rename to b
diff --git a/b b/a
rename from b
rename to a
```

## 合并差异格式（COMBINED DIFF FORMAT）

任何生成差异的命令都可以采取 `-c` 或 `--cc` 选项，在显示合并时产生 `combined diff`（合并差异）。这是在显示具有（1）或（1）个父节点的合并时的默认格式。注意，你也可以给这些命令中的任何一个提供 `-m` 选项，强制生成合并中各个父节点的差异。

`combined diff` 格式如下：

```text
diff --combined describe.c index fabadb8,cc95eb0..4866510
--- a/describe.c
+++ b/describe.c
@@@ -98,20 -98,12 +98,20 @@@
```

1. 它以前一个类似于 `git diff` 头部开头（当使用 `-c` 选项时）：

   `diff --combined file`

   或如下（当使用 `--cc` 选项时）：

   `diff --cc file`

2. 后面跟着一个或多个扩展头部行（此示例显示了两个父节点的合并）：

   `index <hash>,<hash>..<hash> mode <mode>,<mode>..<mode> new file mode <mode> deleted file mode <mode>,<mode>..<mode>`

   只有当至少一个 `<mode>` 与其他模式不同时，才会出现 `<mode>,<mode>..<mode>` 行。带有检测到的内容移动信息（重命名和复制检测）的扩展头部是为与两个 `<tree-ish>` 的差异而设计的，不被合并差异格式使用。

3. 后面紧跟两行的源文件/目标文件头部：

   ```text
   --- a/file
   +++ b/file
   ```

   与传统的 `unified`（统一）diff 格式的双行头部类似，使用 `/dev/null` 来指示创建或删除的文件。

4. 块头部格式经过了修改，以防止人们意外将其输入到 `patch -p1`。合并差异格式是为了审查合并提交的更改而创建，并非用于应用。该更改与扩展 `index` 头部的更改相似：

   `@@@ <from-file-range> <from-file-range> <to-file-range> @@@`

   合并差异格式的块头部中共有（父节点数量 + 1）个 `@` 字符。

与传统的 `unified` diff 格式不同（后者通过单列显示两个文件 `A` 和 `B`，该列带有 `-`（在 `A` 中出现但在 `B` 中删除）、`+`（在 `A` 中缺失但在 `B` 中添加）或 `" "`（空格，未更改）前缀），此格式将两个或多个文件 `file1`、`file2`……与一个文件 `X` 进行比较，并显示 `X` 如何不同于每个 `fileN`。每个 `fileN` 的一列附加在输出行之前，以说明 `X` 的变化。

```text
return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1;
} - static void describe(char *arg)
- static void describe(struct commit *cmit, int last_one)
++ static void describe(char *arg, int last_one)
{ + unsigned char sha1[20];
+ struct commit *cmit;
struct commit_list *list;
static int initialized = 0;
struct commit_name *n;
+ if (get_sha1(arg, sha1) < 0)
+ usage(describe_usage);
+ cmit = lookup_commit_reference(sha1);
+ if (!cmit)
+ usage(describe_usage);
+ if (!initialized) {
initialized = 1;
for_each_ref(get_name);
```

## 其他 diff 格式

`--summary` 选项描述新添加、删除、重命名和复制的文件。`--stat` 选项在输出中添加（1）统计信息。这些选项可以与 `-p` 等其他选项组合，供人类阅读。

当显示涉及重命名或复制的更改时，`--stat` 输出通过合并路径名的公共前缀和后缀来紧凑地格式化路径名。例如，将 `arch/i386/Makefile` 移动到 `arch/x86/Makefile` 同时修改 4 行的将显示为：

`arch/{i386 => x86}/Makefile | 4 +--`

`--numstat` 选项提供了（1）信息，但旨在便于机器读取。`--numstat` 输出中的条目如下：

`1 2 README 3 1 arch/{i386 => x86}/Makefile`

即从左到右：

1. 添加的行数；
2. 制表符；
3. 删除的行数；
4. 制表符；
5. 路径名（可能包含重命名或复制信息）；
6. 换行符。

当 `-z` 输出选项生效时，输出格式如下：

`1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL`

即：

1. 添加的行数；
2. 制表符；
3. 删除的行数；
4. 制表符；
5. `NUL`（仅在重命名或复制时存在）；
6. 原始路径名；
7. `NUL`（仅在重命名或复制时存在）；
8. 镜像路径名（仅在重命名或复制时存在）；
9. `NUL`。

在重命名情况下，重置镜像路径前的额外 `NUL` 是为了让读取输出的脚本能够在无需预读的情况下，判断当前读取的记录是单路径记录还是重命名或复制记录。在读取了添加和删除的行后，读取到 `NUL` 即可获得路径名，但如果为 `NUL`，则该记录将显示两个路径。

# GIT-DIFF

## 名称

`git-diff` - 显示提交之间、提交与工作树之间的更改等

## 语法

`git diff [options] [<commit>] [--] [<path>...]`

`git diff [options] --cached [<commit>] [--] [<path>...]`

`git diff [options] <commit> <commit> [--] [<path>...]`

`git diff [options] <blob> <blob>`

`git diff [options] [--no-index] [--] <path> <path>`

## 描述

显示工作树与索引（`index`）或树之间的更改、索引与树之间的更改、两个树之间的更改、两个 blob 对象之间的更改，或磁盘上两个文件之间的更改。

`git diff [--options] [--] [<path>...]`

此格式用于查看你相对于索引（下一次提交的暂存区）所做的更改。换句话说，差异是你可以告诉 Git 进一步添加到索引中但你尚未添加的内容。你可以通过（1）将这些更改进行暂存。

`git diff --no-index [--options] [--] [<path>...]`

此格式用于比较文件系统中给定的两个路径。当在 Git 控制的工作树中运行命令，且至少有一个路径指向工作树之外时，或者在由 Git 控制的工作树之外运行该命令时，可以省略 `--no-index` 选项。

`git diff [--options] --cached [<commit>] [--] [<path>...]`

此格式用于查看你相对于指定的 `<commit>` 为下一次提交已暂存的更改。通常你可能希望与最新提交进行比较，因此如果你没有给出 `<commit>`，它默认为 `HEAD`。如果 `HEAD` 不存在（例如未创建分支）且未给出 `<commit>`，则将显示所有暂存的更改。`--staged` 是 `--cached` 的别名。

`git diff [--options] <commit> [--] [<path>...]`

此格式用于查看你的工作树相对于指定的 `<commit>` 的更改。你可以使用 `HEAD` 与最新提交进行比较，或使用分支名称与不同分支的末端进行比较。

`git diff [--options] <commit> <commit> [--] [<path>...]`

此格式用于查看两个任意 `<commit>` 之间的更改。

`git diff [--options] <commit>..<commit> [--] [<path>...]`

这与前述格式同义。如果一侧的 `<commit>` 被省略，效果等同于使用 `HEAD`。

`git diff [--options] <commit>...<commit> [--] [<path>...]`

此格式用于查看包含 `<commit>` 直到第二个 `<commit>` 的分支上的更改，从两者的共同祖先开始。`"git diff A...B"` 等同于 `"git diff $(git-merge-base A B)" B`。你可以省略 `<commit>` 中的任何一个，效果等同于使用 `HEAD`。

以防万一，需要注意的是，在上述描述中，除了使用 `".."` 符号的最后两种格式外，所有的 `<commit>` 都可以是 `<tree>`。

要查看指定 `<commit>` 的更完整写法列表，请参见（7）中的“SPECIFYING REVISIONS”部分。然而，`diff` 是关于比较两个端点而不是范围，范围表示法（`<commit>..<commit>` 和 `<commit>...<commit>`）并不代表（7）中“SPECIFYING RANGES”部分中定义的范围。

`git diff [options] <blob> <blob>`

此格式用于查看两个 blob 对象原始内容之间的差异。

### 选项

- `-p, -u, --patch`

  生成补丁（参见生成补丁章节）。这是默认设置。

- `-s, --no-patch`

  抑制 diff 输出。对于默认显示补丁的 `git show` 等命令有用，或者用于取消 `--patch` 的效果。

- `-U<n>, --unified=<n>`

  生成具有 `<n>` 行上下文的 diff，而不是通常的三行。隐含了 `-p`。

- `--raw`

  以原始格式生成 diff。

- `--patch-with-raw`

  `-p` `--raw` 的别名。

- `--minimal`

  花费额外时间以确保产生尽可能小的差异。

- `--patience`

  使用 `"patience diff"` 算法生成 diff。

- `--histogram`

  使用 `"histogram diff"` 算法生成 diff。

- `--diff-algorithm={patience|minimal|histogram|myers}`

  选择一种 diff 算法。变体如下：

  - `default, myers`

    基础贪心 diff 算法。目前是默认值。

  - `minimal`

    花费额外时间以确保尽可能小的差异。

  - `patience`

    在生成补丁时使用 `"patience diff"` 算法。

  - `histogram`

    该算法扩展了 `patience` 算法以“支持低频率公共元素”。例如，如果你将 `diff.algorithm` 变量设为非默认值并想使用默认值，则你必须使用 `--diff-algorithm=default` 选项。

- `--stat[=<width>[,<name-width>[,<count>]]]`

  生成 `diffstat`。默认情况下，将尽可能多的空间用于文件名。

- `--numstat`

  与 `--stat` 类似，但十进制显示添加和删除的行数以及不缩写的路径名，以便机器处理。对于二进制文件，输出两个 `-` 而不是 0。

- `--shortstat`

  仅输出 `--stat` 的最后一行，其中包含修改文件的总数，以及添加和删除的行数。

- `--dirstat=<param1,param2,...>`

  输出每个子目录相对更改量的分布。`--dirstat` 的行为可以通过传递逗号分隔的参数列表来自定义。默认值由 `diff.dirstat` 配置控制（见（1））。可用参数如下：

  - `changes`

    通过计算从源删除的行或添加到目的的行数来计算 `dirstat` 数字。这忽略了文件内部的纯移动。换句话说，在文件中重新排列行不会被视为与其他更改同等数量。这是未给出参数时的默认行为。

  - `lines`

    通过进行常规基于行的 diff 分析并累加删除和添加的行数来计算 `dirstat` 数字。（对于二进制文件，计算 64 字节块，因为二进制文件没有自然的行概念。）这是比 `changes` 行为更耗资源的 `--dirstat` 行为，但它将文件内部重新排列的行视为与其他更改同等。产生的输出与从其他 `--*stat` 选项获得的结果一致。

  - `files`

    通过计算更改的文件数量来计算 `dirstat` 数字。每个更改的文件在 `dirstat` 分析中权重相等。这是计算上最便宜的 `--dirstat` 行为，因为它完全查看文件内容。

  - `cumulative`

    同样将子目录的更改计入父目录。注意，当使用 `cumulative` 时，报告的百分比总和可能会超过 100%。默认（非累积）行为可以通过 `noncumulative` 参数指定。

- `<limit>`

  整数参数指定一个截止百分比（默认为 3%）。贡献低于此百分比更改的目录将不会显示在输出中。

示例：以下命令将统计更改的文件，同时忽略更改数量少于总更改数 10% 的目录，并在父目录中累积子目录计数：`--dirstat=files,10,cumulative`。

### `--summary`

输出扩展头部信息的简要摘要，例如创建、重命名和模式更改。

### `--patch-with-stat`

`-p` `--stat` 的同义词。

### `-z`

当给出 `--raw`、`--numstat`、`--name-only` 或 `--name-status` 时，不对路径进行处理，并使用 `NUL` 作为输出字段终止符。

如果没有此选项，输出的每个路径将 TAB、LF、双引号和反斜杠字符分别替换为 `\t`、`\n`、`\"` 和 `\\`。如果发生了其中任何替换，则路径将被包含在双引号中。

### `--name-only`

仅显示更改文件的文件名。

### `--name-status`

仅显示更改文件的文件名和状态。请参考 `--diff-filter` 选项的描述以了解状态字母的含义。

### `--submodule[=<format>]`

指定子模块差异的方式。当给出 `--submodule` 或 `--submodule=log` 时，使用 `log` 格式。该格式像（1）`summary` 一样列出范围内的提交。省略 `--submodule` 选项或指定 `--submodule=short` 则使用 `short` 格式。该格式仅显示范围开头和结尾的提交名称。可以通过 `diff.submodule` 配置变量进行调整。

### `--color[=<when>]`

显示彩色 diff。`--color`（即不带 `=<when>`）等同于 `--color=always`。`<when>` 可以是 `always`、`never` 或 `auto` 之一。它可以通过 `color.ui` 和 `color.diff` 配置设置进行更改。

### `--no-color`

关闭彩色 diff。这可以用于覆盖配置设置。它等同于 `--color=never`。

### `--word-diff[=<mode>]`

显示单词差异，并使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，且必须是以下之一：

- `color`：仅使用颜色高亮更改的单词。隐含 `--color`。

- `plain`：将单词显示为 `[-removed-]` 和 `{+added+}`。如果输入中出现分隔符，则不尝试转义，因此输出可能是歧义的。

- `porcelain`：使用用于脚本消耗的特殊行格式。新增、删除和未更改的运行按标准的统一 diff 格式打印，行开头为 `+`、`-` 或空格字符并延伸到行尾。输入中的换行符由单独一行的波浪号 `~` 表示。

- `none`：再次禁用单词差异。

注意，尽管第一个模式名为 `color`，但如果启用，所有模式都会使用颜色高亮更改部分。

### `--word-diff-regex=<regex>`

使用 `<regex>` 来判断什么是单词，而不是将非空白字符视为单词。除非已启用，否则隐含 `--word-diff`。

`<regex>` 的每个非重叠匹配都被视为单词。这些匹配之间的任何内容都被视为空白符并在查找差异时被忽略！你可能想向你的正则表达式中附加 `|[^[:space:]]`，以确保它匹配所有非空白字符。包含换行符的匹配会在换行符处静默截断！

正则也可以通过 diff 驱动程序或配置选项设置，见（1）或（1）。显式给出将覆盖任何 diff 驱动程序或配置设置。diff 驱动覆盖配置设置。

### `--color-words[=<regex>]`

等同于 `--word-diff=color` 加上（如果指定了正则）`--word-diff-regex=<regex>`。

### `--no-renames`

关闭重命名检测，即使配置文件默认开启。



### `--check`

如果更改引入了空白错误则发出警告。什么被视为空白错误由`core.whitespace`配置控制。默认情况下，尾部空白（包括仅由空白组成的行）以及行初始缩进内紧跟制表符的空格字符被视为空白错误。如果发现问题，则以非零状态退出。不与`--exit-code`兼容。

### `--ws-error-highlight=<kind>`

在`color.diff.whitespace`指定的颜色中，高亮`<kind>`指定行的空白错误。`<kind>`是旧、新、上下文的逗号分隔列表。当未给出此选项时，仅高亮新行中的空白错误。例如，`--ws-error-highlight=new,old`会高亮删除和添加行的空白错误。所有都可以作为`old,new,context`的简写。

### `--full-index`

在生成 patch 格式输出时，在“index”行上显示完整的原始和后镜像 blob 对象名称，而不是前几个字符。

### `--binary`

除了`--full-index`外，输出一个可以使用`git-apply`应用的二进制 diff。

### `--abbrev[=<n>]`

在 diff-raw 格式输出和 diff-tree 头部行不再显示完整的 40 字节十六进制对象名称，而是仅显示部分前缀。这与上述控制 diff-patch 输出格式的`--full-index`选项无关。可以通过`--abbrev=<n>`指定非默认数字位数。

### `-B[<n>][/<m>], --break-rewrites[...]`

将完全重写的更改拆分为删除和创建对。这有两个目的：

1. 它影响文件的完全重写。
2. 它作为重命名检测的过滤器。

默认相似性索引为 60%。`-B/70%`指定原始文件保留少于 30% 时，Git 将其视为重命名。

### `-M[<n>], --find-renames=<n>]`

检测重命名。如果指定了`n`，它是相似性索引的阈值（即相对于文件大小的添加/删除数量）。例如，`-M90%`意味着如果文件有 90% 没有变化，Git 将将删除/添加对视为重命名。如果没有`%`号，该数字将被读取为带有小数点的分数。例如，`-M5`变为`0.5`，等同于`-M50%`。同样，`-M05`等同于`-M5%`。要限制为精确重命名，请使用`-M100%`。默认相似性索引为 50%。

### `-C[<n>], --find-copies[=<n>]`

同时也检测拷贝。见`--find-copies-harder`。如果指定了`n`，其含义与`-M<n>`相同。

### `--find-copies-harder`

出于性能考虑，默认情况下，`-C`选项仅当拷贝的原文件在同一变更集中被修改时才寻找拷贝。此标志使命令检查未修改的文件作为拷贝源。对于大型项目，这是一个非常昂贵的操作，请谨慎使用。给出多个`-C`选项效果相同。

### `-D, --irreversible-delete`

省略删除的镜像，即仅打印头部，但不打印镜像与`/dev/null`之间的 diff。生成的补丁无法供`patch`或`git apply`应用；这仅适用于只想专注于查看更改后文本的人。此外，输出显然缺少反向应用此类补丁的信息（即使是手动操作），因此该选项才如此。

与`-B`同时使用时，在删除/创建对的删除部分也省略镜像。

### `-l<num>`

`-M`和`-C`选项需要`O(n²)`处理时间，其中`n`是潜在重命名/拷贝目标的数量。如果重命名/拷贝目标的数量超过指定，此选项将防止重命名/拷贝检测运行。

### `--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]`

仅选择已添加 (A)、复制 (C)、删除 (D)、修改 (M)、重命名 (R)、类型更改（即普通文件、符号链接、子模块等...） (T)、未合并 (U)、未知 (X) 或配对断裂 (B) 的文件。可以使用过滤器字符的任意组合（包括不包含任何字符）。当在组合中添加`*`（全有或全无）时，如果比较中有任何文件符合其他标准，则将选择所有路径；如果没有文件符合其他标准的文件，则不选择任何内容。

### `-S<string>`

查找文件中指定字符串出现次数变化（即添加/删除）的差异。旨在供脚本编写人员使用。

当你正在寻找一个精确的代码块（如`struct`），并想知道该块自首次出现以来的历史时它非常有用：迭代使用该功能，将感兴趣的块的输入输入`-S`，持续进行直到获得该块的最早版本。

### `-G<regex>`

查找其补丁文本包含匹配`<regex>`的添加/删除行的差异。

为了说明`-S<regex> --pickaxe-regex`和`-G<regex>`之间的区别，考虑在同一文件中具有以下差异的提交：

```bash
+ return !regexec(regexp, two->ptr, 1, &regmatch, 0); ... - hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
```

虽然`git log -G"regexec\(regexp"`将显示此提交，但`git log -S"regexec\(regexp" --pickaxe-regex`则不会（因为该字符串的出现次数没有变化）。

更多信息请参阅 (7) 中的`pickaxe`条目。

### `--pickaxe-all`

当`-S`或`-G`找到更改时，显示该变更集中的所有更改，而不仅仅是包含`<string>`更改的文件。

### `--pickaxe-regex`

将传递给`-S`的`<string>`视为扩展 POSIX 正则表达式进行匹配。

### `-O<orderfile>`

按照`<orderfile>`指定的顺序输出补丁，该文件每行有一个 shell 通配符模式。这将覆盖`diff.orderFile`配置变量。要取消`diff.orderFile`，使用`-O/dev/null`。

### `-R`

交换两个输入；即从索引或磁盘文件显示到树内容的差异。

### `--relative[=<path>]`

当从项目的子目录运行时，可以通过此选项告诉它排除目录外的更改，并显示相对于该目录的路径。当你不在子目录中（例如在裸仓库中）时，可以通过提供参数`<path>`来指定哪个子目录的相对输出。

### `-a, --text`

将所有文件视为文本。

### `--ignore-space-at-eol`

忽略行尾空白的更改。

### `-b, --ignore-space-change`

忽略空白字符数量的变化。这会忽略行尾的空白，并将所有其他一个或多个空白字符序列视为等效。

### `-w, --ignore-all-space`

在比较行时忽略空白。即使其中一行有空白而另一行没有，也会忽略差异。

### `--ignore-blank-lines`

忽略所有行都为空的更改。

### `--inter-hunk-context=<lines>`

显示差异 hunk 之间的上下文，最多到指定的行数，从而合并彼此较近的 hunk。

### `-W, --function-context`

显示更改周围的完整函数。

### `--exit-code`

使程序以类似于 (1) 的代码退出。即，如果有差异，则以代码 1 退出，0 表示没有差异。

### `--quiet`

禁用程序的所有输出。隐含`--exit-code`。

### `--ext-diff`

允许执行外部 diff 助手。如果你用 (5) 设置了外部 diff 驱动程序，则需要配合 (1) 等选项使用此选项。

### `--no-ext-diff`

不允许外部 diff 驱动程序。

### `--textconv, --no-textconv`

在比较二进制文件时允许（或不允许）运行外部文本转换过滤器。详情见 (5)。由于 textconv 过滤器通常是单向转换，生成的 diff 适用于人类阅读，但无法应用。出于此原因，textconv 过滤器默认对 (1) 和 (1) 启用，而不对 (1) 或 diff plumbing 命令启用。

### `--ignore-submodules[=<when>]`

在生成 diff 时忽略对子模块的更改。`<when>`可以是`"none"`、`"untracked"`、`"dirty"`或默认的`"all"`。使用`"none"`，当子模块包含未跟踪或修改的文件，或者其`HEAD`与父项目记录的提交不同时，会被子模块已修改，它可以覆盖 (1) 或 (5) 中`ignore`选项的任何设置。使用`"untracked"`时，子模块仅包含未跟踪内容时不被视为脏（但仍会扫描修改内容）。使用`"dirty"`会忽略对子模块工作树的所有更改，仅显示存储在父项目中的提交的更改（这是 1.7.0 之前的行为）。使用`"all"`会隐藏对子模块的所有更改。

### `--src-prefix=<prefix>`

显示给定的源前缀代替`"a/"`。

### `--dst-prefix=<prefix>`

显示给定的目标前缀代替`"b/"`。

### `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的更详细解释，请参阅 (7)。

### `<path>...`

当给出`<paths>`参数时，用于将差异限制在指定的路径（你可以提供目录名称并获取其下所有文件的差异）。

## 原始输出格式

`git-diff-index`、`git-diff-tree`、`git-diff-files`和`git diff --raw`的原始输出格式非常相似。

这些命令都比较两组东西；比较的内容不同：

`git-diff-index <tree-ish>`

比较`<tree-ish>`和文件系统上的文件。

`git-diff-index --cached <tree-ish>`

比较`<tree-ish>`和索引。

`git-diff-tree [-r] <tree-ish-1> <tree-ish-2>`

`git-diff-tree <pattern>...`

比较由参数命名的树。

`git-diff-files [<pattern>...]`

比较索引和文件系统上的文件。`git-diff-tree`命令通过打印比较对象的哈希值开始输出。之后，所有命令每个更改的文件打印一行。输出行的格式如下：

```text
mode 10644 src_hash dst_hash path
```

也就是说，从左到右：

1. 一个冒号。
2. `"src"`的 mode；如果是创建或未合并则为`00000`。
3. 一个空格。
4. `"dst"`的 mode；如果是删除或未合并则为`00000`。
5. 一个空格。
6. `"src"`的 sha1；如果是创建或未合并则为`0{40}`。
7. 一个空格。
8. `"dst"`的 sha1；如果是创建、未合并或查看工作树则为`0{40}`。
9. 一个空格。
10. 状态，后面跟着可选的评分数字。
11. 使用`-z`选项时为制表符。
12. `"src"`的路径。
13. 使用`-z`选项时为制表符；仅存在 C 或 R。
14. `"dst"`的路径；仅存在 C 或 R。
15. 换行符或使用`-z`选项时为制表符，用于终止记录。

可能的状态字母为：

A：添加文件

C：将文件复制到新文件

D：删除文件

M：修改文件内容或模式

R：重命名文件

T：文件类型更改

U：文件未合并（你必须在提交前完成合并）

X：“未知”更改类型（很可能是错误，请报告）

状态字母 C 和 R 总是跟随一个评分（表示移动或复制源和目标之间的相似百分比）。状态字母 M 在文件重写时可能会跟随一个评分（表示差异百分比）。

如果文件在文件系统中是新的且与索引不同，则`<sha1>`显示为全 0。

### 示例

```text
:100644 100644 5be4a4...... 000000...... M file.c
```

当不使用`-z`选项时，路径中的`TAB`、`LF`和反斜杠字符分别表示为`\t`、`\n`和`\\`。

## 合并的 DIFF 格式

`git-diff-tree`、`git-diff-files`和`git diff --raw`可以接受`-c`或`--cc`选项为合并提交生成 diff 输出。该输出与上述描述的格式有以下不同：

1. 每个父节点前有一个冒号。
2. 有更多的`"src"`模式和`"src"`sha1。
3. 状态是每个父节点状态字符的拼接。
4. 没有可选的`"score"`数字。
5. 单路径，仅针对`"dst"`。

示例：

```text
::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM describe.c
```

注意，`combined diff`仅列出从所有父节点起修改的文件。

## 使用 `-P` 生成补丁

当运行`git-diff-index`、`git-diff-tree`或`git-diff-files`并带有`-p`选项，或者运行带`--raw`选项的`git diff`或带`-p`选项的`git log`，它们不会产生上述输出；而是产生补丁文件。你可以通过`GIT_EXTERNAL_DIFF`和`GIT_DIFF_OPTS`环境变量自定义此类补丁的创建。

`-p`选项产生的内容与传统的 diff 格式略有不同：

1. 它前面有一个像这样的`"git diff"`头部：

```text
diff --git a/file1 b/file2
```

除非涉及重命名/复制，否则`a/`和`b/`文件名是相同的。具体来说，即使对于创建或删除，也不会用`/dev/null`代替`a/`或`b/`文件名。

当涉及重命名/复制时，`file1`和`file2`分别显示重命名/复制的源文件名以及重命名/复制产生的文件名。

2. 后面跟着一个或多个扩展头部行：

```text
old mode <mode> new mode <mode> deleted file mode <mode> new file mode <mode> copy from <path> copy to <path> rename from <path> rename to <path> similarity index <number> dissimilarity index <number> index <hash>..<hash> <mode>
```

文件模式以 6 位八进制数字打印，包括文件类型和文件权限位。

扩展头部中的路径不包含`a/`和`b/`前缀。

相似性索引是未更改行的百分比，差异性索引是更改行的百分比。它是一个向下取整的整数，后面跟着一个百分号。因此，100% 的相似性索引值留给两个相同的文件，而 100% 的差异性意味着旧文件中没有一行进入了新文件。

索引行包含了更改前后的 SHA-1 校验和。如果文件模式没有变化，则包含`<mode>`；否则，用单独的行指示旧和新模式。

3. 路径中的`TAB`、`LF`、双引号和反斜杠字符分别表示为`\t`、`\n`、`\"`和`\\`。如果需要此类替换，则整个路径会被放在双引号中。

4. 输出中所有的`file1`文件均指提交之前的文件，所有的`file2`文件指提交之后的文件。将每个更改顺序应用到每个文件是错误的。例如，此补丁将交换 a 和 b：

```text
diff --git a/a b/b rename from a rename to b
diff --git a/b b/a rename from b rename to a
```

## 合并 diff 格式

任何生成 diff 的命令都可以接受`-c`或`--cc`选项，在显示合并时产生`combined diff`。这是显示具有 (1) 个或多个父节点的合并时的默认格式。还要注意，你也可以给这些命令中的任何一个提供`-m`选项，强制为合并的各个父节点生成 diff。

`combined diff`格式如下：

```text
diff --combined describe.c index fabadb8,cc95eb0..4866510 --- a/describe.c +++ b/describe.c @@@ -98,20 -98,12 +98,20 @@@ return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1; } - static void describe(char *arg) -static void describe(struct commit *cmit, int last_one) ++static void describe(char *arg, int last_one) { + unsigned char sha1[20]; + struct commit *cmit; struct commit_list *list; static int initialized = 0; struct commit_name *n; + if (get_sha1(arg, sha1) < 0) + usage(describe_usage); + cmit = lookup_commit_reference(sha1); + if (!cmit) + usage(describe_usage); + if (!initialized) { initialized = 1; for_each_ref(get_name);
```

1. 它前面有一个`"git diff"`头部，当使用`-c`选项时如下：

```text
diff --combined file
```

或者像这样（当使用`--cc`选项时）：

```text
diff --combined file
```

2. 后面跟着一个或多个扩展头部行：

```text
index <hash>..<hash> mode <mode>
```

使用了`index <hash>..<hash>`。



### 3. 路径格式

路径中的 `TAB`、`LF`、双引号和反斜杠字符分别表示为 `\t`、`\n`、`\"` 和 `\\`。如果需要此类替换，则整个路径会被放在双引号中。

`1 2 README NUL 3 1 NUL arch/i386/Makefile NUL arch/x86/Makefile NUL`

即：

1. 新增的行数；
2. 一个制表符；
3. 删除的行数；
4. 一个制表符；
5. 一个 `NUL`（仅在重命名/复制时存在）；
6. 镜像（preimage）中的路径；
7. 一个 `NUL`（仅在重命名/复制时存在）；
8. 后镜像（postimage）中的路径（仅在重命名/复制时存在）；
9. 一个 `NUL`。

在重命名情况下，镜像路径前的额外 `NUL` 是为了让读取输出的脚本无需提前读取即可判断当前读取的记录是单路径记录还是重命名/复制记录。在读取新增和删除的行后，读取到 `NUL` 即可获得路径，但如果它是 `NUL`，则该记录将显示两个路径。

## 示例

### 检查工作树的各种方法

`$ git diff` `(1)`  
`$ git diff --cached` `(2)`  
`$ git diff HEAD` `(3)`

**1.** 工作区中尚未暂存到下次提交的更改。

**2.** 索引与上次提交之间的更改；如果你运行 `git commit` 且不带 `-a` 选项，你将提交这些更改。

**3.** 自上次提交以来工作区中的更改；如果你运行 `git commit -a`，你将提交这些更改。

### 与任意提交比较

`$ git diff test` `(1)`  
`$ git diff HEAD -- ./test` `(2)`  
`$ git diff HEAD^ HEAD` `(3)`

**1.** 不使用当前分支的顶，而是与 `test` 分支的顶比较。

**2.** 不与 `test` 分支的顶比较，而是与当前分支的顶比较，但将比较限制在 `test` 文件。

**3.** 比较上一次提交和最后一次提交的版本。

### 比较分支

`$ git diff topic master` `(1)`  
`$ git diff topic..master` `(2)`  
`$ git diff topic...master` `(3)`

**1.** `topic` 分支和 `master` 分支顶之间的更改。

**2.** 同上。

**3.** 自 `topic` 分支从 `master` 分出以来，`master` 分支上发生的更改。

### 限制 diff 输出

`$ git diff --diff-filter=MRC` `(1)`  
`$ git diff --name-status` `(2)`  
`$ git diff arch/i386 include/asm-i386` `(3)`

**1.** 只显示修改、重命名和复制，不显示添加或删除。

**2.** 只显示名称和更改性质，而不显示实际 diff 输出。

**3.** 将 diff 输出限制在指定的子树中。

### 处理 diff 输出

`$ git diff --find-copies-harder -B -C` `(1)`  
`$ git diff -R` `(2)`

**1.** 花额外的周期来寻找重命名、复制和完全重写（非常昂贵）。

**2.** 反向输出 diff。

## 参见

(1), (1), (1), (7), (1), (1)

***

# GIT-DIFFTOOL

## 名称

`git-difftool` - 使用常用的 diff 工具显示更改

## 概要

`git difftool` `[<options>] [<commit> [<commit>]] [--] [<path>...]`

## 描述

`git difftool` 是一个 Git 命令，允许你使用常用的 diff 工具比较和编辑版本之间的文件。`git difftool` 是 `git diff` 的前端，接受相同的选项和参数。见 (1)。

### 选项

`-d, --dir-diff`

将修改后的文件复制到临时位置并对其执行目录 diff。此模式在启动 diff 工具之前永远不会提示。

`-y, --no-prompt`

在启动 diff 工具之前不提示。

`--prompt`

在每次调用 diff 工具之前提示。这是默认行为；提供该选项是为了覆盖任何配置设置。

`-t <tool>, --tool=<tool>`

使用由 `<tool>` 指定 diff 工具。有效值包括 `emerge`、`kompare`、`meld` 和 `vimdiff`。运行 `git difftool --tool-help` 获取有效 `<tool>` 设置列表。

如果未指定 diff 工具，`git difftool` 将使用配置变量 `diff.tool`。如果未设置配置变量 `diff.tool`，`git difftool` 将选择一个默认值。

你可以通过设置配置变量 `difftool.<tool>.path` 来显式提供工具的完整路径。例如，可以通过设置 `difftool.kdiff3.path` 配置 `kdiff3` 的绝对路径。否则，`git difftool` 假设工具在 `PATH` 中可用。

与其运行已知 diff 工具之一，`git difftool` 可以通过在配置变量 `difftool.<tool>.cmd` 中指定命令行来运行替代程序。

当使用此工具调用 `git difftool` 时（通过 `-t` 或 `--tool` 选项或 `diff.tool` 配置变量），将调用配置的命令行并提供以下变量：`$LOCAL` 设置为包含 diff 镜像内容的临时文件名，`$REMOTE` 设置为包含 diff 后镜像内容的临时文件名。`$MERGED` 是正在比较的文件名。`$BASE` 用于兼容自定义合并工具命令，其值与 `$BASE` 相同。

`--tool-help`

打印可与 `--tool` 配合使用的 diff 工具列表。

`--[no-]symlinks`

`git difftool` 的默认是创建符号链接。指定 `--no-symlinks` 指令 `git difftool` 创建副本。

`-x <command>, --extcmd=<command>`

指定用于查看 diff 的自定义命令。`git difftool` 继承文件的右侧。

`-g, --gui`

当使用 `-g` 或 `--gui` 调用 `git difftool` 时，默认工具将从 `diff.guitool` 而不是 `diff.tool`。

`--[no-]trust-exit-code`

如果调用的工具返回非零状态则退出。使用 `--trust-exit-code` 让 `git difftool` 在工具退出时退出。

支持选项的完整列表请见 (1)。

## 配置变量

当未定义等效变量时，`git difftool` 回退到 `mergetool` 配置变量。

`diff.tool`

默认使用的 diff 工具。

`diff.guitool`

指定 `--gui` 时使用的默认 diff 工具。

`difftool.<tool>.path`

覆盖给定工具的路径。

`difftool.<tool>.cmd`

指定调用指定工具的命令行。

`difftool.prompt`

在每次调用 diff 工具之前提示。

`difftool.trustExitCode`

如果调用的工具返回非零状态则退出。

## 参见

(1)

显示提交之间、提交与工作树之间的更改等。

(1)

运行合并工具以解决冲突。

# GIT-FAST-EXPORT

## 名称

`git-fast-export` - Git 数据导出

## 概要

`git fast-export [options]` `|` `git fast-import`

## 描述

此程序以适用于管道 `git fast-import` 的格式导出给版本。

你可以将其人类可读的 bundle 替代方案（见 (1)），或作为交互式的 `git filter-branch`。

### 选项

`--progress=<n>`

每 `<n>` 个对象插入进度语句，由 `git fast-import` 在导入期间显示。

`--signed-tags=(verbatim|warn|warn-strip|strip|abort)`

指定如何处理签名标签。由于导出后的任何转换可能会更改标签名称（在排除版本时也可能发生），签名将无法匹配。

当请求 `abort`（默认值）时，此程序在遇到签名标签时将终止。使用 `strip` 时，标签将静默变为无签名；使用 `warn-strip` 时，将变为无签名但会显示警告；使用 `verbatim` 时，将静默导出；使用 `warn` 时，将导出但你会看到警告。

### `--tag-of-filtered-object=(abort|drop|rewrite)`

指定如何处理标记对象被过滤掉的标签。由于修订和导出的文件受路径限制，标记的对象可能会被完全过滤掉。

当请求 `abort`（默认值）时，程序遇到此类标签时将退出。使用 `drop` 时，它将从输出中忽略此类标签。使用 `rewrite` 时，如果被标记的对象是一个提交，它将重写该标签以指向一个祖先提交（通过父提交重写；见 (1)）。

### `-M`, `-C`

执行移动和/或复制检测，如 (1) 手册页所述，并使用其在输出转储中生成重命名和复制命令。

请注意，该命令的早期版本在提供这些选项时不会报错但会产生错误的结果。

### `--export-marks=<file>`

完成后将内部标记表转储到 `<file>`。标记每行写入一个，格式为 `:markid SHA-1\.`。仅导出修订的标记；忽略二进制对象（blob）标记。后端可以使用此文件在导入完成后验证导入，或者在多次增量运行之间保存标记表。由于 `<file>` 仅在完成时打开并截断，也可以安全地将其传递给 `--import-marks`。如果没有新对象被标记/导出，则不会写入文件。

### `--import-marks=<file>`

在处理任何输入之前，加载 `<file>` 中指定的标记。输入文件必须存在、可读，且格式与 `--export-marks` 生成的相同。

已标记的提交将不再再次导出。如果后端使用类似的 `--import-marks` 文件，则通过保持跨运行的标记相同，允许仓库的增量双向导出。

### `--fake-missing-tagger`

某些旧仓库拥有没有标记者的标签。fast-import 协议对此非常严格，不允许这种情况。因此，伪造一个标记者以便能够进行 fast-import 输出内容。

### `--use-done-feature`

以 `feature done` 段落启动流，并用 `done` 命令终止。

### `--no-data`

跳过 blob 对象的输出，而是通过它们的原始 SHA-1 哈希值引用 blob。这在重写仓库的目录结构或历史而不接触单个文件内容时非常有用。请注意，生成的流只能由已经包含必要对象的仓库使用。

### `--full-tree`

此选项会导致 fast-export 为每个提交发布一个 `deleteall` 指令，随后列出提交中所有文件的完整列表（而不是仅列出与提交的第一个父提交不同的文件）。

### `--anonymize`

匿名化仓库内容，同时保留历史形状和存储树的结构。参见下文的 ANONYMIZING（匿名化）章节。

### `--refspec`

对每个导出的引用应用指定的 refspec。可以指定多个。

### `[<git-rev-list-args>...]`

一组 `git rev-parse` 和 `git rev-list` 可接受的参数列表，用于指定要导出的特定对象和引用。例如 `master~10..master` 会导出当前的 `master` 引用以及自其第 10 个祖先提交以来添加的所有对象。

## 示例

```bash
$ git fast-export --all | (cd /empty/repository && git fast-import)
```

这将导出整个仓库并将其导入现有的空仓库中。除了对非 UTF-8 的提交进行重新编码外，它将是一一对应的镜像。

```bash
$ git fast-export master~5..master | sed "s/refs/heads/master|refs/heads/other|" | git fast-import
```

这将从 `master~5..master` 创建名为 `other` 的新分支（即如果 `master` 是线性历史，它将获取最后 5 个提交）。

注意，这假设该修订范围引用的任何 blob 和提交消息都不包含 `refs/heads/master` 字符串。

## 匿名化

如果给出 `--anonymize` 选项，git 将尝试移除仓库中的所有标识信息，同时保留足够的原始树和历史模式以重现某些 bug。目标是让私有仓库中发现的 git bug 在匿名化仓库中仍然存在，后者可以与 Git 开发人员共享以帮助解决问题。

使用此选项，git 将把输出中的所有引用名、路径、blob 内容、提交和标签消息、名称和电子邮件地址替换为匿名数据。相同字符串的两个实例将被等替换（例如，两个具有相同作者的提交在输出中将具有相同的匿名作者，但与原始作者字符串毫无相似）。提交、分支和标签之间的关系被保留，提交时间戳也被保留（但提交消息和引用名与原始版本并不相似）。树的相对组成被保留（例如，如果你有一个包含 10 个文件和 3 个树的根树，输出也是如此），但它们的名称和文件内容将被替换。

如果你认为发现了一个 git bug，可以从导出整个仓库的匿名化流开始：

```bash
$ git fast-export --anonymize --all > anon-stream
```

然后确认该 bug 是否存在于从该流创建的仓库中（许多 bug 将不存在，因为它们确实取决于具体的仓库内容）：

```bash
$ git init anon-repo
$ cd anon-repo
$ git fast-import <../anon-stream
$ ... 测试你的 bug ...
```

如果匿名化仓库显示了该 bug，那么与其配合错误报告一起共享 `anon-stream`。注意匿名化流压缩率很高，建议对其进行 gzip。如果你想检查流以确保它不包含任何隐私数据，可以在发送之前直接查看。你还可能尝试：

```bash
$ perl -pe 's/\d+/X/g' <anon-stream | sort -u | less
```

这显示所有唯一的行（将数字转换为 `"X"`，将 `"User 0"`、`"User 1"` 等合并为 `"User X"`）。这将产生一个小得多的输出，通常很容易快速确认流中没有隐私数据。

## 局限性

由于 `git fast-import` 无法标记树，你无法完全导出 `linux.git` 仓库，因为它包含指向树而非提交的标签。

## 另请参见

(1)

* *

# GIT-FAST-IMPORT

## 名称

`git-fast-import` - 快速 Git 数据导入器的后端

## 语法

```bash
frontend | git fast-import [options]
```

## 描述

此程序通常不是终端用户想要直接运行的。大多数用户希望使用现有的前端程序，这些程序解析特定类型的外部源并将存储在那里的内容给 fast-import。

fast-import 从标准输入读取混合命令/数据流，并直接向当前仓库写入一个或多个包文件。当在标准输入接收到 EOF 时，fast-import 写入更新后的分支和标签引用，用新导入的数据完全更新当前仓库。

fast-import 后端本身可以导入到空仓库（已通过 `git init` 初始化的仓库）或增量更新现有的填充仓库。是否支持从特定的外部源进行增量导入取决于所使用的前端程序。

### 选项

`--force`

强制更新已修改的现有分支，即使这样做会导致提交丢失（因为新提交包含旧提交）。

`--quiet`

禁用所有非致命输出，使 fast-import 在成功时保持静默。此选项禁用了由 `--stats` 显示的输出。

`--stats`

显示关于 fast-import 创建的对象、存储这些对象的包文件以及 fast-import 在本次运行期间使用的内存的某些基本统计信息。显示此输出目前是默认的，但可以通过 `--quiet` 禁用。

### 前端程序的选项

`--cat-blob-fd=<fd>`

将对 `cat-blob` 和 `ls` 查询的响应写入文件描述符 `<fd>` 而不是标准输出。允许将面向终端用户的进度输出与其他输出分离。

### `--date-format=<fmt>`

指定前端在 `author`、`committer` 和 `tagger` 命令中提供给 fast-import 的日期类型。请参考下文“日期格式”部分关于支持的格式及其语法的细节。

### `--done`

如果流的末尾没有 `done` 命令，则带错误退出。此选项可能用于检测导致前端在开始写入流之前就终止的错误。

### 标记文件的位置

#### `--export-marks=<file>`

在完成后，将内部标记表（marks table）转储到 `<file>`。标记以每行一个的形式写入，格式为 `:markid SHA-1\.`。前端可以使用此文件在导入完成后验证导入情况，或者在多次增量运行之间保存标记表。由于 `<file>` 仅在检查点（或完成时）被打开并截断，因此也可以将相同的路径安全地传递给 `--import-marks`。

#### `--import-marks=<file>`

在处理任何输入之前，加载 `<file>` 中指定的标记。输入文件必须存在、可读，且使用的格式与 `--export-marks` 生成的格式相同。可以提供多个选项来导入多组标记。如果标记被定义为不同的值，则最后一个文件胜出。

#### `--import-marks-if-exists=<file>`

类似于 `--import-marks`，但如果文件不存在，则静默跳过该文件而不是报错。

#### `--[no-]relative-marks`



指定 `--relative-marks` 后，通过 `--import-marks=` 和 `--export-marks=` 指定的路径将相对于当前仓库中的内部目录。在 `git-fast-import` 中，这意味着路径相对于 `.git/info/fast-import` 目录的。然而，其他的导入器可能会使用不同的位置。

可以通过交替使用 `--(no-)-relative-marks` 与 `--(import|export)-marks=` 选项将相对和非相对标记相结合。

## 性能与压缩调整

### `--active-branches=<n>`

同时保持活跃的最大分支数量。详情请见下文“内存利用”部分。默认值为 5。

### `--big-file-threshold=<n>`

`fast-import` 尝试为 blob 创建增量（delta）的最大大小，以字节为单位。默认值为 `512m`（512 MiB）。在内存受限的系统中，某些导入器可能希望降低此值。

### `--depth=<n>`

blob 和 tree 增量计算的最大深度。默认值为 10。

### `--export-pack-edges=<file>`

在创建 packfile 后，向 `<file>` 打印一行数据，列出 packfile 的文件名以及写入该 packfile 的每个分支最后的提交。对于总对象集超过 4 GiB packfile 限制的项目，这些信息可能有用，因为在调用 `git pack-objects` 时，这些提交可以作为边缘点。

### `--max-pack-size=<n>`

每个输出 packfile 的最大大小。默认无限制。

## 性能

`fast-import` 的设计允许以最小的内存占用和处理时间导入大型项目。假设前端能够跟上 `fast-import` 的速度并为其提供持续的数据流，对于拥有 10 年以上历史并包含 100,000 多个独立提交的项目，导入时间通常在相当廉的（约 2,000 美元）硬件上仅需 1-2 小时即可完成。

大多数瓶颈出现在对外部源数据的访问上（源数据提取修订的速度不够快）或磁盘 IO（`fast-import` 的写入速度取决于磁盘接收数据的速度）。如果源数据存储在与目标 Git 仓库不同的驱动器上（由于 IO 竞争较少），导入将运行得更快。

## 开发成本

一个典型的 `fast-import` 前端大约只需要 200 行 Perl/Python/Ruby 代码。尽管开发者是第一次接触 `fast-import`，有时甚至是第一次接触 Git，但大多数开发者也能在几小时内创建出可工作的导入器。这是一个理想的情况，因为大多数转换工具都是一次性的（使用一次后就永不再复用）。

## 并行操作

与 `git push` 或 `git fetch` 一样，由 `fast-import` 处理的导入可以与并行的 `git repack -a -d` 或 `git gc` 调用或其他任何 Git 操作安全运行（包括 `git prune`，因为 `fast-import` 永远不会使用松散对象）。

`fast-import` 不锁定其正在导入的分支或标签引用（refs）。在导入后的引用更新阶段，`fast-import` 会测试每个现有的分支引用以验证更新将是快进式更新（fast-forward，即引用中存储的提交包含要写入的提交的新历史中）。如果更新不是快进式的，`fast-import` 将跳过更新该引用并打印警告信息。`fast-import` 将始终尝试更新所有分支引用，不会在首次失败时停止。

可以使用 `--force` 强制更新分支，但建议仅在原本空闲的仓库中使用。在向空仓库进行初始导入时，不需要使用 `--force`。

## 技术讨论

`fast-import` 在内存中跟踪一组分支。在导入过程的任何点，都可以通过在输入流上发送 `commit` 命令来创建或修改分支。这种设计允许前端程序同时处理无限数量的分支，并按照它们在源数据中的顺序生成提交。它还极地简化了前端程序。

`fast-import` 不使用或修改当前工作目录或其中的任何文件。（但它会更新由 `GIT_DIR` 引用的当前 Git 仓库。）因此，导入前端可以使用工作目录用于用途，例如从外部源提取修订。对工作目录的忽略使得 `fast-import` 运行非常快，因为它在切换分支时不需要执行任何昂贵的文件操作。

## 输入格式

除了原始文件数据（Git 不解释）外，`fast-import` 输入格式是基于文本（ASCII）的。这种文本格式简化了前端程序的开发和调试，特别是使用 Perl 等高级语言时。

`fast-import` 对输入非常严格。我们在下文中说的 SP 指的是一个空格。同样，LF 意味着一个（且仅一个）换行符，HT 意味着一个（且仅一个）制表符。提供空白字符会导致意外结果，例如带有前后空格的分支名称或文件名，或者在遇到意外输入时提前终止 `fast-import`。

### 流注释

为了帮助调试前端，`fast-import` 会忽略任何以 `#`（ASCII 井）开头的行，直到遇到 LF。注释行可以包含任何不包含 LF 的字节序列，因此可以包含特定于前端的调试信息，用于检查 `fast-import` 数据流。

### 日期格式

支持以下日期格式。前端应通过 `--date-format=<fmt>` 命令行选项传递格式名称来选择其导入使用的格式。

#### `raw`

这是 Git 的原生格式，格式为 `<time> SP <offutc>`。如果未指定 `--date-format`，它也是 `fast-import` 的默认格式。

事件时间由 `<time>` 指定，为自 Unix 纪（UTC 1 月 1 日午夜）以来的秒数，并被写为 ASCII 十进制整数。

本地偏移由 `<offutc>` 指定，为相对于 UTC 的正或负偏移。例如，EST（比 UTC 晚 5 小时）在 `<tz>` 中表示为 `"-0500"`，而 UTC 为 `"+0000"`。本地偏移不影响 `<time>`；它仅作为帮助格式化程序显示时间戳的建议。

如果源材料中无法用本地偏移量，请使用 `"+0000"` 或最常见的本地偏移量。例如，许多组织拥有 CVS 仓库，该仓库仅由位于同一位置和时区的用户访问。在这种情况下，可以假设一个相对于 UTC 的合理偏移量。

与 `rfc2822` 格式不同，这种格式非常严格。任何格式上的变体都会导致 `fast-import` 拒绝该值。

#### `rfc2822`

这是 RFC 2822 描述的标准邮件格式。

一个示例值为 `"Tue Feb 6 11:22:18 2007 -0500"`。Git 解析器是准确的，但稍微有些宽松。它与 `git am` 在应用从邮件接收的补丁时使用的解析器是同一个。

某些格式错误的字符串可能会被接受为有效日期。在某些情况下，Git 仍然能够从格式错误的字符串中获取正确的日期。此外，某些类型的格式错误字符串会被 Git 解析错误，但仍认为其有效。严重格式错误的字符串将被拒绝。

与上述原始格式不同，RFC 2822 日期字符串中包含的时区/UTC 偏移量信息将在存储之前用于将日期值调整为 UTC。因此，这些信息尽可能准确非常重要。

如果源材料使用 RFC 2822 风格的日期，前端应该让 `fast-import` 处理解析和转换（而不是尝试自己处理），因为 Git 解析器已经在环境中经过了良好的测试。

如果源材料已经使用 UNIX-epoch 格式、可以诱导提供该格式的日期或其格式很容易转换为该格式，则前端应优先使用原始格式，因为解析时没有歧义。

#### `now`

始终使用当前时间和时区。`<when>` 必须始终提供字面量 `now`。

这是一个演示格式。该系统的当前时间和时区会在 `fast-import` 创建标识字符串时始终复制到该字符串中。没有办法指定不同的时间或时区。

提供这种特殊格式是因为它实现简单，并且对于想要现在创建新提交的进程可能有用，而无需使用工作目录或 `git update-index`。

## Commands

`fast-import` 接受多个命令来更新当前仓库并控制当前的导入过程。后文将对每个命令进行更详细的讨论（带有示例）。

### `commit`

通过创建一个新提交并更新分支指向新创建的提交，来创建一个新分支或更新现有分支。

### `tag`

从现有提交或分支创建一个注释标签对象。此命令不支持轻量级标签，因为不推荐用它们记录有意义的时间点。

### `reset`

将现有分支（或新分支）重置到特定的修订。此命令必须用于在不进行提交的情况下，将分支更改到特定修订。

### `blob`

将原始文件数据转换为 blob，供未来在 `commit` 命令中使用。此命令是可选的，执行导入不需要它。

### `checkpoint`

强制 `fast-import` 关闭当前的 packfile，生成其唯一的 SHA-1 校验和和索引，并启动一个新的 packfile。此命令是可选的，执行导入不需要它。

### `progress`

导致 `fast-import` 将整行回显到其自己的标准输出。此命令是可选的，执行导入不需要它。

### `done`

标记流的结束。除非使用 `--done` 命令行选项或 `done` 命令请求了 done 功能，否则此命令是可选的。

### `cat-blob`

导致 `fast-import` 以 `cat-file --batch` 格式将 blob 打印到通过 `--cat-blob-fd` 设置的文件描述符或标准输出（如果未指定）。

### `ls`

导致 `fast-import` 以 `ls-tree` 格式将描述目录条目的行打印到通过 `--cat-blob-fd` 设置的文件描述符或标准输出（如果未指定）。

### `feature`

启用指定的特定功能。这要求 `fast-import` 支持指定的功能，如果不支持则中止。

### `option`

指定 OPTIONS 下列出的任何选项，且在不改变流语义的前提下以适应前端需求。此命令是可选的，执行导入不需要它。

## `commit`

使用新提交创建或更新分支，记录项目中的一个逻辑更改。

```text
'commit' SP <ref> LF mark? ('author' (SP <name>)? SP LT <email> GT SP <when> LF)? 'committer' (SP <name>)? SP LT <email> GT SP <when> LF data ('from' SP <commit-ish> LF)? ('merge' SP <commit-ish> LF)? (filemodify | filedelete | filecopy | filerename | filedeleteall | notemodify)* LF?
```

其中 `<ref>` 是要提交的分支名称。在 Git 中，分支名称通常带有 `refs/heads/` 前缀，因此导入 CVS 分支符号 `RELENG-1_0` 将使用 `refs/heads/RELENG-1_0` 作为 `<ref>` 的值。`<ref>` 的值必须是 Git 中有效的 refname。由于 LF 在 Git refname 中无效，因此此处不支持引号或转义语法。

`mark` 命令可能会可选地出现，请求 `fast-import` 保存新创建提交的引用，供前端将来使用（格式见下文）。前端标记每个提交是非常常见的，允许从任何导入的提交创建分支。

`committer` 之后的 `data` 命令必须提供提交消息（语法见下文）。导入空提交消息请使用长度为 0 的。提交消息是自由格式的，Git 不对其进行解释。目前它们必须以 UTF-8 编码，因为 `fast-import` 不允许指定编码。

可以包含零或多个 `filemodify`、`filedelete`、`filecopy`、`filename`、`filedeleteall` 和 `notemodify` 命令，在创建提交之前更新分支的内容。这些命令可以以任何顺序提供。然而，建议在同一提交中 `filedeleteall` 命令在所有 `filemodify`、`filecopy`、`filename` 和 `notemodify` 命令之前，因为 `filedeleteall` 会清空分支（见下文）。

命令后的 LF 是可选的（以前是强制要求的）。

### `author`

如果作者信息可能与提交者信息不同，可能会可选出现 `author` 命令。如果省略 `author`，`fast-import` 将自动使用提交者的信息作为提交的作者部分。关于作者字段的描述见下文，它们与提交者字段相同。

### `committer`

`committer` 命令指示谁提交了此提交以及他们何时提交的。

此处 `<name>` 是人的显示名称（例如 `"Com M Itter"`），`<email>` 是人的电子邮件地址（`""`）。`LT` 和 `GT` 是字面的小于号（`\x3c`）和大于号（`\x3e`）符号。这些符号用于将电子邮件地址与行中的其他字段隔开。注意 `<name>` 和 `<email>` 是自由格式的，可以包含任何字节序列，但 LT、GT 和 LF 除外。`<name>` 通常是 UTF-8 编码。

更改的时间通过 `<when>` 指定，使用 `--date-format=<fmt>` 命令行选项选择的日期格式。请参上文“日期格式”以获取支持的格式集及其语法。

### `from`

`from` 命令用于指定初始化此分支的提交。该修订版本将是新提交的第一个祖先。在此提交处构建的树的状态将从 `from` 提交的状态开始，并被此提交中的内容修改所更改。

在新分支的首次提交中省略 `from` 命令将导致 `fast-import` 创建一个没有先祖的提交。这通常只适用于项目的初始提交。如果前端在创建新分支时从头创建所有文件，则可以使用 `merge` 命令代替 `from` 命令，以从空树开始提交。在现有分支上，省略 `from` 命令通常是符合预期的，因为该分支上的当前提交会被自动认为是新提交的第一个先祖。

由于 LF 不在 Git 引用全名（refname）或 `SHA-1` 表达式中有效，因此 `<commit-ish>` 内部不支持任何引号或转义语法。

这里的 `<commit-ish>` 是以下任意内容：

- 存在于 `fast-import` 内部分支表中的现有分支名称。如果 `fast-import` 不认识该名称，则将其处理为 `SHA-1` 表达式。
- 标记引用，`:<idnum>`，其中 `<idnum>` 是标记数字。`fast-import` 使用 `:` 来表示标记引用的原因是该字符在 Git 分支名中是不合法的。开头的 `:` 可以轻松地区分标记 `42`（`:42`）与分支 `42`（`42` 或 `refs/heads/42`），或恰好由十进制数字组成的缩写 `SHA-1`。
- 标记在使用之前必须先声明（通过 `mark`）。
- 完整的 40 字节或十六写的提交 `SHA-1`。
- 任何可以解析为提交的有效 Git `SHA-1` 表达式。详情见（7）中的“SPECIFYING REVISIONS”。
- 特殊的空 `SHA-1`（40 个零）表示要删除该分支。

从当前分支值重启增量导入的特殊情况应写为：

```text
from refs/heads/branch⁰
```

`⁰` 后缀是必要的，因为 `fast-import` 不允许分支从自身开始，而且在从输入中读取 `from` 命令之前，分支就已经在内存中创建。添加 `⁰` 将强制 `fast-import` 通过 Git 的修订解析库解析提交，而不是通过其内部分支表，从而加载分支的现有值。

### `merge`

包含一个额外的先祖提交。此额外的祖先链接不会改变在该提交处构建树状态的方式。如果在创建新分支时省略了 `from` 命令，则第一个合并提交将是当前提交的第一个先祖，且分支将从没有任何文件开始。`fast-import` 允许每个提交包含无限数量的 `merge` 命令，从而建立 n 路合并。

这里的 `<commit-ish>` 是 `from` 命令同样接受的任何提交规格说明表达式（见上文）。

### `filemodify`

包含在 `commit` 命令中，用于添加新文件或更改现有文件的内容。该命令通过两种不同的方法来指定文件的内容。

#### 外部数据格式

文件的数据内容已由之前的 `blob` 命令提供。前端只需要将其连接起来。

```text
'M' SP <mode> SP <dataref> SP <path> LF
```

这里，`<dataref>` 通常必须是由之前的 `blob` 命令设置的标记引用（`:<idnum>`），或现有 Git `blob` 对象的完整 40 字节 `SHA-1`。如果 `<mode>` 为 `040000`，则 `<dataref>` 必须是现有 Git `tree` 对象的完整 40 字节 `SHA-1` 或通过 `--import-marks` 设置的标记引用。

#### 内联数据格式

文件的数据内容尚未提供。前端希望作为此修改命令的一部分提供它。

```text
'M' SP <mode> SP 'inline' SP <path> LF data
```

关于 `data` 命令的详细描述请见下文。

在两种格式中，`<mode>` 都是文件条目的类型，以八进制指定。Git 仅支持以下模式：

- `100644` 或 `644`：普通（不可执行）文件。大多数项目中的大多数文件使用此模式。如果不确定，这通常是你需要的。
- `100755` 或 `755`：普通但可执行的文件。
- `120000`：符号链接（symlink），文件的内容将是链接目标。
- `160000`：git 链接（gitlink），对象的 `SHA-1` 指向另一个仓库中的提交。Git 链接只能通过 `SHA` 或提交标记来指定。
- `040000`：子目录。子目录只能通过 `SHA` 或通过 `--import-marks` 设置的 `tree` 标记来指定。

在两种格式中，`<path>` 是要添加（如果不存在）或修改（如果已存在）文件的完整路径。



`<path>` 字符串必须使用 UNIX 风格的目录分隔符（正斜杠 `/`），可以包含除 `LF` 外的任何字节，且不能以双引号（`"`）开头。

路径可以使用 C 风格字符串引号；这在所有情况下都是接受的，并且文件名以双引号开头或包含 `LF` 则强制要求。在 C 风格引号中，完整名称应用双引号括起来，任何 `LF`、反斜杠或双引号字符必须在它们前面加上反斜杠进行转义（例如 `"path/with\n, \\ and \" in it"`）。

`<path>` 的值必须是规范形式。也就是说它不能：

- 包含空目录组件（例如 `foo//bar` 是无效的）。
- 以目录分隔符结尾（例如 `foo/` 是无效的）。
- 以目录分隔符开头（例如 `/foo` 是无效的）。
- 包含特殊组件 `.` 或 `..`（例如 `foo/./bar` 是无效的）。

### `filedelete`

包含在 `commit` 命令中，用于从分支中删除文件或递归删除整个目录。如果文件或目录的删除导致其父目录为空，则父目录也将被删除。此操作会向上级联，直到到达第一个非空目录。

```text
'D' SP <path> LF
```

这里 `<path>` 是要删除的文件或子目录的完整路径。关于 `path` 的详细描述请见上文 `filemodify`。

### `filecopy`

将现有文件或目录递归复制到分支内的另一个位置。现有文件或目录必须存在。如果目标存在，它将由从源复制的内容完全替换。

```text
'C' SP <path> SP <path> LF
```

这里第一个 `<path>` 是源位置，第二个 `<path>` 是目标位置。关于 `<path>` 可能的样式请见上文 `filemodify`。要使用包含 `SP` 的源路径，则必须对路径加引号。

`filecopy` 命令立即生效。一旦源位置被复制到目标位置，后续应用于源位置的任何命令都将不会影响复制的目标位置。

### `rename`

将现有文件或目录重命名为分支内的另一个位置。现有文件或目录必须存在。如果目标存在，它将被源目录替换。

```text
'R' SP <path> SP <path> LF
```

这里第一个 `<path>` 是源位置，第二个 `<path>` 是目标位置。关于 `<path>` 可能的样式请见上文 `filemodify`。要使用包含 `SP` 的源路径，则必须对路径加引号。

`rename` 命令立即生效。一旦源位置被重命名为目标位置，后续应用于源位置的任何命令将在那里创建新文件，而不会影响重命名的目标。

注意 `rename` 等于 `filecopy` 后对源位置执行 `filedelete`。使用 `rename` 有微小的性能优势，但这种优势非常细微，完全不值得尝试将源材料中的删除/添加对转换为 `rename`。

### `filedeleteall`

包含在 `commit` 命令中，用于从分支中删除所有文件（以及所有目录）。该命令将内部分支结构重置为空，允许前端随后从头添加所有感兴趣的文件。

```text
'deleteall' LF
```

如果前端不知道（或不在乎）当前分支上有哪些文件，因此无法生成正确的 `filedelete` 命令来更新内容，那么此命令将非常有用。

执行 `filedeleteall` 紧接着执行所需的 `filemodify` 命令以设置正确的内容，其结果与仅发送所需的 `filemodify` 和 `filedelete` 命令相同。然而，`filedeleteall` 方法可能需要 `fast-import` 为每个活动分支使用略多的内存（即使对于大多数大型项目，内存量也小于 1 MiB）；因此，建议能够轻松获取 commit 中受影响路径的前端这样做。

### `notemodify`

包含在 `commit <notes_ref>` 命令中，用于为 `<commit-ish>` 添加新的注释（annotating note）或修改此注释内容。在内部，它类似于在 `<commit-ish>` 路径上执行 `filemodify 100644`（可能被拆分为子目录）。除了使用 `filedeleteall` 删除此树中的所有现有注释外，不建议使用任何其他命令写入 `<notes_ref>` 树。该命令有两种不同的方式来指定注释的内容。

#### 外部数据格式

用于注释的数据内容已由之前的 `blob` 命令提供。前端只需要将其连接到要注释的 commit 上。

```text
'N' SP <dataref> SP <commit-ish> LF
```

在这里，`<dataref>` 可以是之前的 `blob` 命令设置的标记引用（`:<idnum>`），也可以是现有 Git blob 对象的完整 40 字节 SHA-1。

#### 内联数据格式

注释的数据内容尚未提供。前端希望作为此修改命令的一部分提供它。

```text
'N' SP 'inline' SP <commit-ish> LF data
```

详见下文对数据命令的详细描述。

在两种格式中，`<commit-ish>` 都是 `from` 命令同样接受的 commit 指定表达式之一（见上文）。

### `mark`

安排 `fast-import` 保存对当前对象的引用，允许前端在未来无需知道 SHA-1 的情况下回溯该对象。这里的当前对象是 `mark` 命令所在的对象创建命令。它可以是 `commit`、`tag` 和 `blob`，但 `commit` 是最常用的用法。

```text
'mark' SP ':' <idnum> LF
```

其中 `<idnum>` 是前端分配给此标记的数字。`<idnum>` 的值用 ASCII 十进制整数表示。值 0 被保留，不能作为标记。只有大于或等于 1 的值可以作为标记。

新标记会自动创建。只需通过在另一个 `mark` 命令中重用相同的 `<idnum>`，即可现有标记移动到另一个对象。

### `tag`

创建一个指向特定 commit 的注释标签。要创建轻量级（非注释）标签，请参阅下方的 `reset` 命令。

```text
'tag' SP <name> LF 'from' SP <commit-ish> LF 'tagger' (SP <name>)? SP LT <email> GT SP <when> LF data
```

其中 `<name>` 是要创建的标签名称。

标签名在存储到 Git 时会自动带有 `refs/tags/` 前缀，因此导入 CVS 分支符号 `RELENG-1_0-FINAL` 时，`<name>` 仅使用 `RELENG-1_0-FINAL`，`fast-import` 将将对应的引用写入 `refs/tags/RELENG-1_0-FINAL`。

`<name>` 的值必须是 Git 中有效的引用名，因此可以包含正斜杠。由于 `LF` 在 Git 引用名中无效，此处不支持任何引号或转义语法。

`from` 命令与 `commit` 命令中的相同；详情请见上文。

`tagger` 命令使用的格式与 `commit` 内部的 `committer` 相同；详情请见上文。

跟随 `tagger` 之后的 `data` 命令必须提供注释标签消息（详见下文数据命令语法）。要导入空标签消息，请使用长度为 0 的 `data`。标签消息是自由格式的，不会被 Git 解释。目前它们必须编码为 UTF-8，因为 `fast-import` 不允许指定其他编码。

不支持在 `fast-import` 内部从导入时对注释标签进行签名。不建议尝试包含您自己的 PGP/GPG 签名，因为前端无法（轻松）访问通常进入此类签名的完整字节集。如果需要签名，请在 `fast-import` 内部通过 `reset` 创建轻量级标签，然后使用标准的 `git tag` 离线创建这些标签的注释版本。

### `reset`

创建（或重新创建）命名的分支，可选地从特定版本开始。`reset` 命令允许前端对现有分支发布新的 `from` 命令，或者从现有 commit 创建新分支而不创建新 commit。

```text
'reset' SP <ref> LF ('from' SP <commit-ish> LF)? LF?
```

关于 `<ref>` 和 `<commit-ish>` 的详细描述，请参阅上文的 `commit` 和 `from` 部分。

命令后的 `LF` 是可选的（以前是强制的）。

`reset` 命令也可以用于创建轻量级（非注释）标签。例如：

```text
reset refs/tags/938 from :938
```

这将创建一个轻量级标签 `refs/tags/938`，指向标记 `:938` 所引用的任何 commit。

### `blob`

请求向 packfile 写入一个文件版本。该版本未与任何 commit 连接；这种连接必须在后续的 commit 命令中通过分配标记引用 blob 来建立。

```text
'blob' LF mark? data
```

在这里 `mark` 命令是可选的，因为某些前端选择自行生成 blob 的 Git SHA-1 并直接传递给 `commit`。然而，这通常工作不划算，因为标记存储成本低廉且易于使用。

### `data`

向 `fast-import` 提供原始数据（用于 blob/文件内容、commit 消息或注释标签消息）。数据可以使用精确字节数提供或使用终止行分隔符提供。旨在用于生产级转换的真实前端应始终使用精确字节数格式，因为它更健壮且性能更好。分隔符格式主要用于测试 `fast-import`。

出现在数据命令 `<raw>` 部分的注释行始终被视为数据正体的一部分，因此 `fast-import` 永远不会忽略。这使得导入任何行可能以 `#` 开头的文件/消息内容时都是安全的。

#### 精确字节数格式

前端必须指定数据的字节数。

```text
'data' SP <count> LF <raw> LF?
```

其中 `<count>` 是出现在 `<raw>` 内的精确字节数。`<count>` 的值用 ASCII 十进制整数表示。`<raw>` 两侧的 `LF` 不包含在 `<count>` 中，也不会包含在导入的数据中。

`<raw>` 后的 `LF` 是可选的（以前是强制的），但建议包含。始终包含它会让调试 `fast-import` 流变得更容易，因为下一个命令始终从下一行的第 0 列开始，即使 `<raw>` 没有以 `LF` 结尾。

#### 分隔符格式

使用分隔符字符串标记数据的结束。`fast-import` 将通过搜索分隔符来计算长度。这种格式主要用于测试，建议用于真实数据。

```text
'data' SP '<<' <delim> LF <raw> LF <delim> LF LF?
```

其中 `<delim>` 是所选的分隔符。字符串 `<delim>` 不得在 `<raw>` 中单独占据一行，否则 `fast-import` 会认为数据比实际结束得早。紧随 `<raw>` 之后的 `LF` 是 `<raw>` 的一部分。这是分隔符格式的限制之一，无法提供一个不以 `LF` 作为最后一个字节的数据块。

`<delim> LF` 之后的 `LF` 是可选的（以前是强制的）。

### `checkpoint`

强制 `fast-import` 关闭当前 packfile，启动一个新的，并保存所有当前的分支引用、标签和标记。

```text
'checkpoint' LF LF?
```

注意，当当前 packfile 达到 `--max-pack-size` 或 4 GiB（以较小者准）时，`fast-import` 会自动切换 packfile。在自动切换 packfile 期间，`fast-import` 不更新分支引用、标签或标记。

由于检查点（checkpoint）需要大量的 CPU 时间和磁盘 I/O（用于计算整个包的 SHA-1 校验和、生成相应的索引文件以及更新 refs），单个检查点命令可能需要几分钟才能完成。

前端可能会在极大且长时间运行的导入过程中发布检查点，或者在需要允许另一个 Git 进程访问分支时发布检查点。然而，考虑到一个 30 GiB 的 Subversion 仓库可以通过 `fast-import` 在约 3 小时内加载到 Git 中，显式的检查点可能并非必要的。

命令后的 `LF` 是可选的（以前是强制要求的）。

### `progress`

当从输入流处理该命令时，使 `fast-import` 封封不动地将整行进度信息打印到其标准输出通道（文件描述符 1）。否则，该命令对当前的导入或 `fast-import` 的任何内部状态均无产生影响。

```text
'progress' SP <any> LF LF?
```

命令的 `<any>` 部分可以包含任何不包含 `LF` 的字节序列。命令后的 `LF` 是可选的。调用者可能希望通过 `sed` 等工具处理输出以删除行的开头部分，例如：

```text
frontend | git fast-import | sed 's/^progress //'
```

在检查点之后立即放置进度命令将告知读者检查点何时完成，此时它就可以安全地访问 `fast-import` 更新的 refs。

### `cat-blob`

使 `fast-import` 将 blob 打印到之前通过 `--cat-blob-fd` 参数指定的句描述符中。否则，该命令对当前的导入无任何影响；其主要目的是获取可能在 `fast-import` 内存中但无法从目标仓库访问的 blob。

```text
'cat-blob' SP <dataref> LF
```

`<dataref>` 可以是之前设置的标记引用（`:<idnum>`），也可以是 Git blob 的完整 40 字节 SHA-1（无论它是已存在还是准备好写入）。

输出使用的格式与 `git cat-file --batch` 相同：

```text
<sha1> SP 'blob' SP <size> LF <contents> LF
```

该命令可以用于接受注释的流中的任何位置。特别是 `cat-blob` 命令可以在 commit 的中间使用，但不能在数据命令的中间使用。

见下文“命令的响应”获取有关如何安全读取此输出的详细信息。

### `ls`

将路径处的对象信息打印到之前通过 `--cat-blob-fd` 参数指定的句符中。这允许从活跃 commit 中打印 blob（使用 `cat-blob`），或从之前的 commit 中复制 blob 或 tree 以供当前 commit 使用（使用 `filemodify`）。

`ls` 命令可以用于接受注释的流中的任何位置，包括 commit 的中间。

#### 从活跃 commit 中读取

此形式只能在 commit 的中间使用。路径名指向 `fast-import` 活跃 commit 中的目录项。在这种情况下，路径必须加引号。

```text
'ls' SP <path> LF
```

#### 从命名树读取

`<dataref>` 可以是标记引用（`:<idnum>`），也可以是 Git tag、commit 或 tree 对象的完整 40 字节 SHA-1（无论它是已存在还是等待写入）。路径相对于 `<dataref>` 命名树的顶层。

```text
'ls' SP <dataref> SP <path> LF
```

见上文 `filemodify` 获取关于 `<path>` 的详细描述。

输出使用的格式与 `git ls-tree <tree> -- <path>` 相同：

```text
<mode> SP ('blob' | 'tree' | 'commit') SP <dataref> HT <path> LF
```

`<dataref>` 代表 `<path>` 处的 blob、tree 或 commit 对象，可以在后续的 `cat-blob`、`filemodify` 或 `ls` 命令中使用。

如果该路径没有文件或子树，`git fast-import` 将报告：

```text
missing SP <path> LF
```

见下文“命令的响应”获取有关如何安全读取此输出的详细信息。

### `feature`

要求 `fast-import` 支持指定的特性，不支持则中止。

```text
'feature' SP <feature> ('=' <argument>)? LF
```

命令的 `<feature>` 部分可以是以下任一内容：

- `date-format`、`export-marks`、`relative-marks`、`no-relative-marks`、`force`：表现就像在命令行上传递了带有 `--` 的相应的命令行选项（见上文 OPTIONS）。
- `import-marks`、`import-marks-if-exists`：类似于 `--import-marks`，但有两点不同：第一，每个流只允许一个 `"feature import-marks"` 或 `"feature import-marks-if-exists"` 命令；第二，`--import-marks=` 或 `--import-marks-if-exists` 命令行选项会覆盖流中的任何此类 `"feature"` 命令；第三，`"feature import-marks-if-exists"` 与相应的命令行选项一样静默跳过不存在的文件。
- `cat-blob`、`ls`：要求后端支持 `cat-blob` 或 `ls` 命令。不支持指定命令的 `fast-import` 版本将带有相应的消息退出。这使得导入能够带有清晰的消息尽早报错，而不是在检测到不支持的命令之前在导入的早期浪费时间。
- `notes`：要求后端支持 `commit` 命令的 `notemodify`（`N`）子命令。不支持 notes 的 `fast-import` 版本将带有相应的消息退出。
- `done`：如果流结束时没有 `done` 命令，则报错。如果没有此特性，导致前端意外结束的错误可能无法被检测。

### `option`

处理指定的选项，使 `fast-import` 的行为符合前端的需求。请注意，前端指定的选项会被用户可能为 `git fast-import` 本身指定的任何选项所覆盖。

```text
'option' SP <option> LF
```

命令的 `<option>` 部分可以包含 OPTIONS 节中列出的任何不导入语义的选项，但不带前缀 `--` 并以相同的方式处理。



选项命令必须是输入中的第一个命令（不计算 `feature` 命令），否则在任何非选项命令之后给出选项命令将报错。

以下命令行选项会改变导入语义，因此不能作为选项传递：

- `date-format`
- `import-marks`
- `export-marks`
- `cat-blob-fd`
- `force`

### done

如果没有使用 `done` 特性，则被视为读取了 EOF。这可以用于告诉 `fast-import` 提前结束。

如果使用了 `--done` 命令行选项或 `done` 特性，则 `done` 命令是强制性的，并标记流的结束。

## 命令的响应

`fast-import` 写入的新对象并非立即可用。大多数 `fast-import` 命令在下一个检查点（或完成）之前没有可见效果。前端可以发送命令来填充 `fast-import` 的输入管道，而无需担心它们何时生效，这通过简化调度提升了性能。

然而，对于某些前端来说，能够从正在更新的仓库中读回数据是有用的（例如当源材料描述应用到已导入对象的补丁时）。这可以通过双向管道连接前端和 `fast-import` 实现：

`mkfifo fast-import-output frontend <fast-import-output | git fast-import >fast-import-output`

以此设置的前端可以使用 `progress`、`ls` 和 `cat-blob` 命令从进行中的导入读取信息。

为了避免死锁，此类前端在执行可能阻塞的 `fast-import` 写入之前，必须完全消耗 `progress`、`ls` 和 `cat-blob` 的待处理输出。

## 崩溃报告

如果 `fast-import` 提供无效输入，它将以非零退出状态终止，并在其导入的 Git 仓库顶层创建一个崩溃报告。崩溃报告包含了 `fast-import` 内部状态的快照以及导致崩溃的最近命令。

所有最近的命令（包括流注释、文件更改和进度命令）都显示在崩溃报告的命令历史，但原始文件数据和提交消息会被排除在崩溃报告之外。这种排除节省了报告文件空间，并减少了 `fast-import` 在执行期间必须执行的缓冲量。

写入崩溃报告后，`fast-import` 将关闭当前的 packfile 并导出标记表（marks table）。这允许前端开发者检查仓库状态并从崩溃点继续导入。修改过的分支和标签在崩溃期间不会更新，因为导入并未成功完成。可以在崩溃报告中找到分支和标签信息，如果需要更新，必须手动应用。

一个崩溃示例：

```
$ cat >in <<END_OF_INPUT # my very first test commit commit refs/heads/master committer Shawn O. Pearce <spearce> 19283 -0400 # who is that guy anyway? data <<EOF this is my commit EOF M 644 inline .gitignore data <<EOF .gitignore EOF M 777 inline bob END_OF_INPUT

$ git fast-import <in fatal: Corrupt mode: M 777 inline bob fast-import: dumping crash report to .git/fast_import_crash_8434

$ cat .git/fast_import_crash_8434 fast-import crash report: fast-import process: 8434 parent process : 1391 at Sat Sep 1 00:58:12 2007

fatal: Corrupt mode: M 777 inline bob

Most Recent Commands Before Crash --------------------------------- # my very first test commit commit refs/heads/master committer Shawn O. Pearce <spearce> 19283 -0400 # who is that guy anyway? data <<EOF M 644 inline .gitignore data <<EOF * M 777 inline bob

Active Branch LRU ----------------- active_branches = 1 cur, 5 max

pos clock name ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ 1) 0 refs/heads/master

Inactive Branches ----------------- refs/heads/master: status : active loaded dirty tip commit : 00000000000000000000000000000000000000000 old tree : 000000000000000000000000000000000000000000 cur tree : 000000000000000000000000000000000000000000 commit clock: 0 last pack : :

------------------- END OF CRASH REPORT
```

## 提示与技巧

以下提示和技巧是从各种 `fast-import` 用户那里收集的，在此提供作为建议。

### 每个提交使用一个标记（Mark）

在进行仓库转换时，为每个提交使用一个唯一的标记（`mark:<n>`）并在命令行上提供 `--export-marks` 选项。`fast-import` 将导出一个文件，列出每个标记及其对应的 Git 对象 SHA-1。如果前端可以将这些标记关联回源仓库，则可以通过比较每个 Git 提交与相应的源版本，轻松验证导入的准确性和完整性。

如果来自 Perforce 或 Subversion 等系统，这应该非常简单，因为 `fast-import` 标记也可以是 Perforce 更改集号或 Subversion 版本号。

### 自由在分支间跳转

不要试图优化前端以便在导入期间一次只固定在一个分支。虽然这样做对 `fast-import` 可能会稍微快一点，但往往会显著增加前端代码的复杂度。

`fast-import` 内置的分支 LRU（最近最少使用）机制表现非常好，激活非活动分支的成本极低，以至于在分支之间切换对导入性能几乎没有影响。

### 处理重命名

在导入重命文件或目录时，只需在相应的提交期间删除旧名称并修改新名称即可。Git 在提交后才进行重命名检测，而不是在提交期间显式地进行。

### 使用标签修复分支（Tag Fixup Branches）

某些其他 SCM 系统允许用户从多个并非同一提交/更改集的文件创建标签，或者创建仓库中可用文件子集的标签。

在 Git 中按原导入这些标签是不可能的，除非至少提交一个提交来“修复”文件以匹配标签的内容。使用 `fast-import` 的 `reset` 命令将一个位于你正常分支空间外的虚拟分支重置为标签的基础提交，然后提交一个或多个文件修复提交，最后标记该虚拟分支。

例如，由于所有正常分支都存储在 `refs/heads/` 下，将标签修复分支命名为 `TAG_FIXUP`。这样，导入器使用的修复分支就不会与源导入的真实分支产生命名空间冲突（`TAG_FIXUP` 不是 `refs/heads/TAG_FIXUP`）。

在提交修复内容时，考虑使用 `mergemerge` 来连接为修复分支提供文件版本的提交。这样做允许 `git blame` 等工具跟踪真实的提交历史并正确地标注源文件。

在 `fast-import` 终止后，前端需要执行 `rm .git/TAG_FIXUP` 来移除虚拟分支。

### 立即导入，稍后重新打包

一旦 `fast-import` 完成，Git 仓库就是完全有效并准备好使用的。这通常只需要很短的时间，即使对于大型项目（100,000+ 个提交）。

然而，重新打包（repacking）仓库对于提高数据局部性和访问性能是必要的。在极大型项目上，这可能需要几个小时（特别是当使用 `-f` 和较大的 `--window` 参数时）。由于重新打包可以在读取器和写入器旁边安全运行，请在后台运行重新打包并让它自行完成。没有理由等待才开始探索你的新 Git 项目！

如果你选择等待重新打包，在重新打包完成之前，不要尝试运行基准测试或性能测试。`fast-import` 输出的次优 packfile 在实际使用场景中永远不会出现。

### 重新打包历史数据

如果你正在重新打包非常旧的导入数据（例如早于一年前的数据），考虑花费一些额外的 CPU 时间并在运行 `git repack` 时提供 `--window=50`（或更高）。这将花费更长时间，但也会产生更小的 packfile。你只需要花费一次精力，所有使用你项目的人都将从更小的仓库中受益。

### 包含进度消息

偶尔让你的前端向 `fast-import` 发送进度消息。消息的内容完全是自由格式的，因此建议每当当前提交日期进入下个月时输出当前的月份和年份。你的用户知道已经处理了多少数据流，会感觉更好。

基于此，强烈建议用户在 `fast-import` 完成后使用 `git repack -a -d` 重新打包仓库，允许 Git 重新组织包文件以加快数据访问。如果 blob 增量（deltas）并非理想（见上文），添加 `-f` 选项强制重新计算所有增量可以显著减少最终包文件的大小（通常减小 30-50% 是很常见的）。

# 内存占用

许多因素会影响 `fast-import` 执行导入时所需的内存量。与 Git 核心的关键区域一样，`fast-import` 使用自己的内存分配器来分摊与 `malloc` 相关的开销。在实践中，由于使用了大块内存分配，`fast-import` 倾向于将任何 `malloc` 开销降低至 0。

### 每个对象 (per object)

`fast-import` 为本次执行中写入的每个对象维护一个内存中的结构。在 32 位系统上，该结构占用 32 字节；在 64 位系统上占用 40 字节（由于指针尺寸较大）。表中的对象在 `fast-import` 终止之前不会被释放。在 32 位系统上导入 200 万个对象大约需要 64 MiB 内存。对象表实际上是以对象名称（唯一的 SHA-1）为键的哈希表。这种存储允许 `fast-import` 重用已存在或已写入的对象，避免重复写入包文件。在导入过程中，由于分支合并，重复 blob 的出现出意外地常见。

### 每个标记 (per mark)

标记存储在一个稀疏数组中，每个标记使用一个指针（4 字节或 8 字节，取决于指针大小）。尽管数组是稀疏的，但仍强烈建议前端使用在 1 到 `n` 标记的标记，其中 `n` 是本次导入所需的标记总数。

### 每个分支 (per branch)

分支被分为活跃（active）和非活跃（inactive）。这两类的内存使用差异显著。

非活跃分支存储在一个结构中，每个分支使用 96 或 120 字节（分别对应 32 位或 64 位系统），加上分支名称长度（通常小于 200 字节）。`fast-import` 可以轻松地在 2 MiB 内存内处理 10,000 个非活跃分支。

活跃分支具有非活跃分支相同的开销，但还包含该分支最近修改过的每个树的副本。如果分支自变为活跃以来未被修改，则其内容不会加载到内存中；但如果分支在活跃后已被 `commit` 修改，则其内容将被加载。由于活跃分支存储该分支包含的文件元数据，其内存存储大小可能会增长（见下文）。`fast-import` 根据简单的最未使用算法自动将活跃分支移动到非活跃状态。LRU 链在每次 `commit` 命令时更新。可以通过命令行 `--active-branches=` 增加或减少活跃分支的数量。

### 每个活跃树 (per active tree)

树（即目录）除了条目所需的内存外仅使用 12 字节内存。树的成本几乎为 0，因为其开销分摊到了单个文件条目。

### 每个活跃文件 (per active file)

活跃树中的文件（以及指向树的指针）每个条目需要 52 或 64 字节（32/64 位平台）。为了节省空间，文件名和树名被池化在一个字符串表中，无论在项目中出现多少次。活跃分支 LRU 结合文件名字符串池和树的懒加载，允许 `fast-import` 在极有限的内存占用下导入 2000+ 分支和 45114+ 文件（每个活跃分支小于 2.7 MiB）。

# 信号 (SIGNALS)

向 `git fast-import` 进程发送 `SIGUSR1` 会提前结束当前的包文件，模拟检查命令。急躁的操作可以使用此机制查看正在导入的对象和引用，代价是增加了一些运行时间和更差的压缩。

# 参见 (SEE ALSO)

(1)

* *

# GIT-FETCH-PACK

## 名称

`git-fetch-pack` - 从另一个仓库接收缺失的对象

## 概要 (SYNOPSIS)

`git fetch-pack` "[--all] [--quiet|-q] [--keep|-k] [--thin] [--include-tag] [--upload-pack=<git-upload-pack>] [--depth=<n>] [--no-progress] [-v] <repository> [<refs>...]`

## 描述 (DESCRIPTION)

通常你会希望使用 `git fetch`，它是该命令的高级封装。

它在可能的远程仓库上调用 `git-upload-pack`，并请求其发送该仓库缺失的对象以更新命名头部。本地的提交列表通过扫描本地 `refs/` 层级找到，并发送到运行在另一端的 `git-upload-pack`。当本地没有共同祖先提交时，该命令退化为下载所有内容以完成远程所需的引用。

## 选项 (OPTIONS)

--all

获取所有远程引用。

--stdin

从 `stdin` 读取引用列表，每行一个。除了此选项外命令行还指定了引用，则 `stdin` 中的引用将在命令行引用之后处理。

如果与此选项一起指定 `--stateless-rpc`，引用列表必须是包格式（`pkt-line`）。每个引用必须在一个包中，列表必须以刷新包（flush packet）结束。

-q, --quiet

将 `-q` 标志传递给 `git unpack-objects`；这会让拷贝过程不那么详细。

-k, --keep

不要对接收的数据调用 `git unpack-objects`，而是将其创建一个单个包文件，并存储在对象数据库中。如果提供两次，则该包被锁定无法重新打包。

--thin

获取一个“薄”包，它根据包中未包含的对象以增量形式记录对象，以减少网络流量。

--include-tag

如果远程端支持，如果标记引用的对象被下载，则注释标记对象将与其他对象在同一连接中下载。否则，调用者必须确定此选项提供了哪些标记。

--upload-pack=<git-upload-pack>

如果在你的 `$PATH` 中未找到，使用此项指定远程侧 `git-upload-pack` 的路径。`sshd` 的安装会忽略登录 shell 的用户环境设置脚本（例如 `.bash_profile`），你私安装的 git 可能在系统默认 `$PATH` 中找不到。另一个建议的变通方法是在 `.bashrc` 中设置 `$PATH`，但此标志适用于那些不想通过精简 `.bashrc` 文件为非交互式 shell 支付开销的人（他们将大部分设置放在 `.bash_profile` 中）。

--exec=<git-upload-pack>

与 `--upload-pack=<git-upload-pack>` 相同。

--depth=<n>

限制获取长度不超过 `n` 的祖先链。`git-upload-pack` 将特殊深度 2147483647 视为无限，即使存在那么长的链。

--no-progress

不显示进度。

--check-self-contained-and-connected

如果收到的包是自包含且连接的，则输出 "connectivity-ok"。

-v

详细运行。

<repository>

远程仓库的 URL。

<refs>...

要从其更新的远程头部。相对于 `$GIT_DIR`（例如 "HEAD", "refs/heads/master"）。未指定时，从远程端所有的头部进行更新。

从一个或多个其他仓库获取分支和/或标签（统称为“refs”）以及完成其历史记录所需的对象。远程跟踪分支将被更新（有关控制此行为的方法，请参见下文对 `<refspec>` 的描述）。

默认情况下，任何指向被获取历史记录的标签也会被获取；其效果是获取指向你感兴趣的分支的标签。这种默认行为可以通过 `--tags` 或 `--no-tags` 选项，或者通过配置 `remote.<name>.tagOpt` 来更改。通过使用显式获取标签的 refspec，你还可以获取那些没有指向你所感兴趣的分支的标签。

`git fetch` 可以从单个命名的仓库或 URL 获取，也可以在给定了 `<group>` 且配置文件中存在 `remotes.<group>` 条目的情况下，一次性从多个仓库获取。（参见 (1)）。

在未指定远程仓库的情况下，默认将使用 `origin` 远程仓库，除非当前分支配置了上游分支。

被获取的 refs 名称以及它们指向的对象名称将写入 `.git/FETCH_HEAD`。这些信息可能被脚本或其他 git 命令使用，例如 (1)。

### 选项

### --all

获取所有远程仓库。

### -a, --append

将获取的 refs 的名称和对象名称追加到 `.git/FETCH_HEAD` 的现有内容中。如果没有此选项，`.git/FETCH_HEAD` 中的旧数据将被覆盖。

### --depth=<depth>



深化或缩短由`git clone`使用`--depth=<depth>`选项创建的浅层（shallow）仓库的历史（参见 (1)），使其延伸到每个远程分支历史顶端起的指定提交数。对于深化的提交，标签不会被获取。

### `--unshallow`

如果源仓库是完整的，则将浅层仓库转换为完整仓库，移除浅层仓库产生的所有限制。

如果源仓库是浅层的，则尽可能获取，使当前仓库与源仓库具有相同的历史。

### `--update-shallow`

默认情况下，当从浅层仓库获取内容时，`git fetch`会拒绝需要更新`.git/shallow`的 refs。此选项会更新`.git/shallow`并接受此类 refs。

### `--dry-run`

显示将要执行的操作，但不进行任何更改。

### `-f, --force`

当使用`<rbranch>:<lbranch>` refspec 执行`git fetch`时，除非获取的远程分支`<rbranch>`是`<lbranch>`的后代，否则它将拒绝更新本地分支`<lbranch>`。此选项将覆盖该检查。

### `-k, --keep`

保留下载的 pack 文件。

### `--multiple`

允许指定多个`<repository>`和`<group>`参数。不能指定任何`<refspec>`。

### `-p, --prune`

获取后，删除任何在远程端已不存在的远程跟踪引用。如果标签仅是因为默认的标签自动跟随或由于`--tags`选项而被获取，则它们不受剪裁的影响。然而，如果标签是因为显式 refspec 获取的（例如在命令行中或远程配置中，或者如果远程仓库是使用`--mirror`选项克隆的），则它们也将受到剪裁的影响。

### `-n, --no-tags`

默认情况下，指向从远程仓库下载对象的标签会被获取并存储在本地。此选项禁用了这种自动跟踪标签。远程仓库的默认行为可以通过`remote.<name>.tagOpt`设置来指定。参见 (1)。

### `--refmap=<refspec>`

在获取命令行列出的 refs 时，使用指定的 refspec（可以给出多次）将 refs 映射到远程跟踪分支，而不是使用该远程仓库的`remote.*.fetch`配置变量的值。详细信息请参见“配置的远程跟踪分支”章节。

### `-t, --tags`

除了其他可能获取的所有内容外，从远程获取所有标签（即将远程标签`refs/tags/*`获取到本地同名的标签中）。单独使用此选项不会使标签受到剪裁，即使使用了`--prune`（但如果标签也是显式 refspec 的目标，它们可能仍会被剪裁；参见`--prune`）。

### `--recurse-submodules[=yes|on-demand|no]`

此选项控制是否以及在什么种条件下也获取已填充子模块的新提交。它可以作为布尔选项使用：当设置为`no`时完全禁用递归；当设置为`yes`时无条件地进入所有已填充的子模块（这是在使用选项时不带任何值时的默认值）。使用`on-demand`仅当超父项目获取了更新子模块引用的提交，且该提交不在本地子模块克隆中时，才递归进入已填充的子模块。

### `--no-recurse-submodules`

禁用子模块的递归获取（这等同于使用`--recurse-submodules=no`选项）。

### `--submodule-prefix=<path>`

在信息消息（如“Fetching submodule foo”）中打印的路径前加上`<path>`。此选项在递归处理子模块时内部使用。

### `--recurse-submodules-default=[yes|on-demand]`

此选项内部用于为`--recurse-submodules`选项临时提供一个非负默认值。所有其他配置 fetch 子模块递归的方法（例如 (5) 和 (1) 中的设置）都会覆盖此选项，直接指定`--[no-]recurse-submodules`也是如此。

### `-u, --update-head-ok`

默认情况下`git fetch`拒绝更新对应当前分支的头。此标志禁用该检查。这纯用于`git pull`内部与`git fetch`通信，除非你正在实现自己的 Porcelain（用户界面），否则不应该使用它。

### `--upload-pack <upload-pack>`

如果提供了该参数，且要获取的仓库由`git fetch-pack`处理，则会将`--exec=<upload-pack>`传递给命令，以指定在对方运行命令的非默认路径。

### `-q, --quiet`

将`--quiet`传递给`git-fetch-pack`并静默其他内部使用的 git 命令。进度不会报告到标准错误流。

### `-v, --verbose`

详细输出。

### `--progress`

当连接到终端时，默认将进度状态报告到标准错误流，除非指定了`-q`。此标志即使在标准错误未定向到终端也会强制报告进度状态。

### `<repository>`

作为 fetch 或 pull 操作的“远程”仓库。此参数可以是 URL（参见下文 GIT URLS 章节）或远程名称（参见下文 REMOTES 章节）。

### `<group>`

指向配置文件中`remotes.<group>`值的仓库列表名称。（参见 (1)）。

### `<refspec>`

指定获取哪些 refs 以及更新哪些本地 refs。当命令行上没有出现`<refspec>`时，将从`remote.<repository>.fetch`变量读取要获取的 refs（参见下文 CONFIGURED REMOTE-TRACKING BRANCHES）。

`<refspec>`参数的格式是一个可选的加号`+`，随后是源 ref`<src>`，然后是冒号`:`，最后是目标 ref`<dst>`。当`<dst>`为空时可以省略冒号。

`tag <tag>`等同于`refs/tags/<tag>:refs/tags/<tag>`；它请求获取指定标签之前的所有。

匹配`<src>`的远程 ref 被获取，如果`<dst>`不是空字符串，则使用`<src>`对匹配的本地 ref 进行快进（fast-forward）。如果使用了可选加号`+`，即使没有导致快进更新，本地 ref 也会更新。

**注意**

当已知要获取的远程分支会经常回滚和重基时，预计其新顶端不会是之前的顶端（即你上次获取时存储在远程跟踪分支中的）的后代。你可能希望使用`+` Sign 来表示需要非快进更新。没有方法可以确定或声明仓库将提供具有这种行为的分支；拉取用户只需知道这是该分支预期的使用模式。

通常情况下，URL 包含有关传输协议、远程服务器地址以及仓库路径的信。根据传输协议的不同，这些信息中的部分可能会缺失。

Git 支持`ssh`、`git`、`http`和`https`协议（此外，可以使用`ftp`和`ftps`用于抓取，可以使用`rsync`用于抓取和推送，但这些效率低下且已弃用；请勿使用）。

原生传输（即`git://` URL）不进行身份验证，在不安全的网络上使用时应谨慎。

这些协议可以使用以下语法：

```
http[s]://host.xz[:port]/path/to/repo.git/
```

```
ftp[s]://host.xz[:port]/path/to/repo.git/
```

在`ssh`协议下也可以使用另一种类似 scp 的语法：

```
[user@]host.xz:path/to/repo.git/
```

这种语法仅在第一个冒号之前没有斜杠时才会被识别。这有助于区分包含冒号的本地路径。例如，本地路径`foo:bar`可以指定为绝对路径或`./foo:bar`，以避免被误读为 ssh url。

`ssh`和`git`协议还支持`~username`扩展：

```
[user@]host.xz:/~[user]/path/to/repo.git/
```

对于 Git 原生支持的本地仓库，可以使用以下语法：

```
/path/to/repo.git/
```

这两种语法大多数情况下是等价，但在克隆（clone）时，前者意味着`--local`选项。详情请见 (1)。

当 Git 不知道如何处理特定的传输协议时，它会尝试使用`remote-<transport>`远程助手（如果存在的话）。要显式请求远程助手，可以使用以下语法：

```
<transport>::<address>
```

其中`<address>`可以是一个路径、服务器和路径，或者是由调用的特定远程助手所识别的任意 URL 类字符串。详情请见 (1)。

如果存在大量命名相似的远程仓库，且你想为它们使用不同的格式（以便你使用的 URL 将被重写为可以运行的 URL），你可以创建一个如下形式的配置节：

```
[url "<actual url base>"]
insteadOf = <other url base>
```

例如，使用以下内容：

```
[url ""]
insteadOf = host.xz:/path/to/
insteadOf = work:
```

那么像`"work:repo.git"`或`"host.xz:/path/to/repo.git"`这样的 URL 在任何接受 URL 为`""`的上下文中被重写。

如果你只想针对推送（push）重写 URL，可以创建一个如下形式的配置节：

```
[url "<actual url base>"]
pushInsteadOf = <other url base>
```

例如，使用以下内容：

```
[url ""]
pushInsteadOf =
```

那么像` `的 URL 在推送时将被重写为` `，但拉取（pull）仍将使用原始 URL。

# REMOTES

可以使用以下名称之一代替 URL 作为`<repository>`参数：

- Git 配置文件中的远程：`$GIT_DIR/config`，
- `$GIT_DIR/remotes`目录下的文件，或
- `$GIT_DIR/branches`目录下的文件。

所有这些都允许你从命令行中省略引用规范（refspec），因为它们各包含一个 git 将默认使用的引用规范。

## 配置文件中的命名远程

你可以选择提供之前通过 (1)、(1) 甚至手动编辑`$GIT_DIR/config`文件配置的远程名称。该远程的 URL 将用于访问仓库。当你不在命令行上提供引用规范时，该远程的引用规范将被默认使用。配置文件中的条显示所示：

```
[remote "<name>"]
url = <url>
pushurl = <pushurl>
push = <refspec>
fetch = <refspec>
```

`<pushurl>`仅用于推送。它是可选的，默认为`<url>`。

## `$GIT_DIR/remotes`中的命名文件

你可以选择提供`$GIT_DIR/remotes`中的一个文件名。该文件中的 URL 将用于访问仓库。当你不在命令行上提供引用规范时，该文件中的引用规范将作为默认使用。该文件应具有以下格式：

```
URL: one of the above URL format
Push: <refspec>
Pull: <refspec>
```

## `$GIT_DIR/branches`中的命名文件

你可以选择提供`$GIT_DIR/branches`中的一个文件名。该文件中的 URL 将用于访问仓库。当你不在命令行上提供引用规范时，该文件中的引用规范将作为默认使用。该文件应具有以下格式：

```
<url>#head>
```

`<url>`是必须的；`<head>`是可选的。

## CONFIGURED REMOTE-TRACKING BRANCHES

你经常通过定期从同一个远程抓取来交互。为了跟踪此类远程的进度，`git fetch`变量可能如下所示：

```
[remote "origin"]
fetch = +refs/heads/*:remotes/origin/*
```

上述命令将远程`refs/heads/`空间下的所有分支并存储到本地`refs/remotes/origin/`空间，除非使用`branch.<name>.fetch`选项来指定非默认的引用规范。

当运行`git fetch`而没有在命令行上指定要抓取的分支和/或标签，`branch.<name>.fetch`值将作为引用规范——它们指定了要更新哪些引用。上面的示例将抓取 origin 中存在的所有分支。

当运行`git fetch`并在命令行明确指定要抓取的分支和/或标签（例如`git fetch origin master`），命令行给出的`<refspec>`决定了抓取的内容（即当命令行列出引用规范时，这些值不被视为引用规范）；它们仅用于通过当映射来决定抓取的引用存储在何处。后者的`remote.<repository>.fetch`值可以通过在命令行上提供`--refmap=<refspec>`参数来覆盖。

## EXAMPLES

更新远程跟踪分支：

```
$ git fetch origin
```

显式使用引用规范：

```
$ git fetch origin +pu:pu maint:tmp
```

这通过从远程仓库分别从`pu`和`maint`分支抓取，更新（根据需要创建）本地仓库中的`pu`和`tmp`分支。

即使`pu`分不是快进（fast-forward），也会被更新，因为它带有加号前缀；`tmp`则不会。

在不在本地仓库中配置远程的情况下查看远程分支：

```
$ git fetch maint
```

```
$ git log FETCH_HEAD
```

目前使用`--recurse-submodules`只能在已检出的子模块中获取新提交。例如，当上游在刚刚获取的父项目提交中添加了新的子模块时，子模块本身无法被获取，导致以后在不重新执行 fetch 的情况下无法检出该子模块。预计将在未来的 Git 版本中修复。

## 另请

(1)

# GIT-FILTER-BRANCH

## 名称

`git-filter-branch` - 重写分支

## 概要概要

```
git filter-branch [--env-filter <command>] [--tree-filter <command>] [--index-filter <command>] [--parent-filter <command>] [--msg-filter <command>] [--commit-filter <command>] [--tag-name-filter <command>] [--subdirectory-filter <directory>] [--prune-empty] [--original <namespace>] [-d <directory>] [-f | --force] [--] [<rev-list options>...]
```

## 描述

允许你通过重写`<rev-list options>`中提到的分支来重写 Git 修订历史，并对每个修订应用自定义过滤器。这些过滤器可以修改每个树（例如删除文件或对所有文件运行 perl 重写）或每个提交的信息。否则，所有信息（包括原始提交时间或合并信息）将得到保留。

该命令只会重写命令行中提到的“正”引用（例如，如果你传递`a..b`，则只有`b`会被重写）。如果你未指定过滤器，提交将在无任何更改的情况下重新提交，这通常不会产生影响。尽管如此，这在未来对于补偿某些 Git 错误等情况可能有用，因此允许这种用法。

**注意**：此命令尊重`.git/info/grafts`文件和`refs/replace/`命名空间中的引用。如果你定义了任何移植（grafts）或替换引用，运行此命令将使它们永久化。

**警告**：重写后的历史所有对象具有不同的不同的名称，且不会与原始分支汇合。你无法轻松地将重写后的分支推送并发布到原始分支之上。如果你不清楚其影响，请勿使用此命令；如果一个简单的单提交就能解决你的问题，请尽量避免使用它。（有关重写已发布历史的更多信息，请参见 (1) 中的“从上游变基中恢复”章节。）

务必验证重写后的版本是正确的：原始引用如果与重写后的不同，将存储在`refs/original/`命名空间中。

注意，由于此操作非常消耗 I/O，使用`-d`选项将临时目录重定向到磁盘外（例如在`tmpfs`上）可能是一个好主意。据报道，速度提升非常明显。

### 过滤器

过滤器按下面的顺序应用。`<command>`参数始终在 shell 环境中使用`eval`命令评估（由于技术原因，提交过滤器除外）。在此之前，将设置环境变量`$GIT_COMMIT`，其内容包含正在重写的提交的 ID。此外，`GIT_AUTHOR_NAME`、`GIT_AUTHOR_EMAIL`、`GIT_AUTHOR_DATE`、`GIT_COMMITTER_NAME`、`GIT_COMMITTER_EMAIL`和`GIT_COMMITTER_DATE`将从当前提交中提取并导出到环境中，以便影响过滤器运行后由 (1) 创建的替换提交的作者和提交者身份。

如果`<command>`的任何评估返回非零退出状态，整个操作将终止。

提供了一个`map`函数，它接收一个“原始 sha1 id”参数，如果提交已重写，则输出“重写后的 sha1 id”，否则输出“原始 sha1 id”；如果你的提交过滤器输出了多个提交，`map`函数可以在单独行返回多个 ID。

### 选项

### `--env-filter <command>`

如果你只需要修改执行提交的环境，则可以使用此过滤器。具体而言，你可能想要重写作者/提交者姓名/邮箱/时间环境变量（详情见 (1)）。不要忘记重新导出这些变量。

### `--tree-filter <command>`

这是用于重写树及其内容的过滤器。该参数在 shell 中评估，其工作目录被设置为检出树的根目录。然后将原样使用新树（新文件将自动添加，消失的文件将自动删除——`.gitignore`文件或任何其他忽略规则**不起作用**！）。

### `--index-filter <command>`



这是用于重写索引的过滤器。它与树过滤器类似，但不会检出树，这使得速度快得多。经常与`git rm --cached --ignore-unmatch ...`配合使用，见下示例。对于复杂情况，请参见(1)。

### `--parent-filter <command>`

这是用于重写提交父节点列表的过滤器。它从标准输入接收父字符串，并在标准输出输出新的父字符串。父字符串的格式如(1)所示：初始提交为空，普通提交为`-p parent`，合并提交为`-p parent1 -p parent2 -p parent3 ...`。

### `--msg-filter <command>`

这是用于重写提交消息的过滤器。该参数在 shell 中评估，标准输入为原始提交消息；其标准输出被用作新的提交消息。

### `--commit-filter <command>`

这是执行提交的过滤器。如果指定了此过滤器，它将代替`git commit-tree`命令被调用，参数格式为`<TREE_ID> [(-p <PARENT_COMMIT_ID>)...]`，标准输入为日志消息。期望在标准输出上获得提交 ID。

作为一种特殊扩展，提交过滤器可能会产生多个提交 ID；在这种情况下，原始提交的重写子节点将所有这些 ID 作为父节点。

你可以在此过滤器中使用`map`方便函数以及方便函数。例如，调用`skip_commit "$@"`将跳过当前提交（但不包括它的更改！如果你需要这样做，请使用`git rebase`）。

如果你不想保留只有一个父节点且对树没有任何更改的提交，可以使用`git_commit_non_empty_tree "$@"`代替`git commit-tree "$@"`。

### `--tag-name-filter <command>`

这是用于重写标签名的过滤器。当传递时，它会对每个指向重写对象（或指向重写对象的标签对象）的标签引用调用。原始标签名通过标准输入传递，期望在标准输出获得新的标签名。原始标签不会删除，但可以覆盖；使用`--tag-name-filter cat`可以简单更新标签。在这种情况下，请务必小心，确保你已备份旧标签，以防转换出错。

支持对标签对象的近完美重写。如果标签带有消息，将创建一个具有相同消息、作者和时间戳的新标签对象。如果标签带有签名，签名将被移除。根据定义，保留签名是不可能的。之所以说是“近乎”完美，是因为理想情况下，如果标签没有变化，它应该保留任何签名。

只查看涉及给定子目录的历史。结果将包含该目录（仅包含该目录）作为其项目根目录。这意味着“映射到祖先”部分。

### `--prune-empty`

某些过滤器会生成空提交（commits），这些提交会让树结构保持不变。此开关允许`git-filter-branch`忽略此类提交。尽管如此，该开关仅适用于有一个且只有一个父提交的提交，因此它会保留合并点。此外，此选项与`--commit-filter`使用不兼容。不过你只需要在提交过滤器中使用函数`git_commit_non_empty_tree "$@"`代替`git commit-tree "$@"`模式即可实现这一效果。

### `--original <namespace>`

使用此选项设置存储原始提交的命名空间。默认值是`refs/original`。

### `-d <directory>`

使用此选项设置用于重写的临时目录路径。在应用树过滤器（tree filter）时，命令需要将树临时检出（checkout）到某个目录，对于大型项目，这可能会消耗大量空间。默认情况下，它在`.git-rewrite/`目录下执行，但你可以通过此参数覆盖该选择。

### `-f, --force`

除非强制执行，否则`git filter-branch`会在已存在临时目录或已存在以`refs/original/*`开头的引用（refs）时拒绝启动。

### `<rev-list options>...`

`git rev-list`的参数。这些选项包含的所有正向引用（positive refs）都会被重写。你也可以指定如`--all`等选项，但你必须使用`--*`将它们与`git filter-branch`的选项分开。这隐含了“重映射到祖先（Remap to ancestor）”部分。

#### 重映射到祖先

通过使用(1)参数（例如路径限制器），你可以限制被重写的修订集。然而，命令行上的正向引用是有区别的：我们不让它们被此类限制器排除。出于此目的，它们会被重写为指向未被排除的最近祖先。

## 示例 (EXAMPLES)

假设你想从所有提交中删除一个文件（包含机信息或侵犯版权）：

```bash
git filter-branch --tree-filter 'rm filename' HEAD
```

然而，如果文件不存在于某个提交的树中，简单的`rm filename`将会导致树和提交失败。因此，你可能想使用`rm -f filename`作为脚本。

配合`git rm`使用`--index-filter`可以得到一个显著更快的版本。就像使用`rm filename`一样，如果文件不存在于提交的树中，`git rm --cached filename`将失败。如果你想“完全忘记”一个文件，它何时进入历史并不重要，所以我们还添加了`--ignore-unmatch`：

```bash
git filter-branch --index-filter 'git rm --cached --ignore-unmatch filename' HEAD
```

现在，你将获得保存在`HEAD`中的重写后的历史。

要重写仓库使得`foodir/`看起来是项目根目录，并丢弃所有其他历史：

```bash
git filter-branch --subdirectory-filter foodir -- --all
```

因此，你可以将一个库子目录转换为它自己的仓库。注意使用`--`将`filter-branch`选项与修订选项分开，并使用`--all`重写所有分支和标签。

为了将一个提交（通常位于另一个历史的末端）设置为当前初始提交的父提交，以便将另一个历史粘贴在当前历史之后：

```bash
git filter-branch --parent-filter 'sed "s/^\$/-p <graft-id>/"' HEAD
```

（如果父字符串为空——这在我们处理初始提交时发生——添加`graftcommit`作为父提交）。注意，这假设历史只有一个根（即没有发生没有共同祖先的合并）。如果不是如此，使用：

```bash
git filter-branch --parent-filter 'test $GIT_COMMIT = <commit-id> && echo "-p <graft-id>" || cat' HEAD
```

或者更简单：

```bash
echo "$commit-id $graft-id" >> .git/info/grafts git filter-branch $graft-id..HEAD
```

从历史中删除由“Darl McBribe”编写的提交：

```bash
git filter-branch --commit-filter ' if [ "$GIT_AUTHOR_NAME" = "Darl McBribe" ]; then skip_commit "$@"; else git commit-tree "$@"; fi' HEAD
```

函数`skip_commit`定义如下：

```bash
skip_commit() { shift; while [ -n "$1" ]; do shift; map "$1"; shift; done; }
```

`shift`魔法操作首先丢弃树 ID，然后丢弃`-p`参数。注意这会正确处理合并！如果 Darl 提交了`P1`和`P2`之间的合并，它将被正确传播，该合并的所有子节点将成为以`P1,P2`为父的合并提交，而不是合并提交本身。

**注意**，提交引入的且未被后续提交撤销的更改仍然存在于重写后的分支中。你可以使用`--msg-filter`重写提交日志消息。例如，由`git svn`创建的仓库中的`git svn-id`字符串可以通过这种方式移除：

```bash
git filter-branch --msg-filter ' sed -e "/^git-svn-id:/d" '
```

如果你需要向例如最后 10 个提交（都不是合并）添加`Acked-by`行，请使用此命令：

```bash
git filter-branch --msg-filter ' cat && echo "Acked-by: Bugs Bunny <>" ' HEAD~10..HEAD
```

`--env-filter`选项可以修改提交者和/或作者身份。例如，如果你发现由于`user.email`配置错误导致你的提交身份错误，你可以在发布项目之前进行如下修正：

```bash
git filter-branch --env-filter ' if test "$GIT_AUTHOR_EMAIL" = "" then GIT_AUTHOR_EMAIL= export GIT_AUTHOR_EMAIL fi if test "$GIT_COMMITTER_EMAIL" = "" then GIT_COMMITTER_EMAIL= export GIT_COMMITTER_EMAIL fi ' -- --all
```

要将重写限制在历史的一部分，除了新分支名称外，还要指定修订范围。新分支名称将指向`git rev-list`该范围打印的最顶端修订。

考虑这段历史：

`D--E--F--G--H / / A--B-----C`

仅重写提交 D,E,F,G,H，但保留 A、B 和 C，使用：

```bash
git filter-branch ... C..H
```

要重写 E,F,G,H，使用以下任一：

```bash
git filter-branch ... D..H
```

```
git filter-branch --not C
```

要将整个树移动到子目录，或者从中移除：

```bash
git filter-branch --tree-filter 'git ls-files -s | sed "s-\t\"&subdir/-" | GIT_INDEX_FILE=$GIT_INDEX_FILE.new \ git update-index --info && mv "$GIT_INDEX_FILE"' HEAD
```

## 缩小仓库的清单 (CHECKLIST FOR SHRINKING A REPOSITORY)

`filter-branch`可用于删除部分文件，通常结合`--index-filter`和`--subdirectory-filter`。人们期望生成的仓库比原始仓库小，但你还需要更多步骤才能使其变小，因为 Git 会尽量不丢失你的对象，除非你告诉它。首先确保：

1. 你确实删除了文件名的所有变体（如果该 blob 在生命周期内移动过）。`git log --name-only --follow --all -- filename`可以帮助查找重命名。

2. 你确实过滤了所有引用：调用`filter-branch`时使用`--tag-name-filter cat -- --all`。

然后有两种获取更小仓库的方法。更安全的方法是克隆，保持原始仓库完整。

使用`git clone`克隆。克隆将不包含被删除的对象。（注意使用普通路径克隆只是硬链接所有内容！）。

出于任何原因，如果你真的不想克隆，请检查以下点（按此顺序）。这是一个极具破坏性的方法，因此请**备份**或返回克隆。你已经收到警告了。

- 删除由`filter-branch`备份的原始引用：例如执行`git for-each-ref --format="%(refname)" refs/original/ | xargs -n 1 git update-ref -d`。

- 过期所有引用日志（reflogs）：`git reflog expire --expire=now --all`。

- 回收所有未引用的对象：`git gc --prune=now`（如果你的`git-gc`尚不支持向`--prune`传递参数，请使用`git repack -ad; git prune`代替）。

`git-filter-branch`允许你对 Git 历史进行复杂的脚本化重写，但如果你只是简单地移除大文件或密码等不需要的数据，你可能不需要这种灵活性。对于这些操作，你可能希望考虑`The BFG Repo-Cleaner`，它是基于 JVM 的`git-filter-branch`替代方案，在这些用例下，速度通常快 10-50 倍，并且具有完全不同的特性：

任何特定版本的都会会被精确清理一次。与`git-filter-branch`不同，`BFG`不允许你根据文件在历史中提交的位置或时间来以不同的方式处理文件。这种限制提供了`The BFG`的核心性能优势，并且非常适合清理坏数据任务——你不在乎坏数据在哪里，你只想让它消失。

默认情况下，`The BFG`会充分利用多核机器，并行清理提交的文件树。而`git-filter-branch`按顺序清理提交（即以单线程方式），尽管可以在针对每个提交执行的脚本中编写包含自身并行性的过滤器。

`command options`比`git-filter-branch`严格得多，并且专门用于移除不需要的数据任务——例如：`--strip-blobs-bigger-than 1M`。

## GIT

(1) 套件的一部分

### NOTES

1. `The BFG Repo-Cleaner`

2. `command options`

# GIT-FMT-MERGE-MSG

## 名称

`git-fmt-merge-msg` - 生成合并提交消息

## 概要

```bash
git fmt-merge-msg [-m <message>] [--log[=<n>] | --no-log] <$GIT_DIR/FETCH_HEAD>
git fmt-merge-msg [-m <message>] [--log[=<n>] | --no-log] -F <file>
```

## 描述

从标准输入读取合并对象的列表，并生成一个用于合并提交的合适提交消息，通常作为`<merge-message>`参数传递给`git merge`。

此命令主要供自动调用`git merge`的脚本内部使用。

## OPTIONS

`--log[=<n>]`: 除了分支名外，使用来自实际合并提交的单行描述填充日志消息。每个合并父节点最多使用`<n>`个提交（如果省略`<n>`则为 20 个）。这会覆盖`merge.log`配置变量。

`--no-log`: 不列出来自实际合并提交的单行描述。

`--[no-]summary`: `--log`和`--no-log`的同义词；这些已弃用，并在未来被移除。

`-m <message>, --message <message>`: 使用`<message>`代替分支名作为日志消息的第一行。配合`--log`使用。

`-F <file>, --file <file>`: 从`<file>`而不是标准输入获取合并对象列表。

## 配置

`merge.branchdesc`: 除了分支名外，用与它们相关的分支描述文本填充日志消息。默认值为 false。

`merge.log`: 除了分支名外，用来自实际合并提交的最多指定数量的单行描述填充日志消息。默认值为 false，且 true 是 20 的同义词。

`merge.summary`: `merge.log`的同义词；这已弃用，并在未来被移除。

## 参见

(1)

# GIT-FOR-EACH-REF

## 名称

`git-for-each-ref` - 输出每个 ref 的信息

## 概要

```bash
git for-each-ref [--count=<count>] [--shell|--perl|--python|--tcl] [(--sort=<key>)...] [--format=<format>] [<pattern>...]
```

## 描述

遍历所有匹配`<pattern>`的 ref，并在根据给定的`<key>`排序后按照给定的`<format>`显示它们。如果给了`<count>`，则在显示相应数量后停止。`<format>`中的插值可以可选地引用为指定主机语言的字符串字面量，允许在相应语言中直接求值。

## OPTIONS

`--count=<count>`: 默认情况下，命令显示所有匹配`<pattern>`的 ref。此选项使其在显示相应数量后停止。

`<key>`: 用于排序的字段名。前缀`-`表示按值的降序排序。如果未指定，则使用`refname`。你可以多次使用`--sort=<key>`选项，在这种情况下，最后一个键将成为主键。

`<format>`: 一个字符串，用于插值来自正在显示的 ref 指向对象的`%(fieldname)`。如果`fieldname`以星号（`*`）为前缀且 ref 指向标签对象，则使用所引标签对象中的字段值。如果未指定，默认为`%(objectname) SPC %(objecttype) TAB %(refname)`。它还会插值`%%`为`%`，并将`%xx`（其中`xx`是十六进制数字）插值为十六进制代码为`xx`的字符；例如`%00`插值为`\0` (NUL)，`%09`插值为`\t` (TAB)，`%0a`插值为`\n` (LF)。

`<pattern>...`: 如果给出一个或多个模式，则仅显示至少一个模式的 ref，使用(3)或字面匹配（后者情况下是完全匹配或从开始到斜杠的匹配）。



`--shell`、`--perl`、`--python`、`--tcl`：如果给出，替换 `%(fieldname)` 占位符的字符串将引用为适用于指定主机语言的字符串字面量。旨在产生一个可以直接被 `eval` 的脚本。

## 字段名称

引用对象中结构化字段的各种值可以插值到结果输出中，或作为排序键。

对于所有对象，可以使用以下名称：

- `refname`：`ref` 的名称（`$GIT_DIR/` 之后的部分）。对于无歧义的 `ref` 短名，附加 `:short`。使用选项 `core.warnAmbiguousRefs` 来选择严格缩写模式。
- `objecttype`：对象的类型（`blob`、`tree`、`commit`、`tag`）。
- `objectsize`：对象的大小（与 `git cat-file -s` 报告的相同）。
- `objectname`：对象名称（即 SHA-1）。对于无歧义的对象名称缩写，附加 `:short`。
- `upstream`：一个本地 `ref` 的名称，可以被视为显示 `ref` 的“上游”。以与上述 `refname` 相同的方式尊重 `:short`。此外，尊重 `:track` 以显示 `[ahead N, behind M]`；`:trackshort` 显示简洁版本：`>`（领先）、`<`（落后）或 `=`（同步）。如果没有关联跟踪信息，则无影响。
- `push`：代表 `@{push}` 位置的本地 `ref` 名称。与 `upstream` 相同，尊重 `:short`、`:track` 和 `:trackshort`。如果没有配置 `@{push}`，则产生空字符串。
- `HEAD`：如果 `HEAD` 匹配当前 `ref`（检出的分支），则为 `' '`；否则为空。
- `color`：更改颜色。后接 `:<colorname>`，其中名称在 `color.*` 中描述。

除了上述内容，对于 `commit` 和 `tag` 对象，头部字段名（`tree`、`parent`、`object`、`type`、`tag`）可用于指定头部字段的值。

具有名称-邮箱-日期元组值的字段（`author`、`committer`、`tagger`）可以附加 `name`、`email` 和 `date`，以提取命名组件。

`commit` 和 `tag` 对象中的完整消息是 `contents`。其第一行是 `contents:subject`，其中 `subject` 是消息中第一个空行之前的所有行。下一行是 `contents:body`，其中 `body` 是第一个空行之后的所有行。最后，可选的 GPG 签名是 `contents:signature`。

为了排序，具有数值的字段按数值排序（`objectsize`、`authordate`、`committerdate`、`taggerdate`）。所有其他字段均按其字节值排序。

在任何情况下，引用 `ref` 指向对象的不可适用字段名都不会导致错误。相反，返回空字符串。

作为日期类型字段的特例，你可以通过在字段名末尾添加 `:default`、`:relative`、`:short`、`:local`、`:iso8661`、`:rfc2822` 或 `:raw` 之一为日期指定格式；例如 `%(taggerdate:relative)`。

## 示例

直接生成格式化文本的示例。显示最近的 3 个标签提交：

```bash
#!/bin/sh
git for-each-ref --count=3 --sort='-authordate' \
  --format='From: %(*authorname) %(*authormail) Subject: %(*subject) Date: %(*ordate) Ref: %(*refname) %(body)'
```

一个在输出上使用 `--shell` 的简单示例，列出所有头部的前缀：

```bash
#!/bin/sh
git for-each-ref --shell --format="ref=%(refname)" refs/heads | \
while read entry
do
  eval "$entry"
  echo `dirname $ref`
done
```

关于标签的更详细报告，是一个完整的脚本：




```bash
#!/bin/sh
fmt='
r=%(refname)
t=%(*objecttype)
T=${r#refs/tags/}
o=%(*objectname)
n=%(*authorname)
e=%(*authormail)
s=%(*subject)
d=%(*ordate)
b=%(*body)
kind=Tag
test "z$t" = z && {
    t=%(objecttype)
    kind="Lightweight tag"
    o=%(*objectname)
    n=%(*authorname)
    e=%(*authormail)
    s=%(*subject)
    d=%(*ordate)
    b=%(*body)
}
echo "$kind $T points at $t object $o"
if test "z$t" = zcommit
then
    echo "The commit was authored by $n at $d, and titled $s"
    echo "Its message reads as: "
    echo "$b" | sed -e "s/^/    /"
    echo
fi
'
eval=`git for-each-ref --shell --format="$fmt" \
    --sort='*objecttype' \
    --sort=-tagdate \
    refs/tags`
eval "$eval"
```

# GIT-FORMAT-PATCH

## 名称

`git format-patch`：为邮件提交准备补丁。

## 语法

`git format-patch` `[-k] (-o|--output-directory) <dir> | --stdout] [--no-thread | --thread[=<style>]] [(--attach|--inline)[=<boundary>] | --no-attach] [-s | --signoff] [--signature=<signature> | --no-signature] [--signature-file=<file>] [-n | --numbered | -N | --no-numbered] [--start-number <n>] [--numbered-files] [--in-reply-to=Message-Id] [--suffix=.<sfx>] [--ignore-if-upstream] [--subject-prefix=Subject-Prefix] [(--max-count|-v) <n>] [--to=<email>] [--cc=<email>] [--[no-]cover-letter] [--quiet] [--notes[=<ref>]] [<common diff options>] [ <since> | <revision range> ]`

## 描述

为每个提交准备一个补丁文件，格式类似于 UNIX 邮箱。该命令的输出便于邮件提交或配合 `git am` 使用。

有两种方法指定要操作的提交：

1. 单个提交 `<since>`，指定指向当前分支顶部但在 `<since>` 之前的提交。
2. 通用的 `<revision range>` 表达式（见 (7) 中的“指定修订版本”部分），表示指定范围内的提交。

对于单个 `<commit>`，第一条规则优先。要应用第二条规则，即格式化从历史开始到 `<commit>` 的所有内容，请使用 `--root` 选项：`git format-patch --root <commit>`。如果你只想格式化 `<commit>` 本身，可以使用 `git format-patch -1 <commit>`。

默认情况下，每个输出文件从 1 开始顺序编号，并使用提交消息的第一行（经过路径安全处理）作为文件名。使用 `--numbered-files` 选项，输出文件名将仅为数字，不附加第一行。输出文件的名称打印到标准输出，除非指定了 `--stdout` 选项。

如果指定了 `-o`，输出文件将在 `<dir>` 中创建。否则，它们将在当前工作目录中创建。

默认情况下，单个补丁的主题为 `[PATCH]`，后接从提交消息到第一个空行的内容（见 (1) 的讨论部分）。

当输出多个补丁时，主题前缀将变为 `[PATCH n/m]`。要强制为单个补丁添加 1/1，使用 `-n`。要从主题中省略补丁编号，使用 `-N`。

如果给出 `--thread`，`git format-patch` 将生成 `In-Reply-To` 和 `References` 头，使第二个及后续补丁邮件显示为第一封邮件的回复；这还会生成用于引用的 `Message-Id` 头。

### 选项

- `-p, --no-stat`

  生成不带任何差异统计的纯补丁。

- `-s, --no-patch`

  抑制差异输出。适用于默认显示补丁的 `git show` 等命令，或取消 `--patch` 的效果。

- `-U<n>, --unified=<n>`

  生成具有 `<n>` 行上下文的差异，而不是默认的三个行。

- `--minimal`

  花费额外时间以确保产生最小的差异。

- `--patience`

  使用 `patience diff` 算法生成差异。

- `--histogram`

  使用 `histogram diff` 算法生成差异。

- `--diff-algorithm={patience|minimal|histogram|myers}`

  选择一种差异算法。变体如下：

  - `default, myers`：默认，使用 myers 算法。
  - `minimal`：花费额外时间确保产生最小的差异。
  - `patience`：使用 patience 算法。
  - `histogram`：使用 histogram 算法。

  例如，当需要使用 `diff.algorithm` 默认值时，使用 `--diff-algorithm=default`。

- `--stat[=<width>[,<name-width>[,<count>]]]`

  生成差异统计（diffstats）。对于二进制文件，输出 `-` 而不是 `0`。这些参数也可以单独设置：`--stat-width`、`--name-width` 和 `--stat-count`。

- `--numstat`

  与 `--stat` 类似，但以十进制符号显示添加和删除的行数，且不缩写路径，对机器友好。对于二进制文件，输出两个 `-` 而不是 `0`。

- `--shortstat`

  仅输出 `--stat` 格式的最后一行，包含修改的文件总数，以及添加和删除的行数。

- `--dirstat[=<param1,param2,...>]`

  输出每个子目录相对变化的分布。`dirstat` 的行为可以通过传递逗号分隔的参数进行自定义。默认值由 `diff.dirstat` 配置变量控制（见 (1)）。可用参数如下：

  - `changes`：通过计算从源删除或向目标添加的行来计算 dirstat 数字。这忽略了文件内部纯代码移动。也就是说，重新排列文件的行不会被视为与其他变化相同。这是未给出参数时的默认行为。
  - `lines`：通过对常规基于行的差异分析来计算 dirstat 数字，并累加删除/添加的行数。（对于二进制文件，计算 64 字节块，因为二进制文件没有自然的行概念。）这比 `changes` 行为更耗资源，但它将文件内部重新排列行视为与其他变化相同。结果输出与其他 `--*stat` 选项一致。
  - `files`：通过计算更改文件的数量来计算 dirstat 数字。每个更改的文件在 dirstat 分析中权重相等。这是计算代价的 dirstat 行为，因为它不需要查看文件内容。
  - `cumulative`：将子目录的变化也计入父目录。注意，当使用累计时，报告的百分比总和可能会超过 100%。默认（非累计）行为可以通过非累计参数指定。

#### `<limit>`

一个整数参数指定截断百分比（默认为 3%）。更改少于此百分比的目录不会在输出中。

示例：以下命令将统计更改的文件，同时忽略更改文件总数少于 10% 的目录，并将子目录计数累计到父目录中：`--dirstat=files,10,cumulative`。

### `--summary`

输出扩展头部信息的简要摘要，例如创建、重命名和模式更改。

### `--no-renames`

关闭重命名检测，即使配置文件默认开启了它。

### `--full-index`

在生成补丁格式输出时，在 `index` 行显示完整的修改前和修改后的 blob 对象名称，而不是只显示前几个字符。

### `--binary`

除了 `--full-index` 之外，还输出可以使用 `git-apply` 应用的二进制差异。

### `--abbrev[=<n>]`

在 `diff-raw` 格式输出和 `diff-tree` 头部行中，不显示完整的 40 字节十六进制对象名称，而是仅显示部分前缀。这与上述控制 `--full-index` 的选项无关，后者控制差异-补丁输出格式。可以使用 `--abbrev=<n>` 指定非默认的位数。

### `-B[<n>][/<m>], --break-rewrites[=[<n>][/<m>]]`

将完全重写的更改分解为删除和创建对。这有两个作用：

1. 它影响对整个文件完全重写更改的处理方式，使其不再被视为一系列删除和插入（夹杂着少量在文本上匹配作为上下文的行），而是被视为一次性删除所有旧内容，然后一次性插入所有新内容。数字 `m` 控制 `-B` 选项的这一方面（默认为 60%）。`-B/70%` 指定如果原始文件中只有少于 30% 的内容剩余，Git 才会将其视为完全重写；否则，生成的补丁将是一系列夹杂了上下文行的删除和插入混合。
2. 当与 `-M` 配合使用时，完全重写的文件也会被视为重命名的源（通常 `-M` 只考虑消失的文件作为重命名的源），数字 `n` 控制 `-B` 选项的这一方面（默认为 50%）。`-B20%` 指定与文件大小相比，添加和删除达到 20% 或以上的更改有资格被选为到另一个文件的可能重命名源。

### `-M[<n>], --find-renames[=<n>]`

检测重命名。如果指定了 `n`，它是相似性索引阈值（即与文件大小相比的添加/删除量）。例如，`-M90%` 意味着如果文件超过 90% 的内容没有变化，Git 应将一个删除/添加对视为重命名。如果没有 `%` 符号，该数字被视为分数，前面带有小数点。即，`-M5` 变为 `0.5`，因此等同于 `-M50%`。同样，`-M05` 等同于 `-M5%`。要将检测限制为精确重命名，请使用 `-M100%`。默认相似性索引为 50%。

### `-C[<n>], --find-copies[=<n>]`

检测复制以及重命名。参见 `--find-copies-harder`。如果指定了 `n`，其含义与 `-M<n>` 相同。

### `--find-copies-harder`

出于性能考虑，默认情况下 `-C` 选项仅在复制的原文件在同一更改集中被修改时才查找复制。此标志使命令检查未修改的文件作为复制源的候选。对于大型项目，这是一个非常贵的操作，请谨慎使用。提供多个 `-C` 选项的效果相同。

### `-D, --irreversible-delete`

省略删除操作的镜像（preimage），即只打印头部，而不打印镜像与 `/dev/null` 之间的差异。生成的补丁并非用于通过 `patch` 或 `git apply` 应用；这仅适用于只想关注更改后文本的人。此外，输出显然缺乏足够反向应用此类补丁的信息（即使是手动），因此该选项得名。

当与 `-B` 同时使用时，也省略删除/创建对中删除部分的镜像。

### `-l<num>`

`-M` 和 `-C` 选项需要 `O(n²)` 处理时间，其中 `n` 是潜在重命名/复制目标的数量。如果重命名/复制目标超过指定的数量，此选项将防止重命名/复制检测运行。

### `-O<orderfile>`

按照 `<orderfile>` 中指定的顺序输出补丁，该文件每行一个 shell glob 模式。这会覆盖 `diff.orderFile` 配置变量（参见 (1)）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

### `-a, --text`

将所有文件视为文本。

### `--ignore-space-at-eol`

忽略行尾空格的更改。

### `-b, --ignore-space-change`

忽略空格数量的更改。这会忽略行尾空格，并将所有其他一个或多个空格序列视为等效。

### `-w, --ignore-all-space`

在比较行时忽略空格。即使一行有空格而另一行没有，也会忽略差异。

### `--ignore-blank-lines`

忽略行全为空白的更改。

### `--inter-hunk-context=<lines>`

在差异块（hunks）之间显示上下文，最多到指定的行数，从而合并彼此的块。

### `-W, --function-context`

显示更改的整个函数。

### `--ext-diff`

允许执行外部差异。如果你通过 (5) 设置了外部差异，则需要使用此选项。

### `--no-ext-diff`

禁止外部差异。

### `--textconv, --no-textconv`

在比较二进制文件时允许（或禁止）运行外部文本过滤器。详情见 (5)。因为 textconv 过滤器通常是单向转换，生成的差异适用于人类阅读，但无法应用。

### `--ignore-submodules[=<when>]`

忽略对子模块的更改。`<when>` 可以是 `"none"`、`"untracked"`、`"dirty"` 或 `"all"`，后者是默认值。使用 `"none"` 会在子模块包含未跟踪内容时将其视为已修改（但仍对其修改内容进行扫描）。使用 `"dirty"` 会忽略所有对子模块的更改。使用 `"untracked"` 在子模块仅包含未跟踪内容时将其视为未修改（这是 1.7.0 之前的行为）。使用 `"all"` 会隐藏所有对子模块的更改。

### `--src-prefix=<prefix>`

显示指定的源前缀代替 `a/`。

### `--dst-prefix=<prefix>`

显示指定的目的前缀代替 `b/`。

### `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的更多详细解释，请参见 (7)。

### `-<n>`

从顶部的 `<n>` 个提交准备补丁。

### `-o <dir>, --output-directory <dir>`

使用 `<dir>` 存储结果文件，而不是当前工作目录。

### `-n, --numbered`

以 `[PATCH n/m]` 格式命名输出，即使只有一个补丁也是如此。

### `-N, --no-numbered`

以 `[PATCH]` 格式命名输出。

### `--start-number <n>`

从 `<n>` 开始为补丁编号，而不是从 1 开始。

### `--numbered-files`

输出的文件名将是数字序列，不附加默认的提交第一行。

### `-k, --keep-subject`

不在提交日志消息的第一行中剥离或添加 `[PATCH]`。

### `-s, --signoff`

在提交消息中添加 `Signed-off-by:` 行，使用你自己的提交者身份。

### `--stdout`

以 mbox 格式将所有提交打印到标准输出，而不是为每个提交创建一个文件。

### `--attach[=<boundary>]`

创建 multipart/mixed 附件，第一部分是提交消息，第二部分是补丁本身，并带有 `Content-Disposition: attachment`。

### `--no-attach`

禁用创建附件，覆盖配置设置。

### `--inline[=<boundary>]`

创建一个 multipart/mixed 附件，其第一部分是提交信息，第二部分是补丁本身，且第二部分带有 `Content-Disposition: inline`。

### `--thread[=<style>], --no-thread`

控制是否在邮件中添加 `In-Reply-To` 和 `References` 请求头，使第二封及后续邮件显示为对第一封邮件的回复。同时也控制用于引用的 `Message-Id` 请求头的生成。

可选的 `<style>` 参数可以是 `shallow` 或 `deep`。`shallow`（浅线程）使每封邮件都成为系列头部的回复，头部根据顺序从第一封信（cover letter）、`--in-reply-to` 和第一封补丁邮件中选择。`deep`（深度线程）使每封邮件都成为前一封邮件的回复。

默认值为 `--no-thread`，除非设置了 `format.thread` 配置。如果指定了 `--thread` 但未指定样式，则默认使用 `format.thread` 指定的样式（如果有），否则默认为 `shallow`。

注意，`git send-email` 的默认设置是对邮件本身进行线程处理。如果你想让 `git format-patch` 来处理线程化，则需要确保 `git send-email` 禁用了线程处理。

### `--in-reply-to=Message-Id`

使第一封邮件（或所有带有 `--no-thread` 的邮件）显示为对给定 `Message-Id` 的回复，从而避免为了提供新的补丁系列而破坏线程。

### `--ignore-if-in-upstream`

不包含匹配 `<until>..<since>` 中提交的补丁。这将检查所有从 `<since>` 可达但从 `<until>` 不可见的补丁，并将其与生成的补丁进行比较，任何匹配的补丁将被忽略。

### `--subject-prefix=<Subject-Prefix>`

主题行不再使用标准的 `[PATCH]` 前缀，而是使用 `[<Subject-Prefix>]`。这允许对补丁系列进行命名，并可以与 `--numbered` 选项结合使用。

### `-v <n>, --reroll-count=<n>`

将系列标记为主题的第 `<n>` 次迭代。输出文件名将加上 `v<n>`，主题前缀（默认是 `"PATCH"`，但可以通过 `--subject-prefix` 配置）末尾将加上 ` v<n>`。例如，`--reroll-count=4` 可能会产生 `v4-0001-add-makefile.patch` 文件，其内容为 `Subject: [PATCH v4 1/20] Add makefile`。

### `--to=<email>`

在邮件头中添加 `To:` 请求头。这是在任何已配置头之外额外添加的，可以使用多次。否定形式 `--no-to` 会丢弃所有已添加的（来自配置或命令行）`To:` 请求头。

### `--cc=<email>`

在邮件头中添加 `Cc:` 请求头。这是在任何已配置头之外添加的，可以使用多次。否定形式 `--no-cc` 会丢弃所有已添加的（来自配置或命令行）`Cc:` 请求头。

### `--from, --from=<ident>`

在每封提交邮件的 `From:` 请求头中使用 `ident`。如果提交的作者标识与提供的 `ident` 在文本上不完全一致，则在消息正文中放置一个带有原始作者的 `From:` 请求头。如果没有给出 `ident`，则使用提交者的 `ident`。

请注意，此选项仅当你实际上在发送邮件并希望将自己标识为发送者，但保留原始作者时有效（`git am` 会正确获取正文中的头）。同样注意，`git send-email` 已经为你处理了这种转换，如果你将结果传递给 `git send-email`，则不应使用此选项。

### `--add-header=<header>`

在邮件头中添加任意请求头。这是在任何已配置头之外添加的，可以使用多次。例如，`--add-header="Organization: git-foo"`。否定形式 `--no-add-header` 会丢弃所有从配置或命令行添加的（`To:`、`Cc:` 和自定义）请求头。

### `--[no-]cover-letter`

除了补丁外，还会生成一个包含 shortlog 和整体 diffstat 的封信（cover letter）文件。你可以在发送之前在文件中填写描述。

### `--notes[=<ref>]`

在三个连字符线之后为提交添加注释（参见第 (1) 节）。

此选项预期的用例是为提交编写不属于提交日志正文的辅助说明，并将其随补丁一起提交。虽然人们可以在运行 `format-patch` 之后但在发送之前简单编写这些说明，但将其保留为 Git notes 允许在补丁序列的版本之间进行维护（请参见 (1) 中关于 `notes.rewrite` 配置选项的讨论以使用此工作流）。

### `--[no-]signature=<signature>`

为生成的每条消息添加签名。根据 RFC 3676，签名与正文通过一行 `-- ` 行分隔。如果省略签名选项，签名默认为 Git 版本号。

### `--signature-file=<file>`

工作方式与 `--signature` 相同，但签名是从文件中读取的。

### `--suffix=.<sfx>`

不再使用 `.patch` 作为生成文件的后缀，而是使用指定的后缀。常见的替代方案是 `--suffix=.txt`。留空将移除 `.patch` 后缀。

注意，起始字符不必是点；例如，你可以使用 `--suffix=-patch` 来获得 `0001-description-of-my-change-patch`。

### `-q, --quiet`

不向标准输出打印生成文件的文件名。

### `--no-binary`

不输出二进制文件的更改内容，而是显示一条这些文件已更改的通知。使用此选项生成的补丁无法正确应用，但它们对于代码审查仍然很有用。

### `--root`

将修订参数视为 `<revision range>`，即使它只是单个提交（这通常会被视为 `<since>`）。注意，包含在指定范围内的根提交始终被格式化为创建补丁，与此标志无关。

## 配置（CONFIGURATION）

你可以通过配置变量指定要添加到每条消息的额外邮件头行、主题前缀和文件后缀的默认值、输出多个补丁时的补丁数量、添加 `To` 或 `Cc:` 请求头、配置附件以及对补丁进行签名（sign off）。

```ini
```




```text
[format] headers = "Organization: git-foo\n" subjectPrefix = CHANGE suffix = .txt numbered = auto to = <email> cc = <email> attach [ = mime-boundary-string ] signOff = true coverletter = auto
```

## 或（DISCUSSION）

`git format-patch` 产生的补丁采用 UNIX 邮箱格式，并带有固定的“魔法”时间戳，指示该文件是由 `format-patch` 输出而非真实的邮箱，如下所示：

```text
From 8f72bad1baf19a53459661343e21d6491c3908d3 Mon Sep 17 00:00:00 2001
From: Tony Luck <>
Date: Tue, 13 Jul 2010 11:42:54 -0700
Subject: [PATCH] =?UTF-8?q?[IA64]=20Put=20ia64=20config=20files=20on=20the=20?=
 =?UTF-8?q?Uwe=20Kleine-K=C3=B6nig=20diet?=
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 8bit

arch/arm config files were slimmed down using a python script (See commit c2330e286f68f1c408b4aa6515ba49d57f05beae comment)

Do the same for ia64 so we can have sleek & looking ...
```

通常它会被放置在 MUA 的草稿文件夹中，经过编辑以添加不应进入三个连字符之后日志的及时注释，然后作为消息发送。在示例中，其正文从“arch/arm config files were...”开始。在接收端，读者可以将有趣的补丁保存到 UNIX 邮箱并用 `git am` 进行应用。

当补丁是正在讨论的一部分时，`git format-patch` 产生的补丁可以进行调整以利用 `git am --scissors` 功能。在对讨论的回复之后有一行由 `-- >8 --`（剪刀和穿孔）组成，随后是删除了不需要头部字段的补丁：

```text
... So we should do such-and-such. Makes sense to me. How about this patch?
-- >8 --
Subject: [IA64] Put ia64 config files on the Uwe Kleine-König diet

arch/arm config files were slimmed down using a python script ...
```

以这种方式发送补丁时，通常情况下你正在发送你自己的补丁，因此除了 `From $SHA1 $magic_timestamp` 标记外，你应该从补丁文件中省略 `From:` 和 `Date:` 行。补丁标题可能与该补丁所响应的讨论主题不同，因此你很可能想要保留 `Subject:` 行，如上面的示例所示。

## 检查补丁损坏

许多邮件处理程序如果配置不当，会损坏空白字符。这里是两种常见的损坏类型：

1. 不包含任何空白的空上下文行。
2. 开头多了一个空白字符的非空上下文行。

测试你的 MUA（邮件用户代理）是否配置正确的一种方法是：

- 将补丁发送给自己，发送方式与平时完全一样，但 `To:` 和 `Cc:` 行不包含列表和维护者地址。
- 将该补丁保存为 UNIX 邮箱格式的文件。假设将其命名为 `a.patch`。
- 应用它：

```bash
$ git fetch <project> master:test-apply
$ git checkout test-apply
$ git reset --hard
$ git am a.patch
```

如果无法正确应用，可能有多种原因：

- 补丁本身无法顺利应用。也就是说补丁是 `bad` 的，但这与你的 MUA 无关。在这种情况下，你可能需要在重新生成补丁之前使用 `git rebase` 进行 rebase。
- MUA 损坏了你的补丁；`am` 会报错补丁无法应用。查看 `.git/rebase-apply/` 子目录，检查 `patch` 文件包含的内容，并检查上述提到的常见损坏模式。
- 顺便也检查 `info` 和 `final-commit` 文件。如果 `final-commit` 中的内容不是你想要在提交日志消息中看到的内容，那么接收者在应用你的补丁时很可能会手动编辑日志消息。补丁邮件中类似 `"Hi, this is my first patch.\n"` 的内容应该出现在信号提交消息结束的三连横线之后。

## 针对 MUA 的提示

以下是一些关于如何使用各种邮件处理程序成功内联提交补丁的提示。

### GMail

GMail 网页界面中没有关闭换行的方法，因此它会破坏你发送的任何邮件。不过，你可以使用 `git send-email` 通过 GMail SMTP 服务器发送你的补丁，或者使用任何 IMAP 邮件客户端连接到 Google IMAP 服务器并通过它转发邮件。

有关如何使用 `git send-email` 通过 GMail SMTP 服务器发送补丁的提示，请参阅 `git send-email(1)` 的 EXAMPLE 部分。

有关使用 IMAP 接口提交的提示，请参阅 `git imap-send(1)` 的 EXAMPLE 部分。

### Thunderbird

默认情况下，Thunderbird 会对邮件进行换行并将其标记为 `format=flowed`，这两者会导致生成的邮件无法被 Git 使用。

有三种方法：使用插件关闭换行、配置 Thunderbird 不损坏补丁，或使用外部编辑器防止 Thunderbird 损坏补丁。

#### 方法 #1（插件）

从 `m[]` 安装 `Toggle Word Wrap` 插件。它会在撰写器的“选项（Options）”菜单中添加一个“Enable Word Wrap”菜单项，你可以取消勾选它。现在你可以像往常一样撰写消息（剪贴、粘贴、`git format-patch`、`git imap-send` 等），但你必须在输入的任何文本中手动插入换行符。

#### 方法 #2（配置）

三个步骤：

1. 将你的邮件服务器撰写配置为纯文本：编辑“账户设置”→“撰写与地址”，取消勾选“使用 HTML 格式撰写消息”。
2. 配置通用撰写窗口不换行。
   - 在 Thunderbird 2 中：`Edit..Preferences..Composition`，将纯文本消息换行设为 `0`。
   - 在 Thunderbird 3 中：`Edit..Preferences..Advanced..Config Editor`。搜索 `mail.wrap_long_lines`，切换确保其设置为 `false`。同样搜索 `mailnews.wraplength` 并将值设置为 `0`。
3. 禁用 `format=flowed` 的使用：`Edit..Preferences..Advanced..Config Editor`。搜索 `mailnews.send_plaintext_flowed`，切换确保其设置为 `false`。

完成这些后，你应该能够像往常一样撰写邮件（剪贴、粘贴、`git format-patch`、`git imap-send` 等），且补丁不会被损坏。

#### 方法 #3（外部编辑器）

需要以下 Thunderbird 扩展：来自 `m[]` 的 `AboutConfig` 和来自 `&pg=8m[]` 的 `External Editor`。

1. 使用你选择的方法将补丁准备为文本文件。
2. 在打开撰写窗口之前，使用 `Edit→Account Settings` 取消用于发送补丁的账户“撰写与地址”面板中的“使用 HTML 格式撰写消息”设置。
3. 在 Thunderbird 主窗口中，在打开补丁的撰写窗口之前，使用 `Tools→about:config` 将以下项设置为指定值：

```text
mailnews.send_plaintext_flowed => false
mailnews.wraplength => 0
```

4. 打开撰写窗口并点击外部编辑器图标。
5. 在外部编辑器窗口中读取补丁文件并正常退出编辑器。

旁注：可能可以通过 `about:config` 和以下设置完成步骤 2，但还没有人尝试过。

```text
mail.html_compose => false
mail.identity.default.compose_html => false
mail.identity.id?.compose_html => false
```

`contrib/thunderbird-patch-inline` 中有一个脚本，可以帮助你轻松地在 Thunderbird 中包含补丁。要使用它，请按照上述步骤操作，然后将该脚本作为外部编辑器使用。

### KMail

这可以帮助你使用 KMail 内联提交补丁。

1. 将补丁准备为文本文件。
2. 点击“新邮件（New Mail）”。
3. 进入撰写窗口的“选项（Options）”，并确保没有设置“换行（Word wrap）”。
4. 使用 `Message → Insert file...` 并插入补丁。
5. 回到撰写窗口：在消息中添加你需要的任何其他文本，完成地址和主题字段，并发送。

## 示例

提取版本 R1 和 R2 之间的提交，并使用 `git am` 将它们应用到当前分支上以进行 cherry-pick：

```bash
$ git format-patch -k --stdout R1..R2 | git am -3 -k
```

提取在当前分支中但不在 origin 分支中的所有提交：

```bash
$ git format-patch origin
```

为每个提交在当前目录下创建一个单独的文件。

提取自项目启动以来通向 `origin` 的所有提交：

```bash
$ git format-patch --root origin
```

与上一个相同：

```bash
$ git format-patch -M -B origin
```

此外，它会智能地检测并处理重命名和完全重写以生成重命名补丁。重命名补丁减少了文本输出量，并通常更容易审查。注意，非 Git 的“补丁”程序无法理解重命名补丁，因此仅在你确定对方使用 Git 应用补丁时才使用它。

从当前分支提取三个顶端提交并将其格式化为可发送邮件的补丁：

```bash
$ git format-patch -3
```

## 参见

`git am(1)`、`git send-email(1)`

---

# GIT-FSCK-OBJECTS

## 名称

`git-fsck-objects` - 验证数据库对象的连接性和有效性

## 摘要

`git fsck-objects ...`

## 描述

这是 `git-fsck(1)` 的同义词。请参考该命令的文档。

---

# GIT-FSCK

## 名称

`git-fsck` - 验证数据库对象的连接性和有效性

## 摘要

`git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs] [--[no-]full] [--strict] [--verbose] [--lost-found] [--[no-]dangling] [--[no-]progress] [<object>...]`

## 描述

验证数据库对象的连接性和有效性。

### 选项

#### `<object>`

一个被视为不可达性追踪头部的对象。如果没有给出任何对象，`git fsck` 默认使用索引文件、refs 空间中的所有 SHA-1 引用以及所有 reflog（除非给了 `--no-reflogs`）作为头部。

#### `--[no-]dangling`

打印存在但从未被直接使用的对象（默认）。可以使用 `--no-dangling` 从输出中省略此类信息。

#### `--root`

报告根节点。

#### `--tags`

报告标签。

#### `--cache`

将索引中记录的任何对象也视为不可达性追踪的头节点（head node）。

#### `--no-reflogs`

不要将仅由 reflog 条目引用的提交视为可达。此选项仅用于搜索曾经存在于 ref 中但现在不存在、仍存在于对应 reflog 中的提交。

#### `--full`

不仅检查 `GIT_OBJECT_DIRECTORY`（`$GIT_DIR/objects`）中的对象，还检查在 `GIT_ALTERNATE_OBJECT_DIRECTORIES` 列出的备用对象池或 `$GIT_DIR/objects/info/alternates` 中的对象，以及在 `$GIT_DIR/objects/pack` 中找到的压缩包 Git 存档和备用对象池相应的包子目录中的对象。这现在是默认设置；可以通过 `--no-full` 关闭。

#### `--strict`

启用更严格的检查，即捕获由旧版本 Git 创建的带有 g+w 位的文件模式。现有的仓库（包括 Linux 内核、Git 自身和稀疏仓库）包含触发此检查的旧对象，但建议使用此标记对新项目进行检查。

#### `--verbose`

详细模式。

#### `--lost-found`

将悬空对象（dangling objects）写入 `.git/lost-found/commit/` 或 `.git/lost-found/other/`，取决于类型。如果对象是 blob，则内容被写入文件，而不是其对象名称。

#### `--[no-]progress`

当标准错误流附加到终端时，默认在标准错误流上报告进度状态，除非指定了 `--no-progress` 或 `--verbose`。`--progress` 即使标准错误流未重定向到终端也会强制报告进度状态。

## 讨论

`git-fsck` 测试 SHA-1 和通用对象的完整性，并对生成的可达性及其他一切进行完整跟踪。它会打印出发现的任何损坏（丢失或错误的对象），如果你使用 `--unreachable` 标记，它还会打印出存在但无法从任何指定的头节点（或上述的默认 set）到达的对象。

任何损坏的对象都必须在备份或其他存档中找到（即：你可以直接删除它们并与其他站点进行 `rsync`，希望别人拥有你所损坏的对象）。

## 提取的诊断信息

`expect dangling commits - potential heads - due to lack of head information`

你没有指定任何节点作为头节点，因此无法区分无父节点的提交和根节点。

`missing sha1 directory <dir>`

存放 SHA-1 对象的目录丢失。

`unreachable <type> <object>`

`<type>` 对象 `<object>` 实际上未在看到的任何树或提交中被直接或间接地引用。这可能意味着存在另一个你未指定的根节点，或者树损坏了。如果你没有漏掉根节点，那么大可以删除这些不可达节点，因为它们是无法使用的。

`missing <type> <object>`

`<type>` 对象 `<object>` 被引用，但在数据库中不存在。

`dangling <type> <object>`

`<type>` 对象 `<object>` 存在于数据库中，但从未被直接使用。悬空提交可能是一个根节点。

`sha1 mismatch <object>`

数据库中的对象 SHA-1 与数据库值不匹配。这表明存在严重的数据完整性问题。

## 环境变量

`GIT_OBJECT_DIRECTORY`

用于指定对象数据库根目录（通常为 `$GIT_DIR/objects`）。

`GIT_INDEX_FILE`

用于指定索引的索引文件。

`GIT_ALTERNATE_OBJECT_DIRECTORIES`

用于指定额外的对象数据库根目录（通常未设置）。

---

# GIT-GC

## 名称

`git-gc` - 清理不需要的文件并优化本地仓库

## 概要

`git gc [--aggressive] [--auto] [--quiet] [--prune=<date> | --no-prune] [--force]`

## 描述

在当前仓库中运行若干项清理任务，例如压缩文件版本（以减少磁盘空间并提高性能）以及删除从之前的调用 `git add` 可能创建的不可达对象。

鼓励用户在每个仓库中定期运行此任务，以保持良好的磁盘空间利用率和运行性能。

某些 Git 命令可能会自动运行 `git gc`；详情请参阅下方的 `--auto` 标记。如果你清楚自己在做什么，并且只是想永久禁用此行为而不考虑其他因素，只需执行：

```bash
$ git config --global gc.auto 0
```



### 选项

`--aggressive`

通常 `git gc` 运行非常快，同时提供良好的磁盘空间利用率和性能。此选项将导致 `git gc` 更积极地优化仓库，代价是花费更多时间。这种优化的效果是持久的，因此此选项只需要偶尔使用；大约每几百个提交使用一次。

`--auto`

使用此选项，`git gc` 会检查是否需要进行清理；如果没有，将在不执行任何工作的情况下退出。某些 git 命令在执行可能创建许多松对象的操作后会运行 `git gc --auto`。

如果仓库中有过多的松对象或过多的包（packs），则需要清理。如果松对象的数量超过 `gc.auto` 配置变量的值，则将使用 `git repack -d -l` 将所有松对象合并为一个包。将 `gc.auto` 的值设为 0 将禁用松对象的自动打包。

如果包的数量超过 `gc.autoPackLimit` 的值，则现有包（被 `.keep` 文件标记的除外）将使用 `git repack` 的 `-A` 选项合并为一个包。将 `gc.autoPackLimit` 设置为 0 将禁用包的自动合并。

`--prune=<date>`

修剪早于日期的松对象（默认两周前，可以通过配置变量 `gc.pruneExpire` 覆盖）。`--prune=all` 无论年龄均修剪松对象。`--prune` 默认开启。

`--no-prune`

不修剪任何松对象。

`--quiet`

抑制所有进度报告。

`--force`

强制运行 `git gc`，即使该仓库上可能正在运行另一个 `git gc` 实例。

### 配置

可选的配置变量 `gc.reflogExpire` 可以设置，以指示每个分支 reflog 中的历史条目在仓库中保留多久。该设置表示为时间长度，例如 `90 days` 或 `3 months`。默认值为 `90 days`。

可选的配置变量 `gc.reflogExpireUnreachable` 可以设置，以指示不属于当前分支的历史 reflog 条目在仓库中保留多久。这些类型的条目通常由于使用 `git commit --amend` 或 `git rebase` 而产生，是发生 amend 或 rebase 之前的提交。由于这些更改不是当前项目的一部分，大多数用户会希望更早让它们过期。此选项默认值为 `30 days`。

上述两个配置变量可以赋予一个模式。例如，这仅为远程跟踪分支设置非默认的过期值：

```
[gc "refs/remotes/*"]
reflogExpire = never
reflogExpireUnreachable = 3 days
```

可选的配置变量 `gc.rerereResolved` 指明你之前解决的冲突合并记录保留多久。默认为 60 天。

可选的配置变量 `gc.rerereUnresolved` 指明未解决的冲突合并记录保留多久。默认为 15 天。

可选的配置变量 `gc.packRefs` 决定 `git gc` 是否运行 `git pack-refs`。可以被设置为 `"notbare"` 以在所有非裸仓库中启用，或者可以设置为布尔值。默认值为 `true`。

可选的配置变量 `gc.aggressiveWindow` 控制在指定 `--aggressive` 选项时，用于优化仓库中对象增量压缩（delta compression）的时间。该值越大，用于优化增量压缩的时间就越长。更多细节请参阅 (1) 中 `--window` 选项的文档。默认值为 250。

同样，可选的配置变量 `gc.aggressiveDepth` 控制 (1) 中的 `--depth` 选项。默认值为 250。

可选的配置变量 `gc.pruneExpire` 控制未引用的松散对象（loose objects）在被清理之前需要有多旧。默认是“2 周前”。

### 注意事项

`git gc` 会非常努力确保其收集的垃圾操作是安全的。特别是，它不仅会保留当前分支和标签引用的对象，还会保留索引（index）、远程跟踪分支、由 `git filter-branch` 保存在 `refs/original/` 中的引用，或引用日志（reflogs）（这些引用日志可能引用了之后被修改或回滚的分支中的提交）。

如果你期望某些对象被回收但它们没有被回收，请检查所有这些位置，并决定在你的情况下删除这些引用是否合理。

### 钩子

`git gc --auto` 命令将运行 `pre-auto-gc` 钩子。更多信息请见 (5)。

### 另

(1) (1) (1) (1)

---

# Git-get-tar-commit-id

## 名称

git-get-tar-commit-id - 从使用 git-archive 创建的归档中提取 commit ID

## 概要

```
git get-tar-commit-id < <tarfile>
```

## 描述

作为一个过滤器使用，提取由 `git archive` 创建的归档中存储的 commit ID。它只读取输入的前 1024 字节，因此运行时间不受 `<tarfile>` 大小的影响。

如果没有找到 commit ID，`git get-tar-commit-id` 将静默退出并返回状态码 1。这可能发生在 `<tarfile>` 不是使用 `git archive` 创建的，或者 `git archive` 的第一个参数是树 ID 而不是 commit ID 或标签的情况下。

---

# GIT-GREP

## 名称

git-grep - 打印匹配模式的行

## 概要

```
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp] [-v | --invert-match] [-h|-H] [--full-name] [-E | --extended-regexp] [-G | --basic-regexp] [-P | --perl-regexp] [-F | --fixed-strings] [-n | --line-number] [-l | --files-with-matches] [-L | --files-without-match] [(-O | --open-files-in-pager) [<pager>]] [-z | --null] [-c | --count] [--all-match] [-q | --quiet] [--max-depth <depth>] [--color[=<when>] | --no-color] [--break] [--heading] [-p | --show-function] [-A <post-context>] [-B <pre-context>] [-C <context>] [-W | --function-context] [-f <file>] [-e] <pattern> [--and|--or|--not|(|)|-e <pattern>...] [ [--[no-]exclude-standard] [--cached | --no-index | --untracked] | <tree>...] [--] [<pathspec>...]
```

## 描述

在工作树中的跟踪文件、索引文件中注册的 blob 或给定树对象中的 blob 中查找指定的模式。模式是按换行符分隔的一个或多个搜索表达式的列表。空字符串作为搜索表达式将匹配所有行。

## 配置

`grep.lineNumber`

如果设置为 true，则默认启用 `-n` 选项。

`grep.patternType`

设置默认匹配行为。使用 `basic`、`extended`、`fixed` 或 `perl` 值将分别启用 `--basic-regexp`、`--extended-regexp`、`--fixed-strings` 或 `--perl-regexp` 选项，而值 `default` 将返回默认匹配行为。

`grep.extendedRegexp`

如果设置为 true，则默认启用 `--extended-regexp` 选项。当 `grep.patternType` 选项设置为非 `default` 时，此选项会被忽略。

`grep.fullName`

如果设置为 true，则默认启用 `--full-name` 选项。

### 选项

`--cached`

不再搜索工作树中的跟踪文件，而是搜索索引文件中注册的 blob。

`--no-index`

搜索当前目录中未由 Git 管理的文件。

`--untracked`

在搜索工作树中的跟踪文件之外，也搜索未跟踪的文件。

`--no-exclude-standard`

通过不遵守 `.gitignore` 机制来搜索被忽略的文件。仅在配合 `--untracked` 时有用。

`--exclude-standard`

不忽略通过 `.gitignore` 机制指定的忽略文件。仅在配合 `--no-index` 搜索当前目录下的文件时有用。

`-a, --text`

将二进制文件当做文本处理。

`--textconv`

尊重 textconv 过滤器设置。

`--no-textconv`

不尊重 textconv 过滤器设置。这是默认设置。

`-i, --ignore-case`

忽略模式与文件之间的大小写差异。

`-I`

不在二进制文件中匹配模式。

`--max-depth <depth>`

对于命令行上给出的每个 `<pathspec>`，最多进入 `<depth>` 级目录。负值表示无限制。如果 `<pathspec>` 包含活动通配符，则此选项会被忽略。换句话说，如果 `"a*"` 匹配名为 `"a*"` 的目录，则 `"*"` 被字面匹配，因此 `--max-depth` 仍然有效。

`-w, --word-regexp`

仅在单词边界匹配模式（要么在行首，或前面是非单词字符；要么在行尾，或后面是非单词字符）。

`-v, --invert-match`

选择不匹配的行。

`-h, -H`

默认情况下，命令显示每个匹配项的文件。`-h` 选项用于抑制此输出。`-H` 是为了完整性存在的，除了覆盖命令行早给出的 `-h` 之外不起任何作用。

`--full-name`

从子目录运行时，命令通常输出相对于当前目录的路径。此选项强制相对于项目根目录输出路径。

`-E, --extended-regexp, -G, --basic-regexp`

对模式使用 POSIX 扩展/基础正则表达式。默认使用基础正则表达式。

`-P, --perl-regexp`

对模式使用 Perl 兼容的正则表达式。需要编译了 libpcre。

`-F, --fixed-strings`

对模式使用固定字符串（不将模式解释为正则表达式）。

`-n, --line-number`

在匹配的行前加上行号。

`-l, --files-with-matches, --name-only, -L, --files-without-match`

不再显示每个匹配行，而是只显示包含（或不包含）匹配项的文件名。为了与 `git diff` 兼容，`--name-only` 是 `--files-with-matches` 的同义词。

`-O [<pager>], --open-files-in-pager`

在分页器中打开匹配的文件（而不是 `grep` 的输出）。如果分页器恰好是 `"less"` 或 `"vi"`，且用户指定了一个模式，则第一个文件会自动定位到第一个匹配处。

`-z, --null`

输出 `\0` 代替通常跟随文件名后的字符。

`-c, --count`

不再显示每个匹配行，而是显示匹配的行数。

`--color[=<when>]`

显示彩色匹配项。值必须是 `always`（默认）、`never` 或 `auto`。

`--no-color`

关闭匹配高亮，即使配置文件为颜色输出提供了默认值。同于 `--color=never`。

`--break`

在不同文件的匹配项之间打印一个空行。

`--heading`

在该文件的匹配项上方显示文件名，而不是在每个显示行的开头显示。

`-p, --show-function`

显示包含匹配项函数名的上一行，除非匹配行本身就是函数名。该名称的确定方式与 *git diff* 计算补丁块头部的方式相同（见 (5) 中的 *定义自定义块头部*）。

`<num>, -C <num>, --context <num>`

显示 `<num>` 行前行和行尾行，并在连续的匹配组之间放置一行包含 `--` 的行。

`-A <num>, --after-context <num>`

显示 `<num>` 行尾行，并在连续的匹配组之间放置一行包含 `--` 的行。

`-B <num>, --before-context <num>`

显示 `<num>` 行前行，并在连续的匹配组之间放置一行包含 `--` 的行。

`-W, --function-context`

显示上一行中包含函数名的周围文本，直到下一个函数名之前的内容，实际上显示了找到匹配项的整个函数。

`-f <file>`

从 `<file>` 读取模式，每行一个。

`-e`

下一个参数是模式。此选项必须用于以 `-` 开头的模式，并应在将用户输入传递给 `grep` 的脚本中使用。多个模式通过 `*or`（或关系）组合。

`--and, --or, --not, ( ... )`

使用布尔表达式指定多个模式的组合方式。`--or` 是默认操作符。`--and` 的优先级高于 `--or`。所有模式都必须使用 `-e`。

`--all-match`

在提供使用 `--or` 组合的多个模式表达式时，指定此标志以限制匹配范围为那些包含匹配所有模式行的文件。

`-q, --quiet`

不输出匹配的行；相反，在存在匹配时以状态 0 退出，在不存在时以非零状态退出。

`<tree>...`

不再搜索工作树中被跟踪的文件，而是搜索给定树对象（trees）中的 blob 对象。

`--`

标志选项的结束；其余参数是 `<pathspec>` 限制符。

`<pathspec>...`

如果给出，则将搜索限制为匹配至少一个模式的路径。支持领先路径匹配和 `(7)` 模式。

### 示例

```bash
git grep 'time_t' -- '*.[ch]'
```

在工作目录及其子目录下所有被跟踪的 `.c` 和 `.h` 文件中查找 `time_t`。

```bash
git grep -e '#define' --and \( -e MAX_PATH -e PATH_MAX \)
```

查找包含 `#define` 以及包含 `MAX_PATH` 或 `PATH_MAX` 的行。

```bash
git grep --all-match -e NODE -e Unexpected
```



在同时包含这两个模式行的文件中，查找包含`NODE`或`Unexpected`的行。

---

# GIT-HASH-OBJECT

## 名字

`git-hash-object` - 计算对象 ID，并可选地从文件创建 blob

## 摘要

```
git hash-object [-t <type>] [-w] [--path=<file>|--no-filters] [--stdin [--literally]] [--] <file>...
git hash-object [-t <type>] [-w] --stdin-paths [--no-filters] < <list-of-paths>
```

## 描述

根据指定类型通过命名文件的内容（可以在工作树外）计算对象的 ID 值，并可选地将结果对象写入对象数据库。将其对象 ID 报告到标准输出。这被`git cvsimport`用于在不修改工作树中文件的情况下更新索引。当未指定`<type>`时，默认为“blob”。

## 选项

`-t <type>`：指定类型（默认: “blob”）。

`-w`：实际上将对象写入对象数据库。

`--stdin`：从标准输入而不是从文件读取对象。

`--stdin-paths`：从标准输入而不是从命令行读取文件名。

`--path`：假定对象位于给定路径处并对其进行哈希。文件位置不直接影响哈希值，但路径用于确定在对象放入对象数据库之前应该应用哪些 Git 过滤器，作为应用过滤的结果，放入对象数据库的实际 blob 可能与给定文件不同。此选项主要用于哈希位于工作区外的临时文件或从标准输入读取的文件。

`--no-filters`：按原样哈希内容，忽略属性机制可能选择的任何输入过滤器，包括换行符转换。如果文件是从标准输入读取的，则始终隐含这一点，除非给了`--path`选项。

`--literally`：允许`--stdin`将任何垃圾数据哈希到松散对象中，否则可能无法通过标准对象解析或`git-fsck`检查。适用于 Git 本身的压力测试或复现在环境中遇到的损坏或伪造对象的特性。

---

# GIT-HELP

## 名字

`git-help` - 显示关于 Git 的帮助信息

## 摘要

```
git help [-a|--all] [-g|--guide] [-i|--info|-m|--man|-w|--web] [COMMAND|GUIDE]
```

## 描述

在没有提供选项且没有`COMMAND`或`GUIDE`的情况下，标准输出将打印`git`命令的摘要和最常用的 Git 命令列表。

如果给出了选项`--all`或`-a`，则在标准输出打印所有可用命令。

如果给出了选项`--guide`或`-g`，则在标准输出打印实用的 Git 指南列表。

如果给出了命令或指南，将打开该命令或指南的帮助页。默认使用`man`程序实现此目的，但可以通过其他选项或配置变量覆盖它。

注意`git --help ...`与`git help ...`相同，因为前者在内部被转换为后者。

要显示 (1) 帮助页，请使用`git help git`。

可以使用`git help help`或`git help --help`显示此页面。

### 选项

`-a, --all`：在标准输出打印所有可用命令。此选项会覆盖任何给定的命令或指南名称。

`-g, --guides`：在标准输出打印有用指南列表。此选项会覆盖任何给定的命令或指南名称。

`-i, --info`：以`info`格式显示命令的帮助页。该目的将使用`info`程序。

`-m, --man`：以`man`格式显示命令的帮助页。此选项可用于覆盖`help.format`中设置的值。默认将使用`man`程序显示帮助页，但`man.viewer`配置变量可能会选择其他程序。

`-w, --web`：以网络 HTML 格式显示命令的帮助页。将使用网络浏览器。可以使用配置变量`help.browser`指定网络浏览器。如果未设置，将选择默认值。关于更多信息请见 (1)。

## 配置变量

### help.format

如果没有传递命令行选项，将检查`help.format`配置变量。支持以下值；使`git help`对应相应的选项：

- “man”对应`-m|--man`，
- “info”对应`-i|--info`，
- “web”或“html”对应`-w|--web`。

### help.browser, web.browser and browser.<tool>.path

当选择`web`格式时（通过命令行选项或配置变量），还将检查`help.browser`、`web.browser`和`browser.<tool>.path`。见选项中的`-w`。

### man.viewer

当选择`man`格式时，将检查`man.viewer`配置变量。目前支持以下值：

- “man”: 像往常一样`man`程序，
- “woman”: 使用`emacsclient`启动“woman”模式（这从 emacsclient 22 版本开始可用），
- “konqueror”: 使用`kfmclient`在新的 konqueror 标签中打开帮助页（见下文 *关于 konqueror 的注意*）。

如果有相应的`man.<tool>.cmd`配置项，可以使用其他工具的值（见下文）。

`man.viewer`可以给出多个值。将按照配置文件中列出的顺序尝试相应的程序。

例如，此配置：

```
[man]
viewer = konqueror
viewer = woman
```

将先尝试 konqueror。但可能会失败（例如，未设置 DISPLAY），在这种情况下将尝试 emacs 的 woman 模式。

如果所有尝试失败或未配置查看器，将尝试环境变量`GIT_MAN_VIEWER`中指定的查看器。如果也失败，将仍然尝试`man`程序。

### man.<tool>.path

可以通过设置配置变量`man.<tool>.path`显式提供首选查看器的完整路径。例如，可以通过设置`man.konqueror.path`来配置 konqueror 的绝对路径。否则，`git help`假设该工具在 PATH 中。

### man.<tool>.cmd

当`man.viewer`配置变量指定的 man 视器不在支持的列表内时，将查找对应的`man.<tool>.cmd`配置变量。如果该变量存在，则指定的工具将被视为自定义命令，并将使用 shell eval 来运行该命令，同时将 man 页面作为参数传递。

### 关于 konqueror 的说明

当在`man.viewer`配置变量中指定`konqueror`时，我们会启动`kfmclient`，尝试尽可能在已打开的 konqueror 的新标签页中打开 man 页面。

为了保持一致性，如果`man.konqueror.path`设置为类似于`A_PATH_TO/konqueror`的路径，我们也会尝试这种技巧。这意味着我们将尝试启动`A_PATH_TO/kfmclient`。

如果你确实想使用`konqueror`，可以使用如下所示的配置：

```
[man]
viewer = konq
[man "konq"]
cmd = A_PATH_TO/konqueror
```

### 关于 git config --global 的说明

注意，所有这些配置变量可能应该使用`--global`标志进行设置，例如：

```
$ git config --global help.format web
$ git config --global web.browser firefox
```

因为它们可能更多地针对特定用户而非特定仓库。更多信息请参阅 (1)。

---

# GIT-HTTP-BACKEND

## 名称

`git-http-backend` - 基于 HTTP 的 Git 服务端实现

## 概要

一个简单的 CGI 程序，用于向通过`http://`和`https://`协议访问仓库的 Git 客户端提供仓库内容。该程序支持客户端使用智能 HTTP 协议（smart HTTP）和向后兼容的原始 HTTP 协议（dumb HTTP）进行拉取，同时也支持客户端使用智能 HTTP 协议进行推送（push）。

它会验证目录是否存在魔法文件“git-daemon-export-ok”，并且拒绝导出任何未通过此方式显式标记为导出的 Git 目录（除非设置了`GIT_HTTP_EXPORT_ALL`环境变量）。

默认情况下，仅启用 upload-pack 服务，它为`git fetch-pack`和`git ls-remote`客户端提供服务，这些客户端由`git fetch`、`git pull`和`git clone`调用。如果客户端通过了身份验证，将启用 receive-pack 服务，它为`git send-pack`客户端提供服务，该客户端由`git push`调用。

## 服务

这些服务可以使用每个仓库的配置文件启用/禁用：

`http.getanyfile`：此服务用于版本低于 1.6.6 无法使用 upload pack 服务的 Git 客户端。启用后，客户端可以读取仓库中的任何文件，包括无法从分支触达但仍然存在的对象。默认启用的，但仓库可以通过将此配置项设置为`false`来禁用它。

`http.uploadpack`：此服务为`git fetch-pack`和`git ls-remote`客户端提供服务。默认启用的，但仓库可以通过将此配置项设置为`false`来禁用它。

`http.receivepack`：此服务为`git send-pack`客户端提供服务，允许推送。对于匿名用户默认禁用，对于通过 Web 服务器身份验证的用户默认启用。可以通过将此项设置为`false`来禁用，或通过设置为`true`为包括匿名用户在内的所有用户启用。

## URL 解析

为了确定仓库在磁盘上的位置，`git http-backend`会拼接环境变量`PATH_INFO`（由 Web 服务器自动设置）和`GIT_PROJECT_ROOT`（必须在 Web 服务器配置中手动设置）。如果未设置`GIT_PROJECT_ROOT`，`git http-backend`将读取同样由 Web 服务器自动设置的`PATH_TRANSLATED`。

## 示例

以下示例均映射`/var/www/git/foo/bar.git`。

### Apache 2.x

确保`mod_cgi`、`mod_alias`和`mod_env`已启用，正确设置`GIT_PROJECT_ROOT`（或`DocumentRoot`），并为 CGI 创建一个`ScriptAlias`：

```
SetEnv GIT_PROJECT_ROOT /var/www/git
SetEnv GIT_HTTP_EXPORT_ALL
ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/
```

若要启用匿名读取访问但需要身份验证的写入访问，则对初始引用广告（我们通过查询字符串中的 service 参数检测其为推送）以及 receive-pack 调用本身都要求授权：

```
RewriteCond %{QUERY_STRING} service=git-receive-pack [OR]
RewriteCond %{REQUEST_URI} /git-receive-pack$
RewriteRule ^/git/ - [E=AUTHREQUIRED:yes]
<LocationMatch "^/git/">
    Order Deny,Allow
    Deny from env=AUTHREQUIRED
    AuthType Basic
    AuthName "Git Access"
    Require group committers
    Satisfy Any
    ...
</LocationMatch>
```

如果没有可用的`mod_rewrite`来匹配查询字符串，则只需保护`git-receive-pack`自身，例如：

```
<LocationMatch "^/git/.*/git-receive-pack$">
    AuthType Basic
    AuthName "Git Access"
    Require group committers
    ...
</LocationMatch>
```

在此模式下，服务器直到客户端实际开始推送的对象协商阶段才会请求身份验证，而不是在初始连接期间。由于此原因，你必须在任何应该接受推送的仓库中启用`http.receivepack`配置选项。如果未设置`http.receivepack`，默认行为是拒绝任何未验证用户的推送；因此，初始请求将向客户端报告 403 Forbidden，甚至不会提供身份验证的机会。

若要对读取和写入都要求身份验证，请在仓库或其父目录周围使用`Location`指令：

```
<Location /git/private>
    AuthType Basic
    AuthName "Private Git Access"
    Require group committers
    ...
</Location>
```

若要在同一 URL 下提供`gitweb`，使用`ScriptAliasMatch`仅针对`git http-backend`能够处理的 URL，并将其余部分转发到`gitweb`：

```
ScriptAliasMatch \
    "(?x)^/git/(.*/(HEAD | \
        info/refs | \
        objects/(info/[^/]+ | \
        [0-9a-f]{2}/[0-9a-f]{38} | \
        pack/pack-[0-9a-f]{40}\.(pack|idx)) | \
        git-(upload|receive)-pack))$" \
    /usr/libexec/git-core/git-http-backend/$1
ScriptAlias /git/ /var/www/cgi-bin/gitweb.cgi/
```

要在同一个仓库中从不同的 (7) 位置提供多个仓库：

```
SetEnvIf Request_URI "^/git/([^/]*)" GIT_NAMESPACE=$1
ScriptAliasMatch ^/git/[^/]*(.*) /usr/libexec/git-core/git-http-backend/storage.git$1
```

### 加速静态 Apache 2.x

与上述类似，但 Apache 可用于返回存储在磁盘上的静态文件。在许多系统中，这可能更高效，因为 Apache 可以请求内核将文件内容从文件系统直接拷贝到网络：

```
SetEnv GIT_PROJECT_ROOT /var/www/git
AliasMatch ^/git/(.*/objects/[0-9a-f]{2}/[0-9a-f]{38})$ /var/www/git/$1
AliasMatch ^/git/(.*/objects/pack/pack-[0-9a-f]{40}.(pack|idx))$ /var/www/git/$1
ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/
```

这可以与`gitweb`配置结合：

```
SetEnv GIT_PROJECT_ROOT /var/www/git
AliasMatch ^/git/(.*/objects/[0-9a-f]{2}/[0-9a-f]{38})$ /var/www/git/$1
AliasMatch ^/git/(.*/objects/pack/pack-[0-9a-f]{40}.(pack|idx))$ /var/www/git/$1
ScriptAlias /git/ /usr/libexec/git-core/git-http-backend/
```

### Lighttpd

确保`mod_cgi`、`mod_alias`、`mod_auth`、`mod_setenv`已加载，然后正确设置`GIT_PROJECT_ROOT`并将请求重定向到 CGI：

```
alias.url += ( "/git" => "/usr/lib/git-core/git-http-backend" )
$HTTP["url"] =~ "^/git" {
    cgi.assign = ("" => "")
    setenv.add-environment = ( "GIT_PROJECT_ROOT" => "/var/www/git", "GIT_HTTP_EXPORT_ALL" => "")
}
```

要启用匿名读取访问但需要身份验证的写入访问：

```
$HTTP["querystring"] =~ "service=git-receive-pack" {
    include "git-auth.conf"
}
$HTTP["url"] =~ "^/git/.*/git-receive-pack$" {
    include "git-auth.conf"
}
```

其中`git-auth.conf`如下所示：

```
auth.require = ( "/" => (
    "method" => "basic",
    "realm" => "Git Access",
    "require" => "valid-user"
) )
# ...并在此处设置 auth.backend
```



对于读取和写入都需要身份验证：

```
$HTTP["url"] =~ "^/git/private" { include "git-auth.conf" }
```

## 环境

`git-http-backend` 依赖于调用 Web 服务器设置的 CGI 环境变量，包括：

- `PATH_INFO`（如果设置了 `GIT_PROJECT_ROOT`，否则使用 `PATH_TRANSLATED`）
- `REMOTE_USER`
- `REMOTE_ADDR`
- `CONTENT_TYPE`
- `QUERY_STRING`
- `REQUEST_METHOD`

环境变量 `GIT_HTTP_EXPORT_ALL` 可以传递给 `git-http-backend`，以便在允许导出该仓库之前跳过对每个仓库中 `git-daemon-export-ok` 文件的检查。

环境变量 `GIT_HTTP_MAX_REQUEST_BUFFER`（或配置变量 `http.maxRequestBuffer`）可以设置以更改 git 在 fetch 过程中处理的最大 ref 协商请求；任何需要更大缓冲的 fetch 将失败。通常不需要更改此值，但如果你是从一个拥有极大量 ref（引用）的仓库拉取数据，则它可能会有所帮助。该值可以指定单位（例如，`100M` 表示 100 兆）。默认值为 10 兆。

后端进程会将 `GIT_COMMITTER_NAME` 设置为 `$REMOTE_USER`，并将 `GIT_COMMITTER_EMAIL` 设置为 `${REMOTE_USER}@http.${REMOTE_ADDR}`，确保 `git-receive-pack` 创建的任何 reflog 都包含执行 push 的远程用户的标识信息。

所有 CGI 环境变量对 `git-receive-pack` 调用的每个 hook 都可用。

# GIT-HTTP-FETCH

## 名称

`git-http-fetch` - 通过 HTTP 从远程 Git 仓库下载

## 概要

```
git http-fetch [-c] [-t] [-a] [-d] [-v] [-w filename] [--recover] [--stdin] <commit> <url>
```

## 描述

通过 HTTP 下载远程 Git 仓库。

**注意**：不带 `-a` 使用此命令的方法已弃用。`-a` 的行为将在未来的版本中成为默认值。

### 选项

`commit-id`
要拉取的哈希值或 `[URL]/refs/` 下的文件名。

`-c`
获取提交对象。

`-t`
获取与提交对象相关的树（trees）。

`-a`
获取所有对象。

`-v`
报告已下载的内容。

`-w <filename>`
传输完成后，将 `commit-id` 写入本地 `$GIT_DIR/refs/<filename>` 下的文件中。

`--stdin`
不再在命令行上指定 commit id（在这种情况下是不符合预期的），`git http-fetch` 期望标准输入中是以下格式的行：
`<commit-id>['\t'<filename-as-in--w>]`

`--recover`
验证从目标可及的所有内容是否已获取。用于之前的 fetch 被中断后。

# GIT-HTTP-PUSH

## 名称

`git-http-push` - 通过 HTTP/DAV 将对象推送到另一个仓库

## 概要

```
git http-push [--all] [--dry-run] [--force] [--verbose] <url> <ref> [<ref>...]
```

## 描述

将缺失的对象发送到远程仓库，并更新远程分支。

**注意**：如果你的 `libcurl` 低于 7.16，此命令将临时禁用，因为报告说这种组合无法工作且有时会损坏仓库。

### 选项

`--all`
不要假设远程仓库当前状态是完整的，并验证整个本地 ref 历史中的所有对象都存在于远程仓库中。

`--force`
通常，命令拒绝更新不是用于覆盖它的本地 ref 祖先的远程 ref。此标志将禁用检查。这意味着远程仓库可能会丢失提交；请谨慎使用。

`--dry-run`
执行所有操作，但实际不发送更新。

`--verbose`
报告在本地遍历的对象列表，以及成功发送到远程仓库的对象列表。

`-d, -D`
从远程仓库中删除 `<ref>`。指定的分支不能是远程 `HEAD`。如果指定了 `-d`，则必须满足以下其他条件：
- 远程 `HEAD` 必须解析为本地存在的对象
- 指定的分支解析为本地存在的对象
- 指定的分支必须是远程 `HEAD` 的祖先

`<ref>...`
要更新的远程 refs。

## 指定 refs

一个 `<ref>` 规范可以是单个模式，也可以是由冒号 `:` 分隔的两个模式对（这意味着 ref 名称中不能包含冒号）。单个模式 `<name>` 只是 `<name>:<name>` 的简写。

每个模式对由源端（冒号之前）和目标端（冒号之后）组成。要推送的 ref 通过找到匹配源端的匹配项来确定，而推送的位置通过使用目标端来确定。

如果 `<src>` 未精确匹配本地 refs 中的任意一个，则为错误。

如果 `<dst>` 不匹配任何远程 ref，则：
- 它必须以 `refs/` 开头；在这种情况下，`<dst>` 被字面用作目标。
- `<src> == <dst>` 且匹配 `<src>` 的 ref 不存在于远程 refs 集中；本地匹配 `<src>` 的 ref 被用作目标的名称。

在没有 `--force` 的情况下，只有当 `<dst>` 不存在时，`<src>` ref 才会存储在远程；如果 `<dst>` 是 `<src>` 的子集，则进行 "forward 检查"。

使用 `--force` 将禁用所有此类检查。可选地，`<ref>` 参数加上 `+` 前缀可以禁用 forward 检查。

# GIT-IMAP-SEND

## 名称

`git-imap-send` - 将标准输入的补丁发送到 IMAP 文件夹

## 概要

```
git imap-send [-v] [-q] [--no-curl]
```

## 描述

此命令将 `git format-patch` 生成的邮件箱上传到 IMAP 草稿。允许无法直接读取邮件箱的邮件客户端使用 "From"、"Date" 和 "Subject" 字段。

典型用法如下：

```
git format-patch --signoff --stdout | git imap-send
```

### 选项

`-v, --verbose`
详细。

`-q, --quiet`
安静。

`--curl`
使用 `libcurl` 与 IMAP 服务器通信，除非通过隧道。如果编译时设置了 `USE_CURL_FOR_IMAP_SEND` 选项，则忽略此项。

`--no-curl`
使用 git 自己的 IMAP 程序与 IMAP 服务器通信，而不是使用 `libcurl`。如果编译时带有 `NOSSL` 选项，则忽略此项。

## 配置

使用该工具时，必须设置 `imap.folder` 以及 `imap.tunnel` 或 `imap.host`。

### 变量

`imap.folder`
存入邮件的文件夹，通常是草稿文件夹。例如：`"INBOX.Drafts"`、`"INBOX/Drafts"` 或 `"[Gmail]/Drafts"`。必需。

`imap.tunnel`
用于设置到 IMAP 服务器隧道的命令，通过隧道传输命令而不是使用直接网络连接。在未设置 `imap.host` 时必需。

`imap.host`
标识服务器的 URL。使用 `imap://` 前缀表示非安全连接，使用 `imaps://` 前缀表示安全连接。设置了 `imap.tunnel` 时忽略，否则是必需的。

`imap.user`
登录服务器时使用的用户名。

`imap.pass`
登录服务器时使用的密码。

`imap.port`
连接到服务器的整数端口。`imap://` 主机默认为 `143`，`imaps://` 默认为 `993`。设置了 `imap.tunnel` 时忽略。

`imap.sslverify`
启用或禁用对 SSL/TLS 连接使用的服务器证书的验证。默认 `true`。设置了 `imap.tunnel` 时忽略。

`imap.preformattedHTML`
启用或禁用发送补丁时使用 html 编码。html 编码的补丁将被 `<pre>` 包裹且内容类型为 `text/html`。讽刺的是，启用此选项会导致 Thunderbird 将补丁以 `plain/text, format=fixed` email 格式发送。默认 `false`。

`imap.authMethod`
指定与 IMAP 服务器进行身份验证的方法。如果编译 Git 时开启了 `NO_CURL` 选项，或者你的 `curl` 版本低于 `7.34.0`，或者你运行 `git-imap-send` 时带 `--no-curl` 选项，则唯一支持的方法是 `CRAM-MD5`。如果没有设置此项，`git imap-send` 将使用基础 IMAP 明文 `LOGIN` 命令。

## 示例

使用隧道模式：

```
[imap]
folder = "INBOX.Drafts"
tunnel = "ssh -q -C /usr/bin/imapd ./Maildir 2> /dev/null"
```

使用直接模式：

```
[imap]
folder = "INBOX.Drafts"
host = user = bob
pass = p4ssw0rd
```

使用带 SSL 的直接模式：

```
[imap]
folder = "INBOX.Drafts"
host = user = bob
pass = p4ssw0rd
port = 123
sslverify = false
```

## 示例

要使用 GMail 的 IMAP 接口提交补丁，首先，编辑你的 `~/.gitconfig` 来指定账户设置：

```
[imap]
folder = "[Gmail]/Drafts"
host = user = port = 993
sslverify = false
```

如果你收到 "Folder doesn't exist" 的错误，可能需要改用：`folder = "[Google Mail]/Drafts"`。

一旦提交准备就绪，运行以下命令：

```bash
$ git format-patch --cover-letter -M --stdout origin/master | git imap-send
```




只需确保在邮件客户端中禁用了换行（GMail 的网页界面无论如何都会换行，因此你需要使用真正的 IMAP 客户端）。

## 注意事项

确保你的邮件程序发送的邮件符合你所属项目的标准仍然是你的责任。许多项目不希望附加补丁。某些邮件代理会转换补丁（例如，换行、以 `format=flowed` 格式发送），导致补丁失效。如果你不检查这一点，将会收到嘲讽你的“怒火”。

Thunderbird 特别被认为存在问题。Thunderbird 用户可能希望访问此网页获取更多信息：`m[]`

## 参见

(1), (1), (5)

***

# GIT-INDEX-PACK

## 名称

`git-index-pack` - 为现有的压缩存档构建包索引文件

## 摘要

`git index-pack [-v] [-o <index-file>] <pack-file>`

`git index-pack --stdin [--fix-thin] [--keep] [-v] [-o <index-file>] [<pack-file>]`

## 描述

从指定文件读取压缩存档（`.pack`），并为其构建包索引文件（`.idx`）。压缩存档与包索引可以放在 Git 仓库的 `objects/pack/` 目录下。

### 选项

`-v`

详细输出运行过程，包括进度状态。

`-o <index-file>`

将生成的包索引写入指定的文件。如果没有此选项，将通过将压缩存档文件的 `.pack` 替换为 `.idx` 来构造包索引文件名（如果压缩存档文件名不以 `.pack` 结尾，程序将失败）。

`--stdin`

当提供此标志时，将从 stdin 读取包，然后将其复制到 `<pack-file>`。如果未指定 `<pack-file>`，包将写入当前 Git 仓库的 `objects/pack/` 目录，默认名称由包内容决定。如果未指定 `<pack-file>`，考虑使用 `--keep` 以防止此进程与 `git repack` 之间发生竞态条件。

`--fix-thin`

通过向包中添加增量对象所基于的排除对象，修复由 `git pack-objects --thin` 产生的“稀”包（详见 (1)）。此选项仅在与 `--stdin` 配合时才有意义。

`--keep`

在将索引移动到最终位置之前，为关联包文件创建一个空的 `.keep` 文件。此选项通常与 `--stdin` 一起使用，以防止同时进行的 `git repack` 进程在引用更新以使用包包含的对象之前删除新构建的包和索引。

`--keep=<msg>`

类似于 `--keep`，在将索引移动到最终位置之前创建一个 `.keep` 文件，但不是创建一个空文件，而是在 `.keep` 文件中写入 `<msg>` 后跟一个 LF。以后可以在所有 `.keep` 文件中搜索 `<msg>` 消息，以定位任何已失效的文件。

`--index-version=<version>[,<offset>]`

此项仅供测试套件使用。它允许强制生成的包索引版本，并强制对位于给定偏移量之上的对象使用 64 位索引项。

`--strict`

如果包包含损坏的对象或链接，则退出。

`--check-self-contained-and-connected`

如果包包含损坏的链接，则退出。仅供内部使用。

`--threads=<n>`

指定解析增量时启动的线程数。这要求 `index-pack` 编译时启用了 `pthreads`，否则该选项将被忽略并警告。这旨在减少多处理器机器上的打包时间。然而，增量搜索窗口所需的内存是线程数的倍数。指定 0 将导致 Git 自动检测 CPU 数量并使用最多 3 个线程。

## 注意

一旦创建了索引，对象列表将进行排序，并将列表的 SHA-1 哈希值打印到标准输出。如果使用了 `--stdin`，则前缀为 `"pack\t"`，或者如果成功创建了新的 `.keep` 文件，则是 `"keep\t"`。这对于移除作为锁的 `.keep` 文件以防止上述与 `git repack` 的竞态有用。

***

# GIT-INIT-DB

## 名称

`git-init-db` - 创建一个新的 Git 仓库

## 摘要

`git init-db [-q | --quiet] [--bare] [--template=<template_directory>] [--separate-git-dir <git dir>] [--shared[=<permissions>]]`

## 描述

这是 (1) 的同义词。请参考该命令的文档。

***

# GIT-INIT

## 名称

`git-init` - 创建一个空的 Git 仓库或重新初始化现有仓库

## 摘要

`git init [-q | --quiet] [--bare] [--template=<template_directory>] [--separate-git-dir <git dir>] [--shared[=<permissions>]] [directory]`

## 描述

此命令创建一个空的 Git 仓库——基本上是一个 `.git` 目录，其中包含 `objects`、`refs/heads`、`refs/tags` 和模板文件。还会创建一个引用 master 分支的 HEAD 文件。

如果设置了 `$GIT_DIR` 环境变量，则它指定了替代 `/.git` 的仓库路径。

如果通过 `$OBJECT_DIRECTORY` 环境变量指定了对象存储目录，则会在其下创建 sha1 目录，否则使用默认 `$GIT_DIR/objects` 目录。

在现有仓库运行 `git init` 是安全的。它不会覆盖已存在的内容。重新运行 `git init` 的主要原因是获取新添加的模板（如果给了 `--separate-git-dir`，则是移动仓库到其他地方）。

### 选项

`-q, --quiet`

仅打印错误和警告消息；将抑制其他输出。

`--bare`

创建一个裸仓库。如果未设置 `GIT_DIR` 环境变量，则将其设置为当前工作目录。

`--template=<template_directory>`

指定从哪个目录使用模板。（参见下文的“模板目录”部分。）

`--separate-git-dir=<git dir>`

不再将仓库初始化为 `$GIT_DIR` 或 `/.git/`，而是在此创建一个包含实际仓库路径的文本文件。该文件作为仓库的文件系统无关 Git 符号链接。

如果是重新初始化，仓库将移动到指定的路径。

`--shared[=(false|true|umask|group|all|world|everybody|0xxx)]`

指定 Git 仓库供多个用户共享。这允许属于同一组的用户向该仓库推送内容。当指定此项时，将设置配置变量 `core.sharedRepository`，以便 `$GIT_DIR` 下的文件和目录按照请求的权限创建。当未指定时，Git 将使用 (2) 提供的权限。

该选项可以具有以下值，如果没有给出值则默认为 `group`：

`umask`（或 `false`）

使用 (2) 提供的权限。未指定 `--shared` 时的默认值。

`group`（或 `true`）

将仓库设为组可写（并设置 g+sx，因为 git 组可能不是所有用户的主组）。这被用于放宽原本安全的 (2) 值的权限。注意，umask 仍然适用于其他权限位（例如，如果 umask 为 `0022`，使用 `group` 将不会移除其他（非组）用户的读取权限）。请参阅 `0xxx` 了解如何精确指定仓库权限。

`all`（或 `world` 或 `everybody`）

与 `group` 相同，但允许所有用户读取仓库。

`0xxx`

`0xxx` 是一个八进制数字，每个文件都将具有模式 `0xxx`。`0xxx` 将覆盖用户的 (2) 值（而不仅仅像 `group` 和 `all` 那样仅放宽权限）。`0640` 将创建一个组可读、但组不可写且其他人不可访问的仓库。`0660` 将创建一个当前用户和组可读可写，但其他人不可访问的仓库。

默认情况下，共享仓库中启用了配置标志 `receive.denyNonFastForwards`，因此你无法强制将非快进推送推入。

如果你提供了一个 `directory`，命令将在其内部运行。如果该目录不存在，将创建它。

## 模板目录（TEMPLATE DIRECTORY）

模板目录包含在创建后将复制到 `$GIT_DIR` 的文件和目录。

模板目录将是以下之一（按顺序排列）：

1. 使用 `--template` 选项提供的参数；
2. 环境变量 `$GIT_TEMPLATE_DIR` 的内容；
3. 配置变量 `init.templateDir`；或
4. 默认模板目录：`/usr/share/git-core/templates`。

默认模板目录某些目录结构、建议的“排除模式”（参见 (5)）以及示例的钩子文件（参见 (5)）。

## 示例（EXAMPLES）

为现有代码库启动一个新的 Git 仓库：

```sh
$ cd /path/to/my/codebase
$ git init (1)
$ git add . (2)
$ git commit (3)
```

**1.** 创建一个 `/path/to/my/codebase/.git` 目录。  
**2.** 将所有现有文件添加到索引。  
**3.** 将原始状态记录为历史中的第一次提交。

***

# GIT-INSTAWEB

## 名称（NAME）

`git-instaweb` - 在 gitweb 中立即浏览你的工作仓库

## 摘要（SYNOPSIS）

`git instaweb [--local] [--httpd=<httpd>] [--port=<port>] [--browser=<browser>]`

`git instaweb [--start] [--stop] [--restart]`

## 描述（DESCRIPTION）

用于设置 gitweb 和用于浏览本地仓库的网络服务器简单脚本。

## 选项（OPTIONS）

- `-l, --local`  
  仅将服务器绑定到本地 IP（127.0.0.1）。
- `-d, --httpd`  
  将执行的 HTTP 守护进程命令行。可以在此处指定命令行选项，配置文件将被添加到命令行末尾。目前支持 apache2、lighttpd、mongoose、plackup 和 webrick。（默认：lighttpd）
- `-m, --module-path`  
  模块路径（仅当 httpd 为 Apache 时需要）。默认：`/usr/lib/apache2/modules`
- `-p, --port`  
  绑定到 httpd 的端口号。（默认：1234）
- `-b, --browser`  
  用于查看 gitweb 页面的网页浏览器。这将与 gitweb 实例的 URL 一起传递给 `git web--browse` 辅助脚本。更多信息请参见 (1)。如果脚本失败，URL 将打印到 stdout。
- `start, --start`  
  启动 httpd 实例并退出。根据需要重新生成启动新实例配置文件。
- `stop, --stop`  
  停止 httpd 实例并退出。这不会生成启动新实例的任何配置文件，也不会关闭浏览器。
- `restart, --restart`  
  重启 httpd 实例并退出。根据需要重新生成启动新实例配置文件。

## 配置（CONFIGURATION）

你可以在 `.git/config` 中指定配置：

```ini
[instaweb]
    local = true
    httpd = apache2 -f
    port = 4321
    browser = konqueror
    modulePath = /usr/lib/apache2/modules
```

如果未设置配置变量 `instaweb.browser`，如果定义了 `web.browser` 则将使用它。更多信息请参见 (1)。

## 参见（SEE ALSO）

(1)

***

# GIT-INTERPRET-TRAILERS

## 名称（NAME）

`git-interpret-trailers` - 帮助向提交消息中添加结构化信息

## 摘要（SYNOPSIS）

`git interpret-trailers [--trim-empty] [(--trailer <token>[(=|:)<value>])...] [<file>...]`

## 描述（DESCRIPTION）

帮助在提交消息的自由格式部分末尾添加类似于 RFC 822 电子邮件头的 `trailers` 行。

此命令从 `<file>` 参数或在未指定 `<file>` 的情况下从标准输入读取某些补丁或提交消息。然后，此命令将使用 `--trailer` 选项传递的参数（如果有）应用到每个输入文件的消息部分。结果输出到标准输出。

某些配置变量控制 `--trailer` 参数应用到每个提交消息的方式，以及提交消息中现有 trailer 的更改方式。它们还使得自动添加某些 trailer 可能。

默认情况下，使用 `--trailer` 提供的 `<token>=<value>` 或 `<token>:<value>` 参数只有在最后一个 trailer 具有不同的（`<token>`、`<value>`）对（或者不存在现有 trailer）时，才会添加到现有 trailer 之后。`<token>` 和 `<value>` 部分将被修剪以移除开头和结尾的空格，修剪后的 `<token>` 和 `<value>` 将如下所示消息中：

```text
token: value
```




这意味着修剪后的 `<token>` 和 `<value>` 将由 `: `（一个冒号和一个空格）分隔。

默认情况下，新 trailer 将出现在所有现有 trailer 的末尾。如果没有现有 trailer，新 trailer 将出现在输出的提交消息部分之后；如果消息部分末尾没有只有空格的行，则会在新 trailer 之前添加一个空行。

现有的 trailer 通过在输入消息中查找一组一个或多个包含冒号（默认值）的行来提取，该组之前应有一个或多个空行（或仅包含空格的行）。三个减号开始消息的后续部分。读取 trailer 时，`token`、分隔符和 `value` 之间存在空格。`token` 和 `value` 内部也可以有空格。

注意，`trailers` 不遵循也不打算遵循 RFC822 头的许多规则。例如，它们不遵循折叠规则、编码规则以及许多其他规则。

## 选项（OPTIONS）

- `--trim-empty`

  如果任何 trailer 的 `<value>` 部分仅包含空格，则从结果消息中删除整个 trailer。这适用于现有的 trailer 和新的 trailer。

- `--trailer <token>[(=|:)<value>`

  指定作为 trailer 应用到输入消息的（`<token>`，`<value>`）对。参见命令描述。

## 配置变量（CONFIGURATION VARIABLES）

### `trailer.separators`

此选项告知哪些字符被识别为 trailer 分隔符。默认情况下，只有 `:` 被识别为 trailer 分隔符，为了兼容其他 git 命令，命令行上始终接受 `=`。

此选项提供的第一个字符将作为在 trailer 配置未指定其他分隔符时的默认分隔符。

例如，如果此选项的值为 `%=$`，则只有包含 `%`、`=` 或 `$` 的行会被视为 trailer。并且 `%` 将是默认分隔符，因此默认情况下 trailer 显示为：`<token>% <value>`（`token` 和 `value` 之间将有一个百分号和一个空格）。

### `trailer.where`

此选项告知在何处添加新 trailer。可以是 `end`（默认值）、`start`、`after` 或 `before`。

如果是 `end`，则每个新 trailer 将出现在现有 trailer 的末尾。

如果设置为 `start`，则每个新的 trailer（脚注）将出现在现有 trailer 的开头，而不是末尾。

如果设置为 `after`，则每个新的 trailer 将紧跟最后一个具有相同 `<token>` 的 trailer 之后。

如果设置为 `before`，则每个新的 trailer 将紧跟第一个具有相同 `<token>` 的 trailer 之前。

### `trailer.ifexists`

此选项允许选择当消息中已经存在至少一个具有相同 `<token>` 的 trailer 时执行什么操作。

该选项的有效值为：`addIfDifferentNeighbor`（默认值）、`addIfDifferent`、`add`、`overwrite` 或 `doNothing`。

使用 `addIfDifferentNeighbor` 时，只有在添加新 trailer 的行上方或下方没有相同（`<token>`、`<value>`）值对的 trailer 时，才会添加新 trailer。

使用 `addIfDifferent` 时，只有在消息中没有具有相同（`<token>`、`<value>`）值对的 trailer 时，才会添加新 trailer。

使用 `add` 时，即使消息中已经存在相同（`<token>`、`<value>`）值对的 trailer，也会添加新 trailer。

使用 `replace` 时，将删除现有的相同 `<token>` 的 trailer 并添加新 trailer。被删除的 trailer 是距离新 trailer 添加位置最近的那个。

使用 `doNothing` 时，如果消息中已经存在相同 `<token>` 的 trailer，则不进行任何操作。

### `trailer.ifmissing`

此选项允许选择当消息中尚无相同 `<token>` 的 trailer 时执行什么操作。

该选项的有效值为：`add`（默认值）和 `doNothing`。

使用 `add` 时，将添加新 trailer。

使用 `doNothing` 时，不进行任何操作。

### `trailer.<token>.key`

在 trailer 中，此键将代替 `<token>`。在此键的末尾可以出现一个分隔符，然后是一些字符。默认情况下，有效分隔符是 `:`，但可以通过 `trailer.separators` 配置变量进行更改。

如果存在分隔符，在添加 trailer 时，此键将同时代替 `<token>` 和默认分隔符。

### `trailer.<token>.where`

此选项的值与 `trailer.where` 配置变量相同，并且对于具有指定 `<token>` 的 trailer，它将覆盖该选项指定的值。

### `trailer.<token>.ifexist`

此选项的值与 `trailer.ifexist` 配置变量相同，并且对于具有指定 `<token>` 的 trailer，它将覆盖该选项指定的值。

### `trailer.<token>.ifmissing`

此选项的值与 `trailer.ifmissing` 配置变量相同，并且对于具有指定 `<token>` 的 trailer，它将覆盖该选项指定的值。

### `trailer.<token>.command`

此选项用于指定一个 shell 命令，自动添加或修改指定 `<token>` 的 trailer。指定此选项时，行为类似于在命令行开头添加了一个特殊的 `<token>=<value>` 参数，其中 `<value>` 取自指定命令的标准输出，并去除了前后的空格。

如果命令包含 `$ARG` 字符串，在启动命令之前，如果存在相同 `<token>` 的 trailer，该字符串将被该 trailer 的 `<value>` 部分替换。

如果在命令行上传递了多个 `<token>=<value>` 参数且配置了 `trailer.<token>.command`，则会为这些参数每一个执行一次命令。参数的 `<value>` 部分（如果有）将用于替换命令中的 `$ARG` 字符串。

## 示例

配置带有 `Signed-off-by` 键的 `sign` trailer，然后在消息中添加两个此类 trailer：

```bash
$ git config trailer.sign.key "Signed-off-by"
$ cat msg.txt
subject message
$ cat msg.txt | git interpret-trailers --trailer 'sign: Alice <>' --trailer 'sign: Bob <>'
subject message
Signed-off-by: Alice <>
Signed-off-by: Bob <>
```

将最后一个提交提取为补丁，并为其添加 `Cc` 和 `Reviewed-by` trailer：

```bash
$ git format-patch -1 0001-foo.patch
$ git interpret-trailers --trailer 'Cc: Alice <>' --trailer 'Reviewed-by: Bob <>' 0001-foo.patch >0001-bar.patch
```

配置带有命令的 `sign` trailer，仅在没有 `Signed-off-by:` 时自动添加带有作者信息的 `Signed-off-by:`，并展示其工作原理：

```bash
$ git config trailer.sign.key "Signed-off-by: "
$ git config trailer.sign.ifmissing add
$ git config trailer.sign.ifexists doNothing
$ git config trailer.sign.command 'echo "$(git config user.name) <$(git config user.email)>"'
$ git interpret-trailers <<EOF
> EOF
Signed-off-by: Bob <>

$ git interpret-trailers <<EOF
> Signed-off-by: Alice <>
> EOF
Signed-off-by: Alice <>
```

配置键包含 `#` 且字符后没有空格的 `fix` trailer，并展示其工作原理：

```bash
$ git config trailer.separators ":#"
$ git config trailer.fix.key "Fix #"
$ echo "subject" | git interpret-trailers --trailer fix=42
subject
Fix #42
```

配置带有命令的 `see` trailer 以显示相关提交的主题，并展示其工作原理：

```bash
$ git config trailer.see.key "See-also: "
$ git config trailer.see.ifExists "replace"
$ git config trailer.see.ifMissing "doNothing"
$ git config trailer.see.command "git log -1 --oneline --format=\"%h (%s)\" --abbrev-commit --abbrev=14 \$ARG"
$ git interpret-trailers <<EOF
> subject
>
> message
>
> see: HEAD~2
> EOF
subject
message
See-also: fe3187489d69c4 (subject of related commit)
```



`-L <start>,<end>:<file>, -L :<funcname>:<file>`

在`<file>`中追踪由`"<start>,<end>"`（或函数名正则`<funcname>`）给定的行范围演变。你不能提供任何路径规格限制器（pathspec limiters）。目前这仅限于从单个修订开始的遍历，即你只能提供零或一个正向修订参数。你可以多次指定此选项。

`<start>`和`<end>`可以采用以下形式之一：

`number`：如果`<start>`或`<end>`是数字，它将指定一个绝对行号（行从 1 开始计数）。

`/regex/`：这种形式将使用匹配给定 POSIX 正则的第一行。如果`<start>`是正则表达式，它将从上一个`-L`范围（如果有）的结尾开始搜索，否则从文件开始开始。如果`<start>`为`^/regex/`，它将从文件开始搜索。如果`<end>`是正则表达式，它将从`<start>`指定的行开始搜索。

`+offset`或`-offset`：这仅对`<end>`有效，并将指定`<start>`指定行之前或之后的行数。

如果在`<start>`和`<end>`处给出`":<funcname>"`，它是一个正则表达式，表示从第一个匹配`<funcname>`的`funcname`行到下一个`funcname`行的范围。`":<funcname>"`从上一个`-L`范围（如果有）的结尾搜索，否则从文件开始。`"^:<funcname>"`从文件开始搜索。

`<revision range>`：仅显示指定修订范围内的提交。未指定`<revision range>`时默认为`HEAD`（即通往当前提交的完整历史）。`origin..HEAD`指定从当前提交（即`HEAD`）可达的所有提交，但从`origin`不可达。关于指定`<revision range>`方式的完整列表，请参阅（7）中的*Specifying Ranges*部分。

`[--] <path>...`：仅显示足以解释匹配指定路径的文件如何产生的提交。详情请参见下文的*History Simplification*以及其他简化模式。当出现歧义时，路径可能需要加上`'-- '`前缀，以将其与选项或修订范围隔开。

### Commit Limiting

除了使用描述中解释的特殊符号指定应列出的提交范围外，还可能应用额外的提交限制。除非另有说明，否则使用更多选项通常会进一步限制输出（例如，`--since=<date1>`限制为`<date1>`之后的提交，配合`--grep=<pattern>`使用时进一步限制为日志消息中匹配`<pattern>`行的提交）。注意，这些限制是在提交排序和格式选项（如`--reverse`）之前应用的。

`-number>, -n <number>, --max-count=<number>`：限制输出的提交数量。

`--skip=<number>`：在开始显示提交输出之前跳过`<number>`个提交。

`--since=<date>, --after=<date>`：显示比特定日期更新的提交。

`--until=<date>, --before=<date>`：显示比特定日期更老的提交。

`--author=<pattern>, --committer=<pattern>`：将提交输出限制为作者/提交者头部行匹配指定模式（正则表达式）的提交。如果有多个`--author=<pattern>`，则选择作者匹配任何给定模式的提交（多个`--committer=<pattern>`亦然）。

`--grep-reflog=<pattern>`：将提交输出限制为 reflog 条目匹配指定模式（正则表达式）的提交。如果有多个`--grep-reflog`，则选择 reflog 消息匹配任何给定模式的提交。除非使用了`--walk-reflogs`，否则使用此选项被视为错误。

`--grep=<pattern>`：将提交输出限制为日志消息匹配指定模式（正则表达式）的提交。如果有多个`--grep=<pattern>`，则选择消息匹配任何给定模式的提交（但请参见`--all-match`）。当`--show-notes`生效时，注释中的消息将作为视为日志消息的一部分进行匹配。

`--all-match`：将提交输出限制为匹配所有给定`--grep`的提交，而不是匹配至少一个的。

`--invert-grep`：将提交输出限制为日志消息不匹配`--grep=<pattern>`指定模式的提交。

`-i, --regexp-ignore-case`：在不区分字母大小的情况下匹配正则表达式限制模式。

`--basic-regexp`：将限制模式视为基本正则表达式；这是默认值。

`-E, --extended-regexp`：将限制模式视为扩展正则表达式而非默认的基本正则表达式。

`-F, --fixed-strings`：将限制模式视为固定字符串（不将模式解释为正则表达式）。

`--perl-regexp`：将限制模式视为 Perl 兼容正则表达式。需要编译时包含 libpcre。

`--remove-empty`：当给定路径从树中消失时停止。

`--merges`：仅打印合并提交。这等同于`--min-parents=2`。

`--no-merges`：不打印有多个父提交的提交。这等同于`--max-parents=1`。

`--min-parents=<number>, --max-parents=<number>, --no-min-parents, --no-max-parents`：仅显示至少（或最多）数量父提交的提交。特别是，`--max-parents=1`等同于`--no-merges`，`--min-parents=2`等同于`--merges`。`--max-parents=0`提供所有根提交，`--min-parents=3`所有章鱼合并（octopus merges）。`--no-min-parents`和`--no-max-parents`重置这些限制（无限制）。等效形式为`--min-parents=0`（任何提交都有 0 或多个父提交）和`--max-parents=-1`（负数表示无上限限制）。

`--first-parent`：在遇到合并提交时仅追踪第一个父提交。在查看特定主题分支的演变时，此选项可以提供更好的概述，因为合并到主题分支的合并通常是为了偶尔适应更新的上游，而此选项允许你忽略由此类合并引入历史历史的单个提交。不能与`--bisect`结合使用。

`--not`：反转后续所有修订规格符`^*`前缀（或其缺失）的含义，直到下一个`--not`。

`--all`：假装`refs/`下所有的引用都作为`<commit>`列在命令行上。

`--branches[=<pattern>]`：假装`refs/heads`下所有的引用都作为`<commit>`列在命令行上。如果给了`<pattern>`，则将分支限制为匹配给定 shell 通配符（shell glob）的分支。如果模式结尾缺少`?`、`***`或`[*]`，则隐含`*/**`。

`--tags[=<pattern>]`：假装`refs/tags`下所有的引用都作为`<commit>`列在命令行上。如果给了`<pattern>`，则将标签限制为匹配给定 shell 通配符的标签。如果模式结尾缺少`?`、`***`或`[*]`，则隐含`*/**`。

`--remotes[=<pattern>]`：假装`refs/remotes`下所有的引用都作为`<commit>`列在命令行上。如果给了`<pattern>`，则将远程跟踪分支限制为匹配给定 shell 通配符的引用。如果模式结尾缺少`?`、`***`或`[*]`，则隐含`*/**`。

`--glob=<glob-pattern>`：假装所有匹配 shell 通配符`<glob-pattern>`的引用都作为`<commit>`列在命令行上。如果缺少`refs/*`，则自动添加。如果模式结尾缺少`?`、`***`或`[*]`，则隐含`*/**`。

`--exclude=<glob-pattern>`：对于下一个`--all`、`--branches`、`--tags`、`--remotes`或`--glob`将会考虑的匹配`<glob-pattern>`的引用。重复此选项会累积排除模式，直到下一个`--all`、`--branches`、`--tags`、`--remotes`或`--glob`选项（其他选项或参数不会清除累积模式）。应用于`--branches`、`--tags`或`--remotes`时，给出的模式不应以`refs/heads`、`refs/tags`或`refs/remotes`开头；应用于`--glob`或`--all`时，必须以`refs/`开头。如果想要`*/**`，必须显式给出。

`--reflog`：假装所有由 reflog 提到的对象都作为`<commit>`列在命令行上。

`--ignore-missing`：在输入中看到无效的句名时，假装该错误输入不存在。

### --bisect

假装错误的二分引用`refs/bisect/bad`已列出，并且假装在命令行上它紧随其后的`--not`以及良好的二分引用`refs/bisect/good-*`。不能与`--first-parent`结合使用。

### --stdin

除了命令行上列出的`<commit>`之外，还从标准输入读取它们。如果看到`--*`分隔符，则停止读取提交并开始读取路径以限制结果。

### --cherry-mark

类似于`--cherry-pick`（见下文），但等价提交会被用`=`标记而不是省略，不等价的提交则会被用`+`标记不等价的提交。

### --cherry-pick

当提交集通过对称差异限制时，省略任何与“另一侧”提交引入了相同更改的提交。例如，如果你有两个分支`A`和`B`，列出它们单侧所有提交的常用方法是使用`--left-right`（见下文`--left-right`选项说明中的示例）。然而，它会显示从另一个分支 cherry-pick 的提交（例如，“3rd on b”可能从分支`A` cherry-pick 来自）。使用此选项，此类提交对将排除在输出之外。

### --left-only, --right-only

仅列出对称范围内相应侧的提交，即仅那些被`--left-right`标记为`< resp. >`的提交。例如，`--cherry-pick --right-only A...B`会省略`B`中位于`A`中或与`A`中的提交等效的提交。换句话说，这列出了`git cherry A B`中的`+`提交。更准确地说，`--cherry-pick --right-only --no-merges`给出了精确列表。

### --cherry

`--right-only --cherry-mark --no-merges`的同义词；用于限制输出在我们侧的提交，并标记那些已应用到分支历史另一侧的提交，类似于`git log --cherry upstream...mybranch`，类似于`git cherry upstream mybranch`。

### -g, --walk-reflogs

不再遍历提交祖先链，而是从最近的一个到较旧的遍历 reflog way。使用此选项时，你无法指定要排除的提交（即不能使用`^commit`、`commit1..commit2`和`commit1...commit2`表示法）。使用`oneline`以外的`--pretty`格式（出于明显原因），会导致输出包含两行额外的 reflog 信息。默认情况下，输出中使用`commit@{Nth}`标记。当起始提交指定为`commit@{now}`时，输出也会使用`commit@{timestamp}`标记。在`--pretty=oneline`下，提交消息在同一行中带有这些信息的标记。此选项不能与`--reverse`结合使用。另见（1）。

### --merge

合并失败后，显示触及冲突文件且在所有合并头中都不存在的引用。

### --boundary

输出被排除的边界提交。边界提交以`-`为前缀。

## 历史简化

有时你只对历史的部分感兴趣，例如修改特定`<path>`的提交。但历史简化分为两部分：一部分是选择提交，另一部分是如何执行，因为有多种简化历史的策略。

以下选项选择要显示的提交：

### <paths>

选择修改给定`<paths>`的提交。

### --simplify-by-decoration

选择被某些分支或标签引用的提交。注意，可以显示额外的提交以提供有意义的历史。

以下选项影响简化的执行方式：

### 默认模式

将历史简化为解释树最终状态的最简单历史。之所以简单，是因为如果结果相同（例如合并内容相同的分支），它会修剪某些侧分支。

### --full-history

与默认模式相同，但不会修剪某些历史。

### --dense

仅显示所选的提交，加上一些为了保持历史意义的提交。

### --sparse

显示简化历史中的所有提交。

### --simplify-merges

`--full-history`的附加选项，用于从结果历史中移除某些不必要的合并，因为没有选定的提交贡献于此合并。

### --ancestry-path

当给定的显示的提交范围（例如`commit1..commit2`或`commit2 ^commit1`）时，仅显示直接存在`commit1`和`commit2`之间祖先链上的提交，即既是`commit1`的后代又是`commit2`的祖先的提交。后续有更详细的解释。

假设你指定了`foo`为`<paths>`。我们将修改`foo`的提交称为`!TREESAME`，其余称为`TREESAME`。（在针对`foo`过滤的 diff 中，它们看起来是不同且相等的。）在下文中，我们将始终引用同一个示例历史来说明简化设置之间的差异。我们假设你正在此提交图中过滤文件`foo`：

```
.-A---M---N---O---P---Q / / / / / / I B C D E Y \ / / / / / `-------------' X`
```

历史的水平线`A---Q`被视为每次合并的第一个父。提交如下：`I`是初始提交，其中`foo`存在。默认，输出中使用`commit@{Nth}`标记。当起始提交指定为`commit@{now}`时，输出也会使用`commit@{timestamp}`标记。在`--pretty=oneline`下，提交消息在同一行中带有这些信息的标记。此选项不能与`--reverse`结合使用。（注：此处原文文本似乎出现了重复或逻辑中断，根据高级文档工程师的规范，仅翻译提供的文本内容。）

与不重写父提交的`--full-history`相比，请注意 E 被剪除了，因为它是`TREESAME`，但 P 的父提交列表被重写了，包含了 E 的父提交 I。C 和 N，以及 X、Y 和 Q 也发生了相同的情况。除了上述设置外，你还可以更改`TREESAME`是否影响包含范围：

### --dense

如果被遍历的提交与任何父提交相比不是`TREESAME`，则它们会被包含。

### --sparse

所有被遍历的提交都会被包含。注意，即使没有`--full-history`，这仍然简化了合并：如果其中一个父提交是`TREESAME`，则我们只追踪那一个，因此合并的其他分支永远不会被遍历。

### --simplify-merges

首先，以与重写父提交的`--full-history`相同的方式构建历史图谱（见上文）。然后，根据以下规则将每个提交`C`简化为在最终历史中的替换项`C'`：

1. 将`C'`设置为`C`。
2. 将`C'`的每个父提交`P`替换为其简化后的`P'`。在此过程中，丢弃其他父提交的祖先或者是与空树`TREESAME`的根提交，并移除重复项，但注意不要丢弃所有我们`TREESAME`的父提交。
3. 如果在这次父提交重写后，`C'`是根提交或合并提交（具有 0 个或>1 个父提交）、边界提交或`!TREESAME`，则保留它。否则，它被替换为它的唯一父提交。

这种效果通过与重写父提交的`--full-history`比较表现得最好。示例变为：

```
.-A---M---N---O / / / I B D \ / / `---------'
```

注意与`--full-history`相比，N、P 和 Q 的主要区别：

- `N`的父提交列表删除了`I`，因为它是另一个父提交`M`的祖先。尽管如此，`N`留了下来，因为它是`!TREESAME`。
- `P'`的父提交列表同样删除了`I`。随后`P`被完全删除，因为它有一个父提交且是`TREESAME`。
- `Q`的父提交列表将`Y`简化为`X`。随后`X`被删除，因为它是一个`TREESAME`根提交。随后`Q`也被完全删除，因为它有一个父提交且是`TREESAME`。

最后，还有第五种简化模式可用：

### --ancestry-path

将显示的提交限制在给定提交范围内，“从”提交和“到”提交之间祖先链上的提交。即：只显示是“到”提交的祖先且“从”提交的后代的提交。

作为一个示例用例，请考虑以下提交历史：

```
D---E-------F / \ \ B---C---G---H---I---J / \ A-------K---------------L--M
```



普通的`D..M`计算`M`的祖先提交集合，但排除了`D`的祖先提交。这对于查看自`D`以来通往`M`的历史发生了什么很有用，即“`M`拥有哪些`D`中不存在的内容”。在本示例中的结果将是所有提交，除了`A`和`B`（当然还有`D`本身）。

然而，当我们想要找出`M`中哪些提交被`D`引入的漏洞污染并需要修复时，可能只想查看`D..M`中实际上是`D`的后代的子集，即排除`C`和`K`。这正是`--ancestry-path`选项的作用。应用于`D..M`范围时，结果为：

```
E-------F
 \       \
  G---H---I---J
       \
        L--M
```

`--simplify-by-decoration`选项允许通过省略未被标签引用的提交来只查看历史拓扑的大体。如果满足(1)它们被标签引用，或(2)它们更改了命令行给出路径的内容，则提交被标记为`!TREESAME`（换说，在上述历史简化规则后保留）。所有其他提交都被标记为`TREESAME`（将被简化移除）。

### 提交排序

默认情况下，提交按时间倒序顺序显示。

`--date-order`

在显示所有子提交之前不显示其父提交，否则按提交时间戳顺序显示提交。

`--author-date-order`

在显示所有子提交之前不显示其父提交，否则按作者时间戳顺序显示提交。

`--topo-order`

在显示所有子提交之前不显示其父提交，并避免显示多行历史交错在一起的提交。

例如，在这样的提交历史中：

```
---1----2----4----7
    \              \
     3----5----6----8---
```

其中数字表示提交时间戳的顺序，`git rev-list`等配合`--date-order`会按时间戳顺序显示提交：8 7 6 5 4 3 2 1。

使用`--topo-order`，它们将显示8 6 5 3 7 4 2 1（或8 7 4 2 6 5 3 1）；某些较旧的提交会在较新的之前显示，以避免将两条并行开发分支的提交混合在一起。

`--reverse`

反序输出提交。不能与`--walk-reflogs`结合。

### 对象遍历

这些选项主要针对Git仓库的打包。

`--no-walk[=(sorted|unsorted)]`

仅显示指定的提交，但不遍历它们的祖先。如果指定了范围，则没有影响。如果给出参数`unsorted`，则按给命令行顺序显示提交。否则（如果给出参数`sorted`），则按提交时间倒序显示提交。不能与`--reflogs`结合。

`--do-walk`

覆盖之前的`--no-walk`。

### 提交格式化

`--pretty=[format]`, `--format=<format>`

以给格式打印提交内容，其中`<format>`可以是`oneline`、`short`、`medium`、`full`、`email`、`raw`、`format:<string>`。当`<format>`不是上述之一时，行为相当于给了`format:<string>`。详情见某些章节。当省略`<format>`时，默认为`medium`。

`--notes=[ref>]`

在显示提交日志消息时，显示注释该提交的注释（见1）。这是`git log`、`git show`和`git whatchanged`命令在没有`--pretty`、`--format`或`--oneline`选项时的默认行为。

默认情况下，显示的注释来自`core.notesRef`和`notes.displayRef`变量列出的注释引用（或相应的环境变量）。更多细节见(1)。

带有可选的`<ref>`参数时，显示此注释引用而非默认的注释引用。如果引用未限定，则认为在`refs/notes/`中。

多个`--notes`选项可以组合使用以控制显示哪些注释。示例：`--notes=foo`将仅显示来自`refs/notes/foo`的注释；`--notes=foo --notes`将显示来自`refs/notes/foo`和默认注释引用的注释。

`--no-notes`

不显示注释。这通过重置显示注释的注释引用列表来抵消上述`--notes`选项。选项按照命令行给出的顺序解析，因此例如`--notes --notes=foo --no-notes --notes=bar`将只会显示来自`refs/notes/bar`的注释。

### `--show-notes[=<ref>]`, `--[no-]standard-notes`

这些选项已弃用。请使用上述`--notes`/`--no-notes`选项。

### `--show-signature`

通过将签名传递给`gpg --verify`来检查签名提交对象的有效性并显示输出。

### `--relative-date`

`--date=relative`的同义词。

### `--date=(relative|local|default|iso|iso-strict|rfc|short|raw)`

仅对以人类可读格式显示的日期生效，例如当使用`--pretty`时。`log.date`配置变量为`log`命令的`--date`选项设置默认值。

- `--date=relative`显示相对于当前时间的日期，例如“2 hours ago”。
- `--date=local`显示用户本地时区的时间戳。
- `--date=iso`（或`--date=iso8601`）以类似ISO 8601的格式显示时间戳。与严格ISO 8601格式的区别在于：
    - 使用空格代替`T`日期/时间分隔符
    - 时间和时区之间有空格
    - 时区的小时和分钟之间没有冒号
- `--date=iso-strict`（或`--date=iso8601-strict`）以严格的ISO 8601格式显示时间戳。
- `--date=rfc`（或`--date=rfc2822`）以RFC 2822格式显示时间戳，常见于邮件。
- `--date=short`仅显示日期不显示时间，格式为YYYY-MM-DD。
- `--date=raw`以Git内部的原始格式`%s %z`显示日期。
- `--date=default`显示原始时区（提交者或作者）的时间戳。

### `--parents`

同时打印提交的父提交（格式为“commit parent...”）。还会启用父提交重写，详见下方的*History Simplification*。

### `--children`

同时打印提交的子提交（格式为“commit child...”）。还会启用父提交重写，详见下方的*History Simplification*。

### `--left-right`

标记提交是从对称差异的哪侧可。来自左侧的提交以`<`前缀，来自右侧的提交以`>`前缀。如果与`--boundary`，这些提交将以前`-`前缀。

例如，你有如下拓扑结构：

```
y---b---b  branch B
 / \ / \
/   \ /   \
o---x---a---a  branch A
```

你将得到如下输出：

```
$ git rev-list --left-right --boundary --pretty=oneline A...B

>bbbbbbb... 3rd on b
>bbbbbbb... 2nd on b
<aaaaaaa... 3rd on a
<aaaaaaa... 2nd on a
-yyyyyyy... 1st on b
-xxxxxxx... 1st on a
```

### `--graph`

在输出的左侧绘制提交历史的文本图形化表示。这可能会导致提交之间打印额外的行，以便正确绘制图形历史。不能与`--no-walk`结合。

这启用父提交重写，详见下方的*History Simplification*。

这隐含了`--topo-order`选项，但也可以指定`--date-order`选项。

### `--show-linear-break[=<barrier>]`

当不使用`--graph`时，所有历史分支都会被展平，这可能很难看出两个连续的提交不属于线性分支。在这种情况下，此选项会在它们之间放置屏障。如果指定了`<barrier>`，则将显示该字符串代替默认字符串。

### Diff Formatting

列出的是控制diff输出格式的选项。其中某些特定于(1)，但也可以给出其他diff选项。更多选项见(1)。

- `-c`: 使用此选项，合并提交的diff输出将同时显示每个父提交与合并结果之间的差异，而不是逐一显示父与结果之间的差异。此外，它只列出从所有父提交修改的文件。
- `--cc`: 此标志意味着`-c`选项，通过省略有趣的hunk来进一步压缩补丁输出，这些hunk在父提交中只有两种变体，而合并结果在未修改的情况下选择了其中一个。
- `-m`: 此标志使合并提交像普通提交一样显示完整的diff；对于每个合并父，生成单独的日志条和diff。异常是当给出`--first-parent`选项时，只显示相对于第一个父提交的diff；在这种情况下，输出代表合并带入当前分支的更改。
- `-r`: 显示递归diff。
- `-t`: 在diff输出中显示树对象。这隐含`-r`。

### PRETTY FORMATS

如果提交是合并，且格式化格式不是`oneline`、`email`或`raw`，则在`Author:`行之前插入额外行。该行以"Merge: "开头，并打印祖先提交的sha1，用空格分隔。请注意，如果你限制了历史视图，列出的提交不一定是直接父提交的列表：例如，如果你只对与特定目录或文件的更改感兴趣。

有几种内置格式，你可以通过将`pretty.<name>`配置选项设置为另一个格式名称或`format:`字符串来定义额外的格式，如下文所示（见(1)）。以下是内置格式的详情：

#### oneline

```
<sha1> <title line>
```

此设计旨在尽可能紧凑。

#### short

```
commit <sha1>
Author: <author>

<title line>
```

#### medium

```
commit <sha1>
Author: <author>
Date: <author date>

<title line>

<full commit message>
```

#### full

```
commit <sha1>
Author: <author>
Commit: <committer>

<title line>

<full commit message>
```

#### fuller

```
commit <sha1>
Author: <author>
AuthorDate: <author date>
Commit: <committer>
CommitDate: <committer date>

<title line>

<full commit message>
```

#### email

```
From <sha1> <date>
From: <author>
Date: <author date>
Subject: [PATCH] <title line>

<full commit message>
```

#### raw

`raw`格式完全按照提交对象中存储的方式显示整个提交。值得注意的是，无论使用`--abbrev`还是`--no-abbrev`，SHA-1都会完整显示，且`parents`信息显示真实的父提交，而不考虑嫁接或历史简化。请注意，这种格式影响提交的显示方式，但不影响diff的显示方式（例如通过`git log --raw`）。要获取完整的对象名称，请使用`--no-abbrev`。

#### format:<string>

`format:<string>`格式允许你指定想要显示的信息。它的工作方式有点像`printf`，但一个异常是你获得的是换行符而不是`\n`。

例如，`format:"The author of %h was %an, %ar%nThe title was %s"`将显示类似：

```
The author of fe6e0ee was Junio Hamano, 23 hours ago

t419: test
```

占位符是：
- `%H`: 提交hash
- `%h`: 缩写的提交hash
- `%T`: 树hash
- `%t`: 缩写的树hash
- `%P`: 父提交hash
- `%p`: 缩写的父hash
- `%an`: 作者名
- `%aN`: 作者名（遵循`.mailmap`，见(1)或(1)）
- `%ae`: 作者邮箱
- `%aE`: 作者邮箱（遵循`.mailmap`，见(1)或(1)）
- `%ad`: 作者日期（`--date=`选项）
- `%aD`: 作者日期，RFC 2822格式
- `%ar`: 作者日期，相对时间
- `%at`: 作者日期，Unix时间戳
- `%ai`: 作者日期，ISO 8601格式
- `%aI`: 作者日期，严格ISO 8601格式
- `%cn`: 提交者名
- `%cN`: 提交者名（遵循`.mailmap`，见(1)或(1)）
- `%ce`: 提交者邮箱
- `%cE`: 提交者邮箱（遵循`.mailmap`，见(1)或(1)）
- `%cd`: 提交者日期（`--date=`选项）
- `%cD`: 提交者日期，RFC 2822格式
- `%cr`: 提交者日期，相对时间
- `%ct`: 提交者日期，Unix时间戳
- `%ci`: 提交者日期，ISO 8601格式
- `%cI`: 提交者日期，严格ISO 8601格式
- `%d`: 引用，类似于`--decorate`选项
- `%D`: 不带括号包裹的引用。
- `%e`: 编码
- `%s`: 主题
- `%f`: 安全的主题，适合文件名
- `%b`: 正文
- `%B`: 原始正文（未折行的主题和正文）
- `%N`: 提交注释
- `%GG`: 签名提交的GPG原始验证消息
- `%G?`: 显示"G"表示良好签名，“B"表示错误签名，“U"表示良好但不可信的签名，“N"表示无签名
- `%GS`: 显示签名提交的签名者名称
- `%GK`: 显示用于签名签名提交的密钥
- `%gD`: reflog选择器，例如`refs/stash@{1}`
- `%gd`: 简短的reflog选择器，例如`stash@{1}`
- `%gn`: reflog身份名称
- `%gN`: reflog身份名称（遵循`.mailmap`，参见(1)或(1)）
- `%ge`: reflog身份邮箱
- `%gE`: reflog身份邮箱（遵循`.mailmap`，参见(1)或(1)）
- `%gs`: reflog主题
- `%Cred`: 将颜色切换为红色
- `%Cgreen`: 将颜色切换为绿色
- `%Cblue`: 将颜色切换为蓝色
- `%Creset`: 重置颜色
- `%C(...)`: 颜色规格，如`color.branch.*`配置选项中描述的；在开头添加`auto`将仅在日志输出启用颜色时输出颜色（通过`color.diff`、`color.ui`或`--color`启用，并且如果目标是终端，则尊重前面的auto设置）。单独的`auto`（即`%C(auto)`）将在后续占位符处开启自动着色，直到颜色再次切换为止。
- `%m`: 左、右或边界标记
- `%n`: 换行
- `%%`: 原始的`%`
- `%x00`: 从十六进制代码打印字节
- `%w([<w>[,<i1>[,<i2>]])`: 切换行换行，类似于(1)的`-w`选项。
- `%<(<N>[,trunc|ltrunc|mtrunc])`: 使下一个占位符至少占据`N`列，必要时在右侧填充空格。如果输出超过`N`列，可以选择在开头（`ltrunc`）、中间（`mtrunc`）或结尾（`trunc`）截断。注意，截断仅在`N >= 2`时才能正常工作。
- `%<|(<N>)*`: 使下一个占位符至少占据到第`N`列为止，必要时在右侧填充空格
- `%>(<N>)*`, `%>|(<N>)*`: 分别类似于`%<(<N>)*`和`%<|(<N>)*`，但在左侧填充空格
- `%>>(<N>)*`, `%>>|(<N>)*`: 分别类似于`%>(<N>)*`和`%>|(<N>)*`，区别在于如果下一个占位符占据的空间比给定的多，且其左侧有空格
- `%><(<N>)*`, `%><|(<N>)*`: 分别类似于`%<(<N>)*`和`%<|(<N>)*`，但在两边都填充（即文本居中）

### 注意

某些占位符可能取决于传递给修订遍历引擎的其他选项。例如，`%g*` reflog选项除非我们在遍历reflog条目时（例如通过`git log -g`），否则插入空字符串。如果命令行上没有提供`--decorate`，则`%d`和`%D`占位符将使用“短”装饰格式。

如果在占位符的`%`之后添加`+`（加号），则当且仅当占位符展开为非空字符串时，在展开之前立即插入一个换行符。

如果在占位符的`%`之后添加`-`（减号），则当且仅当占位符展开为空字符串时，删除紧邻展开之前的换行符。

如果在占位符的`%`之后添加` `（空格），则当且仅当占位符展开为非空字符串时，在展开之前立即插入一个空格。

### tformat:

`tformat:`格式的工作原理与`format:`完全相同，不同在于它提供的是“终止符”语义而不是“分隔符”语义。换句话说，每个提交都附带了一个消息终止符字符（通常是换行符），而不是在条目之间放置分隔符。这意味着单行格式的最后一个条目将用新行正确结束，就像"oneline"格式一样。



```bash
$ git log -2 --pretty=format:%h 4da45bef \ | perl -pe '$_ .= " -- NO NEWLINE\n" unless /\n/'
4da45be
7134973 -- NO NEWLINE

$ git log -2 --pretty=tformat:%h 4da45bef \ | perl -pe '$_ .= " -- NO NEWLINE\n" unless /\n/'
4da45be
7134973
```

此外，任何包含 `%` 的未识别字符串都将被解释为前面带有 `tformat:`。例如，以下二者是等价的：

```bash
$ git log -2 --pretty=tformat:%h 4da45bef
$ git log -2 --pretty=%h 4da45bef
```

## 通用 diff

### `-p, -u, --patch`

生成补丁（参见生成补丁的章节）。

### `-s, --no-patch`

抑制 diff 输出。适用于像 `git show` 这样默认显示补丁的命令，或者为了取消 `--patch` 的效果。

### `-U<n>, --unified=<n>`

生成具有 `<n>` 行上下文的 diff，而不是通常的三行。这隐含了 `-p`。

### `--raw`

对于每个提交，使用原始（raw）格式显示更改摘要。参见 (1) 的“原始输出格式”部分。这与以原始格式显示日志本身不同，后者可以通过 `--format=raw` 实现。

### `--patch-with-raw`

`-p --raw` 的同义词。

### `--minimal`

花费额外时间以确保产生最小的 diff。

### `--patience`

使用“patience diff”算法生成 diff。

### `--histogram`

使用“histogram diff”算法生成 diff。

### `--diff-algorithm={patience|minimal|histogram|myers}`

选择一种 diff 算法。变体如下：

- `default, myers`

  基础的贪心 diff 算法。目前这是默认值。

- `minimal`

  花费额外时间以确保产生最小的 diff。

- `patience`

  在生成补丁时使用“patience diff”算法。

- `histogram`

  该算法扩展了 patience 算法以“支持低出现的公共元素”。例如，如果你将 `diff.algorithm` 变量配置为非默认值并想使用默认值，则必须使用 `--diff-algorithm=default` 选项。

### `--stat[=<width>[,<name-width>[,<count>]]]`

生成 diffstat。默认情况下，文件名部分将使用尽可能的空间，其余部分用于图表部分。最大宽度默认为终端宽度。可以通过第三个参数 `<count>` 限制输出前 `<count>` 行，如果更多，则显示 `...`。

这些参数也可以单独设置：`--stat-width=<width>`、`--stat-name-width=<name-width>` 和 `--stat-count=<count>`。

### `--numstat`

类似于 `--stat`，但使用十进制显示添加和删除的行数且省略路径。对于二进制文件，输出两个 `-` 而不是 `0`。

### `--shortstat`

仅输出 `--stat` 格式的最后一行，包含修改文件的总数以及添加和删除的行数。

### `--dirstat[=<param1,param2,...>]`

输出每个子目录更改的相对分布。`--dirstat` 的行为可以通过传递逗号分隔的参数列表进行自定义。默认由配置变量 `diff.dirstat` 控制（参见 (1)）。可用参数如下：

- `changes`

  通过计算 dirstat 数字。这忽略文件内部的纯代码移动。换句话说，文件中重新排列行的计数与其他更改相同。这是未提供参数时的默认行为。

- `lines`

  通过执行常规的 diff 分析并累加删除/添加的数来计算 dirstat 数字。（对于二进制文件，计算 64 字节块，因为二进制文件没有自然的行概念）。这是比 changes 行为更消耗资源的 `--dirstat` 行为，但它将文件中重新排列行的计数与其他更改相同。其输出结果与其他 `--*stat` 选项的结果一致。

- `files`

  通过计算更改文件的数量来计算 dirstat 数字。每个更改的文件在 dirstat 分析中权重相等。这是计算成本最低的 `--dirstat` 行为，因为它完全不需要查看文件内容。

- `cumulative`

  将子目录的更改也计入父目录。注意，当使用累计时，报告的百分比可能超过 100%。默认（非累计）行为可以通过 `noncumulative` 参数指定。

一个整数参数用于指定截断百分比（默认为 3%）。更改少于此百分比的目录将不会在输出中。

示例：以下命令将统计更改的文件，同时忽略更改文件数少于总量 10% 的目录，并将子目录计数累计到父目录中：`--dirstat=files,10,cumulative`。

### `--summary`

输出扩展头部信息的简要摘要，例如创建、重命名和模式更改。

### `--patch-with-stat`

`-p` `--stat` 的别名。

### `-z`

使用 NUL（空字符）分隔提交，而不是新的换行符。

此外，当给出 `--raw` 或 `--numstat` 时，不要混淆路径，并使用 NUL 作为输出字段的终止符。

如果没有此选项，输出的每个路径名中的 TAB、LF、双引号和反斜杠将被分别替换为 `\t`、`\n`、`\"` 和 `\\`。如果发生了任何一种替换，路径名将被双引号括起来。

### `--name-only`

仅显示更改的文件名。

### `--name-status`

仅显示更改的文件名和状态。有关状态字母的含义，请参见 `--diff-filter` 选项的描述。

### `--submodule[=<format>]`

指定子模块差异的显示方式。当给出 `--submodule` 或 `--submodule=log` 时，使用 `log` 格式。该格式像 `summary` 一样列出范围内的提交。省略 `--submodule` 选项或指定 `--submodule=short` 则使用 `short` 格式。该格式仅显示范围开始和结束的提交名称。可以通过 `diff.submodule` 配置变量进行调整。

### `--color[=<when>]`

显示彩色差异。`--color`（即不带 `=<when>`）等同于 `--color=always`。`<when>` 可以是 `always`、`never` 或 `auto` 其中之一。

### `--no-color`

关闭彩色差异。它等同于 `--color=never`。

### `--word-diff[=<mode>]`

显示单词差异，使用 `<mode>` 来分隔更改的单词。默认情况下，单词由空白符分隔；见下文的 `--word-diff-regex`。`<mode>` 默认为 `plain`，且必须是以下之一：

- `color`

  仅使用颜色高亮更改的单词。隐含 `--color`。

- `plain`

  以 `[-removed-]` 和 `{+added+}` 显示单词。如果输入中出现分隔符，则不尝试对其进行转义，因此输出可能具有歧义性。

- `porcelain`

  使用一种用于脚本解析的特殊行级格式。添加/删除/未更改的运行将按标准的统一差异格式打印，行首以 `+`、`-` 或空格字符开头并延伸到行尾。输入中的换行符由单独占一行的波浪号 `~` 表示。

- `none`

  再次禁用单词差异。

注意，尽管第一个模式的名称带有 color，但在启用了颜色的情况下，所有模式下都会使用颜色来高亮更改部分。

### `--word-diff-regex=<regex>`

使用 `<regex>` 来判断什么是单词，而不是将连续的非空白字符视为单词。除非已启用，否则它也会隐含 `--word-diff`。

`<regex>` 的每个不重叠匹配项都被视为一个单词。这些匹配项之间的任何内容都被视为空白符，并在查找差异时被忽略（`!`）。你可能想在正则表达式后面附加 `|[^[:space:]]` 以确保它匹配所有非空白字符。包含换行符的匹配会在换行符处静默截断（`!`）。

正则也可以通过 diff 驱动程序或配置选项设置，见 (1) 或 (1)。显式提供将覆盖任何 diff 驱动程序或配置设置。diff 驱动程序覆盖配置设置。

### `--color-words[=<regex>]`

等同于 `--word-diff=color` 加上（如果指定了正则）`--word-diff-regex=<regex>`。

### `--no-renames`

关闭重命名检测，即使配置文件默认开启。

### `--check`

如果更改引入了空白错误，则警告。什么是空白错误由 `core.whitespace` 配置控制。默认情况下，尾部空格（包括仅由空白组成的行）以及行初始缩进内紧随制表符的空格字符被视为空白错误。如果发现问题，则以非零状态退出。与 `--exit-code` 不兼容。

### `--ws-error-highlight=<kind>`

以 `color.diff.whitespace` 指定颜色高亮 `<kind>` 指定行的空白错误。`<kind>` 是 `old`、`new`、`context` 的用逗号分隔的列表。当未给出此选项时，仅高亮新行中的空白错误。例如，`--ws-error-highlight=new,old` 会高亮被删除和添加行的空白错误。`all` 均可作为 `old`、`new`、`context` 的简写。

### `--full-index`

在生成补丁格式输出时，在“index”行上显示完整的镜像和后镜像 blob 对象名称，而不是前几个字符。

### `--binary`

除了 `--full-index` 之外，输出可以使用 `git-apply` 应用的二进制差异。

### `--abbrev[=<n>]`

在 diff-raw 格式输出和 diff-tree 头文件中，不再显示完整的 40 字节十六进制对象名称，而是显示部分前缀。这与上述 `--full-index` 选项独立，后者控制 diff-patch 输出格式。可以通过 `--abbrev=<n>` 指定非默认的数字位数。

### `-B[<n>][/<m>], --break-rewrites[=[<n>][/<m>]]`

将完全重写的更改拆分为删除和创建的对。这有两个用途：

1. 它影响了相当于文件完全重写的更改的处理方式，使其不是一系列删除和插入与少数在文本上恰好匹配上下文的行混合在一起，而是一次性删除所有旧内容，随后一次性插入所有新内容。数字 `m` 控制 `-B` 选项的这方面（默认为 60%）。`-B/70%` 指定如果结果中保留少于原始内容的 30%，则 Git 认为其为完全重写（即：否则结果生成的补丁将是一系列带有上下文行的删除和插入的混合）。

2. 当与 `-M` 一起使用时，完全重写的文件也被视为重命名的源（通常 `-M` 只考虑消失的文件作为重命名的源），数字 `n` 控制 `-B` 选项的这方面（默认为 50%）。`-B20%` 指定与文件大小相比，添加和删除达到文件大小的 20% 或比例的更改，有资格被选为重命名到另一个文件的可能源。

### `-M[<n>], --find-renames[=<n>]`

在生成差异时，为每个提交检测并报告重命名。在遍历历史时跨越重命名跟踪后续文件，请参见 `--follow`。如果指定了 `n`，它是相似性索引的阈值（即与文件大小相比的添加/删除量）。例如，`-M90%` 意味着如果文件超过 90% 没有发生变化，Git 应该将一个删除/添加对视为重命名。如果没有 `%` 号，该数字被读为分数，前面带有一个小数点。即，`-M5` 变为 0.5，因此与 `-M50%` 相同。同样，`-M05` 等同于 `-M5%`。要将检测限制为精确重命名，请使用 `-M100%`。默认相似性索引为 50%。

### `-C[<n>], --find-copies[=<n>]`

检测复制以及重命名。见 `--find-copies-harder`。如果指定了 `n`，其含义与 `-M<n>` 相同。

### `--find-copies-harder`

出于性能考虑，默认情况下，`-C` 选项仅当复制的原文件在同一更改集中被修改时才查找复制。此标志使命令检查未修改的文件作为复制源的候选对象。对于大型项目，这是一个非常昂贵的操作，请谨慎使用。提供多个 `-C` 选项效果相同。

### `-D, --irreversible-delete`

省略删除操作的原始映像（preimage），即只打印头部，但不打印原始映像与 `/dev/null` 之间的差异。生成的补丁并非用于 `patch` 或 `git apply`；它仅适用于那些只想在更改后专注于审查文本的人。此外，输出内容显然缺乏反向应用此类补丁所需的信息（即使手动操作也不行），这也是该选项命名的由来。

与 `-B` 配合使用时，省略删除/创建对中删除部分的原始映像。

### `-l<num>`

`-M` 和 `-C` 选项需要 `O(n²)` 的处理时间，其中 `n` 是潜在重命名/复制目标的数量。当重命名/拷贝目标超过指定数量时，此选项将防止重命名/拷贝检测运行。

### `--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]`

仅选择已添加（A）、复制（C）、删除（D）、修改（M）、重命名（R）、类型（即普通文件、符号链接、子模块等）改变（T）、未合并（U）、未知（X）或配对已破坏（B）的文件。可以使用过滤器字符的任意组合（包括无）。当在组合中添加 `*`（全有全无）时，如果比较中存在任何文件符合其他标准，则选择所有路径；如果没有文件符合其他标准，则不选择任何内容。

### `-S<string>`

查找文件中指定字符串出现次数发生变化（即添加/删除）的差异。供脚本编写人员使用。

当你正在寻找一段精确的代码块（如结构体），并想知道该块自首次出现以来的历史时，这非常有用：反复使用该功能将原始映像中感兴趣块馈回 `-S`，并持续直到获取该块的最早版本。

### `-G<regex>`

查找补丁文本中包含匹配 `<regex>` 的添加/删除行的差异。

为了说明 `-S<regex> --pickaxe-regex` 与 `-G<regex>` 之间的区别，请考虑一个在同一文件中具有以下差异的提交：

```diff
+ return !regexec(regexp, two->ptr, 1, &regmatch, 0);
...
- hit = !regexec(regexp, mf2.ptr, 1, &regmatch, 0);
```



虽然 `git log -G"regexec\(regexp"` 会显示此提交，但 `git log -S"regexec\(regexp" --pickaxe-regex` 则不会（因为该字符串的出现次数没有变化）。

更多信息请见 (7) 中的 `pickaxe` 条目。

### `--pickaxe-all`

当 `-S` 或 `-G` 找到更改时，显示该变更集中所有的更改，而不仅仅是包含 `<string>` 更改的文件。

### `--pickaxe-regex`

将传递给 `-S` 的 `<string>` 视为扩展 POSIX 正则表达式进行匹配。

### `-O<orderfile>`

按照 `<orderfile>` 中顺序输出补丁，该文件每行包含一个 shell glob 模式。这会覆盖 `diff.orderFile` 配置变量（见 (1)）。要取消 `diff.orderFile`，请使用 `-O/dev/null`。

### `-R`

交换两个输入；即显示从索引或磁盘文件到树内容的差异。

### `--relative[=<path>]`

当在项目的子目录下运行时，可以通过此选项告诉它排除目录外的更改，并显示相对于该目录的路径。当你不在子目录中（例如在裸仓库中）时，可以通过提供参数 `<path>` 来指定相对于哪个子目录输出。

### `-a, --text`

将所有文件视为文本。

### `--ignore-space-at-eol`

忽略行尾（EOL）空格的更改。

### `-b, --ignore-space-change`

忽略空格数量的变化。这会忽略行尾的空格，并将所有其他一个或多个空白字符序列视为等效。

### `-w, --ignore-all-space`

在比较行时忽略空格。即使其中一行有空格而另一行没有，也会忽略差异。

### `--ignore-blank-lines`

忽略所有行均为空行的更改。

### `--inter-hunk-context=<lines>`

显示差异块（hunks）之间的上下文，最多到指定的行数，从而融合彼此的差异块。

### `-W, --function-context`

显示更改周围的完整函数。

### `--ext-diff`

允许执行外部 diff 助手。如果你通过 (5) 设置了外部 diff 驱动程序，则需要配合 (1) 等选项使用此选项。

### `--no-ext-diff`

禁止外部 diff 驱动程序。

### `--textconv, --no-textconv`

在比较二进制文件时允许（或禁止）运行外部文本转换过滤器。详情见 (5)。由于 `textconv` 过滤器通常是单向转换，生成的差异适用于人类阅读，但无法被应用。由于此原因，`textconv` 过滤器默认仅对 (1) 和 (1) 启用，而未对 (1) 或 diff 管道命令启用。

### `--ignore-submodules[=<when>]`

在生成 diff 时忽略对子模块的更改。`<when>` 可以是 `"none"`、`"untracked"`、`"dirty"` 或 `"all"`，默认为 `"all"`。使用 `"none"` 时，当子模块包含未跟踪或已修改的文件，或者其 HEAD 与主项目记录的提交不同时，会将子模块视为已修改，这可用于覆盖 (1) 或 (5) 中 `ignore` 选项的任何设置。

当使用 `"untracked"` 时，如果子模块仅包含未跟踪的内容，则不会被视为脏（但仍会扫描已修改的内容）。使用 `"dirty"` 会忽略对子模块工作树的所有更改，仅显示存储在主项目中的提交的更改（这是 1.7.0 之前的行为）。使用 `"all"` 则隐藏对子模块的所有更改。

### `--src-prefix=<prefix>`

显示指定的源前缀代替 `"a/"`。

### `--dst-prefix=<prefix>`

显示指定的目标前缀代替 `"b/"`。

### `--no-prefix`

不显示任何源或目标前缀。

关于这些常用选项的更详细解释，请参阅 (7)。

## 使用 `-P` 生成补丁

当运行 `git-diff-index`、`git-diff-tree` 或 `git-diff-files` 并带有 `-p` 选项，或者不带 `--raw` 选项的 `git diff` 或带有 `-p` 选项的 `git log`，它们不会产生上述输出；而是产生一个补丁文件。你可以通过 `GIT_EXTERNAL_DIFF` 和 `GIT_DIFF_OPTS` 环境变量自定义此类补丁的创建。

`-p` 选项产生的内容与传统的 diff 格式略有不同：

1. 它前面有一个像这样的 `"git diff"` 头部：

```text
diff --git a/file1 b/file2
```

除非涉及重命名/复制，否则 `a/` 和 `b/` 文件名是相同的。特别是即使对于创建或删除，也不会用 `/dev/null` 代替 `a/` 或 `b/` 文件名。

当涉及重命名/复制时，`file1` 和 `file2` 分别显示重命名/复制的源文件名和重命名/复制产生的文件名。

2. 后面跟着一个或多个扩展头部行：

```text
old mode <mode>
new mode <mode>
deleted file mode <mode>
new file mode <mode>
copy from <path>
copy to <path>
rename from <path>
rename to <path>
similarity index <number>
dissimilarity index <number>
index <hash>..<hash> <mode>
```

文件模式以 6 位进制数打印，包括文件类型和权限位。

扩展头部中的路径不包含 `a/` 和 `b/` 前缀。

相似性索引是未更改行的百分比，不相似性索引（dissimilarity index）是更改行的百分比。它是一个向下取整的整数，后跟一个百分号。因此，相似性索引值 100% 留给两个相同的文件，而 100% 的不相似性意味着旧文件中的没有任何行被带到新文件中。

索引行包含了更改前后的 SHA-1 校验和。如果文件模式没有更改，则包含 `<mode>`；否则，用单独的行表示旧新模式。

3. 路径中的 TAB、LF、双引号和反斜杠字符分别表示为 `\t`、`\n`、`\"` 和 `\\`。如果需要此类替换，整个路径将放在双引号中。

4. 输出中所有的 `file1` 文件均指 commit 之前的文件，而所有的 `file2` 文件均指 commit 之后的文件。将每个更改顺序应用到每个文件是不准确的。例如，此补丁将交换 `a` 和 `b`：

```diff
diff --git a/a b/b
rename from a
rename to b
diff --git a/b b/a
rename from b
rename to a
```

## 合并 diff 格式（COMBINED DIFF FORMAT）

任何生成 diff 的命令都可以接受 `-c` 或 `--cc` 选项，在显示合并时产生合并 diff（combined diff）。这是显示带有 (1) 或 (1) 的合并时的默认格式。请注意，你也可以给这些命令中的任何一个提供 `-m` 选项，以强制生成相对于合并单个父节点的 diff。

合并 diff 格式如下：

```text
diff --combined describe.c
index fabadb8,cc95eb0..4866510
--- a/describe.c
+++ b/describe.c
@@@ -98,20 -98,12 +98,20 @@@
 return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1;
} - static void describe(char *arg)
-static void describe(struct commit *cmit, int last_one)
++static void describe(char *arg, int last_one)
{
+ unsigned char sha1[20];
+ struct commit *cmit;
struct commit_list *list;
static int initialized = 0;
struct commit_name *n;
+ if (get_sha1(arg, sha1) < 0)
+ usage(describe_usage);
+ cmit = lookup_commit_reference(sha1);
+ if (!cmit)
+ usage(describe_usage);
+ if (!initialized) {
initialized = 1;
for_each_ref(get_name);
```

1. 它前面带有一个 `"git diff"` 头部，如下所示（当使用 `-c` 选项时）：

```text
diff --combined file
```

或者如下（当使用 `--cc` 选项时）：

```text
diff --cc file
```

2. 后面跟着一个或多个扩展头部的行（此示例显示了一个具有两个父节点的合并）：

```text
index <hash>,<hash>..<hash>
mode <mode>,<mode>..<mode>
new file mode <mode>
deleted file mode <mode>,<mode>
```

只有当至少有一个 `<mode>` 与其他不同时，才会出现 `<mode>,<mode>..<mode>` 这一行。带有检测到的内容移动（重命名和复制检测）信息的扩展头部旨在用于两个 `<tree-ish>` 之间的 diff，不被合并 diff 格式使用。

3. 后面跟着两行的源文件/目标文件头部：

```text
--- a/file
+++ b/file
```

与传统的 `unified` diff 格式的双行头部类似，`/dev/null` 用于指示创建或删除的文件。

4. 块头部（Chunk header）格式经过修改，以防止人们意外传递给 `patch -p1`。合并 diff 格式是为了审查合并提交的更改而设计的，并非用于应用。该更改与扩展 `index` 头部的更改相似：

```text
@@@@ <from-file-range> <from-file-range> <to-file-range> @@@
```

合并 diff 格式的块头部中有（父节点数量 + 1）个 `@` 字符。

传统的 `unified` diff 格式不同，它显示两个文件 `A` 和 `B`，并带有一列 `-`（减号——出现在 `A` 中但在 `B` 中移除）、`+`（加号——在 `A` 中缺失但在 `B` 中添加）或 `" "`（空格——未更改）前缀；而这种格式将两个或多个文件 `file1`、`file2`、……与一个文件 `X` 进行比较，并显示 `X` 与每个 `fileN` 的差异。输出行前面为每个 `fileN` 留有一列，以说明 `X` 的行与其何不同。

列 `N` 中的 `-` 字符意味着该行出现在 `fileN` 中但未出现在结果中。列 `N` 中的 `+` 字符意味着该行出现在结果中，而 `fileN` 没有该行（换句话说，从该父节点的角度来看，该行被添加了）。

在上面的示例输出中，函数签名在两个文件中发生了变化（因此在 `file1` 和 `file2` 中都有两个 `-` 移除，加上 `++` 表示添加的行既未出现在 `file1` 也未出现在 `file2`）。此外，其他八行与 `file1` 相同但未出现在 `file2` 中（因此带有 `+` 前缀）。

当通过 `git diff-tree -c` 显示时，它比较合并提交的父节点与合并结果（即 `file1..fileN` 是父节点）。当通过 `git diff-files -c` 显示时，它比较两个未解析的合并父节点与工作树文件（即 `file1` 是阶段 2，即“我们的版本”，`file2` 是阶段 3，即“他们的版本”）。

## 示例

```shell
git log --no-merges
```

显示整个提交历史，但跳过任何合并。

```shell
git log v2.6.12.. include/scsi drivers/scsi
```

显示自版本 `v2.6.12` 以来更改了 `include/scsi` 或 `drivers/scsi` 中任何文件的所有提交。

显示日志时使用的编码。（参见上文的 *Discussion*）。如果设置了 `i18n.commitEncoding`，则默认使用该值，否则使用 UTF-8。

### `log.date`

人类可读日期的默认格式。（对比 `--date` 选项）。默认值为 `"default"`，意味着输出类似 `Sat May 8 19:35:34 2010 -0500` 的日期格式。

### `log.showRoot`

如果为 `false`，`git log` 和相关命令将不会将初始提交视为大的创建事件。在 `git log -p` 输出中，任何根提交将显示但不附带差异（diff）。默认为 `true`。

### `mailmap.*`

参见 (1)。

### `notes.displayRef`

在用 log 族命令显示提交消息时，除了 `core.notesRef` 或 `GIT_NOTES_REF` 设置的默认集外，还从哪些 ref 读取注释。参见 (1)。

可以是未缩写的 ref 名称或通配符（glob），并且可以多次指定。对于不存在的 ref 将发出警告，但不匹配任何 ref 的通配符将被静默忽略。

此设置可以通过 `--no-notes` 选项禁用，被 `GIT_NOTES_DISPLAY_REF` 环境变量覆盖，并被 `--notes=<ref>` 选项覆盖。

***

# GIT-LS-FILES

## 名称

`git-ls-files` - 显示索引和工作树中的文件信息

## 语法概要

```text
git ls-files [-z] [-t] [-v] (--[cached|deleted|others|ignored|stage|unmerged|killed|modified])* (-[c|d|o|i|s|u|k|m])* [-x <pattern>|--exclude=<pattern>] [-X <file>|--exclude-from=<file>] [--exclude-per-directory=<file>] [--exclude-standard] [--error-unmatch] [--with-tree=<tree-ish>] [--full-name] [--abbrev] [--] [<file>...]
```



## 描述

此命令将目录缓存索引的文件列表与实际的工作目录列表合并，并显示两者的不同组合。

可以使用以下一个或多个选项来确定显示的文件：

### 选项

- `-c, --cached`  
  在输出中显示缓存文件（默认）。
- `-d, --deleted`  
  在输出中显示已删除的文件。
- `-m, --modified`  
  在输出中显示已修改的文件。
- `-o, --others`  
  在输出中显示其他文件（即未跟踪的文件）。
- `-i, --ignored`  
  在输出中仅显示被忽略的文件。在显示索引中的文件时，仅打印匹配排除模式的文件。在显示“其他”文件时，仅显示匹配排除模式的文件。
- `-s, --stage`  
  在输出中显示暂存内容的对象名称、模式位和阶段号。
- `--directory`  
  如果整个目录被归类为“其他”，则只显示其名称（带有末尾正斜杠），而不是其全部内容。
- `--no-empty-directory`  
  不列出空目录。在没有使用 `--directory` 时没有效果。
- `-u, --unmerged`  
  在输出中显示未合并的文件（强制使用 `--stage`）。
- `-k, --killed`  
  显示文件由于文件/目录冲突导致 `checkout-index` 无法成功而需要删除的文件。
- `-z`  
  输出中使用 `\0` 换终止。
- `-x <pattern>, --exclude=<pattern>`  
  跳过匹配模式的未跟踪文件。注意模式是 shell 通配符模式。更多信息见下文的 EXCLUDE PATTERNS。
- `-X <file>, --exclude-from=<file>`  
  从 `<file>` 读取排除模式；每行一个。
- `--exclude-per-directory=<file>`  
  从 `<file>` 读取仅适用于该目录及其子目录的额外排除模式。
- `--exclude-standard`  
  添加标准的 Git 排除项：`.git/info/exclude`、每个目录下的 `.gitignore` 以及用户的全局排除文件。
- `--error-unmatch`  
  如果任何 `<file>` 不在索引中，则将其视为错误（返回 1）。
- `--with-tree=<tree-ish>`  
  当使用 `--error-unmatch` 将用户提供的 `<file>`（即路径模式）参数扩展为路径时，假定自命名的 `<tree-ish>` 之后在索引中删除的路径仍然存在。与 `-s` 或 `-u` 选项配合使用此选项没有意义。
- `-t`  
  此功能已半弃用。为了脚本目的，(1)--porcelain 和 (1)--name-status 几乎总是更好的替代方案，用户应该查看 (1)--short 或 (1)--name-status 获取更用户友好的替代方案。

  此选项在每行开头通过以下标记（后跟空格）标识文件状态：

  - `H`: cached
  - `S`: skip-worktree
  - `M`: unmerged
  - `R`: removed/deleted
  - `C`: modified/changed
  - `K`: to be killed
  - `?`: other

- `-v`  
  与 `-t` 类似，但对标记为 assume unchanged（假设未更改，参见 (1)）的文件使用小写字母。
- `--full-name`  
  当从子目录运行时，命令通常输出相对于当前目录的路径。此选项强制输出相对于项目根目录的路径。
- `--abbrev[=<n>]`  
  不显示完整的 40 字节十六进制对象行，而是只显示部分前缀。可以使用 `--abbrev=<n>` 指定非默认的数字位数。
- `--debug`  
  在每个描述文件的行之后，添加关于其缓存条目的更多数据。这旨在尽可能显示信息以便进行手动检查；具体格式可能会随时更改。
- `--`  
  不再将任何后续参数解释为选项。
- `<file>`  
  要显示的文件。如果没有给出文件，则显示所有符合其他指定标准的文件。

## 输出

`git ls-files` 仅输出文件名，除非指定了 `--stage`，此时会输出：

```text
[<tag> ]<mode> <object> <stage> <file>
```

`git ls-files --unmerged` 和 `git ls-files --stage` 可用于检查未合并路径的详细信息。

对于未合并的路径，索引不是记录单个模式/SHA-1 对，而是记录多达三个这样的对；分别来自阶段 1 的树 `O`、阶段 2 的 `A` 和阶段 3 的 `B`。这些信息可以供用户（或 porcelain 命令）使用，以查看最终应该在该路径记录的内容。（有关状态的更多信息参见 (1)。）

当不使用 `-z` 选项时，路径中的 TAB、LF 和反斜杠字符分别表示为 `\t`、`\n` 和 `\\`。

## 排除模式

`git ls-files` 在遍历目录树并在指定标记 `--others` 或 `--ignored` 时查找要显示的文件时，可以使用“排除模式”列表。(5) 规定了排除模式的格式。

这些排除模式按以下顺序来自这些地方：

1. 命令行标记 `--exclude=<pattern>` 指定单个模式。模式的顺序与它们在命令行中出现的顺序相同。
2. 命令行标记 `--exclude-from=<file>` 指定一个包含模式列表的文件。模式的顺序与它们在文件中出现的顺序相同。
3. 命令行标记 `--exclude-per-directory=<name>` 指定 `git ls-files` 检查的每个目录中的文件名，通常为 `.gitignore`。深层目录的文件具有优先级。模式的顺序与它们在文件中出现的顺序相同。

在命令行上通过 `--exclude` 指定的模式或从 `--exclude-from` 指定的文件读取的模式相对于目录树顶部。从 `--exclude-per-directory` 指定的文件读取的模式相对于模式文件所在的目录。

## 参见

(1), (5)

***

# GIT-LS-REMOTE

## 名称

`git-ls-remote` - 列出远程仓库中的引用

## 语法概要

```text
git ls-remote [--heads] [--tags] [-u <exec> | --upload-pack <exec>] [--exit-code] <repository> [<refs>...]
```

## 描述

显示远程仓库中提供的引用以及相关的提交 ID。

### 选项

- `-h, --heads, -t, --tags`  
  分别限制为 `refs/heads` 和 `refs/tags`。这些并不互斥；当同时给出时，显示存储在 `refs/heads` 和 `refs/tags` 中的引用。
- `-u <exec>, --upload-pack=<exec>`  
  指定远程主机 `git-upload-pack` 的完整路径。这允许列出通过 SSH 访问且 SSH 守护进程未使用用户配置的 PATH 的仓库引用。
- `--exit-code`  
  在远程仓库未找到匹配引用时以状态 2 退出。通常命令以状态 0 退出，表示已与远程仓库通信，无论是否找到匹配的引用。
- `--get-url`  
  考虑到任何 `"url.<base>.insteadOf"` 配置设置（参见 (1)），扩展给定的远程仓库的 URL 并在不与远程通信的情况下退出。

`<repository>`

要查询的“远程”仓库。此参数可以是 URL 也可以是远程的名称（参见 (1) 中的 `GIT URLS` 和 `REMOTES` 章节）。

`<refs>...`

如果未指定，将显示经过 `--heads` 和 `--tags` 过滤后的所有引用。当指定了 `<refs>...` 时，则仅显示匹配给定模式的引用。

## 示例

```shell
$ git ls-remote --tags ./. d6602ec5194c87b0fc87103ca4d67251c76f233a refs/tags/v0.99 f25a265a342aed6041ab0cc484224d9ca54b6f41 refs/tags/v0.99.1 7ceca275d047c90c0c7d5afb13ab97efdf51bd6e refs/tags/v0.99.3 c5db5456ae3b0873fc659c19fafdde22313cc441 refs/tags/v0.99.2 0918385dbd9656cab0d1d81ba7453d49bbc16250 refs/tags/junio-gpg-pub

$ git ls-remote master pu rc 5fe978a5381f1fbad26a80e682ddd2a401966740 refs/heads/master c781a84b5204fb294c9ccc79f8b3baceeb32c061 refs/heads/pu

$ git remote add korg

$ git ls-remote --tags korg v\* d6602ec5194c87b0fc87103ca4d67251c76f233a refs/tags/v0.99 f25a265a342aed6041ab0cc484224d9ca54b6f41 refs/tags/v0.99.1 c5db5456ae3b0873fc659c19fafdde22313cc441 refs/tags/v0.99.2 7ceca275d047c90c0c7d5afb13ab97efdf51bd6e refs/tags/v0.99.3
```

# GIT-LS-TREE

## 名称

`git-ls-tree` - 列出树对象的内容

## 语法

`git ls-tree [-d] [-r] [-t] [-l] [-z] [--name-only] [--name-status] [--full-name] [--full-tree] [--abbrev[=<n>]] <tree-ish> [<path>...]`

## 描述

列出给定树对象的内容，类似于在当前工作目录下执行 `"/bin/ls -a"`。注意：

其行为与 `"/bin/ls"` 略有不同，因为 `<path>` 仅表示匹配的模式列表，例如，指定目录名称（不带 `-r`）的行为会有所不同，且参数的顺序并不重要。

其行为与 `"/bin/ls"` 相似，因为 `<path>` 被视为相对于当前工作目录的路径。例如，当你处于一个包含目录 `dir` 的目录 `sub` 中时，你可以运行 `git ls-tree -r HEAD dir` 来列出树的内容（即 `HEAD` 中的 `sub/dir`）。在这种情况下，你不应该提供一个不在根层级的树（例如 `git ls-tree -r HEAD:sub dir`），因为这会导致在 `HEAD` 提交中请求 `sub/sub/dir`。然而，可以通过传递 `--full-tree` 选项来忽略当前工作目录。

## 参数

`<tree-ish>`

树对象的 ID。

`-d`

仅显示命名的树项本身，不显示其子项。

`-r`

递归进入子树。

`-t`

即使在进行递归时也显示树项。如果没有传递 `-r`，则没有效果。`-d` 隐含 `-t`。

`-l, --long`

显示 blob（文件）项的对象大小。

`-z`

输出时使用 `\0` 行终止符。

`--name-only, --name-status`

仅列出文件名（而不是“详细”输出），每行一个。

`--abbrev[=<n>]`

不显示完整的 40 字节十六进制对象行，而是只显示部分前缀。可以使用 `--abbrev=<n>` 指定非默认的位数。

`--full-name`

不显示相对于当前工作目录的路径，而是显示完整路径名称。

`--full-tree`

不将列表限制在当前工作目录。隐含 `--full-name`。

`[<path>...]`

当给定路径时，显示它们（注意这并不是原始路径名，而是匹配的模式列表）。否则，隐式使用树的根层级作为唯一的路径参数。

## 输出格式

`<mode> SP <type> SP <object> TAB <file>`

除非使用 `-z` 选项，否则路径中的 TAB、LF 和反斜杠字符分别表示为 `\t`、`\n` 和 `\\`。此输出格式与 `git update-index --index-info --stdin` 的期望兼容。

当使用 `-l` 选项时，格式变为：

`<mode> SP <type> SP <object> SP <object size> TAB <file>`

由 `<object>` 标识的对象大小以字节给出，并右对齐，最小宽度为 7 个字符。对象大小适用于 blob（文件）项；对于其他项，使用字符代替大小。

# GIT-MAILSPLIT

## 名称

`git-mailsplit` - 简单的 UNIX mbox 分割程序

## 语法

`git mailsplit [-b] [-f<nn>] [-d<prec>] [--keep-cr] -o<directory> [--] [(<mbox>|<Maildir>)...]`

## 描述

将 mbox 文件或 Maildir 分割为指定目录的文件列表："0001"、"0002"……以便你可以从那里进行进一步处理。

**重要**

Maildir 分割依赖于文件名排序，以便按正确的顺序输出补丁。

## 参数

`<mbox>`

要分割的 mbox 文件。如果未给出，则从标准输入读取 mbox。

`<Maildir>`

要分割的 Maildir 根目录。该目录应包含 `cur`、`tmp` 和 `new` 子目录。

`-o<directory>`

放置单个消息的目录。

`-b`

如果任何文件不以 `From` 行开头，则假设它是单条邮件消息而不是信号错误。

`-d<prec>`

与默认的 4 位前导零不同，可以为生成的文件名指定不同的精度。

`-f<nn>`

跳过前 `<nn>` 个数字，例如，如果指定了 `-f3`，则从 `0004` 开始编号。

`--keep-cr`

不删除以 `\r\n` 结尾的行中的 `\r`。

# GIT-MERGE-BASE

## 名称

`git-merge-base` - 为合并寻找尽可能佳的共同祖先

## 语法

```text
git merge-base [-a|--all] <commit> <commit>...
git merge-base [-a|--all] --octopus <commit>...
git merge-base --is-ancestor <commit> <commit>
git merge-base --independent <commit>...
git merge-base --fork-point <ref> [<commit>]
```

## 描述

`git merge-base` 在两个提交之间寻找最佳共同祖先，以用于三路合并。如果一个共同祖先是另一个共同祖先的祖先，则后一个比前者更好。一个没有任何更佳共同祖先的共同祖先就是最佳共同祖先，即合并基准（merge base）。注意，一对提交可能存在多个合并基准。

## 模式

作为最常见的特殊情况，在命令行上仅指定两个提交意味着计算给定两个提交之间的合并基准。

更通地说，在要计算合并基准的两个提交之间，一个由第一个提交参数指定；另一个提交是命令行上剩余提交的（假设的）提交。

结果是，当指定多个提交时，合并基准并不在每个提交参数中。这与使用 `merge-base` 选项时与 (1) 不同。

`--octopus`

为所有提交计算最佳共同祖先，为 n 路合并做准备。这模拟了 `git show-branch --merge-base` 的行为。

`--independent`

不是打印合并基准，而是打印相同提交的最小子集。也就是说，在给定的提交中，列出无法从其他提交到达的提交。这模拟了 `git show-branch --independent` 的行为。

`--is-ancestor`

检查第一个 `<commit>` 是否是第二个 `<commit>` 的祖先，如果是则以状态 0 退出，否则以状态 1 退出。错误通过非 1 的零状态信号。

`--fork-point`

寻找分支（或任何指向 `<commit>` 的历史）从另一个分支（或任何引用）`<ref>` 分叉的点。这不仅寻找两个提交的共同祖先，还考虑 `<ref>` 的 reflog，以查看指向 `<commit>` 的历史是否是从分支 `<ref>` 的早期版本分支的（参见下面的讨论）。

## 参数

`-a, --all`

输出提交的所有合并基准，而只有一个。

## 讨论

给定两个提交 `A` 和 `B`，`git merge-base A B` 将输出父关系从 `A` 和 `B` 到达的提交。

例如，具有如下拓扑结构：

```text
o---o---o---B
/
---o---1---o---o---o---A
```

`A` 和 `B` 之间的合并基是 `1`。

给定三个提交 `A`、`B` 和 `C`，`git merge-base A B C` 将计算 `A` 与假设提交 `M` 之间的合并基，其中 `M` 是 `B` 和 `C` 的合并。例如，具有如下拓扑结构：

```text
o---o---o---o---C
/ /
o---o---o---B
/
---2---1---o---o---o---A
```

`git merge-base A B C` 的结果是 `1`。这是因为在 `B` 和 `C` 之间存在合并提交 `M` 的等效拓扑结构为：

```text
o---o---o---o---o
\ /
o---o---o---o---M
/
---2---1---o---o---o---A
```

`git merge-base A M` 的结果是 `1`。提交 `2` 也是 `A` 和 `M` 的共同祖先，但 `1` 是更好的共同祖先，因为 `2` 是 `1` 的祖先。因此，`2` 不是合并基。

`git merge-base --octopus A B C` 的结果是 `2`，因为 `2` 是所有提交的最优共同祖先。

当历史涉及交叉合并（criss-cross merges）时，两个提交可能存在多个最佳共同祖先。例如，具有如下拓扑结构：

```text
---1---o---A
\ /
X
/ \
---2---o---o---B
```



`1` 和 `2` 都是 `A` 和 `B` 的合并基。它们互不优（都是最佳合并基）。在没有给出 `--all` 选项的情况下，未指定输出哪一个最佳。

检查两个提交 `A` 和 `B` 之间是否为“快进”（fast-forward）的常用写法（或过去常用）是计算 `A` 和 `B` 之间的合并基，并检查它是否等于 `A`，如果是则 `A` 是 `B` 的祖先。你会在旧脚本中经常看到这种用法。

```
A=$(git rev-parse --verify A)
if test "$A" = "$(git merge-base A B)"
then
    ... A is an ancestor of B ...
fi
```

在现代 git 中，你可以用更直接的方式表达：

```
if git merge-base --is-ancestor A B
then
    ... A is an ancestor of B ...
fi
```

而不是上述写法。

## 关于分支点模式（FORK-POINT MODE）的讨论

在通过 `git checkout -b topic origin/master` 创建的主分支上工作后，远程追踪分支 `origin/master` 的历史可能被回滚并重建，导致如下形状的历史：

```
o---B1
/
---o---o---B2--o---o---o---B (origin/master)
    \
     B3
      \
       Derived (topic)
```

其中 `origin/master` 曾经指向提交 `B3`、`B2`、`B1`，现在指向 `B`，而你的主题分支是在 `origin/master` 处于 `B3` 时在其上方开始创建的。该模式使用 `origin/master` 的 reflog 来找到 `B3` 作为分支点，从而可以将主题分支在更新后的 `origin/master` 之上进行 rebase：

```
$ fork_point=$(git merge-base --fork-point origin/master topic)
$ git rebase --onto origin/master $fork_point topic
```

## 另参

(1), (1), (1)

---

# GIT-MERGE-FILE

## 名称

`git-merge-file` - 执行三路文件合并

## 语法

`git merge-file` `[-L <current-name> [-L <base-name> [-L <other-name>]]] [--ours|--theirs|--union] [-p|--stdout] [-q|--quiet] [--marker-size=<n>] [--[no-]diff3] <current-file> <base-file> <other-file>`

## 描述

`git merge-file` 将从 `<base-file>` 到 `<other-file>` 的所有更改合并到 `<current-file>` 中。结果通常进入 `<current-file>`。`git merge-file` 有助于合并对原始文件的多个独立修改。假设 `<base-file>` 是原始文件，且 `<current-file>` 和 `<other-file>` 都是 `<base-file>` 的修改，那么 `git merge-file` 将合并这两处更改。

如果 `<current-file>` 和 `<other-file>` 在公共行范围内都有更改，则发生冲突。如果发现冲突，`git merge-file` 通常会输出警告并用包含 `<<<<<<<` 和 `>>>>>>` 标记的行将冲突括起来。典型的冲突如下：

```
<<<<<<< A
lines in file A
=======
lines in file B
>>>>>>> B
```

如果存在冲突，用户应该编辑结果并删除其中一种方案。然而，当 `--ours`、`--theirs` 或 `--union` 选项生效时，这些冲突将分别倾向于 `<current-file>` 的行、`<other-file>` 的行或两者的行。冲突标记的长度可以通过 `--marker-size` 选项指定。

该程序的退出值在出错时为负数，否则为冲突的数量。如果合并顺利，退出值为 0。

`git merge-file` 设计为 RCS `merge` 的最小化克隆；换言之，它实现了 (1) 所需的所有 RCS `merge` 功能。

### 选项

`-L <label>`

此选项最多可给出三次，用于指定在冲突报告中代替相应文件名的标签。即，`git merge-file -L x -L y -L z a b c` 生成的输出看起来来自文件 `x`、`y` 和 `z`，而不是文件 `a`、`b` 和 `c`。

`-p`

将结果发送到标准输出而不是覆盖 `<current-file>`。

`-q`

静默模式；不对冲突发出警告。

`--diff3`

以 "diff3" 样式显示冲突。

`--ours`, `--theirs`, `--union`

不再在文件中保留冲突，而是通过倾向于我们（或他们或双方）的行来解决冲突。

## 示例

```
git merge-file README.my README README.upstream
```

合并 `README.my` 和 `README.upstream` 自 `README` 以来产生的更改，尝试合并它们并将结果写入 `README.my`。

```
git merge-file -L a -L b -L c tmp/a123 tmp/b234 tmp/c345
```

以 `tmp/b234` 为基合并 `tmp/a123` 和 `tmp/c345`，但使用 `a` 和 `c` 代替 `tmp/a123` 和 `tmp/c345`。

---

# GIT-MERGE-INDEX

## 名称

`git-merge-index` - 为需要合并的文件执行合并

## 语法

`git merge-index` `[-o] [-q] <merge-program> (-a | [--] <file>*)`

## 描述

这会在索引中查找 `<file>(s)`，如果有任何合并条目，会将这些文件的 SHA-1 哈希值作为参数 1、2、3 传递（如果没有文件则为空），并将 `<file>` 作为参数 4。三个文件的文件模式将作为参数 5、6 和 7 传递。

### 选项

`--`

不再将任何后续参数视为选项。

`-a`

对索引中所有需要合并的文件运行合并。

`-o`

不要在第一次合并失败时停止，一次性处理所有合并。

`-q`

不对合并失败报错（合并程序失败通常表示合并期间存在冲突）。这对于可能输出自定义消息的瓷器（porcelains）很有用。

如果 `git merge-index` 调用多个 `<file>`（或 `-a`），它将按顺序处理，仅在合并返回非零退出码时停止。

通常这是通过脚本运行 Git 对 RCS `merge` 命令的模拟。

发行中包含一个名为 `git-merge-file` 的示例脚本。

警告 警告 警告！Git 的“合并对象顺序”与 RCS `merge` 程序不同。在上述排序中，原始文件在前。但三路合并程序 `merge` 的参数顺序是将原始文件放在中间。别问为什么。

示例：

```
:~/merge-test> git merge-index cat MM
原始树中的 MM。
# 分支 A 中的修改 MM。
# merge1 分支 B 中的修改 MM。
# merge2 分支 B 中的修改 MM。
# 当前内容
```

或者

```
:~/merge-test> git merge-index cat AA MM
cat: : No file or directory
分支 A 中的新增 AA。
分支 B 中的新增 AA。
分支 B 中的新增 AA。
致命错误：合并程序失败
```




其中后一个示例显示了`git merge-index`在任何内容返回错误后将停止尝试合并（即`cat`对于`AA`文件返回了错误，因为在原始文件中不存在，因此`git merge-index`甚至没有尝试合并`MM`东西）。

# GIT-MERGE-ONE-FILE

## 名称

`git-merge-one-file` - `git-merge-index`使用的标准辅助程序

## 语法

`git merge-one-file`

## 描述

这是供`git merge-index`用于解析通过`git read-tree -m`完成的简易合并的标准辅助程序。

# GIT-MERGE-TREE

## 名称

`git merge-tree` - 在不接触索引的情况下显示三路合并

## 语法

`git merge-tree` `<base-tree> <branch1> <branch2>`

## 描述

读取三个树状对象，并将简易的合并结果和冲突阶段输出到标准输出。这与三路`git read-tree -m`的作用类似，但它不是将结果存储在索引中，而是将项输出到标准输出。

此命令旨在用于高级脚本，在索引之外计算合并结果，并将结果写回索引。因此，该命令的输出会省略与`<branch1>`树匹配的项。

# GIT-MERGE

## 名称

`git-merge` - 将两个或多个开发历史合并

## 概要

```
git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit] [-s <strategy>] [-X <strategy-option>] [-S[<key-id>]] [--[no-]rerere-autoupdate] [-m <msg>] [<commit>...]
git merge <msg> HEAD <commit>...
git merge --abort
```

## 描述

将指定提交（自其历史与当前分支分叉以来）的更改合并到当前分支。该命令被`git pull`用于合并来自另一个仓库的更改，也可以手动用于将一个分支的更改合并到另一个分支。

假设存在以下历史且当前分支为 "master"：

```
A---B---C topic
/
D---E---F---G master
```

那么`git merge topic`将 topic 分支自从 master 分叉以来的更改（即 E）直到其当前提交（C）重放到 master 之上，并将结果记录在一个新的提交中，同时包含两个父提交名称以及用户描述更改的日志消息。

```
A---B---C topic
/         \
D---E---F---G---H master
```

第二种语法 (`<msg> HEAD <commit>...`) 出历史原因被支持。请勿在命令行或新脚本中使用它。它等同于`git merge -m <msg> <commit>....`。

第三种语法 (`git merge --abort`) 只能在合并产生冲突后运行。`git merge --abort`将中止合并过程并尝试重构合并前的状态。然而，如果在合并开始时存在未提交的更改（特别是如果这些更改在合并开始后被进一步修改），某些情况下`git merge --abort`将无法还原原始（合并前）更改。因此：

**警告**：不建议在存在非复杂的未提交更改时运行`git merge`：虽然可行，但在发生冲突时，它可能会让你处于一种难以撤销的状态。

### 选项

`--commit, --no-commit`

执行合并并提交结果。此选项可覆盖`--no-commit`。

使用`--no-commit`执行合并，但假装合并失败且不自动提交，以便用户在提交前有机会检查并进一步微调合并结果。

`--edit, -e, --no-edit`

在对成功的机械合并提交之前调用编辑器，进一步编辑自动生成的合并消息，以便用户解释并证明合并的合理性。`--no-edit`选项用于接受自动生成的消息（这通常是不建议的）。如果你通过命令行使用`-m`选项提供了草稿消息并想在编辑器中编辑，则`--edit`（或`-e`）选项仍然有用。

旧的脚本可能依赖于过去不允许用户编辑合并日志消息的历史行为。它们在运行`git merge`时会看到编辑器打开。为了方便将此类脚本调整为更新后的行为，可以在开头将环境变量`GIT_MERGE_AUTOEDIT`设置为`no`。

`--ff`

当合并解析为快进（fast-forward）时，仅更新分支指针，而不创建合并提交。这是默认行为。

`--no-ff`

即使合并解析为快进，也创建一个合并提交。这是合并带注释（且可能已签名的）标签时的默认行为。

`--ff-only`

除非当前`HEAD`已经是最新的，或者合并可以解析为快进，否则将拒绝合并并以非零状态退出。

`--log[=<n>], --no-log`

除了分支名称外，在日志消息中填充最多`<n>`个正在合并的实际提交的单行描述。另参见 (1)。

使用`--no-log`不列出正在合并的实际提交的单行描述。

`--stat, -n, --no-stat`

在合并结束时显示差异统计（diffstat）。diffstat 也由配置选项`merge.stat`控制。

使用`-n`或`--no-stat`不在合并结束时显示差异统计。

`--squash, --no-squash`

产生工作树和索引状态，就像发生了真实的合并一样（但合并信息除外），但实际上不会创建提交、移动`HEAD`或记录`$GIT_DIR/MERGE_HEAD`（这会导致下次`git commit`命令创建一个合并提交）。这允许你在当前分支上创建一个提交，其效果等同于合并另一个分支（如果是章鱼合并则为多个）。

使用`--no-squash`执行合并并提交结果。此选项可覆盖`--squash`。

`-s <strategy>, --strategy=<strategy>`

使用指定的合并策略；可以多次提供以指定尝试的顺序。如果没有`-s`选项，则使用内置策略列表（合并单个头节点时使用`git merge-recursive`，否则使用`git merge-octopus`）。

`-X <option>, --strategy-option=<option>`

将合并策略特定的选项传递给合并策略。

`--verify-signatures, --no-verify-signatures`

验证正在合并的提交具有良好且受信任的 GPG 签名，如果没有则中止合并。

`--summary, --no-summary`

`--stat`和`--no-stat`的同义词；这些已弃用，并将在未来移除。

`-q, --quiet`

静默操作。隐含`--no-progress`。

`-v, --verbose`

详细输出。

`--progress, --no-progress`

显式开启/关闭进度显示。如果未指定，当标准错误连接到终端时将显示进度。注意，并非所有的合并策略都支持进度报告。

`-S[<keyid>], --gpg-sign[=<keyid>]`

对生成的合并提交进行 GPG 签名。

`-m <msg>`

设置用于合并提交的消息（如果创建了提交）。

如果指定了`--log`，会将合并提交的短日志追加到指定的消息中。

可以使用`git fmt-merge-msg`命令为自动化的`git merge`调用提供良好的默认值。

`--[no-]rerere-autoupdate`

允许 rerere 机制在可能的情况下使用自动冲突解决的结果更新索引。

`--abort`

中止当前的冲突解决过程，并尝试重构合并前的状态。如果在合并开始时存在未提交的工作树更改，某些情况下`git merge --abort`将无法还原这些更改。因此，建议在运行`git merge`之前始终提交或储存（stash）你的更改。

当存在`MERGE_HEAD`时，`git merge --abort`等同于`git reset --merge`。

`<commit>...`

要合并到我们分支的提交，通常是其他分支头。指定多个提交将创建一个具有多个父提交的合并（亲切地称为章鱼合并）。

如果未从命令行提供提交，则合并当前分支配置为使用的上游的远程跟踪分支。参见此手册页的配置部分。

当指定`FETCH_HEAD`（且未指定其他提交）时，上一次调用`git fetch`记录在`.git/FETCH_HEAD`文件中的分支将合并到当前分支。

## 合并前检查

在应用外部更改之前，你应该将自己的工作处理好良好状态并在本地提交，这样在发生冲突时就不会被覆盖。另参见 (1)。当本地未提交的更改与`git pull`/`git merge`可能需要更新的文件重叠时，`git pull`和`git merge`将停止而不执行任何操作。

为了避免在合并提交中记录无关的更改，如果索引中相对于`HEAD`提交有任何已的更改，`git pull`和`git merge`也会中止。（异常情况是：更改的索引条目所处已经是合并后的结果了。）

如果所有命名的提交已经是`HEAD`的祖先，`git merge`将提前退出并显示消息 "Already up-to-date."。

## 快进合并 (FAST-FORWARD MERGE)

通常情况下，当前分支的头节点是命名提交的祖先。这是最常见的情况，特别是在通过`git pull`调用时：你正在跟踪一个远程仓库，你没有提交任何本地更改，现在你想更新到更新的远程版本。在这种情况下，不需要新的提交来存储合并后的历史；相反，`HEAD`（以及索引）将更新为指向命名的提交，而不会创建一个额外的合并提交。

可以通过`--no-ff`选项来抑制这种行为。

## 真正的合并 (TRUE MERGE)

除了快进合并（见上文）外，要合并的分支必须通过一个合并提交在一起，该提交将这两个分支都作为其父节点。

会将所有待合并分支的更改协调后的合并版本提交，并且你的`HEAD`、索引和工作树将更新为该版本。只要工作树中的修改不重叠，就可以存在这些修改；更新将保留它们。

当不清楚如何协调更改时，会发生以下：

1. `HEAD`指针保持不变。
2. `MERGE_HEAD`引用被设置为指向另一个分支的头。
3. 清洁合并的路径在索引文件和你的工作树中都会更新。
4. 对于冲突路径，索引文件记录最多三个版本：stage 1 存储公共祖先的版本，stage 2 存储`HEAD`的版本，stage 3 存储`MERGE_HEAD`的版本（可以使用`git ls-files -u`查看这些阶段）。工作树文件包含 "合并" 程序的结果；即带有熟悉的冲突标记`<<<===>>>`的三路合并结果。
5. 不进行任何其他更改。特别是你在开始合并之前的本地修改将保持不变，它们的索引条目也保持原样，即与`HEAD`匹配。

如果你尝试了导致复杂冲突的合并并想重新开始，可以使用`git merge --abort`进行恢复。

## 合并标签 (MERGING TAG)

在合并注释（并可能签过）标签时，Git 总是会创建一个合并提交，即使可以进行快进合并，并且使用标签消息准备消息模板。此外，如果标签经过了签名，签名检查将作为注释报告在消息模板中。参见 (1)。

当你只想与通向标签提交的工作进行集成（例如，与远程发布点同步）时，你可能不想创建一个不必要的合并提交。

在这种情况下，你可以在将其传递给`git merge`之前自己 "解包" 标签，或者在你没有任何自己的工作时传递`--ff-only`。例如：

```
git fetch origin
git merge v1.2.3⁰
git merge --ff-only v1.2.3
```

## 冲突是如何呈现的

在合并期间，工作树文件将被更新以反映合并的结果。在对公共祖先版本所所的更改中，不重叠的更改（即你更改了文件的一个区域，而另一侧保持该区域完好，反之亦然）将原封不动地包含在最终结果。然而，当双方都对同一区域进行了更改时，Git 无法随机选择其中一方而非另一方，并要求你通过保留双方对该区域所的操作来解决它。

默认情况下，Git 使用与 RCS 套件中的 "merge" 程序相同的样式来呈现此类冲突块，如下：

```
Here are lines that are either unchanged from the common ancestor,
or cleanly resolved because only one side changed.
<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
=======
Git makes conflict resolution easy.
>>>>>>> theirs:sample.txt
And here is another line that is cleanly resolved or unmodified.
```

发生一对冲突更改的区域用`<<<<<<<`、`=======`和`>>>>>>>`标记标记。`=======`之前的部分通常是你的侧，`=======`之后的部分通常是他们侧。

默认格式不显示冲突区域的原始内容。你无法判断你侧有多少行被删除并替换为关于芭比的评论。你唯一能确定的是你的一侧想说这很难，而且你更倾向于去购物，而另一侧则声称这很容易。

通过将配置变量`merge.conflictStyle`设置为 "diff3"，可以使用另一种样式。在 "diff3" 样式中，上述冲突可能像这样：

```
Here are lines that are either unchanged from the common ancestor,
or cleanly resolved because only one side changed.
<<<<<<< yours:sample.txt
Conflict resolution is hard;
let's go shopping.
|||||||
Conflict resolution is hard.
=======
Git makes conflict resolution easy.
>>>>>>> theirs:sample.txt
And here is another line that is cleanly resolved or unmodified.
```

除了`<<<<<<<`、`=======`和`>>>>>>>`标记外，它使用了另一个`|||||||`标记，后面跟着原始文本。你可以看出原始文本只是陈述了一个事实，你的一侧只是顺从了该声明并放弃了，而另一侧试图采取更积极的态度。你有时可以通过查看原始文本找到更好的解决方案。

## 如何解决冲突 (HOW TO RESOLVE CONFLICTS)

看到冲突后，你可以做两件事：

1. 决定不合并。你需要的清理是将索引文件重置为`HEAD`提交以撤销操作 2，并清理操作 2 和 3 产生的工作树更改；可以使用`git merge --abort`完成此。
2. 解决冲突。Git 会在工作树中标记冲突。编辑文件使其正确并使用`git add`将它们添加到索引。使用`git commit`最终定稿。

你可以使用多种工具处理冲突：

- 使用 mergetool。运行`git mergetool`启动图形化合并工具，它将引导你完成合并。
- 查看差异。`git diff`将显示三路差异，突出来自`HEAD`和`MERGE_HEAD`版本的更改。
- 查看每个分支的差异。`git log --merge -p <path>`将先显示`HEAD`版本的差异，然后显示`MERGE_HEAD`版本的差异。
- 查看原始文件。`git show :1:filename`显示公共祖先，`git show :2:filename`显示`HEAD`版本，`git show :3:filename`显示`MERGE_HEAD`版本。

## 示例 (EXAMPLES)

在分支之上合并修复和增强，进行章鱼合并：

```
$ git merge fixes enhancements
```

使用`ours`合并策略将`obsolete`分支合并到当前分支：

```
$ git merge -s ours obsolete
```

将`maint`分支合并到当前分支，但不自动创建新提交：

```
$ git merge --no-commit maint
```




当你想要在合并中包含更多更改，或想编写自己的合并提交消息时可以使用此选项。你应该避免滥用此选项将重大更改悄溜入合并提交中。像更新发布/版本名称这样的小幅修复是可以接受的。

## 合并策略 (MERGE STRATEGIES)

合并机制（`git merge` 和 `git pull` 命令）允许通过 `-s` 选项选择后端合并策略。某些策略还可以接受自己的选项，可以通过向 `git merge` 和/或 `git pull` 提供 `-X<option>` 参数来传递。

**resolve**

这只能使用三路合并算法解决两个头（即当前分支和你从其拉取的的另一个分支）。它尝试仔细检测交叉合并的歧义，并通常被认为是安全且快速的。

**recursive**

这种方法仅使用 3 路合并算法解决两个头提交。当存在多个一个可用于 3 路合并的共同祖先时，它会创建一个共同祖先的合并树，并将其用作 3 路合并的引用树。根据对 Linux 2.6 内核开发历史中实际合并提交的测试，这种方法可以减少合并冲突，且不会导致错误合并（mismerges）。此外，它还能检测并处理涉及重命名的合并。这是拉取或合并单个分支时的默认合并策略。

`recursive` 策略可以接受以下选项：

### ours

此选项强制通过优先考虑 `our`（我们的）版本来对冲突的代码块进行自动清洁解决。另一个树中与我们的一侧不冲突的更改将反映在合并结果中。对于二进制文件，整个内容将从我们这边获取。

这不应与 `ours` 合并策略混淆，后者完全不查看另一个树包含什么。它会丢弃另一个树的所有操作，并声明我们的 `our` 历史包含了其中发生的所有事件。

### theirs

这是 `ours` 的相反选项。

### patience

使用此选项时，`merge-recursive` 会花费一点额外时间来避免有时因不重要的匹配行（例如不同函数的括号括号）而导致的错误合并。当要合并的分支发生巨大差异时请使用此选项。另见 (1)--patience。

### diff-algorithm=[patience|minimal|histogram|myers]

告诉 `merge-recursive` 使用不同的 `diff` 算法，这有助于避免因不重要的匹配行（如不同函数的大括号）而导致的错误合并。另见 (1)--diff-algorithm。

### ignore-space-change, ignore-all-space, ignore-space-at-eol

为了进行三路合并，将具有指定类型空格更改的行视为未更改。与行其他更改混合的空格更改不会被忽略。另见 (1)-b, -w 和 `--ignore-space-at-eol`。

- 如果 `their`（他们的）版本仅对某行引入了空格更改，则使用 `our` 版本；
- 如果 `our` 版本引入了空格更改，但 `their` 版本包含实质性更改，则使用 `their` 版本；
- 否则，合并按通常方式进行。

### renormalize

在解决三路合并时，对文件的所有三个阶段运行虚拟检出和检入。此选项用于合并具有不同清理过滤器（clean filters）或行尾规范化规则的分支。详见 (5) 中的“合并具有不同检入/检出属性的分支”。

### no-renormalize

禁用 `renormalize` 选项。这会覆盖 `merge.renormalize` 配置变量。

### rename-threshold=<n>

控制用于重命名检测的相似性阈值。另见 (1)-M。

### subtree[=<path>]

此选项是 `subtree` 策略的更高级的形式，该策略在合并时会猜测两个树必须如何移动以相互匹配。相反，会在指定的路径前加上前缀（或从开头删除），以使两个树的形状相匹配。

### octopus

这种方法解决多于两个头提交的情况，但拒绝执行需要手动解决的复杂合并。它主要用于将多个主题分支头打包在一起。这是拉取或合并两个以上分支时的默认合并策略。

### ours

这种方法解决任意数量的头，但合并生成的树始终是当前分支头，有效地忽略了来自所有其他分支的所有更改。它用于取代侧分支的开发历史。注意，这与 `recursive` 合并策略的 `-Xours` 选项不同。

### subtree

这是一个改进的递归策略。在合并树 A 和 B 时，如果 B 对应于 A 的子树，则先调整 B 以匹配 A 的树结构，而不是在相同级别读取树。这种调整也会对共同祖先树进行。

对于使用 3 路合并的策略（包括默认的 `recursive`），如果两个分支上都进行了更改，但随后在一个分支上撤销了该更改，则该更改将出现在合并结果中；有些人发现这种行为很令人困惑。这是因为在执行合并时只考虑头和合并基底（merge base），而不考虑单个提交。因此，合并算法将撤销的更改视为没有任何更改，并代之以更改后的版本。

## 配置 (CONFIGURATION)

### merge.conflictStyle

指定合并时将冲突代码块写入工作树文件中的样式。默认值是 `"merge"`，它会显示 `<<<<<<<` 冲突标记、一侧的更改、`=======` 标记、另一侧的更改，然后是 `>>>>>>>` 标记。另一种样式 `"diff3"` 会在 `=======` 标记之前添加 `|||||||` 标记和原始文本。

### merge.defaultToUpstream

如果在调用 `merge` 时没有带任何提交参数，则通过使用当前分支配置的上游分支在远程跟踪分支中存储的最后观测值来合并这些分支。会查询 `branch.<current branch>.merge` 来命名了由 `branch.<current branch>.remote` 指定的远程分支，然后通过 `remote.<remote>.fetch` 将其映射到相应的远程跟踪分支，并合并这些跟踪分支的末端。

### merge.ff

默认情况下，Git 在合并作为当前提交之后代的提交时不会创建额外的合并提交。相反，当前分支的末端将进行快进（fast-forward）。当设置为 `false` 时，此变量告诉 Git 在此类创建一个额外的合并提交（等同于在命令行提供 `--no-ff` 选项）。当设为 `only` 时，仅允许此类快进合并（等同于在命令行提供 `--ff` 选项）。

### merge.branchdesc

除了分支名称外，日志中还将填充相关的分支描述文本。默认值为 `false`。

### merge.log

除了分支名称外，日志中还将从正在合并的实际提交中填充最多指定数量的单行描述。默认值为 `false`，`true` 是 `20` 的同义词。

### merge.renameLimit

执行合并期间重命名检测时考虑的文件数；如果未指定，默认值为 `diff.renameLimit` 的值。

### merge.renormalize

告诉 Git 仓库中文件的标准表示随时间发生了变化（例如，早期的提交记录了带有 CRLF 行结束的文本文件，但最近的使用 LF 结束）。在这样的仓库中，Git 可以在执行合并之前将提交中记录的数据转换为标准形式以减少不必要的冲突。更多信息请参见 (5) 中的“合并具有不同检入/检出属性的分支”。

### merge.stat

在合并结束时是否打印 `ORIG_HEAD` 和合并结果之间的 `diffstat`。默认值为 `true`。

### merge.tool

控制 (1) 使用哪种合并工具。下面的列表显示了有效的内置值。任何其他值都被视为自定义合并工具，并要求定义相应的 `mergetool.<tool>.cmd` 变量。

- `araxis`
- `bc`
- `bc3`
- `codecompare`
- `deltawalker`
- `diffmerge`
- `diffuse`
- `emerge`
- `gvimdiff`
- `gvimdiff2`
- `gvimdiff3`
- `kdiff3`
- `meld`
- `opendiff`
- `p4merge`
- `tkdiff`
- `tortoisesemerge`
- `vimdiff`
- `vimdiff2`
- `vimdiff3`
- `winmerge`
- `xxdiff`

### merge.verbosity

控制递归合并策略显示的输出量。级别 `0` 除了检测到冲突时的最终错误消息外不输出任何内容。级别 `1` 输出冲突，`2` 输出冲突和文件更改。级别 `5` 及以上输出调试信息。默认级别为 `2`。可以通过环境变量 `GIT_MERGE_VERBOSITY` 覆盖。

### merge.<driver>.name

为自定义低级合并驱动程序定义一个可读的名称。详见 (5)。

### merge.<driver>.driver

定义实现自定义低级合并驱动程序的命令。详见 (5)。

### merge.<driver>.recursive

命名一个低级合并驱动程序，用于在共同祖先之间执行内部合并时。详情参见 (5)。

### branch.<name>.mergeOptions

设置合并到分支 `<name>` 的默认选项。语法和支持的选项与 `git merge` 相同，但目前不支持包含空白字符的选项值。

## 另请

(1), (1), (5), (1), (1), (1), (1), (1), (1)

***

# GIT-MERGETOOL--LIB

## 名称

`git-mergetool--lib` - 通用的 Git 合并工具 shell 脚本

## 概述

```
TOOL_MODE=(diff|merge) . "$(git --exec-path)/git-mergetool--lib"
```

## 描述

这不是终端用户想要运行的命令。永远不会。此文档适用于正在研究瓷级（Porcelain-ish）脚本和/或正在编写新脚本的人。

`git-mergetool--lib` 脚本供其他 shell 脚本加载（使用 `.`），以设置处理 Git 合并工具的函数。

在加载 `git-mergetool--lib` 之前，你的脚本必须设置 `TOOL_MODE` 来定义下列函数的操作模式。`diff` 和 `merge` 是有效值。

## 函数

`get_merge_tool`

返回一个合并工具。

`get_merge_tool_cmd`

返回合并工具的自定义命令。

`get_merge_tool_path`

返回合并工具的自定义路径。

`run_merge_tool`

根据工具名称和指示是否存在合并基的真/假标志启动合并工具。`$MERGED`、`$LOCAL`、`$REMOTE` 和 `$BASE` 必须定义供合并工具使用。

***

# GIT-MERGETOOL

## 名称

`git-mergetool` - 运行冲突解决工具来解决合并冲突

## 概述

```
git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>...]
```

## 描述

使用 `git mergetool` 运行多个合并工具之一来解决合并冲突。它通常在 `git merge` 之后运行。

如果给了一个或多个 `<file>` 参数，将运行合并工具程序来解决每个文件的差异（跳过没有冲突的文件）。指定目录将包含该路径下所有未解决的文件。如果没有指定任何 `<file>` 名称，`git mergetool` 将对每个具有合并冲突的文件运行合并工具程序。

### 选项

`-t <tool>, --tool=<tool>`

使用由 `<tool>` 指定合并解决程序。有效值包括 `emerge`, `gvimdiff`, `kdiff3`, `meld`, `vimdiff` 和 `tortoisemerge`。运行 `git mergetool --tool-help` 查看有效的 `<tool>` 设置列表。

如果未指定合并解决程序，`git mergetool` 将使用配置变量 `merge.tool`。如果未设置配置变量 `merge.tool`，`git mergetool` 将选择一个合适的默认值。

你可以通过设置配置变量 `mergetool.<tool>.path` 来显式地提供工具的完整路径。例如，你可以通过设置 `mergetool.kdiff3.path` 配置 `kdiff3` 的绝对路径。否则，`git mergetool` 假设工具在 `PATH` 中可用。

与其运行已知的合并工具程序之一，`git mergetool` 可以通过在配置变量 `mergetool.<tool>.cmd` 中指定调用命令行来定制运行替代程序。

当使用此工具调用 `git mergetool` 时（通过 `-t` 或 `--tool` 选项或 `merge.tool` 配置变量），将调用已配置的命令行，其中 `$BASE` 设置为包含合并共同基的临时文件名（如果可用）；`$LOCAL` 设置为包含当前分支文件内容的临时文件名；`$REMOTE` 设置为包含待合并文件内容的临时文件名；而 `$MERGED` 设置为合并工具应写入合并解决结果的文件名。

如果自定义合并工具通过其退出码正确指示了合并解决的成功，则可以将配置变量 `mergetool.<tool>.trustExitCode` 设置为 `true`。否则，`git mergetool` 将在自定义工具退出后提示用户指示解决是否成功。

`--tool-help`

打印可能与 `--tool` 使用的合并工具列表。

`-y, --no-prompt`

在每次调用合并解决程序之前不进行提示。如果通过 `--tool` 选项或 `merge.tool` 配置变量显式指定了合并解决程序，则这是默认值。

`--prompt`

在每次调用合并解决程序之前进行提示，给用户跳过路径的机会。

## 临时文件

`git mergetool` 在解决合并时会创建 `*.orig` 备份文件。一旦文件合并完成且 `git-mergetool` 会话结束，就可以安全地删除它们。

将配置变量 `mergetool.keepBackup` 设置为 `false` 会导致 `git mergetool` 在文件成功合并后自动删除备份。

***

# GIT-MKTAG

## 名称

`git-mktag` - 创建标签对象

## 概述

```
git mktag < signature_file
```

## 描述

从标准输入读取标签内容，并创建一个也可以用于签名其他对象的标签对象。

输出是新标签的 `<object>` 符。

## 标签格式

标签签名文件具有非常简单的固定格式：四行：

```
object <sha1> type <typename> tag <tagname> tagger <tagger>
```

随后是某些可选的自由格式消息（某些由旧 Git 创建的标签可能没有 `tagger` 行）。消息如果存在，则通过空行与头部分离。消息部分可能包含 Git 本身不关心的签名，但可以使用 `gpg` 进行验证。

***

# GIT-MKTREE

## 名称

`git-mktree` - 从 `ls-tree` 格式的文本构建树对象

## 概述

```
git mktree [-z] [--missing] [--batch]
```

## 描述

以非递归的 `ls-tree` 输出格式读取标准输入，并创建一个树对象。树条目的顺序由 `mktree` 归一化，因此不需要对输入进行预排序。构建的树对象的对象名称将写入标准输出。

### 选项

`-z`

读取以 NUL 终止的 `ls-tree` 输出代替。

`--missing`

允许缺失的对象。默认行为（不使用此选项）是验证每个条目的 `sha1` 标识现有对象。此选项对 `gitlink` 条目（即模块）没有影响，它们始终允许缺失。

`--batch`

允许在退出前构建多个树对象。每个树由空行分隔。最后的换行符是可选的。注意 - 如果使用了 `-z` 选项，行以 NUL 终止。

***

# GIT-MV

## 名称

`git-mv` - 移动或重命名文件、目录或符号链接

## 概述

```
git mv <options>... <args>...
```

## 描述

移动或重命名文件、目录或符号链接。

```
git mv [-v] [-f] [-n] [-k] <source> <destination>
git mv [-v] [-f] [-n] [-k] <source> ... <destination directory>
```



在第一形式中，它重命名`<source>`（必须存在且是文件、符号链接或目录）为`<destination>`。在第二形式中，最后一个参数必须是现有目录；指定的源将移动到该目录。

成功完成后会更新索引，但必须提交更改。

### 选项

`-f, --force`

即使目标存在也强制重命名或移动文件

`-k`

跳过会导致错误条件的移动或重命名操作。当源既不存在也不受 Git 控制，或者当它将覆盖现有文件（除非给了`-f`）时，会发生错误。

`-n, --dry-run`

什么都不做；仅显示将发生什么

`-v, --verbose`

报告被移动的文件名。

## 子模块

使用 gitfile 移动子模块（这意味着是用 Git 1.7.8 或更高版本克的）将更新 gitfile 和`core.worktree`设置，以便子模块在新位置工作。它还会尝试更新 (5) 文件中的`submodule.<name>.path`设置并暂存该文件（除非使用了`-n`）。

## 缺陷

每当超级项目（superproject）更新移动了一个已填充的子模块（例如在移动前后的提交之间切换），旧位置将保留一个过时的子模块检出（checkout），而新位置会出现一个空目录。要在新位置重新填充子模块，用户必须在之后运行`git submodule update`。只有当旧目录使用`gitfile`时，删除旧目录才是安全的，否则子模块的历史也将被删除。当实现递归子模块更新后，这两个步骤将变得过时。

# GIT-NAME-REV

## NAME
`git-name-rev` - 为给定的修订版本查找符号名称

## SYNOPSIS
`git name-rev` [--tags] [--refs=<pattern>] ( --all | --stdin | <commit-ish>... )`

## DESCRIPTION
对于任何可由`git rev-parse`解析的格式的修订，查找适合人类阅读的符号名称。

## OPTIONS
`--tags`
不使用分支名，仅使用标签（tags）命名提交。

`--refs=<pattern>`
仅使用名称匹配给定 shell 模式的引用（refs）。模式可以是分支名、标签名或完全限定的引用名。

`--all`
列出从所有引用可及的所有提交。

`--stdin`
通过将标准输入中的所有 40 字符 SHA-1 十进制字符串（假设为`$hex`）替换为`"$hex ($rev_name)"`。与`--name-only`使用时，替换为`$rev_name`，完全省略`$hex`。供脚本编写使用。

`--name-only`
不再同时打印 SHA-1 和名称，仅打印名称。如果与`--tags`一起使用，名称中还将省略常用的标签前缀`"tags/"`，这更接近`git-describe`的输出。

`--no-undefined`
当引用未定义时，以错误码 != 0 退出，而不是打印 undefined。

`--always`
显示唯一缩短的提交对象作为回退。

## EXAMPLE
给定一个提交，找出它相对于本地引用（refs）的位置。假设有人向你提到了那个神奇的提交`33db5f4d9027a10e477ccf054b2c1ab94f74c85a`。当然，你查看了提交，但这只能告诉你发生了什么，而不能告诉你上下文。

输入`git name-rev`：

```
% git name-rev 33db5f4d9027a10e477ccf054b2c1ab94f74c85a 33db5f4d9027a10e477ccf054b2c1ab94f74c85a tags/v0.99~940
```

现在你更理智了，因为你知道它发生在`v0.99`之前的 940 次修订中。

你可以做的另一件好事是：

```
% git log | git name-rev --stdin
```

# GIT-NOTES

## NAME
`git-notes` - 添加或检查对象注释

## SYNOPSIS
`git notes` [list [<object>]]
`git notes` add [-f] [--allow-empty] [-F <file> | -m <msg> | (-c | -C) <object>] [<object>]`
`git notes` copy [-f] ( --stdin | <from-object> <to-object> )`
`git notes` append [--allow-empty] [-F <file> | -m <msg> | (-c | -C) <object>] [<object>]`
`git notes` edit [--allow-empty] [<object>]`
`git notes` show [<object>]`
`git notes` merge [-v | -q] [-s <strategy> ] <notes-ref>`
`git notes` merge --commit [-v | -q]`
`git notes` merge --abort [-v | -q]`
`git notes` remove [--ignore-missing] [--stdin] [<object>...]`
`git notes` prune [-n | -v]`
`git notes` get-ref`

## DESCRIPTION
添加、删除或读取附加到对象上的注释而不触碰对象本身。

默认情况下，注释保存并读取自`refs/notes/commits`，但可以覆盖此默认。请参下文的 OPTIONS、CONFIGURATION 和 ENVIRONMENT 部分。

## SUBCOMMANDS
`list`
列出给定对象的注释。如果没有给出对象，则显示所有注释。

`add`
向对象添加注释（默认为 HEAD）。如果该对象已有注释，除非使用`-f`，否则将失败。

`append`
向对象追加注释（默认为 HEAD）。如果对象不存在，则创建它。

`edit`
编辑给定对象的注释（默认为 HEAD）。这会打开编辑器。

`show`
显示给定对象的注释（默认为 HEAD）。

`merge`
将给定的注释引用（ref）合并到当前注释中。如果发生冲突且未给出策略，则使用手动解析器。这会在特殊的工作树`.git/MERGE_WORKTREE`中检出冲突的注释。

`--commit`
通过提交注释完成合并。

`--abort`
中止合并。

`remove`
删除给定对象的注释。

`prune`
删除所有不存在/不可及对象的注释。

`get-ref`
打印当前的注释引用。

请求从一个没有关联注释的对象中移除注释不被视为错误。

`--stdin`

也可以从标准输入读取要移除注释的对象名称（没有理由不将其与命令行中的对象名称结合使用）。

`-n, --dry-run`

不删除任何内容；仅报告将要移除注释的对象名称。

`-s <strategy>, --strategy=<strategy>`

在合并注释时，使用给定的策略解决注释冲突。识别以下策略："manual"（默认）、"ours"、"theirs"、"union" 和 "cat_sort_uniq"。请参下文“注释合并策略”部分获取有关每种注释合并策略的更多信息。

`--commit`

完成正在进行中的`git notes merge`。当您解决了`git notes merge`存储在`.git/NOTES_MERGE_WORKTREE`中的冲突时，使用此选项。这会通过添加`.git/NOTES_MERGE_WORKTREE`中的注释，来对`git notes merge`创建的部分合并提交（存储在`.git/NOTES_MERGE_PARTIAL`）进行修订。存储在`.git/NOTES_MERGE_REF`符号引用中的 notes ref 将更新为生成的提交。

`--abort`

中止/重置正在进行中的`git notes merge`，即带有冲突的注释合并。这将简单地删除所有与注释合并相关的文件。

`-q, --quiet`

在合并注释时，静默操作。

`-v, --verbose`

在合并注释时，输出更详细的信息。在修剪注释时，报告所有移除注释的对象名称。

## 讨论

提交注释（Commit notes）是包含对象额外信息的 blob（通常是补充提交消息的信息）。这些 blob 提取自注释引用（notes refs）。注释引用通常是一个分支，其中包含一些“文件”，这些“文件”的路径是它们所描述的对象的名称，出于性能考虑，路径中包含了一些目录分隔符 [1]。

每次注释更改都会在指定的注释引用创建一个新提交。因此，您可以通过调用例如`git log -p notes/commits`来检查注释历史。目前，提交消息仅记录了什么操作触发了更新，且提交作者根据常规规则确定（见 (1)）。这些细节在未来可能会发生变化。

注释引用允许直接指向树对象（tree object），在这种情况下，可以使用`git log -p -g <refname>`读取注释历史。

## 注释合并策略

默认的注释合并策略是 "manual"，它会在特殊的工作树（`.git/NOTES_MERGE_WORKTREE`）中检出冲突的注释以解决注释冲突，并指示用户在该工作树中解决冲突。完成后，用户可以使用`git notes merge --commit`完成合并，或使用`git notes merge --abort`中止合并。

"ours" 自动解决注释冲突并倾向于本地版本（即当前的注释引用）。

"theirs" 自动解决注释冲突并倾向于远程版本（即合并到当前注释引用的给定的注释引用）。

"union" 通过拼接本地和远程版本自动解决注释冲突。

"cat_sort_uniq" 与 "union" ，但除了拼接本地和远程版本外，该策略还会对生成的行进行排序，并移除结果中的重复行。这等同于对本地和远程版本应用`cat | sort | uniq`壳管道。如果注释遵循基于行的格式，且希望避免合并结果中出现重复行，则此策略非常有用。注意，如果本地或远程版本在合并之前包含重复行，这些行也会被此注释合并策略移除。

## 示例

您可以使用注释添加写入提交时不可用信息的注释。

```
$ git notes add -m 'Tested-by: Johannes Sixt <>' 72a144e2 $ git show -s 72a144e [...] Signed-off-by: Junio C Hamano <> Notes: Tested-by: Johannes Sixt <>
```

从原则上说，注释是一个普通的 Git blob，接受任何格式的（或非格式）。您可以使用`git hash-object`从任意文件二进制安全地创建注释：

```bash
$ cc *.c $ blob=$(git hash-object -w a.out) $ git notes --ref=built add --allow-empty -C "$blob" HEAD
```




您不能简单地使用`git notes --ref=built add -F a.out HEAD`，因为这不是二进制安全的。当然，用`git log`显示非文本格式注释没有意义，所以如果您使用此类注释，可能需要编写一些特殊工具来对它们进行一些有用的操作。

## 配置

### `core.notesRef`

用于读取和操作的注释引用，而不是`refs/notes/commits`。必须是未缩写的引用名。此设置可以通过环境变量和命令行覆盖。

### `notes.displayRef`

在使用`git log`系列命令显示提交消息时，除了`core.notesRef`或`GIT_NOTES_REF`设置的默认集外，还要从哪些引用（或多个引用，如果使用了通配符或指定多次）读取注释。此设置可以通过命令行或`GIT_NOTES_DISPLAY_REF`环境变量覆盖。见 (1)。

### `notes.rewrite.<command>`

当使用`<command>`重写提交（当前为 amend 或 rebase）时，如果此变量为 false，git 将不会从原始提交复制注释到修订后的提交。默认 true true。见下文的 "notes.rewriteRef"。

此设置可以通过环境变量`GIT_NOTES_REWRITE_REF`覆盖。

### `notes.rewriteMode`

在重写期间复制注释时，如果目标提交已经有了注释，该做什么。必须是 overwrite（覆盖）、concatenate（拼接）或 ignore（忽略）之一。默认是 concatenate。

此设置可以通过环境变量`GIT_NOTES_REWRITE_MODE`覆盖。

### `notes.rewriteRef`

在重写期间复制注释时，指定应复制注释的（完全限定的）引用。可以是通配符，在这种情况下，将复制所有匹配引用的注释。您也可以多次指定此配置。

没有默认值；您必须配置此变量以启用注释重写。

可以通过环境变量`GIT_NOTES_REWRITE_REF`覆盖。

## 环境

### `GIT_NOTES_REF`

要从哪个引用操作注释，而不是`refs/notes/commits`。这会覆盖`core.notesRef`设置。

### `GIT_NOTES_DISPLAY_REF`

用冒号分隔的引用或通配符列表，表示在显示提交消息时，除了来自`core.notesRef`或`GIT_NOTES_REF`的默认值外，还要从哪些引用读取注释。这会覆盖`notes.displayRef`设置。

对于不存在的引用将发出警告，但不匹配任何引用的通配符将被静默忽略。

### `GIT_NOTES_REWRITE_MODE`

在重写期间复制注释时，如果目标提交已经有了注释，该做什么。必须是 overwrite、concatenate 或 ignore 之一。这会覆盖`core.rewriteMode`设置。

### `GIT_NOTES_REWRITE_REF`

在重写提交时，从原始提交复制哪些注释到修订后的提交中。必须是用冒号分隔的引用或通配符列表。

如果未在环境变量中设置，复制的注释列表取决于`notes.rewrite.<command>`和`notes.rewriteRef`设置。

## GIT

(7) 套件的一部分

## 注释

1. 允许的路径名形式为`ab*/*cd*/*ef*/*...*/*abcdef...`：一系列由两个十六进制数字组成的目录名称，后跟一个带有对象 ID 剩余部分的文件。

# GIT-PACK-OBJECTS

## 名称

`git-pack-objects` - 创建对象的压缩归档

## 摘要

`git pack-objects [-q | --progress | --all-progress] [--all-progress-implied] [--no-reuse-delta] [--delta-base-offset] [--non-empty] [--local] [--incremental] [--window=<n>] [--depth=<n>] [--revs [--unpacked | --all]] [--stdout | base-name] [--shallow] [--keep-true-parents] < object-list`

## 描述

从标准输入读取对象列表，并带有指定的 base-name 写入压缩归档，或写入标准输出。

压缩包（packed archive）是在两个仓库之间传输一组对象的高效方式，也是一种访问高效的归档格式。在压缩包中，对象要么被存储为压缩后的整体，要么存储为相对于其他对象的差异。后者通常被称为`delta`（增量）。

压缩包格式（`.pack`）被设计为自包含，因此可以在不需要任何额外信息的情况下进行解包。因此，delta 所依赖的每个对象都必须存在包内。

会生成一个包索引文件（`.idx`），以便对包中的对象进行快速的随机访问。将索引文件（`.idx`）和压缩包（`.pack`）都放在`$GIT_OBJECT_DIRECTORY`的`pack/`子目录中（或`$GIT_ALTERNATE_OBJECT_DIRECTORIES`中的任何目录），即可允许 Git 从压缩包中读取数据。

`git unpack-objects`命令可以读取压缩包，并将包中包含的对象展开为“一文件一对象”格式；这通常由智能拉取（smart-pull）命令完成，这些命令会在为对端进行高效网络传输时动态创建压缩包。

## 选项

### `base-name`

写入一对文件（`.pack`和`.idx`），使用`<base-name>`来确定创建的文件名。当使用此选项时，两个文件将写入`<base-name>-<SHA-1>.{pack,idx}`文件中。`<SHA-1>`是基于包内容的哈希值，并输出到命令的标准输出。

### `--stdout`

将包的内容（本应写入`.pack`文件的内容）输出到标准输出。

### `--revs`

从标准输入读取修订参数，而不是单个对象名称。修订参数的处理方式与`git rev-list`使用`--objects`标志的方式相同，后者使用其提交参数来构建其输出的对象列表。结果列表中的对象将被压缩。除了修订外，还接受`--not`或`--shallow <SHA-1>`行。

### `--unpacked`

这隐含了`--revs`。在处理从标准输入读取的修订参数列表时，将要压缩的对象限制为那些尚未压缩的对象。

### `--all`

这隐含了`--revs`。除了从标准输入读取的修订参数列表外，假装`refs/`下的所有引用（refs）都已指定包含在内。

### `--include-tag`

如果其引用的对象已包含在生成的包文件中，则包含未被请求的注释标签（tags）。这对于将新标签发送给原生 Git 很有用。

### `--window=<n>`、`--depth=<n>`

这两个选项影响使用 delta 压缩存储包中对象的方式。对象首先内部按类型、大小以及可选的名称进行排序，并与`--window`内的其他对象进行比较，以查看使用 delta 压缩是否节省空间。`--depth`限制最大 delta 深度；过深会影响解包端的性能，因为需要多次应用 delta 数据才能获得所需的对象。`--window`的默认值为 10，`--depth`为 50。

### `--window-memory=<n>`

此选项在`--window`的基础上提供了额外的内存限制；窗口大小将动态缩小，以确保占用的内存不超过`<n>`字节。这对于混合了大、小对象的仓库非常有用，可以避免在使用大窗口时耗尽内存，同时仍然让较小对象利用大窗口。大小可以带有后缀 "k"、"m" 或 "g"。`--window-memory=0`使内存使用无限制，这是默认值。

### `--max-pack-size=<n>`

每个输出包文件的最大大小。大小可以带有后缀 "k"、"m" 或 "g"。允许的最小大小限制为 1 MiB。如果指定，可能会创建多个包文件。除非配置变量`pack.packSizeLimit`被设置，否则默认无限。

### `--honor-pack-keep`

此标志会导致本地包中已存在`.keep`文件的对象被忽略，即使它原本会被压缩。

### `--incremental`

此标志会导致已存在于包中的对象被忽略，即使它原本会被压缩。

### `--local`

此标志会导致从替代对象存储（alternate object store）借用的对象被忽略，即使它原本会被压缩。

### `--non-empty`

只有当压缩包至少包含一个对象时，才创建压缩包。

### `--progress`

默认情况下，当标准错误连接到终端时，会在标准错误流上报告进度状态，除非指定了`-q`。此标志即使在标准错误流未重定向到终端也会强制报告进度状态。

### `--all-progress`

当指定`--stdout`时，在对象计数和压缩阶段会显示进度报告，但在输出阶段会被抑制。这是因为在某些情况下，输出流直接链接到另一个命令，该命令在处理传入的包数据时可能希望显示自己的进度状态。此标志类似于`--progress`，区别在于它即使在使用`--stdout`时也会强制在输出阶段进行进度报告。

### `--all-progress-implied`

此标志用于在激活进度显示时隐含`--all-progress`。与`--all-progress`不同，此标志本身并不会强制执行任何进度显示。

### `-q`

此标志使命令不在标准错误流上报告其进度。

### `--no-reuse-delta`

在具有现有压缩包的仓库中创建压缩包时，命令会重用现有的 delta。这有时会导致包略微欠优。此标志告诉命令不要重用现有的 delta，而是从头开始计算。

### `--no-reuse-object`

此标志告诉命令完全不要重用现有对象数据（包括 delta 化的对象），强制重新压缩。这隐含了`--no-reuse-delta`。仅在需要对所有数据强制统一压缩级别的极少数情况下有用。

### `--compression=<n>`

指定生成包中新压缩数据的压缩级别。如果没有指定，包压缩级别首先由`pack.compression`决定，然后是`core.compression`，如果两者未设置则默认为 -1（zlib 默认值）。如果你希望对所有数据强制统一压缩级别，请添加`--no-reuse-object`。

### `--thin`

通过省略发送者和接收者之间的共同对象创建一个“薄包”，以减少网络传输。此选项在结合`--stdout`时才有意义。

注意：薄包由于缺少了对象而违反了压缩包格式，因此在不使其自包含的情况下无法被 Git 使用。使用`git index-pack --fix-thin`（见 (1)）来恢复自包含属性。

### `--shallow`

为浅仓库客户端优化包。此选项结合`--thin`可以以速度为代价获得更小的包。

### `--delta-base-offset`

压缩包可以将 delta 的基对象表示为 20 字节的对象名称或流中的偏移量，但旧版本的 Git 不理解后者。默认，`git pack-objects`为了兼容性仅使用前者格式。此选项允许命令使用后者以提高紧凑性。取决于平均 delta 链的长度，此选项通常能使生成的包文件缩小 3%–5%。

注意：在现代 Git 中，如`git gc`（见 (1)）、`git repack`（见 (1)）等 Porcelain 命令在将仓库中的对象放入包文件时默认会传递此选项。`git bundle`（见 (1)）在创建 bundle 时也是如此。

### `--threads=<n>`

指定在搜索最佳 delta 匹配时启动的线程数。这要求`pack-objects`使用 pthreads 编译，否则该选项将被忽略并发出警告。这旨在减少多处理器机器上的打包时间。然而，delta 搜索窗口所需的内存量将乘以线程数倍。指定 0 将使 Git 自动检测 CPU 数量并相应设置线程数。

### `--index-version=<version>[,<offset>]`

此命令仅供测试套件使用。它允许强制生成的包索引（pack index）版本，并强制位于给定偏移量以上的对象使用 64 位索引项。

### `--keep-true-parents`

使用此选项时，被嫁接（grafts）隐藏的父节点会被打包。

## 另请参阅

(1) (1) (1)

# GIT-PACK-REDUNDANT

## 名称

`git-pack-redundant` - 查找冗余的包文件（pack files）

## 语法

`git pack-redundant [--verbose] [--alt-odb] < --all | .pack filename ... >`

## 描述

此程序计算仓库中哪些包是冗余的。如果你在仓库根目录下，输出结果可以传递给`xargs rm`。

`git pack-redundant`接受标准输入中的对象列表。在检查需要哪些包时，将忽略任何给定的对象。在想要删除包含不可达对象的包时，以下命令非常有用。

```bash
git fsck --full --unreachable | cut -d ' ' -f3 | \ git pack-redundant --all | xargs rm
```




## `--all`

处理所有包。命令行上的任何文件名都会被忽略。

## `--alt-odb`

不要求来自替代对象目录（alternate object directories）包中的对象存在于本地包中。

## `--verbose`

将某些统计信息输出到`stderr`。会有轻微的性能影响。

## 另请

`(1)` `(1)` `(1)`

# GIT-PACK-REFS

## 名称

`git-pack-refs` - 打包分支头部和标签以实现高效仓库访问

## 语法

```
git pack-refs [--all] [--no-prune]
```

## 描述

传统上，分支和标签的末端（统称为`refs`）存储在`$GIT_DIR/refs`目录下的（子）目录中，每个引用对应一个文件。虽然许多分支头部往往经常更新，但大多数标签和某些分支头部从未更新过。当仓库有数百或数千个标签时，这种“每个引用一个文件”的格式既浪费空间又影响性能。

此命令通过将引用存储在单个文件`$GIT_DIR/packed-refs`中来解决存储和性能问题。当传统的`$GIT_DIR/refs`层级结构中缺少引用时，将在该文件中查找，如果找到则使用。

对分支的后续更新始终会在`$GIT_DIR/refs`目录层级下创建新文件。

处理引用过多仓库的推荐做法是：使用`--all`一次打包其引用，并偶尔运行`git pack-refs`。根据定义，标签是静态的，预计不会更改。分支头部将通过初始的`pack-refs --all`进行打包，但只有当前活跃的分支头部变为解包状态，下一次`pack-refs`（不带`--all`）将保持它们为解包状态。

## `--all`

命令默认打包所有已经打包的标签和引用，并忽略其他引用。这是因为预计分支会进行活跃开发，打包它们的头部对性能没有帮助。此选项会导致分支头部也被打包。这对于具有许多历史兴趣分支的仓库非常有用。

## `--no-prune`

命令在打包后通常会删除`$GIT_DIR/refs`层级结构下的松散引用（loose refs）。此选项告诉它不要删除。

## 缺陷

在引入`packed-refs`机制之前编写的旧文档可能仍会说“.git/refs/heads/<branch>文件存在”，而其意思是“分支<branch>存在”。

# GIT-PARSE-REMOTE

## 名称

`git-parse-remote` - 解析远程仓库访问参数的程序

## 语法

```
. "$(git --exec-path)/git-parse-remote"
```

## 描述

此脚本包含在各种脚本中，提供解析`$GIT_DIR/remotes/`和`$GIT_DIR/branches/`下的文件以及与获取、提取和推送相关的配置变量的程序。

# GIT-PATCH-ID

## 名称

`git-patch-id` - 为补丁计算唯一 ID 标识符

## 语法

```
git patch-id [--stable | --unstable] < <patch>
```

## 描述

“补丁 ID”仅仅是补丁相关文件差异的`SHA-1`之和，忽略了空格和行号。因此，它是“相对稳定的”，但同时也具有相对唯一性，即两个具有相同“补丁 ID”的补丁几乎可以认为是同一个东西。

因此，你可以使用此工具来寻找可能的重复提交。

在处理`git diff-tree`输出时，它利用了补丁带有提交对象名称前缀的事实，并输出两个 40 字节的十六进制字符串。第一个字符串是补丁 ID，第二个字符串是提交 ID。这可以用于从补丁 ID 到提交 ID 的映射。

## `--stable`

使用“稳定的”哈希和作为补丁 ID。使用此选项时：

- 重排组成补丁的文件差异不会影响 ID。特别是，通过使用两个不同的`-O<orderfile>`设置比较同一个两个树产生的两个补丁将产生相同的补丁 ID 签名，从而允许计算结果被用作键来索引关于两个树之间更改的一些元信息；

- 结果与`git` 1.9及更早版本产生的值不同，或与配置了“不稳定”哈希（见下文`--unstable`）时产生的值不同——即使在未使用任何`-O<orderfile>`获取的差异输出上也是如此，这使得存储此类“不稳定”或历史补丁 ID 的现有数据库无法使用。

如果`patchid.stable`设置为`true`，则为默认值。

## `--unstable`

使用“不稳定的”哈希作为补丁 ID。使用此选项时，产生的结果与`git` 1.9及更早版本产生的`patch-id`值兼容。拥有存储由`git` 1.9及更早版本产生的补丁 ID 的现有数据库（且不处理重排补丁）的用户可能想要使用此选项。

这是默认值。

## `<patch>`

用于创建 ID 的差异。

# GIT-PRUNE-PACKED

## 名称

`git-prune-packed` - 移除已在包文件中的额外对象

## 语法

```
git prune-packed [-n|--dry-run] [-q|--quiet]
```

## 描述

此程序在`$GIT_OBJECT_DIRECTORY`中搜索当前存在于包文件以及独立对象目录中的所有对象。

此类额外对象将被移除。

包是对象的集合，每个对象单独压缩并应用了增量压缩，存储在单个文件中，并关联一个索引文件。

包用于减少镜像系统、备份引擎、磁盘存储等的负载。

### 选项

`-n, --dry-run`
不实际删除任何对象，仅显示将要删除的对象。

`-q, --quiet`
静默进度指示器。

## 另请

`(1)` `(1)`

# GIT-PRUNE

## 名称

`git-prune` - 从对象数据库中清理所有不可达对象

## 语法

```
git prune [-n] [-v] [--expire <expire>] [--] [<head>...]
```

## 描述

**注意**

在大多数情况下，用户应该运行`git gc`，它会调用`git prune`。参见下文“备注”部分。

它使用`refs/`中所有可用引用运行`git fsck --unreachable`，可选在命令行上指定额外的对象组，并从对象数据库中清理从这些头部对象任不可达的所有解包对象。此外，它通过运行`git prune-packed`清理同样位于包中的解包对象。它还会移除`.git/shallow`中无法通过任何引用可达的条目。

注意，不可达的已包对象将保留。如果不需要，请参阅`(1)`。

### 选项

`-n, --dry-run`
不删除任何内容；仅报告将要删除的内容。

`-v, --verbose`
报告所有被移除的对象。

`--`
不再将任何参数解释为选项。

`--expire <time>`
仅对于`<time>`的松散对象过期。

`<head>...`
除了从我们的任何引用可达的对象外，还保留从列出的`<head>`可达的对象。

## 示例

清理未被你的仓库或其他通过`.git/objects/info/alternates`借用你仓库的其他使用的使用的：

```
$ git prune $(cd ../another && git rev-parse --all)
```

## 备注

在大多数情况下，用户不需要直接调用`git prune`，而是应该调用`git gc`，它会处理修剪以及许多其他维护任务。

关于哪些对象会被考虑进行修剪，请参见`git fsck`的`--unreachable`选项。

## 参见

`(1)` `(1)` `(1)`

# GIT-PULL

## 名称

`git-pull` - 从另一个仓库或本地分支获取内容并集成

## 概要

```
git pull [options] [<repository> [<refspec>...]]
```

## 描述

将远程仓库的更改合并到当前分支。在默认模式下，`git pull`是`git fetch`后接`git merge FETCH_HEAD`的简写。

更准确地说，`git pull`带有给定参数运行`git fetch`并调用`git merge`将获取到的分支头合并到当前分支。使用`--rebase`时，它会运行`git rebase`而不是`git merge`。

`<repository>`应该是传递给`(1)`的远程仓库名称。`<refspec>`可以指定任意远程引用（例如，标签名称），甚至是一组具有相应远程追踪分支的引用（例如，`refs/heads/*:refs/remotes/origin/*`），但通常它是远程仓库中分支的名称。

`<repository>`和`<branch>`的默认值是从`(1)` `--track`设置的当前分支的“remote”和“merge”配置中读取的。

假设存在以下历史且当前分支为`"master"`：

```
A---B---C master on origin / D---E---F---G master ^ origin/master in your repository
```

那么，“`git pull`”将获取并重放远程`master`分支自分叉本地`master`（即`E`）以来的所有更改，直到其当前提交（`C`）位于`master`之上，并将结果记录在一个新的提交中，同时包含两个父提交的名称以及用户描述更改的日志消息。

```
A---B---C origin/master / \ D---E---F---G---H master
```




详情请参见 (1)，包括如何展示和处理冲突。

在 Git 1.7.0 或更高版本中，若要取消冲突的合并，请使用 `git reset --merge`。**警告**：在旧版本的 Git 中，不建议在有未提交更改的情况下运行 `git pull`：虽然可行，但它会让你处于一种在发生冲突时可能难以撤销的状态。

如果任何远程更改与本地未提交的更改重叠，合并将自动取消且工作树不受影响。通常最好在拉取之前让任何本地更改处于就绪状态，或者使用 (1) 将它们存储起来。

### 选项

- `-q, --quiet`

  此选项将传递给底层的 `git-fetch` 以抑制传输期间的报告，传递给底层的 `git-merge` 以抑制合并期间的输出。

- `-v, --verbose`

  将 `--verbose` 传递给 `git-fetch` 和 `git-merge`。

- `--[no-]recurse-submodules[=yes|on-demand|no]`

  此选项控制是否也获取所有已填充子模块的新提交（参见 (1) 和 (5)）。这对于获取合并子模块提交所需的数据可能是必要的，这是 Git 在 1.7.3 中学会的功能。注意，合并的结果不会检子模块检，之后必须调用 `git submodule update` 以使工作树与合并结果同步。

### 与合并相关的选项

- `--commit, --no-commit`

  执行合并并提交结果。此选项可覆盖 `--no-commit`。

  使用 `--no-commit` 执行合并但假装合并失败且不自动提交，以便给用户在提交前检查和进一步调优合并结果的机会。

- `--edit, -e, --no-edit`

  在对成功的机械合并进行提交之前调用编辑器，进一步编辑自动生成的合并消息，以便用户可以解释并证明合并的理由。`--no-edit` 选项可接受自动生成的消息（这通常不建议这样做）。

  旧脚本可能依赖于“不允许用户编辑合并日志消息”的历史行为。当他们运行 `git merge` 时会看到编辑器被打开。为了方便将此类脚本调整为更新后的行为，可以在它们开头将环境变量 `GIT_MERGE_AUTOEDIT` 设置为 `no`。

- `--ff`

  当合并解决为快进（fast-forward）时，仅更新分支指针，而不创建合并提交。这是默认行为。

- `--no-ff`

  即使合并解决为快进，也创建一个合并提交。这是合并带注释（且可能已签名的）标签时的默认行为。

- `--ff-only`

  除非当前 `HEAD` 已经是最新的或合并可以解决为快进，否则拒绝合并并以非零状态退出。

- `--log[=<n>], --no-log`

  除了分支名称外，使用最多 `<n>` 个正在合并的实际提交的单行描述来填充日志消息。另参见 (1)。

  使用 `--no-log` 不列出正在合并的实际提交的单行描述。

- `--stat, -n, --no-stat`

  在合并结束时显示差异统计（diffstat）。差异统计也由配置选项 `merge.stat` 控制。

  使用 `-n` 或 `--no-stat` 不在合并结束时显示差异统计。

- `--squash, --no-squash`

  产生工作树和索引状态，就像发生过真实的合并一样（除了合并信息外），但实际上不会创建提交、移动 `HEAD` 或记录 `$GIT_DIR/MERGE_HEAD`（以导致下一次 `git commit` 命令创建一个合并提交）。这允许你在当前分支上创建一个单一提交，其效果等同于合并另一个分支（如果是章鱼合并则为多个）。

  使用 `--no-squash` 执行合并并提交结果。此选项可覆盖 `--squash`。

- `-s <strategy>, --strategy=<strategy>`

  使用给定的合并策略；可以多次提供以按它们应该尝试的顺序指定策略。如果没有 `-s` 选项，则使用内置策略列表（合并单个头节点时使用 `git merge-recursive`，否则使用 `git merge-octopus`）。

- `-X <option>, --strategy-option=<option>`

  将特定合并策略的选项传递给合并策略。

- `--verify-signatures, --no-verify-signatures`

  验证正在合并的提交具有良好且受信任的 GPG 签名，否则则中止合并。

- `--summary, --no-summary`

  `--stat` 和 `--no-stat` 的同义词；这些已弃用并将在未来移除。

- `-r, --rebase[=false|true|preserve]`

  设置为 `true` 时，获取后将当前分支重基到上游分支。如果存在对应上游分支的远程追踪分支，且上游分支自上次获取以来已重基，则利用该信息避免重基本地更改。

  设置为 `preserve` 时，使用传递给 `git rebase` 的 `--preserve-merges` 选项进行重基，这样本地创建的合并提交将不会平坦。

  设置为 `false` 时，将当前分支合并到上游分支。

  如果你想让 `git pull` 始终使用 `--rebase` 而不是合并，请参见 (1) 中的 `pull.rebase`、`branch.<name>.rebase` 和 `branch.autoSetupRebase`。

  **注意**

  这是一个潜在危险的操作模式。它会重写历史，这对于已经发布的历史来说并不妙妙。除非你已仔细阅读了 (1)。

- `--no-rebase`

  覆盖早前的 `--rebase`。

### 与获取相关的选项

- `--all`

  获取所有远程仓库。

- `-a, --append`

  将获取的引用名称和对象名称追加到 `.git/FETCH_HEAD` 的现有内容。如果不使用此选项，`.git/FETCH_HEAD` 中的旧数据将被覆盖。

- `--depth=<depth>`

  对于通过 `git clone` 使用 `--depth=<depth>` 选项创建的浅仓库，深化或缩短其历史，从每个远程分支历史末端指定的指定的提交数量。深层提交的标签不会被获取。

- `--unshallow`

  如果源仓库是完整的，将浅仓库转换为完整仓库，移除浅仓库带来的所有限制。

  如果源仓库是浅的，则获取尽可能多的内容，使当前仓库与源仓库具有相同的历史。

- `--update-shallow`

  默认情况下，从浅层仓库（shallow repository）获取数据时，`git fetch` 会拒绝需要更新 `.git/shallow` 的引用。此选项会更新 `.git/shallow` 并接受此类引用。

- `-f, --force`

  当 `git fetch` 使用 `<rbranch>:<lbranch>` 引用规范时，除非获取的远程分支 `<rbranch>` 是 `<lbranch>` 的后代，否则将拒绝更新本地分支 `<lbranch>`。此选项将覆盖该检查。

- `-k, --keep`

  保留下载的包文件（pack）。

- `--no-tags`

  默认情况下，指向从远程仓库下载对象的标签会被获取并存储在本地。此选项将禁用这种自动跟踪标签。可以通过 `remote.<name>.tagOpt` 设置指定远程的默认行为。见 (1)。

- `-u, --update-head-ok`

  默认情况下，`git fetch` 拒绝更新对应当前分支的头。此标志将禁用该检查。这完全用于 `git pull` 与 `git fetch` 通信的内部使用，除非你正在实现自己的 Porcelain 命令（用户界面），否则不应使用它。

- `--upload-pack <upload-pack>`

  当给定该参数且要获取的仓库由 `git fetch-pack` 处理时，会将 `--exec=<upload-pack>` 传递给命令，以指定在远程运行命令的非默认路径。

- `--progress`

  默认情况下，当连接终端时，进度状态会通过标准错误流报告，除非指定了 `-q`。此标志即使在标准错误流未重定向到终端也会强制报告进度状态。

- `<repository>`

  获取或 `pull` 操作源的“远程”仓库。该参数可以是 URL（见下文 GIT URLS 节）或远程名称（见下文 REMOTES 节）。

- `<refspec>`

  指定要获取哪些引用以及更新哪些本地引用。当命令行没有出现 `<refspec>` 时，要获取的引用将从 `remote.<repository>.fetch` 变量读取（见 (1)）。

  `<refspec>` 参数的格式为可选的加号 `+`，跟随源引用 `<src>`，然后是冒号 `:`，最后是目标引用 `<dst>`。当 `<dst>` 为空时，可以省略冒号。

  `tag <tag>` 等同于 `refs/tags/<tag>:refs/tags/<tag>`；它请求获取到指定标签的所有内容。

  匹配 `<src>` 的远程引用将被获取，如果 `<dst>` 不是空字符串，则匹配它的本地引用将使用 `<src>` 进行快进（fast-forward）。如果使用了可选的加号 `+`，即使没有导致快进更新，本地引用也会更新。

### Note

如果已知你要获取的远程分支经常被回滚（rewound）和变基（rebased），则预计其新端点不会是其之前端点（即上次获取时存储在你的远程追踪分支中的）的后代。你可能希望使用 `+` 符号指示此类分支需要非快进更新。目前没有方法确定或声明某个分支在具有此类行为的仓库中可用；执行操作的用户只需知道这是该分支预期的使用模式。

### Note

在 `git pull` 命令行直接列出多个 `<refspec>` 与在针对 `<repository>` 的配置中拥有多个 `remote.<repository>.fetch` 条目并运行不带任何显 `<refspec>` 参数的 `git pull` 命令是有区别的。命令行上显式列出的 `<refspec>` 在获取后始终合并到当前分支。换句话说，如果你列出了多个远程引用，`git pull` 将创建一个章鱼合并（Octopus merge）。相反，如果你在命令行上不列出任何显式 `<refspec>` 参数，`git pull` 将获取它在 `remote.<repository>.fetch` 配置中找到的所有 `<refspec>`，并仅将找到的 `<refspec>` 合并到当前分支。这是因为从远程引用创建章鱼合并很少见，而通过获取多个引用来一次性跟踪多个远程头通常是很有用的。

## GIT URLS

通常情况下，URL 包含有关传输协议、远程服务器地址以及仓库路径的信息。取决于传输协议，这些信息中的某些可能会缺失。

Git 支持 `ssh`、`git`、`http` 和 `https` 协议（此外，`ftp` 和 `ftps` 可用于获取，`rsync` 可用于获取和推送，但这些效率低下且已过时；请勿使用它们）。

原生传输（即 `git://` URL）不进行身份验证，在不安全的网络上应谨慎使用。

以下语法可以使用这些 URL：

```text
http[s]://host.xz[:port]/path/to/repo.git/

ftp[s]://host.xz[:port]/path/to/repo.git/
```

`ssh` 协议也可以使用另一种类似于 `scp` 的语法：

```text
[user@]host.xz:path/to/repo.git/
```

该语法仅在第一个冒号之前没有斜线时才会被识别。这有助于区分包含冒号的本地路径。例如，本地路径 `foo:bar` 可以被指定为绝对路径或 `./foo:bar` 以避免被误解为 ssh URL。

`ssh` 和 `git` 协议还支持 `~username` 扩展：

```text
[user@]host.xz:/~[user]/path/to/repo.git/
```

对于 Git 原生支持的本地仓库，可以使用以下语法：

```text
/path/to/repo.git/
```

这两种语法大部分情况下等效，但在克隆（cloning）时，前者意味着 `--local` 选项。详情见 (1)。

当 Git 不知道如何处理某种传输协议时，它会尝试使用 `remote-<transport>` 远程助手（如果存在）。要显式请求远程助手，可以使用以下语法：

```text
<transport>::<address>
```

其中 `<address>` 可以是路径、服务器和路径，或者是被调用的特定远程助手识别的任意类 URL 字符串。详情见 (1)。

如果有大量命名相似的远程仓库，且你想为它们使用不同的格式（以便你使用的 URL 被重写为可工作的 URL），你可以创建一个如下的配置节：

```text
[url "<actual url base>"]
    insteadOf = <other url base>
```

例如，使用以下配置：

```text
[url ""]
    insteadOf = host.xz:/path/to/
    insteadOf = work:
```

像 `"work:repo.git"` 或像 `"host.xz:/path/to/repo.git"` 的 URL 将在任何接受 `""` 作为 URL 的上下文中被重写。

如果你只想为推送重写 URL，可以创建一个如下的配置节：

```text
[url "<actual url base>"]
    pushInsteadOf = <other url base>
```

例如，使用以下配置：

```text
[url ""]
    pushInsteadOf =
```

像 `""` 的 URL 在推送时将被重写为 `" "`，但拉取（pull）仍将使用原始 URL。

## REMOTES

可以使用以下之一的名称代替 URL 作为 `<repository>` 参数：

- Git 配置文件中的远程仓库：`$GIT_DIR/config`；
- `$GIT_DIR/remotes` 目录下的文件；或
- `$GIT_DIR/branches` 目录下的文件。

所有这些项都允许你省略命令行上的 refspec，因为它们每个都包含一个 Git 将默认使用的 refspec。

### 配置文件中的命名远程仓库

你可以选择提供之前通过 (1) 配置的远程名称，甚至通过手动编辑 `$GIT_DIR/config` 文件来提供名称。该远程仓库的 URL 将用于访问仓库。当你没有在命令行上提供 refspec 时，将默认使用该远程的 refspec。配置文件中的条目所示：

```text
[remote "<name>"]
    url = <url>
    pushurl = <pushurl>
    push = <refspec>
    fetch = <refspec>
```

`<pushurl>` 仅用于推送。它是可选的，默认为 `<url>`。

### `$GIT_DIR/remotes` 中的命名文件

你可以选择提供 `$GIT_DIR/remotes` 中的一个文件名。该文件中的 URL 将用于访问仓库。当你没有在命令行上提供 refspec 时，该文件中的 refspec 将作为默认。该文件应具有以下格式：

```text
URL: one of the above URL format
Push: <refspec>
Pull: <refspec>
```

`Push:` 行被 `git push` 使用，`Pull:` 行被 `git pull` 和 `git fetch` 使用。可以指定多个 `Push:` 和 `Pull:` 行用于额外的分支映射。

#### `$GIT_DIR/branches` 中的具名文件

你可以选择提供 `$GIT_DIR/branches` 中某一个文件的名称。该文件中的 URL 将被用于访问仓库。此文件应具有以下格式：

```text
<url>#<head>
```

`<url>` 是必需的；`#<head>` 是可选。

根据操作类型，如果你没有在命令行中提供 refspec，Git 将使用以下 refspec 之一。`<branch>` 是 `$GIT_DIR/branches` 中该文件的文件名，`<head>` 默认为 `master`。

`git fetch` 使用：

```text
refs/heads/<head>:refs/heads/<branch>
```

`git push` 使用：

```text
HEAD:refs/heads/<head>
```




## 合并策略

合并机制（`git merge` 和 `git pull` 命令）允许通过 `-s` 选项选择后端**合并策略**。某些策略还可以接受自己的选项，这些选项可以通过向 `git merge` 和/或 `git pull` 传递 `-X<option>` 参数来传递。

### `resolve`

该策略只能使用 3 路合并算法解析两个头（即当前分支和你拉取的的另一个分支）。它会尝试仔细检测交叉合并（criss-cross merge）歧义，并被认为是安全且快速的。

### `recursive`

该策略只能使用 3 路合并算法解析两个头。当存在多个共同祖先可以用于 3 路合并时，它会创建一个共同祖先的合并树，并将其作为 3 路合并的引用树。根据对 Linux 2.6 内核开发历史中实际合并提交进行的测试，这种方法报告可以减少合并冲突，且不会引起错误合并。此外，该策略还可以检测并处理涉及重命名的合并。这是拉取或合并一个分支时的默认合并策略。

`recursive` 策略可以接受以下选项：

#### `ours`

此选项强制通过倾向于 `our`（我们的）版本来自动地解决冲突的代码块。来自另一个树的与我们侧不冲突的更改将反映在合并结果中。对于二进制文件，整个内容取自我们侧。

这不应与 `ours` 合并策略混淆，后者根本不看另一个树包含什么。它会丢弃另一个树所做的一切，声明 `our`（我们的）历史包含了其中发生的所有内容。

#### `theirs`

这是 `ours` 的相反操作。

#### `patience`

使用此选项时，`merge-recursive` 会花额外的时间来避免有时因不重要的匹配行（例如来自不同函数的大括号）而导致的错误合并。当要合并的分支分歧很大时请使用此选项。另见 `(1)--patience`。

#### `diff-algorithm=[patience|minimal|histogram|myers]`

告诉 `merge-recursive` 使用不同的差异算法，这有助于避免因不重要的匹配行（如不同函数的大括号）而导致的错误合并。另见 `(1)--diff-algorithm`。

#### `ignore-space-change`、`ignore-all-space`、`ignore-space-at-eol`

为了进行 3 路合并，将具有指示类型空白字符更改的行视为未更改。如果空白更改与该行的其他更改混合在一起，则不会被忽略。另见 `(1)-b`、`-w` 和 `--ignore-space-at-eol`。

如果 `their`（他们的）版本仅对某行引入了空白更改，则使用 `our`（我们的）版本；

如果 `our` 版本引入了空白更改但 `their` 版本包含实质性更改，则使用 `their` 版本；

否则，按通常方式进行合并。

#### `renormalize`

在解析 3 路合并时，对文件的所有三个阶段运行虚拟的检出和检入。此选项旨在用于合并具有不同清理过滤器（clean filters）或行尾归一化规则的分支。详情见 (5) 中的“合并具有不同 checkin/checkout 属性的分支”。

#### `no-renormalize`

禁用 `renormalize` 选项。这将覆盖 `merge.renormalize` 配置变量。

#### `rename-threshold=<n>`

控制用于重命名检测的相似性阈值。另见 `(1)-M`。

#### `subtree[=<path>]`

此选项是 `subtree` 策略的一种更高级的形式，该策略在合并时会猜测两个树必须如何移动以相互匹配。相反，指定的路径会被加上前缀（或从开头删除），以使两棵树的形状相匹配。

### `octopus`

该策略解决多于两个头的情况，但拒绝执行需要手动解决的复杂合并。它主要用于将多个主题分支头打包在一起。这是拉取或合并一个以上分支时的默认合并策略。

### `ours`

该策略解决任意数量的头，但合并后的树始终是当前分支头，有效地忽略了来自所有其他分支的所有更改。它用于取代侧分支旧开发历史。注意，这与 `recursive` 合并策略的 `-Xours` 选项不同。

### `subtree`

这是修改后的 `recursive` 策略。在合并树 A 和 B 时，如果 B 对应于 A 的子树，则先调整 B 以匹配 A 的树结构，而不是在同一层级读取树。这种调整也会对共同祖先树进行。

对于使用 3 路合并的策略（包括默认的 `recursive`），如果在两个分支上都进行了更改，但随后在其中一个分支上撤销了，该更改将存在于合并结果中；有些人发现这种行为令人困惑。这是因为只考虑了头和合并基（merge base）。

## 默认行为

人们经常在不给出任何参数的情况下使用 `git pull`。传统上，这等同于执行 `git pull origin`。然而，当在分支 `<name>` 存在配置 `branch.<name>.remote` 时，将使用该值而非 `origin`。

为了确定使用什么 URL 进行抓取，会查询配置 `remote.<origin>.url` 的值，如果没有该变量，则使用 `$GIT_DIR/remotes/<origin>` 文件中的 `URL:` 行。

为了确定在命令行上不带任何 refspec 参数运行命令时要抓取哪些远程分支（并可选存储在远程跟踪分支中），会查询配置 `remote.<origin>.fetch` 的值，如果没有，则查询 `$GIT_DIR/remotes/<origin>` 文件并使用其 `Pull:` 行。除了 OPTIONS 部分中描述的 refspec 格式外，你还可以拥有如下的通配符 refspec（globbing refspec）：

```
refs/heads/*:refs/remotes/origin/*
```

通配符 refspec 必须有一个非空的 RHS（即必须将抓取的内容存储在远程跟踪分支中），且其 LHS 和 RHS 必须以 `/*` 结尾。上述指定了所有远程分支都使用 `refs/remotes/origin/` 层级下同名的远程跟踪分支进行跟踪。

确定在抓取后合并哪个远程分支的规则有点复杂，以防破坏向后兼容性。

如果在 `git pull` 命令行上给出了显式 refspec，则它们都将被合并。

当命令行上没有提供 refspec 时，`git pull` 使用配置或 `$GIT_DIR/remotes/<origin>` 中的 refspec。在这种情况下，适用以下规则：

1. 如果当前分支 `<name>` 存在 `branch.<name>.merge` 配置，则该配置为远程站点合并的分支。
2. 如果 refspec 是通配符，则不合并任何内容。
3. 否则，合并第一个 refspec 的远程分支。

## 示例

更新你克隆仓库的远程跟踪分支，然后将其中之一合并到你的当前分支：

```
$ git pull
$ git pull origin
```

通常合并的分支是远程仓库的 `HEAD`，但具体选择由 `branch.<name>.remote` 和 `branch.<name>.merge` 选项决定；详情请参见 (1)。

将下述远程分支合并到当前分支：

```bash
$ git pull origin next
```

这会将 `next` 的副本临时保存在 `FETCH_HEAD` 中，但不会更新任何远程跟踪分支。使用远程跟踪分支，可以通过调用 `fetch` 和 `merge` 来实现相同的操作：

```bash
$ git fetch origin
$ git merge origin/next
```




如果你尝试的 `pull` 导致了复杂的冲突并想要重新开始，可以使用 `git reset` 进行恢复。

## BUGS

目前，使用 `--recurse-submodules` 只能在已检出的子模块中获取新提交。例如，当上游在刚刚获取的主项目提交中添加了新的子模块时，子模块本身无法被获取，导致以后在不再次执行 `fetch` 的情况下无法检出该子模块。这预计将在未来的 Git 版本中修复。

## 另参见

(1), (1), (1)

***

# GIT-PUSH

## 名称

`git-push` - 更新远程引用以及关联对象

## 概要

`git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>] [--repo=<repository>] [-f | --force] [--prune] [-v | --verbose] [-u | --set-upstream] [--signed] [--force-with-lease[=<refname>[:<expect>]]] [--no-verify] [<repository> [<refspec>...]]`

## 描述

使用本地引用更新远程引用，同时发送完成给定引用所需的对象。

通过在仓库中设置钩子（hooks），你可以在每次推送时让仓库发生一些有趣的变化。详情请参见 (1) 的文档。

当命令行没有通过 `<repository>` 参数指定推送到何处时，将查询当前分支的 `branch.*.remote` 配置来确定推送位置。如果缺少该配置，则默认为 `origin`。

当命令行没有通过 `<refspec>...` 参数或 `--all`、`--mirror`、`--tags` 选项指定推送内容时，命令将通过查询 `remote.*.push` 配置查找默认的 `<refspec>`；如果未找到，则遵循 `push.default` 配置来决定推送内容（`push.default` 的含义参见 (1)）。

### 选项

#### `<repository>`

推送操作的目标“远程”仓库。此参数可以是 URL（参见下文 GIT URLS 节）或远程名称（参见下文 REMOTES 节）。

#### `<refspec>...`

指定用什么源对象更新哪个目标引用。`<refspec>` 参数的格式为可选的加号 `+`，后跟源对象 `<src>`，接着是冒号 `:`，然后目标引用 `<dst>`。

`<src>` 通常是你想要推送的分支名称，但也可以是任意的“SHA-1 表达式”，例如 `master~4` 或 `HEAD`（参见 (7)）。

`<dst>` 告诉远程端的哪个引用通过此次推送进行更新。此处不能使用任意表达式，必须指定具体的引用名称。如果在不带任何 `<refspec>` 参数的情况下执行 `git push [<repository>]`，并设置为通过 `remote.<repository>.push` 配置变量来更新目标地处的某个引用，则可以省略 `:<dst>` 部分——此类推送将更新在命令行无 `<refspec>` 的情况下 `<src>` 通常更新的引用。否则，缺少 `:<dst>` 表示更新与 `<src>` 相同的引用。

由 `<src>` 引的对象用于更新远程端的 `<dst>` 引用。默认情况下，只有当 `<dst>` 不是标签（注释标签或轻量级标签）且可以对 `<dst>` 进行快进（fast-forward）时才允许这样做。通过添加可选的前缀 `+`，你可以告诉 Git 即使在默认不允许的情况下（例如它不是快进）也更新 `<dst>` 引用。这不会尝试将 `<src>` 合并到 `<dst>`。详情参见下文示例。

`tag <tag>` 等同于 `refs/tags/<tag>:refs/tags/<tag>`。

推送一个空 `<src>` 允许你从远程仓库中删除 `<dst>` 引用。

特殊的 refspec `:`（或允许非快进更新的 `+:`）引导 Git 推送“匹配”分支：对于本地存在的每个分支，如果远程端已存在同名分支，则更新远程端。

#### `--all`

推送所有分支（即 `refs/heads/` 下的引用）；不能与其他 `<refspec>` 一起使用。

#### `--prune`

删除没有本地对应项远程分支。例如，如果本地不再存在同名的分支，则远程分支 `tmp` 将被删除。这也尊重 refspecs，例如 `git push --prune remote refs/heads/*:refs/tmp/*` 将确保如果 `refs/heads/foo` 不存在，远程的 `refs/tmp/foo` 将被删除。

#### `--mirror`

不是为要推送的引用命名，而是指定 `refs/` 下的所有引用（包括但不限于 `refs/heads/`、`refs/remotes/` 和 `refs/tags/`）镜像到远程仓库。新创建的本地引用将被送到远程，本地更新的引用将在远程端强制更新，删除的引用将从远程端移除。如果设置了配置选项 `remote.<remote>.mirror`，则默认如此。

#### `-n, --dry-run`

执行除实际发送更新以外的所有操作。

#### `--porcelain`

产生机器可读的输出。每个引用的状态行将用制表符分隔并发送 stdout 而不是 stderr。将给出引用的完整符号名称。

#### `--delete`

所有列出的引用都从远程仓库删除。这等同于在所有引用前加冒号。

#### `--tags`

除了命令行显式列出的 refspecs 之外，`refs/tags` 下的所有引用都会被推送。

#### `--follow-tags`

推送所有在没有此选项时会被推送的引用，并且推送 `refs/tags` 中远程端缺失、但指向从被推送的引用可达的提交对象（commit-ish）的注释标签。这也可以通过配置变量 `push.followTags` 进行指定。更多信息请参见 (1) 中的 `push.followTags`。

#### `--signed`

对更新接收端引用的推送请求进行 GPG 签名，以便通过钩子检查和/或被记录。接收端的详情参见 (1)。

#### `--[no-]atomic`

如果可用，在远程端使用原子事务。要么所有引用都更新，或者在出错时不更新任何引用。如果服务器不支持原子推送，推送将失败。

#### `--receive-pack=<git-receive-pack>, --exec=<git-receive-pack>`

远程端 `git-receive-pack` 程序的路径。有时在通过 `ssh` 推送到远程仓库时有用，且你没有在默认 `$PATH` 目录下的该程序。

#### `--[no-]force-with-lease, --force-with-lease=<refname>, --force-with-lease=<refname>:<expect>`

通常，`git push` 拒绝更新不是用于覆盖它的本地引用祖先的远程引用。

如果远程引用的当前值是预期值，则此选项将覆盖此限制。否则，`git push` 失败。

假设你必须 rebase 你已经发布的内容。你将需要绕过“必须快进”规则，以便用 rebase 的历史替换你最初发布的历史。如果在你 rebase 期间，其他人在你的原始历史基础上构建了内容，远程分支的顶部可能会随着她的提交而推进，盲目使用 `--force` 推送将丢失她的工作。

此选项允许你声明，你期望正在更新的历史是你 rebase 并想要替换的历史。如果远程引用仍然指向你指定的提交，你可以确定没有其他人对该引用做过任何操作。这就像在不显式锁定的情况下对引用获取了“租约”（lease），只有当“租约”仍然有效时，远程引用才会被更新。

`--force-with-lease` 单独使用时（不指定细节），将通过要求所有将被更新的远程引用的当前值与我们对应的远程跟踪分支相同来保护它们。

`--force-with-lease=<refname>` 在不指定预期值的情况下，如果命名的 ref（单独）将要更新，它将要求其当前值与我们拥有的远程跟踪分支一致，从而保护它。

`--force-with-lease=<refname>:<expect>` 如果命名的 ref（单独）将要更新，它将要求其当前值与指定的值 `<expect>` 一致（该值允许与我们为该 refname 提供的远程跟踪分支不同，在使用这种形式时我们甚至不需要拥有该远程跟踪分支）。

注意，除了 `--force-with-lease=<refname>:<expect>` 之外，所有显式指定 ref 预期当前值的其他形式仍处于实验阶段，随着我们对该功能经验的增加，其语义可能会发生。

`--no-force-with-lease` 将取消命令行上之前所有的 `--force-with-lease`。

#### `-f, --force`

通常，命令会拒绝更新不是覆盖它的本地 ref 祖先的远程 ref。此外，当使用 `--force-with-lease` 选项时，命令会拒绝更新当前值与预期不符的远程 ref。

此标志禁用了这些检查，可能会导致远程仓库丢失提交；请谨慎使用。

注意，`--force` 应用于所有推送的 ref，因此将其与设置为 `matching` 的 `push.default` 或与配置了多个 `remote.*.push` 推送目标使用可能会覆盖当前分支以外的 ref（包括严格落后于其远程对应的本地 ref）。要强制推送到单个分支，请在推送的 refspec 前使用 `+`（例如，使用 `git push origin +master` 强制推送 master 分支）。详情见上文的 `<refspec>`... 部分。

#### `--repo=<repository>`

此选项等同于 `<repository>` 参数。如果两者都指定，则命令行参数具有优先级。

#### `-u, --set-upstream`

对于每个更新或成功推送的分支，添加上游（跟踪）引用，该引用供不带参数的 (1) 和其他命令使用。更多信息请参阅 (1) 中的 `branch.<name>.merge`。

#### `--[no-]thin`

这些选项被传递给 (1)。当发送者和接收者共享许多相同对象时，薄传输会显著减少发送的数据量。默认是 `--thin`。

#### `-q, --quiet`

抑制所有输出，包括更新 ref 的列表，除非发生错误。进度不会报告到标准错误流。

#### `-v, --verbose`

详细模式运行。

#### `--progress`

默认情况下，当附加到终端时，进度状态会在标准错误流上报告，除非指定了 `-q`。此标志即使在标准错误流未重定向到终端的情况下强制报告进度状态。

#### `--recurse-submodules=check|on-demand`

确保推送的版本所使用的所有子模块提交在远程跟踪分支上可用。如果使用 `check`，Git 将验证要推送版本中更改的所有子模块提交在子模块的至少一个远程上可用。如果缺少任何提交，推送将中止并以非零状态退出。如果使用 `on-demand`，所有要推送版本中更改的子模块都会被推送。如果 `on-demand` 无法推送所有必要的版本，也将中止并以非零状态退出。

#### `--[no-]verify`

切换预推送钩子（见 (5)）。默认是 `--verify`，为钩子提供了阻止推送的机会。使用 `--no-verify` 则将完全跳过钩子。

## GIT URLS

通常，URL 包含有关传输协议、远程服务器地址以及仓库路径的信息。根据传输协议的不同，这些部分信息可能会缺失。

Git 支持 `ssh`、`git`、`http` 和 `https` 协议（`ftp` 和 `ftps` 可用于获取，`rsync` 可用于获取和推送，但这些效率低下且已过弃；请勿使用）。

原生传输（即 `git://` URL）不进行身份验证，在不安全的网络上应谨慎使用。

可以使用以下语法配合它们：

`http[s]://host.xz[:port]/path/to/repo.git/`

`ftp[s]://host.xz[:port]/path/to/repo.git/`

`ssh` 协议还可使用另一种类似 scp 的语法：

`[user@]host.xz:path/to/repo.git/`

只有在第一个冒号之前没有斜杠时，该语法才会被识别。这有助于区分包含冒号的本地路径。例如，本地路径 `foo:bar` 可以指定为绝对路径或 `./foo:bar`，以避免被误解为 ssh url。

`ssh` 和 `git` 协议额外支持 `~username` 扩展：

`[user@]host.xz:/~[user]/path/to/repo.git/`

对于 Git 原生支持的本地仓库，可以使用以下语法：

`/path/to/repo.git/`

这两种语法在大多数情况下是等等的，但在克隆时，前者隐含了 `--local` 选项。详情见 (1)。

当 Git 不知道如何处理某种传输协议时，它会尝试使用 `remote-<transport>` 远程助手（如果存在的话）。要显式请求远程助手，可以使用以下语法：

`<transport>::<address>`

其中 `<address>` 可以是一个路径、服务器和路径，或者是被调用的特定远程助手所识别的任意类 URL 字符串。详情见 (1)。

如果存在大量命名相似的远程仓库，且你想为它们使用不同的格式（以便你使用的 URL 将被重写为可以运行的 URL），你可以创建一个如下形式的配置段：

`[url "<actual url base>"] insteadOf = <other url base>`

例如，使用以下内容：

`[url ""] insteadOf = host.xz:/path/to/ insteadOf = work:`

像 `work:repo.git` 或像 `host.xz:/path/to/repo.git` 的 URL 在任何接受 URL 为空的上下文中都会被重写。

如果你只想为推送重写 URL，可以创建一个如下形式的配置段：

`[url "<actual url base>"] pushInsteadOf = <other url base>`

例如，使用以下内容：

`[url ""] pushInsteadOf =`

像空字符串这样的 URL 在推送时将被重写为空字符串，但拉取将仍然使用原始 URL。

## REMOTES

可以使用以下之一的名称代替 `<repository>` 参数：

- Git 配置文件中的远程：`$GIT_DIR/config`
- `$GIT_DIR/remotes` 目录下的文件
- `$GIT_DIR/branches` 目录下的文件

这些都允许你在命令行中省略 refspec，因为它们各包含一个 Git 将默认使用的 refspec。

### 配置文件中的命名远程

你可以选择提供你之前通过 (1)、(1) 甚至通过手动编辑 `$GIT_DIR/config` 文件配置的远程名称。该远程的 URL 将用于访问仓库。当你不在命令行提供 refspec 时，该远程的 refspec 将作为默认。配置文件中的条目如下：

`[remote "<name>"] url = <url> pushurl = <pushurl> push = <refspec> fetch = <refspec>`

`<pushurl>` 用于推送。它是可选的，默认为 `<url>`。

### `$GIT_DIR/remotes` 中的命名文件

你可以选择提供 `$GIT_DIR/remotes` 中的文件名。该文件中的 URL 将用于访问仓库。当你不在命令行提供 refspec 时，该文件中的 refspec 将作为默认。此文件应遵循以下格式：

`URL: 上述 URL 格式 Push: <refspec> Pull: <refspec>`

`Push:` 行被 `git push` 使用，`Pull:` 行被 `git pull` 和 `git fetch` 使用。可以指定多个 `Push:` 和 `Pull:` 行来实现额外的分支映射。

### `$GIT_DIR/branches` 中的命名文件

你可以选择提供 `$GIT_DIR/branches` 中的文件名。该文件中的 URL 将用于访问仓库。此文件应遵循以下格式：

`<url>#<head>`

`<url>` 是必须的；`#<head>` 是可选的。

取决于操作类型，如果你没有在命令行中提供 refspec，`git` 将使用以下 refspecs 之一。`<branch>` 是 `$GIT_DIR/branches` 中该文件名，而 `<head>` 默认为 `master`。

`git fetch` 使用：

```text
refs/heads/<head>:refs/heads/<branch>
```

`git push` 使用：

```text
HEAD:refs/heads/<head>
```

# 输出

`git push` 的输出取决于所使用的传输方法；本节描述了通过 Git 协议（本地或通过 `ssh`）推送时的输出。

推送的状态以表格形式输出，每行代表单个引用（ref）的状态。每行的格式如下：

```text
<flag> <summary> <from> -> <to> (<reason>)
```

如果使用了 `--porcelain`，则输出的每行格式为：

```text
<flag> \t <from>:<to> \t <summary> (<reason>)
```




只有在使用`--porcelain`或`--verbose`选项时，才会显示已更新 ref 的状态。

## flag
一个表示 ref 状态的单个字符：
- `(space)`：表示成功推送了快进（fast-forward）；
- `+`：表示强制更新成功；
- `-`：表示删除 ref 成功；
- `*`：表示成功推送了新 ref；
- `!`：表示 ref 被拒绝或推送失败；以及
- `=`：表示 ref 是最新的，不需要推送。

## summary
对于推送成功的 ref，summary 以适用于作为`git log`参数的形式显示 ref 的旧值和新值（大多数情况下为`<old>..<new>`，对于强制非快进更新则为`<old>...<new>`）。

对于失败的更新，提供了更多细节：
- **rejected**（被拒绝）：Git 完全没有尝试发送该 ref，通常是因为它不是快进且你没有进行强制更新。
- **remote rejected**（远程拒绝）：远程端拒绝更新。通常是由远程端的钩子（hook）引起的，或者是因为远程仓库启用了以下安全选项之一：`receive.denyCurrentBranch`（推送到已检出的分支）、`receive.denyNonFastForwards`（针对强制非快进更新）、`receive.denyDeletes`或`receive.denyDeleteCurrent`。参见 (1)。
- **remote failure**（远程失败）：远程端没有报告 ref 的成功更新，可能是因为远程端的临时错误、网络连接中断或其他瞬态错误。

## from
正在推送的本地 ref 的名称，去掉了其`refs/<type>/`前缀。在删除操作的情况下，会省略本地 ref 的名称。

## to
正在更新的远程 ref 的名称，去掉了其`refs/<type>/`前缀。

## reason
人类可读的解释。对于推送成功的 ref，不需要解释。对于推送失败的 ref，将描述失败的原因。

# 关于快进（FAST-FORWARDS）的说明

当更新将一个分支（更广义地说，一个引用）从指向提交 A 更改为指向另一个提交 B 时，当且仅当 B 是 A 的后代时，这种更新被称为快进更新。

在从 A 到 B 的快进更新中，原始提交 A 之上构建的提交集是新提交 B 之上构建的提交集的子集。因此，它不会丢失任何历史。

相比之下，非快进更新将丢失历史。例如，假设你和另一个人从同一个提交 X 开始，你构建了通往提交 B 的历史，而另一个人构建了通往提交 A 的历史。历史如下：

```
B
/
---X---A
```

假设另一个人已经将通往 A 的更改推回了你们获取原始提交 X 的原始仓库。

另一个人执行的推送更新了原本指向提交 X 的分支，使其指向了提交 A。这是一个快进操作。

但如果你尝试推送，你将尝试用提交 B 更新（现在指向 A 的）分支。这*不是*快进。如果你强制执行了这一操作，由提交 A 引入的更改将会丢失，因为现在所有人都将从 B 开始构建。

默认情况下，该命令不允许进行非快进更新，以防止此类历史丢失。

如果你不想丢失你的工作（从 X 到 B 的历史）或另一个人的工作（从 X 到 A 的历史），你将先从仓库获取历史，创建一个包含双方修改更改的历史，然后将结果推回。

你可以执行`git pull`，解决潜在的冲突，并对结果执行`git push`。`git pull`会在提交 A 和 B 之间创建一个合并提交 C。

```
B---C
/
---X---A
```

使用生成的合并提交更新 A 将是快进的，你的推送将被接受。

或者，你可以通过`git pull --rebase`将你在 X 和 B 之间的更改变基到 A 之上，并将结果推回。变基将创建一个新的提交 D，它在 A 之上构建了 X 和 B 之间的更改。

```
B     D
/   /
---X---A
```

再次，使用此提交更新 A 将是快进的，你的推送将被接受。

当你尝试推送时还会遇到另一种非快进拒绝的常见情况，即使当你推送到一个没有其他人推送的仓库时也是可能的。当你自己推送了提交 A（见本节第一图），用`git commit --amend`产生提交 B，并尝试将其推出去，因为你忘记了已经推送过 A 了。在这种情况下，只有当你确定在此期间没有人获取过你早期的提交 A（并开始在其基础上构建）时，你才能运行`git push --force`来覆盖它。换句话说，`git push --force`是一个预留给确实想要丢失历史的情况的方法。

## 示例

`git push`
作用类似于`git push <remote>`，其中`<remote>`是当前分支的远程仓库（如果当前分支没有配置远程仓库，则为 origin）。

`git push origin`
在没有额外配置的情况下，如果当前分支与名称相同，则将当前分支推送到配置的上游（`remote.origin.merge`配置变量），否则报错且不推送。

当没有给出`<refspec>`时，此命令的默认行为可以通过设置远程的推送选项或`push.default`配置变量来配置。

例如，要默认仅推送当前分支到 origin，请使用`git config remote.origin.push HEAD`。任何有效的`<refspec>`（如下例所示）都可以配置为`git push origin`的默认值。

`git push origin :`
向 origin 推送匹配分支。关于匹配分支的描述参见上面的 OPTIONS `<refspec>`。

`git push origin master`
在源仓库中找到 master 的引用（最可能会找到`refs/heads/master`），并更新 origin 中相同的引用（例如`refs/heads/master`）。如果远程不存在 master，将创建它。

`git push origin HEAD`
将当前分支推送到远程同名分支的便捷方法。

`git push mothership master:satellite/master dev:satellite/dev`
使用匹配 master 的源引用（例如`refs/heads/master`）更新 mothership 仓库中匹配 satellite/master 的引用（可能是`refs/remotes/satellite/master`）；对 dev 和 satellite/dev 执行同样的操作。

这是为了通过相反方向运行`git push`来模拟在 mothership 上运行`git fetch`，以便整合在 satellite 上完成的工作。当你只能单向连接时通常是必要的（即 satellite 可以 ssh 到 mothership，但 mothership 无法连接 satellite，因为后者在防火墙后或未运行 sshd）。

在 satellite 机器运行此`git push`后，你将 ssh 进入 mothership 并在那里运行`git merge`，以完成在 mothership 上模拟拉取 satellite 更改的`git pull`。

`git push origin HEAD:master`
将当前分支推送到 origin 仓库中匹配 master 的引用。这种形式便于在不考虑本地名称的情况下推送当前分支。

`git push origin master:refs/heads/experimental`

通过复制当前的`master`分支在源仓库中创建`experimental`分支。这种形式仅在本地名称和远程名称不同时，才用于在远程仓库中创建新的分支或标签；否则，直接使用 ref 名称即可。

```
git push origin :experimental
```

在源仓库中找到与`experimental`的 ref（例如`refs/heads/experimental`）并将其删除。

```bash
git push origin +dev:master
```

使用`dev`分支更新源仓库的`master`分支，允许非快进更新。**这可能会在源仓库中留下未引用的悬空提交。**请考虑以下情况，此时无法进行快进更新：

```
o---o---o---A---B origin/master
         \
          X---Y---Z dev
```

上述命令将源仓库更改为：

```
A---B (unnamed branch)
     /
o---o---o---X---Y---Z master
```

提交`A`和`B`将不再属于任何符号名称的分支，因此将无法访问。因此，这些提交将通过在源仓库上执行`git gc`命令被移除。

***

# GIT-QUILTIMPORT

## NAME
`git-quiltimport` - 将 quilt 补丁集应用到当前分支

## SYNOPSIS
`git quiltimport` `--dry-run | -n] [--author <author>] [--patches <dir>]`

## DESCRIPTION
将 quilt 补丁集应用到当前的 Git 分支，保留该补丁集中存在的补丁边界、补丁顺序和补丁描述。

对于每个补丁，代码尝试从补丁描述中提取作者。如果失败，则回退到使用`--author`指定的作者。如果没有给出`--author`标志，则会显示补丁描述并要求用户交互式输入补丁的作者。

如果在补丁描述中未找到主题，则补丁名称将作为 Git 描述中的第 1 行主题。

## OPTIONS
- `-n, --dry-run`
遍历序列中的补丁，如果无法找到提交补丁所需的所有信息，则警告。在本文编写时，仅会对缺失的作者信息进行警告。

- `--author Author Name <Author Email>`
当补丁描述中找不到作者信息时使用的作者姓名和电子邮件地址。

- `--patches <dir>`
查找 quilt 补丁和 quilt 系列文件的目录。补丁目录的默认值为`patches`或环境变量`$QUILT_PATCHES`的值。

***

# GIT-READ-TREE

## NAME
`git-read-tree` - 将树信息读入索引

## SYNOPSIS
`git read-tree` `[[-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>] [-u [--exclude-per-directory=<gitignore>] | -i]] [--index-output=<file>] [--no-sparse-checkout] (--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])]]`

## DESCRIPTION
将由`<tree-ish>`提供的树信息读入索引，但实际上不会**更新**它"缓存"的任何文件。(见：(1))

可选地，可以使用`-m`标志将树合并到索引中，执行快进（即二路）合并或三路合并。当与`-m`使用时，`-u`标志会导致它同时根据合并结果更新工作区中的文件。

简单易合并由`git read-tree`自身完成。当`git read-tree`返回时，只有冲突路径会处于未合并状态。

## OPTIONS
- `-m`
执行合并而不仅仅是读取。如果索引文件存在未合并的条目，命令将拒绝运行，表明你尚未完成之前的合并。

- `--reset`
与`-m`相同，区别是丢弃未合并的条目而不是报错。

- `-u`
成功合并后，根据合并结果更新工作区中的文件。

- `-i`
通常，合并需要索引文件以及工作区中的文件与当前头提交保持同步，以防丢失本地更改。此标志禁用了对工作区的检查，用于将与当前工作区状态没有直接关联的树合并到临时索引文件中。

- `-n, --dry-run`
检查命令是否会报错，而不会真实更新索引或工作区中的文件。

- `-v`
显示检出文件的进度。

- `--trivial`
限制`git read-tree`的三路合并，使其仅在不需要文件级合并时发生，而不是为简单情况解决合并问题并在索引中留存未解决的冲突文件。

- `--aggressive`
通常，`git read-tree`的三路合并会解决非常简单情况的合并，并在索引中留存其他未解决的情况，以便 porcelain 接口可以实现不同的合并策略。此标志使命令在内部解决更多情况：
- 当一侧删除路径而另一侧保持该路径未修改时。解决方法是移除该路径。
- 当双方都删除路径时。解决方法是移除该路径。
- 当双方相同地添加路径时。解决方法是添加该路径。

- `--prefix=<prefix>/`
保留当前索引内容，并在`<prefix>`目录下读取命名树-ish 的内容。命令将拒绝覆盖原始索引文件中已存在的条目。注意`<prefix>/`值必须以斜杠结尾。

- `--exclude-per-directory=<gitignore>`
在使用`-u`和`-m`选项运行命令时，合并结果可能需要覆盖当前分支中未跟踪的路径。命令通常拒绝继续合并以避免丢失此类路径。但这种安全机制有时会干扰。例如，经常发生另一个分支添加了一个在你分支中曾是生成的文件，当你运行`make`之后但在运行`make clean`删除生成文件之前尝试切换到该分支时，安全机制就会触发。此选项告诉命令读取按目录排除的文件（通常为`*.gitignore`），并允许此类未跟踪但显式忽略的文件被覆盖。

- `--index-output=<file>`
不将结果写入`$GIT_INDEX_FILE`，而是将生成的索引写入命名文件。在命令运行期间，原始索引文件将使用相同的机制锁定。该文件必须允许从在常规索引文件旁边创建的临时文件进行拷贝；通常这意味着它需要与索引文件本身位于同一个文件系统中，并且你对索引文件和索引输出文件所在的目录具有写入权限。

- `--no-sparse-checkout`
即使`core.sparseCheckout`为 true 也禁用稀疏检出支持。

- `--empty`
不将树对象读入索引，直接清空。

- `<tree-ish#>`
要读取/合并的树对象的 ID。

## MERGING
如果指定了`-m`，`git read-tree`可以执行 3 种合并：如果只给 1 个树，则执行单树合并；2 个树执行快进合并；提供 3 个树则执行三路合并。

### 单树合并
如果只指定了 1 个树，`git read-tree`的操作就像用户没有指定`-m`，但如果原始索引中存在给定路径的条目，且该路径的内容与读入的树匹配，则使用索引中的 stat 信息。（换句话说，索引的`stat()`优先于合并的树）。

这意味着如果你执行了`git read-tree -m <newtree>`然后执行`git checkout-index -f -u -a`，`git checkout-index`只会检出真正变化的内容。

这用于避免在运行`git read-tree`后运行`git diff-files`时产生不必要的误报。

### 双树合并
通常这被调用为`git read-tree -m $H $M`，其中`$H`是当前仓库的头提交，`$M`是外部树的头，该树仅领先于`$H`（即我们处于快进状态）。

当指定两个树时，用户正在告诉`git read-tree`：
1. 当前索引和工作区派生自`$H`，但用户自`$H`之后在其中可能有本地更改。
2. 用户想要快进到`$M`。

在这种情况下，`git read-tree -m $H $M`命令确保了不会因为这次"合并"的结果而丢失任何本地更改。以下是"进位"规则，其中"I"表示索引（index），"clean"意味着索引和工作树一致，"exists"/"nothing"指的是指定提交中是否存在该路径：

```
I    H    M    Result
-------------------------------------------------------
0    nothing    nothing    nothing    (does not happen)
1    nothing    nothing    exists    use M
2    nothing    exists    nothing    remove path from index
3    nothing    exists    exists, use M if "initial checkout", H == M
     keep index otherwise, exists, fail H != M

clean    I==H    I==M
------------------
4    yes    N/A    N/A    nothing    nothing    keep index
5    no    N/A    N/A    nothing    nothing    keep index

6    yes    N/A    yes    nothing    exists    keep index
7    no    N/A    yes    nothing    exists    keep index
8    yes    N/A    no    nothing    exists    fail
9    no    N/A    no    nothing    exists    fail

10    yes    yes    N/A    exists    nothing    remove path from index
11    no    yes    N/A    exists    nothing    fail
12    yes    no    N/A    exists    nothing    fail
13    no    no    N/A    exists    nothing    fail

clean    (H==M)
------
14    yes    exists    exists    keep index
15    no    exists    exists    keep index

clean    I==H    I==M    (H!=M)
------------------
16    yes    no    no    exists    exists    fail
17    no    no    no    exists    exists    fail
18    yes    no    yes    exists    exists    keep index
```



# 19 no no yes exists exists keep index
# 20 yes yes no exists exists use M
# 21 no yes no exists exists fail

在所有“保留索引”（keep index）的情况下，索引条目保持与原始索引文件一致。如果该条目未更新，`git read-tree` 在`-u`标志下操作时会保持工作树中的副本完好无。

这种形式的`git read-tree`成功返回时，你可以运行`git diff-index --cached $M`来查看你所做的“本地更改”中有哪些被带入了。请注意，这并不等同于在这种双树合并之前`git diff-index --cached $H`会产生的结果。这是由于第18和第19情况导致的——如果你已经有了`$M`中的更改（例如，可能你通过邮件补丁的形式获取了它），`git diff-index --cached $H`会在合并前告知你该更改，但在双树合并后的`git diff-index --cached $M`输出中不会显示它。

情况3稍微有点复杂，需要解释。该规则的逻辑结果应该是：如果用户暂存了删除路径的操作并切换到新分支，则删除该路径。然而这将阻止初始检出（initial checkout）的发生，因此规则被修改为：仅当索引内容为空时才使用`M`（新树）。否则，只要`$H`和`$M`相同，路径的删除就会保留。

## 三路合并 (3-Way Merge)

每个“索引”条目都有两个位的“阶段”（stage）状态。`stage 0`是正常状态，也是你在任何正常使用下唯一会看到的状态。

然而，当你对三个树执行`git read-tree`时，“阶段”从1开始。

这意味着你可以执行：

```
$ git read-tree -m <tree1> <tree2> <tree3>
```

并且你会得到一个索引，其中所有的`<tree1>`条目处于"stage1"，所有的`<tree2>`条目处于"stage2"，而所有的`<tree3>`条目处于"stage3"。在将另一个分支合并到当前分支时，我们使用共同祖先树作为`<tree1>`，当前分支头作为`<tree2>`，另一个分支头作为`<tree3>`。

此外，`git read-tree`具有特殊情况逻辑：如果你看到一个文件在以下状态下各方面都匹配，它将“折叠”回“stage0”：

- `stage 2`和`stage 3`相同；取其中任一（这没有区别——在我们的分支`stage 2`中做的工作与他们的分支`stage 3`中做的是一样的）
- `stage 1`和`stage 2`相同且`stage 3`不同；取`stage 3`（我们的分支`stage 2`自从`stage 1`的祖先以来没有做任何操作，而他们的分支`stage 3`进行了处理）
- `stage 1`和`stage 3`相同且`stage 2`不同；取`stage 2`（我们做了操作，而他们什么都没做）

`git write-tree`命令拒绝写入无意义的树，如果它看到任何不是`stage 0`的条目，它会对未合并的条目报错。

好了，这听起来像是一组完全毫无意义的规则，但它实际上正是为了进行快速合并所需要的。不同的阶段`1`、`2`和`3`分别代表“结果树”（`stage 0`，即“已合并”）、原始树（`stage 1`，即“orig”）以及你正尝试合并的两个树（分别为`stage 2`和`stage 3`）。

当你从已经填充的索引文件开始三路合并时，阶段`1`、`2`和`3`的顺序（即三个`<tree-ish>`命令行参数的顺序）是非常重要的。以下是算法原理的概述：

- 如果文件在三个树中的格式完全相同，`git read-tree`将自动将其折叠为“已合并”状态。
- 在三个树中存在*任何*差异的文件将作为独立的条目保留在索引中。如何移除非0阶段并插入合并后的版本，取决于“瓷器策略”（porcelain policy）。
- 索引文件保存和恢复时带有所有这些信息，因此你可以增量地合并，但只要它还存在`1/2/3`阶段的条目（即“未合并条目”），你就无法写入结果。因此，合并算法变得非常简单：
- 你按顺序遍历索引，忽略所有的`stage 0`条目，因为它们已经处理过了。
- 如果你发现`stage1`但没有匹配的`stage2`或`stage3`，你知道它已从两个树中都被删除了（它只存在于原始树中），并删除该条目。
- 如果你发现匹配的`stage2`和`stage3`树，移除其中一个，并将另一个转换为`stage0`条目。如果存在匹配的`stage1`条目，也将其删除……所有常见的简单规则……

你通常会使用`git merge-index`配合提供的`git merge-one-file`来完成最后一步。该脚本会在合并每个路径以及成功合并结束后更新工作树中的文件。

当你从已经填充的索引文件开始三路合并时，假设它代表了你工作树中文件的状态，你甚至可能拥有在索引文件中未记录更改的文件。进一步假设该状态是“衍生”自`stage 2`树的。如果在原始索引文件中发现与`stage 2`不匹配的条目，三路合并将拒绝运行。

这样做是为了防止你丢失进行中的更改，并防止将随机更改混杂在无关的合并提交中。为了说明，假设你从仓库中最后一次提交的状态开始：

```
$ JC=`git rev-parse --verify "HEAD⁰"` $ git checkout-index -f -u -a $JC
```

你进行了随机编辑，而没有运行`git update-index`。然后你注意到自从从那里拉取以来，你的“上游”树端已经向前了：

```
$ git fetch linus $ LT=`git rev-parse FETCH_HEAD`
```

你的工作树仍然基于你的`HEAD`（`$JC`），但你之后又有一些编辑。三路合并确保你没有自`$JC`以来添加或修改索引条目，如果没有，它就会执行正确的操作。因此通过以下序列：

```
$ git read-tree -m -u `git merge-base $JC $LT` $JC $LT $ git merge-index git-merge-one-file -a $ echo "Merge with Linus" | \ git commit-tree `git write-tree` -p $JC -p $LT
```

你将提交的是`$JC`和`$LT`之间的纯合并，不包含你进行中的更改，并且你的工作树将更新为合并的结果。

但然而，如果你在工作树中拥有会被这次合并覆盖的本地更改，`git read-tree`将拒绝运行以防止你的更改丢失。

换句话说，无需担心仅存在于工作树中的内容。当你对项目中未参与合并的部分有本地更改时，你的更改不会与合并冲突，并会被完好地保留。当它们**确实**发生冲突时，合并甚至不会开始（`git read-tree`会大报错并失败，且不会修改任何内容）。在这种情况下，你只需继续你正在的操作，等你的工作树准备就绪（即你完成了正在进行的工作），再次尝试合并。

## 稀疏检出 (SPARSE CHECKOUT)

“稀疏检出”允许稀疏地填充工作目录。它使用 skip-worktree 标记（见 (1)）来告诉 Git 工作目录中的某个文件是否值得查看。

`git read-tree`和其他基于合并的命令（`git merge`、`git checkout`...）可以帮助维护 skip-worktree 位图和工作目录的更新。`$GIT_DIR/info/sparse-checkout`用于定义 skip-worktree 引用位图。当`git read-tree`需要更新工作目录时，它会根据该文件重置索引中的 skip-worktree 标记，该文件的语法与`.gitignore`文件相同。如果条目匹配此文件中的模式，则该条目不会设置 skip-worktree。否则，将设置 skip-worktree。

然后它会将新的 skip-worktree 值与上一个值进行比较。如果 skip-worktree 从设置为变为未设置，它将把对应文件加回来。如果从未设置变为设置，则该文件将被删除。

虽然`$GIT_DIR/info/sparse-checkout`通常用于指定哪些文件在内，但你也可以使用取反模式指定哪些文件*不在*在内。例如，要移除不需要的文件：

```
/* !unwanted
```

另一个棘手的问题是在当你不再需要稀疏检出时完全重新填充工作目录。你不能简单地禁用“稀疏检出”，因为 skip-worktree 标记仍在索引中，且你的工作目录仍然是稀疏填充的。你应该如下使用`$GIT_DIR/info/sparse-checkout`文件的内容重新填充工作目录：

```
/*
```

然后你就可以禁用稀疏检出了。`git read-tree`和类似命令中的稀疏检出支持默认是禁用。你需要开启`core.sparseCheckout`才能获得稀疏检出支持。

## 参见 (SEE ALSO)

(1); (1); (5)

# GIT-REBASE

## 名称 (NAME)

`git-rebase` - 将本地提交向前移植到更新的上游头部

## 概要 (SYNOPSIS)

`git rebase [-i | --interactive] [options] [--exec <cmd>] [--onto <newbase>] [<upstream> [<branch>]]`
`git rebase [-i | --interactive] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]`
`git rebase --continue | --skip | --abort | --edit-todo`

## 说明 (DESCRIPTION)

如果指定了`<branch>`，`git rebase`在执行其他操作之前将执行自动的`git checkout <branch>`。如果未指定`<upstream>`，将使用在`branch.<name>.remote`和`branch.<name>.merge`选项中配置的上游（详情见 (1)），并假设启用了`--fork-point`选项。如果你当前不在任何分支上，或者当前分支没有配置上游，则 rebase 将终止。

由当前分支提交产生但不在`<upstream>`中的所有更改将被保存到一个临时区域。这与`git log <upstream>..HEAD`显示的提交集相同；或者如果激活了`--fork-point`，则与`git log 'fork_point'..HEAD`显示（见下文 --fork-point 的说明）；或者如果指定了`--root`选项，则与`git log HEAD`显示。

当前分支被重置为`<upstream>`，或者如果提供了`--onto`选项则为`<newbase>`。这与`git reset --hard <upstream>`（或`<newbase>`）的效果完全相同。`ORIG_HEAD`被指向重置之前的分支顶端。

之前保存到临时区域的提交将按顺序逐个重新应用当前分支。注意，`HEAD`中任何与`HEAD..<upstream>`中提交相同文本更改的提交将被跳过（即上游已接受具有不同提交信息或时间戳的提交将被跳过）。

合并失败可能会导致此过程无法完全自动。你必须解决任何此类合并失败并运行`git rebase --continue`。另一个选项是使用`git rebase --skip`跳过导致合并失败的提交。要检出原始`<branch>`并移除`.git/rebase-apply`工作文件，请使用命令`git rebase --abort`。

假设存在以下历史且当前分支为 "topic"：

```
A---B---C topic / D---E---F---G master
```

从此点开始，以下任一命令的结果：

```
git rebase master git rebase master topic
```

结果将是：

```
A'--B'--C' topic / D---E---F---G master
```

**注意：** 后者形式只是`git checkout topic`之后接`git rebase master`的简写。当 rebase 退出时，topic 将保持为检出的分支。

如果上游分支已经包含了你所做的更改（例如，因为你发送的补丁已应用到上游），则该提交将被跳过。例如，在以下历史上运行`git rebase master`（其中 A' 和 A 引入了相同的更改，但具有不同的提交者信息）：

```
A---B---C topic / D---E---A'---F master
```

将导致：

```
B'---C' topic / D---E---A'---F master
```

这里是如何使用`rebase --onto`将基于一个分支的 topic 分支移植到另一个分支，假装你是从另一个分支分叉出 topic 分支。

首先，假设你的`topic`基于分支`next`。例如，在`topic`中开发的功能依赖于`next`中的某些功能。

```
o---o---o---o---o master \ o---o---o---o---o next \ o---o---o---o topic
```

我们想让`topic`从`master`分支分叉；例如，因为`topic`依赖的功能已合并到更稳定的`master`分支中。我们希望我们的树看起来像这样：

```
o---o---o---o---o master | \ | o'--o'--o' topic \ o---o---o---o---o next
```

我们可以使用以下命令实现这一点：

```
git rebase --onto master next topic
```

`--onto`选项的另一个例子是 rebase 分支的一部分。如果我们有以下情况：

```
H---I---J topicB / E---F---G topicA / A---B---C---D master
```

那么命令

```
git rebase --onto master topicA topicB
```

将导致：

```
H'--I'--J' topicB / | E---F---G topicA |/ A---B---C---D master
```

这在`topicB`不依赖于`topicA`时非常有用。

也可以通过 rebase 移除一个范围的提交。如果我们有以下情况：

```
E---F---G---H---I---J topicA
```

那么命令

```
git rebase --onto topicA~5 topicA~3 topicA
```

将导致提交 F 和 G 的移除：

```
E---H'---I'---J' topicA
```

这如果 F 和 G 在某些方面存在缺陷，或不应成为`topicA`的部分，则很有用。注意，`--onto`的参数和`<upstream>`参数可以是任何有效的 commit-ish。

发生冲突时，`git rebase`将停在第一个问题的提交上，并在树中留下冲突标记。你可以使用`git diff`定位标记（<<<<<<）并进行编辑以解决冲突。对于你编辑的每个文件，你都需要告诉 Git 冲突已解决，通常通过这样做：

```
git add <filename>
```

在手动解决冲突并使用所需的解析更新索引后，你可以继续 rebasing 过程：

```
git rebase --continue
```

或者，你可以通过以下命令撤销`git rebase`：

```
git rebase --abort
```




## 配置（CONFIGURATION）

### `rebase.stat`

是否显示自上次 `rebase` 以来上游更改的 diffstat。默认默认为 `False`。

### `rebase.autoSquash`

如果设置为 `true`，则默认启用 `--autosquash` 选项。

### `rebase.autoStash`

如果设置为 `true`，则默认启用 `--autostash` 选项。

## 选项（OPTIONS）

### `--onto <newbase>`

创建新提交的起点。如果没有指定 `--onto` 选项，则起点为 `<upstream>`。它可以是任何有效的提交，而不仅仅是现有的分支名。

作为一个特殊情况，如果 `A` 和 `B` 恰好有一个合并基，你可以使用 `"A...B"` 作为 `A` 和 `B` 合并基的快捷方式。你可以最多省略 `A` 和 `B` 中的一个，在这种情况下它默认为 `HEAD`。

### `<upstream>`

用于比较的上游分支。可以是任何有效的提交，而不仅仅是现有的分支名。默认是当前分支配置的上游。

### `<branch>`

工作分支；默认为 `HEAD`。

### `--continue`

在解决合并冲突后重新启动变基过程。

### `--abort`

中止变基操作并将 `HEAD` 重置为原始分支。如果在启动变基操作时提供了 `<branch>`，则 `HEAD` 将被重置为 `<branch>`。否则，`HEAD` 将重置为变基操作开始时的位置。

### `--keep-empty`

在结果中保留与其父提交相比没有任何更改的提交。

### `--skip`

跳过当前补丁并重新启动变基过程。

### `--edit-todo`

在交互式变基期间编辑待办列表。

### `-m, --merge`

使用合并策略进行变基。当使用递归（默认）合并策略时，这允许变基感知上游侧的重命名。

请注意，变基合并通过将工作分支中的每个提交重新应用到 `<upstream>` 分支之上来。正因如此，当发生合并冲突时，报告为 `ours`（我们的）的一侧是到目前变基序列（从 `<upstream>` 开始），而 `theirs`（他们的）是工作分支。换句话说，双方交换了。

### `-s <strategy>, --strategy=<strategy>`

使用指定的合并策略。如果没有 `-s` 选项，则将使用 `git merge-recursive`。这意味着使用了 `--merge`。

由于 `git rebase` 使用给定的策略将工作分支的每个提交重新应用到 `<upstream>` 分支之上，因此使用 `ours` 策略将简单丢弃 `<branch>` 中的所有补丁，这几乎没有意义。

### `-X <strategy-option>, --strategy-option=<strategy-option>`

将 `<strategy-option>` 传递给合并策略。这意味着使用了 `--merge`，并且如果没有指定策略，则使用 `-s recursive`。请注意上述针对 `-m` 选项的 `ours` 和 `theirs` 的反转。

### `-S[<keyid>], --gpg-sign[=<keyid>]`

对提交进行 GPG 签名。

### `-q, --quiet`

安静模式。意味着 `--no-stat`。

### `-v, --verbose`

详细模式。意味着 `--stat`。

### `--stat`

显示自上次变基以来上游更改的差异统计（diffstat）。差异统计由配置选项 `rebase.stat` 控制。

### `-n, --no-stat`

在变基过程中不显示差异统计。

### `--no-verify`

此选项跳过变基前钩子（pre-rebase hook）。另见 (5)__。

### `--verify`

允许运行变基前钩子，这是默认设置。此选项可用于覆盖 `--no-verify`。另见 (5)__。

### `-C<n>`

确保每次更改前后至少有 `<n>` 行周围上下文相匹配。如果周围上下文行较少，则它们必须全部匹配。默认情况下不忽略任何上下文。

### `-f, --force-rebase`

即使当前分支是最新的，且不带 `--force` 的命令直接返回而不执行任何操作，也强制变基。

在撤销主题分支合并后，你可能会发现此操作（或配合交互式变基使用 `--no-ff`）很有帮助，因为此选项会使用新的提交重建主题分支，以便能够重新合并，而无需“撤销撤销的操作”（详见 `revert-a-faulty-merge How-To`m[][1]）。

### `--fork-point, --no-fork-point`

在计算哪些提交是由 `<branch>` 引入的时，使用 reflog 在 `<upstream>` 和 `<branch>` 之间找到更佳的共同祖先。

当 `--fork-point` 激活时，将使用 `fork_point` 而不是 `<upstream>` 来计算变基的提交集，其中 `fork_point` 是 `git merge-base --fork-point <upstream> <branch>` 命令的结果（见 (1)__）。如果 `fork_point` 最终为空，将使用 `<upstream>` 作为备选方案。

如果在命令行上给了 `<upstream>` 或 `--root`，则默认使用 `--no-fork-point`，否则默认使用 `--fork-point`。

### `--ignore-whitespace, --whitespace=<option>`

这些标志被传递给应用补丁的 `git apply` 程序（见 (1)__）。与 `--interactive` 选项兼容。

### `--committer-date-is-author-date, --ignore-date`

这些标志被传递给 `git am` 以轻松更改变基提交的日期（见 (1)__）。与 `--interactive` 选项兼容。

### `-i, --interactive`

列出即将变基的提交列表。让用户在变基前编辑该列表。此模式也可用于拆分提交（见下文 SPLITTING COMMITS）。

### `-p, --preserve-merges`

重新创建合并提交，而不是通过重放合并提交引入的提交来扁平化历史。合并冲突的解决或对合并提交的手动修改不会被保留。

这在内部使用了 `--interactive` 机制，但显式与 `--interactive` 选项结合使用通常不是好主意，除非你清楚自己在做什么（见下文 BUGS）。

### `-x <cmd>, --exec <cmd>`

在最终历史中创建提交的每行之后添加 `"exec <cmd>"`。`<cmd>` 将解释为一个或多个 shell 命令。

此选项只能与 `--interactive` 选项配合使用（见下文 INTERACTIVE MODE）。

你可以通过在单个 `--exec` 实例中使用多个命令来执行多个命令：

```bash
git rebase -i --exec "cmd1 && cmd2 && ..."
```

或者通过提供多个 `--exec`：

```bash
git rebase -i --exec "cmd1" --exec "cmd2" --exec ...
```

如果使用了 `--autosquash`，中间提交将不会附加 `"exec"` 行，这些行只会出现在每个 squash/fixup 序列的末尾。

### `--root`

变基从 `<branch>` 可达的所有提交，而不是通过 `<upstream>` 限制它们。这允许你变基分支上的根提交。当与 `--onto` 使用时，它将跳过已在 `<newbase>` 中的更改（而不是 `<upstream>`），而在没有使用 `--onto` 时它将作用于每一个更改。当同时与 `--onto` 和 `--preserve-merges` 使用时，所有根提交将被重写为以 `<newbase>` 为父节点。

### `--autosquash, --no-autosquash`

当提交日志以 `"squash! ..."`（或 `"fixup! ..."`）开头，且有一个提交标题以相同的开头时，自动修改 `rebase -i` 的待办列表，使标记为压缩的提交紧跟在要修改提交之后，并将移动提交的操作从 `pick` 改为 `squash`（或 `fixup`）。忽略后续的 `"fixup! "` 或 `"squash! "`，以防你通过 `git commit --fixup/--squash` 引用了之前的修复/压缩。

此选项仅在使用 `--interactive` 选项时有效。

如果通过配置变量 `rebase.autoSquash` 默认启用 `--autosquash` 选项，可以使用此选项覆盖并禁用该设置。

### `--[no-]autostash`

操作开始前自动创建一个临时 stash，操作结束后应用它。这意味着你可以在脏工作树上运行变基。但请谨慎使用：成功变基后最后的 stash 应用可能会导致非平凡的冲突。

### `--no-ff`

在交互式模式下，应用 `pick` 所有变基后的提交，而不是对未更改的部分进行快进。这确保了变基分支的整个历史都由新提交组成。

在非交互式模式下，它是 `--force-rebase` 的同义词。

合并机制（`git merge` 和 `git pull` 命令）允许通过 `-s` 选项选择后端的 `merge strategies`。某些策略还可以接受自己的选项，这些选项可以通过向 `git merge` 和/或 `git pull` 提供 `-X<option>` 参数来传递。

## `resolve`

该策略只能使用 3 路合并算法解析两个头节点（即当前分支和从某处拉取的另一个分支）。它会尝试仔细检测交叉合并（criss-cross merge）歧义，通常被认为是安全且快速的。

## `recursive`

该策略只能使用 3 路合并算法解析两个头节点。当存在多个可用于 3 路合并的公共祖先时，它会创建一个公共祖先的合并树，并将其作为 3 路合并的参考树。根据对 Linux 2.6 内核开发历史中实际合并提交的测试，这种方法报告可以减少合并冲突，且不会导致错误合并（mismerges）。此外，它还可以检测并处理涉及重命名的合并。这是拉取或合并单个分支时默认的合并策略。

`recursive` 策略可以接受以下选项：

### `ours`

此选项强制冲突的代码块（hunks）通过倾向 `our` 版本来自动解决。来自另一个树的与我们侧不冲突的更改将反映在合并结果中。对于二进制文件，整个内容将取自我们侧。

这不应与 `ours` 合并策略混淆，后者完全不看另一个树包含的内容。它会丢弃另一个树所做的所有操作，声明 `our` 历史包含了其中发生的所有内容。

### `theirs`

这是 `ours` 的相反选项。

### `patience`

使用此选项时，`merge-recursive` 会花费额外的时间来避免有时因无关紧要的匹配行（例如不同函数的括号）而导致的错误合并。当要合并的分支差异巨大时，请使用此选项。另见 `(1)--patience`。

### `diff-algorithm=[patience|minimal|histogram|myers]`

告诉 `merge-recursive` 使用不同的差异算法，这有助于避免因无关紧要的匹配行（如不同函数的括号）而导致的错误合并。另见 `(1)--diff-algorithm`。

### `ignore-space-change, ignore-all-space, ignore-space-at-eol`

为了进行三路合并，将带有指定类型空格更改的行视为未更改。与行其他更改混合的空格更改不会被忽略。另见 `(1)-b`、`-w` 和 `--ignore-space-at-eol`。

- 如果 `their` 版本仅对某行引入了空格更改，则使用 `our` 版本；
- 如果 `our` 版本引入了空格更改但 `their` 版本包含实质性更改，则使用 `their` 版本；
- 否则，按通常方式合并。

### `renormalize`

在解析三路合并时，它会对文件的三个阶段都运行虚拟的检出（check-out）和检入（check-in）。此选项用于合并具有不同清理过滤器（clean filters）或行尾归一化（eol normalization）规则的分支。详情请见 (5) 中的“合并具有不同检入/检出属性的分支”。

### `no-renormalize`

禁用 `renormalize` 选项。这会覆盖 `merge.renormalize` 配置变量。

### `rename-threshold=<n>`

控制用于重命名检测的相似性阈值。另见 `(1)-M`。

### `subtree[=<path>]`

此选项是 `subtree` 策略的一种更高级的形式，该策略在合并时对两个树必须如何移动以彼此匹配做出猜测。相反，指定的路径将被添加前缀（或从开头剥离），以使两个树的形状相匹配。

### `octopus`

该策略解析多于两个头节点的情况，但拒绝执行需要手动解决的复杂合并。它主要用于将多个主题分支头组合在一起。这是拉取或合并多个分支时的默认合并策略。

### `ours`

该策略解析任意数量的头节点，但合并后的树始终是当前分支头的树，实际上忽略了所有其他分支的所有更改。它用于取代侧分支的旧开发历史。注意，这与 `recursive` 合并策略的 `-Xours` 选项不同。

### `subtree`

这是改进的 `recursive` 策略。在合并树 A 和 B 时，如果 B 对应于 A 的子树，则先调整 B 以匹配 A 的树结构，而不是在相同层级读取树。这种调整也会对公共祖先树进行。

对于使用 3 路合并的策略（包括默认的 `recursive`），如果对两个分支上都做了更改，但随后在其中一个分支上撤销了该更改，那么该更改将出现在合并结果中；一些人发现这种行为令人困惑。这是因为在执行合并时只考虑头节点和合并基（merge base），而不考虑单个提交。因此，合并算法将撤销的更改视为没有任何更改，并代之以更改的版本。

## NOTES

你应该理解在你们共享的仓库上使用 `git rebase` 的影响。另见下文 RECOVERING FROM UPSTREAM REBASE。

运行 `git-rebase` 命令时，如果存在，它将首先执行“pre-rebase”钩子（hook）。你可以使用此钩子进行健全性检查，并在不合适时拒绝 rebase。请参考模板 pre-rebase 钩子脚本示例。

完成后，`<branch>` 将成为当前分支。

## INTERACTIVE MODE

交互式 `rebase` 意味着你有机会编辑被 `rebase` 的提交。你可以重新排序提交，也可以删除它们（剔除糟糕或其他不需要的补丁）。

交互式模式适用于这种类型的工作流：

1. 有了一个棒的主意
2. 对代码进行黑客操作
3. 准备一系列用于提交的提交
4. 提交

其中第 2 点包含若干个实例：

### a) 常规使用

1. 完成某些值得提交的内容
2. 提交

### b) 独立的修复（fixup）

1. 发现某些东西不起作用
2. 修复它
3. 提交

有时 b.2 中修复的内容无法合并到它所修复的那个并不完美的提交中，因为该提交深埋在补丁序列中。这正是交互式 `rebase` 的用处：在进行了大量的“a”和“b”之后，通过重新排列和编辑提交，并将多个提交合并（squash）为一个，来使用它。

从你想要原样保留的最后一个提交启动它：

```bash
git rebase -i <after-this-commit>
```

将启动一个编辑器，显示你当前分支中所有在给定提交之后的提交（忽略合并提交）。你可以根据随心所欲地重新排列此列表中的提交，也可以删除它们。该列表看起来大致如下：

```text
pick deadbee The oneline of this commit
pick fa1afe1 The oneline of the next commit
...
```

单行描述纯粹供你阅读；`git rebase` 不会查看它们，而是查看提交名称（此示例中的 `deadbee` 和 `fa1afe1`），因此不要删除或编辑名称。

通过将命令 `pick` 替换为命令 `edit`，你可以告诉 `git rebase` 在应用该提交后停止，这样你就可以编辑文件和/或提交信息、修正提交并继续 `rebase`。

如果你只想编辑某个提交的提交消息，请将命令 `pick` 替换为命令 `reword`。

如果你想将两个或多个提交合并为一个，请将第二个及后续提交的命令 `pick` 替换为 `squash` 或 `fixup`。如果这些提交有不同的作者，合并后的提交将归属于第一个提交的作者。合并后提交的建议提交消息是第一个提交的提交消息与带有 `squash` 命令的提交的提交消息的拼接，但会省略带有 `fixup` 命令的提交的提交消息。

当 `pick` 被替换为 `edit` 或命令因合并错误导致执行失败时，`git rebase` 将停止。当你完成编辑和/或解决冲突后，可以运行 `git rebase --continue` 继续。

例如，如果你想重新排序最后的 5 个提交，使得原来的 `HEAD~4` 变成新的 `HEAD`。为了实现这一点，你可以这样调用 `git rebase`：

```bash
$ git rebase -i HEAD~5
```

并将第一个补丁（patch）移动到列表的末尾。

如果你有如下历史，你可能想要保留合并提交：

```text
      X
     / \
A---M---B
 \ /
  o---O---P---Q
```

假设你想将从 `A` 开始的侧边分支 `rebase` 到 `Q`。确保当前的 `HEAD` 是 `B`，然后调用：

```bash
$ git rebase -i -p --onto Q O
```

重新排序和编辑提交通常会创建未经过测试的中间步骤。你可能希望通过运行测试来检查你的历史记录编辑是否破坏了某些内容，或者至少使用 `exec` 命令（快捷方式为 `x`）在历史的中间点进行重新编译。你可以通过创建一个像下面这样的待办列表（todo list）来执行操作：




# Git Rebase 交互式命令示例

`pick deadbee` 实现功能 XXX，`fixup f1a5c00` 修复功能 XXX，`exec make`，`pick c0ffeee` 下一个提交的单行说明，`edit deadbab` 之后提交的单行说明，`exec cd subdir; make test` ...

```
交互式 rebase 会在命令失败（即以非 0 状态退出）时停止，以便你有机会修复问题。你可以使用 `git rebase --continue` 继续。
```

`exec` 命令在 shell 中启动命令（使用 `$SHELL` 指定的 shell，或者如果 `$SHELL` 未设置则使用默认 shell），因此你可以使用 shell 功能（如 `"cd"`、`>`, `;` ...）。该命令从工作树的根目录运行。

```
$ git rebase -i --exec "make test"
```

此命令允许你检查中间提交是可编译的。待办列表会变成如下：

```
pick 5928aea one
exec make test
pick 04d0fda two
exec make test
pick ba46169 three
exec make test
pick f4593f9 four
exec make test
```

## 分拆提交 (SPLITTING COMMITS)

在交互模式下，你可以用 `"edit"` 动作标记提交。然而，这并不意味着 `git rebase` 期望该编辑的结果恰好是一个提交。事实上，你可以撤销该提交，也可以添加其他提交。这可以用于将一个提交拆分为两个：

- 使用 `git rebase -i <commit>^` 启动交互式 rebase，其中 `<commit>` 是你想要拆分的提交。事实上，任何提交范围都可以，只要它包含该提交即可。
- 用 `"edit"` 动作标记你想要拆分的提交。

当要编辑该提交时，执行 `git reset HEAD^`。效果是 `HEAD` 回退一个版本，索引（index）随之移动。然而，工作树保持不变。

现在，将你想放入第一个提交的更改添加到索引中。你可以使用 `git add`（可能是交互式地）或 `git gui`（或两者都用）来完成此操作。

使用任何合适的提交信息提交当前的索引。

重复最后两个步骤，直到你的工作树变干净为止。

使用 `git rebase --continue` 继续 rebase。

如果你不能完全确定中间版本是一致的（它们可以编译、通过测试套件等），你应该在每次提交、测试后使用 `git stash` 暂存尚未提交的更改，并在必要时修复提交。

## 从上游 rebase 中恢复 (RECOVERING FROM UPSTREAM REBASE)

对他人在其基础上工作的分支进行 rebase 是一个坏主意：其下游的任何人都被强制手动修复他们的历史记录。本节解释了如何从下游的角度进行修复。然而，真正的修复方法是从根本避免对上游进行 rebase。

为了说明，假设你处于这样的情况：有人开发了一个 `subsystem` 分支，而你正在开发一个依赖该 `subsystem` 的 `topic`。你可能会得到如下历史：

```
o---o---o---o---o---o---o---o---o master
     \
      o---o---o---o---o subsystem
           \
            *---*---* topic
```

如果 `subsystem` 对 `master` 进行 rebase，会发生以下情况：

```
o---o---o---o---o---o---o---o master
     \       \
      o---o---o---o---o o'--o'--o'--o'--o' subsystem
           \
            *---*---* topic
```

如果你现在照常继续开发，并最终将 `topic` 合并到 `subsystem`，来自 `subsystem` 的提交将永远重复：

```
o---o---o---o---o---o---o---o master
     \       \
      o---o---o---o---o o'--o'--o'--o'--o'--M subsystem
           \            /
            *---*---*-..........-*--* topic
```

这种重复通常是不受欢迎的，因为它们会弄乱历史记录，使其更难追踪。为了清理，你需要将 `topic` 上的提交移植到新的 `subsystem` 顶端，即 rebase `topic`。这会产生连锁反应：`topic` 下游的任何人都被迫也进行 rebase，以此类推！

有两种修复方法，将在接下来的小节中讨论：

**简单情况：** 更改完全相同。如果 `subsystem` 的 rebase 是简单的 rebase 且没有冲突，就会发生这种情况。

**困难情况：** 更改并不相同。如果 `subsystem` 的 rebase 存在冲突，或者使用了 `--interactive` 来省略、编辑、合并（squash）或修复（fixup）提交；或者上游使用了提交 `--amend`、`reset` 或 `filter-branch` 之一，就会发生这种情况。

### 简单情况

只有当 `subsystem` 上的更改（基于 diff 内容的补丁 ID）在 `subsystem` rebase 之前后完全相同时才有效。

在这种情况下，修复是简单的，因为 `git rebase` 知道跳过已经存在于新上游更改。所以如果你说（假设你处于 `topic` 上）：

```
$ git rebase subsystem
```

你将得到修复后的历史：

```
o---o---o---o---o---o---o---o master
     \
      o'--o'--o'--o'--o' subsystem
           \
            *---*---* topic
```

### 困难情况

如果 `subsystem` 的更改与 rebase 之前的并不完全对应，情况就会变得复杂。

**注意**

虽然“简单情况恢复”即使在困难情况下有时看起来也是成功的，但可能会产生意外的后果。例如，通过 `git rebase --interactive` 移除的提交将被**复活**！

其思路是手动告诉 `git rebase` “旧的 `subsystem` 在哪里结束，你的 `topic` 从哪里开始”，即它们之间旧的合并基（merge-base）是什么。你必须找到一种命名旧 `subsystem` 最后一个提交的方法，例如：

- 使用 `subsystem` 的 reflog：执行 `git fetch` 后，旧的 `subsystem` 顶端位于 `subsystem@{1}`。随后的 fetch 会增加数字。（见 (1)。）
- 相对于 `topic` 的顶端：知道你的 `topic` 有三个提交，旧的 `subsystem` 顶端必须是 `topic~3`。

你可以通过以下操作将旧的 `subsystem..topic` 移植到新顶端（对于 reflog 情况，并假设你已经在 `topic` 上）：

```
$ git rebase --onto subsystem subsystem@{1}
```

“困难情况”恢复的连锁反应特别糟糕：`topic` 下游的*每个人*现在都必须执行一次“困难情况”恢复！

## 缺陷 (BUGS)

由 `--preserve-merges --interactive` 提供的待办列表并不代表修订图的拓扑。编辑提交和重写提交信息应该正常工作，但尝试重新排序提交往往会产生违反直觉的结果。

例如，尝试重新排列

```
1 --- 2 --- 3 --- 4 --- 5
```

到

```
1 --- 2 --- 4 --- 3 --- 5
```

通过移动 `"pick 4"` 行将导致以下历史：

```
      3
     /
1 --- 2 --- 4 --- 5
```

## GIT

(1) 套件的一部分

## 注释 (NOTES)

1. `revert-a-faulty-merge` How-To

---

# GIT-RECEIVE-PACK

## 名称

`git-receive-pack` - 接收推送到仓库的内容

## 摘要

`git-receive-pack` `<directory>`

## 描述

由 `git send-pack` 调用，并使用从远程端输入的信息更新仓库。

该命令通常不由最终用户直接调用。协议的 UI 在 `git send-pack` 端，该程序对旨在用于向远程仓库推送更新。对于拉取操作，请参见 (1)。

该命令允许在远程端创建和快进 sha1 引用（heads/tags）（严格来说，是本地端 `git-receive-pack` 在运行，但对于坐在 send-pack 端的用户来说，它正在更新远程。感到困惑？）

在 `Documentation/howto` 目录下可以找到其他使用 `update` 和 `post-update` 钩子的真实示例。

`git-receive-pack` 遵循 `receive.denyNonFastForwards` 配置选项，该选项告诉它如果 ref 的更新不是快进（fast-forwards），则应该拒绝更新。

## OPTIONS

`<directory>`

要同步到的仓库。

## PRE-RECEIVE 钩子

在更新任何 ref 之前，如果 `$GIT_DIR/hooks/pre-receive` 文件存在且具有执行权限，它将被调用一次，且不带任何参数。钩子的标准输入是每个要更新的 ref 占一行：

```
sha1-old SP sha1-new SP refname LF
```

`refname` 值相对于 `$GIT_DIR`；例如，对于 master 头部，其值为 `"refs/heads/master"`。每个 `refname` 之前的两个 `sha1` 值是该 `refname` 在更新前后的对象名称。要创建的 ref，其 `sha1-old` 等于 `0{40}`，而要删除的 ref，其 `sha1-new` 等于 `0{40}`，否则 `sha1-old` 和 `sha1-new` 应该是仓库中的有效对象。

在接受签名推送（见 (1) 部分）时，签名推送证书被存储在 blob 中，并可以通过环境变量 `GIT_PUSH_CERT` 查询其对象名称。请参见 `post-receive` 钩子的描述以获取示例。此外，证书使用 GPG 进行验证，结果通过以下环境变量导出：

`GIT_PUSH_CERT_SIGNER`

签名推送证书的密钥所有者的名称和电子邮件地址。

`GIT_PUSH_CERT_KEY`

签名推送证书的密钥的 GPG 密钥 ID。

`GIT_PUSH_CERT_STATUS`

推送证书的 GPG 验证状态，使用与 `git log` 系列命令的 `%G?` 格式相同的助记符（见 (1) 部分）。

`GIT_PUSH_CERT_NONCE`

该过程请求签名者包含推送证书的随机数字符串（nonce string）。如果该值与推送证书中 `"nonce"` 头部记录的值不匹配，则可能表明该证书是有效的，但正在从另一个 `"git push"` 会话中重放。

`GIT_PUSH_CERT_NONCE_STATUS`

`UNSOLICITED`

`"git push --signed"` 在我们没有要求它发送随机数时发送了一个 nonce。

`MISSING`

`"git push --signed"` 没有发送任何 nonce 头部。

`BAD`

`"git push --signed"` 发送了伪造的 nonce。

`OK`

`"git push --signed"` 发送了我们要求它发送的随机数。

`SLOP`

`"git push --signed"` 发送的随机数与我们现在要求发送的不同，但在之前的会话中发送过。请参见 `GIT_PUSH_CERT_NONCE_SLOP` 环境变量。

`GIT_PUSH_CERT_NONCE_SLOP`

`"git push --signed"` 发送的随机数与我们现在要求发送的不同，但在另一个会话中，该会话的开始时间与当前会话差这么多秒。仅当 `GIT_PUSH_CERT_NONCE_STATUS` 为 `SLOP` 时才有意义。另请阅读 (1) 部分中的 `receive.certNonceSlop` 变量。

此钩子在任何 `refname` 更新之前以及任何快进检查执行之前被调用。

如果 `pre-receive` 钩子以非零状态退出，将不会执行任何更新，且更新、`post-receive` 和 `post-update` 钩子也不会被调用。这对于在不支持该更新时快速退出非常有用。

## UPDATE 钩子

在更新每个 ref 之前，如果 `$GIT_DIR/hooks/update` 文件存在且具有执行权限，它会每个 ref 被调用一次，带有三个参数：

```
$GIT_DIR/hooks/update refname sha1-old sha1-new
```

`refname` 参数相对于 `$GIT_DIR`；例如，对于 master 头部，其值为 `"refs/heads/master"`。两个 `sha1` 参数是该 `refname` 在更新前后的对象名称。注意，钩子是在 `refname` 更新之前调用的，因此 `sha1-old` 要么是 `0{40}`（意味着尚不存在该 ref），要么它应该与 `refname` 中记录的内容匹配。

如果钩子想要不允许更新命名的 ref，则应以非零状态退出。否则，应以零退出。

此钩子的成功执行（零退出状态）并不保证 ref 实际上会被更新，它只是一个前提条件。因此，从此钩子中发送通知（例如电子邮件）并不是好主意。考虑使用 `post-receive` 钩子。

## POST-RECEIVE 钩子

在所有 ref 更新（或尝试更新）之后，如果任何 ref 更新成功，且 `$GIT_DIR/hooks/post-receive` 文件存在且具有执行权限，它将被调用一次，且不带任何参数。钩子的标准输入是每个每个成功更新的 ref 占一行：

```
sha1-old SP sha1-new SP refname LF
```

`refname` 值相对于 `$GIT_DIR`；例如，对于 master 头部，其值为 `"refs/heads/master"`。每个 `refname` 之前的两个 `sha1` 值是该 `refname` 在更新前后的对象名称。创建的 ref，其 `sha1-old` 等于 `0{40}`，而被删除的 ref，其 `sha1-new` 等于 `0{40}`，否则 `sha1-old` 和 `sha1-new` 应该是仓库中的有效对象。

在接受签名推送后，可以像 `pre-receive` 钩子一样检查 `GIT_PUSH_CERT*` 环境变量。

使用此钩子可以很容易地生成描述仓库更新的邮件。示例脚本为每个 ref 发送一个邮件，列出推送到仓库的提交，并将签名良好的签名推送的证书记录到日志服务中：

```
#!/bin/sh
# mail out commit update information.
while read oval nval ref
do
    if expr "$oval" : '0*$' >/dev/null
    then
        echo "Created a new ref, with the following commits:"
        git rev-list --pretty "$nval"
    else
        echo "New commits:"
        git rev-list --pretty "$nval" "^$oval"
    fi |
    mail -s "Changes to ref $ref"
done
# log signed push certificate, if any
if test -n "${GIT_PUSH_CERT-}" && test ${GIT_PUSH_CERT_STATUS} = G
then
    (
        echo expected nonce is ${GIT_PUSH_NONCE}
        git cat-file blob ${GIT_PUSH_CERT}
    ) | mail -s "push certificate from $GIT_PUSH_CERT_SIGNER"
fi
exit 0
```

此钩子调用的退出码被忽略，但非零退出码将生成错误信息。

注意，当此钩子运行时，`refname` 可能没有 `sha1-new`。如果另一个用户在 `git-receive-pack` 更新 ref 之后但在钩子能够评估它之前修改了该 ref，这种情况很容易发生。建议钩子依赖于 `sha1-new` 而不是 `refname` 的当前值。

## POST-UPDATE 钩子

在所有其他处理之后，如果至少有一个 ref 被更新了，且 `$GIT_DIR/hooks/post-update` 文件存在且具有执行权限，则 `post-update` 将带有已更新的 ref 列表被调用。这可以用于实现任何仓库的清理任务。

此钩子调用的退出码被忽略；此时 `git-receive-pack` 唯一需要做的事就是直接退出。

此钩子可以用于，例如在仓库已打包并并通过哑传输（dumb transport）提供时，运行 `update-server-info`。

```
#!/bin/sh
exec update-server-info
```



## 参见

(1)、(7)

---

# GIT-REFLOG

## 名称

`git-reflog` - 管理 reflog 信息

## 语法

`git reflog <子命令> <选项>`

## 描述

该命令接受不同的子命令，根据子命令有不同的选项：

```text
git reflog [show] [log-options] [<ref>]
git reflog expire [--expire=<time>] [--expire-unreachable=<time>] [--rewrite] [--updateref] [--stale-fix] [--dry-run] [--verbose] [--all | <refs>...]
git reflog delete [--rewrite] [--updateref] [--dry-run] [--verbose] ref@{specifier}...
```

引用日志（或“reflogs”）记录了分支和其他引用的头部在本地仓库中更新的时间。Reflog 在各种 Git 命令中非常有用，用于指定引用的旧值。例如，`HEAD@{2}` 意味着“两个移动之前的 HEAD 位置”，`master@{one.week.ago}` 意味着“在本地仓库中上周前的 master 指向位置”，依此类推。更多细节请见 (7)。

此命令管理记录在 reflog 中的信息。

`show` 子命令（在没有任何子命令时，这也是默认命令）显示命令行中提供的引用（或默认为 `HEAD`）的日志。reflog（引用日志）涵盖了所有最近的操作，此外，`HEAD` reflog 记录了分支切换。`git reflog show` 是 `git log -g --abbrev-commit --pretty=oneline` 的别名；更多信息请参见 (1)。

`expire` 子命令修剪较旧的 reflog 条目。早于 `expire` 时间的条目，或早于 `expire-unreachable` 时间且无法从当前端点（tip）访问的条目将从 reflog 中删除。终端用户通常不直接使用此命令 --- 请参见 (1)。

`delete` 子命令用于删除 reflog 中的单个条目。其参数必须是一个精确的（exact）条目（例如 `git reflog delete master@{2}`）。该子命令通常也不由终端用户直接使用。

## OPTIONS

### `show` 的选项

`git reflog show` 接受 `git log` 接受的任何选项。

### `expire` 的选项

#### `--all`

处理所有引用的 reflogs。

#### `--expire=<time>`

修剪早于指定时间的条目。如果未指定此选项，过期时间将从配置设置 `gc.reflogExpire` 获取，该设置默认为 90 天。`--expire=all` 不管多久都修剪条目；`--expire=never` 关闭对可访问条目的修剪（但请使用 `--expire-unreachable`）。

#### `--expire-unreachable=<time>`

修剪早于 `<time>` 且无法从分支当前端点访问的条目。如果未指定此选项，过期时间将从配置设置 `gc.reflogExpireUnreachable` 获取，该设置默认为 30 天。`--expire-unreachable=all` 不管多久都修剪不可访问的条目；`--expire-unreachable=never` 关闭对不可访问的早期修剪（但请使用 `--expire`）。

#### `--updateref`

如果上一个顶部条目被修剪，则将引用更新为新的顶部 reflog 条目的值（即 `<ref>@{0}`）（此选项对符号引用会被忽略）。

#### `--rewrite`

如果 reflog 条目的前驱节点被修剪，则将其“旧” SHA-1 调整为与其现在在其之前的条目的“新” SHA-1 字段相等。

#### `--stale-fix`

修剪任何指向“损坏提交”的 reflog 条目。损坏的提交是指无法从任何引用端点访问，且直接或间接引用缺失的提交、树（tree）或二进制（blob）对象的提交。

此计算涉及遍历所有可访问的对象，即代价与 `git prune` 相同。它主要用于修复使用旧版本 Git 进行垃圾回收引起的损坏，旧版本不会保护被 reflog 引用的对象。

#### `-n, --dry-run`

不实际修剪任何条目；仅显示将要修剪的条目。

#### `--verbose`

在屏幕上打印额外信息。

### `delete` 的选项

`git reflog delete` 接受选项 `--updateref`、`--rewrite`、`-n`、`--dry-run` 和 `--verbose`，其含义与用于 `expire` 时相同。

---

# GIT-RELINK

## NAME

`git-relink` - 在本地仓库中对公共对象建立硬链接

## SYNOPSIS

`git relink [--safe] <dir>... <master_dir>`

## DESCRIPTION

这将扫描 1 个或多个对象仓库，并寻找与主仓库共同拥有的对象。尚未与主仓库建立硬链接的对象将被替换为指向主仓库的硬链接。

## OPTIONS

### `--safe`

如果存在两个哈希相同但大小不同的对象，则停止。默认行为是警告并继续。

### `<dir>`

包含 `.git/objects/` 子目录的目录。
