
# 高级 Bash 脚本指南

exit 0
可选地，`wait` 可以接受一个任务标识符作为参数，例如 `wait $!` 或 `wait $PPID`。
[67] 查看任务 ID 表。

在脚本内部，使用和符号 `&` 在后台运行命令可能会在按下回车后导致脚本挂起。这似乎发生在向 `stdout` 写入内容的命令上。这可能是一个非常困扰的问题。

```bash
#!/bin/bash
# test.sh

ls -l &
echo "Done."
bash$ ./test.sh
Done.
[bozo@localhost test-scripts]$ total 1
-rwkr-xr-x 1 bozo 34 Oct 11 15:09 test.sh
```

正如 Walter Brameld IV 所解释的：

据我所知，这类脚本并没有真正挂起。它们看起来像挂起了，是因为后台命令在提示符之后向控制台写入了文本。用户认为提示符从未显示。以下是事件发生的顺序：

1. 脚本启动后台命令。
2. 脚本退出。
3. Shell 显示提示符。
4. 后台命令继续运行并向控制台写入文本。
5. 后台命令完成。
6. 用户在输出底部没有看到提示符，导致看起来像挂起了。

在后台命令后重定向 `wait` 似乎可以解决这个问题。

```bash
#!/bin/bash
# test.sh

ls -l &
echo "Done."
wait
bash$ ./test.sh
Done.
[bozo@localhost test-scripts]$ total 1
-rwkr-xr-x 1 bozo 34 Oct 11 15:09 test.sh
```

将命令的输出重定向到文件甚至 `/dev/null` 也能解决这个问题。

这与 `Control-Z` 具有类似的效果，但它会挂起 shell（shell 的父进程会在适当的时间恢复它）。

15. 内置命令与内置函数

212

# 高级 Bash 脚本指南

logout
退出登录 shell，可选地指定退出状态。

times
提供执行命令时经过的系统时间统计，格式如下：

```
0m0.020s 0m0.020s
```

此功能价值相对有限，因为在脚本执行期间并不常见性能分析和基准测试。

kill
通过发送适当的终止信号强制终止进程（参见示例 17-6）。

示例 15-27. 一个自杀的脚本

> kill -1 列出所有信号（与文件 /usr/include/asm/signal.h 相同）。
> -9 是强制强杀，它通常会终止那些顽固拒绝被普通 `kill` 杀死的进程。有时，`kill -15` 有用。僵尸进程是一个已经终止但无法被注销用户杀死的进程——你无法杀死已经死的东西，`init` 早晚会清理它。

killall
按名称而非进程 ID 命令运行中的进程。如果运行了特定命令的多个实例，对命令执行 `killall` 将终止它们。

> 这指的是 `/usr/bin` 中的 `killall` 命令，而不是 `/etc/rc.d/init.d` 中的 `killall` 脚本。

command
该命令直接禁用紧随其后的命令的别名和函数。

```bash
bash$ command ls
```

这是影响命令处理的三个 shell 指令之一。另外两个是 `builtin` 和 `enable`。

调用 `builtin BUILTIN_COMMAND` 将作为 shell内置运行 `BUILTIN_COMMAND`，临时禁用同名的函数和外部系统命令。

这启用或禁用 shell内置命令。例如，`enable -n kill` 禁用内置的 `kill`，这样 Bash 随后遇到 `kill` 时，会调用外部命令 `/bin/kill`。

`enable` 的 `-a` 选项列出所有 shell内置，指示它们是否已启用。`-f` 选项允许从经过编译的对象文件作为动态库 (DLL) 模块加载内置。[68]

这是 ksh 自动加载器的移植。有了 `autoload`机制，带有 `autoload` 声明的函数将在第一次调用时从外部文件加载。[69] 这节省了系统资源。

注意 `autoload` 不是 Bash 核心的一部分。它需要通过 `enable -f` 加载（见上文）。

# 表 15-1 任务标识符

| 符号 | 含义 |
|---|---|
| %N | 任务编号 [N] |
| %S | 以字符串 S 开头的任务调用（命令行） |
| %S | 包含字符串 S 的任务调用（命令行） |
| %% | “当前”任务（最后一个在前台停止或在后台启动的任务） |
| %+ | “当前”任务（最后一个在前台停止或在后台启动的任务） |
| %- | 上一个任务 |
| $% | 上一个后台进程 |

# 16. 外部过滤器、程序和命令

标准的 UNIX 命令让 shell 脚本更加灵活。脚本的力量源于系统命令、shell 指令与简单编程结构的结合。

# 16.1 基础命令

初学者学习的命令

ls

基础的文件“列出”命令。很容易低估这个简陋命令的力量。例如，使用递归选项 `-R`，`-l` 提供了目录结构的树状列表。其他实用的选项有 `-S`（按大小排序）、`-t`（按修改时间排序）、`-v`（按文件名嵌入的数字版本排序）、`-b`（显示转义字符）以及 `-i`（显示文件节点，参见示例 16-4）。

```bash
bash$ ls -l
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter10.txt
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter11.txt
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter12.txt
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter1.txt
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter2.txt
-rw-r--r-- 1 bozo bozo 0 Sep 14 18:44 chapter3.txt
```
