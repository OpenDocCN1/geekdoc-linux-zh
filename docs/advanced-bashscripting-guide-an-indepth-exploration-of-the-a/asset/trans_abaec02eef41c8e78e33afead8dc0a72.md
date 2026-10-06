
```bash
ls -l &
echo "Done."
wait
bash$ ./test.sh
Done.
[bozo@localhost-test-scripts]$ total 1
-rwxr-xr-x 1 bozo bozo 34 Oct 11 15:09 test.sh
```

将命令输出重定向到文件甚至 `/dev/null`。

**suspend**

这与 Control-Z 的效果类似，但它会暂停 shell（shell 的父进程）。你可以在适当的时间恢复它。

**logout**

退出登录 shell，可以选择指定退出状态。

**times**

给出执行命令时使用的系统时间统计，格式如下：

```
0m0.020s 0m0.020s
```

这种能力价值有限，因为对 shell 脚本进行分析和基准测试并不常见。

**kill**

通过向进程发送适当的终止信号来强制终止进程（参见示例 13–4）。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_144_0.png)

`kill -1` 列出所有信号。`kill -9` 是“强杀”，通常会终止顽固拒绝普通 `kill` 杀死的进程。有时 `kill -15` 有效。“僵尸进程”是指父进程已终止（你无法杀死它），且无法被杀死（已经死亡），但系统通常迟晚会清理它。

**command**

`command COMMAND` 会禁用命令 "COMMAND" 的所有别名和函数。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_144_1.png)

这是影响脚本命令处理的三个 shell 指令之一。另外两个是 `builtin` 和 `enable`。

**builtin**

# 11.1. 作业控制命令

# 高级 Bash 脚本指南

调用 **builtin** `BUILTIN_COMMAND` 会作为 shell 内置命令运行命令 "BUILTIN_COMMAND"，临时禁用同名的函数和外部系统命令。

**enable**

这用于启用或禁用 shell 内置命令。例如，`enable -n` 会禁用 shell 内置的 `kill`，因此当 Bash 随后遇到 kill 时，它会调用 `/bin/kill`。

`enable` 的 `-a` 选项列出所有 shell 内置命令，并指示它们是否已启用`-f` 文件选项允许从编译的对象的文件作为共享库（DLL）模块加载。[127]

**autoload**

这是 **ksh** 自动加载器在 Bash 中的移植。使用 `autoload` 后，带有 "autoload" 声明的函数将在首次调用时从外部文件加载。[28] 这节省了系统资源。

注意 `autoload` 不是 Bash 核心安装的一部分。它需要通过 `enable -f` 加载。

# 表 11–1 作业标识符

| 符号 | 含义 |
|--- |--- |
| %N | 作业号 [N] |
| %S | 作业启动（命令行）以字符串 S 开头 |
| ?S | 作业启动（命令行）包含字符串 S |
| %# | “当前”作业（上一个在前台停止或在后台启动的作业） |
| %+ | “当前”作业（上一个在前台停止或在后台启动的作业） |
| %- | 上一个作业 |
| %! | 上一个后台进程 |

# 11.1. 作业控制命令

# 第 12 章. 外部过滤器、程序和命令

标准的 UNIX 命令让 shell 脚本更加灵活。脚本的威力源于系统命令、shell 指令与简单编程构造的结合。

# 12.1 基础命令

# 命令列表

基础的文件“列出” (list) 命令。人们很容易低估这个谦逊命令的力量。例如，使用递归选项 `-R`，`ls` 可以提供目录结构的树形列出。其他风趣的选项还有 `-s`（按文件大小排序）、`-t`（按修改时间排序）和 `-i`（显示文件 inode，参见示例 12-3）。

示例 12-1. 使用其为刻录 CDR 创建目录

```bash
#!/bin/bash

SPEED=2                # 如果你的硬件支持，可以使用更高速度
IMAGEFILE=cdimage.iso
CONTENTSFILE=contents
DEFAULTDIR=/opt       # 确保此目录存在。

# 自动化刻录 CDR 的脚本。

# 使用 Josef Schilling 的 "cdrecord" 包。
# (http://www.fokus.de/ntyp/employees/schilling/cdrecord.html)

# 如果以普通用户调用此脚本，需要以 root 身份执行 sudo cdrecord
+# chmod u+s /usr/bin/cdrecord )

if [ -z "$1" ];
then
    IMAGE_DIRECTORY=$DEFAULTDIR
    # 如果命令行未指定，则使用默认目录。
else
    IMAGE_DIRECTORY=$1
fi

ls -lRF $IMAGE_DIRECTORY
# ... (此处省略脚本后续逻辑，原文存在重复且逻辑混乱)
```
