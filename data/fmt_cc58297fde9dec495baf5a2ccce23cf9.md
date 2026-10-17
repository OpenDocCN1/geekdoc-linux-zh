
# 高级 Bash 脚本指南

## 第 16 章 外部过滤器、程序和命令

### 查找 Shell 脚本

在给定目录查找和 Bash 脚本：

```bash
DIRECTORY=/usr/local/bin
KEYWORD=Bourne
# Bourne 和 Bourne-Again shell 脚本

file $DIRECTORY/* | grep $KEYWORD

# 输出:
# /usr/local/bin/burn-cd: Bourne-Again shell script text executable
# /usr/local/bin/burnit: Bourne-Again shell script text executable
# /usr/local/bin/cassette.sh: Bourne shell script text executable
# /usr/local/bin/copy-cd: Bourne-Again shell script text executable
#
```

### 示例 16-32. 从 C 程序中删除注释

```bash
#!/bin/bash
# strip-comment.sh: 去除 C 程序中的注释 (* */) 。

E_NOARGS=0
E_ARGERROR=66
E_WRONG_FILE_TYPE=67
if [ $# -eq "$E_NOARGS" ]
then
    echo "Usage: $basename $0 C-program-file" >&2 # 输出错误信息到 stderr。
    exit $E_ARGERROR
fi

# 测试文件类型是否正确。
type=$(file $1 | awk '{print $2, $3, $4, $5}')
# "file $1" 输出文件类型
# 然后 awk 移除第一个字段，即文件名
# 结果被赋值给变量 "type。"
correct_type="ASCII C program text"

if [ "$type" != "$correct_type" ]
then
    echo "此脚本仅作用于 C 程序文件。"
    echo
    exit $E_WRONG_FILE_TYPE
fi

# 一个相当晦涩的 sed 脚本：
sed 's/^\*/\d/\..*\*/\d' $1

# 如果你花几个小时学习基础知识，这很容易理解。

# 需要在 sed 脚本中多添加一行，以处理
# 代码行在同一行后面带有注释的情况。
# 这被留作一项非而易举的练习。

# 此外，上面的代码会删除带有 "/*" 的非注释行 . .
# 这并不是一个理想的结果。

exit 0
```

```bash
# 此行以下代码将不会执行，因为上面有 'exit 0'。
# Stephanie 建议如下所示：

usage() {
    echo "Usage: $basename $0 C-program-file" >&2
    exit 1
}

WEIRD=$(echo -n "$1")

[[ $# -eq 1 ]] || usage

case "$file" in
  "*C program text*") sed -e "s/*${WEIRD}.*/${WEIRD}/g;" | \
    tr -d '\n' | sed -ne 'p' | \
    tr '\n' ' '; 
    ;;
esac

# 这仍然会被这些内容欺骗：

# printf("*");

# 或 /* 嵌入注释 */

# 为了处理所有特殊情况（字符串中的注释、... 中的注释），

# 唯一的方法是编写解析器（使用 lex 或 yacc?）。

exit 0
```

### 命令查找工具

这会给出 `command` 的完整路径。这对于确定系统是否安装了某个特定的实用程序有用。

```bash
which rm
```

与 `which` 类似，`whereis` 不仅提供 `command` 的完整路径，还提供其手册页（`manpage`）。

```bash
whereis rm

/usr/share/man/man1/rm
```

`whatis command` 在 `whatis` 数据库中查找 `command`。这对于识别系统命令和配置文件非常有用。考虑一个简化的命令。

```bash
whatis (1) - 在 whatis 数据库中搜索完整单词
```

**示例 16-13. 探索 whatis**

```bash
#!/bin/bash

# /bin 中所有神秘的二进制文件是什么？

DIRECTORY="/usr/bin"

# 也可以尝试 "/bin", "/usr/local"

# 遍历所有文件

for file in $DIRECTORY/*
do
    whatis $file # 输出文件的 whatis 信息
done

exit 0
```

### 文件工具

显示符号链接指向的。

```bash
readlink
```

使用 `strings` 命令查找二进制或数据文件中的可打印字符串。这可能对于快速检查转储文件或查看未知图像文件有用。在脚本中，你可能会用 `grep` 或 `sed` 解析 `strings` 的输出。

### 比较

**`diff`, `patch`**: 灵活的文件比较工具。它按顺序逐行比较目标文件。在应用中，如比较单词字典，这可能有助于通过 `sort` 和 `uniq` 管道过滤文件并将其传递给 `diff`。**`diff file-1 file-2`** - 输出文件中不同的行，并用插入符号显示每个特定行属于哪个文件。

**`diff`** 的 **side-by-side**（并列）选项将每个比较的文件按行输出，分列对齐在单独的列中，并标记不匹配的行。`-c` 和 `-u` 选项同样让命令的输出更易解释。

`diff` 有一些可用的花哨界面，如 `sdiff`, `wdiff`, `xdiff` 和 `mgdiff`。

