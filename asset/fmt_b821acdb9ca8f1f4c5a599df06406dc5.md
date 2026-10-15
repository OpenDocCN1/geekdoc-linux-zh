
此命令将停止用户 `bball` 发送到打印机 `mylp` 的所有打印作业。

### 使用 `lpr` 命令发送传真

如果你已经安装并配置了传真服务，`lpr` 命令也可用于发送传真，如第 11 章“配置调制解调器和传真服务”中的“配置传真服务”节。你必须首先确保 `efax` 软件包的传真服务运行正常。

使用 `lpr` 和 `elax` 发送传真

1. 以 `root` 操作员身份登录。
2. 使用你偏好的文本编辑器打开 `/etc/printcap` 数据库。

# 第一部分 Linux 基础

## 第5章 打印文件

- 3. 输入以下内容创建一个传真打印机条目：

```
lp=/dev/null:\nsd=/var/spool/fax:\nif=/usr/bin/faxlr
```

- 4. 使用如下所示 `ln` 命令为 `fax` 命令创建一个名为 `faxlpr` 的链接：

```bash
# /usr/bin/fax /usr/bin/faxlpr
```

- 5. 使用 `mkdir` 命令创建一个名为 `/var/spool/fax` 的目录，如下：

```bash
# mkdir /var/spool/fax
```

- 6. 使用 `chmod` 命令为传真目录赋予正确的权限，如下：

```bash
# chmod 770 /var/spool/fax
```

- 7. 若要发送传真，请使用 `-P`（打印机）和 `-J`（作业号）选项来指定传真打印机和传出的的传真号码，如下所示：

```bash
# lpr -Pfax -J 1650555212 myfax.txt
```

这将把文本文件 `myfax.txt` 发送到 `lpr` 命令命令行指定的传真号码。

# 另需参考

- ➤ 有关设置 `-fax` 服务的更多信息，请参阅第 161 页。

# 配置您的系统

- 配置您的环境 99
- 硬盘操作 113
- 添加磁带和 Zip 驱动器 129
- 启用 PC 卡设备 137
- 添加指针设备 147
- 配置调制解器和传真服务 153

# 第6章

## 配置您的环境

- 使用 `printenv` 命令显示环境变量
- 自定义您的登录
- 创建别名 (`aliases`)
- 使用 `linuxconf` 工具

# 第二部分 配置您的系统

## 第6章 配置您的环境

你在 `/etc/passwd` 条目中指定的 `shell` 在你登录 Linux 后运行。随后，你的 `shell` 会加载位于系统不同目录下的几个文件。这些文件被称为资源文件（`resource`）、配置文件（`profile`）或登录文件（`login files`），它们位于你的主目录和 `/etc` 目录。对于默认的 Linux `shell` —— `bash`，这些文件包括：

- `/etc/profile`—包含系统环境设置。这是 `shell` 登录时查找的第一个文件。该文件设置了环境变量，如用户在系统中的路径。
- `.bash_profile`, `.bash_login` 或 `.profile`—这些文件存在于你的主目录中，包含你账户本地的环境设置。`shell` 会按照列出的顺序查找这些文件。如果没有找到 `.bash_profile`，它会查找 `.bash_login`，然后查找 `.profile`。这些文件几乎相同，并且专门为该用户设置环境变量（如他们的路径）。
- `/etc/bashrc`—包含别名（`aliases`）。`shell` 在查看 `.bashrc` 之前会先查看这里。此文件中的信息适用于系统上的所有用户。
- `.bashrc`—位于你的主目录中，包含你账户本地的别名。更改 `.bashrc` 文件只会影响该文件的用户。这设置了特定于该用户的别名。
- `.bash_history`—最近进入的命令列表。

`profile` 文件包含环境变量，这些是在你登录后 `shell` 或其他程序识别的值的定义。`bash` 识别超过 50 种不同的环境变量，你也可以定义许多你自己的变量。

# 使用 `printenv` 命令显示环境变量

`printenv` 命令位于 `/usr/bin` 目录下，用于打印特定变量的值或当前定义的环境变量列表，如下所示：

