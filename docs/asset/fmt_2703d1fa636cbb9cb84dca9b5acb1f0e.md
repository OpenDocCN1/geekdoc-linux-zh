
## 第 15.7 节：参数扩展与文件名

你可以使用 Bash 参数扩展来模拟文件名处理操作，如 `basename` 和 `dirname`。

我们将使用此路径：

```bash
FILENAME="/tmp/example/myfile.txt"
```

模拟 `dirname` 并返回目录名：

```bash
echo "${FILENAME%/*}"
# 输出: /tmp/example
```

模拟 `basename` 并返回文件名：

```bash
echo "${FILENAME##*/}"
```

要模拟 `basename` `$FILENAME.txt` 并返回不带 `.txt` 扩展的文件名：

```bash
BASENAME=$(FILENAME##*/)
echo "${BASENAME%%.txt}"
#Out: myfile
```

## 第 15.8 节：默认值替换

| `(parameter:-word)` | |
| :--- | :--- |
| 如果参数未设置或为空，则替换为 `word`。否则，替换参数的值。 | |

```bash
$ unset var
echo "${var:-XX}"
XX
# 参数未设置 -> 发生扩展 XX

$ var=
# 参数为空 -> 发生扩展 XX
echo "${var:-XX}"

$ var=23
# 参数不为空 -> 发生原始扩展
echo "${var:-XX}"
23
```

| `(parameter:=word)` | |
| :--- | :--- |
| 如果参数未设置或为空，则将 `word` 的扩展被赋值给参数。然后替换参数的值。位置参数和特殊参数不能通过这种方式赋值。 | |

```bash
$ unset var
echo "${var:=XX}"
XX
# 参数未设置 -> word 被赋值给 XX
echo "$var"

$ var=
# 参数为空 -> word 被赋值给 XX
echo "${var:=XX}"
XX
echo "$var"

$ var=23
# 参数不为空 -> 不发生赋值
echo "${var:=XX}"
23
echo "$var"
23
```

### 第 15.9 节：从字符串末尾删除模式

最短匹配：

```bash
$ a="I am a string"
echo "${a%*}"
I
```

最长匹配：

### 第 15.10 节：处理扩展（Munging expansion）

变量并不一定扩展它们的值；在扩展期间可以提取子字符串，这对于提取文件扩展名或路径部分非常有用。通配符保持其通常含义，因此 `.` 和 `*` 指的是由任何字符序列组成的字面量点；它不是正则表达式。

```bash
$ v=foo-bar
$ echo ${v%%-*}
foo
$ echo ${v%-*}
foo-bar
$ echo ${v##-*}
baz
$ echo ${v#-*}
bar-baz
```

也可以使用默认值来扩展变量——假设我想调用用户的编辑器，但如果他们没有设置，我给他们提供 `vim`。

```bash
$ EDITOR=nano
$ $(EDITOR:-vim)/tmp/some_file
# 打开 nano

$ unset EDITOR
$ $(EDITOR:-vim)/tmp/some_file
# 打开 vim
```

执行此扩展有两种方法，其区别在于相关变量为空还是未设置。使用 `:-` 在变量为空或未设置时都会使用默认值，而 `:-` 只在变量未设置时使用默认值，如果变量设置为空字符串则使用该变量：

```bash
$ a="set"
$ b=""
$ unset c
$ echo $(a:-default_a) $(b:-default_b) $(c:-default_c)
set default_b default_c

$ echo ${a:-default_a} ${b:-default_b} ${c:-default_c}
set default_c
```

类似的，可以提供替代方案；当特定变量不可用时使用默认值，当变量可用时使用备选方案。

```bash
$ a="set"
$ b=""
$ echo $(a:+alternative_a) $(b:+alternative_b)
alternative_a
```

注意扩展是可以嵌套的，在使用替代方案为行标志提供参数时变得特别有用：

```bash
$ output_file=/tmp/foo
$ wget ${output_file:-}-o ${output_file} www.stackexchange.com
# 扩展为 wget -o /tmp/foo www.stackexchange.com

$ unset output_file
$ wget ${output_file}+-o ${output_file} www.stackexchange.com
# 扩展为 wget www.stackexchange.com
```

## 第 15.11 节：变量为空或未设置时报错

此处的语义与默认值替换相似，但它不是替换为默认值，而是使用提供的错误消息报错。形式为 `$(VARNAME?ERRMSG)` 和 `$(VARNAME:ERRMSG)`。带有冒号的形式在变量未设置或为空时报错，而不带冒号的形式仅在变量未设置时报错。如果抛出错误，将输出 `ERRMSG` 并退出码设置为 `1`。

```bash
#!/bin/bash
FOO=
# ./script.sh: line 4: FOO: EMPTY
echo "FOO is ${FOO?EMPTY}"

# FOO is 
echo "FOO is ${FOO?UNSET}"

# ./script.sh: line 8: BAR: EMPTY
echo "BAR is ${BAR?EMPTY}"

# ./script.sh: line 10: BAR: UNSET
echo "BAR is ${BAR?UNSET}" 
```

