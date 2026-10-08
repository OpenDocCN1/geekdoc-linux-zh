

# 高级 Bash 脚本指南

八进制/十六进制常量的算术评估将在 `[[ ... ]]` 结构中自动进行。

在 `if` 之后，测试命令并不识别括号 `( )`，`[[ ]]` 是严格必要的。

```bash
dir=/home/bozo

if cd "$dir" 2>/dev/null; then # 2>/dev/null 隐藏错误信息
    echo "Now in $dir"
else
    echo "Can't change to $dir."
fi
```

"COMMAND" 返回 COMMAND 的退出状态。

同样，在 `test` 括号内的条件在与列表结构（list construct）结合使用时可以独立存在而无需 `if`。

```bash
var1=20
var2=22
[ "$var1" -ne "$var2" ] // echo $var1 不等于 $var2
home=/home/bozo
[ -d "$home" ] // echo $home 目录不存在。
```

`(( ))` 扩展并求值算术表达式。如果表达式求值为 0，它返回退出状态 1，或“false”（假）。非零表达式返回退出状态 0，或“true”（真）。这样做是为了与之前讨论过的 `test` 和 `[ ]` 结构对比。

第 7 章 测试

# 高级 Bash 脚本指南

示例 7-3. 使用 (()) 进行算术测试

```bash
#!/bin/bash
# arith-tests.sh
# 算术测试。
```

```bash
# (( ... )) 结构求值并测试数值表达式。
# 退出状态与 [ ... ] 结构相反！
```

```bash
(( 0))
echo "Exit status of \(( 0 ))" is $?
# 1
```

```bash
(( 1))
echo "Exit status of \(( 1 ))" is $?
# 0
```

```bash
(( 5 > 4))
echo "Exit status of \(( 5 > 4 ))" is $?
# true
```

```bash
(( 5 > 9))
echo "Exit status of \(( 5 > 9 ))" is $?
# false
```

```bash
(( 5 == 5))
echo "Exit status of \(( 5 == 5 ))" is $?
# (( 5 = 5 )) 产生错误信息。
```

```bash
(( 5 - 5))
echo "Exit status of \(( 5 - 5 ))" is $?
# 0
```

```bash
(( 1 / 2))
echo "Exit status of \(( 1 / 2 ))" is $?
# 除法结果 < 1。
# 四舍五入为 0。
```

```bash
(( 1 / 0 ))>/dev/null
echo "Exit status of \(( 1 / 0 ))" is $?
# 非法除以零。
```

```bash
# "2>/dev/null" 有什么影响？
# 如果移除它会发生什么？
# 尝试移除它，然后重新运行脚本。
```

```bash
# (( ... )) 在 if 测试中也很有用。
```

```bash
var1=5
var2=4
```

```bash
if (( var1 > var2 ));
then
    # 注意：不是 $var1, $var2。为什么？
    echo "$var1 is greater than $var2"
fi
# 5 大于 4
```

```bash
exit 0
```

## 7.2. 文件测试运算符

如果... 则返回真：

- -e 文件存在
- -a 文件存在

这在效果上与 -e 相同。它已被“废用”[34]，且不建议使用。

- -f 文件是普通文件（不是目录或设备文件）
- -s 文件大小不为零
- -b 文件是目录
- -c 文件是字符设备

```bash
device0="/dev/sda2" # / (根目录)
if [ -b "$device0" ]
then
echo "$device0 is a block device."
fi

# /dev/sda2 是一个块设备。
```

```bash
devicel=/dev/tty1 # PCMCIA 调制解调器卡
if [ -c "$devicel" ]
then
echo "$devicel is a character device."
fi

# /dev/tty1 是一个字符设备。
```

- -p 文件是管道

```bash
function show_input_type() {
  -p /dev/fd/0 && echo PIPE || echo STDIN
}
show_input_type "Input" # STDIN
echo "Input" | show_input_type # PIPE
# 示例由 Carl Anderson 感谢。
```

- -h 文件是符号链接

# 高级 Bash 脚本指南

file 是符号链接

- -S
- -t
file 是套接字

file（描述符）与终端设备关联

此选项可用于检查给定脚本中的 stdin [-t 0 ] 或 stdout [-t 1 ] 是否为终端。

- -r
- -w
file 读权限（对于运行测试的用户）
file 写入权限（对于运行测试的用户）
- -x
file 可执行权限（对于运行测试的用户）
- -g
文件或目录设置了 set-gid (sgid) 标记

如果目录设置了 sgid 标记，那么在该目录内创建的文件将属于该目录的组，而不一定属于创建文件用户的组。这对于一个组共享的目录可能很有用。

- -u
文件设置了 set-uid (suid) 标记

由 root 拥有并设置了 set-user-id 标记的二进制文件以 root 权限运行，即使是普通用户调用它。[35] 这对于访问系统硬件的可执行文件（如 pppd 和 cdrecord）非常有用。缺少 suid 标记，二进制文件将被非 root 用户调用。

```bash
-rwxrxr-t 1 root 178236 Oct 2 2000 /usr/sbin/pppd
```

设置了 suid 标记的文件在其权限中显示 s。

- -k
粘滞位 (sticky bit)

通常称为粘滞位的保存文本模式（save-text-mode）标记是一种特殊的文件权限。如果文件设置了此标记，该文件将保留在缓存内存中以便快速访问。[36] 如果目录上设置该标记，它将限制写入权限。设置粘滞位会在文件或目录列表权限上添加 t。这会将该目录中文件的访问或删除限制为这些文件的所有者。

| drwxrwxrwt 7 root 178236 Oct 2 2000 /usr/sbin/pppd |

（注：此处部分原文似乎存在乱码或重复片段，已根据上下文进行清理性翻译）

