
结果 系统将提示你为用户 `tidus` 设置新密码。

CLI 显示 `[root@centos:/]# password tidus`

`New password:`

`Retype new password:`

`passwd: all tokens updated successfully`

好了，现在我们已经设置好了 `tidus`，但仍然需要授予他 `sudo` 权限。我们只对可能需要增加安全权限的用户执行此操作。首先，我们需要打开 `sudoers` 配置文件进行修改。我们可以通过使用 `visudo` 命令来实现这一点。

## 给用户授予 sudo 权限

命令 `visudo`

结果 系统将打开 `sudoers` 文件。

```
[root@centos:/]# visudo
## This file MUST be edited with the ‘visudo’ command as root.
#
#
Note: 使用方向方向键向下滚动文档
#
#Allow root to run any commands anywh..
root ALL=(ALL) ALL
```

此文件中有很多文本，但不要被吓到。在上面的表格中，我向下移动箭头直到找到高亮部分：`root ALL=(ALL) ALL`。

在该选择下方，我们需要添加以下内容：

`tidus ALL=(ALL) ALL`

在 `visudo` 中，你始终处于两种模式之一：命令模式或插入模式。按 `I` 插入文本，按 `ESC` 返回命令模式。

一直按向下键直到进入 `root` 下方的空白区域。在那里按 `I` 并输入 `tidus`，按 `Tab` 键，输入 `ALL=(ALL)`，按 `Tab` 键并输入 `ALL`。现在按 `ESC` 键输入 `:w` 然后按回车保存。

现在可以松口气了。我知道我们进展得有点快，但开始使用比 `root` 之外的用户 ID 是重要的。同时，我们能够能够安装软件并学习更多知识也很重要，所以这是必须的。

在继续之前，我们可以学习两个快速命令。现在你的 CLI 上可能有很多文本。如果你想清理掉它们，可以使用 `clear` 命令。

| 命令 | `clear` |
| :--- | :--- |
| 结果 | 系统将清除屏幕 |
| CLI 显示 | `[root@centos:/]# clear` |

现在屏幕是清洁的，如果你在使用 VPS，就可以关闭 PuTTY 了。如果你在使用虚拟机，请执行 `logout`。我们将继续使用新用户 ID `tidus` 操作。

| 注销 |  |
| :--- | :--- |
| 命令 | `logout` |
| 结果 | 系统将关闭 SSH 会话并退出 PuTTY 或注销虚拟机 |
| CLI 显示 | `[root@centos:/]# logout` |

## 快速回顾

- 1) 我们应该避免使用“root”用户，这是一个良好的使用习惯。
- 2) 在命令前加上 `sudo` 允许用户拥有超级用户权限。
- 3) 我们可以使用命令 `adduser` 加上用户名来添加用户。
  1. 示例：`adduser nathan`
- 4) 我们可以通过在用户名名前使用 `passwd` 命令更改用户密码。
  1. 示例：`passwd nathan`
- 5) 要获得使用 `sudo` 的权限，用户必须先被添加到配置文件中，该文件可以通过使用 `visudo` 命令进行编辑。
- 6) 如果我们的 CLI 变得太乱，可以使用 `clear` 命令将其清空。
- 7) 要结束会话并注销，我们可以使用 `logout`。

# 第 7 章

## 系统状态概览

使用我们在上一章中创建的新用户登录你的服务器。从现在开始，在本书的剩余部分，我们将不再使用 `root` 用户 ID。

让我们来看一些设置，看看我们的服务器运行如何。

首先，我们可以查看 `uptime` 系统。这在系统管理中非常有用。它可以让你知道服务器已经运行了多久，有多少用户登录以及平均系统负载。

### 检查运行时间

| 命令 | `uptime` |
| :--- | :--- |
| 结果 | 系统将显示运行时间和平均负载数据 |
| CLI 显示 | `[tidus@centos~]$` |

接下来，我们可以通过使用 `top` 命令查看哪些进程正在占用系统最多的内存。如果你的系统运行缓慢，这有助于查看是什么在占用系统资源。