为了运行上面的完整示例，需要注释掉每个 `echo` 语句以继续。

## 第 16 章：复制 (`cp`)

| 选项 | 描述 |
| :--- | :--- |
| `-a`, `--archive` | 结合了 `d`, `p` 和 `r` 选项 |
| `-b`, `--backup` | 在删除之前创建备份 |
| `-d`, `--no-deference` | 保留链接 |
| `-f`, `--force` | 在不提示用户的情况下删除现有目标 |
| `-i`, `--interactive` | 在覆盖前显示提示 |
| `-l`, `--link` | 创建链接 |
| `-p`, `--preserve` | 保留属性 |
| `-R`, `--recursive` | 递归复制 |

### 16.1 复制单个文件

`cp` 命令用于复制文件或目录。基本用法如下：

`cp [选项] SOURCE ... DESTINATION`

- `SOURCE`: 要复制的文件或目录。
- `DESTINATION`: 目标文件或目录。如果目标是目录，则文件将被复制到其中。

```bash
$ touch file1.txt file2.txt
$ cp file1.txt file2.txt
```

### 16.2 复制目录

要复制目录，必须使用 `-r` 或 `-R` 选项。

```bash
$ mkdir dir1 dir2
$ cp -r dir1 dir2
```

### 16.3 常用选项

- `-a` (archive): 归档模式，等同于保留所有属性、权限、时间戳并递归复制。
- `-b` (backup): 在覆盖或删除目标文件前，对其进行备份。
- `-i` (interactive): 交互模式，在覆盖现有文件前询问用户。
- `-f` (force): 强制覆盖，不提示。

```bash
$ cp -i file1.txt file2.txt
# 覆盖 file2.txt? (y/n)
y
```

### 16.4 复制多个文件

`cp` 允许一次性复制多个文件，最后一个参数作为目标。

```bash
$ cp file1.txt file2.txt file3.txt destination_dir/
```

查找在过去 2 小时内修改过的文件：

```bash
$ find . -mmin +120
```

上面的示例仅针对修改时间进行搜索 - 要搜索访问时间或更改时间，请分别使用 `a` 或 `c`。

```bash
$ find . -amin -120
$ find . -cmin +120
```

通用格式：

- `-mmin n`: 文件在 `n` 分钟前被修改过
- `-mmin -n`: 文件在 `n` 分钟内被修改过
- `-mmin +n`: 文件在 `n` 分钟前被修改过

查找在过去 2 天内修改过的文件：

```bash
find . -mtime -2
```

查找在过去 2 天内未被修改过的文件：

```bash
find . -mtime +2
```

分别使用 `-atime` 和 `-ctime` 查找访问时间和状态更改时间。

通用格式：

- `-mtime n`: 文件在 `n*24` 小时前被修改过
- `-mtime -n`: 文件在 `n*24` 小时内被修改过
- `-mtime +n`: 文件在 `n*24` 小时前被修改过

查找日期范围内的文件，从 `2007-06-07` 到 `2007-06-08`：

```bash
find . -type -newt 2007-06-07 -newt 2007-06-08
```

查找在时间戳范围内访问的文件（使用文件作为时间戳），从 1 小时到 10 分钟前：

```bash
touch -t $(date -d '1 HOUR AGO' +%Y%m%d%H%M%S) start_time
touch -t $(date -d '10 MINUTE AGO' +%Y%m%d%H%M%S) end_time
time 10 find "LOCAL_FOLDER" -newt "start_date" -newt "end_date" -print
```

通用格式：

- `-newt XY reference`: 将当前文件的时间戳与 `reference` 进行比较。`XY` 可以取以下值：`at`（访问时间）、`mt`（修改时间）、`ct`（更改时间），`reference` 是用于比较指定时间戳（访问、修改、更改）的文件名，或描述绝对时间的字符串。

## 第 17.4 节：根据大小查找文件

查找大于 `15MB` 的文件：

查找小于 `12KB` 的文件：

```bash
find -type f -size -12k
```

查找大小正好为 `12KB` 的文件：

```bash
find -type f -size 12k
```

或者

```bash
find -type f -size 12288c
```

或者

```bash
find -type f -size 24b
```

或者

```bash
find -type f -size 24M
```

通用格式：

```bash
find [options] -size n[cwbkMG]
```

> 查找大小为 `n` 块的文件，其中 `+n` 意味着大于 `n` 块，`-n` 意味着小于 `n` 块，`n`（不带任何符号）意味着恰好为 `n` 块。

块大小：

- `c`: 字节 (bytes)
- `w`: 2 字节
- `b`: 512 字节（默认）
- `k`: 1 KB
- `M`: 1 MB
- `G`: 1 GB

## 第 17.5 节：过滤路径

- `-path` 参数允许指定一个用于匹配结果路径的模式。该模式也可以匹配名称本身。

查找路径中任何位置（文件夹或名称）包含 `log` 的文件：

```bash
find . -type f -path '*log*'
```

查找名为 `log` 的文件夹内的文件（任意层级）：

```bash
find -type f -path '*/log/*'
```

查找名为 `log` 或 `data` 的文件夹内的文件：

