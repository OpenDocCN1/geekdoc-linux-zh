
- `archie`: 在互联网存档中搜索文件。

- `flip`: 在 Unix 和 DOS 格式之间转换文本文件。

- `glimpse`: 在大量文件中进行模糊字符串搜索（使用 `agrep`）。

- `lynx`: 文本模式 浏览器。

这里是与 Unix 系统管理相关的 Web 页面：

通用信息 [链接](http://www.ensta.fr/internet/unix/sys_admin/) 或 [链接](http://www.sai.msu.edu/sysadm.html)

在 [链接](http://www.iem.ac.ru/sysadm.html) 有一个 Unix 系统管理教程。

Unix 在线杂志首页 [链接](http://www.wcm.com/uworld/)

Unix 系统管理员互联网基础教程 [链接](http://www.greatcircle.com/tutorials/ieusa.html)

互联网上可用 Unix 实用工具的链接 [链接](http://www.ensta.fr/internet/unix/)

互联网上可用 Unix 系统管理“工具”的链接 [链接](http://www.ensta.fr/internet/unix/sys_admin/)

## 5. 阶段 4 Linux 下的 Emacspeak

`Emacspeak` 的 `Slack` 设置脚本应该创建必要的环境变量，并安装一个让 `emacs` 通过 `emacspeak` 启动的脚本（`emacs` with `emacs`）。这是你学习 `Emacs` 的第四种选择。这是你第一次能够使用 `Emacspeak`。下面显示一个简短的教程。在 `Emacs` 内部，你可以输入 `C-h c` 获取命令列表。要进行搜索，使用 `C-h a`。要获取键序列的解释，使用 `C-h`。还有一个作为 `Emacspeak` 一一部分的 `info` 文件。在 `Emacs` 内部，你可以输入 `C-h i` 打开 `info` 页面目录。通过输入 `C-h c` 搜索 `emacspeak` 菜单项，按两次回车（第一次终止搜索，第二次进入 `info` 页面）。如果你安装了独立的 `info` 程序，可以使用该命令查阅 `info` 文件。

### 5.1 Emacspeak 介绍 - 语音启用

所有正常的移动功能在移动后都会读出相关信息。以下是一些启用了语音的光标移动函数。注意，这仅列出了其中少数几个；`Emacspeak` 的目的是让所有 `emacs` 启用语音，并在工作时为你提供语音反馈。因此，此列表作为 `Emacspeak` 提供的语音命令类型的代表：

- `C-n` 或 `M-x next-line` 或 `down`: 将光标移动到下一行并读出。

- `C-p` 或 `M-x previous-line` 或 `up`: 将光标移动到上一行并读出。

- `C-f` 或 `M-x forward-word`: 将光标移动到下一个单词并读出。它将光标放在下一个单词的首字符上，而不是它之前的空格（这是我的偏好）。

- `M-b` 或 `M-x backward-word`: 将光标移动到上一个单词并读出。

- `M-C-b` 或 `M-x backward-sex`: 将光标移动到上一个单词（`sex`）并读出。如果语音跨多行，则只读第一行。

- `M-<` 或 `M-x beginning-of-buffer`: 读出移动到的行。

- `M->` 或 `M-x end-of-buffer`: 读出移动到的行。

- `M-m` 或 `M-x back-to-indentation`: 读出回到缩进的行。

### 5.2 Emacspeak 介绍 - 新命令

`Emacspeak` 提供了许多用于读取缓冲区内容、获取状态以及修改 `Emacspeak` 状态的命令。这些命令名称都以 `emacspeak-` 前缀。在 `EMACSPEAK-KEYMAP` 中绑定到 `l` 的 `emacspeak-line` 命令通过 `Control-e` 访问。这里是某些读取文本的命令：

- `C-e c` 或 `M-x emacspeak-speak-char`: 使用音标字母读出字符。

- `C-e w` 或 `M-x emacspeak-speak-word`: 读出当前单词。

- `C-e l` 或 `M-x emacspeak-speak-line`: 读出当前行。带有 `C-u` 前缀时，从光标处开始读。如果语音锁定模式（`voice-lock-mode`）开启，则读出缩进。如果 `emacspeak-show` 开启（见 `emacspeak-show-point`）。

- `C-e q` 或 `M-x emacspeak-speak-point`: 读出当前句子。

- `C-e C` 或 `M-x emacspeak-speak-current-window`: 读出当前窗口的所有内容。

- `C-e =` 或 `M-x emacspeak-speak-column`: 读出光标所在的列。

`Emacspeak` 提供的第二类命令操作语音设备的状态。这些命令的名称都以 `dtk-` 前缀。你可以通过 `Control-d` 前缀访问这些命令。因此，在 `EMACSPEAK-SUBMAP` 中绑定到 `r` 的 `dtk-set-rate` 命令可以通过 `Control-d` 执行。

- `C-e s` 或 `M-x emacspeak-dt-stop`: 立即停止语音。此外，任何产生语音输出的命令都会丢弃缓冲区中的任何内容。

- `C-e d I` 或 `M-x emacspeak-dt-stop-immediately-while-typing`: 切换 `dtk-stop-immediately-while-typing` 变量的状态。正如名称所示，如果为真，会在输入时刷新语音。

- `C-e i` 或 `M-x emacspeak-audio-indentation`: 切换 `Emacspeak` 语音缩进的状态。将缩进方法指定为 `tone` 会导致 `DECTalk` 长度取决于行缩进的音调。指定为 `speak` 则会读出初始空格数。

- `C-e dk` 或 `M-x emacspeak-character-echo`: 切换 `Emacspeak` 字符回显的状态（即：输入的字符是否被回显）。

- `C-e w` 或 `M-x emacspeak-toggle-echo`: 切换 `Emacspeak` 单词回显的状态（初始开启）。

- `C-e d l` 或 `M-x emacspeak-toggle-line-echo`: 切换 `Emacspeak` 行回显的状态（即：按回车键后输入的文本是否被回显）。

- `C-e p` 或 `M-x dtk-set-punctuations`: 设置标点符号状态。可能的值有 `'some'`、`'all'` 或 `'none'`。

- `C-e q` 或 `M-x dtk-toggle-quiet`: 在语音设备的安静和健谈之间切换状态。当你想继续使用一个加载了 `emacspeak` 的 `emacs` 会话但希望它闭嘴时，这非常有用。

## 5. 第 4 阶段 Linux 下的 Emacspeak

`C-e d R` 或 `M-x dtk-reset-state`

恢复 `Delta` 的正常状态。通常在 `Deltacl` 循环电源后使用。

`C-e SPC` 或 `M-x dtk-toggle-splitting-on-white-space`

切换 `emacspeak` 状态，决定是仅根据语句边界拆分语音，还是包含空白符。

`C-e d r` 或 `M-x dtk-set-rate`

为 `deltacl` 设置语音速率。

`C-e d s` 或 `M-x dtk-toggle-split-caps`

切换大写拆分模式。从小写到大写的转换被视为新单词的开始。这在阅读程序源代码中的匈牙利命名法（`Hungarian notation`）时非常有用。

`C-e d v` 或 `M-x voice-lock-mode`

切换语音锁定（`Voice Lock`）模式（默认关闭）。启用语音锁定模式时，文本会在你输入时朗读，如下：

- 注释将以 `voice-lock-personality-`（该值应为个性名称）朗读。
