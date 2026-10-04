
main()
{
    char message[] = "Print straight to console\n";
    
    if (printcons(message, strlen(message))==-1)
        printf("Error occurred in printcons() call\n");
}

_syscall2() 宏在这里被使用，因为我们的系统调用有两个参数。该宏本身将在你的程序中展开为一个名为 printcons() 的函数，随后的 main() 内部调用将执行它。预处理器生成的程序中 printcons() 函数内部的代码将包含加载系统调用参数值到适当的 CPU 寄存器所需的所有机器代码指令，然后执行 int 0x80 异常。当异常返回时，将检查来自你的内核函数的返回值，并将适当的值返回给 main() 中的代码。

## Linux 排列索引

本书中没有直接涵盖许多命令、系统调用、库函数和其他 Linux 设施。使用这些设施最大的困难之一就是首先发现它们存在。本索引旨在使找到那些否则会保持未知的许多设施变得更容易。

为此，我收集了大量存在手册页的设施的名称，以及这些设施的简单描述，并根据名称和描述中的关键词创建了索引。

为了使用该索引，你需要做的就是想出一个或多个可能与你感兴趣的主题相关的关键词，然后查找这些关键词。你会找到包含你的关键词的任何设施的名称、手册章节和描述的列表。

例如，假设你不知道如何在软盘上删除一个 DOS 文件。这里明显的关键词可能是：delete 或 DOS。事实上，这两者中的任何一个都会引导你发现手册第 (1) 节中的 mdel 命令。

对关键词 delete 进行索引查找将给出以下条目：

- delete - lprm (1) - 删除排队的打印机作业
- delete - mdel (1) - mtools 删除 DOS 文件
- delete - rm (1) - 删除文件
- delete - rmdir (1) - 删除空目录
- delete - rmdir (2) - 删除一个目录
- delete_module - delete_module (2) - 内核可加载模块支持

正如你所见，你不仅会得到 mdel 的线索，还会得到其他与删除其他事物相关的命令和函数。你应该记住，在你的系统上，你可用的手册页列表取决于你安装的 Linux 发行版以及你选择加载的该发行版的软件包。

