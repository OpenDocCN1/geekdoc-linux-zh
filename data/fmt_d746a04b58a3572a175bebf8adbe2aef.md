
# 第 14 章 使用脚本让工作更轻松

## 使用 `awk` 处理文本

以下是一个 `awk` 脚本示例，用于打印行号和内容：

```awk
increment = 1;
}
{
// 打印数字并回显行。
printf("*%d %s\n", line, 0);
line += increment;
}
```

从文件中执行此操作，将代码保存为扩展名为 `.awk` 的文件，并颁发以下命令。（`.awk` 扩展名不是必须的，但包含它可以标明你正在调用的脚本类型。）

```bash
awk -f file.awk file > newfile
```

每个匹配条件表达式的行前面都会带有一个行号前缀。如果没有匹配条件表达式的行，文件的每一行都会回显到新文件中，且不会添加任何行号。

这里是另一个示例，将实际操作添加到命令中，而不是在文件中：

```bash
awk '{print $1, $2, $3}' file > newfile
```

由于 `0` 代表命令，而 `$1` 代表每行的第一个单词，在这种情况下，结果将是一个名为 `newfile` 的文件，其中包含 `file` 中每行的前三个单词。这通常是以不同格式输出报告最快的方法。

有几本书说明了 `awk` 的用法。流行的一本是 `Sed & Awk (Nutshell Handbook)`，由 Dale Dougherty 和 Arnold Robbins 编写（O'Reilly, 1997）。该工具或称为 `GAWK` 的 GNU 版本包含在大多数 Linux 发行版中，并适用于大多数 Unix 变体。

## `sed` 流编辑器

正如其名，`sed` 是一个流编辑器。它允许对正则表达式进行搜索和替换以及更多操作——当当前任务涉及更新文件时，这是一项有价值的功能。你可以使用 `sed` 通过搜索字符串并根据需要更改它来自动化文本文件的更新。当你需要通过将命令管道到另一个命令来更改命令输出时，它也非常有用，例如使用 `s:phrase/newphrase/` 在编辑器中将一个短语替换为另一个，然后你将知道如何使用 `sed` 命令了；然而，这种更改会自动全局应用，因为 `sed` 是对文件中的每一行进行工作的。

`sed` 可以将操作作为命令行参数执行吗？有时这样做是有益的，例如，一个非常长文件的输出需要微调，以便可以按照老板要求的格式将其打印到新文件中。这是一个相当简单的示例：

```bash
cat /tmp/calendar | sed -e 's/Jan&/uary/' | sed -e 's/Feb&/ruary/' |
sed -e 's/Mar&/ch/' | sed -e 's/Apr&/il' | sed -e 's/Jun/&/' | sed -e 's/Jul&/y/' > newfile
```

在这个示例中，一个包含当年前七个月日期的文件需要被修改，以便缩写的月份名称替换为该月份的完整名称。编辑后的文件将写入 `newfile`。首先，我们通过 `cat` 将文件连接到一系列 `sed` 命令。`sed` 告诉我们下一步是一个要执行的 `sed` 命令。该命令在单引号内的位置将其与该行的其余部分区分开来。`s` 表示我们希望用第二个短语替换第一个。因此，此命令行满足了我们对文件修改的需求，当它在一个例如 1000 行的文件中节省大量按键次数时，其长度是完全合理的。

与 `awk` 一样，`sed` 包含在大多数 Linux 发行版中并适用于大多数 Unix 变体。

## 系统初始化脚本

通常当你使用某些最近开发的工具时，你需要在启动时启动该工具，并且无法依赖现有的脚本来完成。对于这些情况，你需要编写自己的初始化脚本，并将其添加到我们在第 5 章中讨论的初始化脚本中。如果你遵循现有脚本的示例，这实际上非常容易。这些脚本是 `Bash Shell` 脚本，并共享共同格式。

![System Initialization Script](img/4fb617eb648f87def380ef5d92052d01_502_0.png)

## 适配 Bash Shell 脚本

你将处理许多脚本都是 `Bash Shell` 脚本。这些脚本本身通常已经足够好了。你不需要更改其中的许多。尽管如此，知道如何这样做是非常重要的，因为某些特殊情况会要求你编写脚本或编辑现有的脚本。

## 编写初始化脚本

假设你从某个网站下载了我的 `mynewutility` 的 `tar` 包。显然，在 `/etc/rc.` 层次级结构中没有 `mynewutility` 脚本，因为该工具不是标准发行版的一部分。当你完成工具的安装并配置它后，你可能希望在启动时像 `/etc/rc.d` 层次结构中的其他守护进程一样启动。为了实现这一点，你需要编写一个初始化脚本来管理这个新工具。

让我们看看打印守护进程的现有脚本并将其适配用于管理 `mynewutility`。Red Hat 7.0 的打印机启动脚本是 `/etc/rc.d/init.lpd`，如列表 14.9 所示。

### 列表 14.9 `lpd` 的示例初始化脚本

```bash
#!/bin/sh

# lpd            此壳脚本负责启动和停止
# lpd (打印机守护进程)。

# chkconfig 2345 60 60
# description: lpd 是 lpr 正常工作所需的打印守护进程 \
#      properly. 它基本上是一个调配 \
#      打印作业到打印机(s) 的服务器。
# processname: /usr/sbin/lpd

if [ -x /etc/rc.d ]; then
    . /etc/rc.d
fi

start() {
    echo "Starting lpd..."
    if [ -f /var/run/lpd.pid ]; then
        echo "lpd is already running"
        return 0
    fi
    /usr/sbin/lpd /var/run/lpd.pid
    if [ $? -eq 0 ]; then
        return 0
    else
        return 1
    fi
}

stop() {
    echo "Stopping lpd..."
    if [ -f /var/run/lpd.pid ]; then
        kill `cat /var/run/lpd.pid`
        rm /var/run/lpd.pid
    else
        echo "lpd is not running"
    fi
    return 0
}

status() {
    if [ -f /var/run/lpd.pid ]; then
        echo "lpd is running"
    else
        echo "lpd is not running"
    fi
}

case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    status)
        status
        ;;
    *)
        echo "Usage: $0 {start|stop|status}"
        exit 1
        ;;
esac
```

`lpd` 脚本的最后一行是 `$RETVAL` 变量的返回值，该变量是由脚本执行的函数生成的。

现在你已经理解了现有的脚本，为 `mynewemutility` 创建你自己的初始化脚本将变得容易。假设 `mynewemutility` 需要网络激活状态，且可执行文件位于 `/usr/sbin/mynewutilityd`。在这种情况下，我们只需要 `start`、`restart`、`stop` 和 `status` 功能。新脚本看起来类似于列表 14.10。

### 列表 14.10 `mynewemutility` 的初始化脚本
