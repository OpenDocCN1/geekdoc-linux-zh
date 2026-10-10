
# Linux 编程入门指南 [电子资源]

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_0_0.png)

## Alan Cox 序

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_2_0.png)

# 关于 Neil

Neil Matthew 自 1974 年以来一直对计算机和编程感兴趣。他毕业于诺丁汉大学数学系，并对编程语言充满热情。

Neil Matthew 自 1993 年 8 月获得 `Linux` 软盘发行版 (`SLS`) 以来就使用了几乎所有的语言。他在家里和工作都会使用 `C`、`C++`、`Prolog`、`Tcl` 和 `Java`。

Neil 的大多数“家庭”项目最初是在 `Unix` 系统上开发的，但现在都已迁移到 `Linux`。

Neil 曾在 `Camel Electronics` 担任软件主管和首席工程师，使用 `C` 和 `C++` 开发实时嵌入式系统。从那时起他一直从事开发技术和质量保证工作。作为 `Celestio AG` 的顾问，他目前担任系统架构师。

Neil 的妻子是 Christine，有两个孩子 Alexandra 和 Adrian。他们住在英国诺丁汉郡的一座改造过的农场里。他的爱好包括计算机解谜、音乐、科幻小说、山地骑车以及不自己动手。

# 关于 Rick Stones

Rick 在学校时期就开始编程了，时间久到他自己记得，当时在一台搭载 `6502` 处理器的 `BBC` 微型计算机上进行。他毕业于诺丁汉大学电子工程专业，但发现软件开发更有趣。

多年来，他曾在各种公司工作过，从只有几个人的初创公司到大型企业都有涉及。他参与的 `IT` 服务项目涵盖了从实时通信到会计系统、大型帮助帮助台系统，以及最近作为 `EPO` 和零售中央系统的技术专家。

作为一名编程语言爱好者，他使用过各种语言，包括一种名为 `SL-1` 的私有电信语言、一些 `FORTRAN`、`Pascal`、`Perl`、`SQL` 以及少量的 `Python` 和 `C++`，还有 `C`。他承认自己曾精通 `Visual Basic`，但尽量不公开宣传这一弱点。

Rick 住在英国莱彻斯特郡的一个村庄，与他的妻子 Ann、孩子 Jennifer 和 Andrew 以及两只猫一起生活。在工作之余，他的主要爱好是古典音乐，尤其是早期宗教音乐，并尽力找时间练习钢琴。他目前正在学习德语。

# 致谢

- 作者
- 副总裁兼执行发行人：Bob Ipsen
- 执行编辑：Debra Williams Cauley
- 副总裁兼发行商：Joseph B. Wikert
- 开发编辑：James H. Russell
- 执行编辑总：Mary Bednarek
- 制作编辑：Pamela Hanley
- 项目协调员：Regina Snyder, April Farling
- 技术编辑：Arthur Griffith, Tobias DiPasquale
- 图形与制作专家：Steved Arany, Beth Brooks, Carrie Foster, Lauren McMullan, Kristin Seib
- 文字编辑：出版服务部
- 质量控制技术：Laura Albert, Andy Hollandbeck, Rob Springer
- 高级制作经理：Fred Bernardi
- 编辑经理：Mary Beth Wakefield
- 校对与索引：`TECHBOOKS Production Services`
- 副总裁兼执行集团发行商：Richard Swadley

Alan Cox 写的序言 xxxi
引言 xxxiii

# 第 1 章：入门 1

## UNIX、Linux 和 GNU 简介 1
### 什么是 UNIX? 2
### UNIX 简史 2
### UNIX 哲学 2
### 什么是 Linux? 3
### GNU 项目与自由软件基金会 3
### Linux 发行版 4

## Linux 编程 5
### Linux 程序 5
### C 编译器 6
### 尝试一下——我们的第一个 Linux C 程序 7
### 开发系统路线图 8
### 应用程序 8
### 头文件 8
### 库文件 9
### 静态库 10
### 尝试一下——静态库 10
### 共享库 12

## 获取帮助 13
### 尝试一下——手册页与 info 14
### 总结 15

# 第 2 章：Shell 编程 17

## 为什么用用 Shell 编程? 18
### 一点哲学 18
### 什么是 Shell? 19
### 管道与重定向 21
### 输出重定向 21
### 输入重定向 22
### 管道 23

