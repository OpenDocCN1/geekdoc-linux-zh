
![](img/0798d50a0e5dbf1265fbda3832b3e015_130_0.png)

通常情况下，你会看到发行版将其默认系统 shell（**sh**）通过软链接指向 Bash shell。以下是在 CentOS 发行版上的一个示例：

```
$ which sh
/usr/bin/sh
$ ls -l /usr/bin/sh
lrwxrwxrwx. 1 root root 4 Nov 8 11:30 /usr/bin/sh -> bash
$
```

然而，请注意，在某些发行版中，默认系统 shell 的链接方式不同，例如在这个 Ubuntu 发行版中：

```
$ which sh
/usr/bin/sh
$ ls -l /usr/bin/sh
lrwxrwxrwx 1 root root 4 Mar 10 18:43 /usr/bin/sh -> dash
$
```

在这种情况下，默认系统 shell `/usr/bin/sh` 指向的是专用的 Debian dash shell，而不是 Bash shell。

> **提示**
> 对于 Bash shell 脚本来说，这两种不同的 shell（默认交互式 shell 和默认系统 shell）可能会导致问题。请务必阅读第 11 章“基本脚本构建”中关于 Bash shell 脚本第一行所需的重要语法的说明，以避免这些问题。

你不必局限于使用默认的交互式 shell。只需输入其名称，即可启动你的发行版中可用的任何 shell。但是，系统不会显示任何隆重提示或消息来指示你当前正在使用什么 shell。不过，$0 变量可以提供帮助。`echo $0` 命令将显示当前 shell 的名称，提供所需的参考信息。

> **注意**
> `echo $0` 命令只有在 shell 提示符下执行时，才会显示当前正在使用的 shell。如果在 shell 脚本中使用，它会显示脚本的名称。这在第 14 章“处理用户输入”中有详细说明。

借助便捷的 $0 变量，你可以显示当前正在使用的 shell，通过输入 **dash** 命令启动 Dash shell，并再次通过 `echo $0` 显示新 shell 的名称：

```
$ echo $0
-bash
$
$ dash
$
$ echo $0
dash
$
```

在上面的示例中，请注意第一个 `$ echo $0` 命令返回的 **bash** 响应前面的短横线（–）。这表明该 shell 是用户的登录 shell。

`$` 提示符是 **Dash** shell 的 CLI 提示符。你可以通过输入 **exit** 命令离开 **Dash** shell 程序（就此而言，也可以离开 **Bash** shell）：

```
$ echo $0
dash
$ exit
$ echo $0
-bash
$
```

在各个 shell 之间来回切换看似简单，但幕后发生的动作更为复杂。为了说明这一过程，下一节将探讨登录 shell 程序与新启动的 shell 程序之间的关系。

## 探索父子 shell 关系

用户登录到虚拟控制台终端或在图形界面中启动终端模拟器时启动的默认交互式 shell（登录 shell）是一个*父 shell*。*正如你在本书中读到的一样，父 shell 进程提供 CLI 提示符并等待输入命令。*

当在 CLI 提示符下输入 **bash** 命令（或其他 shell 程序名称）时，会创建一个新的 shell 程序。这是一个*子 shell*。子 shell 也有 CLI 提示符，并等待输入命令。

由于你在输入 **bash** 并生成子 shell 时看不到任何相关消息，另一个命令可以帮助澄清情况。第 4 章“更多 Bash Shell 命令”中介绍了 **ps** 命令。在进入子 shell之前和之后使用带 `–f` 选项的该命令非常有用：

```
$ ps -f
  UID         PID   PPID C STIME TTY          TIME CMD
christi+  6160   6156  0 11:01 pts/1    00:00:00 -bash
christi+  7141   6160  0 12:51 pts/1    00:00:00 ps -f
$
$ bash
$
$ ps -f
  UID         PID   PPID C STIME TTY          TIME CMD
christi+  6160   6156  0 11:01 pts/1    00:00:00 -bash
christi+  7142   6160  0 12:52 pts/1    00:00:00 bash
christi+  7164   7142  0 12:52 pts/1    00:00:00 ps -f
$
```

**ps –f** 的第一次使用显示了两个进程。一个进程具有进程 ID 6160（第二列），正在运行 **Bash** shell 程序（最后一列）。第二个进程（进程 ID 7141）是实际正在运行的 **ps –f** 命令。

> **注意**
> 进程是正在运行的程序。Bash shell 是一个程序，当它运行时，它就是一个进程。正在运行的 shell 只是进程的一种类型。因此，在阅读关于运行 Bash shell 的内容时，你经常看到“shell”和“process”这两个词互换使用。

