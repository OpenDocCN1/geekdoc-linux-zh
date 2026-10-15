
# 必学的重要 Linux 命令：初学者口袋指南

> 唯一真正的智慧在于知道自己一无所知。
>
> - 苏格拉底

Manjunath.R

#16/1, 8th Main Road, Shivanajagar, Bangalore 560010, Karnataka, India

邮箱：manjunath5496@gmail.com

## 致辞

我将这本书献给世界上每一位个人、程序员、教师、教育机构和企业公司，感谢他们在创建、设计、部署和支持软件的过程中所付出的巨大贡献……

## 致谢

如果没有一些知名程序员的卓越工作，以及他们在软件编程领域的创造力和发明精神，这本书将无法完成。我想借此机会感谢我最亲爱的朋友和支持者“Lawrence”，感谢他在新冠危机期间给予我无私的支持，并让我获取了完成这本书所需的所有资源。我想向我的家人感谢他们在我写书期间给予的支持和鼓励，特别是我的母亲，她一直是我生活中巨大的灵感源泉。我非常感谢我的母亲，她教会了我如何在生活中保持坚韧和坚强。最后，我想强调在写书或承担生活中的任何其他项目时，耐心是多么关键。

## 前言

我既不是知名出版社的所有者，也不是拥有数百名内部程序员的顶尖 IT 公司（他们可以轻松生产我需要的任何东西）。我是一个自由软件工程师，对我的事业充满热情。请相信我的话，编写这本**综合版**投入了大量的心水和努力。如果它能帮助其他几人在他们的职业领域达到理想位置，我将不胜荣幸。

## 感谢

– Manjunath.R

## 引言

想要使用基于 Linux 的开源类 Unix 操作系统来提高你日常计算的生产力和效率吗？你可以在书中获得关于如何执行这些任务的思路、策略和技巧。本书的主要目标是通过提供你所需的所有信息，让 Linux 系统的系统管理变得简单。本书采用了以任务为导向的管理方法；因此，它的结构是围绕系统管理员的需求而非 Linux 操作系统的特征构建的。

命令行界面是 Linux 几乎所有优秀标志之一。Linux 命令多如海。然而，这到最后产生了一个问题：面对如此多可用可管理的命令，你不知道该从哪里以及在何时开始学习它们，尤其是当你还是一个初学者时。如果你面临这个问题，并并在书中寻找一种无痛的方法来开启命令行之旅，那么你来对地方了。在书中，我们将带你进入一系列受欢迎且实用的 Linux 命令世界：

- 你可以复制、管理和删除文件
- 识别任何网络连接问题
- 修改文件和文件夹的所有权和权限
- 管理、添加和创建用户及组
- 使用 `su` 和 `sudo` 安全地访问 root 账户
- 使用图形编辑器创建和修改文本文件，以及更多内容

本书侧重于 Linux 系统管理。它将尝试解释如何更有效地使用命令行界面。一切是如何运作的？它的范围是什么？哪种使用方法是最理想的？通过让读者建立命令行使用方面的坚实基础（这是任何重大系统管理活动的必要工具），它将为他们进一步探索命令行可执行软件或实用程序奠定基础。通往 Linux 之智慧没有捷径。命令行很难，需要付出巨大的努力。它并不是那么困难，而是太庞大了。在典型的 Linux 系统上，你可以通过命令行使用字面意义大量的程序。预警：学习命令行不是你应该轻视的事情。另一方面，由于 90% 的云基础设施和托管服务使用 Linux，精通 Linux 命令行是非常有利的。

## 玩开心！

请记住，在你阅读这本书的过程中，命令行是一个接收文本行并将其转换为计算机指令的界面。**图形用户界面**（GUI）仅仅是命令行应用程序的一种抽象化。例如，每当你点击“X”关闭窗口时，就会执行一条命令。在深入学习最常用的命令之前，请确保你的电脑已安装了 Linux。

> “生活中所有最棒的人似乎都喜欢 LINUX。”
>
> – Steve Wozniak

### 注意

- **使用的 Linux 版本：** `CentOS Linux release 7.3.1611 (Core)`

## UNIX 哲学的 17 原则

- **模块化**原则：系统应该由几个组件组成，这些组件连接良好、协作良好并具有定义定义的功能
- **清晰性**原则：清晰比聪明更好
- **组合**原则：创建可以与其他软件通信的软件
- **分离**原则：编程机制和规则应保持独立。将前端接口和后端引擎分离
- **简单性**原则：为简单构建，仅在必要时增加复杂性
- **节约**原则：只有在证明没有其他方法可以工作时，才编写大型程序
- **透明性**原则：设计时考虑可见性，以简化分析和故障排除
- **健壮性**原则：清晰度和易用性产生健壮性
- **表示性**原则：让任何参与项目的程序员都能更容易地理解程序，以便进行维护
- **最小惊讶**原则：鼓励开发者创建用户友好、直观的产品
- **沉默**原则：允许程序员和其他程序从程序的输出中获取所需数据，而无需解释不必要的、详尽的
- **修复**原则：程序员应该创建以简单识别和诊断的方式失败的软件
- **经济性**原则：应尽可能减少项目开发成本
- **生成**原则：程序员应该开发抽象的高级程序来产生代码，而不是手写代码，以减少人为错误并节省时间
- **优化**原则：在优化之前，先让它运行起来。软件在被开发者精雕细琢之前应经过开发和测试
- **多样性**原则：增加程序的灵活性，使其能够以创作者意之外的方式被使用
- **可扩展性**原则：增加开发者编写代码的实用性和寿命

## 更好的技能随着学习的增加而提升

> 作为一个初学者，你的主要重点应该是熟悉操作系统架构的每一个细节，并发现快捷方法和节省时间的技巧。

如果你使用 Windows 并且想学习 Linux，CentOS 是一个很棒的选择，因为它是最适合初学者的 Linux 发行版之一。你使用 CentOS 的前几天不会觉得那么奇怪。但如果你想体验它的全部功能，必须学会如何使用 Linux 的命令行界面。起初学习几条指令时可能会遇到一些困难。虽然使用这些指令不会让你成为天才，但它们将帮助你执行某些基础任务。以下是为新用户准备的最基础 CentOS 命令，以确保顺利开始。让我们开始吧！

> "... 成为一名 Linux 用户就像是住在一个由大量木工和建筑师居住的房子里。每天早上当你醒来，房子都会有一点不同。也许多了一个新塔楼，或者某些墙移动了。又也许有人暂时移走了你床下的地板。"
>
> ~ 《傻瓜版 Unix》，第2版

## Linux 命令

### `date`

**描述：** 显示系统日期和时间。

**命令：**

```
date
```

### `cal`

**描述：** 显示日历。

**命令：**

```
cal
```

### `date & cal`

**描述：** 显示日期、时间和日历。

**命令：**

```
date & cal
```

### `cal 8 2016`

**描述：** 显示 2016 年 8 月日历。

**命令：**

```
cal 8 2016
```

### `clear`

**描述：** 用于清除终端窗口。

**命令：**

```
clear
```

### `exit`

**描述：** 退出终端窗口。

**命令：**

```
exit
```

### `free`

**描述：** 显示空闲和已使用的系统内存。

**命令：**

```
free
```

### `free -b`

**描述：** 以字节为单位显示空闲和已使用的系统内存。

**命令：**

```
free -b
```

### `free -k`

**描述：** 以字节为单位显示空闲和已使用的系统内存。

**命令：**

```
free -k
```

### `free -m`

**描述：** 以兆为单位显示空闲和已使用的系统内存。

**命令：**

```
free -m
```

### `passwd`

**描述：** 更改用户密码。

**命令：**

```
passwd
```

### `shutdown`

**描述：** 关机。

**命令：**

```
shutdown
```

### `shutdown -h now`

**描述：** 立即关机。

**命令：**

```
shutdown -h now
```

### `shutdown -h +10`

**描述：** 10 分钟后关机。

**命令：**

```
shutdown -h +10
```

### `echo $PWD`

**描述：** 打印当前目录。

**命令：**

```
echo $PWD
```

### `echo $OLDPWD`

**描述：** 打印上一个目录。

**命令：**

```
echo $OLDPWD
```

### `!!`

**描述：** 执行上一条命令。

**命令：**

```
!!
```

### `history`

**描述：** 显示命令历史。

**命令：**

```
history
```

### `reboot`

**描述：** 重启系统。

**命令：**

```
reboot
```

### `ip address`

**描述：** 显示 IP 地址。

**命令：**

```
ip address
```

### `ls`

**描述：** 列出所有文件。

**命令：**

```
ls
```

### `mount`

**描述：** 查看挂载的文件系统。

**命令：**

```
mount
```

### `du`

**描述：** 显示磁盘占用。

**命令：**

```
du
```

### `top`

**描述：** 显示运行中的进程。

**命令：**

```
top
```

### `pstree`

**描述：** 以树形式显示运行进程。

**命令：**

```
pstree
```

### `reset`

**描述：** 重置你的终端。

**命令：**

```
reset
```

### `date -d fri`

**描述：** 显示今天是周几。

**命令：**

```
date -d fri
```

### `du -a`

**描述：** 显示每个单独的大小。

**命令：**

```
du -a
```

### `acpi`

**描述：** 显示高级配置和电源接口。

**命令：**

```
acpi
```

### `cd ..`

**描述：** 返回上级目录。

**命令：**

```
cd ..
```

### `cd -`

**描述：** 回到上一个目录。

**命令：**

```
cd -
```

### `help`

**描述：** 列出 Shell 内置命令列表。

**命令：**

```
help
```

### `last username`

**描述：** 列出最后登录记录。

**命令：**

```
last username
```

### `mkdir myfiles`

**描述：** 创建一个名为 myfiles 的新目录。

**命令：**

```
mkdir myfiles
```

### `rmdir myfiles`

**描述：** 删除 myfiles 目录。

**命令：**

```
rmdir myfiles
```

### `passwd -d root1`

**描述：** 禁用特定用户 root1 的密码。

**命令：**

```
passwd -d root1
```

### `sudo su root1`

**描述：** 切换到用户 root1。

**命令：**

```
sudo su root1
```

### `logout`

**描述：** 退出终端窗口。

**命令：**

```
logout
```

### `useradd "root1"`

**描述：** 创建用户 root1。

**命令：**

```
useradd "root1"
```

### `passwd "root1"`

**描述：** 为用户 root1 分配密码。

**命令：**

```
passwd "root1"
```

### `whoami`

**描述：** 显示你当前登录的用户。

**命令：**

```
whoami
```

### `logname`

**描述：** 显示当前用户的登录名。

**命令：**

```
logname
```

### `uname`

**描述：** 报告内核名称。

**命令：**

```
uname
```

### `uname -v`

**描述：** 打印内核版本。

**命令：**

```
uname -v
```

### `uname -o`

**描述：** 打印操作系统。

**命令：**

```
uname -o
```

### `uname -m`

**描述：** 报告机器硬件名称。

**命令：**

```
uname -m
```

### `uname --version`

**描述：** 打印版本信息并退出。

**命令：**

```
uname --version
```

### `uname -r`

**描述：** 打印内核发布版本。

**命令：**

```
uname -r
```

### `uname -n`

**描述：** 报告网络节点主机名。

**命令：**

```
uname -n
```

### `netstat -a`

**描述：** 显示所有端口连接（包括 TCP 和 UDP）。

**命令：**

```
netstat -a
```

### `netstat -at`

**描述：** 仅显示 TCP（传输控制协议）端口连接。

**命令：**

```
netstat -at
```

### `netstat -au`

**描述：** 仅显示 UDP（用户数据报协议）端口连接。

**命令：**

```
netstat -au
```

### `netstat -l`

**描述：** 显示所有活跃的监听端口。

**命令：**

```
netstat -l
```

### `netstat -lt`

**描述：** 显示所有活跃的监听 TCP 端口。

**命令：**

```
netstat -lt
```

### `netstat -lu`

**描述：** 显示所有活跃的监听 UDP 端口。

**命令：**

```
netstat -lu
```

### `id`

**描述：** 显示关于当前用户的所有信息（用户 ID、用户名、组 ID、组名等）。

**命令：**

```
id
```

### `id root1`

**描述：** 显示关于用户 "root1" 的所有信息（用户 ID、用户名、组 ID、组名等）。

**命令：**

```
id root1
```

### `arch`

**描述：** 打印机器架构。

**命令：**

```
arch
```

### `fc-list`

**描述：** 显示可用字体的列表。

**命令：**

```
fc-list
```

### `mkdir myfiles files`

**描述：** 创建两个目录（myfiles, files）。

**命令：**

```
mkdir myfiles files
```

### `yum install httpd`

**描述：** 安装 apache (CentOS)。

**命令：**

```
yum install httpd
```

### `apt install httpd`

**描述：** 安装 apache (Ubuntu)。

**命令：**

```
apt install httpd
```

### `yum update httpd`

**描述：** 升级 apache (CentOS)。

**命令：**

```
yum update httpd
```

### `apt update httpd`

**描述：** 升级 apache (Ubuntu)。

**命令：**

```
apt update httpd
```

### `yum remove httpd`

**描述：** 卸载 apache (CentOS)。

**命令：**

```
yum remove httpd
```

### `apt remove httpd`

**描述：** 卸载 apache (Ubuntu)。

**命令：**

```
apt remove httpd
```

### `date --help`

**描述：** 显示命令 (date) 的用法摘要。

**命令：**

```
date --help
```

### `ss -tup`

**描述：** 列出与系统进出的活跃连接。

**命令：**

```
ss -tup
```

### `ss -tup l`

**描述：** 列出系统上的互联网服务。

**命令：**

```
ss -tup l
```

### `netstat -lx`

**描述：** 显示所有活跃的 UNIX 监听端口。

**命令：**

```
netstat -lx
```

### `ifconfig`

**描述：** 显示所有活跃接口的细节。

**命令：**

```
ifconfig
```

### `ifconfig -a`

**描述：** 显示所有网络接口的信息。

**命令：**

```
ifconfig -a
```

### `diff 1.txt 2.txt`

**描述：** 比较两个文件的内容 (1.txt, 2.txt)。

**命令：**

```
diff 1.txt 2.txt
```

### `wc 1.txt`

**描述：** 告诉您文件 (1.txt) 中包含多少行、单词和字符。

**命令：**

```
wc 1.txt
```

### `gzip 1.txt`

**描述：** 压缩文件 (1.txt)，使其占用更少的空间。

**命令：**

```
gzip 1.txt
```

### `gunzip 1.txt`

**描述：** 解压缩由 gzip 压缩的文件 (1.txt)。

**命令：**

```
gunzip 1.txt
```

### `cat 1.txt`

**描述：** 检查文件 (1.txt) 的内容。

**命令：**

```
cat 1.txt
```

### `ncal`

**描述：** 显示日历。

**命令：**

```
ncal
```

### `rm 1.txt`

**描述：** 删除文件 (1.txt)。

**命令：**

```
rm 1.txt
```

### `mv 1.txt 0.txt`

**描述：** 将名为 1.txt 的文件重命名为 0.txt。

**命令：**

```
mv 1.txt 0.txt
```

### `cp 1.txt 0.txt`

**描述：** 用 1.txt 的内容替换 0.txt 的内容。

**命令：**

```
cp 1.txt 0.txt
```

### `touch test.txt`

**描述：** 创建一个空文件 (test.txt)。

**命令：**

```
touch test.txt
```



# Linux 常用命令速查

## 文件操作

### 创建文件
```bash
touch test.txt
```

### 查看文件内容
| 命令 | 说明 |
| :--- | :--- |
| `tail 1.txt` | 打印文件最后 10 行 |
| `tail -n N 1.txt` | 从文件打印 N 行 |
| `less 1.txt` | 查看文件内容（支持翻页） |
| `cat myfile.txt` | 显示文件全部内容 |
| `tac myfile.txt` | 反向打印文件行（从最后一行到第一行） |
| `more myfiles.txt` | 显示文件内容（分页） |
| `od -b myfiles.txt` | 以八进制格式显示文件内容 |
| `od -c myfiles.txt` | 以字符格式显示文件内容 |
| `od -An -c myfiles.txt` | 以字符格式显示文件内容，不包含偏移信息 |

### 文件统计信息
| 命令 | 说明 |
| :--- | :--- |
| `wc -w 1.txt` | 打印文件单词数 |
| `wc -m 1.txt` | 打印文件字符数 |
| `wc -L 1.txt` | 打印文件中最长行的长度 |
| `stat 1.txt` | 显示文件状态信息 |
| `file myfiles.txt` | 显示文件类型 |

### 文件内容写入与追加
```bash
# 覆盖写入
echo 'Hello World' > myfiles.txt
printf 'Hello World' > myfiles.txt

# 追加写入
echo "Hello world!" >> 1.txt
echo "this is 2nd line text" >> 1.txt
echo "last line!" >> 1.txt

# 合并多文件到一个文件
cat 1.txt 2.txt 3.txt > 0.txt

# 循环追加多文件
for i in {1..3}; do cat "$i.txt" >> 0.txt; done
```

### 文件比较与校验
| 命令 | 说明 |
| :--- | :--- |
| `diff 1.txt 2.txt` | 逐行比较两个文件 |
| `comm 1.txt 2.txt` | 比较两个文件中共有的行 |
| `cmp 1.txt 2.txt` | 按字节级比较两个文件 |
| `cksum myfiles.txt` | 计算文件的 CRC 校验和 |
| `md5sum myfiles.txt` | 使用 MD5 算法打印 32 字符 (128 位) 校验和 |
| `sha1sum myfiles.txt` | 打印 SHA1 (160 位) 校验和 |