```bash
$ printenv SHELL
/bin/bash

$ printenv
USERNAME=
ENV=/home/bball/.bashrc
BROWSER=/usr/local/bin/netscape
HISTSIZE=1000
HOSTNAME=localhost.localdomain
```

```bash
LOGNAME=bball
HISTFILESIZE=1000
MAIL=/var/spool/mail/bball
HOSTTYPE=i386
PATH=/usr/local/bin:/bin:/usr/bin::/usr/sbin:sbin:/usr/X11R6/bin:
usr/local/bin:/usr/bin/mh:/home/bball/bin
HOME=/root
SHELL=/bin/bash
USER=bball
HOSTDISPLAY=localhost.localdomain:0.0
DISPLAY=:0.0
NNTPServer=news.staffnet.com
SHLVL=5
EDITOR=/usr/bin/pico
```

这里列出的所有环境变量并不一定都会出现在你的系统中。许多系统具有不同的值（例如 `USER`、`ENV` 或 `HOSTNAME`）。一些常用的环境变量列在表 6.1 中。

# 表 6.1 常用的 bash 和用户环境变量

| 变量 | 描述 |
| --- | --- |
| `EDITOR` | 默认系统编辑器 |
| `HISTSIZE` | 记住命令行的数量 |
| `HOME` | 当前用户的主目录 |
| `HOSTTYPE` | 正在使用的系统架构 |
| `LOGNAME` | 当前用户名 |
| `MAIL` | 检查入站邮件的目录 |
| `OSTYPE` | 正在使用的操作系统 |
| `PATH` | 搜索命令的路径 |
| `PS1` | 命令行提示符的定义 |
| `PS2` | 二级命令行提示符中使用的字符 |
| `SHELL` | 当前使用的 shell 名称 |
| `SHLVL` | 当前运行的 shell 数量 |
| `TERM` | 正在使用的终端类型 |
| `USER` | 当前用户名 |

# 第二部分 配置您的系统

## 第6章 配置您的环境

# 使用 `env` 命令显示环境变量

你也可以使用 `env` 命令来打印你当前定义的环境变量列表，如下：

```bash
$ env
```

与 `printenv` 命令不同，`env` 会显示你所有的环境变量，而不仅仅是单个变量的值。

# 在命令行上设置环境变量

使用何种方法从命令行设置环境变量取决于所使用的 `shell`。`bash` `shell` 要求使用内置的 `export` 命令。环境变量在传统上使用大写字母命名，尽管这不是强制要求的。使用 `bash` 在命令行上创建变量的格式如下：

```bash
$ VARIABLE_NAME='value'; export VARIABLE_NAME
```

虽然你可以将其简写为形式：

```bash
$ export VARIABLE_NAME='value'
```

# 创建 `EDITOR` 变量

- 1. 若要创建或设置默认编辑器（许多系统实用程序使用），使用如下命令导出该变量：

```bash
$EDITOR='/usr/bin/emacs'; export EDITOR
```

- 2. 若要验证变量，使用如下所示的 `printenv` 命令：

```bash
$ printenv EDITOR
/usr/bin/emacs
```

`tsh` 需要使用内置的 `setenv` 命令：

```bash
# setenv VARIABLE_NAME=value
```

使用 `ksh` `shell` 定义变量需要使用内置的 `export` 命令：

```bash
# export VARIABLE_NAME=value
```

在任何 `shell` 中设置环境变量更方便的方法是使用 `env` 命令：

```bash
# env VARIABLE_NAME=value
```

# 第二部分 使用 `printenv` 命令显示环境变量 第6章

# 临时环境变量

从命令行设置的环境变量是临时的。虽然这种方法可能适用于测试新的软件或输入密码，但这些变量仅持续到你登录或运行特定的终端。要使此更改生效，请将定义添加到正确的 `shell` 初始化或资源文件中。更多信息请参阅后文“自定义您的登录”部分。环境变量在传统上使用大写字母命名，尽管这不是强制要求的。`tsh` 需要使用内置的 `setenv` 命令来定义变量：

```bash
> setenv VARIABLE_NAME=value
```

使用 `ksh` `shell` 定义变量需要使用内置的 `export` 命令：

```bash
$ export VARIABLE_NAME=value
```
