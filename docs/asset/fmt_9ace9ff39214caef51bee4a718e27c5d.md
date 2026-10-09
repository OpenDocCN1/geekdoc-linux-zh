
## 滚动回滚模式

我们可以在 `screen` 窗口中执行此操作。在 `screen` 窗口中发布 `screen` 命令并不会调用 `screen` 窗口切换到另一个。它是通过进入所谓的“回滚模式”来实现的。它告诉现有的 `screen` 实例执行类似创建新窗口的操作。

## 复制与粘贴

考虑到 `GNU screen` 是为了既没有图形用户界面也没有鼠标的系统开发的，因此 `screen` 提供一种从一个 `screen` 窗口复制文本到另一个窗口的方法是合理的。在这种模式下，`screen` 允许文本光标在当前窗口中以及回滚缓冲区（其中包含窗口之前的内容）中自由移动。

我们通过输入 `` `Ctrl-a {` `` 进入回滚模式。在回滚模式下，我们可以使用方向键以及 `Page Up` 和 `Page Down` 键导航回滚缓冲区。要复制文本，我们首先需要标记目标文本的开头并按下空格键，这是通过将光标移动到目标文本的开头（光标移动时会高亮）并再次按下空格键来标记要复制文本的结束。标记文本会退出回滚模式并将标记的文本复制到 `screen` 的内部缓冲区。我们现在可以将文本粘贴到任何 `screen` 窗口中。要做到这一点，我们转到目标窗口并输入 `` `Ctrl-a ]` ``。

## 分离会话

要从终端分离会话，使用 `` `Ctrl-a d` ``。这会让会话在后台运行，允许你注销。重新连接到分离会话，使用 `screen -r`。如果有多个会话运行，使用 `screen -ls` 列出它们，然后指定 PID 或名称重新连接。要强制分离已在别处连接会话，使用 `screen -d -r`。

## 自定义 Screen

像交互式工具一样，`screen` 是自定义的。在调用期间，`screen` 会读取存在的 `/etc/screenrc` 和 `~/.screenrc` 文件。虽然自定义功能列表非常详尽（许多与类 Unix 平台上的终端显示有关），但我们将关注键绑定和启动会话配置。

首先，让我们看看示例 `.screenrc` 文件：

```bash
## 这是一个注释

## 设置一些键绑定

bind k           # 解绑 "k" 键（设置为无操作）

bind K kill      # 'Ctrl-a K' 销毁当前窗口

bind ) history  # 'Ctrl-a -' 复制粘贴当前
                 # 命令行

## 在启动时定义窗口 7、8 和 9

screen -t "mc cmdr" 7 mc

screen -t htop 8 htop

screen -t 9 tail /var/log/syslog
```

如我们所示，格式非常简单。`bind` 指令后跟着按键和要绑定的命令。`screen` 手页中找到的命令完整列表。我们到为止讨论的所有 `screen` 命令都类似于示例中的键绑定。我们可以重新定义所有内容。

示例 `.screenrc` 结尾的三行在启动时创建窗口。这些命令设置了窗口标题（`-t` 选项）、窗口编号以及窗口包含的命令。这样，我们就可以设置一个自动构建的 `screen` 会话。

当我们启动 `screen` 时，会包含一个完整的多窗口命令行环境，其中运行着我们所有喜爱的程序。

## tmux

尽管 `GNU screen` 仍然很流行，但由于其代码复杂性（甚至到了“不可维护”的地步）和资源消耗一直受到批评。此外，据报道 `screen` 已不再进行活跃开发。为了应对这些担忧，一个更新的程序 `tmux` 吸引了广泛关注。

`tmux` 更现代、更友好、更高效，并且在大多数方面普遍优于 `screen`。在概念上，`tmux` 与 `screen` 非常相似，它们都支持会话（sessions）、窗口和区域（在 `tmux` 中称为 `panes`）的概念。事实上，它甚至与 `screen` 共享一些键盘命令。