### 文件分割与处理
```bash
# 按行分割文件
# 若 myfiles.txt 有 123 行，将创建四个文件：
# xx00 (1-12行), xx01 (13-61行), xx02 (62-100行), xx03 (101-123行)
csplit myfiles.txt 13 62 101

# 删除重复行
uniq myfiles.txt

# 安全删除（反复覆盖使数据难以恢复）
shred myfiles.txt
```

### 文件搜索
```bash
# 在当前目录及子目录中搜索匹配模式的文件
find test*
```

## 系统信息与日历

| 命令 | 说明 |
| :--- | :--- |
| `ncal` | 显示日历 |
| `cal -3` | 显示上个月、本月和下个月 |
| `hostid` | 以十六进制格式显示主机的数字 ID |
| `hostname -i` | 显示主机名的 IP 地址 |
| `tty` | 显示连接到标准输入的终端的文件名 |

## 网络命令

| 命令 | 说明 |
| :--- | :--- |
| `wget http://website.com/files/file.txt` | 从 URL 下载文件 |
| `ping google.com` | 检查主机与服务器之间的网络连接性 |
| `netstat -nuttlp` | 显示正在监听的 TCP 和 UDP 端口及对应程序 |

## 权限管理

### 权限模式对照表

| 数字模式 | 权限类型 | 符号模式 |
| :--- | :--- | :--- |
| 0 | 无权限 | `---` |
| 1 | 执行 | `--x` |
| 2 | 写入 | `-w-` |
| 3 | 执行 + 写入 | `-wx` |
| 4 | 读取 | `r--` |
| 5 | 读取 + 执行 | `r-x` |
| 6 | 读取 + 写入 | `rw-` |
| 7 | 读取 + 写入 + 执行 | `rwx` |

## 进程管理

| 命令 | 说明 |
| :--- | :--- |
| `ps -A` | 列出所有进程的状态、进程 ID 和 PID |
| `ps -ef \| grep sshd` | 检查 SSH 服务器 (`sshd`) 是否正在运行 |

## 包管理

### RPM 系
| 命令 | 说明 |
| :--- | :--- |
| `rpm -qa` | 列出所有已安装包 |

### YUM (CentOS)
| 命令 | 说明 |
| :--- | :--- |
| `yum list installed` | 列出所有已安装包 |
| `yum info httpd` | 显示包 "httpd" 的描述和摘要信息 |

## 磁盘使用

| 命令 | 说明 |
| :--- | :--- |
| `du -ah` | 以易读格式显示所有文件和目录的磁盘使用情况 |
| `du -sh` | 显示当前目录的总磁盘使用量 |

## 目录导航

```bash
cd /etc          # 切换到 /etc 目录
cd /etc && ls    # 切换到 /etc 后执行 ls
```

## Shell 与环境变量

```bash
# 变量引用示例
echo This is the $SHELL shell
# 输出: This is the /bin/bash shell

echo This is the $SHELL on computer $HOSTNAME
# 输出: This is /bin/bash on computer localhost.localdomain

echo The User ID of $USER is $UID
# 输出: The User ID of manju is 1000

echo My home directory is $HOME
# 输出: My home directory is /home/manju

# 环境隔离执行
bash -c 'echo $SHELL $HOME $USER'
# 输出: /bin/bash /home/manju manju

env -i bash -c 'echo $SHELL $HOME $USER'
# 输出: /bin/bash (环境变量被清空)

# 通配符扩展
env LANG=C bash -c 'ls test[a-z].txt'
# 输出: testa.txt testb.txt
```

## 逻辑控制操作符

```bash
# 且 (&&) / 或 (||)
rm myfiles.txt && echo success || echo failed
# 如果 myfiles.txt 被删除则打印 'success'，否则打印 'failed'
```

## 编程语言编译执行

### C 语言
```c
#include <stdio.h>
int main()
{
    printf("Hello world\n");
    return 0;
}
```
```bash
gcc Hello.c
```

### C++
```cpp
#include <iostream>
int main()
{
    std::cout << "Hello world!";
    return 0;
}
```
```bash
g++ Hello.cpp
```

### Java
```java
public class MyClass {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
```bash
javac MyClass.java
```

### Python (在 vi 中编写)
```bash
vi hello.py
# 按 i 进入插入模式
a = 20; b = 64; print(a + b)
# 按 Escape 返回普通模式
:w hello.py  # 保存
:q           # 退出
python hello.py
# 输出: 84
```

### Perl (在 vi 中编写)
```bash
vi hello.pl
# 按 i 进入插入模式
$name = "Paul";
print "$name";
# 按 Escape 返回普通模式
:w hello.pl
:q
perl hello.pl
# 打印输出：Paul
```

### Shell 脚本 (在 vi 中编写)
```bash
vi hello.sh
# 按 i 进入插入模式
echo "What is your name?"
read PERSON
echo "Hello, $PERSON"
# 按 Escape 返回普通模式
:w hello.sh
:q
sh hello.sh
# 输出示例：
# 你叫什么名字？
# 如果输入：Zara Ali
# Hello, Zara Ali
```

## vi 编辑器常用命令

| 命令 | 说明 |
| :--- | :--- |
| `vi` | 打开 vi 编辑器 |
| `i` | 进入插入模式 |
| `Escape` | 返回普通模式 |
| `:w filename` | 保存文本 |
| `:q` | 退出 |
| `:q!` | 不保存强制退出 |

## 系统关机与服务

| 命令 | 说明 |
| :--- | :--- |
| `halt -p` | 关闭系统电源 |
| `chkconfig --list` | 列出系统服务及其在运行级别 0-6 中的启动/停止状态 |

## 用户管理

| 命令 | 说明 |
| :--- | :--- |
| `cat /etc/passwd` \| `more /etc/passwd` \| `less /etc/passwd` \| `getent passwd` | 列出 Linux 所有用户 |
| `tail -5 /etc/passwd` | 列出 Linux 上最后 5 个用户 |
| `head -5 /etc/passwd` | 列出 Linux 上前 5 个用户 |
| `lastlog` | 打印上次登录详情（登录名、端口、时间） |
| `lastlog -t 1` | 显示 1 天前的登录信息 |
| `lastlog -u manju` | 显示特定用户的 lastlog 信息 |
| `wall "The system will be shutdown in 10 minutes."` | 向所有登录用户广播消息 |
| `chage -l manju` | 列出用户密码及相关详细信息 |
| `chage -M 10 manju` | 为用户设置密码过期天数 |
| `chage -E "2020-07-30" manju` | 为用户设置账户过期日期 |
| `chage -I 10 manju` | 强制用户账户在 10 天后锁定 |

## 文件打开

| 命令 | 说明 |
| :--- | :--- |
| `xdg-open myfiles.txt` | 打开文件 |

## 命令帮助

| 命令 | 说明 |
| :--- | :--- |
| `whatis cal` | 显示关于命令的单行描述 |
| `whereis cal` | 查找命令源文件/二进制文件的位置 |



# Linux 命令参考

## 编译与构建

### Java 编译
**命令**：
```
javac MyClass.java
```
**描述**：使用 `javac` 编译器编译保存在 `MyClass.java` 文件中的 Java 程序

### C 编译
**命令**：
```c
#include <stdio.h>
int main()
{
    printf("Hello world\n");
    return 0;
}

gcc Hello.c
```
**描述**：编译保存在 `Hello.c` 文件中的 C 程序

### C++ 编译
**命令**：
```cpp
#include <iostream>
int main()
{
    std::cout << "Hello world!";
    return 0;
}
// Hello.cpp
g++ Hello.cpp
```
**描述**：编译保存在 `Hello.cpp` 文件中的 C++ 程序

## 文件查看与处理

### od - 八进制/字符转储
**命令**：
```
od -b myfiles.txt
```
**描述**：以八进制格式显示 `myfiles.txt` 文件的内容

**命令**：
```
od -c myfiles.txt
```
**描述**：以字符格式显示 `myfiles.txt` 文件的内容

**命令**：
```
od -An -c myfiles.txt
```
**描述**：以字符格式显示 `myfiles.txt` 文件的内容，但不包含偏移信息

### csplit - 文件分割
**命令**：
```
csplit myfiles.txt 13 62 101
```
**描述**：如果文件 `myfiles.txt` 有 123 行，`csplit` 命令将创建四个文件：`xx00` 文件包含 1–12 行，`xx01` 文件包含 13–61 行，`xx02` 文件包含 62–100 行，`xx03` 文件包含 101–123 行

### 校验和
**命令**：
```
md5sum myfiles.txt
```
**描述**：使用 MD5 算法打印 `myfiles.txt` 文件的 32 字符 (128 位) 校验和

**命令**：
```
sha1sum myfiles.txt
```
**描述**：打印 `myfiles.txt` 文件的 SHA1 (160 位) 校验和

### 文件内容查看
**命令**：
```
more myfiles.txt
```
**描述**：显示 `myfiles.txt` 文件的内容

### shred - 安全删除
**命令**：
```
shred myfiles.txt
```
**描述**：反复覆盖 `myfiles.txt` 文件 —— 以便即使是极其昂贵的硬件探测也难以恢复数据

### tac - 反向输出
**命令**：
```
cat myfile.txt
01. Einstein
02. Newton
03. Maxwell
04. Tesla
05. Edison

tac myfile.txt
05. Edison
04. Tesla
03. Maxwell
02. Newton
01. Einstein
```
**描述**：反向打印 `myfile.txt` 的行（从最后一行到第一行）

### uniq - 去重
**命令**：
```
uniq myfiles.txt
```
**描述**：删除文件 (`myfiles.txt`) 中的重复行

## 系统管理

### 服务管理
**命令**：
```
chkconfig --list
```
**描述**：列出系统服务列表以及它们在运行级别 0–6 中是启动 (on) 还是停止 (off)

### 关机/重启
**命令**：
```
halt -p
```
**描述**：关闭系统电源

**命令**：
```
sudo shutdown 2
```
**描述**：2 分钟后关机

**命令**：
```
shutdown -c
```
**描述**：取消关机进程

### 用户管理
**命令**：
```
lastlog
```
**描述**：打印上次登录的详情（登录名、端口和上次登录时间）

**命令**：
```
lastlog -t 1
```
**描述**：显示登录信息（1 天前）

**命令**：
```
lastlog -u manju
```
**描述**：显示特定用户 (`manju`) 的 lastlog 信息

**命令**：
```
cat /etc/passwd
more /etc/passwd
less /etc/passwd
getent passwd
```
**描述**：列出 Linux 所有用户

**命令**：
```
tail -5 /etc/passwd
head -5 /etc/passwd
```
**描述**：列出 Linux 上最后 5 个用户 / 列出 Linux 上前 5 个用户

**命令**：
```
wall "The system will be shutdown in 10 minutes."
```
**描述**：消息（系统将在 10 分钟后关机）将广播给所有当前登录的用户

### 密码策略 (chage)
**命令**：
```
chage -l manju
```
**描述**：列出用户 (`manju`) 的密码及其相关详细信息

**命令**：
```
chage -M 10 manju
```
**描述**：为用户 (`manju`) 设置密码过期日期

**命令**：
```
chage -E "2020-07-30" manju
```
**描述**：为用户 (`manju`) 设置账户过期日期

**命令**：
```
chage -I 10 manju
```
**描述**：强制用户 (`manju`) 账户在 10 天后锁定

## 包管理

### yum
**命令**：
```
yum info httpd
```
**描述**：显示包 "httpd" 的描述和摘要信息 (CentOS)

## 磁盘与存储

### du - 磁盘使用
**命令**：
```
du -ah
```
**描述**：以易读格式显示所有文件和目录的磁盘使用情况

**命令**：
```
du -sh
```
**描述**：显示当前目录的总磁盘使用量

### df - 文件系统空间
**命令**：
```
df -h
```
**输出**：
```
Filesystem      Size  Used Avail Use Mounted on
sda             18G   13G    5G  29% /
```

## 目录导航

**命令**：
```
cd /etc
```
**描述**：切换到 `/etc` 目录

## 进程管理

### ps - 进程状态
**命令**：
```
ps -A
```
**描述**：列出所有进程的状态以及进程 ID 和 PID

**命令**：
```
ps -p $$
```
**输出**：
| PID | TTY | TIME | CMD |
| 3352 | pts/0 | 00:00:00 | bash |
**描述**：打印当前 shell 的进程 ID (`$$` 是当前 shell 的进程 ID)

### pstree
**描述**：提供关于 `pstree` 命令的信息（该命令以树状图显示当前系统中运行的进程名称）

### pmap - 内存映射
**命令**：
```
pmap 3244
```
**描述**：查看进程 ID (3244) 进程的内存映射

## 内核与模块

**命令**：
```
less /proc/modules
```
**描述**：显示系统中加载的内核模块信息

## 内存信息

**命令**：
```
free -tm
```
**输出**：
```
              total        used        free      shared  buff/cache   available
