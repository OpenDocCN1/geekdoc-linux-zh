

## 第5章 (CH05)

- ssg_scripts/ch05/chkauth.pl
- ssg_scripts/ch05/loadtest.pl
- ssg_scripts/ch05/newsysdoc.txt

## 第6章 (CH06)

- ssg_scripts/ch06/conv_tab.bc
- ssg_scripts/ch06/DocBook
- ssg_scripts/ch06/DocBook/getcommands.xslt
- ssg_scripts/ch06/DocBook/Makefile
- ssg_scripts/ch06/DocBook/maketest.sh
- ssg_scripts/ch06/DocBook/testarticle.xml
- ssg_scripts/ch06/DocBook/testbook.xml
- ssg_scripts/ch06/RSS
- ssg_scripts/ch06/RSS/articles
- ssg_scripts/ch06/RSS/articles/backchange.rss
- ssg_scripts/ch06/RSS/articles/cpustats.rss
- ssg_scripts/ch06/RSS/articles/newcpucluster.rss
- ssg_scripts/ch06/RSS/articles/newraid.rss
- ssg_scripts/ch06/RSS/articles/rssmand1.rss
- ssg_scripts/ch06/RSS/demo.rss
- ssg_scripts/ch06/RSS/genrss1.sh

## 第7章 (CH07)

- ssg_scripts/ch07/dirlister1.sh

请注意，由于脚本结构的设置方式，光盘上存在一些空文件夹。这是故意的。

# 索引

# (脚本注释) 符号，32
# ! (shebang) 在可执行文件中，26–27
$ (变量) 符号，36
/ 快捷方式和可执行文件，27
[ ] (正则表达式) 符号，15
| (命令输出) 符号，13
\ (续行) 符号
用于命令文件，83
用于脚本，40
. (点) 和文件名，10

A
访问控制列表 (ACLs)，96
未使用的账户，226–228
添加用户，96
管理员，参见系统管理员
aide 命令，206–210
AIT 磁带系统，112
AIX
init 状态，157–160
instfix 命令，170
开源软件，274
smit 程序，96
警报消息，141
读取警报结果，241–244
ARPnet，227
at 命令
Solaris 作业票据的内容，51–52
执行，51
待处理作业队列，50
从队列中移除待处理作业，50–51
atq 命令，50
atrm 命令，50–51
auth syslog 设施，140
自动化
at 命令，49–53
cron 机制，53–55
概述，49

awk 命令，34, 35

B
反引号字符 (`) 和命令，3
备份
到另一系统，119–120
启动磁盘克隆，120–121
检查完整性，124
复制重要命令，132–133
每日，108–109
专用服务器，122–123
重要文件，113–117
索引文件，117
媒体，111–112, 132–133, 205, 210
每月，110
异地，110
可读性，109
冗余备份硬件，117–118
保留期，109
策略，108
使用 rcs，118
每周，109
执行窗口，110–111

基线
每日基线检查，101–102
采样数据，58
目录结构，59–60
在浏览器中绘图，87–89
通过 gnuplot 绘图，79–87
入侵检测系统 (IDS)，238
保留数据的时间长度，59
管理日志文件，89–91
网络重传，68–74
原因，58
另见 监控

bash shell
bc 计算器，187
提示符，自定义，3–4
bc 计算器，186–188
bin 目录，2–3, 130, 132, 138

启动磁盘克隆，120–121
启动过程
root 的 $HOME 可访问性，10
特洛伊木马的存活，199
启动系统
init 状态，10, 157–160
概述，157
广播时间，135–136
浏览器中显示图表，87–89。另见 HTML
BSD 系统
cron 机制，54
负载测试，156
ps 命令，13
sudo 命令，11
新系统老化，154–157
C
cal 程序，268
日历
cal 程序，268
gcal 程序，268–270
cat 命令，258
catman -w 选项，4
cd 命令，10
CD-ROM (附带)
按章节的文件，277–279
系统要求，277
CDs/DVDs
用于备份，111–112, 132–133, 205, 210
从中执行程序，27
Cheswick, Bill，223
chrootkit，213–217
chmod 命令，10, 33, 152–154, 205
chop 函数，45
ci (check in) 命令，30
时钟和 ntp 设置，133–137
克隆启动磁盘，120–121
命令文件
使用 Perl 生成，83–85
通过 gnuplot 绘图，80–81
命令输出 (|) 符号，13
命令行开关和 Getopt Perl 模块，47–49
命令，在脚本中，34–35。另见具体命令
逗号分隔值 (CSV)，47
注释 (#) 在脚本中，32
compress 命令，144
会议安排，269–270
配置文件
在 /etc 中，22
IDS 模式下 snort 的配置，240–241
续行 (\ ) 符号
用于命令文件，83
用于脚本，40
转换，十进制/二进制，186–188
复制重要命令，132–133
计数器，参见 基线
cp 命令，97
cpio 命令，97
CPU 监控
通过 sar 命令，17–19, 63–66, 171
通过 top 命令，15–17
crit 消息，141, 143
cron 机制
CPU 监控，63–64
cron.allow 文件，53
cron.deny 文件，53
crontab，53–55
DST (夏令时)，54–55
网络监控，66–68
概述，53
模板，crontab，54
cron syslog 设施，140
CSV (逗号分隔值)，47
客户关系，104
D
daemon syslog 设施，140
每日备份，108–109
日常任务，99–104
date 命令，8–9
日期
日历，268–270
使用日期保存日志文件，90–91
通过 at 命令安排执行，49–53
debug 消息，141
十进制/二进制转换，186–188
国防高级研究计划局 (DARPA)，242
删除
核心文件，255–256
防止通过粘滞位删除文件，152–154
从队列中删除计划作业，50–51
拒绝服务 (DOS) 攻击，77
$DESTDIR 变量，116
开发