```bash
find . -type f -path '*/log/*' -o -path '*/data/*'
```

查找排除 `bin` 文件夹内包含的文件：

```bash
find . -type f -not -path '*/bin/*'
```

查找所有排除在 `bin` 文件夹或 `log` 文件之外的文件：

```bash
find . -type f -not -path '*/log*' -not -path '*/bin/*'
```

## 第 17.6 节：按类型查找文件

查找文件，使用 `-type f` 标志

```bash
$ find . -type f
```

查找目录，使用 `-type d` 标志

```bash
$ find . -type d
```

查找块设备，使用 `-type b` 标志

```bash
$ find /dev -type b
```

查找符号链接，使用 `-type 1` 标志

```bash
$ find . -type 1
```

## 第 17.7 节：按特定扩展名查找文件

要在当前路径下查找特定扩展名的文件，可以使用以下 `find` 语法。它通过 `bash` 内置的 `glob` 结构来匹配所有具有 `.extension` 后名的名称。

```bash
find /directory/to/search -maxdepth 1 -type f -name "*.extension"
```

仅从当前目录查找所有 `.txt` 类型的文件，执行

```bash
find . -maxdepth 1 -type f -name "*.txt"
```

## 第 18 章：使用 `sort`

| 选项 | 含义 |
| :--- | :--- |
| `-u` | 使输出的每行唯一 |

`sort` 用于对行排序。

## 第 18.1 节：排序输出

`sort` 用于对行排序。

## 第 18.2 节：排序输出

`sort` 用于对行排序。

## 第 18.3 节：数值排序

`sort` 用于对行排序。

## 第 18.4 节：按键排序

如果我们有多个键，那么对于 `-k` 选项，我们需要指定排序开始的位置。

## 第 20 章：在此文档 (here documents) 和在此字符串 (here strings)

### 第 20.1 节：使用在此文档执行命令

```bash
ssh -p 21 example@example.com <<EOF
echo 'printing pwd'
echo '\$(pwd)'
ls -a
find '*.txt'
EOF
```

`$` 需要转义是因为我们不希望它被当前 `shell` 扩展，例如 `$(pwd)` 将在远程 `shell` 上执行。

另一种方法：

```bash
ssh -p 21 example@example.com <<'EOF'
echo 'printing pwd'
echo "$(pwd)"
ls -a
find '*.txt'
EOF
```

注意：结束的 `EOF` 应该位于行首（前面不要有空格）。如果需要缩进，当你在启动 heredoc 时使用 `<<`，可以使用制表符。请参考“缩进文档”和“限制字符串”示例获取更多信息。

### 第 20.2 节：在此文档的缩进

你可以使用制表符对在此文档内的文本进行缩进，此时你需要使用 `<<` 重定向运算符而不是 `<<`。

```bash
$ cat << EOF
	这是一个用制表符缩进的内容 \t。
	你不能用空格缩进，你必须使用制表符。
	Bash 会移除这些行之前的空格。
	__注意__：在复制此示例时，请确保将空格替换为制表符。
EOF
```

这是一个用制表符缩进的内容 `\t`。
你不能用空格缩进，你必须使用制表符。
`Bash` 会移除这些行之前的空格。
注意：在复制此示例时，请确保将空格替换为制表符。

这种用法的一个实际案例（如 `man bash` 中提到的）是在 `shell` 脚本中，例如：

```bash
if cond; then
	cat << EOF
		hello
		there
	EOF
```

为了更好的可读性，通常会对代码块（如此 `if` 语句）内的行进行如下缩进。如果没有 `<<-` 语法，我们将被迫像这样编写上面的代码：

```bash
if cond; then
	cat << EOF
hello
there
EOF
fi
```

这读起来非常不舒服，在更复杂的实际脚本中情况会更糟。

### 第 20.3 节：创建一个文件

在此文档的一个经典用法是通过输入其内容来创建一个文件：

```bash
cat > fruits.txt << EOF
apple
orange
lemon
EOF
```

在此文档是 `<< EOF` 和 `EOF` 之间的行。

该文档成为 `cat` 命令的输入。`cat` 命令只需输出其输入，使用输出重定向运算符 `>` 将其重定向到文件 `fruits.txt`。

结果 `fruits.txt` 文件将包含以下行：

```text
apple
orange
lemon
```

适用于输出重定向的规则：如果 `fruits.txt` 之前不存在，它将被创建。如果它已存在，它将被截断。

### 第 20.4 节：在此字符串

版本 ≈ `2.05b`

你可以像这样使用在此字符串为命令提供输入：

```bash
$ awk '{print $2}' <<< "hello world - how are you?"
world
```

```bash
$ awk '{print $1}' <<< "hello how are you
> she is fine"
hello
she
```

你也可以用在此字符串为 `while` 循环提供输入：

```bash
$ while IFS=" " read -r word1 word2 rest
> do
	echo "$word1"
> done <<< "hello how are you - i am fine"
hello
```

### 第 20.5 节：使用 `sudo` 运行多个命令

```bash
sudo -s <<EOF
```
