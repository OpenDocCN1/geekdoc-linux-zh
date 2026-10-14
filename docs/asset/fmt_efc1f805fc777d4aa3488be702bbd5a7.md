
大多数现代系统都有一套管理多个进程的机制。Linux 为此目的提供了丰富的工具。鉴于 Linux 是全球部署最广泛的服务器操作系统，这非常有意义。然而，与某些其他系统不同，Linux 主要依赖命令行工具进行进程管理。尽管 Linux 有图形化进程工具，但由于其速度快且占用资源少，命令行工具更受青睐。虽然 GUI 工具看起来很漂亮，但它们本身通常会产生大量的系统负载，这在某种程度上违背了初衷。

# 第 2 部分 – 配置与环境

## 11 – 环境

正如我们之前讨论过的，`shell` 在我们的 `shell` 会话期间维护一组信息。存储在环境变量中的数据被程序用于确定有关我们配置的实信息。虽然大多数程序使用配置文件来设置设置，但它们也会查找存储在环境变量中的值来调整行为。通过这一点，我们可以使用环境变量来定制我们的 `shell` 体验。

在本章中，我们将使用以下命令：

- `printenv` – 打印部分或全部环境变量
- `set` – 设置 `shell` 选项
- `export` – 将环境变量导出到后续执行的程序
- `alias` – 为命令创建别名

### 环境中存储了什么？

`shell` 在环境中存储了两种基本类型的数据，尽管在 `bash` 中这些类型在很大程度上无法区分。它们是环境变量和 `shell` 变量。`shell` 变量是 `bash` 放置的数据片段，而环境变量是其他所有内容。除了变量外，`shell` 还存储了程序化数据，即别名和 `shell` 函数。我们在第 5 章中涵盖了别名，`shell` 函数（与 `shell` 脚本相关）将在第 4 部分介绍。

#### 检查环境

要查看环境中存储了什么，可以使用 `bash` 内置的 `set` 命令或 `printenv` 程序。`set` 命令会显示 `shell` 变量和环境变量，而 `printenv` 只显示后者。由于环境变量内容的列表相当长，最好将任一命令的输出通过到 `less`：

```
[me@linuxbox ~]$ printenv | less
```

这样做后，我们应该得到类似这样的内容：

```
KDE_MULTIHEAD=false
SSH_AGENT_PID=6666
HOSTNAME=linuxbox
GPG_AGENT_INFO=/tmp/gpg-Pddt7g/S.gpg-agent:6689:1
SHELL=/bin/bash
TERM=xterm
XDG_MENU_PREFIX=kde-
HISTSIZE=1000
XDG_SESSION_COOKIE=6d7b05c650846c3eaf301b0046bd2b00-
120852190.996705-11756199
GTK2_RC_FILES=/etc/gtk-2.0/.gtkrc=/home/me/.gtkrc
2.0:/home/me/.kde/share/config/gtkrc-2.0
GTK_RC_FILES=/etc/gtk:/gtkrc:/home/me/.kde/share/config/gtkrc
GL_LIB=/home/me/.fonts
WINDOWID=2936016
QTDIR=/home/me/.fonts
EDITOR=/bin/xvim
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PS1=\u@\h:\w\$$
COLOR=/usr/bin/less -R
LANG=en_US.UTF-8
HOME=/home/me
PWD=/home/me
TERM=xterm
USER=me
```
