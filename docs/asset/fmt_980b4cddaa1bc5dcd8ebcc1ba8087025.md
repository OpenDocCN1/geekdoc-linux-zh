
使用 `1>&2` 进行重定向在这里实现了什么吗？没有，目前还没有，但我们在对脚本做一个微小更改后，它就会实现。注意，使用 `>>` 向 `addressbook` 追加行会导致 `addressbook` 在每次迭代时都被打开和关闭。这是昂贵的，我们可以从那里移除重定向，转而是在 `done` 关键字处提供：

```bash
done >> addressbook # addressbook 只打开一次
```

这会重定向循环体中所有语句的标准输出。通过 `1>&2` 发送到标准错误的消息不受影响。在当前情况下，只有一个语句受此影响。这种技术也是高效的，因为 `addressbook` 只被打开和关闭了一次。

重定向也可以用于 `fi` 和 `esac` 关键字，并包括输入重定向和管道：

- `< param.lst`：循环中的语句从 `param.lst` 获取输入
- `done | while read name`：`while` 从标准输入获取输入
- `fi > foo`：影响 `if` 和 `fi` 之间的语句
- `esac > foo`：影响 `case` 和 `esac` 之间的语句

我们将在 13.13.3 节使用第二种形式，即循环从管道获取输入。

### 13.13.2 使用 while 等待文件

在某些情况下，循环需要等待一个文件。

```bash
#!/bin/sh
# monitor.sh: 等待文件
while [ ! -f /tmp/lock ]; do
  sleep 1
done
touch /tmp/lock
```

`break` 语句导致控制流跳出循环。当发现文件 `$1` 是可读的时，在这里执行了此操作。

`continue` 语句暂停其后所有语句的执行，并开始下一次迭代。`break` 和 `continue` 在 C 和 Java（以及 awk）中也有同名命令，但只有在 shell 中它们可以带参数使用。第 13.16 节讨论的一个示例使用了 `break 2`。

shell 还提供了 `until` 语句控制命令，它使用了与 `while` 相反的逻辑。在 `while` 循环中，只要条件为真，就会执行循环体。因此，`while [ ! -r $1 ]` 等同于 `until [ -r $1 ]`。

## 13.14 示例脚本 2：为备份文件提供数字扩展

我们将汇总目前获得的所有知识来开发两个示例脚本。脚本 2 `cpback.sh`（图 13.14）的行为类似于增强型且非交互式的 `cp` 命令。如果目标位置已存在一个文件（例如 `foo`），它会为其提供一个数字扩展名（例如 `.1`）。由于该带扩展名的文件可能存在，它会反复增加数字，最终在不覆盖的情况下复制文件。

从参数列表 (`$@`) 中，我们需要将目录名与文件名分离。UNIX shell 没有标识最后一个参数的符号，因此我们必须利用对 `sed` 的知识来完成这项工作。第一个 `sed` 命令匹配零个或多个非空格字符。第二个 `sed` 命令匹配之前未匹配的表达式以复制文件名。注意，这两种情况下都使用了正则表达式，不同在于对表达式的不同部分进行了分组。

让我们开始使用多个文件名复制文件到安全目录。我们假设安全目录中存在一个 `toc.pl` 文件，但不存在 `index`。我们将运行相同次数的命令行行：

```
$ cpback.sh vvi.sh toc.pl index safe
File vvi.sh copied to vvi.sh.3
File toc.pl copied to toc.pl.1
$ cpback.2 vvi.sh toc.pl index safe
File vvi.sh copied to vvi.sh.4
File toc.pl copied to toc.pl.2
File index copied to index.1
$ cpback.3 vvi.sh toc.pl index safe
File vvi.sh copied to vvi.sh.5
File toc.pl copied to toc.pl.3
File index copied to index.2
```

反复运行。我们将得到一个可以复制一个或多个文件但不会覆盖目标的工具。将其放在本地的 `bin` 目录中并链接到一个更短的名字——例如 `cp2`。

### 图 13.14 cpback.sh：不覆盖即复制多个文件的脚本