## 作为编程语言的 Shell 23
### 交互式程序 23
### 创建脚本 25
### 使脚本具有执行权限 26

## Shell 语法 27
### 变量 28
### 引用 28
### 尝试一下——变量 29
### 环境变量 29
### 参数变量 30
### 尝试一下——参数和环境变量 31
### 条件 32
### `test` 命令或 `[` 命令 32
### 控制结构 35
### `if` 35
### 尝试一下——使用 `if` 命令 35
### `elif` 36
### 尝试一下——使用 `elif` 进行进一步检查 36
### 变量的问题 36
### `for` 37
### 尝试一下——固定字符串的 `for` 循环 38
### 尝试一下——带通配符扩展的 `for` 循环 38
### `while` 39
### 尝试一下——再次，再来 40
### `until` 41
### `case` 41
### 尝试一下——Case I：用户输入 42
### 尝试一下——Case II：组合模式 42
### 尝试一下——Case III：执行多个语句 43
### 列表 44
### 尝试一下——AND 列表 45
### 尝试一下——OR 列表 46
### 语句块 47
### 函数 47
### 尝试一下——简单函数 47
### 尝试一下——返回值 49

## 命令 50
### `break` 50
### `:` 命令 51
### `continue` 51
### 的 `.` 命令 52
### 尝试一下——点命令 53
### `echo` 53
### `eval` 54
### `exec` 54
### `exit n` 55
### `export` 55
### 尝试一下——导出变量 56
### `expr` 56
### `printf` 57
### `return` 58
### `set` 58
### `shift` 59
### `trap` 60
### 尝试一下——捕获信号 (`Trap Signals`) 60
### `unset` 62

## 两个实用的命令与正则表达式 62
### 尝试一下——带测试的 `find` 64
### 尝试一下——基础 `grep` 用 66
### 尝试一下——正则表达式 68

## 命令执行 69
### 算术扩展 70
### 参数扩展 70
### 尝试一下——参数处理 72
### 在此文档 (`Here Documents`) 73
### 尝试一下——使用在此文档 73
### 尝试一下——在此文档的另一种用途 74

## 脚本调试 75
### 迈向图形化——`Dialog` 工具 76
### 尝试一下——使用 `dialog` 工具 78
### 尝试一下 79
### 整合一切 80
### 需求 81
### 设计 81
### 尝试一下——一个 `CD` 应用程序 83
### 应用程序的说明 90
### 总结 90

# 第 3 章：文件操作 91

## Linux 文件结构 92
### 目录 92
### 文件与设备 93
### `/dev/console` 93
### `/dev/tty` 93
### `/dev/null` 94

## 系统调用与设备驱动 94

## 库函数 95

## 低级文件访问 96
### `write` 96
### `read` 97
### `open` 98
### 初始权限 100
### `umask` 100
### `close` 101
### `ioctl` 102
### 尝试一下——文件程序 102
### 管理文件的其他系统调用 104
### `lseek` 104
### `fstat`, `stat`, 和 `lstat` 104
### `dup` 和 `dup2` 106
### 标准 I/O 库 107
### `fopen` 108
### `fread` 108
### `fwrite` 109
### `fclose` 109
### `fflush` 109
### `fseek` 110
### `fget`, `getc`, 和 `getchar` 110
### `fput`, `put`, 和 `putchar` 110
### `fgets` 和 `gets` 111

## 格式化输入与输出 111
### `printf`, `fprintf`, 和 `sprintf` 112
### `scanf`, `scanf`, 和 `sscanf` 114
### 其他流函数 116
### 尝试一下——另一个程序 116
### 流错误 117
### 文件描述符 118

## 文件与目录维护 118
### `chmod` 118
### `chown` 119
### `unlink`, `link`, 和 `symlink` 119
### `mkdir` 和 `rmdir` 119
### `chdir` 和 `getcwd` 120
### `opendir` 121
### `readdir` 121
### `seekdir` 222
### `closedir` 222
### 尝试一下——目录程序 222
### 错误 225
### `perror` 226
### `/proc` 文件 226

## 高级主题：`fcntl` 和 `mmap` 130
### `fcntl` 130
### `mmap` 131
### 尝试一下——使用 `mmap` 132
### 总结 134

# 第 4 章：Linux 环境 135

## 程序参数 135
### 尝试一下——程序参数 137
### `getopt` 138
### 尝试一下——`getopt` 139
### `getopt_long` 140
### 环境变量 142
