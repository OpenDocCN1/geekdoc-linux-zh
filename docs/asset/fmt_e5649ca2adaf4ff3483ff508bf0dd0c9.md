
要找到正在运行的任务的任务号，请列出你的任务（参见 Recipe 3.3.4 [列出你的任务]，第 42 页）。

以下章节描述了管理任务的各种命令。

### 3.3.1 挂起任务

输入 `C-z` 来挂起或停止前台任务——当在 shell 中做其他事情并在稍后返回当前任务时有用。任务将停止，直到你将其带回前台或让它在后台运行（参见 Recipe 3.3.3 [将任务放入前台]，第 42 页和参见 Recipe 3.3.2 [将任务放入后台]，第 41 页）。

例如，如果你正在 `info` 中阅读文档，输入 `C-z` 将挂起 `info` 程序并返回到 shell 提示符，你可以在那里做其他事情（参见 Recipe 2.8.5 [使用 GNU Info 系统]，第 31 页）。shell 会输出一行给出任务的任务号（括号内）、指示任务已停止的文本 'Stopped' 以及命令本身，如下所示：

```
[1]+ Stopped    info -f cookbook.info
```

在此示例中，任务号是 1，停止的命令是 'info -f cookbook.info'。任务号旁边的 '+' 字符表示这是最近的任务。

如果你在注销时有挂起的任务，shell 会提示你而不是直接注销：

```
$ logout RET
There are stopped jobs.
$
```

此时，你可以列出你的任务（参见 Recipe 3.3.4 [列出你的任务]，第 42 页），停止任何正在运行的任务（参见 Recipe 3.3.5 [挂起任务]，第 43 页），然后注销。

### 3.3.2 将任务放入后台

除非另有指定，否则新任务会在前台运行。要在后台运行任务，请在输入行末尾加上和符号（'&'）。这对于运行执行大量计算的非交互式程序有用。

- 要将命令 `apropos shell > shell-commands` 作为后台任务运行，输入：

```
$ apropos shell > shell-commands & RET
[1] 6575
$
```

shell 会输出任务号（在此处为 1）和进程 ID（在此处为 6575），然后返回 shell 提示符。当后台任务完成后，shell 将列出任务号、命令和文本 'Done'，表示任务已成功完成：

Linux 烹饪之道：日常使用的技巧与技术

[1]+ Done apropos shell >shell-commands

要将任务从前台移动到后台，首先要挂起它（参见 Recipe 3.3.1 [挂起任务]，第 41 页）并输入 `bg`（代表“background”的缩写）。

- 例如，要在前台启动命令 `apropos shell > shell-commands`，先挂起它，然后指定其在后台运行，你将输入：

```
$ apropos shell > shell-commands RET
C-z

[1]+ Stopped apropos shell >shell-commands
$ bg RET
[1]+ apropos shell &
$
```

如果你挂起了多个任务，通过提供其任务号作为参数来指定要放入后台的任务。

- 要在后台运行任务 4，输入：

$ bg %4 RET

注意：在后台运行任务有时被称为“backgrounding”或对任务进行“amping off”（后台化）。

### 3.3.3 将任务放入前台

输入 `fg` 将任务移动到前台。默认情况下，`fg` 作用于最近的后台任务。

- 将最近的后台任务带回前台，输入：

  $ fg RET

当后台有多个任务时，要将特定任务移回前台，指定任务号作为 `fg` 的选项。

- 要将任务 3 带回前台，输入：

  $ fg %3 RET

### 3.3.4 列出你的任务

要列出当前 shell 中运行的任务，输入 `jobs`。

- 列出你的任务，输入：

```
$ jobs RET apropos shell >shell-commands
[1]- Stopped apropos shell >bash-commands
[2]+ Stopped apropos shell >bash-commands
```

第 3 章：Shell

列出当前 shell 中运行的任务，输入 `jobs`。

此示例显示了任务。任务号旁边的 '+' 字符表示这是最近的任务，'-' 字符表示它是之前的任务。如果你没有运行的任务，`jobs` 将什么都不返回。

