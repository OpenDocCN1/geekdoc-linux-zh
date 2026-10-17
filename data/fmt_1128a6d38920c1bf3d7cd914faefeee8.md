
`-h,--help` 打印帮助信息并退出。`-v,--version` 打印版本信息并退出。`-m,--manual` 默认使用 man 页而不是 info（`pinfo -m` 可作为手册分页器）。警告：此选项后的所有内容都传递给 `man` 程序。如果 `pinfo` 选项跟随 `-m` 不起作用，不要困惑。使用此选项时，`pinfo` 不再照常解析 info 选项！它调用程序的 man 部分。

你也可以通过另一种方式调用 `pinfo` 的函数。当调用 `pinfo` 且其 `argv[0]`（程序名）包含 'man' 字样时，man 功能会自动启用。

之前有一个 `pinfo` 的同步工具名为 `man`，但我必须从发行版中删除了它，因为它的名称与其他工具冲突。总之，如果你需要，可以创建一个链接。

`- --force-manual-table-` 强制手动检测标签表（tag table）。这允许你查看 info 页面，这些页面可能是损坏的（例如 RH5.0 自带的 jed 页面版本）。标签表损坏通常体现在 info 链接上，你点击这些链接时会将你带到完全意料之外的节点。

`- --node=nodena, --node nodena-` 跳转到 info 文件中的 `nodena` 节点。从 0.6.7 版本开始，也可以通过文件路径作为独立的内联 info 来指定节点，例如 `(gcc)Introduction`。

`- --rcfile=filena, --rcfile filena-` 使用备用配置文件。

`- --long-manual-links, -l-` 在手册中使用链接全名。在某些系统上，手册层级被划分为如 `3ncurses` 这样的子章节，而在另一些系统上，所有内容都属于章节 `3`。如果你的系统是这种情况，请随时使用它。

`- --clear-at-exit,- -x-` 退出时清除屏幕。

这些选项由 GNU `getopt` 处理，因此你可以像其他程序一样，通过选项之间差异的最少字符数来缩写选项名称。

警告！如果你没有安装 `getopt`，这些选项将无法工作！

## 浏览 info 文件时的默认按键

请查看示例配置文件（下文）以及按键描述。手册查看器中的可用按键与 info 查看器中的可用按键略有不同。

## 环境变量

存在一个变量 `$INFOPATH`，它可以指定搜索 info 文件的路径。

它的格式与 `$PATH` 变量相似。一个设置示例可能如下：

`/usr/info:/usr/sowhere/info:/not/even/in/usr/info`

等目录之间用冒号分隔。

## 颜色和按键定义

名为 `~/.pinfo/etc/pinfo` 的配置文件，用于本地和全局配置（前缀是 `pinfo` 安装目录的 la缀，例如 `/usr/local` 或 `/`）。这里是一个文件示例，我们将讨论其内容：