```bash
#!/bin/sh
# cpback.sh: 将多个文件复制到目录
# 创建备份而不是覆盖目标文件
# 如果 foo 存在则复制到 foo.1，如果 foo.1 存在则复制到 foo.2 ......

if [ $# -lt 2 ]; then
    echo "Usage: $0 source destination"; exit
fi

# 从参数列表中分离目录
dest=$(echo "$0" | sed 's/.*\(\([^/]*\*/)/\/')

# ... 从参数列表中分离文件
filelist=$(echo "$@" | sed 's/\(.*\\) .*/1/')

if [ -d "$dest" ]; then
    echo "Directory $dest doesn't exist"; exit 1
fi

for file in $filelist; do
    if [ ! -f "$file" ]; then  # 如果文件不存在
        echo "$file doesn't exist"
        continue
    else  # 目标位置存在文件
        ext=1  # 从 .1 开始
        # 获取最大的可用扩展
        while true; do
            if [ ! -f "$dest/$file.$ext" ]; then  # 如果文件不存在
                cp "$file" "$dest/$file.$ext"  # 使用该扩展名
                echo "File $file copied to $file.$ext"
                break  # 无需进一步迭代
            else
                ext=`expr $ext + 1`  # 该扩展名存在，继续尝试
            fi 
        done
    fi
done
```

## 13.15 使用 set 和 shift 操作位置参数

在此阶段，我们已经涵盖了能够为我们完成大量工作的基础编程结构。但 UNIX 以其文本处理能力闻名，其中一些技能也可以在 shell 中实现。许多 shell 应用需要处理单行命令输出：

```
$ date
Dec 9 10:39:47 IST 2003
$ ls -1 /etc/password
-r--r--r 1 root sys 9995 28 15:30 /etc/password
$ ps -e | grep find
1149 tty 00:00:00 find
```

开发一个知道星期几、`/etc/password` 修改日期，或者在不知道其 PID 的情况下杀死 `find` 命令的程序又如何？在讨论时，我们必须使用 `cut` 从日期输出中提取星期：

```
case 'date' | cut -d' ' -f1
```

这显得有些大材小用，且这种技术有局限性。我们可能需要使用 `cut` 和 `awk` 的服务从单行命令输出中提取所有单词。shell 的 `set` 给其参数（如 `$1`, `$2`, ...）以及 `$#` 和 `$0` 分配值。

`set` 的参数通常通过命令替换获取。`set` 将值赋值给其参数（如 `$1`, `$2`, ...）以及 `$#` 和 `$0`。

### 13.15.1 set：赋值参数

```bash
$ set -- $(date)
$ echo "$0"
Wed Jan 8 09:48:44 IST 2003
```

---

### 13.15.2 shift：向左移动位置参数

许多程序使用循环遍历程序的参数，但不包含第一个参数。该参数可能代表目录，剩下的是普通文件名。我们需要 `"$1"`，但是在移除第一个参数并重命名参数之后。这就是 `shift` 的作用。每次调用 `shift` 会将位置参数的内容传输到其左侧编号较低的参数。`$2` 变成 `$1`，`$3` 变成 `$2`，以此类推：

```bash
$ set -- $(date)
$ echo "$0"
Wed Jan 8 09:48:44 IST 2003
$ shift
$ echo $1 $2 $3
Jan 8 09:48:44
$ shift 3
$ echo $1
```

在这里，`"$1"` 和 `$*` 是互换的。三个参数丢失了！当调用 `shift` 时，最左侧参数 `$1` 的内容会丢失。如果 `$1` 很重要，你必须在调用 `shift` 之前将其保存在独立的变量中。注意 `shift` 也可以带整数参数工作；`shift n` 向左移动 n 个单词。

让我们设计一个脚本 `ln.sh`（图 13.16），它为单个目标创建一组符号链接。第一个参数是目标，剩下的是要待创建的符号链接。确保在调用 `shift` 之前保存了 `$1`。

我们确保目标存在，在调用 `shift` 之前保存其名称，然后使用 `for` 循环创建多个符号链接。`ln` 的 `-f` 选项确保现有目标会被移除。

### 图 13.15 ln.sh