## 可用性

`tmux` 广泛可用，尽管没有 `screen` 那么普及。它适用于大多数发行版的软件库。软件包得名为“`tmux`”。

## 调用

通过命令 `tmux new` 调用程序以创建一个新会话。我们可以可选地添加 `-s <session_name>` 为新会话命名，并添加 `-n <window_name>` 为第一个窗口命名。如果未提供 `new` 命令的选项，可以省略 `new` 本身；系统会默认执行。以下是一个示例：

```bash
me@linuxbox: ~ $ tmux new -s "my session" -n "window 1"
```

程序启动后，我们将看到一个 shell 提示符和窗口底部一个精美的状态栏。

![](img/9aafc495f4afbc0a97de2b31a0d13f46_46_0.png)

初始 `tmux` 窗口

## 多窗口

`tmux` 使用键盘的方式与 `screen` 类似，但它不是使用 `Ctrl-a` 作为命令前缀，而是使用 `Ctrl-b`。这是件好事，因为在 `bash` 中编辑命令行时，`Ctrl-a` 用于将光标移动到行首。

以下是创建窗口和导航窗口的基本命令：

| 命令 | 描述 |
| --- | --- |
| `Ctrl-b ?` | 显示按键绑定列表（即帮助） |
| `Ctrl-b c` | 创建新窗口 |
| `Ctrl-b n` | 转到下一个窗口 |
| `Ctrl-b p` | 转到上一个窗口 |
| `Ctrl-b 0` | 转到窗口 0。数字 1-9 类似。 |
| `Ctrl-b w` | 显示窗口列表。状态栏也列出了窗口。 |
| `Ctrl-b ,` | 重命名当前窗口 |

`tmux` 窗口命令

## 多窗格

像 `screen` 一样，`tmux` 可以将终端显示划分为称为 `panes` 部分。然而，与 `screen` 中区域的实现不同，`tmux` 中的 `panes` 不仅仅提供各个窗口的视图。在 `tmux` 中，它们是与窗口关联的完整伪终端。因此，单个 `tmux` 窗口可以包含多个终端。

## 命令描述

| 命令 | 描述 |
| --- | --- |
| `Ctrl-b "` | 水平分割窗格 |
| `Ctrl-b %` | 垂直分割窗格 |
| `Ctrl-b arrow` | 移动到相邻窗格 |
| `Ctrl-b Ctrl-arrow` | 按1字符调整窗格大小 |
| `Ctrl-b Alt-arrow` | 按5字符调整窗格大小 |
| `Ctrl-b x` | 销毁当前窗格 |

## `tmux` 窗格命令

我们可以通过创建一个会话和窗口来演示 `panes` 的行为。首先，我们将创建一个会话，命名它，并命名初始窗口：

```bash
@linuxbox: ~ $ tmux new -s PaneDemo -n Window0
```

接下来，我们将创建第二个窗口并给它命名：

```bash
@linuxbox: ~ $ tmux new -n Window1
```

我们本可以使用 `Ctrl-b` 命令完成第二步，但通过命令行方法可以为稍后某些操作做些准备。

假设一切顺利，现在我们正处于一个名为 `"PaneDemo"` 的 `tmux` 会话和一个名为 `"Window1"` 的窗口中。现在我们通过输入 `Ctrl-b .` 将窗口水平平分为两部分。我们只有两个窗口（`Window0` 和 `Window1`），但现在 `Window1` 上有两个提示符。我们可以通过输入 `Ctrl-b` 后跟上方向箭头或向下箭头在两个窗格之间来回切换。

为了好玩，我们输入 `Ctrl-b t`，当前窗格中出现了一个数字时钟。这只是 `tmux` 可以做的一个趣事。

![](img/9aafc495f4afbc0a97de2b31a0d13f46_48_0.png)

## 多窗格