前几行将提供你系统资源利用情况的摘要，并可以按 CPU 或内存使用情况对进程列表进行排序，让你能够快速看到服务器资源需求最大的点在哪里。

| 命令 | `top` |
| :--- | :--- |
| 结果 | 系统将显示占用最多 CPU 资源的进程 |
| CLI 显示 | `[tidus@centos~]$ top` |

退出 `top` 请按 `control + c`。

要检查系统的内存资源，我们可以使用 `vmstat` 命令。

| 检查内存使用 |  |
| :--- | :--- |
| 命令 | `vmstat` |
| 结果 | 系统将显示空闲和使用的内存量 |
| CLI 显示 | `[tidus@centos~]$ vmstat` |

随着你变得越来越熟练，通过 `vmstat` 和 `top`，你能够在出现问题时确定哪些脚本或程序耗尽资源。在较大的环境中，你可能想查看哪些用户登录了服务器。使用 `w` 命令可以为我们提供这些信息。

| 检查内存使用 |  |
| :--- | :--- |
| 命令 | `w` |
| 结果 | 系统将显示服务器上的用户 |
| CLI 显示 | `[tidus@centos~]# w` |

## 导航、创建目录和文件

部分将是对前面章节的复习，但这种重复对于记忆日常使用中用到的命令非常重要。现在我们已经登录，使用 `pwd` 命令查看我们当前的目录。

| 查找你的当前目录位置 |  |
| :--- | :--- |
| 结果 | 系统将输出你所在的目录。 |
| CLI 显示 | `[tidus@centos~]$pwd` |
|  | `/home/tidus` |

注意，我们的目录时间与使用 `root` 用户登录时不同。上次我们在 `/root`，那是 `root` 的主目录。现在在 `/home/tidus`，这是用户 `tidus` 的主目录。

**提示：** 如果你随时需要返回主目录，使用 `cd` 回到你的主文件夹。

现在我们已经在主文件夹中了，让我们创建一个名为 `documents` 的新目录。

| 创建新目录 |  |
| :--- | :--- |
| 命令 | `mkdir documents` |
| 结果 | 系统将创建一个名为 `documents` 的子目录 |
| CLI 显示 | `[tidus@centos~]$ mkdir documents` |
|  | `[tidus@centos~]$` |

使用 `ls` 命令列出我们主目录的内容，看看 `documents` 目录是否存在。

| 列出文件 |  |
| 命令 | `ls` |
| Result | 列出当前目录下的文件 |
| CLI Display | [tidus@centos:~]# ls documents |

通过使用 `ls`，我们现在看到在 `documents` 目录之外，我们的目录是空的。

让我们利用之前章节中学到的知识来练习导航技能，并进入 `documents` 目录。

尝试使用命令：`cd Documents`

你可能会注意到它返回了‘cd: Documents: No such file or directory.’。Linux 是区分字母大小的，这意味着‘Documents’ 和 ‘documents’ 是两个不同的东西。在使用 CentOS 时你需要记住这一点，因为使用正确的大小至关重要。

现在，让我们用正确的方法来。

### 切换到子目录

| Command | `cd documents` |
| Result | 切换到 `documents` 目录 |
| CLI Display | [tidus@centos:~]$ cd documents [tidus@centos: documents]$ |

使用 `ls` 命令列出目录中的文件，你会发现它是空的。现在让我们使用 `cd` 回到主目录。

### 切换到用户主目录

| Command | `cd` |
| Result | 切换到用户主目录 |
| CLI Display | [tidus@centos: documents]$ cd [tidus@centos:~]$ |

如果我们使用 `pwd`，将发现我们回到了 `/home/tidus`。

现在，使用 `documents` 目录的完整路径来执行 `cd`。记住，Linux 是区分字母大小的。

### 使用全路径切换目录

| Command | `cd /home/tidus/documents` |
| Result | 切换到指定目录 |
| CLI | [tidus@centos:~]$ cd /home/tidus/documents\n[tidus@centos: documents]$ |