```
# 这里还有颜色设置。条目之间的空格是可选的。
COL_NORMAL = COLOR_WHITE, COLOR_BLACK, NO_BOLD, NO_BLINK
COL_MOUSESELECTED = 
COL_MENU=COLOR_BLUE, COLOR_BLACK, BOLD, NO_BLINK
COL_SELECTED=COLOR_RED, COLOR_BLACK, BOLD, NO_BLINK
COL_NOTE=COLOR_GREEN, COLOR_BLACK, BOLD, NO_BLINK
COL_TOPLINE=COLOR_YELLOW, COLOR_BLUE, BOLD, NO_BLINK
COL_BOTTOMLINE=COLOR_YELLOW, COLOR_BLUE, BOLD, NO_BLINK
COL_VARIALABLE=COLOR_WHITE, COLOR_BLACK, BOLD, NO_BLINK
COL_MANUAL=COLOR_WHITE, COLOR_BLACK, BOLD, NO_BLINK
COL_URL=COLOR_MAGENTA, COLOR_BLACK, BOLD, NO_BLINK
COL_SELECTED=COLOR_RED, COLOR_BLACK, BOLD, NO_BLINK
COL_INFOLIGHT=COLOR_WHITE, COLOR_BLACK, BOLD, NO_BLINK
# 这里是按键绑定，
KEY_SEARCH_1 = '/' KEY_SEARCH_2 = '=' KEY_GOTO_1='g' KEY_GOTO_2='m'
KEY_HOME_1='h' KEY_HOME_2='h' KEY_PREVIOUS_1='p' KEY_PREVIOUS_2='p'
KEY_NEXT_1='n' KEY_NEXT_2='n' KEY_UP_1='u' KEY_UP_2='u'
KEY_END_1='e' KEY_END_2='e' KEY_PGDN_1='pgdn' KEY_PGDN_2='b'
KEY_PGUN_1='o' KEY_PGUN_2='o' KEY_PGUP_1='pgup' KEY_PGUP_2='b'
KEY_PAGE_1='p' KEY_PAGE_2='p' KEY_DOWN_1='d' KEY_DOWN_2='d'
KEY_TOP_1='t' KEY_TOP_2='t' KEY_LEFT_1='l' KEY_LEFT_2='l'
KEY_LINK_1='f' KEY_LINK_2='f' KEY_SHELL_1='s' KEY_SHELL_2='s'
KEY_REFRESH_1='r' KEY_REFRESH_2='r' KEY_DIRPAGE_1='d' KEY_DIRPAGE_2='d'
KEY_QUIT_1='q' KEY_QUIT_2='q' KEY_GOLINE_1='g' KEY_GOLINE_2='g'
KEY_PRINT_1='p' KEY_PRINT_2='p' 
# 这些选项，在 man 页中启用 Manual=false CUT-MAN-HEADERS=true
EMPTY-LINES=true FILENAME=false APROS=false DONT-WITHOUT-CUT-CONFIRMATION=true-DEFAULT=no SCREEN-EXIT=true
STDERR="2"/dev/null FTPviewer=lynx
MAILER=1:0x33
INFOPATH=/usr/info/share/info/usr/local/info
HIGHLIGHTREGEXP=#has SAFE-USER=nobody SAFE-GROUP=nobody
```

如你所示，颜色格式非常简单。首先我解释颜色定义。你可以输入颜色名称（所有可用颜色都在示例中，并且具有解释性）。还有一个特殊颜色 `COLOR_DEFAULT`，表示透明。然后输入前景颜色和背景颜色。`BOLD` 属性指定要高亮的颜色（例如浅蓝色、浅绿色）。`BLINK` 属性是配置中的闪烁或高亮背景。

现在让我们来看看按键定义。在这里我们放置一个键（再次，所有按键都在示例中）；然后输入它——要么用单引号括，要么使用键码（如 `KEY_REFRESH_1` 所示）。如果你想通过代码指定键，请使用提供的 'key' 来获取所需值。这主要是一个功能，允许你添加 `CTRL+字母` 的按键绑定等。对于每个功能，你可以绑定两个键，例如可以同时将 Enter 和光标右键绑定到 FollowLink（跟随链接）。如示例所示，这两个键别为 `KEY_FOLLOWLINK_1` 和 `KEY_FOLLOWLINK_2`。

### KEY_TOTARCH_1

用于搜索 info 文件所有节点的按键。

### KEY_TOTARCH_2

搜索 info 文件所有节点的备用按键。

### KEY_SEARCH_1

用于在当前节点（或手册）中搜索的按键。

### KEY_SEARCH_2

用于在当前节点（或手册）中搜索的备用按键。

### KEY_GOTO_1

用于跳转到节点的按键。

### KEY_GOTO_2

用于跳转到节点的备用按键。

### KEY_HOME_1

跳转到首页的按键。

### KEY_HOME_2

跳转到首页的备用按键。

### KEY_PREVIOUS_1

向上上一个节点的按键。

### KEY_PREVIOUS_2

向上上一个节点的备用按键。

### KEY_NEXT_1

向下到下一个节点的按键。

### KEY_NEXT_2

向下到下一个节点的备用按键。

### KEY_UP_1

向上滚动的按键。

### KEY_UP_2

向上滚动的备用按键。

### KEY_END_1

跳转到末尾的按键。

### KEY_END_2

跳转到末尾的备用按键。

### KEY_PGDN_1

向下翻页的按键。

### KEY_PGDN_2

向下翻页的备用按键。

### KEY_PGUP_1

向上翻页的按键。

### KEY_PGUP_2

向上翻页的备用按键。

### KEY_PAGE_1

翻页的按键。

### KEY_PAGE_2

翻页的备用按键。

### KEY_DOWN_1

向下滚动的按键。

### KEY_DOWN_2

向下滚动的备用按键。

### KEY_TOP_1

跳转到顶部的按键。

### KEY_TOP_2
