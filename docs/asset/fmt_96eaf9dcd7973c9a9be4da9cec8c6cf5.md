
这解释起来有点困难，但此输出说明 87.3% 的用户选择 `csh` 作为其登录 shell，另外 9.4% 使用修改过的 `tcsh`，只有 2.2% 使用 `ksh`。剩余的 1.1% 使用 Bourne shell 或 MH shell，或者默认使用 Bourne shell（前述输出中的两个账户没有指示任何 shell）。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_317_1.png)

# 第 14 小时

## 命令 shell 简介

> `scale=4` 命令告诉 `bc` 在数字小数点位后显示多少位数。遗憾的是，`bc` 默认不显示小数点位后的任何数字。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_0.png)

有许多不同的 shell 可用，在我熟悉的网站上最常见的是 C shell。显然，我用于这组特定示例的系统拥有绝大多数的 C shell 用户：高达 97% 的用户正在 C shell 或其后代 `tsh` 中工作。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_1.png)

### 任务 14.2：识别你的 shell

识别正在使用的 shell 有许多方法。但最的方法是直接进入 `/etc/passwd` 文件查看你的账户列出了什么。了解一些替代方案是有用的，因为 `/etc/passwd` 并不总是可用的（出于安全考虑，某些系统没有 `/etc/passwd` 文件）。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_2.png)

- 1. 识别 shell 的一种简单技巧是检查你的提示符（prompt）。如果你的提示符包含 `$`，你可能正在使用 C shell 或修改过的 C shell (`tsh`)。如果你的提示符包含 `#$`，你可能在使用 Bourne shell、`Korn shell` 或其变体。
- 2. 确定你正在使用的 shell 更为可靠的方法是询问操作系统你当前正在运行什么。shell 会标识 shell 的 ID。你可以使用 `$$` 作为 `ps` 输出的 `grep` 搜索模式，以查看你正在使用什么 shell。以下是我尝试时的结果：

```
$ ps -ef | grep $$
taylor 26905 0.0 0.2 256 144 Ai S 0:03 -csh (csh)
taylor 29751 0.0 0.1 52 28 Ai S 0:00 grep 26905
```

你可以看到我正在运行 C shell。以这种方式使用 `$$` 也会匹配 `grep` 进程（注意 `$$` 已经扩展为当前的 shell 进程标识 26905）。在指示它是我的登录 shell 还是我运行的一个 shell 的标识前，有一个横杠。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_318_3.png)

- 3. 发现我正在运行什么 shell 的另一种方法是查看 `/etc/passwd` 文件，只要你对 `awk` 有足够的运用，它不再神秘，就可以做到。

```
% awk -F: ' if ($1 == "taylor") print "your shell is: \$7" ' < /etc/passwd
nyour shell is: /bin/csh
```

- 4. 然而，确定你运行什么 shell 的最佳方法是使用 `csh`。在下一个任务中学习如何使用 `csh`。

一旦你识别了你的 shell，就可以考虑选择另一个。

### 任务 14.3：如何选择新 shell

在过去，在许多系统中切换登录 shell 的唯一方法是要求管理员直接编辑 `/etc/passwd` 文件。这通常意味着要等管理员有空。好消息是，几乎所有的 UNIX 系统都有一个简单的程序来更改登录 shell——它就是 `csh`，或者说 `change csh`。它没有启动标志或选项。

- 1. 第一步是识别哪些 shell可用。按照惯例，shell 位于 `/bin` 或 `/usr/bin`。你可以使用 `ls` 命令查看那里有什么：

```
$ ls /bin
bash
csh
dash
ksh
sh
```

- 2. 如果你的系统上有 `csh`，你可能想尝试这个不同的 shell。要将我的登录 shell 更改为这些 shell 之一，或者仅仅是验证我正在运行它，可以使用 `change shell` 命令：

```
% chsh
```

- 3. 遗憾的是，它要求你指定一个。我将通过请求 `emacs` 成为我的登录 shell 来干扰你：

```
% chsh
Changing shell for taylor.
Old shell: /bin/csh
New shell: /usr/local/bin/gnuacs
/usr/local/gnuacs is unacceptable as a new shell.
```

- 4. 程序某些某些 shell 名称。你可以查看 `etsh` 使用的文件来确认哪些程序是有效的 shell。我会检查 `/etc/shells`，它看起来如下：

```
% cat /etc/shells
/bin/ksh
/bin/sh
/bin/csh
/usr/local/bin/csh
/usr/local/bin/tcsh
```

- 5. 如果你的系统上有 `csh`，你可能想尝试这个 `/bin/tcsh`。我将我的登录 shell 从 `/bin/csh` 更改为 `/usr/local/bin/tcsh`：

```
% chsh
Changing login shell for taylor
Old shell: /bin/csh
New shell: /usr/local/bin/tcsh
```

注意，在 UNIX 风格中，并没有实际的确认执行了什么。幸运的是，可以通过再次使用 `etsh` 或使用 C shell 历史命令重做 `awk` 程序来轻松检查：

```
% awk -F: '{if ($1 == "taylor") print "your shell is: " $7}' < /etc/passwd
your shell is: /usr/local/bin/tcsh
```

## 命令行 Shell 简介

在接下来的一小时里，你将更多地学习强大的 C shell 命令历史记录机制。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_322_0.png)

由于 C shell 极其流行，接下来的几个小时将重点介绍 C shell。为了充分利用这几个小时的时光，我强烈建议你使用 C shell。

只需稍等

- 5. 快速调用 `csh` 命令可以将你的 shell 切换回 `/bin/csh`：

```bash
% csh
Changing login shell for taylor
Old shell: /usr/local/bin/tcsh
New shell: /bin/csh
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_322_1.png)

如果你无法更改登录 shell（可能是因为没有安装 `csh`），你始终可以在登录后通过输入 `csh` 来进入 C shell。

只需稍等

更改登录 shell 很容易。你可以尝试不同的 shell 直到找到最适合你交互风格的一个。不过，在大多数情况下，所有的 shell 都具有相同的字节语法并使用相同的命令：`ls -i` 在不同 shell 中执行的是相同的操作。那么，差异真正在你使用更高级的功能时才会体现，包括对 shell 进行编程（使用 shell 脚本）、通过命令别名（`aliases`）自定义其功能，以及使用历史记录机制减少按键次数。这正是 C shell 的优势所在，也是它如此流行的原因。正如你在接下来的一小时中将学的，它简单、直接，并且拥有强大的历史记录和作业控制能力。

### 任务 14.4：学习 Shell 环境

在这一小时早些，你使用了 `env` 或 `print` 命令来查找工作环境的各种特性。现在是时候使用该命令更仔细地查看 C shell 环境，并定义其中的每一个变量。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_322_2.png)

- 1. 首先，我输入 `env` 来列出我工作环境的各个方面。你的系统也是如此，尽管你的环境不会与我的完全相同，但两者之间应该有很大的相似之处。
