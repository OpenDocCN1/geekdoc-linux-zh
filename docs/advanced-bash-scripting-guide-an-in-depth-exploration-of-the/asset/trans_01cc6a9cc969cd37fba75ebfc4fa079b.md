

# 高级 Bash 脚本指南

出于安全考虑，当前的“工作目录”`.` 通常会从 $PATH 中省略。

$PIPESTATUS 数组变量，用于存储最后执行的前台管道的退出状态（们）。

```bash
bash$ echo $PIPESTATUS
0

bash$ ls -al | bogus_command
bash: bogus_command: command not found
bash$ echo ${PIPESTATUS[1]}
127

bash$ ls -al | bogus_command
bash: bogus_command: command not found
bash$ echo $?
127
```

$PIPESTATUS 数组的成员持有管道中执行的每条命令的退出状态。$PIPESTATUS[0] 存储管道中第一个命令的退出状态，$PIPESTATUS[1] 存储第二个命令的退出状态，依此类推。

> $PIPESTATUS 变量在登录 shell 中可能包含一个错误的 0 值值（在 Bash 3.0 之前的版本中）。

```
tcsh$ bash
bash$ who | grep nobody | sort
bash$ echo ${PIPESTATUS[*]}
0
```

上述行包含在脚本中将产生预期的 0 1 0 输出。

感谢 Wayne Pollock 指出这一点并提供上述示例。

> $PIPESTATUS 变量在某些上下文中会意料之外的结果。

```bash
bash$ echo $BASH_VERSION
3.00.14(1)-release

bash$ ls | bogus_command | wc
bash: bogus_command: command not found
0 0 0

bash$ echo ${PIPESTATUS[@]}
141 127 0
```

Chet Ramsey 将上述输出归因于 ls 的行为。如果 ls 向一个输出未被读取的管道写入数据，则 SIGPIPE 会杀死它，退出状态为 141。否则，其退出状态为 0，正如预期所示。tr 也是如此。

> $PIPESTATUS 是一个“易变”变量。它需要在相关的管道执行后立即被捕获，在任何其他操作干预之前。

# 高级 Bash 脚本指南

```bash
bash$ ls bogus_command | wc
bash: bogus_command: command not found
0 0

bash$ echo ${PIPESTATUS[@]}
127 0
```

在 $PIPESTATUS 未给出预期结果的情况下，pipefail 选项可能有用。

- $PIPESTATUS[0] 存储管道中第一个命令的退出状态。
- $PIPESTATUS[1] 存储管道中第二个命令的退出状态。
- $PS1 是主提示符，显示在命令行上。
- $PS2 是次提示符，在预期额外输入时显示。
- $PS3 是三级提示符，在 select 循环中显示（参见示例 1）。
- $PS4 是四级提示符，在使用 -x 跟踪调用脚本时，显示在每行输出的开头。它显示为 "*"。

进程的 $PPID 是其父进程的进程 ID。

在 $PS4 中嵌入诊断信息可能是很有用的：$PS4=$(read time < /proc/stat; echo "$time")
# 根据 Erik 的选择而添加。

$PWD 工作目录（你所在的时间）
这是对 pwd 命令的别名。

```bash
#!/bin/bash
ECHO_DIRECTORY=5
clear the screen.
DIRECTORY=/home/projects/
cd
echo "Deleting stale files in $PWD"
if [ "$PWD" != "$DIRECTORY" ]; then
# 防止意外擦除目录。
fi
```

# 2. 变量的其他视角

# 高级 Bash 脚本指南

```bash
echo "Wrong directory!"
echo "In $PWD, rather than $DIRECTORY!"
echo "Bailing out!"
```

```bash
rm -rf * # 删除点文件。
rm -f .* # 移除以多个点开头的文件名。
# (shift -s dotglob; rm -f*) 同样有效。
# 感谢 S. 指出这一点。

# 文件名 'basename' 可能包含 0-255 范围内的所有字符，除了 ""。
# 删除带有特殊字符的文件是一个练习。（提示：rm -name 或 rm -weird）
result=$? # 删除操作的结果。如果成功 = 0。

ls -al # 还有留的文件吗？
echo "Done."
echo "Old files deleted in $DIRECTORY."
# 根据需要在此处进行各种操作。

exit $result
```

该值没有提供给 read。同样适用于 select 菜单，但仅提供所选变量的项编号，而不是值本身。

```bash
#!/bin/bash
# reply.sh

# REPLY 是 'read' 命令的默认值。

echo -n "What is your favorite vegetable? "
read
echo "Your favorite vegetable is $REPLY."
# 只有当没有提供变量时，REPLY 才会持有最后一个 "read" 的值。

echo -n "What is your favorite fruit? "
read fruit
echo "Your favorite fruit is $fruit."
echo ""
echo "Value of REPLY is still $REPLY."
# REPLY 仍然设置为它之前的值，因为变量 $fruit 吸收了新的 "read" 值。

exit 0
```

此脚本运行的秒数。

```bash
#!/bin/bash
```

# 第 9 章 变量的其他视角

# 高级 Bash 脚本指南

```bash
TIME_LIMIT=10
INTERVAL=1

echo "Hit Control-C to exit before $TIME_LIMIT seconds."

while [ "$SECONDS" -le "$TIME_LIMIT" ]; do
  # $SECONDS 是一个内部 shell 变量。
  if [ "$SECONDS" -eq 1 ]; then
    units=second
  else
    units=seconds
  fi

  echo "This has been running $SECONDS $units."
  # 在缓慢或过载的机器上，脚本可能会跳过每次计数。
  sleep $INTERVAL
done
echo -e "\a" # 哔！

exit 0
```

$SHELLTS 已启用选项列表，一个可读变量。

```bash
echo $SHELLTS
braceexpand:hashall:histext:monitor:history:interactive-comments:emacs
```

$SSHLLV Shell 嵌套深度。如果在命令行处，$SSHLLV 为 1，在脚本中将递增到 2。

> 此变量不受子 shell的影响。当你需要 嵌套指示时使用 $BASH_SUBSHELL。

$TMOUT TMOUT 环境变量设置为非零值时间，则 shell 提示将在 $shell 秒后超时。这会导致注销。

从 Bash 2.05b 开始，现在可以在脚本中结合 read 使用 $TMOUT。

```bash
#  Bash 2.05b 及更高版本的脚本。
TMOUT=3    # 提示三秒后超时。
echo "What is your favorite song?"
echo "Quickly now, you have only $TMOUT seconds."
```

# 第 9 章 变量的其他视角

# 高级 Bash 脚本指南

```bash
echo "Your song is $song."
```

脚本中还有其他更复杂的定时输入方法。

```bash
#!/bin/bash
# timeout-in-script.sh

# The pipefail 选项在 $PIPESTATUS 未给出预期结果的情况下可能有用。

# The pipefail 选项在 $PIPESTATUS 未给出预期结果的情况下可能有用。
```