> `diff` 命令如果所比较的文件完全相同，则返回退出代码 `0`；如果它们不同（或正在比较 2 个二进制文件），则返回其他。这允许在 shell 脚本的测试结构中使用 `diff`（见下文）。
> `diff` 的常见用途是生成用于 `patch` 的文件。`-e` 选项输出适用于 `ed` 或 `ex` 脚本的内容。

`patch`: 文件版本控制工具。给定由 `diff` 生成的差异文件，`patch` 可以将软件包旧版本升级到新版本。与发布整个新修订的包相比，发布一个较小的“diff”文件要方便得多。内核“补丁”已成为发布 Linux 内核频繁更新的首选方法。

```bash
patch -p1 < patch-file
```

**第 16 章 外部过滤器、程序和命令**

为内核打补丁：

```bash
cd /usr/src
gzip -cd patchXX.gz | patch -p0

# 使用 'patch' 升级内核源码
```

**`diff`** 命令可以递归地比较目录（比较其中存在的文件）。

```bash
bash$ diff -r ~/notes1 ~/notes2

Only in /home/bozo/notes1: file02
Only in /home/bozo/notes1: file03
Only in /home/bozo/notes2: file04
```

使用 **`diff`** 比较经过 `gzip` 压缩的文件。

**`diff`** 的扩展版本，可同时比较三个文件。该命令在成功执行后返回退出值 `0`，但遗憾的是这没有提供任何比较结果的信息。

`diff3`. `merge`

**`merge`**（三路文件）命令是 **`diff3`** 的一个有趣的补充。它的语法是 **`merge file1 file2`**。结果是 `merge file1` 合并从 `file2` 产生的更改。此命令创建了 **`patch`** 的精简版本。

`sdiff`

比较/并编辑两个文件以将它们合并到一个输出文件中。由于其交互性质，这在脚本中几乎没有用处。

`cmp`

**`cmp`** 是 **`diff`** 的简单版本，而 **`diff`** 报告两个文件之间的差异，**`cmp`** 仅显示它们在何处不同。

与 **`diff`** 一样，如果比较的文件完全相同，**`cmp`** 返回退出状态 `0`，如果不同则返回 `1`。这允许在 shell 脚本的测试结构中使用。

**示例 16-35. 使用 `cmp` 在脚本中比较两个文件。**

```bash
#!/bin/bash

# file-comparison.sh

ARGS=2 # 预期脚本两个参数。

E_BADARGS=5

E_UNREADABLE=86

if [ $# -ne "$ARGS" ];
then
    echo "Usage: $(basename $0) file1 file2"
    exit $E_BADARGS
fi

if [ ! -r "$1" ] || [ ! -r "$2" ]
then
    echo "两个要比较的文件必须存在且可读的。"
    exit $E_UNREADABLE
fi

cmp $1 $2 /dev/null

# 重定向到 /dev/null 隐藏了 "cmp" 命令的输出。

# cmp -s $1 $2 结果相同 "-s" 是 "cmp" 的静默标志

# 感谢 Anders Gustavson 指出这一点。

# 同样适用于 "diff"

diff $1 $2 /dev/null

if [ $? -eq 0 ];
then
    echo "文件1 和文件2 相同"
else
    echo "文件1 和文件2 不同"
fi
```

### 校验数据库脚本

```bash
check_database ()
{
  local n=0
  local filename
  local checksum

  # 这个文件检查本是不必要的，

  # 但防患于未然为好。

  if [ ! -r "$dbfile" ];
  then
    echo "无法读取校验和数据库文件!"
    exit $E_BAD_DBFILE
  fi

  while read -a record
  do
    directory_checked="${record[0]}"

    if [ "$directory_checked" != "$directory" ];
    then
      echo "目录不匹配!"

      # 尝试对不同的目录使用文件。

      exit $E_DIR_MATCH
    fi

    if [ "$n" -gt 0 ]; # 不是目录名。
    then
      filename[n]=$(echo "${record[n]}" | awk '{ print $2}')

      # mdsum 逆序写入记录，

      # 先写入校验和，然后是文件名。

      checksum[n]=$(mdsum "${filename[n]}")
    fi

    if [ "${record[n]}" = "${checksum[n]}" ];
    then
      echo "${filename[n]} 未发生变化。"

    elif [ "$(basename ${filename[n]})" != "$dbfile" ]; then
      # 跳过校验和数据库文件，

      # 因为它每次调用脚本时都会变化。

    # 遗憾的是，当在 $PWD 上运行此脚本时，

      # 对校验和数据库文件的篡改将无法检测到。

      # 练习：修复这个问题。

      then
        echo "${filename[n]} : 校验和错误!"

        # 文件自上次检查以来已更改。

      fi
    fi

    let "n+1" # 从校验和数据库文件中读取。

  done < "$dbfile";
}

############################################################

main () {

if [ -z "$1" ]

then
    directory="$PWD"    # 如果未指定，

else
    directory="$1"      # 使用当前工作目录。

fi

clear

echo " 正在 $directory 执行文件完整性检查"

echo

############################################################

if [ ! -r "$dbfile" ]; # 需要创建数据库文件吗？

then
```
