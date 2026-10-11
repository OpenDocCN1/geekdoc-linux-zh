
```csh
if (-o $1) then
echo "你拥有 $1"
else
echo "你并不拥有 $1"
```
```csh
if (-r $1) then
echo "$1 可读"
else
echo "$1 不可读"
```
```csh
if (-w $1) then
echo "$1 可写"
else
echo "$1 不可写"
```
```csh
if (-x $1) then
echo "$1 可执行"
else
echo "$1 不可执行"
```

这是一个测试文件的极有些极端的例子；但是，想要包含许多文件测试。

## Shell 编程

以下是使用 `.profile` 作为输入的 `filetest` 输出：

```
martyp filetest /home/martyp/.profile
/home/martyp/.profile 存在
/home/martyp/.profile 不是零长度
/home/martyp/.profile 是文件
/home/martyp/.profile 不是目录
/home/martyp/.profile 可读
/home/martyp/.profile 可写
```

在 `.profile` 上运行 `filetest` 的结果产生了我们预期的文件结果。下一节介绍了使用 `switch` 进行决策的方法。

你可以使用 `switch` 在 Shell 程序中进行决策。你可以使用 `switch` 测试命令行参数或交互式输入，如后续示例所示。例如，你想在 Shell 程序中创建一个菜单，并确定用户在运行此 Shell 时选择了哪个选项，你可以使用 `switch`。`switch` 的语法如下：

```csh
switch (pattern_to_match)
case pattern1
    commands
case pattern2
    commands
default
    commands
```

## 第23章 Shell 编程简介

`pattern_to_match` 是你正在测试的用户输入，如果它等于 `pattern1`，则执行 `pattern1` 下的命令。如果 `pattern_to_match` 和 `pattern2` 相同，则执行 `pattern2` 下的命令，依此类推。如果 `pattern_to_match` 与任何 `case` 模式都不匹配，则执行 `default`。以下程序允许你从菜单中选择脚本。这些是本章之前编写的 Shell 程序。你可以扩展此脚本以包含尽可能多的程序。此示例使用了 `switch`：

```csh
#!/bin/csh
# 运行你创建的一些 C 脚本的程序
# 用法: pick
echo "管理员"
echo "1 检查网络接口"
echo "2 检查连接"
echo "etc/hosts 文件"
echo "请输入你的选择"
set pick=$ # 读取脚本数量
switch ($pick) # 赋值给变量 pick
case 1
    $HOME/cshscripts/netcheck
case 2
    $HOME/cshscripts/hostck
default
    echo "下次请选择 1 或 2"
```

该程序允许我们在两个脚本之间选择。让我们来看运行该程序的示例：

```
martyp pickscript
  管理员菜单
1  检查网络接口
2  检查连接
     到 etc/hosts 文件
```

## C Shell 编程

你的那行代码出错了什么。在这种情况下，显然是我漏掉了一个右括号。

修复问题后，我可以使用 `-x` 参数运行程序，这会导致所有命令在执行之前立即回显。下面的示例展示了搜索程序的运行情况：

```
martyp $ csh -xv searchl shellprogs grep csh_hostck
if ( $argv != 3 ) then
if ( 3 != 3 ) then
  echo ""
  echo
  cd $1
  cd /home/martyp/shellprogs
  grep -n "$2" $3
  grep -n grep csh_hostck
25: /usr/sbin/ping $sys 64 1 | grep "is alive" > /dev/null
  echo ""
  echo
endif
endif
martyp $
```

你可以逐行跟踪正在发生的情况。以 25 开头的那行是文件 `csh_hostck` 文件中包含 `grep` 的那行，也就是说，如果你在不使用 `-xv` 选项的情况下运行程序，将会收到的输出。

我建议使用语法检查 (`-n`) 测试一个新的 shell 程序，只有在运行程序时得到意料之外的结果时，才使用 `-x` 选项显示所有命令。当你编写的 shell 程序遇到问题时，这些调试选项无疑会对你有所帮助。

![](img/6969df54e516231f8e64fd1177ac1127_1600_0.png)

## 需要多长时间？

你可以使用 `time` 命令来查看你的 shell 程序运行所需时间的报告。`time` 的输出在许多 UNIX 变体中不同。你可能想查看 `time` 的手册页以了解预期的输出。在 `csh` 中 `time` 的典型输出如图 23-5 所示：

```
sysl 1: time netcheck
1.3u 0.8s 0:03 70%    % of CPU to real time used
                               real time time to execute
n                               system time used
nuser time used
```
