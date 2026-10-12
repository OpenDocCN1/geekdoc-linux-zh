
其他一些环境变量包括 `USER`、`PWD` 和 `HOME`，它们分别持有当前用户用户名、当前工作目录和主目录的值。

```
kali@kali:- echo $USER
kali
kali@kali:- echo $PWD
/home/kali
kali@kali:- echo $HOME
/home/kali
```

> 列表 29 - 使用 `echo` 显示 `USER`, `PWD` 和 `HOME` 环境变量

可以使用 `export` 命令定义环境变量。例如，如果我们正在扫描目标且不想重复输入系统的 IP 地址，可以快速为其赋值并使用：

```
kali@kali:-$ export b=10.11
```

```
kali@kali:-$ ping -c 3 b
PING 10.11 (10.11) 56(84) bytes of
64 bytes from 10.11: icmp_seq=1 ttl=62 time=23 ms
64 bytes from 10.11: icmp_seq=2 ttl=62 time=23 ms
64 bytes from 10.11: icmp_seq=3 ttl=62 time=56 ms

---
---
3 packets transmitted, 3 received, 0% packet loss, time 102ms
rtt min/avg/max/mdev = 23/34.0/56.0/16.5 ms
```

> `export` 命令使变量对我们从当前 shell 生成的所有进程可见。如果没有使用 `export` 设置变量，该变量将仅在当前 shell 中可用。我们将使用 `$$` 显示当前 shell 的进程 ID，以确保我们在不同的 shell 中执行命令：

```
kali@kali:-$ echo $$
1827
```

```
kali@kali:-$ var="My Var"
```

```
kali@kali:-$ echo $var
My Var
```

```
kali@kali:-$ bash
```

```
kali@kali:-$ echo $$
1908
```

```
kali@kali:-$ echo $var
My Var
```

```
kali@kali:-$ exit
```

```
kali@kali:-$ export othervar="Global Var"
```

```
kali@kali:-$ echo othervar
Global Var
```

```
kali@kali:-$ bash
```

```
kali@kali:-$ echo othervar
Global Var
```

```
kali@kali:-$ exit
```

> 列表 31 - 使用 `export` 声明变量

Kali Linux 中默认定义了许多环境变量。我们可以通过命令行运行 `env` 来查看这些变量：

```
SHELL=/bin/bash
PWD=/home/kali
XDG_DESKTOP=lightdm-session
LOGNAME=kali
XDG_SESSION_TYPE=x11
AUTHORITY=/home/kali/.Xauthority
XDG_RUNTIME_DIR=/var/lib/lightdm/kali
HOME=/home/kali
...
TERM=xterm-256color
USER=kali
```

> 列表 32 - 使用 `env` 显示所有环境变量

## 补全

Bash 自动补全功能允许我们使用 Tab 键补全文件名和目录路径。这一功能加速了 shell 的使用，而在其他 shell 中是缺失的。让我们从用户主目录看看它是如何工作的。我们将输入以下命令开始：

```
ls Desktop/ Downloads/
ls Desktop/
ls Desktop/
```

> 列表 33 - 在 Bash 中演示 Tab 补全

当我们在 "D" 之后第一次按下 Tab 键时，bash shell 会建议三个以该字符开头的目录，然后向我们展示部分完成的命令以便我们继续。由于我们指定了 "Desktop"，我们继续输入 "e" 然后再次按下 Tab 键。此时，bash 会自动补全 "Desktop" 的剩余部分，因为它是唯一以 "De" 开头的。关于 Tab 补全更多信息可以在 Debian 网站上找到。

### 3.1.3 Bash 历史

在渗透测试期间，记录输入 shell 的命令是非常重要的。幸运的是，Bash 维护了已输入命令的历史，可以使用 `history` 命令显示。

```
kali@kali:-$ history
1 cat /etc/lsb-release
2 clear
3 history
```

> 列表 34 - `history` 命令

与其从历史记录中重新输入长命令，我们可以利用历史扩展功能。例如，回看列表 34，历史记录中有三个命令，每个命令前面都有行号。要重新运行第一个命令，我们只需输入 `!` 后跟行号（在本例中为 1），即可执行 `cat /etc/lsb-release` 命令：

```
kali@kali:-$ !1
cat /etc/lsb-release
DISTRIB_ID=Kali
DISTRIB_RELEASE=kali-rolling
DISTRIB_COAME=kali-rolling
DISTRIB_DESCRIPTION="Kali GNU/Linux Rolling"
```

> 列表 35 - 历史扩展的应用

另一个有快捷键是 `!!`，它重复我们在终端会话期间执行的上一个命令：

```
kali@kali:- sudo systemctl restart apache2
kali@kali:- !!
sudo systemctl restart apache2
kali@kali:-$
```

> 列表 36 - 轻松重复上一个命令

默认情况下，命令历史保存到用户主目录。环境变量 `bash_history` 控制命令历史的大小：`HISTSIZE` 和 `HISTFILE`。

`HISTSIZE` 控制存储在当前会话内存中的命令数量，`HISTFILE` 配置历史文件中保留的命令数量。这些变量可以根据需要进行编辑，并保存到稍后我们将探索的 Bash 配置文件 `.bashrc` 中。

探索 Bash 历史最简单的方法之一直接通过命令行提示符。我们可以通过两种最常用的方法浏览历史记录：

- 向后滚动历史

- 向前滚动历史

最后但同样重要的，按下 `Ctrl+R` 将调用反向搜索功能。输入一个字母，例如 c，你将获得历史中包含字母 "c" 的最新命令的匹配项。继续输入以缩小搜索范围，当找到所需的命令时，按回车键执行它。

## 3.1.2 练习

- 检查你的 bash 历史记录，并使用历史扩展（history expansion）重新运行其中的命令。

- 执行你选择的命令，并尝试通过快捷键以及反向搜索功能（reverse-i search）浏览历史。

## 3.2 管道与重定向

命令行执行的每个程序都连接着三个数据流，作为与外部环境通信的通道。这些流定义如下：

| 流名称 | 描述 |

|---|---|

| 标准输入 (`STDIN`) | 输入到程序的数据 |

| 标准输出 (`STDOUT`) | 程序的输出（默认到终端） |

| 标准错误 (`STDERR`) | 错误信息（默认到终端） |

管道（使用 `|`）和重定向（使用 `<` 和 `>` 运算符）将程序和文件之间的流连接起来，以适应近乎无限可能的场景。

## 3.2.1 重定向到新文件

在之前的命令示例中，输出是打印在屏幕上的。这很方便，但我们可以使用 `>` 运算符将输出保存到文件中，以便日后参考或处理：

```
kali@:- ls
Desktop Documents Downloads Pictures Public Templates Videos
kali@:- echo "test"
test
kali@:- echo "test" > redirection_test.txt
kali@:- ls
Desktop Documents Downloads Pictures Public redirection_test.txt Template
kali@:- cat redirection_test.txt
test
kali@:- echo "Kali Linux is an open source project" > redirection_test.txt
kali@:- cat redirection_test.txt
Kali Linux is an open source project
```

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

如列表 38 所示，如果我们将输出重定向到一个不存在的文件，该文件将被自动创建。然而，如果我们输出输出到一个已经存在的文件，该文件的内容将被替换。请小心重定向！没有撤销功能。

## 3.2.2 重定向到现有文件

要向文件追加额外数据（而不是覆盖文件），请使用 `>>` 运算符：
