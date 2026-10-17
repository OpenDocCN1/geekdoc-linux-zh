
```
export MY_VARIABLE=my_value
```

以下是通过命令行在 Linux “用户环境”部分使用的主要命令（见表 3.12）。

表 3.12 – Linux 中“用户环境”部分的命令

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `whoami` | 返回当前用户名 | 无 | `whoami` |
| `hostname` | 返回主机名 | 无 | `hostname` |
| `echo` | 在屏幕上显示消息或将其保存到文件 | `-n` – 不输出最后的换行符, `-e` – 解释转义序列, `-E` – 不解释转义序列 | `echo "Hello, World!"`, `echo -n "Hello, World!" >` |
| `export` | 设置环境变量的值 | 无 | `export MY_VAR="Hello"` |
| `env` | 列出所有环境变量 | 无 | `env` |
| `alias` | 为另一个命令创建别名 | 无 | `alias ll="ls -al"` |
| `source` | 在当前环境中运行脚本 | 无 | `source myscript.sh` |
| `su` | 切换到另一个用户 | - | `su username` |

## 逐步进阶 Linux：三合为一

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `su` | 输入该用户的密码 | | |
| `sudo` | 允许用户以另一个用户（通常是 `root`）身份运行命令 | | `sudo command` |
| `date` | 显示或设置系统的当前日期时间 | | `date`, `date +%format` |
| `uname` | 显示系统信息，包括内核名称、版本、硬件平台 | | `uname` |
| `uptime` | 显示系统运行时间、平均负载 | | `uptime` |
| `sleep` | 按指定的秒数延迟命令执行 | | `sleep 5` |
| `yes` | 重复指定的字符串 `"y"` | | `"hello"` |
| `bash` | `Bash` shell 路径 | 无选项 | `echo $BASH` |
| `PATH` | 系统查找可执行文件的路径 | 冒号分隔的目录 | `echo $PATH` |
| `HOME` | 用户的家目录 | 无选项 | `echo $HOME` |

## 第三章：Linux 命令行操作

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `LANG` | 指定用户的语言和区域设置 | 语言代码 | `echo $LANG` |
| `PS1` | 指定提示符 | 格式字符串 | `export PS1='\u@h:\$'` |
| `PS2` | 指定二级提示符（输入命令时使用） | 格式字符串 | `export PS2='> '` |
| `HISTSIZE` | 指定历史文件中存储命令的数量 | 命令数量 | `export HISTSIZE=1000` |
| `HISTFILESIZE` | 指定历史文件的最大大小 | 字节 | `export HISTFILESIZE=1000` |

### III.2.10 获取系统各种信息的命令

Linux 是全球流行的操作系统之一。它对开发者开放，更加灵活且可定制。Linux 命令行是一个强大的工具，允许用户获取系统及其组件的信息。通过使用命令行，你还可以了解 CPU 使用率、内存、磁盘空间、网络接口等重要设置。在本节中，我们将查看一些命令（见表 3.13），这些命令可以帮助我们通过命令行获取 Linux 系统的信息。

Linux 命令行提供了许多获取系统及其组件信息的命令。

# 表 3.13 - 获取 Linux 系统各种信息的命令

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `uname` | 返回系统信息 | `-a`: 返回所有选项, `-r`: 返回内核版本, `-s`: 返回操作系统名称 | `uname -a` |
| `top` | 显示运行进程和系统资源 | `q`: 退出命令, `k`: 结束进程, `u`: 显示用户进程 | `top -u username` |
| `free` | 显示内存使用情况 | `-m`: 以 MB 为单位返回, `-g`: 以 GB 为单位返回 | `free -m` |
| `df` | 显示磁盘空间使用 | `-h`: 以人类格式返回, `-T`: 返回文件系统类型 | `df -h` |
| `ifconfig` | 显示网络接口信息 | `-a`: 返回所有接口, `-s`: 返回摘要信息 | `ifconfig`, `ifconfig -a` |
| `ip` | 显示网络接口信息 | `-s`: 返回摘要信息, `-4`: 仅返回 IPv4 地址信息 | `ip`, `-s`, `ip -4 address` |
| `ps` | 显示运行进程 | `ax`: 返回所有用户的进程信息, `-u username`: | `ps ax`, `ps -u username` |

## 第三章：Linux 命令行中的常用命令

| 命令 | 说明 | 重要参数 | 示例 |
|---|---|---|---|
| `du` | 显示文件和目录的磁盘空间占用 | `-h`: 以易读的格式返回结果，`-s`: 返回指定目录的总大小 | `du -h` |
| `fdisk` | 管理磁盘分区 | `-l`: 列出所有磁盘分区，`-p`: 以紧凑格式列出分区表 | `sudo fdisk -l`, `sudo fdisk -p /dev/sda` |
| `lsb_release` | 返回已发布的 Linux 发行版信息 | `-a`: 返回所有选项 | `lsb_release -a` |
| `os-release` | 返回已发布的 Linux 发行版信息 | 无选项 | `cat /etc/os-release` |
| `hostnamectl` | 提供主机名及其设置信息 | `status`: 返回当前主机设置，`set-hostname`: 修改主机名 | `hostnamectl status`, `sudo hostnamectl set-hostname` |
| `hostname` | 返回系统主机名 | 无选项 | `hostname` |

在处理磁盘分区时，`fdisk` 命令非常有用，而 `lsb_release` 和 `os-release` 可以帮助确定 Linux 发行版版本。`hostnamectl` 和 `hostname` 命令可获取主机名信息并更改其设置。这些命令只是 Linux 命令行功能的一小部分，在操作系统时非常有用。

## III.2.11 管理 Linux 软件包的基本命令

Linux 比其他操作系统有许多优势，其中之一就是包管理。包管理是在 Linux 上安装、更新和删除软件包的过程。Linux 中的包管理系统存在是为了简化安装和更新程序的过程，并确保系统的安全稳定。

Linux 有多个包管理器，每个都有自己的特性和优点。在本节中，我们将查看几个 Linux 包管理器及其特性以及如何通过命令行安装它们。具体的参数和命令使用示例可能会根据 Linux 发行版和包管理器版本略有不同。以下是（见表 3.14）一些管理 Linux 软件包的命令。

表 3.14 – 管理 Linux 软件包的命令

| 命令 | 说明 | 重要参数 | 示例 |
|---|---|---|---|
| `apt-get` | Debian 及其衍生发行版的包管理 | `install`, `remove`, `update`, `upgrade`, `search` | `sudo apt-get install package_name`, `sudo apt-get remove package_name` |
| `aptitude` | Debian 及其衍生发行版的文本界面包管理器 | `install`, `remove`, `update`, `upgrade`, `search` | `sudo aptitude install package_name`, `sudo aptitude remove package_name` |
| `yum` | CentOS、Fedora 及其他使用 RPM 包发行版的包管理 | `install`, `remove`, `update`, `upgrade`, `search` | `sudo yum install package_name`, `sudo yum remove package_name` |
| `dnf` | Fedora 及其他使用 RPM 包发行版的包管理 | `install`, `remove`, `update`, `upgrade`, `search` | `sudo dnf install package_name`, `sudo dnf remove package_name` |
| `pacman` | Arch Linux 及其衍生发行版的包管理 | `-S` (安装), `-Rs` (删除) | `sudo pacman -S package_name`, `sudo pacman -Rs package_name` |