我们可以通过输入 `q` 来启用时钟显示。如果我们通过输入 `Ctrl-b 0` 回到第一个窗口，会发现 `panes` 仍然与 `Window1` 关联，且对 `Window0` 没有影响。

回到 `Window 1`，让我们调整窗格的大小。我们通过输入 `Ctrl-b Alt-arrow` 将边界向上或向下移动 5 行。输入 `Ctrl-b Ctrl-arrow` 将将边界移动 1 行。

可以将一个窗格拆分为它自己的新窗口。这是通过输入 `Ctrl-b !` 实现的。

`Ctrl-b x` 用于销毁窗格。注意，与 `screen` 不同，在 `tmux` 中销毁窗格会销毁运行在其内部的终端以及任何关联的窗格。

## 复制模式

像 `screen` 一样，`tmux` 有复制模式。通过输入 `Ctrl-b [` 触发。在复制模式下，我们可以在滚动缓冲区内自由移动光标。为了标记复制内容，我们首先输入 `Ctrl-space` 开始。

```bash
set -g default-terminal "screen-256color"

## Make copy work like vi

## Start copy 'b-

## Use vi movement keys (arrows, etc.)

## Select with V, y

## Yank and copy mode with y

## Paste with 'b-

## View all key bindings with 'b-: followed by list-keys -T copy-mode-vi

set-window-option -g mode-keys vi

bind-key -T copy-mode-vi 'v' send -X begin-selection

bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel
```

## byobu

`byobu`（发音为 "BEE-oh-boo”）源自日语，意为“折叠的装饰性的多面板屏幕”，它并不是一个终端复用器本身，而是 `GNU screen` 或 `tmux` 的封装器（默认为 `tmux`）。它的目的是创建一个简化的用户界面，重点是在状态栏上显示实用的系统信息。

## 可用性

`byobu` 最初由 Canonical 员工 Dustin Kirkland 开发，因此通常在 Ubuntu 和其他基于 Debian 的发行版中找到。最近的版本比初始版本更具移植性，并开始出现在更广泛的发行版中。它以包 "byobu"的形式发行。

## 调用

可以通过输入命令 `byobu` 来启动 `byobu`，后面跟跟传递给后端终端复用器（即 `tmux` 或 `screen`）的选项和命令。对于本次介绍，我们将讨论限制在 `tmux` 后端，因为它支持更丰富的功能。

```bash
me@linuxbox - $ _
```

初始 `byobu` 窗口

## 使用

与 `screen` 和 `tmux` 不同，`byobu` 不使用像 `Ctrl-a` 这样的命令前缀来启动命令。`byobu` 极地依赖功能键。这使得 `byobu` 变得稍微更容易，但作为交换，它牺牲了底层终端复用器的一些某些和灵活性。尽管如此，`byobu` 为最实用的功能提供了易于使用的界面，并提供了一个按键（`F12`），作为 `tmux` 命令的命令前缀。以下是使用 `tmux` 作为默认值时 `byobu` 提供的帮助文件摘录：

| 按键 | 描述 |
|---|---|
| F1 | * 由 F1 使用 |
| Shift-F1 | 显示帮助 |
| F2 | 创建新窗口 |
| Shift-F2 | 创建水平分割 |
| Ctrl-F2 | 创建垂直分割 |
| Ctrl-Shift-F2 | 创建新会话 |
| F3/4 | 在窗口间切换焦点 |
| Shift-F3/F4 | 在分割间切换焦点 |
| Ctrl-F3/F4 | 移动分割 |
| Ctrl-Shift-F3/F4 | 移动窗口 |
| Alt-Up/Down | 在会话间切换焦点 |
| Shift-Left/Right/Up/Down | 在分割间切换焦点 |
| Ctrl-Shift-Left/Right | 在窗口间切换焦点 |
| Ctrl-Left/Right/Up/Down | 调整分割大小 |
| F5 | 重新加载配置，刷新状态 |
| Shift-F5 | 切换状态行显示/隐藏 |
| Ctrl-F5 | 重新连接 ssh/gpg/dbus 套接 |
| Ctrl-Shift-F5 | 随机更改状态栏颜色 |
| F6 | 分离会话并注销 |
| Shift-F6 | 分离会话但不注销 |
| Ctrl-F6 | 杀死焦点所在的分割 |