列出 shell 中运行的任务，输入 `jobs`。

- 列出你的任务，输入：

```
$ jobs RET apropos shell >shell-commands
[1]- Stopped apropos shell >bash-commands
[2]+ Stopped apropos shell >bash-commands
```

第 3 章：Shell

此示例显示了任务。任务号旁边的 '+' 字符表示这是最近的任务，'-' 字符表示它是之前的任务。如果你没有运行的任务，`jobs` 将什么都不返回。

列出 shell 中运行的任务，输入 `jobs`。参见 2.7 [系统活动]，第 26 页。

### 3.3.5 停止任务

输入 `C-z` 挂起前台任务——当你想在 shell 中做其他事情并在稍后返回当前任务时有用。任务将停止，直到你将其带回前台或让它在后台运行（参见 Recipe 3.3.3 [将任务放入前台]，第 42 页和参见 Recipe 3.3.2 [将任务放入后台]，第 41 页）。

例如，如果你正在 `info` 中阅读文档，输入 `C-z` 将挂起 `info` 程序并返回到 shell 提示符，你可以在那里做其他事情（参见 Recipe 2.8.5 [使用 GNU Info 系统]，第 31 页）。shell 会输出一行给出任务的任务号（括号内）、指示任务已停止的文本 'Stopped' 以及命令本身，如下所示：

```
[1]+ Stopped    info -f cookbook.info
```

在此示例中，任务号是 1，停止的命令是 'info -f cookbook.info'。任务号旁边的 '+' 字符表示这是最近的任务。

如果你在注销时有挂起的任务，shell 会提示你而不是直接注销：

```
$ logout RET
There are stopped jobs.
$
```

此时，你可以列出你的任务（参见 Recipe 3.3.4 [列出你的任务]，第 42 页），停止任何正在运行的任务（参见 Recipe 3.3.5 [挂起任务]，第 43 页），然后注销。

### 3.3.2 将任务放入后台

新任务会在前台运行，除非另有指定。要在后台运行任务，请在输入行末尾加上和符号（'&'）。这有对于运行执行大量计算的非交互式程序有用。

- 要将命令 `apropos shell > shell-commands` 作为后台任务运行，输入：

```
$ apropos shell > shell-commands & RET
[1] 6575
$
```

shell 会输出任务号（在此处为 1）和进程 ID（在此处为 6575），然后返回 shell 提示符。当后台任务完成后，shell 将列出任务号、命令和文本 'Done'，表示任务已成功完成：

Linux 烹饪之道：日常使用的技巧与技术

[1]+ Done apropos shell >shell-commands

要将任务从前台移动到后台，首先要挂起它（参见 Recipe 3.3.1 [挂起任务]，第 41 页）并输入 `bg`（代表“background”的缩写）。

- 例如，要在前台启动命令 `apropos shell > shell-commands`，先挂起它，然后指定其在后台运行，你将输入：

```
$ apropos shell > shell-commands RET
C-z

[1]+ Stopped apropos shell >shell-commands
$ bg RET
[1]+ apropos shell &
$
```

如果你挂起了多个任务，通过提供其任务号作为参数来指定要放入后台的任务。

- 要在后台运行任务 4，输入：

$ bg %4 RET

注意：在后台运行任务有时被称为“backgrounding”或对任务进行“amping off”（后台化）。

### 3.3.3 将任务放入前台

输入 `fg` 将任务移动到前台。默认情况下，`fg` 作用于最近的后台任务。

- 将最近的后台任务带回前台，输入：

  $ fg RET

当后台有多个任务时，要将特定任务移回前台，指定任务号作为 `fg` 的选项。

- 要将任务 3 带回前台，输入：

  $ fg %3 RET

### 3.3.4 列出你的任务

要列出当前 shell 中运行的任务，输入 `jobs`。

- 列出你的任务，输入：

```
$ jobs RET apropos shell >shell-commands
[1]- Stopped apropos shell >bash-commands
[2]+ Stopped apropos shell >bash-commands
```

第 3 章：Shell