Mem:           999336      115656      734800        15300       284236        209748
Swap:             209748
```
**描述**：显示内存使用情况，包括 MB

## 日期时间

**命令**：
```
date -d "3 months ago"
```
**输出**：`Mon Jul 18 23:47 2022`
**描述**：打印当前日期 3 个月前的日期

**命令**：
```
date -d "3 days"
```
**输出**：`Fri Apr 22 23:01 2022`
**描述**：打印现在 3 天后的日期

## 文件操作

### 基础操作
**命令**：
```
cat files.txt
```
**描述**：列出文件的内容

**命令**：
```
cp *.txt *.md
```
**描述**：将以 `.txt` 或 `.md` 结尾的文件复制到用户主目录

### 文件查找与过滤
**命令**：
```
ls file
```
**描述**：列出当前目录中以 "file" 开头的文件

**命令**：
```
ls file
```
**描述**：列出当前目录中以 "file" 结尾的文件

**命令**：
```
grep -i files.txt
```
**描述**：在文件 "files.txt" 中查找字符串 "He" (忽略大小写)

### 文件内容处理
**命令**：
```
cat files.txt | tr 'H' 'A'
```
**描述**：在文件 "files.txt" 中将字符 'H' 替换为 'A'

**命令**：
```
ffmpeg files.txt
```
**描述**：列出当前目录下的文件 (注：此处原文可能有误，`ffmpeg` 通常用于音视频处理)

**命令**：
```
lsattr
```
**描述**：列出文件属性

### 文件清空
**命令**：
```
cat /dev/null > phy.txt
```
**命令**：
```
cp /dev/null phy.txt
```
**命令**：
```
echo "" > phy.txt
```
**命令**：
```
echo > phy.txt
```
**描述**：清空文件 (`phy.txt`) 的内容

## 文本处理

### cut - 列提取
**命令**：
```
cat score.txt
Albert-30
John-50
William-80
Stephen-20
Justin-40
cut -d -f2 score.txt
30
50
80
20
40
cut -d -f1 score.txt
Albert
John
William
Stephen
Justin
```
**描述**：使用 `-` 作为分隔符提取字段

### paste - 合并行
**命令**：
```
cat 1.txt
Hello World
cat 2.txt
Computer Program
paste 1.txt 2.txt
Hello World Computer Program
```
**描述**：将文件按行合并

### join - 关联行
**命令**：
```
cat 1.txt
Hello World
cat 2.txt
Computer Program
join 1.txt 2.txt
Hello World Computer Program
```
**描述**：基于公共字段关联两个文件的行

### rev - 反转
**命令**：
```
rev files.txt
```
**描述**：反转文件中的行顺序

### sort - 排序
**命令**：
```
sort -n files.txt
```
**描述**：按数字顺序排序行

**命令**：
```
sort -r files.txt
```
**描述**：按数字倒序排序行

**命令**：
```
sort -u files.txt
```
**描述**：按数字顺序排序行并去重

**命令**：
```
sort -c files.txt
```
**描述**：检查行是否按数字排序

**命令**：
```
sort -v files.txt
```
**描述**：按版本顺序排序行

**命令**：
```
sort files.txt
```
**描述**：按字母顺序排序行

**命令**：
```
sort -r files.txt
```
**描述**：按字母倒序排序行

**命令**：
```
sort -u files.txt
```
**描述**：按字母顺序排序行并去重

**命令**：
```
sort -c files.txt
```
**描述**：检查行是否按字母排序

**命令**：
```
sort -v files.txt
```
**描述**：按版本顺序排序行

### tr - 字符转换
**命令**：
```
tr 'A-Z' 'a-z' files.txt
```
**描述**：将行内容转换为小写

**命令**：
```
tr 'a-z' 'A-Z'
```
**描述**：将行内容转换为大写

### uniq - 去重
**命令**：
```
uniq files.txt
```
**描述**：显示文件中唯一的行

**命令**：
```
uniq files.txt
```
**描述**：显示文件中唯一的行（去重）

## 网络工具

### traceroute
**命令**：
```
traceroute google.com
```
**描述**：打印数据包到达本地机器的路径

### ss - 套接字统计
**命令**：
```
ss | less
```
**描述**：列出所有连接

**命令**：
```
ss -a tcp
```
**描述**：过滤 TCP（传输控制协议）连接

**命令**：
```
ss -a udp
```
**描述**：过滤 UDP（数据报协议）连接

**命令**：
```
ss -lnt
```
**描述**：仅显示监听的套接字

**命令**：
```
ss -ltp
```
**描述**：打印进程名和 PID

**命令**：
```
ss -s
```
**描述**：打印摘要统计信息

**命令**：
```
ss -t
```
**描述**：仅显示 IPv6 连接

**命令**：
```
ss -t -f inet
```
**描述**：仅显示 IPv4 套接字连接

**命令**：
```
ss -t state
```
**描述**：显示所有处于连接状态的 IPv4 TCP 套接字

## 压缩工具

### bzip2
**命令**：
```
bzip2 -k phy.txt
```
**描述**：压缩但不删除原始文件

**命令**：
```
bzip2 -d phy.txt.bz2
```
**描述**：解压压缩文件 (`phy.txt.bz2`)

**命令**：
```
bzcat phy.txt.bz2
```
**描述**：显示压缩文件的内容 (`phy.txt.bz2`)

## 定时任务

**命令**：
```
crontab -l
```
**描述**：显示当前登录用户的 crontab 条目

## 后台任务

**命令**：
```
nohup ping google.com &
```
**描述**：ping google.com 并在后台运行该进程

**命令**：
```
nohup ping google.com > log.txt &
```
**描述**：将 ping 日志保存到 log.txt

## 进程查找与终止

**命令**：
```
pgrep -a ping
```
**输出**：
```
3858 ping google.com
4200 ping google.com
4236 ping google.com
```
**命令**：
```
kill 3858
```
**命令**：
```
pgrep -a ping
```
**输出**：
```
4200 ping google.com
4236 ping google.com
```

## 目录列表

**命令**：
```
ls -la /home
```
**描述**：显示 `/home` 的内容

**命令**：
```
ls -1
```
**描述**：每行列出一个文件

**命令**：
```
echo m*
```
**描述**：显示当前文件夹中以字母 "m" 开头的文件

**命令**：
```
echo *
```
**描述**：打印所有文件和文件夹 - 类似于 `ls` 命令

## 用户登录历史

**命令**：
```
last
```
**描述**：列出用户的最后登录情况以及发生的情况，例如“shutdown”或“crash”等

## 环境变量

**命令**：
```
echo $SHELL
```
**描述**：打印用户的默认 shell

**命令**：
```
echo $0
```
**描述**：显示当前运行进程的名称 (`$0` 是正在运行进程的名称)。如果你在 shell 内部使用它，它将返回 shell 的名称。如果你在脚本中使用它，它将返回脚本的名称

**命令**：
```
echo ~
```
**描述**：打印你的家目录路径

**命令**：
```
env
```
**描述**：打印所有环境变量列表

**命令**：
```
cat /etc/shells
```
**描述**：列出所有的 shells

## 文件比较

**命令**：
```
diff files.txt 2.txt
```
**描述**：比较两个压缩文件的内容 (注：`diff` 通常用于文本文件比较)

## 查看压缩文件

**命令**：
```
cat files.txt
```
**描述**：查看压缩文件的内容 (注：通常使用 `zcat`、`bzcat` 等)

## 命令查找

### apropos
**命令**：
```
apropos -r 'remove file'
```
**描述**：查找删除文件的命令

**命令**：
```
apropos editor
```
**描述**：显示系统中可用编辑程序的信息

**描述**：当你知道想做什么，但不知道应该使用什么命令来实现时，`apropos` 命令非常有用。例如，如果你想知道如何查找文件，相关命令以及 `apropos find`、`apropos locate` 将提供很多建议。

## basename - 文件名提取
**命令**：
```
basename /etc/passwd
```
**输出**：`passwd`

**命令**：
```
basename /usr/local/apache2/conf/httpd.conf
```
**输出**：`httpd.conf`

## xargs - 参数构建
**命令**：
```
echo a b c d e f | xargs
```
**输出**：`a b c d e f`

**命令**：
```
echo a b c d e f | xargs -n 3
```
**输出**：
```
a b c
d e f
```
**描述**：每行仅显示 3 个项目

## 终端设置

**命令**：
```
stty -a
```
**描述**：显示所有当前终端设置

## 文件分页

**命令**：
```
pr 36.txt
```
**描述**：逐页显示文件 (`36.txt`) 的内容

## 广播消息

**命令**：
```
wall "The system will be shutdown in 10 minutes."
```
**描述**：消息（系统将在 10 分钟后关机）将广播给所有当前登录的用户

## 终端设备

**命令**：
```
tty
```
**描述**：显示连接到标准输入的终端的文件名

## Linux 与 Unix 对比

| Linux | Unix |
| :--- | :--- |
| 免费使用（开源） | 许可的操作系统（闭源） |
| Linux 仅仅是内核 | Unix 是一个完整的操作系统包 |
| Bash (Bourne Again Shell) 是 Linux 的默认 shell | Bourne Shell 是 Unix 的默认 shell |
| 可移植且可从 USB 闪盘启动 | 不可移植 |
| 源代码对公众可见 | 源代码无人可见 |
| 使用可选的图形用户界面 | 使用命令行界面 |
| 命令行界面 | |

## 确认输出

**命令**：
```
yes John
```



| Linux | Unix |
| --- | --- |
| 免费使用（开源） | 许可的操作系统（闭源） |
| Linux 仅仅是内核 | Unix 是一个完整的操作系统包 |
| Bash (Bourne Again Shell) 是 Linux 的默认 shell | Bourne Shell 是 Unix 的默认 shell |
| 可移植且可从 USB 闪盘启动 | 不可移植 |
| 源代码对公众可见 | 源代码无人可见 |
| 使用可选的图形用户界面 | 使用命令行界面 |
| 命令行界面 | |

Command:
```
echo $SHELL
```
Description:
打印用户的默认 shell

Command:
```
echo $0
```
Description:
> 显示当前运行进程的名称 (`$0` 是正在运行进程的名称)。如果你在 shell 内部使用它，它将返回 shell 的名称。如果你在脚本中使用它，它将返回脚本的名称

Command:
```
echo *
```
Description:
打印所有文件和文件夹 - 类似于 `ls` 命令

Command:
```
ps -p $$
```
Output:
| PID | TTY | TIME | CMD |
| --- | --- | --- | --- |
| 3352 | pts/0 | 00:00:00 | bash |
Description:
打印当前 shell 的进程 ID (`$$` 是当前 shell 的进程 ID)

Command:
```
sudo du -a Documents/ | sort -n -r | head -n 5
```
### 列出 "Documents" 目录中最大的 5 个文件

Command:
```
cat /etc/shells
```
Description:
列出所有的 shells

Command:
```
echo m*
```
Description:
显示当前文件夹中以字母 "m" 开头的文件

Command:
```
last
```
Description:
列出用户的最后登录情况以及发生的情况，例如“shutdown”或“crash”等。

Command:
```
echo ~
```
Description:
打印你的家目录路径

Command:
```
bzip2 -k phy.txt
```
Description:
压缩但不删除原始文件
![](img/df24534eff215443b1bf728f904e6756_110_0.png)

Command:
```
bzip2 -d phy.txt.bz2
```
Description:
解压压缩文件 (`phy.txt.bz2`)
![](img/df24534eff215443b1bf728f904e6756_110_1.png)

Command:
```
bzcat phy.txt.bz2
```
Description:
显示压缩文件的内容 (`phy.txt.bz2`)

Command:
```
crontab -l
```
Description:
显示当前登录用户的 crontab 条目

Command:
```
cat /dev/null > phy.txt
```

Command:
```
cp /dev/null phy.txt
```

Command:
```
echo "" > phy.txt
```

Command:
```
echo > phy.txt
```
Description:
清空文件 (`phy.txt`) 的内容

Command:
```
nohup ping google.com &
```
Description:
`ping google.com` 并在后台运行该进程

Command:
```
nohup ping google.com > log.txt &
```
Description:
将 ping 日志保存到 `log.txt`

Command:
```
pgrep -a ping
```
Output:
```
3858 ping google.com
4200 ping google.com
4236 ping google.com
```
Command:
```
kill 3858
```
Command:
```
pgrep -a ping
```
Output:
```
4200 ping google.com
4236 ping google.com
```

Command:
```
ls -la /home
```
Description:
显示 `/home` 的内容

Command:
```
sudo shutdown 2
```
Description:
2 分钟后关机

Command:
```
shutdown -c
```
Description:
取消关机进程

Command:
```
pr 36.txt
```
Description:
逐页显示文件 (`36.txt`) 的内容

Command:
```
stty -a
```
Description:
显示所有当前终端设置

Command:
```
ls -1
```
Description:
每行列出一个文件

Command:
```
yes John
```
Description:
重复输出字符串 (John) 直到被杀死

Command:
```
vdir
```
Description:
列出当前目录下的文件和目录（每行一个）并带有详细信息

Command:
```
who -b
```
Description:
打印系统启动时间

Command:
```
nano phy.txt
```
### 使用 nano 打开 phy.txt

Command:
```
ls -al *.txt
```
Description:
显示所有 .txt 文件，包括各自的权限

Command:
```
nano phy.txt
```
### 使用 vim 打开 phy.txt
```
vim phy.txt
```

Command:
```
uname -i
```
Description:
显示硬件平台

Command:
```
uname -p
```
Description:
显示处理器类型

Command:
```
cat /proc/interrupts
```
Description:
显示中断情况

Command:
```
w --ip-addr
```
Description:
显示关于当前登录到机器的用户信息、登录时间、空闲时间、TTY 和 CPU 时间
Output:
```
11:, login time, IDLE time, TTY and CPU time
```



```
3858 ping google.com
4200 ping google.com
4236 ping google.com

kill 3858

pgrep -a ping
```

Output:
```
4200 ping google.com
4236 ping google.com
```

### Command: `ls -la /home`
**Description:** 显示 `/home` 的内容

### Command: `sudo shutdown 2`
**Description:** 2 分钟后关机

### Command: `shutdown -c`
**Description:** 取消关机进程

### Command: `pr 36.txt`
**Description:** 逐页显示文件 (`36.txt`) 的内容

### Command: `stty -a`
**Description:** 显示所有当前终端设置

### Command: `ls -1`
**Description:** 每行列出一个文件

### Command: `yes John`
**Description:** 重复输出字符串 (`John`) 直到被杀死

### Command: `vdir`
**Description:** 列出当前目录下的文件和目录（每行一个）并带有详细信息

### Command: `who -b`
**Description:** 打印系统启动时间

### 使用 `nano` 打开 `phy.txt`

### Command: `ls -al *.txt`
**Description:** 显示所有 `.txt` 文件，包括各自的权限

### Command: `nano phy.txt`

### 使用 `vim` 打开 `phy.txt`

```
vim phy.txt
```

### Command: `uname -i`
**Description:** 显示硬件平台

### Command: `uname -p`
**Description:** 显示处理器类型

### Command: `cat /proc/interrupts`
**Description:** 显示中断情况

### Command: `w --ip-addr`
**Description:** 显示关于当前登录到机器的用户信息、登录时间、空闲时间、TTY 和 CPU 时间

### Command: `ulimit -a`
**Description:** 报告当前用户的所有资源限制

### Command: `ulimit -s`
**Description:** 检查当前用户的最大栈大小

### Command: `ulimit -e`
**Description:** 检查当前用户的最大调度优先级

### Command: `ulimit -u`
**Description:** 显示最大进程数

### Command: `ulimit -v`
**Description:** 检查虚拟内存的大小

### Command: `ulimit -n`
**Description:** 检查进程可以拥有多少文件描述符

### Command: `man limits.conf`
**Description:** 显示关于 `limits.conf` 配置文件的详细信息

### Command: `sar -V`
**Description:** 显示 `sar` 版本

### Command: `sar -u 2 5`
**Description:** 以每隔 2 秒为间隔报告 5 次 CPU 详细信息

### Command: `sar -n DEV 1 3 | egrep -v lo`
**Description:** 报告网络接口、网络速度、IPV4、TCPV4、ICMP4 网络流量和错误

### Command: `sar -v 1 3`
**Description:** 报告关于进程、内核线程、i-node 和文件表的详细信息

### Command: `sar -S 1 3`
**Description:** 报告关于交换的统计信息

### Command: `sar -b 1 3`
**Description:** 报告关于 I/O 操作的细节，如每秒事务数、每秒读取、每秒写入

### Command: `sudo systemctl status firewalld`
**Description:** 显示 `firewalld` 的状态

### Command: `sudo systemctl start firewalld`
**Description:** 启动 `firewalld` 服务

`firewalld` 是适用于 Linux 操作系统的防火墙管理工具

### Command: `firewall-config`
**Description:** 启动图形化防火墙配置工具

### `firewall-cmd`

### Command: `firewall-cmd --list-all-zones`
**Description:** 列出所有区域 (zones)

### Command: `firewall-cmd --get-default-zone`
**Description:** 检查当前设置的默认区域

### Command: `firewall-cmd --list-services`
**Description:** 显示系统上当前允许的服务

### Command: `firewall-cmd --list-ports`
**Description:** 列出系统中开放的端口

### Command: `firewall-cmd --zone=work --list-services`
**Description:** 列出公共区域（public zone）允许的服务

### Command: `mtr --report google.com`
**Description:** 提供关于互联网流量在本地系统和远程主机 (`google.com`) 之间传输路由的信息

### Command: `sudo yum install samba`
**Description:** 安装 Samba (CentOS)

Samba 是一种实现跨操作系统资源共享的客户端/服务器技术。通过 Samba，文件和打印机可以在 Windows、Mac 和 Linux/UNIX 客户端之间共享

### Command: `sudo firewall-cmd --add-service samba --permanent`
**Description:** 将 Samba 服务添加到 `firewalld` 中

### Command: `zip q.zip q.txt`
**Description:** 创建一个 zip 文件 (`q.zip`)

### Command: `unzip q.zip`
**Description:** 解压一个 zip 文件 (`q.zip`)

```
zipcloak q.zip
```

### `zipcloak` 会提示你输入密码，然后要求你确认：

```
Enter password:
Verify password:
```

...如果密码匹配，它将对 `q.zip` 文件加密

```
unzip q.zip
```

### 当你尝试解压 `q.zip` 文件时，它会在允许你提取其中包含的文件 (`q.txt`) 之前提示输入密码

### Command: `zgrep -l "Einstein" *`
**Description:** 显示包含单词 (`Einstein`) 的文件名

### Command: `zipsplit -n 1048576 q.zip`
**Description:** 将 `q.zip` 文件拆分为一系列 zip 文件 (`q1.zip`, `q2.zip`...)，每个文件的大小不超过 1048576 字节（1 兆字节）。你可以使用命令将 (`q1.zip`, `q2.zip`...) 合并成新文件 `w.zip`：

### Command: `cat q*.zip > w.zip`

### Command: `mtr google.com`
**Description:** 测试到目标主机的路由和流量质量

### Command: `route`
**Description:** 显示 Linux 系统的 IP 路由表

### Command: `nmcli dev status`
**Description:** 查看所有网络设备

### Command: `nmcli show`
**Description:** 检查系统的网络连接

### Command: `ss -ta`
**Description:** 列出服务器上打开的所有 TCP 端口 (sockets)

### Command: `ss -to`
**Description:** 显示所有带有计时器的活动 TCP 连接

### Command: `type -a`
**Description:** 检查 Linux 中的别名 (Aliases)

### Command: `echo $(date +%Y)`
**Description:** `%Y` 和 `%y` 的区别在于：`%Y` 会打印 4 位数字，而 `%y` 会打印年份的最后 2 位数字

### Command: `echo $(date +%b)`
**Description:** `%B` 和 `%b` 的区别在于：`%B` 会打印月份的全称，而 `%b` 会打印月份的缩写（注：此处原文描述有误，已按意译修正）

### Command: `echo $(date +%A)`
**Description:** `%A` 和 `%a` 的区别在于：`%A` 会打印周几名称，而 `%a` 会打印周期的缩写

### Command: `echo $(date +%F)`
**Description:** `%F` 和 `%x` 的区别在于：`%F` 会打印完整日期（YYYY-MM-DD），而 `%x` 只打印日期

### Command: `echo $(date +%T)`
**Description:** `%T` 和 `%t` 的区别在于：`%T` 会打印完整时间（HH:MM:SS），而 `%t` 只打印时间

### Command: `echo $(date +%R)`
**Description:** `%R` 和 `%r` 的区别在于：`%R` 会打印 24 小时制，而 `%r` 会打印 12 小时制

### Command: `echo $(date +%Z)`
**Description:** `%Z` 和 `%z` 的区别在于：`%Z` 会打印本地时区名称，而 `%z` 会打印 UTC 偏移量

### Command: `echo $(date "yesterday")`
**Description:** 显示昨天的日期和时间

### Command: `echo $(date "tomorrow")`
**Description:** 显示明天的日期和时间

### Command: `echo $(date "1 week ago")`
**Description:** 显示上周前的日期和时间

### Command: `echo $(date "1 week from now")`
**Description:** 显示下周后的日期和时间

### Command: `echo $(date "1 month ago")`
**Description:** 显示上个月前的日期和时间

### Command: `echo $(date "1 month from now")`
**Description:** 显示下个月后的日期和时间

### Command: `echo $(date "1 year ago")`
**Description:** 显示去年的日期和时间

### Command: `echo $(date "1 year from now")`
**Description:** 显示明年的日期和时间

### Command: `echo $(date "10 days ago")`
**Description:** 显示 10 天前的日期和时间

### Command: `echo $(date "10 days from now")`
**Description:** 显示 10 天后的日期和时间

### Command: `echo $(date "last-monday")`
**Description:** 显示上周一的日期和时间

### Command: `echo $(date "next-monday")`
**Description:** 显示下周一的日期和时间

### Command: `echo $(date "last-sunday")`
**Description:** 显示上周周日的日期和时间

### Command: `echo $(date "next-sunday")`
**Description:** 显示下周周日的日期和时间

```bash
[manju@localhost ~]$ ls *.txt; echo $_

