
确保已安装的文件具有正确的所有权和权限。如果没有这些选项，使用 `tar` 将使用上游创建者的值安装软件包文件。

### 6.51.2. Python 3 内容

已安装的程序：`2to3`, `idle3`, `pip3`, `pydoc3`, `python3`, `python3-config`, 和 `pyvenv`

已安装的库：`libpython3.7so` 和 `libpython3.so`

已安装的目录：`/usr/include/python3.7m`, `/usr/lib/python3` 和 `/usr/share/doc/python-3.7.4`

#### 简述

- `2to3` 是一个 Python 程序，读取 Python 2.x 源代码并应用一系列修复将其转换为有效的 Python 3.x 代码。
- `idle3` 是打开 Python GUI 编辑器的封装脚本。要运行此脚本，你必须在安装 Python 之前安装 Tk，这样才能构建 Tkinter Python 模块。
- `pip3` Python 的包安装器。你可以使用 `pip` 从 Python Package Index 以及其他索引安装包。
- `pydoc3` 是 Python 文档工具。
- `python3` 是一种解释性的、交互式的、面向对象的编程语言。
- `pyvenv` 在一个或多个目标目录中创建虚拟 Python 环境。

## 52. Ninja-1.9.0

Ninja 是一个专注于速度的小型构建系统。

预计编译时间：0.2 SBU
所需磁盘空间：69 MB

### 52.1. 安装 Ninja

当 Ninja 运行时，它通常会并行运行最大数量的进程。默认情况下，这是系统核心数加二。在某些情况下，这会导致 CPU 过热或系统内存耗尽。如果从命令行运行，传递 `-j` 参数将限制并行进程的数量，但某些软件包允许执行 `ninja` 且不传递 `-j` 参数。

使用可选步骤允许用户通过环境变量 `NINJAJOBS` 限制并行进程数。例如，设置：

```bash
export NINJAJOBS=4
```

将限制 `ninja` 限制为四个并行进程。

如果需要，运行以下命令添加使用环境变量 `NINJAJOBS` 的能力：

```bash
sed -i '/int Guess a/ \
int j = 0;\
char* jobs = getenv("NINJAJOBS");\
if (jobs != NULL) j = atoi(j);\
if (j > 0) return j;\
'src/ninja.cc
```

使用以下命令构建 Ninja：

```bash
python3 configure.py --bootstrap
```

构建选项的含义：

```bash
--bootstrap
此参数强制 ninja 为当前系统进行重新构建。
```

要测试结果，执行：

```bash
.ninja ninja_test
./ninja_test --git-filter=SubprocessTest.SetWithLots
```

安装软件包：

```bash
install -vm7555 ninja
```

# Linux From Scratch - 版本 9.0

