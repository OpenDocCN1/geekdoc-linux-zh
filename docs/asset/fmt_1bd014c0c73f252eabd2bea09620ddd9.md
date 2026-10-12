
```
ps -u username
```

列出系统中运行的所有进程，使用：

```
ps aux
```

### 终止进程

要杀死一个进程，你需要它的进程 ID (PID)。你可以使用 `ps` 找到 PID。一旦有了 PID，使用：

```
kill PID
```

要强制停止进程，请使用 `-9` 标记：

```
kill -9 PID
```

### 更改优先级

要以特定优先级启动进程，使用 `nice`：

```
nice -n 10 command
```

要更改运行进程的优先级，使用 `renice`：

```
renice +5 PID
```

## 练习 1

目标：

理解前台作业（foreground job）的工作原理

### 1. 创建 shell 脚本

首先，让我们创建一个处理时间较长的 shell 脚本。下面的 shell 脚本（`loop.sh` 文件）将从 1,000,000 开始倒数。

使用 `vim` 创建一个名为 `loop.sh` 的 shell 脚本。

命令行 - 输入

```
ubuntuip-172-26-0-53:- | mkdir dir_ch8
ubuntuip-172-26-0-53:- | cd dir_ch8
ubuntuip-172-26-0-53:- | vim loop.sh
```

按下 `i` 键切换到插入模式。接下来，复制下面的代码并粘贴到文件中。粘贴代码后，按下 `esc` 键，接着按下 `:` 键，并按 `w + q` 键保存文件。要学习如何使用 Vim，请查看第 3 章 Vim 编辑器。

`loop.sh`

```bash
#!/bin/bash
count=5000000
while [ $count -ge 0 ]
do
  echo "countdown $count"
  count=$((count - 1))
done
```

### 2. 运行 shell 脚本

要运行 shell 脚本，请调整访问模式并使用文件路径运行脚本。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:$ | sudo chmod+x loop.sh
ubuntu@ip-172-26-0-53:$ | ./loop.sh
```

当你将其作为前台作业运行时，你将在终端上看到倒数。在倒数完成之前，你的命令行会被占用，你无法创建另一个作业。

命令行 - 响应

```
:countdown 920071
countdown 920070
countdown 920069
:
```

要挂起或停止作业，请按下 `Ctrl + Z` 或 `Ctrl + C`。

即使你将标准输出重定向到文本文件，该作业仍然作为前台作业运行，你无法创建另一个作业。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:$ | ./loop.sh > countdown.txt
```

## 后台作业（Background Job）

由于在前台作业运行时你无法创建新作业，如果一个程序需要很长的过程，将其作为后台作业运行是比较好的。你可以同时运行多个后台作业，因为它们在后台运行。要启动后台作业，请在命令末尾带有 `&` 运行命令。

## 练习 2

目标：

理解后台作业的工作原理

### 1. 多次作为后台作业运行 shell 脚本

运行 `loop.sh` 文件并将其重定向到文本文件，并在末尾加上 `&`。命令行会给你一个数字，即作业的 ID。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:-$ | ./loop.sh > countdown_bg_1.txt &
```

命令行 - 响应

```
[2] 83447
```

你也可以多次执行相同的命令。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:-$ | ./loop.sh > countdown_bg_2.txt &
```

命令行 - 响应

```
[3] 83450
```

命令行 - 输入

```
ubuntu@ip-172-26-0-53:-$ | ./loop.sh > countdown_bg_3.txt &
```

命令行 - 响应

```
[4] 83451
```

### 2. 检查作业状态

要查看运行中的作业，请运行 `jobs` 命令，将在下一节中解释。你可以看到多个作业正在并行运行。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:~$ jobs
```

命令行 - 响应

| | |
| :--- | :--- |
| [1] Running | countdown_bg_1.txt & /loop.sh > |
| [2]- Running | countdown_bg_2.txt & /loop.sh > |
| [3]+ Running | countdown_bg_3.txt & /loop.sh > |

### `jobs` 和 `ps` (显示作业与进程)

![](img/87e31443ff747018655a0f4f95ee6187_311_0.png)

- 显示当前作业（带有 `-l` 选项，显示进程 ID）
- 显示当前进程（带有 `-e` 选项，显示所有进程）

`jobs` 命令用于检查运行中的作业，而 `ps` 命令用于检查运行中的进程。

## 检查运行中的作业 - `jobs`

`jobs` 命令显示作业 ID、每个作业的状态（运行、停止、完成、终止）以及作业名称。作业数字后还有 `+` 或 `-` 符号。`-` 指当前作业，`+` 指上一个作业。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:~$$ jobs
```

命令行 - 响应

| | | |
| :--- | :--- | :--- |
| [1] Running | /loop.sh > countdown_bg.txt & |
| [2]+ Stopped | /loop.sh > countdown_bg.txt |
| [3] Running | /loop.sh > countdown_bg.txt & |
| [4]- Running | /loop.sh > countdown_bg.txt & |

### `-l` 选项

如果你想显示进程号，请使用 `-l` 选项。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:-$ | jobs -l
```

命令行 - 响应

| | | | |
| :--- | :--- | :--- | :--- |
| [1] | 85945 | Running | /loop.sh > countdown_bg.txt |
| [2]+ | 85946 | Stopped | /loop.sh > countdown_bg.txt |
| [3] | 85947 | Running | /loop.sh > countdown_bg.txt |
| [4]- | 85949 | Running | /loop.sh > countdown_bg.txt |

## 检查运行中的进程 - `ps`

`ps` 命令显示由终端启动的进程。进程信息包括 PID（进程 ID）、TTY（终端名称）、TIME（运行时间）和 CMD（命令名称）。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:-$ ps
```

命令行 - 响应

| PID | TTY | TIME | CMD |
| :--- | :--- | :--- | :--- |
| 85871 | pts/2 | 00:00:00 | bash |
| 85945 | pts/2 | 00:00:41 | loop.sh |
| 85946 | pts/2 | 00:00:11 | loop.sh |
| 85947 | pts/2 | 00:00:22 | loop.sh |
| 85949 | pts/2 | 00:00:11 | loop.sh |
| 85950 | pts/2 | 00:00:00 | ps |

### `-e` 选项

`ps` 命令显示你的终端启动的运行进程。它不会显示计算机上运行的所有进程。例如，由本身或其他终端启动的进程不会显示。要显示计算机上运行的所有进程，请使用 `-e` 选项。

命令行 - 输入

```
ubuntu@ip-172-26-0-53:~ | ps -e
```

命令行 - 响应

| PID | TTY | TIME | CMD |
| :--- | :--- | :--- | :--- |
| 85871 | pts/2 | 00:00:00 | bash |
| 1 | ? | | systemd |
| 85945 | pts/2 | 00:00:41 | loop.sh |
| 85946 | pts/2 | 00:00:11 | loop.sh |
| 85947 | pts/2 | 00:00:22 | loop.sh |
| 85949 | pts/2 | 00:00:11 | loop.sh |