12.txt 1.txt 2.txt abc.txt my.txt phy.txt
13.txt 24.txt 3.txt marks.txt names.txt mphy.txt
```

```bash
[manju@localhost ~]$ cut -d, -f2,1 <<<'Albert,Bob,John'
Albert,Bob
[manju@localhost ~]$ cut -d, -f2,2 <<<'Albert,Bob,John'
Bob
[manju@localhost ~]$ cut -d, -f2,3 <<<'Albert,Bob,John'
Bob,John
```

```bash
[manju@localhost ~]$ x="W X Y"; echo "$x"
W X Y
[manju@localhost ~]$ x="W X Y"; echo "$x"
W X Y
```

> `echo $x` 和 `echo "$x"` 产生不同的结果
> **引用变量会保留空格**

```bash
[manju@localhost ~]$ let x=20+7; echo "The value of \"x\" is $x."
The value of "x" is 27.
[manju@localhost ~]$ x=100; let x += 1; echo "x = $x"
x = 101
```

```bash
[manju@localhost ~]$ x="a+b+c"; IFS=+; echo $x
a b c    "+" "+" 号将被解释为分隔符
```

```bash
[manju@localhost ~]$ x="a-b-c"; IFS=-; echo $x
a b c    减 "-" 号将被解释为分隔符
```

```bash
[manju@localhost ~]$ x="a,b,c"; IFS=; echo $x
a b c    逗号 "," 号将被解释为分隔符
```

```
free | grep Mem | awk '{ print $4 }'
```
### 显示未使用的 RAM

```
du -ach
```
### 显示（磁盘）文件使用情况

```
readelf -h /bin/bash
```
### 显示指定 elf 二进制文件的信息和统计数据

```bash
[manju@localhost ~]$ expr 5 \* 2 + 3
13 # 10 + 3
[manju@localhost ~]$ expr 5 \( 2 + 3 \)
25 # 5 * 5
```

```bash
[manju@localhost ~]$ echo -e "\033[4mAlbert Einstein.\033[0m"
Albert Einstein.
```

```bash
[manju@localhost ~]$ echo -e "\033[1mAlbert Einstein.\033[0m"
Albert Einstein.
```

```bash
[manju@localhost ~]$ echo -e '\E[34;47mAlbert Einstein'; tput sgr0
Albert Einstein
```

```bash
[manju@localhost ~]$ echo -e '\E[33;34m"Albert Einstein"'; tput sgr0
Albert Einstein
```

```bash
[manju@localhost ~]$ echo -e '\E[1;33;44m"Albert Einstein"'; tput sgr0
Albert Einstein
```

```bash
[manju@localhost ~]$ x=2; y=3; echo $((2*$x + 3*$y))
13
[manju@localhost ~]$ x=2; y=3; echo $((2*x + 3*y))
13
[manju@localhost ~]$ let x=2+3 y=3+2; echo $x $y
5
```

### 命令: `sdiff phy.txt score.txt`
**描述:** 显示两个文件（`phy.txt` 和 `score.txt`）之间的差异

### 命令: `history -c`
**描述:** 删除或清除 bash 历史中的所有记录

### 命令: `ping -c 5 www.google.com`
**描述:** ping 测试将在发送 5 个数据包后停止

```bash
### 统计每个 .txt 文件的行数
```



## 统计文件信息

### 统计每个 .txt 文件的行数
```bash
ls *.txt | xargs wc -l
```

### 统计每个 .txt 文件的单词数
```bash
ls *.txt | xargs wc -w
```

### 统计每个 .txt 文件的字符数
```bash
ls *.txt | xargs wc -c
```

### 统计每个 .txt 文件的行、单词和字符数
```bash
ls *.txt | xargs wc
```

## 系统服务管理

### 列出所有加载的服务
**命令：**
```bash
systemctl list-units --type=service
```
**描述：** 列出系统上所有加载的服务（无论处于活动、运行、退出还是失败状态）

**命令：**
```bash
systemctl --type=service
```
**描述：** 列出系统上所有加载的服务（无论处于活动、运行、退出还是失败状态）

### 列出所有激活的服务
**命令：**
```bash
systemctl list-units --type=service --state=active
```
**描述：** 列出所有加载且激活的服务

**命令：**
```bash
systemctl --type=service --state=active
```
**描述：** 列出所有加载且激活的服务

### 列出所有正在运行的服务
**命令：**
```bash
systemctl list-units --type=service --state=running
```
**描述：** 列出所有正在运行的服务（即所有加载且正在活跃运行的服务）

**命令：**
```bash
systemctl --type=service --state=running
```
**描述：** 列出所有正在运行的服务（即所有加载且正在活跃运行的服务）

## 用户账户信息

**命令：**
```bash
lslogins -u
```
**描述：** 显示用户账户

## 网络扫描

### 扫描单个端口
```bash
nmap -v -w 2 192.168.56.1 22
```

### 扫描多个端口
```bash
nmap -v -w 2 192.168.56.1 22 80
```

### 扫描端口范围
```bash
nmap -v -w 2 192.168.56.1 20-25
```

## DNS 配置查看

**命令：**
```bash
cat /etc/resolv.conf
```
**描述：** 查找你的 DNS 服务器 IP 地址

**命令：**
```bash
less /etc/resolv.conf
```
**描述：** 查找你的 DNS 服务器 IP 地址

## 挂载监控

**命令：**
```bash
findmnt --poll --mountpoint /mnt/test
```
**描述：** 监控目录的挂载、卸载、重新挂载和移动操作（例如 `/mnt/test`）

## 系统运行时间

**命令：**
```bash
uptime -p
```
**描述：** 检查 Linux 服务器运行时间

**命令：**
```bash
uptime -s
```
**描述：** 检查 Linux 服务器启动时间

**命令：**
```bash
uptime -h
```
**描述：** 显示 `uptime` 的版本信息

## 文件查找与删除

**命令：**
```bash
find . -type f -name "phy.txt" -exec rm -f {} \;
```
**描述：** 查找并删除 `phy.txt` 文件

**命令：**
```bash
find . -type f -name "*.txt" -exec rm -f {} \;
```
**描述：** 查找并删除多个 `.txt` 文件

**命令：**
```bash
find . -type f -name "*.mp3" -exec rm -f {} \;
```
**描述：** 查找并删除多个 `.mp3` 文件

**命令：**
```bash
find /tmp -type d -empty
```
**描述：** 查找所有空目录

**命令：**
```bash
find /tmp -type f -name ".*"
```
**描述：** 查找所有隐藏文件

## 字符处理

**命令：**
```bash
echo "Phone number: 55602369" | tr -cd [:digit:]
```
**输出：**
```
55602369
```

**命令：**
```bash
echo "Phone number: 55602369" | tr -d [:digit:]
```
**输出：**
```
Phone number:
```
**描述：** 从字符串中删除所有数字

## 基于时间的文件查找

**命令：**
```bash
find / -mtime 50
```
**描述：** 查找过去 50 天内修改过的文件

**命令：**
```bash
find / -atime 50
```
**描述：** 查找过去 50 天内访问过的文件

**命令：**
```bash
find / -cmin 60
```
**描述：** 查找过去 1 小时内修改的文件

**命令：**
```bash
find / -mmin -60
```
**描述：** 查找过去 1 小时内修改过的文件

**命令：**
```bash
find / -amin -60
```
**描述：** 查找过去 1 小时内访问过的文件

## 命令类型识别

| 命令 | 说明 |
| :--- | :--- |
| `type cat` | 识别 `cat` 命令是 shell 内置命令、子程序、别名还是关键字。 |

## 基于大小的文件查找与删除

**命令：**
```bash
find / -size 50M
```
**描述：** 查找所有 50MB 的文件

**命令：**
```bash
find / -type f -size +100M -exec rm -f {} \;
```
**描述：** 查找并删除 100MB 的文件

**命令：**
```bash
find / -type f -name *.mp3 -size +10M -exec rm {} \;
```
**描述：** 查找所有大于 10MB 的 `.mp3` 文件并删除它们

## 目录列表示例

```bash
ls -l --color
# 列出当前目录下的文件（带颜色输出）

man df
# 加载 "df" 帮助页

ls /usr/include
# 列出编译 C 程序的头文件

ls /usr/local
# 列出本地安装的文件

ls /usr/bin/d*
# 列出 /usr/bin 目录下所有以字母 "d" 开头的文件
```

```bash
ls .b*
```
**输出：**
```
.bash_history .bash_logout .bash_profile .bashrc
```

```bash
ls [a-h]*
```
**输出：**
```
all DICT file1 file34.txt file.md fool.txt
allfiles.txt echo file123.txt file23.txt file3.txt first.bash
bu.txt file file1.txt file2.txt FILE.backup first.txt
```

```bash
touch hello.cpp; touch hello.f99
ls *?[9p]?
```
**输出：**
```
hello.cpp hello.f99
```

```bash
ls /usr
# 列出 /usr 目录

ls /usr
# 列出用户的家目录和 /usr 目录
```

## 文件内容处理

```bash
cat myfiles.txt
```
**输出：**
```
Hello World
```

```bash
cat myfiles.txt | tr ' ' '\n'
```
**输出：**
```
Hello
World
```

```bash
find . -name "*.txt"
# 查找当前目录及所有子目录下以 .txt 结尾的文件
```

```bash
find /etc > 12.txt
# 查找 /etc 下的所有文件并将列表存入 12.txt
```

```bash
find . -newer file1.txt
# 查找比 file1.txt 新的文件
```

## 日期时间操作

```bash
date +'%A %d-%m-%Y'
```
**输出：**
```
Tuesday 19-04-2022
```

```bash
date -d '2022-04-01 + 2000000000 seconds'
```
**输出：**
```
Thu Aug 16 03:33:20 PDT 2085
```

```bash
find /etc -type f -name '*.txt' | wc -l
# /etc 及其所有子目录中 .txt 文件的数量
```

## 正则表达式与 grep

```bash
cat myfiles.txt
```
**输出：**
```
Hello World
```

```bash
grep -E 'o*' myfiles.txt
```
**输出：**
```
Hello World
```

```bash
grep -E 'o+' myfiles.txt
```
**输出：**
```
Hello World
```

## sed 替换示例

```bash
echo Albert Einstein | sed 's/Albert/&&'
```
**输出：**
```
AlbertAlbert Einstein
```

```bash
echo Albert Einstein | sed 's/Einstein/&&'
```
**输出：**
```
Albert EinsteinEinstein
```

```bash
echo Albert | sed 's_\(Alb)_\lert_'
```
**输出：**
```
Albertert
```

```bash
echo Albert | sed 's_\(Alb)_\lert \i_'
```
**输出：**
```
Albert Albert
```

```bash
echo -e 'Albert\tis\tScientist'
```
**输出：**
```
Albert is Scientist
```

```bash
echo -e 'Albert\tis\tScientist' | sed 's_\s_ _g'
```
**输出：**
```
Albert is Scientist
```

```bash
cat myfiles.txt
```
**输出：**
```
Hello World
```

```bash
cat myfiles.txt | sed 's/\11\?/A/'
```
**输出：**
```
HeAo World
```

```bash
cat myfiles.txt
```
**输出：**
```
Hello World
```

```bash
cat myfiles.txt | sed 's/1\{2\}/A/'
```
**输出：**
```
HeAo World
```

```bash
echo Albert `echo -n Einstein`
```

## 测试与条件判断

```bash
test 50 -gt 15 ; echo $?
```
**输出：**
```
0
```
**说明：** True: 50 is greater than 15

```bash
test 5 -gt 15 ; echo $?
```
**输出：**
```
1
```
**说明：** False: 5 is not greater than 15

```bash
test 5 -lt 15 ; echo $?
```
**输出：**
```
0
```
**说明：** True: 5 is lesser than 15

```bash
test 50 -gt 15 && echo true || echo false
```
**输出：**
```
true
```

```bash
test 5 -gt 15 && echo true || echo false
```
**输出：**
```
false
```

```bash
[ 50 -gt 15 ] && echo true || echo false
```
**输出：**
```
true
```

```bash
[ 5 -gt 15 ] && echo true || echo false
```
**输出：**
```
false
```

```bash
[ 100 -gt 10 -a 100 -lt 150 ] && echo true || echo false
```
**输出：**
```
true
```

```bash
[ 100 -gt 10 -a 100 -lt 155 ] && echo true || echo false
```
**输出：**
```
false
```

```bash
a=2; b=a; eval c=$b; echo $c
```
**输出：**
```
2
```

## 日期计算

```bash
date
```
**输出：**
```
Tue Apr 19 02:55:39 PDT 2022
```

```bash
date --date="1 week ago"
```
**输出：**
```
Tue Apr 12 02:55:05 PDT 2022
```

## 系统信息查看

**命令：**
```bash
uname -or
```
**描述：** 获取 Linux Kernel 版本

**命令：**
```bash
uname -a
```
**描述：** 打印 Linux 系统信息

**命令：**
```bash
cat /proc/version
```
**描述：** 显示部分系统信息，包括 Linux 内核版本

**命令：**
```bash
cat /etc/centos-release
```
**描述：** 获取 Linux 发行版名称和发布版本

## 进程与文件占用

**命令：**
```bash
fuser .
```
**描述：** 显示正在访问当前工作目录的进程 ID (PID)

**命令：**
```bash
fuser -v -m .bashrc
```
**描述：** 确定哪些进程正在访问你的 `.bashrc` 文件

**命令：**
```bash
sudo fuser --list-signals
```
**描述：** 显示 `fuser` 工具可以使用的所有信号

**命令：**
```bash
sudo fuser -k /etc
```
**描述：** 向 `/etc` 下的所有进程发送信号

## ls 常用选项

| 命令 | 说明 |
| :--- | :--- |
| `ls -al` | 列出详细信息（权限、所有者、大小等） |
| `ls -n` | 以用户 ID 和组 ID 列出文件 |
| `ls -R` | 递归列出目录内容 |
| `ls -t` | 按修改时间排序文件 |
| `ls -lh` | 以易读格式（如 KB, MB）显示大小 |
| `ls -S` | 按文件大小排序 |
| `ls -u` | 按最近访问时间排序 |
| `ls -r` | 反向排序列出 |
| `ls -i` | 显示文件的索引号 |
| `ls -m` | 用逗号分隔列出 |
| `ls --version` | 查看 `ls` 命令的版本 |

## 目录列表示例

**命令：**
```bash
ls /tmp
```
**描述：** 列出 `/tmp` 目录的内容

**命令：**
```bash
ls -l /tmp
```
**描述：** 详细列出 `/tmp` 目录的内容

## find 常用用法

| 命令 | 说明 |
| :--- | :--- |
| `find .` | 在当前目录下查找 |
| `find /` | 从根目录下查找 |
| `find -maxdepth 1` | 限制查找深度为 1 层 |
| `find . -name "*.txt"` | 查找以 `.txt` 结尾的文件 |
| `find . -iname "*.txt"` | 不区分大小写查找 `.txt` 文件 |
| `find . -type f` | 仅查找文件 |
| `find . -type d` | 仅查找目录 |
| `find . -size +10M` | 查找大于 10MB 的文件 |
| `find . -size -1G` | 查找小于 1GB 的文件 |
| `find . -mtime -7` | 查找 7 天内修改过的文件 |
| `find . -mtime +30` | 查找 30 天前的文件 |



# Linux 常用命令速查

## find 命令

### 查找 60 分钟内修改过的文件
**命令:**
```bash
find . -mmin -60
```

### 查找空文件或空目录
**命令:**
```bash
find . -empty
```

### 删除所有 .log 文件
**命令:**
```bash
find . -name "*.log" -delete
```

### 对所有 .log 文件执行删除命令
**命令:**
```bash
find . -name "*.log" -exec rm {} \;
```

## grep 命令

### 在文件中搜索特定模式
**命令:**
```bash
grep "pattern" file.txt
```

### 忽略大小写搜索
**命令:**
```bash
grep -i "pattern" file.txt
```

### 显示不匹配模式的行
**命令:**
```bash
grep -v "pattern" file.txt
```

### 显示匹配行的行号
**命令:**
```bash
grep -n "pattern" file.txt
```

### 统计匹配的行数
**命令:**
```bash
grep -c "pattern" file.txt
```

### 递归在当前目录下搜索模式
**命令:**
```bash
grep -r "pattern" .
```

### 使用扩展正则表达式
**命令:**
```bash
grep -E "pattern" file.txt
```

### 只列出包含模式的文件名
**命令:**
```bash
grep -l "pattern" *
```

### 仅匹配完整单词
**命令:**
```bash
grep -w "pattern" file.txt
```

## awk 命令

### 打印文件的第一列
**命令:**
```bash
awk '{print $1}' file.txt
```

### 使用冒号作为分隔符打印第二列
**命令:**
```bash
awk -F: '{print $2}' file.txt
```

### 打印包含模式的行
**命令:**
```bash
awk '/pattern/' file.txt
```

### 统计行数
**命令:**
```bash
awk 'END {print NR}'
```

### 计算第一列的总和
**命令:**
```bash
awk '{sum+=$1} END {print sum}'
```

## sed 命令

### 替换文件中的字符串
**命令:**
```bash
sed 's/old/new/' file.txt
```

### 直接修改文件
**命令:**
```bash
sed -i 's/old/new/g' file.txt
```

### 删除文件的第 5 行
**命令:**
```bash
sed '5d' file.txt
```

### 删除第 1 到第 5 行
**命令:**
```bash
sed '1,5d' file.txt
```

## sort 与 uniq 命令

### 对文件进行排序
**命令:**
```bash
sort file.txt
```

### 反向排序
**命令:**
```bash
sort -r file.txt
```

### 排序并去重
**命令:**
```bash
sort -u file.txt
```

### 删除相邻的重复行
**命令:**
```bash
uniq file.txt
```

### 统计重复行出现的次数
**命令:**
```bash
uniq -c file.txt
```

## 文件操作命令

### 合并文件
**命令:**
```bash
cat file1.txt file2.txt
```

### 比较两个文件的差异
**命令:**
```bash
diff file1.txt file2.txt
```

### 统计行数、单词数和字节数
**命令:**
```bash
wc file.txt
```

### 查看文件前 10 行
**命令:**
```bash
head -n 10 file.txt
```

### 查看文件后 10 行
**命令:**
```bash
tail -n 10 file.txt
```

### 实时监控文件内容变化
**命令:**
```bash
tail -f file.log
```

## 压缩与解压命令

### 压缩文件
**命令:**
```bash
gzip file.txt
```

### 解压缩文件
**命令:**
```bash
gunzip file.txt.gz
```

### 创建压缩包
**命令:**
```bash
tar -cvf archive.tar.gz directory/
```

### 解压压缩包
**命令:**
```bash
tar -xvf archive.tar.gz
```

## 系统信息命令

### 显示 BIOS 信息（需要提升权限）
**命令:**
```bash
dmidecode -t 0
```

### 显示 CPU 信息（需要提升权限）
**命令:**
```bash
dmidecode -t 4
```

### 查看所有系统日志
**命令:**
```bash
gnome-system-log
```

### 识别 SSH 客户端版本
**命令:**
```bash
ssh -V
```

### 显示用户的总连接时间
**命令:**
```bash
ac -d
```

### 显示所有用户的连接时间
**命令:**
```bash
ac -p
```

### 显示特定用户 "manju" 的连接时间报告
**命令:**
```bash
ac -d manju
```

### 显示 Apache 内部编译的模块
**命令:**
```bash
httpd -l
```

### 查看当前用户拥有的进程
**命令:**
```bash
ps U $USER
```

### 显示文件系统类型信息
**命令:**
```bash
df -Tha
```

### 显示带有进程 ID 和程序名的活动连接
**命令:**
```bash
netstat -tap
```

### 显示原始 RAW 网络统计数据
**命令:**
```bash
netstat --statistics --raw
```

## Linux 基础知识

### Linux 用户模式
![Linux 用户模式](img/df24534eff215443b1bf728f904e6756_212_0.png)

### LILO (Linux 加载程序)
Linux 下文件名的最大长度为 255 字节。

### Shell 提示符修改示例
```bash
[manju@localhost ~]$ PS1="Please enter a command: "
Please enter a command: date
Thu Apr 21 20:51:19 PDT 2022
```

### cal 命令输出示例
```text
Please enter a command: cal
April 2022

