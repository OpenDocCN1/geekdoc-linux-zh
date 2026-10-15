

## 设置历史。

C shell 历史变量设置为你希望从历史列表中保存并在屏幕上显示的事件数。通常，这是在 .cshrc 文件中设置，用户初始化文件。

### EXAMPLE 9.12

```
set history=50
```

### EXPLANATION

在终端输入的最后 50 条命令会被保存，并且可以通过输入 history 命令在屏幕上显示。

## 保存历史。

要跨登录保存历史事件，请设置 savehist 变量。此变量通常在 .cshrc 文件中设置，用户初始化文件。

### EXAMPLE 9.13

```
set savehist=25
```

### EXPLANATION

历史列表中的最后 25 条命令会被保存，并在下次登录时位于历史列表顶部。

## 显示历史。

history 命令会显示历史列表中的事件。history 命令还有控制将显示的事件数量和格式的选项。事件的编号不一定从 1 开始。如果你历史列表中有 100 条命令，并且将 history 变量设置为 25，你将只看到保存的最后 25 条命令。 （TC shell 支持使用方向键。参见第 470 页的“Accessing Commands from the History File”。）

### EXAMPLE 9.14

```
% history
1 ls
2 vi file1
3 df
4 ps -eaf
5 history
6 more /etc/passwd
7 cd
8 echo $USER
9 set
```

### EXPLANATION

历史列表被显示。每个命令都被编号。

### EXAMPLE 9.15

```
% history -h    # Print without line numbers
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
```

### EXPLANATION

历史列表不带行号显示。

### EXAMPLE 9.16

```
% history -r    # Print the history list in reverse
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

### EXPLANATION

历史列表以相反顺序显示。

### EXAMPLE 9.17

```
% history 5    # Prints the last 5 events on the history list
7 echo $USER
8 cd
9 set
10 history -n
11 history 5
```

### EXPLANATION

历史列表上的最后五个命令被显示。

## 重新执行命令。

要从历史列表重新执行命令，使用感叹号（bang）。如果你输入两个感叹号 (!!)，则重新执行最后一条命令。如果你输入感叹号后跟一个数字，该数字与历史列表中的命令相关联并执行该命令。如果你输入感叹号和一个字母，则执行以该字母开头的最后一条命令。插入符号（^）也用作编辑上一条命令的快捷方法。

### EXAMPLE 9.18

```
1 % date
Mon Apr 26 8 12:27:35 PST 2004
2 % !!
date
Mon Apr 26 12:28:25 PST 2004
3 % !3
date
Mon Apr 26 12:29:26 PST 2004
4 % !d
date
Mon Apr 26 12:30:09 PST 2004
5 % dare
dare: Command not found.
6 % ^A^t
date
Mon Apr 26 12:33:25 PST 2004
```

### EXPLANATION

- 1 date 命令在命令行执行。历史列表已更新。
- 2 !!（bang bang）获取历史列表中的最后一条命令；该命令被重新执行。
- 3 历史列表中的第三条命令被重新执行。
- 4 历史列表中以字母 d 开头的最后一条命令被重新执行。
- 5 命令输入错误。
- 6 使用插入符号从历史列表中的最后一条命令替换字母。第一次出现的 r 被替换为 t。

### EXAMPLE 9.19

```
1 % cat file1 file2 file3
<Contents of file1, file2, and file3 are displayed here>
% vi 1:1
vi file1
```

### EXAMPLE 9.19 (CONTINUED)

```
2
% cat file1 file2 file3
<Contents of file1, file2, and file3 are displayed here>

% ls !:2
ls file2
file2
```

```
3
% cat file1 file2 file3
% ls !:3
ls file3
file3
```

```
4
% echo a b c
a b c
% echo !$
echo c
c
```

```
5
% echo a b c
a b c
% echo !^ 
echo a
a
```

```
6
% echo a b c
a b c
% echo !:
 echo a b c
a b c
```

```
7
% !!:p
echo a b c
```

### EXPLANATION

1 cat 命令将 file1、file2 和 file3 的内容显示到屏幕。历史列表已更新。命令行被拆分为单词，从单词号 0 开始。如果单词号前面有冒号，则可以从历史列表中提取该单词。!:1 记法表示：获取历史列表中最后一条命令的第一个参数并将其替换到命令字符串中。最后一条命令的第一个参数是 file1。 （单词 0 是命令本身。）

2 !:2 被替换为最后一条命令的第二个参数 file2，并作为 ls 的参数给出。file2 被打印。 （file2 是第三个单词。）

3 ls !:3 的含义是：转到历史列表中的最后一条命令并获取第四个单词（单词从 0 开始）并将其作为参数传递给 ls 命令（file3 是第四个单词）。