; . (1) - bash 内置命令
; : (1) - bash 内置命令
1970 - kernel_mktime (9) - 将 struct mktime 转换为自 1970 年 1 月 1 日以来的秒数
8086 - vm86 (2) - 进入虚拟 8086 模式
abnormal - abort (3) - 导致异常进程终止
abort - abort (3) - 导致异常进程终止
abs - abs (3) - 绝对值数学函数
absolute - abs (3) - 绝对值数学函数
absolute - fabs (3) - 浮点数的绝对值
absolute - labs (3) - long int 的绝对值
absolute - realpath (3) - 从相对路径名或符号链接创建绝对路径名
accept - accept (2) - 在套接字上接受连接
access - access (2) - 检查用户对文件的权限
accounting - acct (2) - 开启或关闭进程记账
accounting - pac (8) - 显示打印机记账信息
acct - acct (2) - 开启或关闭进程记账
acos - acos (3) - 反余弦三角函数
acosh - acosh (3) - 逆双曲余弦三角函数
across - gpm (1) - 在虚拟控制台之间剪切和粘贴
addtinfo - addtinfo (1) - 修改 troff 字体文件以供 groff 使用
addmntent - addmntent (3) - 访问 fstab 和 mtab 文件条目
address - elmalias (1) - 展开并显示 elm 地址别名
address - mailaddr (7) - 邮件地址描述
address - newalias (1) - 安装新的 elm 邮件地址别名
addresses - inet_addr, inet_network, inet_ntoa, inet_makeaddr, inet_lnaof, inet_netof (3) - 操作 Internet 地址
add_timer - add_timer (9) - 内核事件定时器
adjtimex - adjtimex (2) - 调整内核时钟
adjust_clock - adjust_clock (9) - 根据时区值将内核时钟设置为 GMT
administrative - intro (8) - 管理/特权命令简介
Adobe - afa2tfm (1) - 将 Adobe 字体度量转换为 TeX 字体度量
afm2tfm - afm2tfm (1) - 将 Adobe 字体度量转换为 TeX 字体度量
afmtodit - afmtodit (1) - 创建供 groff 使用的字体文件
afs.syscall - afs.syscall (2) - 未实现的系统调用
agetty - agetty (8) - 用于登录提示的 getty
alarm - alarm (2) - 设置闹钟信号的时钟
alias - alias (1) - bash 内置命令
alias - checkalias (1) - 测试别名是否已定义
aliases - elmalias (1) - 展开并显示 elm 地址别名
aliases - listalias (1) - 显示 elm 别名
aliases - newalias (1) - 安装新的 elm 邮件地址别名
alloca - alloca (3) - 分配内存
allocate - alloca (3) - 分配内存
allocation - calloc, malloc, free, realloc (3) - 动态内存分配函数
alphasort - alphasort (3) - 按特定属性搜索目录条目
alter - renice (8) - 修改正在运行进程的优先级
amount - sleep (1) - 休眠指定时间
amount - sleep (3) - 休眠指定时间
amslatex - amslatex (1) - 文本格式和排版
amstex - amstex (1) - 文本格式和排版
anagram - strfry (3) - 生成字符串的字母异位词
analog - xclock (1) - X-windows 的模拟和数字时钟
analysis - gnua (6) - 生成国际象棋对局分析
analyzer - flex (1) - 快速词法分析器生成器
anonymous - pipe (2) - 创建匿名管道
another - write (1) - 向另一用户发送消息
ANSI - ansi2knr (1) - 将 ANSI C 转换为 Kernighan & Ritchie C
ansi2knr - ansi2knr (1) - 将 ANSI C 转换为 Kernighan & Ritchie C
answer - answer (1) - elm 电话留言系统
a.out - ld.so (8) - a.out 链接器
application's - appres (1) - 列出应用程序的 X 资源
applications - xlsclients (1) - 列出在显示器上运行的客户端应用程序
appres - appres (1) - 列出应用程序的 X 资源
apropos - apropos (1) - 列出与查询相关的手册条目
ar - ar (1) - 创建、修改和从归档中提取
arc - acos (3) - 反余弦三角函数
arc - asin (3) - 反正弦三角函数
arc - atan (3) - 反正切三角函数
arc - atan2 (3) - 双变量反正切三角函数
arch - arch (1) - 显示处理器架构
architecture - arch (1) - 显示处理器架构
archive - funzip (1) - 从 ZIP 归档中提取文件
archive - ranlib (1) - 为 ar 归档生成索引
archive - size (1) - 列出归档和目标文件中的节大小
archive - unzip (1) - 从 zip 归档中提取压缩文件
archive - zip, zipcloak, zipnote, zipsplit (1) - 打包和压缩（归档）文件
archive - zipinfo (1) - 列出 zip 归档的详细信息
archives - ar (1) - 创建、修改和从归档中提取
archives - cpio (1) - 复制文件到归档和从归档复制
archives - fiz (1) - 从损坏的 zoo 归档中恢复数据
archives - shar (1) - 创建 shell 归档
archives - unzipsfx (1) - 创建自解压 zip 归档
archives - zoo (1) - 操作压缩文件归档
archiving - tar (1) - 磁带归档实用程序
argument - stdarg (3) - 可变参数列表宏
ARP - arp (8) - 操作系统 ARP 表
arp - arp (8) - 操作系统 ARP 表
array - bcmp, bcopy, bzero, memccpy, memchr, memcmp, memcpy, memfrob, memmem, memmove, memset (3) - 字节数组操作
array - bsearch (3) - 在已排序数组中进行二分搜索
array - qsort (3) - 快速排序数组
as - banner (6) - 以大横幅形式打印文本
as - pstree (1) - 以树形显示进程层次结构
as - znew (1) - 将 .Z 文件重新压缩为 .gz 文件
ascii - ascii (7) - ascii 字符集
ascii - asctime, ctime, difftime, gmtime, localtime, mktime (3) - 将日期和时间转换为 ascii
ascii - hexdump (1) - 以十六进制、十进制、ascii 和八进制显示文件内容
ascii - pfbtops (1) - 将 .pfb postscript 字体转换为 ascii
ascii - uuencode (1) - 对二进制文件进行 ascii 编码
asctime - asctime (3) - 将日期和时间转换为 ascii
asin - asin (3) - 反正弦三角函数
asinh - asinh (3) - 逆双曲正弦三角函数
assert - assert (3) - 如果断言为假则终止进程
assertion - assert (3) - 如果断言为假则终止进程
assign - putenv (3) - 为环境变量赋值
at - at (1) - 操作稍后执行的批处理作业
atan - atan (3) - 反正切三角函数
atan2 - atan2 (3) - 双变量反正切三角函数
atanh - atanh (3) - 逆双曲正切三角函数
atexit - atexit (3) - 在程序终止时调用函数
atobm - atobm (1) - X11 的位图编辑器和实用程序
atof - atof (3) - 将字符串转换为 double
atoi - atoi (3) - 将字符串转换为整数
atol - atol (3) - 将字符串转换为长整数
atoms - xlsatoms (1) - 列出服务器上定义的已驻留原子
atq - atq (1) - 操作稍后执行的批处理作业
atrm - atrm (1) - 操作稍后执行的批处理作业
atrun - atrun (8) - 运行排队稍后执行的批处理作业
attribute - mattrb (1) - 更改 DOS 文件的属性位标志
attributes - chattr (1) - 在第二扩展文件系统中更改文件属性
attributes - lsattr (1) - 列出第二扩展文件系统上的文件属性
attributes - rcs (1) - 更改修订控制系统文件属性
attributes - scandir, alphasort (3) - 按特定属性搜索目录条目
attributes - setterm (1) - 设置终端属性
attributes - termios, tcgetattr, tcsetattr, tcsendbreak, tcdrain, tcflush, tcflow, cfgetospeed, cfgetispeed, cfsetispeed, cfsetospeed (2) - 获取和设置终端属性和控制
audio - workbone (1) - 在 CD-ROM 驱动器上播放音频光盘
audio - workman (1) - 在 CD-ROM 驱动器上播放音频光盘
authority - mcookie (1) - 为 X 授权系统生成魔术 cookie
authority - xauth (1) - X11 授权文件实用程序
authorization - iceauth (1) - 显示或设置 ICE 授权信息
auto-key - kbrdate (8) - 设置键盘自动按键重复率和初始重复延迟时间
automatic - depmod, modprobe (1) - 可加载模块的自动处理
average - tload (1) - 提供系统负载平均值的图形显示
awaiting - select (2) - 休眠等待文件描述符事件
backgrounds - bggen (1) - 为 X11 生成彩色背景
bad - badblocks (8) - 在磁盘分区上搜索坏块
badblocks - badblocks (8) - 在磁盘分区上搜索坏块
bandwidth - lbxproxy (1) - X11 的低网络带宽代理服务器
banner - banner (6) - 以大横幅形式打印文本
basename - basename (1) - 从文件路径名中去掉目录前缀
bash - :, ., alias, bg, bind, break, builtin, bye, case, cd, command, continue, declare, dirs, echo, enable, eval, exec, exit, export, fc, fg, for, getopts, hash, help, history, if, jobs, kill, let, local, logout, popd, pushd, pwd, read, readonly, return, set, shift, source, suspend, test, times, trap, type, typeset, ulimit, umask, unalias, unset, until, wait, while (1) - bash 内置命令
bash - bash (1) - GNU Bourne-Again SHell
batch - at, batch, atq, atrm (1) - 操作稍后执行的批处理作业
batch - atrun (8) - 运行排队稍后执行的批处理作业
batch - fastmail (1) - 快速批处理邮件接口
bcmp - bcmp (3) - 字节数组操作
bcopy - bcopy (3) - 字节数组操作
BDF - fstobdf (1) - 从 X11 字体创建 BDF 文件
bdflush - bdflush (2) - 控制磁盘缓冲区守护进程
bdflush - bdflush (8) - 将缓冲区刷新回磁盘的守护进程
bdf topcf - bdf topcf (1) - X11 字体转换程序
before light - before light (1) - X11 屏幕保护程序
behaviour - reboot (2) - 重启 Linux 或修改 Ctrl-Alt-Del 行为
behaviour - siginterrupt (3) - 更改系统调用的信号行为
Bessel - j0, j1, jn, y0, y1, yn (3) - Bessel 数学函数
bg - bg (1) - bash 内置命令