在上面的示例中，输入 `bash` 命令后，创建了一个子 shell。第二个 `ps -f` 是在子 shell 内部执行的。从这个显示中，你可以看到两个 Bash shell 程序正在运行。第一个 Bash shell 程序，即父 shell 进程，具有原始的进程 ID（PID）6160。第二个 Bash shell 程序，即子 shell 进程，具有 PID 7142。注意，子 shell 具有父进程 ID（PPID）6160，表示父 shell 进程是其父进程。图 5.1 图解了这一关系。

### 图 5.1
父子和子 Bash shell 进程。

![](img/0798d50a0e5dbf1265fbda3832b3e015_132_0.png)

当子 shell 进程被生成时，父进程的环境仅有一部分被复制到子 shell 环境中。这可能会导致诸如变量等问题。第 6 章“使用 Linux 环境变量”中涵盖了如何防止此类问题。

子 shell 可以由另一个子 shell 创建：

```
$ ps -f
UID        PID PPID C STIME TTY          TIME CMD
christia+  7650  7649 0 16:01 pts/0      00:00:00 -bash
christia+  7686  7650 0 16:02 pts/0      00:00:00 ps -f
$
$ bash
$ bash
$ bash
$
$ ps --forest
  PID TTY          TIME CMD
 7650 pts/0      00:00:00 bash
 7687 pts/0      00:00:00 \_ bash
 7709 pts/0      00:00:00 \_ \_ bash
 7731 pts/0      00:00:00 \_ \_ \_ bash
 7753 pts/0      00:00:00 \_ \_ \_ \_ ps
$
```

在之前的示例中，`bash` 命令被输入了三次。实际上，这创建了三个子 shell。`ps --forest` 命令显示了这些子 shell 的嵌套结构。图 5.2 也展示了这种子 shell 嵌套。

### 图 5.2
子 shell 嵌套。

![](img/0798d50a0e5dbf1265fbda3832b3e015_133_0.png)

`Bash` shell 程序可以使用命令行选项来修改 shell 的启动方式。表 5.1 列出了可用于 `bash` 命令的几个可用开关。

### 表 5.1 `bash` 命令行选项

| 选项 | 描述 |
| :--- | :--- |
| `-c` `string` | 从 `string` 读取命令并处理它们 |
| `-i` | 启动交互式 shell，允许用户输入 |
| `-l` | 表现得像是作为登录 shell 被调用 |
| `-r` | 启动受限 shell，将用户限制在默认目录 |
| `-s` | 从标准输入读取命令 |

通过输入 `man bash`，你可以找到有关 `bash` 命令的更多帮助，甚至更多的命令行参数。`bash -help` 命令也提供额外的帮助。

> **提示**
> 如果你想查看 Bash shell 的版本，只需在命令行输入 `bash --version`。这不会创建子 shell，而是显示你系统中 GNU Bash shell 程序的当前版本。

你可以通过输入 `exit` 命令优雅地退出子 shell。`exit` 命令不仅允许你离开子 shell，还可以让你注销当前虚拟控制台终端或终端仿真软件。只需在父 shell 中输入 `exit`，即可优雅地退出 CLI。

## 查看进程列表和子 shell

在一行中，你可以指定要依次运行的一系列命令。这是通过输入命令列表并在命令之间使用分号 (;) 来完成的：

```
$ pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my*
/home/christine
test_file test_one test_two
/etc
/home/christine
my_file my_scrap my_script my_scrpyt
$
```

在上面的示例中，所有命令都按顺序执行，没有任何问题。然而，虽然以这种方式使用命令被称为*列表*，但它并不是*进程列表*。要使命令列表被视为*进程列表*，命令必须用括号括起来：

```
$ (pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my*)
/home/christine
test_file test_one test_two
/etc
/home/christine
my_file my_scrap my_script my_scrpyt
$
```

虽然添加括号看起来可能不是很大的区别，但它们确实会产生非常不同的效果。添加括号并将命令列表转换为*进程列表*会创建一个*子 shell* 来执行命令。子 shell 是父 shell 的完整副本。与子 shell 不同，子 shell 包含父 shell 中设置的所有环境变量。

> **注意**
> 进程列表是一种*命令分组*类型。另一种命令分组类型将命令放在花括号之间，并用分号 (;) 结束命令列表。语法如下：`{ command; }`。使用花括号进行命令分组*不会*像进程列表那样创建子 shell。