Su Mo Tu We Th Fr Sa
1 2
3 4 5 6 7 8 9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
```

### 检查 httpd 进程
```bash
ps -aux | grep 'httpd'
# 检查 httpd 进程
```

### 目录结构说明
> `/var/spool` 存放池化的文件，例如为打印作业和网络传输生成的文件

```bash
[manju@localhost ~]$ ls /var/spool
abrt abrt-upload anacron at cron cups lpd mail plymouth postfix
```

> `/usr/share/man` 存放在线帮助页 (Man pages)

```bash
[manju@localhost ~]$ ls /usr/share/man
ca en hu ko man1x man3p man5 man7 man9 pl ro tr zh_TW
cs es id manop2 man2x man3x man5x man7x man9x pt ru uk
da fr it man1 man2x man4 man6 man8 mann pt_BR sk zh
de hr ja man1 man3 man4x man6x man8x overrides pt_PT sv zh_CN
```

### GDM 与 GConf 配置目录
```bash
[manju@localhost ~]$ ls /etc/gdm
# 列出 GDM 配置目录的内容
custom.conf  Init PostLogin PostSession PreSession Xsession

ls /etc/gconf
# 列出 GConf 配置

ls /usr/share/gnome
# 列出 GNOME 应用程序使用的文件
```

### 系统配置文件目录
```bash
[manju@localhost ~]$ ls /etc/sysconfig
# 列出系统配置文件
atd         firewall        libvirt-guests  qemu-ga        samba
authconfig  grub            man-db          radvd           saslauth
autofs      init            modules         raid-check     selinux
cbq         ip64-tables-config netconsole     rdisc           smartmontools
cgrep      iptables-config network        readonly-root  sshd
console     irqbalance     network-scripts  rpcbind        sysstat
cpuower     kdump           nfs             rpc-quotad     sysstat.iconf
crond       kernel          ntpd            rsyncd          virtlockd
etables-config ksm             ntpdate         rsyslog         virtlogd
fcoe        libvirtd        pluto           run-parts      wpa_supplicant

