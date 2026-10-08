

# 高级 Bash 脚本指南

```bash
# 3) 最后一个变量获取行的剩余部分。
# 4) 如果需要设置的变量比文件第一行中空白分隔的字符串
#   多，则多余的变量将保持为空。

echo "----------------------------------------------------------------------"
```

```bash
# 如何使用循环解决上述问题：
while read line; do
  echo "$line"
done <data-file
#  Heiner Steven 指出这一点。

echo "----------------------------------------------------------------------"
```

```bash
# 使用 IFS（内部字段分隔符变量）来将输入行拆分
# 给 "read" 命令，如果你不希望默认使用空白作为分隔符。

echo "所有用户列表"
IFS=$IFS; IFS=":" # /etc/passwd 使用 ":" 作为字段分隔符。
while read name passwd uid fullname ignore; do
  echo "$name ($fullname)"
done </etc/passwd  # I/O 重定向。
IFS=$IFS  # 恢复原始的 $IFS。
# 此代码段由 Heiner Steven 增加。
```

```bash
# 在循环内部设置 $IFS 变量
## 就可以消除了将原始 $IFS 存储
## 在临时变量中的需要。
# Dim Segebart 指出这一点。

echo "----------------------------------------------------------------------"
echo "所有用户列表"
```

```bash
while IFS= read name passwd uid fullname ignore; do
  echo "$name ($fullname)"
done </etc/passwd  # I/O 重定向。

echo
echo "\IFS still $IFS"
```

```bash
exit 0
```

将输出管道传输给 `read` 并使用 `echo` 设置变量将失败。

然而，管道传输 `cat` 的输出似乎是有效的。

```bash
cat file file2 |
while read line; do
  echo $line
done
```

但是，正如 Björn Eriksson 所示：

# 高级 Bash 脚本指南

示例 15-8. 从管道读取的问题

```bash
#!/bin/sh
# readpipe.sh
# 此示例由 Bjon Eriksson 贡献。

### shopt -s lastpipe

last="(null)"
cat $0 |
while read line; do
    echo "${line}"
    last=$line
done

echo
echo "\nall done, last: $last"
```

```bash
./readpipe.sh
#!/bin/sh
{last="(null")}
cat $0 |
while read line; do
    echo "${line}"
    last=$line
done
printf "\nall done, last: %s\n" "$last"
```

All done, last: (null)

变量 (last) 在循环/子壳内部设置，
但它的值不会在循环外持久化。
gendiff 脚本（通常在许多 Linux 发行版的 /usr/bin 中）将 `find` 的
输出通过管道传给 `while read` 结构。

```bash
find $1 -name "*$2" -o -name ".*$2" -print |
while read f; do
```

> 可以将文本粘贴到 `read` 的输入字段中（但不是多行！）。参见示例 A-38。

# 文件系统

cd

第 15 章。内部命令与内置函数

熟悉的 `cd` 切换目录命令用于脚本，当执行某个命令需要位于指定目录时。

```bash
cd /source/directory tar cf - . | (cd /dest/directory tar xpvf -)
来自上文 Alan Cox 的示例
```

- `cd` 的 `P`（物理）选项导致它忽略符号链接。
- `cd -` 切换到 `$PWD`，即上一个工作目录。

当 `cd` 遇到两个正斜杠时，其功能不符合预期。

```bash
bash$ cd //
bash$ pwd
```

输出理应该是 `/`。这在命令行和脚本中都是一个问题。

pwd

打印工作目录。此 `cd` 命令给出用户（或脚本）的当前目录（参见示例 15-9）。其效果对于读取内置变量 `$PWD` 的值是理想的。

pushd, popd, dirs
这些命令是用于工作目录书签的机制，是一种能够按顺序在目录之间来回移动的方法。使用一个压入栈来跟踪目录名。选项允许对目录栈进行各种操作。

> pushd dir-name 将 dir-name 推入目录栈（到栈顶），并同时将当前工作目录更改为 dir-name

popd 从目录栈中移除（弹出）栈顶目录路径，并同时将当前工作目录更改为现在栈顶的目录。

dirs 列出目录栈的内容（与 `$DIRSTACK` 变量对比）。成功的 `pushd` 或 `popd` 会自动调用 `dirs`。

在不硬编码目录名称的情况下更改当前工作目录的脚本可以充分利用这些命令。注意，在脚本内部可以访问隐式 `$DIRSTACK` 数组持有目录栈的内容。

# 示例 15-9. 更改当前工作目录

```bash
#!/bin/bash
dir1=/usr/local
dir2=/var/spool

push $dirs (列目录栈到标准输出)。
# 将自动执行 "Now in directory `pwd`。" # 使用反引号执行 'pwd'。
```

第 15 章。内部命令与内置函数

```bash
# 现在，在目录 'dir1' 中做一些
pushd $dir2
echo "Now in directory 'pwd'"

# 现在，在目录 'dir2' 中做一些
echo "The top entry in the DIRSTACK is $DIRSTACK"
popd
echo "Now back in directory 'pwd'"

# 现在，在目录 'dir1' 中做更多
popd
echo "Now back in original directory 'pwd'"
```

```bash
exit 0

# 如果你不执行 'popd' -- 然后退出脚本
# 你会在哪个目录？为什么？
```

# 变量

let

`let` 命令对变量执行算术运算。在许多情况下，它是 `expr` 的一个简单版本。

示例 15-10. 让它执行算术。

```bash
#!/bin/bash

let a=11      # 等同于 'a=11'
let a=+5       # 等同于 let a = a + 5
              # (双引号和空格使其具可读性。)
echo 11 + 5 = $a # 16

let a <<=3     # 等同于 let a = a << 3
echo "\$a" (-16) # 左移 3 位 = $a
              # 128

let a /=4      # 等同于 let a = a / 4
echo 128 / 4 = $a # 32

let a -=5      # 等同于 let a = a - 5
echo 32 - 5 = $a # 27

let a *=10     # 等同于 let a = a * 10
echo 27 * 10 = $a # 270

let a%%8       # 等同于 let a = a % 8
echo 270 modulo 8 = $a (270 / 8 = 33, 余数为 $a)
              # 6
```

```bash
# "let" 允许 C 风格运算符吗？
是的，就像 ((...)) 双括号结构一样。
```

```bash
let a++      # C 风格（后置）递增。
echo 6++ = $a # 6++ = 7
let a--        # C 风格递减。
```