终端复用器 43

| 按键 | 描述 |
|---|---|
| F7 | 进入滚动回滚历史 |
| Alt-PageUp/PageDown | 进入并滚动回滚历史 |
| F7 (cont.) | 更改当前窗口名称 |
| F8 | 切换分割布局 |
| Shift-F8 | 恢复分割面板布局 |
| Ctrl-F8 | 保存当前分割面板布局 |
| Ctrl-Shift-F8 | 启动 byobu-config 窗口 |
| F9 | * 由 X11 使用 * |
| F10 | * 由 X11 使用 * |
| Shift-F12 | 将分割扩展为全窗口 |
| Ctrl-Shift-F12 | 将窗口合并为水平分割 |
| Modrian 方块 | 将窗口合并为垂直分割 |
| F12 | 转义序列 |
| Shift-F12 | 切换/关闭 Byobu 的按键绑定 |
| Ctrl-Shift-F12 | 转义序列 |

正如我们所看到的，大多数命令对应于我们在 `tmux` 中已经过的功能。然而，还有几个有趣的添加。

首先是 `F9` 键，它会弹出一个菜单屏幕：

![](img/9aafc495f4afbc0a97de2b31a0d13f46_53_0.png)

`byobu` 菜单

选项非常直而易见，尽管“更改转义序列”项仅在用作背景时才相关。如果我们选择“切换状态通知”，我们就得到了 `byobu` 中一个非常实用的功能：丰富且易于配置的状态栏。

## Byobu 配置菜单

![](img/9aafc495f4afbc0a97de2b31a0d13f46_54_0.png)

元素之间使用 `<Tab>` | `<Enter>` 选择 | `<Esc>` 退出
`[0] 0-:config* 222h 2.55 0.7GHz 438M50 2014-03-19 19:07:27`

## 状态通知

在这里我们可以从各种系统状态信息中选择显示。如果我们正在监控状态，这非常有用。

第二个是 `Shift-F12` 键，它可以禁用 `byobu`。遗憾的是，`byobu` 提供了一系列功能。

## 复制模式

`byobu` 提供了一个复制文本的模式。以下是按键：

| 按键 | 描述 |
|---|---|
| F9 | 打开菜单屏幕 |
| F12 | 切换状态通知 |

## 分离会话

与 `screen` 和 `tmux` 不同，`byobu` 不使用像 `Ctrl-a` 这样的命令前缀来启动命令。`byobu` 极地依赖功能键。

## Shell 函数示例

正如我们在 TLCL 中回顾过的样，shell 函数是微型的 shell 脚本，我们可以将其添加到 `.bashrc` 文件中，以执行任何我们本可能通过 shell 脚本完成的操作。这里是一个显示系统健康快速摘要的示例函数：

```bash
status() {

  echo -e "uptime:"

  utime

  echo -e "disk space:"

  df -h 2>/dev/null

  echo -e "inodes:"

  df -i 2>/dev/null

  echo -e "\nblock devices:"

  blkid

  echo -e "\nmemory"

  free -m

  if [[ -f /var/log/syslog ]]; then

    echo -e "syslog"

    tail /var/log/syslog

  fi

  if [[ -f /var/log/messages ]]; then

    echo -e "messages"

    tail /var/log/messages

  fi

} | less
```

与别名（aliases）不同，shell 函数可以接受位置参数：

```bash
params() {

  local argc=0

  while [[ -n $1 ]]; do

    argc=$((++argc))

    echo "Argument $argc $1"

    shift

  done

}
```