ls /etc/rc.d
# 列出系统启动和关闭文件
```

### 初始化脚本目录
```bash
[manju@localhost ~]$ ls /etc/init.d
# /etc/init.d 存放用于启动网络连接的脚本
functions netconsole network  README
```

## Linux 操作系统的重要特性
- 免费且开源
- 可移植且更安全
- 健壮且适应性强

![Linux 特性](img/df24534eff215443b1bf728f904e6756_215_0.png)

### 切换目录与查看路径
```bash
[manju@localhost ~]$ cd /etc
[manju@localhost etc]$ pwd
/etc
```

### 查看 /etc/hosts 文件
```bash
[manju@localhost etc]$ cat /etc/hosts
# /etc/hosts 包含带有 IP 地址的主机
127.0.0.1    localhost localhost.localdomain localhost4 localhost4.localdomain4
::1          localhost localhost.localdomain localhost6 localhost6.localdomain6
```

## 权限管理 (chmod)

### 移除用户写权限
**命令:**
```bash
chmod u-w myfiles.txt
```

### 添加组写权限
**命令:**
```bash
chmod g+w myfiles.txt
```

### 移除组读权限
**命令:**
```bash
chmod g-r myfiles.txt
```

### 为其他用户添加执行权限
**命令:**
```bash
chmod o+x myfiles.txt
```

### 为所有用户添加执行权限
**命令:**
```bash
chmod a+x myfiles.txt
```

### 允许所有用户读取和执行
**命令:**
```bash
chmod a=rx myfiles.txt
```

## 进程与用户管理

### 列出特定进程的所有线程（进程 ID 为 3315）
**命令:**
```bash
ps -L 3315
```

### 查找用户名
**命令:**
```bash
[manju@localhost ~]$ awk -F: '/root/ {print $1}' /etc/passwd
```

### 显示进程状态
**命令:**
```bash
ps aux -w
```

### 统计 /etc 目录下文件行数
**命令:**
```bash
ls -l /etc | awk 'END {print NR}'
```

### 显示用户连接时间报告
**命令:**
```bash
[manju@localhost ~]$ ac -d
```

### 显示特定用户 "manju" 的连接时间报告
**命令:**
```bash
[manju@localhost ~]$ ac -d manju
```

### 移除文件用户组和其他用户的读、写、执行权限
**命令:**
```bash
chmod go-rwx myfiles.txt
```

### 为所有用户赋予文件读和写权限
**命令:**
```bash
chmod a+rw myfiles.txt
```

### 历史命令执行示例
**命令:**
```bash
! -3
```

### 查看操作系统类型
**命令:**
```bash
[manju@localhost ~] echo $OSTYPE
linux-gnu  # 你正在使用的操作系统
```

### 检查文件系统的 Inodes 索引节点使用情况
**命令:**
```bash
df -i /dev/sda1
```

### 查找文件的 Inode 号
**命令:**
```bash
ls -il myfiles.txt
```

### 检查文件上配置的 ACL（访问控制列表）
**命令:**
```bash
getfacl myfiles.txt
```

> SSH（Secure Shell）是一种网络协议，它为用户和系统管理员提供了一种通过不安全网络访问计算机的安全方式。

### Linux 中的三个标准流
![标准流](img/df24534eff215443b1bf728f904e6756_224_0.png)

### 检查机器上文件和目录的磁盘使用信息
**命令:**
```bash
du -sh /var/log/*
```

### 显示 "cp" 命令的依赖项
**命令:**
```bash
ldd /bin/cp
```

### 显示 "cp" 命令的详细依赖项
**命令:**
```bash
ldd -v /bin/cp
```

### 显示 "cp" 命令未使用的直接依赖项
**命令:**
```bash
ldd -u /bin/cp
```

### 顺序执行命令
```bash
[manju@localhost ~] date cal
Thu Apr 21 19:44:12 PDT 2022
April 2022
Su Mo Tu We Th Fr Sa
      1 2
3 4 5 6 7 8 9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
```
> 先执行 `date` 命令，后执行 `cal` 命令

## 测试运算符

| 运算符 | 含义 |
| :--- | :--- |
| `-gt` | 大于 |
| `-lt` | 小于 |
| `-ge` | 大于等于 |
| `-le` | 小于等于 |
| `-eq` | 等于 |
| `-ne` | 不等于 |

### 逻辑与执行 (&&)
```bash
[manju@localhost ~]$ date && cal
Thu Apr 21 19:44:21 PDT 2022
April 2022
Su Mo Tu We Th Fr Sa
      1 2
3 4 5 6 7 8 9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
```
> 只有当 `date` 命令成功执行时，才会执行 `cal` 命令

### 文件通配符列表示例
```bash
[manju@localhost ~]$ ls *.co
hello.c hello.o vim.c
```



```
[manju@localhost ~]$ a='ls *.c'; echo $$

hello.c main.c vim.c

[manju@localhost ~]$ test 50 -ge 15 && echo true || echo false
true

[manju@localhost ~]$ test 50 -ge 50 && echo true || echo false
true

[manju@localhost ~]$ test 20 -le 50 && echo true || echo false
true

[manju@localhost ~]$ test 20 -le 20 && echo true || echo false
true

[manju@localhost ~]$ test 30 -eq 30 && echo true || echo false
true

[manju@localhost ~]$ test 320 -eq 30 && echo true || echo false
false

[manju@localhost ~]$ test 30 -ne 30 && echo true || echo false
false

[manju@localhost ~]$ test 320 -ne 30 && echo true || echo false
true
```

## 命令

```
cat /proc/net/dev
```

## 说明

显示网络适配器及统计数据

## 命令

```
cat /proc/mounts
```

## 说明

显示挂载的文件系统

## 命令

```
telinit 0
```

## 说明

关闭系统

```
cd /home
# 将你带上手目录
cd ..
# 将你带回上一级目录
```

`ls * [0-9] *` 显示包含数字 0 到 9 的和文件夹

```
iconv -l
# 显示已知加密算法列表

ls -lr | more
# 按大小显示文件和目录的大小

du -sk * | sort -rn
# 按大小显示文件和目录的大小
```

| 命令 | 说明 |
| :--- | :--- |
| `ls -lh` | 显示权限 |
| `yum list` | 列出系统中所有安装的包 |
| `yum clean packages` | 清理所有已保存的包 |

## 命令

```
yum clean headers
```

## 说明

清理包的头文件

## 命令

```
yum clean all
```

## 说明

清理所有缓存信息

## 命令

```
yum clean metadata
```

## 说明

清理元数据

## 命令

```
ip link show
# 显示所有接口的状态
ps -ef
# 显示任务
lssof -p
# 显示进程打开的文件列表
find /var -atime -90
```

## 说明

查找 `/var` 目录中过去 90 天内未被访问的文件

## 命令

```
find -name -exec rm {} \;
```

## 说明

在整个树结构中搜索文件并直接删除它们，不提示确认

## 命令

```
who -r
```

## 说明

检查 Linux 的运行级别

## Bash 脚本

```
for i in *; rm $i; done
```

## 说明

删除当前目录下所有包含 "linux" 单词的文件

## 命令

```
awk '{print}' myfiles.txt
```

## 说明

显示文件 (`myfiles.txt`) 的内容 ![img/df24534eff215443b1bf728f904e6756_232_0.png](img/df24534eff215443b1bf728f904e6756_232_0.png)

## 命令

```
ln -f myfiles.txt
```

## 说明

为 `myfiles.txt` 创建硬链接

## 命令

```
cat myfiles.txt
```

## 说明

检查硬链接的内容

## 命令

```
ln -s myfiles.txt
```

## 说明

为 `myfiles.txt` 创建软链接

## 命令

```
cat myfiles.txt
```

## 说明

检查软链接的内容

| 前台进程 | 后台进程 |
| :--- | :--- |
| 需要用户启动或与其交互。 | 独立于用户运行。 |

## 命令

```
ps -p
```

## 说明

显示指定进程 ID（PID）的进程信息

## 命令

```
ulimit -f 100
```

## 说明

将文件大小限制设为 100 字节

## 命令

```
lsmod
```

## 说明

找出当前加载了哪些内核模块

| 绝对路径 | 相对路径 |
| :--- | :--- |
| 来自根目录的包或目录。 | 来自当前工作目录的文件或目录。 |

## 命令

```
sudo yum install php
```

## 说明

安装 php 7.2

## 命令

```
php -r 'echo "Hello World\n";
```

## 说明

从命令行运行 PHP 语句无需创建文件

## 命令

```
php -a
```

## 说明

启动 PHP 交互式 shell

## 命令

```
du -h -d 1 /
```

## 说明

显示顶级目录的磁盘占用

## 命令

```
yum install man
```

## 说明

在 CentOS 中安装 man 包

## 命令

```
man -f ls
```

## 说明

显示 `ls` 命令的帮助描述

## 命令

```
man -a ls
```

## 说明

显示 `ls` 命令的所有帮助页

## 命令

```
man -k ls
```

## 说明

允许用户搜索 `ls` 命令的描述和帮助页名称

## 命令

```
man -w ls
```

## 说明

显示 `ls` 命令帮助页的位置

## 命令

```
cat /etc/redhat-release
# 显示 Linux 发行版名称和版本

ls ~
# 显示主目录的内容

ls ../
# 显示父目录的内容
```

| 命令 | 说明 |
| :--- | :--- |
| `ps -U root -u root` | 显示 root 用户运行的所有进程 |
| `cal -1` | 显示当前月份日历 |
| `cal -j` | 以数字形式打印日历 |

## 命令

```
su
```

## 说明

用于从一个账户切换到另一个

## 命令

```
nmcli show
```

## 说明

显示系统中连接了哪些网络连接

## 命令

```
ps aux | grep 'telnet'
```

## 说明

搜索 'telnet' 进程 ID

- `ps r` - 列出 Linux 上正在运行的进程
- `ps T` - 列出当前终端的所有进程
- `ps -f` - 列出进程及其关联的父进程 ID

## 命令

```
ps -x
# 查看你所属的所有进程

ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem
# 显示内存占用最高的进程

sudo yum list --installed | more
# 列出 CentOS 上已安装的包
```

## 命令

```
sudo rpm -qa
sudo rpm -qa | more
```

## 说明

使用 `rpm` 命令获取所有已包的列表

## 命令

```
sudo rpm -q nginx
```

## 说明

检查是否安装了 `nginx` 包

## Command

```bash
sudo rpm -q bash
```

## Description

检查是否安装了 `bash` 包

## Command

```bash
sudo yum history
```

## Description

在 CentOS 历史记录命令中列出所有通过 `yum` 安装的包

## Command

```bash
sudo yum history info 2
```

## Description

使用事务 ID [2] 详细检查历史条目

## Command

```bash
file /etc/passwd
```

## Description

显示给定文件的类型

```
[root@localhost manju]# file /etc/passwd
/etc/passwd: ASCII text
```

## Command

```bash
wc /etc/passwd
46 91 2373 /etc/passwd
```

## Output

`/etc/passwd` 文件包含 46 行、91 个单词和 2373 个字母

## Command

```bash
grep root: /etc/passwd
```

## Description

显示 `/etc/passwd` 中所有包含字符串 "root" 的行行

## Command

```bash
grep -n root /etc/passwd
```

## Description

带行号显示 `/etc/passwd` 中所有包含字符串 "root" 的行

## Command

```bash
grep -c false /etc/passwd
```

## Description

显示以 `/bin/false` 为 shell 的账户数量

## Command

```bash
grep ^root: /etc/passwd
```

## Description

显示 `/etc/passwd` 中所有以字符串 'root' 开头后跟冒号的行

## Command

```bash
last | head
```

## Description

显示登录和注销系统的用户信息（仅显示前 10 行）

```
lastb
# 显示最后失败的登录尝试

du -sh /etc/passwd
# 显示 /etc/passwd 文件的磁盘占用

killall proc
# 杀死所有名为 proc 的进程

wget https://repo.mysql.com/mysql80-community-release-el8-11.noarch.rpm
# 下载 RPM 文件进行安装
sudo yum localinstall mysql80-community-release-el8-11.noarch.rpm
# 安装 RPM 文件
```

```bash
sudo localinstall https://repo.mysql.com/mysql80-community-release-el7-1.noarch.rpm
# 通过 URL 安装 RPM 包
```

```bash
curl --version
# 显示 curl 版本

curl -O http://website.com/myfiles.tar.gz
# 从 url "http://website.com/myfiles.tar.gz" 下载文件 (myfiles.tar.gz)
# 保存为 myfiles.tar.gz
```

```bash
curl -o files.tar.gz http://website.com/myfiles.tar.gz
# 从 url "http://website.com/myfiles.tar.gz" 下载文件 (myfiles.tar.gz)
# 保存为 files.tar.gz
```

```bash
echo 'https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm' > urls.txt

xargs -n 1 curl -O < urls.txt
# 从 "urls.txt" 文件中的 URL 列表下载文件
```

```bash
exit 110
# 退出终端窗口

sudo -l
# 了解当前主机允许和不允许执行哪些命令
```

## Command

```bash
echo -e "\hello\nworld"

hello
world
```

```
history | grep cd | head -12
搜索前 12 条匹配 cd 单词的历史命令记录
```

## 开源操作系统的缺点

- 使用困难
- 兼容性问题

## Command

```bash
rpm -qa | grep ftp
```

## Description

检查所有已安装的 ftp 包

## Command

```bash
find /home -mtime +120
```

## Description

在 `/home` 目录中查找 120 天前修改的文件

Samba 使 Linux /UNIX 机器可以在网络中与 Windows 机器通信。

- `/etc` 目录包含 Linux 中的配置文件。
- 网络文件系统 (NFS) 是一种在网络上存储文件的机制。
- "init" 是 Linux 中由内核启动的第一个进程，其进程 ID 为 1。

![](img/df24534eff215443b1bf728f904e6756_245_0.png)
![](img/df24534eff215443b1bf728f904e6756_245_1.png)
![](img/df24534eff215443b1bf728f904e6756_245_2.png)

## Command

```bash
cd ../../..
```

带你回退三个文件夹

## Command

```bash
ps -ef | grep xlogo
```

## Description

列出系统中所有包含字符串 'xlogo' 的进程

```bash
echo -n "abc";echo "def"
```

```
abcdef
```

```bash
echo "abc";echo "def"
```

```
abc
def
```

```bash
ls -ltr /etc
```

按最后修改时间列出 `/etc` 中的文件

## Command

```bash
ls -Rlh /var | grep [0-9]M
```

## Description

列出 `/var` 中大于 0 兆但小于 1GB 的文件

## Command

```bash
ls -lhS
```

## Description

按大小列出文件

```bash
cat /etc/passwd /etc/group
```

显示多个文件的内容（`/etc/passwd` 和 `/etc/group`）

```bash
find /tmp -name *.txt -exec rm -f {} \;
```

在 `/tmp` 目录中搜索所有名为 `*.txt` 的文件并删除它们

```bash
echo 'https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm' > urls.txt

xargs -n 1 curl -O < urls.txt
# 从 "urls.txt" 文件中的 URL 列表下载文件
```

```bash
exit 110
# 退出终端窗口

sudo -l
# 了解当前主机允许和不允许执行哪些命令
```

## Command

```bash
echo -e "\hello\nworld"

hello
world
```

```
history | grep cd | head -12
搜索前 12 条匹配 cd 单词的历史命令记录
```

## 开源操作系统的缺点

- 使用困难
- 兼容性问题

```bash
rpm -qa | grep ftp
```

## Description

检查所有已安装的 ftp 包

## Command

```bash
find /home -mtime +120
```

## Description

在 `/home` 目录中查找 120 天前修改的文件

Samba 使 Linux /UNIX 机器可以在网络中与 Windows 机器通信。

- `/etc` 目录包含 Linux 中的配置文件。
- 网络文件系统 (NFS) 是一种在网络上存储文件的机制。
- "init" 是 Linux 中由内核启动的第一个进程，其进程 ID 为 1。

![](img/df24534eff215443b1bf728f904e6756_245_0.png)
![](img/df24534eff215443b1bf728f904e6756_245_1.png)
![](img/df24534eff215443b1bf728f904e6756_245_2.png)

## Command

```bash
cd ../../..
```

带你回退三个文件夹

## Command

```bash
ps -ef | grep xlogo
```

## Description

列出系统中所有包含字符串 'xlogo' 的进程

```bash
echo -n "abc";echo "def"
```

```
abcdef
```

```bash
echo "abc";echo "def"
```

```
abc
def
```

```bash
ls -ltr /etc
```

按最后修改时间列出 `/etc` 中的文件

## Command

```bash
ls -Rlh /var | grep [0-9]M
```

## Description

列出 `/var` 中大于 0 兆但小于 1GB 的文件

## Command

```bash
ls -lhS
```

## Description

按大小列出文件

```bash
cat /etc/passwd /etc/group
```

显示多个文件的内容（`/etc/passwd` 和 `/etc/group`）



## Linux 常用命令与系统知识

### 文件查找与删除

```bash
find /tmp -name *.txt -exec rm -f {} \;
```

在 `/tmp` 目录中搜索所有名为 `*.txt` 的文件并删除它们。

### 文件下载

```bash
echo 'https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm' > urls.txt
xargs -n 1 curl -O < urls.txt
# 从 "urls.txt" 文件中的 URL 列表下载文件
```

### 终端控制与权限查看

```bash
exit 110
# 退出终端窗口

sudo -l
# 了解当前主机允许和不允许执行哪些命令
```

### 转义字符输出

```bash
echo -e "\hello\nworld"
```
```
hello
world
```

### 历史命令搜索

```bash
history | grep cd | head -12
```
搜索前 12 条匹配 `cd` 单词的历史命令记录。

### 开源操作系统的缺点

- 使用困难
- 兼容性问题

### 包管理与查询

```bash
rpm -qa | grep ftp
```
检查所有已安装的 ftp 包。

```bash
find /home -mtime +120
```
在 `/home` 目录中查找 120 天前修改的文件。

### 系统基础知识

Samba 使 Linux/UNIX 机器可以在网络中与 Windows 机器通信。

- `/etc` 目录包含 Linux 中的配置文件。
- 网络文件系统 (NFS) 是一种在网络上存储文件的机制。
- `init` 是 Linux 中由内核启动的第一个进程，其进程 ID 为 1。

![](img/df24534eff215443b1bf728f904e6756_245_0.png)
![](img/df24534eff215443b1bf728f904e6756_245_1.png)
![](img/df24534eff215443b1bf728f904e6756_245_2.png)

### 目录导航

```bash
cd ../../..
```
带你回退三个文件夹。

### 进程管理

```bash
ps -ef | grep xlogo
```
列出系统中所有包含字符串 `xlogo` 的进程。

### Echo 命令对比

```bash
echo -n "abc";echo "def"
```
```
abcdef
```

```bash
echo "abc";echo "def"
```
```
abc
def
```

### 文件列表与排序

```bash
ls -ltr /etc
```
按最后修改时间列出 `/etc` 中的文件。

```bash
ls -Rlh /var | grep [0-9]M
```
列出 `/var` 中大于 0 兆但小于 1GB 的文件。

```bash
ls -lhS
```
按大小列出文件。

### 文件内容显示

```bash
cat /etc/passwd /etc/group
```
显示多个文件的内容（`/etc/passwd` 和 `/etc/group`）。

### 包安装与检查

```bash
sudo rpm -q bash
```
检查是否安装了 bash 包。

```bash
sudo yum history
```
在 CentOS 历史记录命令中列出所有通过 yum 安装的包。

```bash
sudo yum history info 2
```
使用事务 ID 2 详细检查历史条目。

### 文件类型与统计

```bash
file /etc/passwd
```
显示给定文件的类型。

```bash
wc /etc/passwd
```
```
/etc/passwd 文件包含 46 行、91 个单词和 2373 个字母
```

### Grep 文本搜索

```bash
grep root: /etc/passwd
```
显示 `/etc/passwd` 中所有包含字符串 `root` 的行。

```bash
grep -n root /etc/passwd
```
带行号显示 `/etc/passwd` 中所有包含字符串 `root` 的行。

```bash
grep -c false /etc/passwd
```
显示以 `/bin/false` 为 shell 的账户数量。

```bash
grep ^root: /etc/passwd
```
显示 `/etc/passwd` 中所有以字符串 `root` 开头后跟冒号的行。

### 登录记录

```bash
last | head
```
显示登录和注销系统的用户信息（仅显示前 10 行）。

```bash
lastb
# 显示最后失败的登录尝试
```

### 磁盘使用与进程控制

```bash
du -sh /etc/passwd
# 显示 /etc/passwd 文件的磁盘占用

killall proc
# 杀死所有名为 proc 的进程
```

### RPM 包下载与安装

```bash
wget https://repo.mysql.com/mysql80-community-release-el8-11.noarch.rpm
# 下载 RPM 文件进行安装

sudo yum localinstall mysql80-community-release-el8-11.noarch.rpm
# 安装 RPM 文件
```

```bash
sudo localinstall https://repo.mysql.com/mysql80-community-release-el7-1.noarch.rpm
# 通过 URL 安装 RPM 包
```

### Curl 命令用法

```bash
curl --version
# 显示 curl 版本

curl -O http://website.com/myfiles.tar.gz
# 从 url "http://website.com/myfiles.tar.gz" 下载文件 (myfiles.tar.gz)
# 保存为 myfiles.tar.gz
```

```bash
curl -o files.tar.gz http://website.com/myfiles.tar.gz
# 从 url "http://website.com/myfiles.tar.gz" 下载文件 (myfiles.tar.gz)
# 保存为 files.tar.gz
```

### 批量下载

```bash
echo 'https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm' > urls.txt
xargs -n 1 curl -O < urls.txt
# 从 "urls.txt" 文件中的 URL 列表下载文件
```

### 进程树查看

```bash
ps -efH | more
```
以树形结构查看当前运行进程。

### 文件系统类型

```bash
df -T
```
显示文件系统类型。

### 目录创建

```bash
mkdir ~/temp
```
在主目录下创建一个名为 temp 的目录。

### 文件列表与 Shell 信息

```bash
ls *.py
# 列出所有 Python 文件

chsh -l
# 显示所有 shell 列表
```

### IPC 资源查看

```bash
ipcs -a
# 显示消息队列、信号量和共享内存的详情

ipcs -q
# 仅列出当前进程具有读取权限的消息队列

ipcs -s
# 列出可用的信号量

ipcs -m
# 列出所有共享内存
```

### 系统统计与监控

```bash
quotastats
# 显示从内核收集的配额系统统计报告

pcinfo
# 显示本地所有的 RPC（远程过程调用）服务

slabtop
# 实时显示内核 slab 缓存信息

tload
# 向指定的 tty 显示当前系统负载平均图表
```

### /proc 文件系统查看

```bash
cat /proc/devices
# 显示当前运行内核配置的设备驱动程序

cat /proc/dma
# 显示当前使用的 DMA 通道

cat /proc/filesystems
# 显示配置到内核中的文件系统

cat /proc/kmsg
# 显示内核生成的消息

cat /proc/loadavg
# 显示系统负载平均值

ls /proc/net
# 列出网络协议

ls /etc/udev
# 列出 udev 配置目录的内容

cat /proc/stat
# 显示系统运行统计数据

cat /proc/uptime
# 显示系统运行时间
```

### 系统关机与重启

```bash
poweroff -i -f
# 关闭系统
```

### Shell 逻辑与类型判断

```bash
[ 2 = 2 ]; echo $$
# 0 (逻辑为真)

[ 2 = 6 ]; echo $$
# 1 (逻辑为假)

type echo
# echo 是 shell 内置命令
```

### 文件查找

```bash
find /usr -print
# 查找并打印 "/usr" 下的所有文件
```

### Systemd 服务管理

```bash
systemctl list-units --type=target
# 列出所有 target 配置

systemctl list-timers
# 列出内存中所有的 timer

systemctl list-units --type=service
# 列出所有 service 配置

systemctl list-dependencies --all
# 列出所有单元服务的依赖关系

systemctl list-sockets
# 列出内存中所有的 socket 单元

systemctl poweroff
# 关闭系统

systemctl reboot
# 关闭并重启系统

systemctl suspend
# 挂起系统

systemctl hibernate
# 休眠系统
```

### 网络端口查看

```bash
netstat -ln --tcp
# 查找监听的 TCP 端口（数字形式）
```

### Logctl 状态查看

```bash
logctl user-status
# 显示调用者会话用户的简短运行状态信息

logctl session-status
# 显示调用者会话的简短运行状态信息
```

### IP 路由与邻居

```bash
ip route show
# 以数字地址显示所有路由表

ip neigh
# 显示邻居表（ARP 表）
```



# 显示 ARP（地址解析协议）缓存表的当前内容

```
netstat -l --inet
```

# 查找监听端口

```
atq -h
```

列出用户的待处理作业

```
lsof | grep deleted
```

# 打印所有声占用磁盘空间的已删除文件

```
echo $$\n
```

# 显示当前进程的进程 ID (PID)

```
echo $!
```

# 显示最近启动的后台作业的 PID

```
date --date="yesterday"
# 显示昨天的日期

date --date="10 days ago"
# 显示 10 天前的日期

ls | wc -w
# 列出根目录下的目录数量

sudo sfdisk -1 -uM
# 以 MB 显示每个分区的大小
```

```
sudo parted -l
# 列出分区详情

df -h | grep ^/dev
# 过滤出真实的硬盘分区/文件系统
```

```
sudo blkid
```

# 显示可用块设备的信息

```
ls / > info.txt
```

- bin
- boot
- dev
- etc
- home
- lib
- lib64
- media
- mnt
- opt
- proc
- root
- run
- sbin
- srv
- sys
- tmp
- usr
- var

```
export NAME="Albert Einstein"
echo $NAME
```

# 阿尔伯特·爱因斯坦

```
TZ=US/Pacific date
# 显示美国/太平洋时区的当前日期/时间
```

```
ls -l /etc/shadow
# 显示加密形式存储的用户密码和密码过期数据
```

```
sudo journalctl --since yesterday
# 显示从昨天开始的所有日志

sudo journalctl --since "2019-12-10 13:00:00"
# 显示从 2019-12-10 13:00:00 开始的所有日志
```

```
journalctl --disk-usage
# 显示日志文件的总大小
```

```
ls -m
# 用逗号分隔打印目录和文件
```

```
ls -Q
# 为所有目录和文件加上引号
```

```
echo -f unix
# 列出 Unix Socket

echo *.desktop
# 列出当前目录下所有的 .desktop 文件
```

```
ss --raw
```

# 列出原始套接字

```
tracepath www.google.com
```

# 追踪到网络主机 (www.google.com) 的路径，并发现沿途的 MTU

```
echo -e "123\b44"
124
```

```
echo -e "123\b44"
124
# 查找最后一次写入的共享内存
```

```
ipcs -m
# 列出所有共享内存
```

```
ipcs -q
# 消息队列详情
```

```
ipcs -s
# 列出可用的信号量
```

```
ipcs -m
# 列出所有共享内存
```

```
quotastats
# 显示从内核收集的配额系统统计报告
```

```
pcinfo
# 显示本地主机所有的 RPC（远程过程调用）服务
```

```
slabtop
# 实时显示内核 slab 缓存信息
```

```
tload
# 向指定的 tty 显示当前系统负载平均图表
```

```
cat /proc/devices
# 显示当前运行内核配置的设备驱动程序
```

```
cat /proc/dma
# 显示当前使用的 DMA 通道
```

```
cat /proc/filesystems
# 显示配置到内核中的文件系统
```

```
cat /proc/kmsg
# 显示内核生成的消息
```

```
cat /proc/loadavg
# 显示系统负载平均值
```

```
ls /proc/net
# 列出网络协议
```

```
ls /etc/udev
# 列出 udev 配置目录的内容
```

```
cat /proc/stat
# 显示系统运行统计数据
```

```
cat /proc/uptime
# 显示系统运行时间
```

```
poweroff -i -f
# 关闭系统
```

```
[ 2 = 2 ]; echo $$
# 0 (逻辑为真)

[ 2 = 6 ]; echo $$
# 1 (逻辑为假)

type echo
# echo 是 shell 内置命令
```

```
find /usr -print
# 查找并打印 "/usr" 下的所有文件

systemctl list-units --type=target
# 列出所有 target 配置

systemctl list-timers
# 列出内存中所有的 timer

systemctl list-units --type=service
# 列出所有 service 配置

systemctl list-dependencies --all
# 列出所有单元服务的依赖关系

systemctl list-sockets
# 列出内存中所有的 socket 单元

systemctl poweroff
# 关闭系统
```

```
systemctl reboot
# 关闭并重启系统
```

```
netstat -ln --tcp
# 查找监听的 TCP 端口（数字形式）
```

```
systemctl suspend
# 挂起系统
```

```
systemctl hibernate
# 休眠系统
```

```
logctl user-status
# 显示调用者会话用户的简短运行状态信息
```

```
logctl session-status
# 显示调用者会话的简短运行状态信息
```

```
ip route show
# 以数字地址显示所有路由表
```

```
ip neigh
# 显示 ARP（地址解析协议）缓存表的当前内容
```

```
netstat -l --inet
# 查找监听端口
```

```
atq -h
# 列出用户的待处理作业
```

```
lsof | grep deleted
# 打印所有声占用磁盘空间的已删除文件
```

```
echo $$\n
# 显示当前进程的进程 ID (PID)

echo $!
# 显示最近启动的后台作业的 PID
```

```
date --date="yesterday"
# 显示昨天的日期

date --date="10 days ago"
# 显示 10 天前的日期

ls | wc -w
# 列出根目录下的目录数量

sudo sfdisk -1 -uM
# 以 MB 显示每个分区的大小
```

```
sudo parted -l
# 列出分区详情

df -h | grep ^/dev
# 过滤出真实的硬盘分区/文件系统
```

```
sudo blkid
# 显示可用块设备的信息
```

```
ls / > info.txt
```

- bin
- boot
- dev
- etc
- home
- lib
- lib64
- media
- mnt
- opt
- proc
- root
- run
- sbin
- srv
- sys
- tmp
- usr
- var

```
export NAME="Albert Einstein"
echo $NAME
```

# 阿尔伯特·爱因斯坦

```
TZ=US/Pacific date
# 显示美国/太平洋时区的当前日期/时间
```

```
ls -l /etc/shadow
# 显示加密形式存储的用户密码和密码过期数据
```

```
sudo journalctl --since yesterday
# 显示从昨天开始的所有日志

sudo journalctl --since "2019-12-10 13:00:00"
# 显示从 2019-12-10 13:00:00 开始的所有日志
```

```
journalctl --disk-usage
# 显示日志文件的总大小
```

```
ls -m
# 用逗号分隔打印目录和文件
```

```
ls -Q
# 为所有目录和文件加上引号
```

```
echo -f unix
# 列出 Unix Socket

echo *.desktop
# 列出当前目录下所有的 .desktop 文件
```

```
ss --raw
# 列出原始套接字
```

```
tracepath www.google.com
# 追踪到网络主机 (www.google.com) 的路径，并发现沿途的 MTU
```

```
echo -e "123\b44"
124
```

```
ps -efH | more
# 以树形结构查看当前运行进程
```

## 命令

```
df -T
```

## Description

显示文件系统类型

```
mkdir ~/temp
# 在主目录下创建一个名为 temp 的目录
```

```
ls *.py
# 列出所有 Python 文件

chsh -l
# 显示所有 shell 列表

ipcs -a
# 显示消息队列、信号量和共享内存的详情
```

```
ipcs -q
# 仅列出当前进程具有读取权限的消息队列
```

```
ipcs -s
# 列出可用的信号量

ipcs -m
# 列出所有共享内存

quotastats
# 显示从内核收集的配额系统统计报告

pcinfo
# 显示本地主机所有的 RPC（远程过程调用）服务

slabtop
# 实时显示内核 slab 缓存信息

tload
# 向指定的 tty 显示当前系统负载平均图表
```

```
cat /proc/devices
# 显示当前运行内核配置的设备驱动程序
```

```
cat /proc/dma
# 显示当前使用的 DMA 通道
```

```
cat /proc/filesystems
# 显示配置到内核中的文件系统
```

```
cat /proc/kmsg
# 显示内核生成的消息
```

```
cat /proc/loadavg
# 显示系统负载平均值
```

```
ls /proc/net
# 列出网络协议
```

```
ls /etc/udev
# 列出 udev 配置目录的内容
```

```
cat /proc/stat
# 显示系统运行统计数据
```

```
cat /proc/uptime
# 显示系统运行时间
```

```
poweroff -i -f
# 关闭系统
```

```
[ 2 = 2 ]; echo $$
# 0 (逻辑为真)

[ 2 = 6 ]; echo $$
# 1 (逻辑为假)

type echo
# echo 是 shell 内置命令
```

```
find /usr -print
# 查找并打印 "/usr" 下的所有文件

systemctl list-units --type=target
# 列出所有 target 配置

systemctl list-timers
# 列出内存中所有的 timer

systemctl list-units --type=service
# 列出所有 service 配置

systemctl list-dependencies --all
# 列出所有单元服务的依赖关系

systemctl list-sockets
# 列出内存中所有的 socket 单元

systemctl poweroff
# 关闭系统
```

```
systemctl reboot
# 关闭并重启系统
```

```
netstat -ln --tcp
# 查找监听的 TCP 端口（数字形式）
```

```
systemctl suspend
# 挂起系统
```

```
systemctl hibernate
# 休眠系统
```

```
logctl user-status
# 显示调用者会话用户的简短运行状态信息
```

```
logctl session-status
# 显示调用者会话的简短运行状态信息
```

```
ip route show
# 以数字地址显示所有路由表
```

```
ip neigh
# 显示 ARP（地址解析协议）缓存表的当前内容
```

```
netstat -l --inet
# 查找监听端口
```

```
atq -h
# 列出用户的待处理作业
```

```
lsof | grep deleted
# 打印所有声占用磁盘空间的已删除文件
```

```
echo $$\n
# 显示当前进程的进程 ID (PID)

echo $!
# 显示最近启动的后台作业的 PID
```

```
date --date="yesterday"
# 显示昨天的日期

date --date="10 days ago"
# 显示 10 天前的日期

ls | wc -w
# 列出根目录下的目录数量

sudo sfdisk -1 -uM
# 以 MB 显示每个分区的大小
```

```
sudo parted -l
# 列出分区详情

df -h | grep ^/dev
# 过滤出真实的硬盘分区/文件系统
```

```
sudo blkid
# 显示可用块设备的信息
```

```
ls / > info.txt
```

- bin
- boot
- dev
- etc
- home
- lib
- lib64
- media
- mnt
- opt
- proc
- root
- run
- sbin
- srv
- sys
- tmp
- usr
- var

```
export NAME="Albert Einstein"
echo $NAME
```

# 阿尔伯特·爱因斯坦

```
TZ=US/Pacific date
# 显示美国/太平洋时区的当前日期/时间
```

```
ls -l /etc/shadow
# 显示加密形式存储的用户密码和密码过期数据
```

```
sudo journalctl --since yesterday
# 显示从昨天开始的所有日志

sudo journalctl --since "2019-12-10 13:00:00"
# 显示从 2019-12-10 13:00:00 开始的所有日志
```

```
journalctl --disk-usage
# 显示日志文件的总大小
```

```
ls -m
# 用逗号分隔打印目录和文件
```

```
ls -Q
# 为所有目录和文件加上引号
```

```
echo -f unix
# 列出 Unix Socket

echo *.desktop
# 列出当前目录下所有的 .desktop 文件
```

```
ss --raw
# 列出原始套接字
```

```
tracepath www.google.com
# 追踪到网络主机 (www.google.com) 的路径，并发现沿途的 MTU
```

```
echo -e "123\b44"
124
```

```
nmcli con show -a
# 显示活动连接

netstat -r
# 显示内核路由表

yum install nmap
# 在 CentOS 上安装 nmap

nmap google.com
# 扫描主机

nmap 193.169.1.1
# 扫描 IP 地址

nmap --iflist
# 显示主机接口和路由

echo [[:digit:]]
# 打印所有不以数字开头的文件和文件夹

echo *[[:lower:]123]
# 打印所有以小写字母或数字结尾的文件和文件夹

echo g*
# 打印所有以 "g" 开头的文件和文件夹

echo b*.txt
# 打印所有以 "b" 开头、包含任意字符并以 ".txt" 结尾的文件和文件夹

echo [abc]*
# 打印所有以 "a","b" 或 "c" 开头的文件和文件夹

netstat -t
# 显示活动连接的下载状态

netstat -x
# 显示网络直接（Network Direct）所有连接、监听器和共享端点的信息

netstat -n
# 以数字形式显示地址和端口号

echo $LANG
# 显示 Linux 系统的语言

echo "AAA" | grep AAA
# → AAA

echo "BBB" | grep -E 'AAA|BBB'
# → BBB

echo "AAA" | grep BBB
# →

echo "AAA" | grep -E 'AAA|BBB'
# → AAA

echo "albert einstein" | tr a-z A-Z
# ALBERT EINSTEIN

echo "albert einstein" | tr [:lower:]] E
# EEEEEE EEEEEE

echo "Albert Einstein was a German-born theoretical physicist." | fold -w 12

echo " Albert Einstein was a German-born theoretical physicist." | fold -w 12 -s

printf "English theoretical physicist: %s\n" Hawking
# English theoretical physicist: Hawking

ls /usr/bin | pr -3 -w 65 | head
# 以分页、三列输出格式显示 /usr/bin 的目录列表

for i in A B C D; do echo $i; done

Scientists=("Einstein" "Hawking" "Darwin"); for i in ${Scientists[*]}; do echo $i; done

for i in {A..D}; do echo $i; done

Scientists=("Einstein" "Hawking" "Darwin"); for i in "${Scientists[*]}"; do echo $i; done
```



# Linux 命令参考

## Shell 基础

```bash
for i in file*.txt; do echo $i; done
```

```bash
echo ${!BASH*}
```

# 列出所有以 BASH 开头的环境变量

```bash
bc <<< "6+6"
```

```bash
df -k
```

# 检查文件系统空间

```bash
ls -alh
```

# 详细列出目录下所有文件

```bash
find /home -name file.txt
```

# 检查 /home 目录下名为 file.txt 的文件

```bash
find /home -iname File.txt
```

# 忽略大小写搜索 /home

```bash
find / -ctime +90
```

# 查找 90 天前修改的文件

```bash
find / -size 0c
```

# 查找所有空文件

```bash
find / -size +1G
```

# 查找所有大于 1GB 的文件和文件夹

```bash
df -a
```

# 显示文件系统的完整磁盘占用

```bash
df -i
```

# 显示已用和空闲 inode

```bash
du -ch *.png
```

# 显示当前目录下每个 png 文件的大小

```bash
du -a /etc/ | sort -n -r | head -n 10
```

# 列出 /etc/ 中占用磁盘空间最大的 10 个目录

```bash
ac
```

# 显示用户连接到系统的总时间

```bash
ac --individual-totals
```

# 显示单个用户的登录时间报告

```bash
cancel
```

# 取消打印作业

```bash
yum install finger
```

# 安装 finger 工具 (CentOS)

```bash
finger manju
```

# 显示用户 "manju" 的详情

```bash
chfn
```

# 允许修改用户信息

```bash
finger -s manju
```

# 显示用户 "manju" 的空闲状态和登录详情

```bash
groups
```

# 列出用户所属的所有组

```bash
id -nG
```

# 列出用户所属的所有组

```bash
groupadd mygroup
```

# 创建名为 "mygroup" 的组

```bash
groupdel mygroup
```

# 删除名为 "mygroup" 的组

```bash
less /etc/group
```

# 查看所有组

```bash
getent group
```

```bash
usermod -a -G mygroup user
```

# 将用户加入组

```bash
userdel user
```

# 删除用户

```bash
chgrp mygroup file
```

# 修改文件的组

```bash
chgrp mygroup
```

# 修改文件的组

```bash
chown user file
```

# 修改文件的所有者

```bash
du -sh /dir
```

# 显示目录的大小

```bash
du -h file
```

# 显示文件的大小

## 网络与路由

```bash
netstat -rn
```

# 显示绑定到服务器的所有 IP 地址的路由表

```bash
netstat -an
```

# 显示与服务器的所有活动连接的信息

## 文件查看与处理

```bash
od -b myfiles.txt
```

# 以八进制格式显示 "myfiles.txt" 的内容

```bash
od -Ax -c myfiles.txt
```

# 以 ASCII 字符格式显示 "myfiles.txt" 的内容 - 字节偏移以十六进制显示

## 信号处理

```bash
trap -l
```

# 显示信号名称及其对应数字列表

```bash
trap
```

# 显示当前设置的信号陷获器列表

## 包管理

```bash
yum list openssh
```

# 搜索名为 "OpenSSH" 的软件包

```bash
yum grouplist
```

# 列出所有可用的组软件包

```bash
yum repolist
```

# 列出所有启用的 Yum 仓库

```bash
yum repolist all
```

# 列出所有已启用和禁用的 Yum 仓库

## 文件合并与格式化

```bash
paste 1.txt 2.txt
```

# 并排显示 1.txt 和 2.txt 的内容

```bash
ls -a | pr -n -h "Files in $(pwd)" > dc.txt
cat dc.txt
```

| 2022-04-02 01:10 | Files in /home/manju | Page 1 |
| :--- | :--- | :--- |
| 1 | | |
| 2 | .. | |
| 3 | 1.txt | |
| 4 | 2.txt | |
| 5 | .bash_history | |
| 6 | .bash_logout | |
| 7 | .bash_profile | |
| 8 | .bashrc | |
| 9 | bio.txt | |
| 10 | .cache | |
| 11 | .config | |
| 12 | Data.txt | |
| 13 | Desktop | |
| 14 | dir | |
| 15 | Documents | |

```bash
printf "Hi, I'm %s.\n" $LOGNAME
```

-> Hi, I'm manju.

```bash
printf "%.*s" 6 "abcdef"
```

-> abcdef

## 进程管理

```bash
ps -eLF
```

# 获取关于线程的信息

```bash
ps axms
```

# 获取关于线程的信息

- `ps -eo euser,ruser,suser,user,f,comm,label`
- `ps axZ`
- `ps -eM`

![](img/df24534eff215443b1bf728f904e6756_283_0.png)

| Command | Description |
| :--- | :--- |
| `pstree -h` | 以树形式显示所有进程，并高亮当前进程及其祖进程 |

| Command | Description |
| :--- | :--- |
| `rm -- 1.txt` | 删除当前目录下的 "1.txt" 文件 |
| `rm /1.txt` | 删除根目录下的 "1.txt" 文件 |
| `rm /home/manju/2.txt` | 删除 "/home/manju" 目录下的 "2.txt" 文件 |

```bash
ip route list
```

# 列出当前路由表

```bash
route -n
```

# 显示绑定到服务器的所有 IP 的路由表

## 会话记录

```bash
script -c 'echo "Hello, World!"' hello.txt
```

```
Script started, file is hello.txt
Hello, World!
Script done, file is hello.txt
```

```bash
cat hello.txt
```

```
Script started on Sat 02 Apr 2022 03:24:52 AM PDT
Hello, World!
Script done on Sat 02 Apr 2022 03:24:52 AM PDT
```

## 磁盘与文件系统

```bash
sfdisk -s
```

# 列出所有磁盘的大小

```bash
ls -d ~/.ssh
```

# 检查 .ssh 目录是否存在

```bash
sha224sum myfiles.txt
```

# 显示当前目录下 "myfiles.txt" 文件的 SHA224 校验和

```bash
sha256sum myfiles.txt
```

# 显示当前目录下 "myfiles.txt" 文件的 SHA256 校验和

```bash
sha384sum myfiles.txt
```

# 显示当前目录下 "myfiles.txt" 文件的 SHA384 校验和

```bash
sha512sum myfiles.txt
```

# 显示当前目录下 "myfiles.txt" 文件的 SHA512 校验和

## 系统关机与延迟

```bash
shutdown 8:00
```

# 计划系统在早上 8 点关机

```bash
shutdown 20:00
```

# 计划系统在晚上 8 点关机

```bash
shutdown +15 "The system will be shut down in 15 minutes."
```

# 计划在 15 分钟后关机，并带有正常消息提示用户系统正在关机

```bash
shutdown -P now
```

# 立即关闭系统

```bash
sleep 10
```

# 延迟 10 秒

```bash
startx --depth 16
```

# 以 16 位色深启动 X 会话

## 时间与文本处理

```bash
time cal
```

# 报告 "cal" 命令完成所需的时间

```bash
tr "[:lower:]" "[:upper:]" < myfiles.txt
```

# 将 "myfiles.txt" 的内容翻译为大写

```bash
tr -cd "[:print:]" < myfiles.txt
```

# 从 "myfiles.txt" 中删除所有非打印字符

| Hello World |
| :--- |

| # 列出默认 X 服务器和显示所有可用字体 |
| :--- |

```bash
tr -cs "[:alpha:]" "\n" < myfiles.txt
```

```
Hello
World
```

```bash
uncompress myfiles.txt.xz
```

# 解压缩文件 "myfiles.txt.xz"

# 为名为 "manju" 的用户显示信息

```bash
write albert
```

# 向用户 "albert" 发送消息

![](img/df24534eff215443b1bf728f904e6756_286_0.png)

| Command | Description |
| :--- | :--- |
| `yes \| rm -i *.txt` | 删除当前目录下所有 .txt 扩展的文件 |

# 什么是 Linux，以及它为什么如此受欢迎？

无论你是否知道，你每天都在使用 Linux（最知名且使用最广泛的开源操作系统）。从超级计算机到智能手机，Linux 操作系统无处不在。作为一种操作系统，Linux 是一个基于 Linux 内核的开源 Unix 类软件家族 - 它们位于计算机上所有其他软件之下，接收这些程序的请求并将这些请求转发给计算机硬件。在职业发展方面，拥有 Linux 技能比仅仅知道如何使用 Windows 越来越有用。通常而言，Linux 比 Windows 更难管理，但提供了更多的灵活性和配置选项。

每台桌面电脑都使用操作系统。今天最流行的操作系统有：Windows、Mac OS 和 Linux。

操作类型、调用应用程序等。由于招聘重点正越来越多地向 DevOps 类型的技能转移，Linux 技能组将是使你极具部署能力的类型。

## Shell 扩展与变量示例

```bash
[manju@localhost ~]$ echo al{an,bert,alexander}
an albert alexander

[manju@localhost ~]$ mkdir {txt,doc,pdf}
[manju@localhost ~]$ ls
txtfiles pdffiles
```

```bash
[manju@localhost ~]$ x=Albert; y="$x won \$100.00"; echo $y
Albert won $100.00

[manju@localhost ~]$ x=5; test $x -eq 10; echo $?
exit status of the test command is 1

[manju@localhost ~]$ x=5; test $x -eq 5; echo $?
exit status of the test command is 0
```

## 配置文件查看

```bash
cat /etc/profile
```

# 显示系统登录初始化文件

```bash
cat /etc/bashrc
```

# 显示系统 BASH shell 配置文件

```bash
cat .bash_profile
```

# 显示登录初始化文件

## 环境变量示例

```bash
[manju@localhost ~]$ date
Wed Sep 28 08:14:17 PDT 2022

[manju@localhost ~]$ alias x=date
[manju@localhost ~]$ x
Wed Sep 28 08:14:27 PDT 2022
```

```bash
[manju@localhost ~]$ echo $BASH_VERSION
4.26(1)-release
```

```bash
[manju@localhost ~]$ echo $HISTCMD
290
```

```bash
[manju@localhost ~]$ echo $HOSTTYPE
x86_64
```

```bash
[manju@localhost ~]$ echo $OSTYPE
linux-gnu
```

```bash
[manju@localhost ~]$ echo $PPID
3563
```

```bash
[manju@localhost ~]$ echo $SHLVL
2
```

```bash
[manju@localhost ~]$ echo $TERM
xterm-256color
```

```bash
[manju@localhost ~]$ echo $EUID
1000
```

- 显示当前的 BASH 版本号
- 显示历史列表中当前命令的次数
- 显示主机运行的机器类型
- 显示正在使用的操作系统
- 显示 shell 父进程的进程 ID
- 显示当前的 shell 层级
- 显示终端类型
- 显示有效用户 ID (EUID)

## PS1 提示符定制

```bash
[manju@localhost ~]$ PS1="\d"
Sun Oct 02 # 显示当前日期

[manju@localhost ~]$ PS1="\h"
localhost # 显示主机名

[manju@localhost ~]$ PS1="\s"
bash # 显示当前激活的 Shell 类型

[manju@localhost ~]$ PS1="\t"
18:42:10 # 显示时、分、秒的时间

[manju@localhost ~]$ PS1="\u"
manju # 显示用户名

[manju@localhost ~]$ PS1="\v"
4.2 # 显示 Shell 版本
```

| PS1 值 | 说明 |
| :--- | :--- |
| `PS1="\w"` | 显示当前工作目录的完整路径 |
| `PS1="\W"` | 显示当前工作目录的名字 |

```bash
[manju@localhost ~]$ PS1="\n World"
Hello
World

[manju@localhost ~]$ PS1="Hello \ World"
Hello \ World
```

## 目录结构

| 目录 | 功能 |
| :--- | :--- |
| `/` | Linux 系统的顶层目录，包含了组织成目录的所有文件、设备信息和系统信息 |
| `/home` | 存放用户的“家目录” |
| `/bin` | 包含每个基本的命令和实用程序 |
| `/usr` | 包含命令和实用程序 |

## 正则表达式与 grep

```bash
grep "^[[:space:]]" myfiles.txt
```

# 在 "myfiles.txt" 中搜索以空格字符开头的行

```bash
grep "^[[:upper:]]" myfiles.txt
```

# 在 "myfiles.txt" 中搜索以大写字母开头的行

```bash
grep "^[[:xdigit:]]" myfiles.txt
```

# 在 "myfiles.txt" 中搜索以十六进制数字开头的行

## 内存与虚拟内存统计

```bash
vmstat -a
```

# 显示活动和闲内存

```bash
vmstat -s
```

# 显示内存和调度统计

```bash
vmstat -f
```

# 显示系统启动以来创建的 fork 数量

```bash
vmstat -D
```

# 显示所有磁盘活动的快速摘要统计信息

```bash
vmstat -d
```

# 显示每个磁盘使用情况的详细统计

```bash
vmstat 5 -S M
```

# 此命令用于每五秒更新一次统计信息，并将显示单位改为兆字节

```bash
[manju@localhost ~]$ free -h --total
```

```markdown
| total | used | free | shared | buff/cache | available |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Mem: | 976M | 566M | 75M | 8.7M | 334M | 209M |
| Swap: | 2.0G | 84K | 2.0G | | | |
| Total: | 3.0G | 566M | 2.1G | | | |
```

- `hostname -s`
- `hostname --short`

![](img/df24534eff215443b1bf728f904e6756_302_0.png)

```bash
hostname --all-ip-addresses
```

# 显示所有网络地址

```bash
date -r /etc/hosts
```

# 显示日期文件的最后修改时间戳

## 文件重定向与 cat 命令

```bash
[manju@localhost ~]$ cat 1.txt
Albert Einstein

[manju@localhost ~]$ cat 2.txt
Elsa Einstein

[manju@localhost ~]$ cat 1.txt > 2.txt

[manju@localhost ~]$ cat 2.txt
Albert Einstein
```

```bash
[manju@localhost ~]$ cat 12.txt
Albert Einstein
Elsa Einstein

[manju@localhost ~]$ cat -n 12.txt
1 Albert Einstein
2 Elsa Einstein
```

```bash
[manju@localhost ~]$ cat 1.txt
Albert Einstein

[manju@localhost ~]$ cat -e 1.txt
Albert Einstein$
```

## 关机与广播

```bash
sudo shutdown 08:00
```

# 在早上 8 点关机系统

## 多模式搜索

```bash
grep 'but\|is' phy.txt
```

# 在 phy.txt 文件中搜索单词 "but" 和 "is"

```bash
grep 'is\|but\|of' phy.txt
```

# 在 phy.txt 文件中搜索单词 "but", "is" 和 "of"

```bash
grep -e but -e is -e of phy.txt
```

```bash
echo "The system will be shutdown in 10 minutes." | wall
```

消息（系统将在 10 分钟后关机）将广播给所有当前登录的用户

## echo 转义示例

```bash
[manju@localhost ~]$ echo -e 'Albert Einstein'
Albert Einstein

[manju@localhost ~]$ echo -e 'Albert \c Einstein'
```



Albert `[manju@localhost ~]$`

```bash
ss --all
# 列出所有监听和非监听连接
```

```bash
ss --listen
# 仅列出监听的套字
```

```bash
ss -t state listening
# 查找所有监听的 TCP 连接
```

```bash
[manju@localhost ~]$ hostname -I | awk '{print $1}'
192.168.6.131
```

```bash
yum erase httpd
# 卸载 apache
```

- 读 (read) 的值为 4
- 写 (write) 的值为 2
- 执行 (execute) 的值为 1
- 无权限 (no permission) 的值为 0

```bash
chmod 644 1.txt
# 用户: 6 = 4 + 2 (读和写)
# 组: 4 = 4 + 0 + 0 (读)
# 其他: 4 = 4 + 0 + 0 (读)
```

- 7 = 4 + 2 + 1 (读、写和执行)
- 6 = 4 + 2 + 0 (读和写)
- 5 = 4 + 0 + 1 (读和执行)
- 4 = 4 + 0 + 0 (读)

```bash
rpm -qi httpd
# 显示特定软件包 (apache) 的信息
```

```bash
sudo rpm -qa | wc -l
# 显示已安装软件包的总数
```

```bash
sudo repoquery -a --installed
# 使用 repoquery 命令列出所有已安装软件包
```

```bash
cat /var/log/boot.log
# 显示所有与启动操作相关的信息
```

```bash
cat /var/log/maillog
# 显示所有与邮件服务器和邮件存档相关的信息
```

```bash
cat /var/log/yum.log
# 显示 Yum 命令日志
```

```bash
mkdir -m777 myfiles
# 创建一个具有读、写、执行权限的目录 "myfiles"
```

```bash
rpm -qa centos-release
# 显示 CentOS 版本
```

```bash
ps -A1FH
# 获取线程信息 (LWP 和 NLWP)
```

```bash
ps -eM
ps axZ
# 获取 Linux 进程的安全信息
```

```bash
ps -auxf | sort -nr -k 4 | head -10
# 显示内存消耗最高的 10 个进程
```

```bash
ps -auxf | sort -nr -k 3 | head -10
# 显示 CPU 消耗最高的 10 个进程
```

```bash
sar -n DEV | more
# 监控、收集和报告 Linux 系统活动
```

```bash
# 创建或覆盖 "1.txt" 文件
echo "Albert Einstein" > 1.txt
# 创建或追加到 "1.txt" 文件
echo "Albert Einstein" >> 1.txt
```

```bash
grep -i "is" phy.txt
# 在文件 "phy.txt" 中搜索给定字符串
```

```bash
grep -A 3 -i "is" phy.txt
# 匹配行及其后续三行
```

```bash
grep -r "is" *
# 在所有文件中递归查找给定字符串
```

```bash
export |
```

```bash
# 在文件 "phy.txt" 中搜索给定字符串
grep -A 3 -i "is" phy.txt
# 匹配行及其后续三行
```

```bash
grep -r "is" *
# 在所有文件中递归查找给定字符串
```

```bash
export |
```

```bash
sudo netstat -anp | grep tcp | grep LISTEN
# 显示各种正在使用的端口以及使用它的进程
```

```bash
sudo netstat -anp | grep 8080
# 显示监听在端口 8080 进程
```

```bash
printf "%s\n" *
# 打印当前目录下的文件和目录
```

```bash
printf "%s\n" */
# 仅打印当前目录下的目录
```

```bash
printf "%s\n" *.{gif,jpg,png}
# 列出某些图像文件
```

```bash
[manju@localhost ~]$ alias x='date'  # 创建别名
[manju@localhost ~]$ x  # 预览别名
Fri Oct 7 03:51:39 PDT 2022
[manju@localhost ~]$ unalias x  # 移除别名
[manju@localhost ~]$ x
bash: x: command not found.
```

```bash
[manju@localhost ~]$ x="alan"; printf '%s\n' "${x^}"
Alan
```

```bash
[manju@localhost ~]$ x="alan"; printf '%s\n' "${x^^}"
ALAN
```

```bash
[manju@localhost ~]$ x="alan"; declare -u name="$x"; echo "$name"
ALAN
```

```bash
find . -name "xyz[a-z][0-9]"
# 查找以 "xyz" 开头并在一位数字后跟一个字母的目录和文件
```

```bash
find . -mmin -120
# 搜索过去两个小时内更改过的文件
```

```bash
find . -mmin +120
# 搜索过去两小时内未更新的文件
```

```bash
find . -mtime -3
# 查找过去 3 天内修改过的文件
```

```bash
find . -mtime +3
# 查找过去 3 天内未修改过的文件
```

```bash
[manju@localhost ~]$ names="Albert Alan John Mary"; x=(${names// //}); echo ${x[0]};
Albert
```

```bash
[manju@localhost ~]$ names="Albert Alan John Mary"; x=(${names// //}); echo ${x[3]};
Mary
```

```bash
names="Albert+Alan+John+Mary"
x=(${names//+/});
echo ${x[0]}
# 输出: Albert
```

```bash
names="Albert+Alan+John+Mary"
x=(${names//+/});
echo ${x[3]}
# 输出: Mary
```

```bash
x=(hello world); echo "${x[@]/#/A}"
# 输出: Ahello Aworld
```

```bash
[manju@localhost ~]$ awk '{print $2}' <<< "Alan Mathison Turing"
Mathison
```

```bash
[manju@localhost ~]$ awk '{print $1}' <<< "Alan Mathison Turing"
Alan
```

```bash
x='4 * 2'; echo "$x"
# 打印 4 * 2
```

```bash
x='4 * 2'; echo $x
# 打印 4，当前目录下的文件列表和 2
```

```bash
x='4 * 2'; echo "$(($x))"
# 打印 8
```

```bash
[manju@localhost ~]$ x="ALAN"; printf '%s\n' "${x,}"
aALAN
```

```bash
[manju@localhost ~]$ x="ALAN"; printf '%s\n' "${x,,}"
alan
```

```bash
[manju@localhost ~]$ x="ALAN"; echo "${x~~}"
aALAN
```

```bash
[manju@localhost ~]$ x="ALAN"; echo "${x~}"
alan
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x/a/A}"
You Are A genius
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x//a/A}"
You Are A geniusu
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x/%s/N}"
You are a geniuN
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x/s/}"
You are a genius
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x#*a}"
re a genius
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x#*g}"
enius
```

```bash
[manju@localhost ~]$ foo=25; i=foo; echo ${i}
foo
```

```bash
[manju@localhost ~]$ foo=25; i=foo; echo ${!i}
25
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x%*a}"
You are
```

```bash
[manju@localhost ~]$ x='You are a genius'; echo "${x%%*a}"
Youou
```

```bash
[manju@localhost ~]$ x=Bob-Dev-Fox; echo ${x%%-*}
Bob
```

```bash
[manju@localhost ~]$ x=Bob-Dev-Fox; echo ${x%-*}
Bob-Dev
```

```bash
[manju@localhost ~]$ x=Bob-Dev-Fox; echo ${x###-*}
Fox
```

```bash
[manju@localhost ~]$ x=Bob-Dev-Fox; echo ${x#*-}
Dev-Fox
```

```bash
find -type f -path '*/Documents/*'
# 查找名为 Documents 的文件夹内的文件
```

```bash
find -type f -path '*/Documents/*' -o -path '*/Downloads/*'
# 查找 Documents 或 Downloads 文件夹内的文件
```

```bash
find -type f -not-path '*/Documents/*' -not-path '*/Downloads/*'
# 查找 Documents 或 Downloads 文件夹以外的所有文件
```

```bash
find -type f -not-path '*/Documents/*' -not-path '*/Downloads/*' -not-path '*/log'
# 查找 Documents、Downloads 或 log 文件夹以外的所有文件
```

```bash
find -maxdepth 1 -type f -name "*.txt"
# 在当前目录下查找 .txt 文件
```

```bash
ps -eF --sort -nl | head
ps -eF
# 显示进程线程信息
```

> "Linux 是对古董的精美复制——比原始版本更亮，但仍由它定义。"
>
> — Jaron Lanier, [You Are Not a Gadget](https://example.org/wiki/You_Are_Not_a_Gadget)

## 每位超级用户都应该阅读的 Linux 经典：

- [How Linux Works: What Every Superuser Should Know] - Brian Ward
- [The Linux Programming Interface] - Michael Kerrisk
- [Linux pocket guide] - Daniel J. Barrett
- [Linux for Beginners] - Jason Cannon
- [How Linux Works: What Every Superuser Should Know] - Brian Ward
- [Linux Kernel Development] - Robert Love
- [Linux: The Complete Reference] - Richard Petersen
- [Linux in a Nutshell] - Ellen Siever and Robert Love
- [Linux Basics for Hackers: Getting Started with Networking, Scripting, and Security in Kali] - OccupyTheWeb
- [Linux Command Line and Shell Scripting Bible] - Christine Bresnahan and Richard Blum
- [Linux Administration: The Linux Operating System and Command Line Guide for Linux Administrators] - Jason Cannon
- [The Art of Unix Programming] - Eric S.Raymond
- [The Linux Command Line, 2nd Edition: A Complete Introduction] - William Shotts
- [Linux Bible] - Christopher Negus
- [Linux System Programming: Talking Directly to the Kernel and C Library] - Robert Love
- [A Practical Guide to Linux Commands, Editors, and Shell Programming] - Mark G. Sobell
- [Linux for Beginners and Command Line Kung Fu] - Jason Cannon
- [Linux Device Drivers] - Alessandro Rubini, Greg Kroah-Hartman, and Jonathan Corbet
- [Advanced Linux programming] - Alex Samuel, Jeffrey Oldham, and Mark Mitchell
- [Understanding the Linux Kernel] - Daniel Pierre Bovet and Marco Cesati
- [Learn Linux Quickly: A Beginner-friendly Guide to Getting Up and Running with the World's Most Powerful Operating System] - Ahmed Alkabary
- [Linux administration] - Wale Soyinka
- [Linux For Dummies] - Richard Blum
- [Linux Essentials] - Christine Bresnahan and Richard Blum
- [The Linux Command Line Beginner's Guide] - Jonathan Moeller
- [Linux All-in-One for Dummies] - Emmett Dulaney
- [Learning the bash Shell] - Cameron Newham
- [Linux for Developers: Jumpstart Your Linux Programming Skills] - William "Bo" Rothwell
- [Lfm: Linux Field Manual] - Tim Bryant
- [CompTIA Linux+ Study Guide: Exam XK0-005] - Christine Bresnahan and Richard Blum
- sed & awk
- Arnold Robbins 和 Dale Dougherty 所著的书籍
- Linux From Scratch
- Gerard Beekmans 所著的书籍

**Linux** 是群体智慧的一个复杂案例。它是一个很好的范例，意义在于它向你展示了如何以去中心化的方式让人们工作——也就是说，没有人真正地引导他们朝着某个**特定方向**努力——但仍然相信他们会给出完美的答案。

> - James Surowiecki

## 最后的想法：

如果你觉得这些信息对你有所帮助，请花一点时间在 LinkedIn、Facebook 和 Twitter 上与你的朋友分享。如果你觉得这本书对你的 Linux 管理员职业有所帮助，并且你学到了有价值的内容，请考虑在 Google Play Books 上写简短的评论。

从宏观角度来看，我相信 Linux 是不可思议的。这是一个极的平台，作为一个中立、可靠的枢纽，为开发者和企业组织构建、管理和扩展开源技术项目及生态系统。我希望将我的热情传递给尽可能多的人。希望这并不是你学习的终点。

## 谢谢！

我漏掉任何命令了吗？请告诉我！发送邮件给我 manjunath5496@gmail.com



# 面向新型 GNU/Linux 用户的命令行指南

你是一个想要学习不仅仅是拖动窗口和点击鼠标的新型 GNU/Linux 用户吗？本书为完全接触 GNU/Linux 命令行并想要学习基础知识的用户而设计。书中涵盖了用于导航、文件和目录管理、软件安装以及基础系统故障排除的 Linux 命令。你将在书中发现如何使用这些 Linux 命令。

多年来，Linux 经历了巨大的变革，目前被认为是世界上顶级操作系统之一。作为系统管理员，你维护着全球计算基础设施的功能。问题必须被解决，系统必须被维护，并且必须随时保持安全。希望这些命令对你有帮助，并让你能够更高效地完成工作。