- `bsum` 打印或检查 BLAKE2 (512-bit) 校验和
- `basename` 从文件名中删除任何路径和指定的后缀
- `basenc` 使用各种算法对数据进行编码或解码
- `cat` 将文件连接到标准输出
- `chcon` 更改文件和目录的安全上下文
- `chgrp` 更改文件和目录的组所有权
- `chmod` 将每个文件的权限更改为指定的模式；模式可以是要进行更改的符号表示，也可以是表示新权限的八进制数
- `chown` 更改文件和目录的用户/或组所有权
- `chroot` 以指定的目录作为 / 目录运行命令
- `cksum` 打印每个指定文件的循环冗余检查 (CRC) 校验和和字节数
- `comm` 比较两个排序后的文件，以三列形式输出唯一的行以及相同的行
- `cp` 复制文件
- `split` 将给定的文件拆分为多个新文件，根据给定的模式或行号进行分割，并输出每个新文件的字节数
- `cut` 打印行的部分，根据给定的字段或位置选择部分
- `date` 以给定的格式显示当前时间，或设置系统日期
- `dd` 使用块大小和计数复制文件，同时可以对其执行转换
- `df` 报告挂载文件系统的可用（及已用）磁盘空间，或仅报告持有所选文件的文件系统
- `dir` 列出每个给定目录的内容（与 `ls` 命令相同）
- `dircolors` 输出设置 `LS_COLOR` 环境变量的命令，以更改 `ls` 使用的颜色方案
- `dirname` 从文件名中删除非目录后缀
- `du` 报告当前目录、每个给定目录（包括所有子目录）或每个给定文件使用的磁盘空间
- `echo` 显示给定的字符串
- `env` 在修改的环境中运行命令
- `expand` 将制表符转换为空格
- `expr` 评估表达式
- `factor` 打印所有指定整数的质因数
- `false` 什么都不做，且执行失败；它始终以一个表示失败的状态码存在
- `fmt` 重新格式化给定文件中的段落
- `fold` 折叠给定文件中的行
- `groups` 报告用户的组成员关系
- `head` 打印每个给定文件的前十行（或指定的行数）
- `hostid` 报告主机的数字标识符（十六进制）
- `id` 报告当前用户或指定用户的有效用户 ID、组 ID 和组成员关系
- `install` 复制文件并设置其权限模式，如果可能，还设置其所有者和组
- `sha256sum` 打印 256 位安全哈希算法校验和
- `sha384sum` 打印 384 位安全哈希算法校验和
- `sha512sum` 打印 512 位安全哈希算法校验和
- `shred` 用复杂模式反复覆盖给定文件，使数据难以恢复
- `shuf` 打乱文本行的顺序
- `sleep` 暂停指定长度的时间
- `sort` 对给定文件的行进行排序
- `split` 按大小或行数将给定的文件拆分
- `stat` 显示文件或文件系统状态
- `stdbuf` 以更改其标准流的缓冲操作的方式来运行命令
- `stty` 设置或报告终端行设置
- `sum` 打印每个给定文件的校验和和块计数
- `sync` 刷新文件缓冲区；它将块写入磁盘并更新超级块
- `tac` 反向顺序连接给定的行
- `tail` 打印每个给定文件的最后十行（或指定的行数）
- `tee` 从标准输入读取并同时写入标准输出和给定文件
- `test` 比较值并检查文件类型
- `timeout` 在时间限制内运行命令
- `touch` 修改时间戳，将给定文件的访问和修改时间设置为当前时间；不存在的文件将创建为零长度
- `tr` 从标准输入翻译、挤压并删除给定的字符
- `true` 什么都不做，且执行成功；它始终以一个表示成功的状态码退出
- `truncate` 将文件缩小或扩展到指定大小
- `sort` 执行拓扑排序；它根据给定文件中的部分序关系写入一个完全排序的内容
- `tty` 报告连接到标准输入的终端文件名
- `uname` 报告系统信息
- `unexpand` 将空格转换为制表符
- `uniq` 丢弃连续相同行中的其余行
- `unlink` 删除给定的文件
- `users` 报告当前登录的用户名
- `vdir` 等于 `-l`
- `wc` 报告每个给定文件的行数、单词数和字节数，当给出多个文件时报告总行数
- `who` 报告谁登录了
- `whoami` 报告与当前有效用户 ID 关联的
- `yes` 重复输出“y”或给定的字符串直到被杀死为止
- `libstdbuf` `stdbuf` 使用的库

## 6.55. Check-0.12.0

Check 是一个 C 语言的单元测试框架。
近似编译时间：0.1 SBU（带有测试约需 3.7 SBU）
需要的磁盘空间：12 MB

### 6.55.1. 安装 Check

为编译准备 Check：

```bash
./configure --prefix=/usr
```

构建包：

```bash
make
```

编译现在已完成。要运行 Check 测试套件，执行以下命令：

```bash
make check
```

注意，Check 测试套件可能需要较长时间（多达 4 SBU）。
安装包并修复脚本：

```bash
make docdir=/usr/share/doc/check-0.12.0 install
sed -i '1 s/$tools/usr/' /usr/bin/checkmk
```

### 6.55.2. Check 的内容

已安装程序：`checkmk`
已安装的库：`libcheck.{a,so}`

#### 简短描述

- `checkmk`: 用于配合 Check 单元测试框架 `libcheck.{a,so}` 生成 C 单元测试的 Awk 脚本。包含允许从测试程序中调用 Check 的函数

## 6.56. Diffutils-3.7

Diffutils 包包含显示文件或目录之间的程序。

近似编译时间：0.4 SBU
需要的磁盘空间：36 MB

### 6.56.1. 安装 Diffutils

为编译准备 Diffutils：

```bash
./configure --prefix=/usr
```

编译包：
```bash
```
