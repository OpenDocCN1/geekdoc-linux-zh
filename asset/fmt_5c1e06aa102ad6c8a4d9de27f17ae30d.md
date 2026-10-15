
## 示例 3：多行命令别名

通常一个进程需要多个命令。由于在 UNIX 中这些命令被视为一行，因此它们可以分配别名。由于某些列表输出可能超过一个屏幕，将输出管道到 `more` 是一个好主意。我们在会话 5.35 中结合了这一变化。再次收缩输出。

### 会话 5.35 使用多行命令别名

```
$ alias dir="ls -l | more"
$ dir
total 30
-rw------ 1 bergberg staff 5782 Sep 10 16:19 TheRaven
-rw------ 1 bergberg staff 366 Sep 9 19:56 TheRavenV1
-rw-r--r-- 1 bergberg staff 149 Apr 18 2000 teeOut
```

## 示例 4：在别名定义中使用别名

可以使用定义来创建别名。然而，这种用法有一个危险：如果一个定义使用了多个别名，且其中一个指向另一个，定义可能会变成递归并导致 Shell 崩溃。由于这个原因，我们建议定义新别名时只使用单一定义。会话 5.36 包含了定义内的简单定义。

### 会话 5.36 在别名定义中使用别名

```
$ alias dir=ls
$ alias ldir="dir -l | more"
$ ldir
total 30
-rw------ 1 bergberg staff 5782 Sep 10 16:19 TheRaven
-rw------ 1 bergberg staff 366 Sep 9 19:56 TheRavenV1
-rw-r--r-- 1 bergberg staff 149 Apr 18 2000 teeOut1
```

## 别名命令的参数

只要不产生歧义，就可以参数传递给别名。参数在命令之后添加。参数可以适当包含通配符。例如，我们在会话 5.37 中将文件传递给列表命令。

### 会话 5.37 向别名传递参数

```
$ alias fl="ls -l"
$ fl*
+ ls -l lsLoop.scr fileout
-rw------ 1 bergberg staff 175 Sep 13 10:38 fgLoop.scr
-rw-r--r-- 1 bergberg staff 15 May 17 20:00 file1
-rw-r--r-- 1 bergberg staff 395 Sep 9 20:00
```

**会话 5.37 分析：** 我们将别名命名为（`fl`）。为了看到此命令的具体情况，我们开启了扩展选项。扩展后的命令以加号开头，后面跟着参数。有时参数会出现歧义。这通常发生在一个别名中包含多个命令时。在会话 5.38 中，我们使用了错误的别名（`indir`），导致歧义。输出是收缩的。

### 会话 5.38 歧义别名命令

```
$ indir
+ ls -l
+ more
```

**会话 5.38 分析：** 我们想要的是 `TheRavenfile` 的长列表。得到的却是内容。从扩展命令中，我们注意到 Shell 将参数添加到了最后一个命令。因此，我们得到的是内容列表而不是文件的详细列表。

## 列出别名

Korn 和 Bash Shell 都提供了列出所有别名和特定别名的方法。它们都使用 `alias` 命令。列出所有别名时使用带参数的 `alias` 命令。列出特定命令时使用带有一个参数（别名名称）的 `alias` 命令。这些变体在会话 5.39 中进行了演示。

### 会话 5.39 别名命令列表

```
$ alias
autoload='typeset -f'
cat=/sbin/cat
dir='echo Listing for gallery'; ls -1 | more
fl='ls -1 | more'
stop='kill -STOP'
suspend='kill -STOP'

$ alias dir
dir='echo Listing for gallery'; ls -1 | more
```

**会话 5.39 分析：** 第一次执行以收缩格式列出所有别名。一眼发现已经定义了许多别名。我们的两个是第三和第四个。第二次执行显示了特定别名 `dir` 的结果。

## 删除别名

通过 `unalias` 命令删除别名。当配合选项（`-a`）使用时，它会删除所有要删除的别名。使用时它会删除所有别名。然而，使用此选项要非常小心：它会删除所有别名，甚至是系统管理员定义的。由于这个原因，某些系统管理员会禁用此选项。会话 5.40 仅演示了名称参数。

### 会话 5.40 删除别名名称

```
$ alias dir
dir='echo Listing for gallery'; ls -l | more'
$ unalias dir
$ alias dir
dir: alias not found
```

## C Shell 中的别名

C shell 在格式上与 Korn shell 别名不同，但功能相同。它们还有更强大的特性，特别是参数定义。C shell 定义别名的语法略有不同，在于没有赋值运算符。基本格式为：

![](img/6e4cdc423ec40606ea72b32fdafff220_195_0.png)

在会话 5.41 中，我们为 C shell 重新定义了列表选项。

### 会话 5.41 C Shell 中的别名定义

```
% alias dir "echo Gallery List; ls -l | more"
% dir
Gallery Directory List
total 30
-rw------- 1 bergberg staff 5782 Sep 10 16:19 TheRaven
-rw-r-r-- 1 bergberg staff 149 Apr 18 2000 teeOut1
-rw-r-r-- 1 bergberg staff 149 Apr 18 2000 teeOut2
```

别名命令的参数由于 Korn shell 将参数放在生成命令的末尾，而 C shell 允许我们控制位置。表 5.4 包含了用于别名参数的设计符。

### 表 5.4 C Shell 参数设计符

| 设计符 | 含义 |
| --- | --- |
| `\*` | 唯一参数的位置 |
| `!^` | 第一个参数的位置 |
| `$` | 最后一个参数的位置 |
| `\!:n` | 第 n 个参数的位置。 |

当我们在 Korn shell 中编写文件列表别名时，参数位于末尾，这导致了一个问题。在 5.42 章节中，我们使用唯一参数位置指示符重写了它。

### 章节 5.42 唯一参数位置示例

```
% alias fl 'ls -1 |*' | more
% fl1 TheRavenV1
-rw--- 1 gilberg staff 366 Sep 9 19:56 TheRavenV1
% fl
total 30
-rw--- 1 gilberg staff 5782 Sep 10 16:19 TheRaven
-rw-r--r--- 1 gilberg staff 149 Apr 18 2000 teeOut2
```

**章节 5.42 分析：** 注意，引号包裹在别名命令周围，包含了唯一参数指示符（`!!`），它被放置在命令中间恰恰是它所属的位置。我们运行了两次命令：一次带参数，一次不带参数。不带参数的输出是缩略的。

为了一个更复杂的例子，让我们写一个复制文件并重命名的命令。我们需要两个参数：一个用于原始文件名，另一个用于副本名。代码在 5.43 章节中。

### 章节 5.43 带两个参数的命令

```
% ls -delete.me
No such file or directory
% alias cpto 'cpto \!:1 \:$'
% cpto file1 -delete.me
% ls -delete.me
/mnt/diska/staff/gilberg/delete.me
```

**章节 5.43 分析：** 我们从列表命令开始，以证明文件不存在。然后我们创建了复制命令并执行它，将文件从当前目录复制到主目录（`~/`）。复制后，我们再次列出它以证明它已被复制。

### 列出别名

就像 Korn shell 一样，我们可以列出特定的别名或所有别名。两者的语法相同。5.44 章节包含一个别名列表。

#### 章节 5.44 别名列表示例

```
% alias \
cpto     cp \!:1 \:$
dir      echo Gilbergs Directory List; ls -1 | more
fl       ls -1 \!* | more
```

### 删除别名

正如我们在 Korn shell 中看到的，C shell 使用 `unalias` 命令来删除一个或所有别名。5.45 章节演示了 C shell 中的 `unalias` 命令。

#### 章节 5.45 在 C Shell 中删除别名

