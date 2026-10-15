

### 示例 11.16

（~/.sh_history 文件）
（该文件包含用户在命令行输入的命令列表）

```
netscape&
ls
mkdir javascript
cd javascript
cp ../javapdf.zip .
gunzip javapdf.zip
unzip javapdf.zip
ls
ls
more chapter10&
ls -l
rm chapter9.pdf
ls
ls -l

... continues ...
```

```
1  $ history -1 -5      # List last 5 commands, preceding this one in reversed order.
13  history -3
12  history 8
11  history -n
10  history
9   set

2  $ history -5 -1      # Print last 5 commands, preceding this one in order.
10  history
11  history -n
12  history 8
13  history -3
14  history -1 -5

3  $ history             # (Different history list)
78  date
79  ls
80  who
81  echo hi
82  history

4  $ history ls echo     # Display from most recent ls command to
                        # most recent echo command.
79  ls
80  who
81  echo hi

5  $ history -r ls echo  # -r reverses the list
81  echo hi
80  who
79  ls
```

## 11.3 命令行

### history 命令/重显命令。

内置的 history 命令列出之前输入的命令，并在前面加上编号。该命令可以接受参数来控制显示。

```
EXAMPLE 11.17

1  $ history              # Same as fc -l
   1 ls
   2 vi file1
   3 df
   4 ps -eaf
   5 history
   6 more /etc/passwd
   7 cd
   8 echo $USER
   9 set
  10 history

2  $ history -n           # Print without line numbers
   ls
   vi file1
   df
   ps -eaf
   history
   more /etc/passwd
   cd
   echo $USER
   set
   history
   history -n

3  $ history 8            # List from 8th command to present
   8 echo $USER
   9 set
  10 history
  11 history -n
  12 history 8

4  $ history -3           # List this command and the 3 preceding it
  10 history
  11 history -n
  12 history 8
  13 history -3

5  $ history -1 -5        # List last 5 commands, preceding this one in reversed order.
  13 history -3
  12 history 8
  11 history -n
  10 history
   9 set

6  $ history -5 -1    # Print last 5 commands, preceding this one in order.
10 history
11 history -n
12 history 8
13 history -3
14 history -1 -5
7  $ history           # (Different history list)
78 date
79 ls
80 who
81 echo hi
82 history
```

### 使用 r 命令重新执行命令。

r 命令重新执行在命令行输入的最后一条命令。如果 r 命令后面跟一个空格和一个数字，则执行该编号的命令。如果 r 命令后面跟一个空格和一个字母，则执行以该字母开头的最后一条命令。如果没有参数，r 命令将重新执行历史列表中最前面的命令。

### 示例 11.18

```
1  $ r date
date
Mon May 15 12:27:35 PST 2004
2  $ r 3    redo command number 3
df
Filesystem  kbytes  used  avail  capacity  Mounted on
/dev/sd0a   7735    6282   680    90%       /
/dev/sd0g  144613  131183 0      101%      /usr
/dev/sd2c  388998  211395 138704  60%       /home
3  $ r vi    # Redo the last command that began with pattern vi.
4  $ r vi file1=file2  # Redo last command that began with vi and substitute the first occurrence of file1 with file2.
```

### 解释

- 1. 最后一条命令 date 被重新执行。
- 2. 历史文件中的第三条命令被执行。
- 3. 最后一条以字符串 vi 开头的命令被执行。
- 4. 字符串 file1 被替换为字符串 file2。最后一条命令 vi file1 被替换为 vi file2。

### 11.3.7 命令行编辑

Korn shell 提供了两个内置编辑器，emacs 和 vi，允许你交互式地编辑历史列表。要启用 vi 编辑器，请添加下面列出的 set 命令并将其放入你的 .profile 文件中。emacs 内置编辑器一次处理历史文件中的一行，而 vi 内置编辑器处理由多行组成的命令。要设置 vi，输入

```
set -o vi   or   VISUAL=vi   or   EDITOR=/usr/bin/vi
```

如果使用 emacs，输入

```
set -o emacs   or   VISUAL=emacs   or   EDITOR=/usr/bin/emacs
```

请注意 set -o vi 会覆盖 VISUAL，而 VISUAL 会覆盖 EDITOR。

### vi 内置编辑器。

要编辑历史列表，请按 Esc 键并使用你在 vi 中用于向上、向下、向左、向右移动、删除、插入和更改文本的标准键。参见表 11.2。编辑完成后，按 Enter 键。该命令将被执行并添加到历史列表底部。要在历史文件中向上滚动，请按 Esc 键然后按 K 键。

### 表 11.2 vi 命令

| Command | Function |
|---|---|
| Moving Through the History File | |
| Esc k or + | Move up the history list |
| Esc j or - | Move down the history list |
| Esc G | Move to first line in history file |
| Esc 5G | Move to fifth command in history file |
| /string | Search upward through history file for string |
| ? | String search downward through history file |
| Moving Around on a Line (Press the Esc Key First) | |
| h | Move left on a line |
| l | Move right on a line |
| b | Move backward a word |
| e or w | Move forward a word |

