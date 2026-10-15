
```
bash-2.005$ ls
Complete  NewProject  bogus2
→ ftp      puppy
Completed News      dead_letter
→ mail     temp
Mail      access      files
→ public_html  testme
bash-2.005$ cd public_html/
bash-2.005$
```

代码清单 3.8 在此示例中，我们只输入了 `ls` 命令，然后输入 `"cd pub"` 并按下 `Tab` 键；`bash` 为我们完成了命令。

## 在 bash Shell 中使用补全

`bash` shell 的一个很酷的功能是命令参数补全，你可以只输入命令的一部分，按下 `Tab`，`bash` 就会为你补全命令（代码清单 3.8）。

### 在 bash shell 中使用补全：

- 1. `ls -l`

使用 `ls -l` 列出当前目录中的文件。

- 2. `cd pub Tab`

输入部分命令，然后按 `Tab` 补全命令。在此示例中，我们输入了 `cd` 命令和 `public_html` 目录的一部分（在示例中截断为 `pub`），然后按 `Tab` 补全它（参见代码清单 3.8）。

### 提示

- 补全仅在你在按 `Tab` 之前输入的字母只有一个可能匹配时才有效。例如，如果你输入 `cd pu`（对应 `public_html`），而另一个子目录名为 `puppy`，shell 会发出蜂鸣声并等待你输入足够多的字母以区分这两个子目录。

- 你可以使用补全来补全命令、命令中的目录名，以及几乎任何你可能输入且足够明确的内容。

## 在 bash Shell 中查看会话历史

`bash` shell 的另一个很酷的功能是它能让你轻松重用会话历史中的命令，会话历史会显示你在当前会话或之前会话中使用过的命令列表（代码清单 3.9）。查看历史记录对于回顾你的 Unix 会话、再次使用之前的命令（而不是重新输入它们）以及修改（而不是完全重新输入）复杂命令非常有用。

### 在 bash shell 中查看会话历史：

- 1. 使用 shell 一段时间，切换目录、重定向输出或执行其他任务。慢慢来。我们会等。

- 2. 按一次 `↑`。请注意，你上一个使用的命令会出现在命令行上，如代码清单 3.9 所示。要重新执行该命令，只需按 `Enter`。

- 3. 继续按 `↑` 或 `↓` 向后或向前滚动历史记录。当你找到想要使用的命令时，按 `Enter`。如果看到一个接近但不完全是你想要使用的命令，你可以编辑它。只需使用 `←` 和 `→` 键在行中移动，通过输入来插入文本，并使用 `Backspace` 或 `Delete` 删除文本。修改好命令后，按 `Enter`（你不必位于行尾即可）。

- 4. `history`

在 shell 提示符下输入 `history` 以查看之前输入的命令的编号列表。

```
[ejr@hobbes clean]$ ls
background.htm info.htm logo.gif
[ejr@hobbes clean]$ ls
background.htm info.htm logo.gif
[ejr@hobbes clean]$ history
1 free
2 id deb
3 id ejr
4 uname -a
5 ls
...
40 cd
41 cp .bash_history oldhistory
42 vi .bash_history
43 elm
44 ls -la
45 ls -la.e*
46 elm
47 lynx
48 history
49 vi .bash*nis*
50 history
51 cd clean
52 ls
53 ls
54 history
[ejr@hobbes clean]$ !40
cd
[ejr@hobbes ejr]$
```

代码清单 3.9 在此示例中，我们输入了第一个命令，然后按 `↑` 重用之前的 `ls` 命令。`!40` 循环使用了列表中的第 40 个命令。

#### 提示

- 当前会话的命令保存在内存中以便滚动浏览，而之前会话的命令保存在 `~/.bash_history` 文件中。你可以用任何编辑器编辑 `.bash_history` 来删除不需要的命令，或者直接删除该文件以清除整个历史记录，之后在你发出下一个命令时历史文件将被重新创建。（命令历史是编写脚本以自动执行这些命令的绝佳起点。第 10 章会给出具体说明。）

