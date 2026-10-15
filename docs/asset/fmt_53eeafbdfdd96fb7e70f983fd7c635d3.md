
### EXPLANATION

历史列表显示了在命令行中输入的最后几条命令。列表中的每个事件前面都有一个数字（称为事件编号）和在命令行中输入的时间。

## The history Variable.

TC shell 的 `history` 变量可以被设置为将在终端上显示的历史列表中的事件数。通常，这是在 `/etc/.cshrc` 或 `~/.tcshrc` 文件中设置的，即用户的初始化文件。默认设置为 100。你也可以为 `history` 变量提供一个可选的第二个值来控制历史的格式。此值使用与 `prompt` 变量相同的格式化序列。（参见表 9.10。）`history` 的默认格式字符串为 `%h\t%T\r\n`。

## EXAMPLE 9.75

```
1 set history=1000

2 set history=( 1000 '%bh %B%t\n' )

3 history

136 history

137 set history = ( 1000 '%bh %B%t\n' )

138 history

139 ls

140 pwd

141 cal

141 pwd

142 cd
```

### EXPLANATION

- 1 The last 1,000 commands typed at the terminal can be displayed on the screen by typing the `history` command.

### EXPLANATION (CONTINUED)

- 2. The last 1,000 commands typed at the terminal are displayed. The format string causes the history list to be displayed in bold text (`%B`) first with the event number (`%h`), then a space, and finally the command that was typed (`%R`) at the command line followed by a newline (`\n`).
- 
- 3. When you type `history`, the new format is shown. This is only a selected section of the real history list.

## Saving History and the savehist Variable.

要跨登录保存历史事件，请设置 `savehist` 变量。此变量通常在 `.tcshrc` 文件中设置，即用户的初始化文件。如果分配给 `savehist` 的第一个值是一个数字，则它不能超过 `history` 变量中设置的数量，如果 `history` 变量已设置。如果第二个值设置为 `merge`，则历史列表将与现有历史文件合并而不是替换它。它按时间戳排序，并保存最近的事件。

### EXAMPLE 9.16

```
1  set savehist

2  set savehist = 1000

3  set savehist = 1000 merge
```

### EXPLANATION

- 1. The commands from the history list are saved in the history file and will be at the top of the history list the next time you log in.
- 
- 2. The history file is replaced with the last 1,000 commands from the history list, and saved. It will be displayed when you next log in.
- 
- 3. Rather than replacing the existing history file, the current history list will be merged with the existing history file when you log out, and loaded into memory after you log in.

## Displaying History.

`history` 命令显示历史列表中的事件。`history` 命令还具有控制将显示多少个事件以及事件格式的选项。事件的编号不一定从一开始。如果历史列表中有 100 条命令，并且你将 `history` 变量设置为 25，你将只看到保存的最后 25 条命令。

### EXAMPLE 9.17

```
1  > set history = 10

2  > history

   1 ls

   2 vi file1

   3 df
```

## EXAMPLE 9.77 (CONTINUED)

```
4 ps -eaf

5 history

6 more /etc/passwd

7 cd

8 echo $USER

9 set

10 ls
```

### EXPLANATION

- 1. The `history` variable is set to 10. Only the last 10 lines of the history list will be displayed, even if there are many more.
- 2. The last 10 events from the history are displayed. Each command is numbered.

## EXAMPLE 9.78

```
1 > history -h   # print without line numbers

ls

vi file1

df

ps -eaf

history

more /etc/passwd

cd

echo $USER

set

history -n

2 > history -c
```

### EXPLANATION

- 1. With the `h` option, the history list is displayed without line numbers.
- 2. With the `c` option, the history list is cleared.

## EXAMPLE 9.79

```
> history -r   # print the history list in reverse

11 history -r

10 history -h

9 set

8 echo $USER

7 cd

6 more /etc/passwd

5 history

4 ps -eaf

3 df

2 vi file1

1 ls
```

# 解释

历史列表以相反顺序显示。

## 示例 9.80

```
> history 5   # prints the last 5 events on the history list

7  echo $USER

8  cd

9  set

10 history -n

11 history 5
```

# 解释

历史列表上的最后五个命令被显示。

## 从历史文件访问命令。

有几种方法可以从历史列表访问和重复命令。`tcsh` 中包含了一个很棒的新功能：你可以使用历史记录配合方向键。它们允许你上下滚动历史列表，并在行间左右移动，同时进行编辑；你可以使用一种称为历史替换的机制来重新执行并修正拼写错误；或者你可以使用内置的 `emacs` 或 `vi` 编辑器来检索、编辑和执行之前的命令。我们将逐步介绍这些程序，然后你可以选择最适合你的方式。

## 1. 方向键

要从历史列表访问命令，你可以使用键盘上的方向键在历史列表中上下移动，并左右移动。你可以使用标准的删除、退格等键来编辑历史列表中的任何一行。只要你编辑了该行，按下回车键（Enter 键）就会导致命令行重新执行。你也可以使用标准的 `emacs` 或 `vi` 命令来编辑历史列表。（参见第 475 页的表 9.13 和第 476 页的表 9.14。）对于 `vi` 和 `emacs` 两种键绑定，方向键的行为方式相同。（参见表 9.11。）

### 表 9.11 方向键

| 键 | 其作用 |
| --- | --- |
| ↑ | 上箭头向上移动历史列表 |
| ↓ | 下箭头向下移动历史列表 |
| → | 右箭头将光标移动到历史命令的右侧 |
| ← | 左箭头将光标移动到历史命令的左侧 |

## 示例 9.81（续）

```
8 > set histlit

9 > history

1 16:18 1s

2 16:19 date

3 16:19 !!

4 16:20 !3

5 16:21 dare

6 16:21 ArAt
```
