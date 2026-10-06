

# 高级 Bash 脚本指南

此详细的“if-test”解释由 Stephane Chazelas 提供。

# 示例 7–1. 什么是真？

```bash
#!/bin/bash

echo
echo "Testing \"0\"
if [ 0 ] # 0
then
echo "0 is true."
else
echo "0 is false."
fi # 0 is true.

echo
echo "Testing \"1\"
if [ 1 ] # 1
then
echo "1 is true."
else
echo "1 is false."
fi # 1 is true.

echo
echo "Testing \"-1\"
if [ -1 ] # 负1
then
echo "-1 is true."
else
echo "-1 is false."
fi # -1 is true.

echo
echo "Testing \"NULL\"
if [ ] # 空条件（空条件）
then
echo "NULL is true."
else
echo "NULL is false."
fi # NULL is false.

echo
echo "Testing \"xyz\"
if [ xyz ] # 字符串
then
echo "Random string is true."
else
echo "Random string is false."
fi # Random string is true.

echo
echo "Testing \"\$xyz\"
if [ $xyz ] # 测试 $xyz 是否为空，但是...
# 它只是一个未初始化的变量。
then
echo "Uninitialized variable is true."
else
echo "Uninitialized variable is false."
fi
# Uninitialized variable is false.
echo
echo "Testing \-n \$xyz\"
if [ -n "$xyz" ]
# 更符合规范的写法。
then
echo "Uninitialized variable is true."
else
echo "Uninitialized variable is false."
fi
# Uninitialized variable is false.
echo
xyz=
# 已初始化，但被设置为空值。
echo "Testing \-n \$xyz\"
if [ -n "$xyz" ]
then
echo "Null variable is true."
else
echo "Null variable is false."
fi
echo
# 什么时候 "false" 是真的？
echo "Testing \$false\"
if [ "false" ]
# 看起来 "false" 仅仅是一个字符串。
then
echo "\$false\" is true." # 并且它测试为真。
else
echo "\$false\" is false.
fi
# "false" is true.
echo
echo "Testing \$false\" # 再次，未初始化的变量。
if [ "$false" ]
then
echo "\$false\" is true.
else
echo "\$false\" is false.
fi
# "false" is false.
# 现在，我们得到了预期的结果。
echo
0
```

练习。解释上述示例 7–1 的行为。

# 第 7 章. 测试

```bash
if [ condition-true ]
then
  command 1
  command 2
else
  # 可选（如果不需要可以省略）
  # 添加默认代码块，当原始条件测试为假时执行。
  command 3
  command 4
fi
```

在条件测试中，如果 `if` 和 `then` 位于同一行，必须用分号 `;` 结束 `if` 语句。`if` 和 `then` 都是关键字。关键字（或命令）开始语句，如果同一行有新语句，旧语句必须结束。

```bash
if [ -x "filename" ]; then
```

# Else if 和 elif

`elif` 是 `else if` 的缩写。其效果是在外部 `if` 内部嵌套一个 `if`。

```bash
if [ condition1 ]
then
  command1
  command2
elif [ condition2 ]
# 等同于 else if
then
  command4
else
  default
fi
```

`test condition-true` 结构与 `if [ condition-true ]` 完全等价。恰好，左括号 `[` 是一个调用 `test` 命令的标记。右括号 `]` 并不严格 way，但较新版本的 Bash 要求使用。`test` 是一个用于填充和比较字符串的 Bash 内置命令。因此，在 Bash 脚本中，`test` 不调用外部的 `/bin/test` 二进制文件（后者链接到 `/bin/[`）。

```bash
test is a shell builtin
[ is a shell builtin
[[ is a shell keyword
]] is not found
```

# 示例 7–2. [ ] 和 test 的等价性

```bash
#!/bin/bash
echo
if test -z "$1"
then
    echo "No command-line arguments."
else
    echo "First command-line argument is $1"
fi
exit 0
```

`([ ])` 结构是 `[ ]` 的 shell 等价物。这是采用自 ksh 的扩展命令。在 `[` 和 `]` 之间不会发生文件名扩展或单词分割，但存在参数扩展和命令替换。使用 `[[ ]]` 结构而不是 `[ ]` 可以防止脚本中的许多逻辑错误。例如，`&&`、`||` 和 `>` 运算符在 `[[ ]]` 测试中可以工作，尽管它们在 `[ ]` 结构中会报错。

```bash
file=/etc/passwd
if [ -e $file ]
then
    echo "Password file exists."
fi
```

# 测试

在 `if` 之后，测试命令或测试括号 `[ ]` 或 `[[ )) 并不是严格必要的。

```bash
dir=/home/bozo
if cd "$dir" 2>/dev/null; then
    echo "Now in $dir."
else
    echo "Can't change to $dir."
fi
```

“if COMMAND” 结构返回 `COMMAND` 的退出状态。同样，测试括号内的条件可以脱离 `if` 独立存在，与列表结构结合使用。

```bash
var=20
var=22
[ "$var" -ne "$var" ] && echo "$var"

home=/home
[ -d "$home" ] || echo "home not exist."
```

`(( ))` 展开并评估算术表达式。如果表达式为零，则返回退出状态 1（假）；非零表达式返回退出状态 0（真）。这与之前讨论的 `test` 和 `[ ]` 形成对比。

# 示例 7–3. 使用 (( )) 进行算术测试

```bash
#!/bin/bash
# 算术测试。

# (( )) 结构评估数值表达式。
# 状态与 [ ] 结构相反！

(( 0 )) && echo "Exit status of ((0 ))" is $?" # 1
(( 1 )) && echo "Exit status of ((1 ))" is $?" # 0

(( 5 > 4 ))              # true
echo $?               # 0

(( 5 > 9 ))              # false
echo $?               # 1
```

# 7.2. 文件运算符

如果满足以下条件返回真：

- -e: 文件存在
- -f: 是普通文件（不是目录或设备文件）
- -s: 文件大小不为零
- -d: 是目录
- -b: 是块设备（软磁盘、光驱等）
- -c: 是字符设备（键盘、调制解调器、声卡等）
- -p: 是管道
- -h: 是符号链接
- -L: 是符号链接
- -S: 是套接字
- -t: 文件（描述符）与终端设备关联。此选项用于检查给定脚本的 stdin (`[-t 0]`) 或 stdout (`[-t 1]`) 是否为终端。
- -r:具有读取权限（对于运行测试的用户）
- -w: 文件具有写入权限（对于运行测试的用户）
- -x: 文件具有执行权限（对于运行测试的用户）
- -g: 文件或目录设置组 ID (sgid) 标志。如果目录设置了 sgid 标志，则在该其中创建的文件属于该目录的组，而不是创建用户的组。这对于工作组共享的目录可能有用。
- -u: 文件设置用户 ID (suid) 标志。带有 suid 标志的 root 二进制文件即使由普通用户调用也会以 root 权限运行。这对于需要访问系统硬件的可执行文件（如 pppt 和 cdrecord）非常有用。缺少 suid 标志会导致这些二进制文件无法被非 root 用户调用。带有 suid 标志的文件在权限中显示 s。
- -k: 设置了粘位。通常被称为“粘位”，是一种特殊的文件权限。如果文件设置了此标志，该文件将保留在缓存内存中以便快速访问。如果在目录上设置，它将限制写入权限。设置粘位会在文件或目录列表上添加 t。
- -O: 你是文件的所有者
- -G: 文件的组 ID 与你的相同
- -m: 文件自上次读取以来被修改过