- 当你查看历史记录时，可以通过输入感叹号 `!` 和你想再次运行的命令的行号来复用命令。例如，输入 `!40` 即可重新运行第 40 条命令。

- 使用 `history` 后跟一个数字来指定要列出的项目数。例如，`history 10` 显示最后 10 条命令。

## 在 zsh Shell 中使用补全

`zsh` shell 也提供补全功能，但相比 `bash` shell 对高级用户来说增加了一些变化。基本上，你只需输入命令的一部分，按下 `Tab` 键，Z-shell 就会为你补全命令（代码清单 3.10）。

### 在 zsh shell 中使用补全：

1. `ls -l`

使用 `ls -l` 列出当前目录中的文件。

2. `cd pub Tab`

输入部分命令，然后按 `Tab` 键补全命令。在此示例中，我们输入了 `cd` 命令和 `public_html` 目录的一部分（在示例中截断为 `pub`），然后按 `Tab` 键将其补全（参见代码清单 3.10）。

### 提示

- 在 Z-shell 中，即使多个文件可能匹配你输入的部分命令，命令补全也有效。例如，如果你输入 `cd pu`（对应 `public_html`），并且还有另一个名为 `puppy` 的子目录，那么使用 `Tab` 补全名称时，shell 会显示选项（`public_html` 和 `puppy`），然后在你继续按 `Tab` 时在选项之间循环。

- 你可以使用命令补全来补全命令、命令中的目录名以及几乎你可能输入的任何内容。

- Z-shell 足够智能，只会显示你可切换到的子目录。`bash` 另一方面会显示文件和目录，并发出蜂鸣声——肯定没有那么有帮助。

```
$ ls
Complete    NewProject   bogus2
+ ftp        puppy
Completed   News         dead.letter
+ mail       temp
Mail        access       files
+ public_html           testme
$ cd public_html/
$
```

代码清单 3.10 在此示例中，我们只输入了 `ls` 命令，然后输入 `cd pub` 并按 `Tab` 键；`zsh` 为我们补全了命令。

#### 提示

- 如果你只是对命令做少量修改，可以快速轻松地编辑它。例如，如果你刚刚使用了 `cd /home/users/e/eric`，并且接下来想执行 `ls /home/users/e/eric`，你可以只输入 `^cd^ls` 来告诉系统用 `ls` 替换上一个命令中的 `cd`，然后重新发出命令。

- 当前会话的命令保存在内存中以便滚动浏览，而之前会话的命令保存在 `~/.zsh_history` 文件中。你可以用任何编辑器编辑 `.zsh_history` 来删除不需要的命令，或者直接删除该文件以清除整个历史记录，之后在你发出下一个命令时历史文件将被重新创建。

- 回顾会话历史是识别你的工作模式和需求的好方法。如果你发现自己反复使用同一系列命令，请考虑编写脚本以自动执行这些命令，如第 10 章所述。

- `bash` 中的大多数命令补全选项在 `zsh` 中也适用。试试看！

## 在 ksh Shell 中使用补全

`ksh` 是另一个提供命令补全的 shell。你输入部分命令，按两次 `Esc`，`ksh` 就会为你补全命令（参见代码清单 3.12）。在 `ksh` 中使用命令补全没有在 `zsh` 或 `bash` 中那么容易，但结果是一样的。

### 在 ksh shell 中使用补全：

1. `set -o emacs`

首先，你必须通过输入 `set -o emacs` 来启用命令补全。此命令启用命令补全并将其设置为使用 emacs 命令。（Emacs 是一个编辑器，但你不需要使用或熟悉它即可复用 `ksh` 命令。）

2. `ls -l`

使用 `ls -l` 列出当前目录中的文件。你这样做是为了知道可以在步骤 3 中切换到的目录（`public_html`）。

3. `cd pub Esc Esc`

输入部分命令。在此示例中，我们输入了 `cd` 命令和 `public_html` 目录的一部分（截断为 `pub`）。按两次 `Esc` 来补全命令。（根据你的终端仿真，你可能需要使用两次 `Ctrl+[` 而不是两次 `Esc`。）
