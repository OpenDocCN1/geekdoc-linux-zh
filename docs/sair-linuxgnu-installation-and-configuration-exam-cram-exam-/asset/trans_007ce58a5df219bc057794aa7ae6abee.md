
## Question 27
以下关于 GNU GPL 软件的哪些陈述是不正确的？

- a. 你可以将其出售以获取利润。
- b. 你可以在未经许可的情况下将其与其他专有软件集成。
- c. 你可以修改源代码以满足你的需求。
- d. 你可以访问其文档。

## Question 28
Sarah 是你一起工作的管理员之一，她在自己的 Linux 计算机上忘记了 root 密码。由于她对 Linux 尚不熟悉，她向你寻求帮助。以下哪条建议最合理？

- a. 启动 Linux，并使用 init 命令切换到单用户模式。然后你可以更改 root 密码。
- b. 从启动软盘启动 Linux，并使用 linux single 命令启动单用户模式。然后你可以更改 root 密码。
- c. 从网络连接访问 Sarah 的 Linux 计算机并切换到单用户模式。然后你可以更改 root 密码。
- d. 从调制解调器连接访问 Sarah 的 Linux 计算机并切换到单用户模式。然后你可以更改 root 密码。

## Question 29
当你按下 x 键时，你发现键盘重复率太慢，无法满足你的需求。目前大约是每秒五个字符。以下哪个命令可以将此速率提高到每秒 30 个字符？

- a. /sbin/kbdrate -c 30
- b. /sbin/kbd -r 30
- c. /sbin/kbdrate -r 30
- d. /sbin/krate -c 30

## Question 30
以下哪项陈述最能描述多用户多终端多任务？

- a. 一个用户在多个终端上多次登录以同时运行多个程序。
- b. 多个用户各登录一次，每个用户在自己的终端上，并各自并发运行多个程序。
- c. 一个用户一次登录，并在多个终端上同时运行多个程序。
- d. 多个用户同时登录。每个用户可以轮流运行他的程序。

## Question 31
你的 IP 地址格式为 a.b.c.d。这些字母各自代表什么？

- a. 4 位
- b. 小于 192 的数字
- c. 一个八位字节
- d. 一个点分四组

## Question 32
以下哪个目录包含打印机 spool 的处理文件？

- a. /var/
- b. /var/spool
- c. /var/spool/lpd
- d. /var/spool/lp

## Question 33
以下哪个是配置 X Window 的标准 GNU GUI 工具？

- a. Xconfigurator
- b. xf86config
- c. XF86Setup
- d. xdm
- e. 没有标准 GNU GUI 工具，因为它们不如相应的命令行工具可靠。

## Question 34
你已将第二个虚拟终端专用于数字数据输入。你希望在进入此终端时 Num Lock 键始终处于激活状态。以下哪个命令可以实现此功能？

- a. setleds num < /dev/tty2
- b. setleds num < /dev/tty2 > /dev/null
- c. setleds +num < /dev/ttyx
- d. setleds +num < /dev/tty2 > /dev/null

## Question 35
GPL 软件不提供任何保修。以下哪些方法可以弥补缺乏保修的不足？

- a. 与 Linux 顾问或公司签订服务合同。
- b. 聘请能够修改 Linux 源代码以满足你需求的人员。
- c. 在 Linux 文档和新闻组的帮助下自行维护软件。
- d. 根据需要下载驱动程序以跟上你的硬件。
- e. 以上所有。

## Question 36
你想在 /etc/passwd 配置文件中查找所有包含星号 (*) 的行。你知道 grep * /etc/passwd 命令会使用当前目录中的文件名（而不是星号）来搜索 /etc/passwd 文件。哪个命令可以搜索 /etc/passwd 文件中的星号？[全部选择正确选项]

- a. grep "*" /etc/passwd
- b. grep "\*" /etc/passwd
- c. grep "\*\*" /etc/passwd
- d. grep "\*" /etc/passwd

## Question 37
由于某种原因，你在命令行界面中看到屏幕上出现一堆乱码字符。以下哪个命令可以用来解决这个问题？

- a. rewrite
- b. reset
- c. bash
- d. xdm

## Question 38
以下关于环境变量的哪些陈述是正确的？

- a. 它们在 shell 之间适用。
- b. 它们的值仅适用于你的默认 shell。
- c. 你可以使用 environ 命令找到当前环境变量设置。
- d. 环境变量从 shell 到 shell 发生变化。

## Question 39
你拥有一家软件公司，想进入销售 GPL 软件的业务。你意识到你必须免费提供软件（和源代码）作为下载。你必须怎么做才能从 GPL 软件中赚钱？

- a. 重新定位你的业务并宣传你在销售的 GPL 软件方面的专业知识。
- b. 尽可能让用户轻松下载你的软件，并为此特权收取费用。
- c. 出售权利给他人，让他们转售和再销售你的软件。
- d. 免费分发软件，但向用户收取源代码副本的费用。

## Question 40
以下哪个是 Linux Loader（LILO）的限制？

- a. 你不能使用它来确保 Linux 识别你的所有 RAM。
- b. 你不能使用它在任何硬盘上启动超过四个操作系统。
- c. 你不能使用它来启动多个版本的 Linux。
- d. 你只能在 Linux 位于硬盘的第一个主分区时使用它。
- e. 以上都不是。

## Question 41
以下哪项陈述最能描述 ln 和 cp 命令之间的区别？假设适用的文件位于同一卷上。

- a. 使用 cp 命令创建的任何文件都与原始文件具有相同的 inode 号。ln 命令不具备此特性。
- b. 使用 cp 和 ln 命令创建的文件都与原始文件具有相同的 inode 号。
- c. 使用 ln 命令创建的任何文件都与原始文件具有相同的 inode 号。cp 命令不具备此特性。
- d. 使用 cp 和 ln 命令创建的文件都与原始文件具有不同的 inode 号。

## Question 42
以下哪项陈述最能描述 find 和 locate 命令之间的区别？

- a. find 命令比 locate 快，但由于它基于文件名数据库，因此不太及时。
- b. 尽管 find 命令在系统文件上工作更好，但 locate 命令在用户主目录中的个人文件上工作更好。
- c. 没有区别：find 和 locate 命令本质上是相同的命令。
- d. find 命令比 locate 慢，但它更准确，因为它搜索所有当前文件。

## Question 43
以下哪个运行级别专用于重新启动计算机？

- a. 0
- b. 1
- c. 6
- d. 取决于你的发行版。

## Question 44
你已通过修改 /etc/passwd 配置文件为新用户创建了一个账户。在账户准备好供新用户使用之前，你需要采取以下哪些操作？用户名是 gsmith。[全部选择正确选项]

- a. 使用 chown 命令将所有权转让给新用户。
- b. 使用 su - gsmith 命令进入新账户。从 /etc/skel 目录复制所有文件。
- c. 使用 passwd gsmith 命令分配新密码。
- d. 运行 adduser 命令以记录更改。

## Question 45
你有一个名为 runaway 的程序似乎无法停止。你已登录到另一个虚拟控制台。你需要做什么来停止 runaway 程序？

- a. 运行 grep runaway < ps auxl 命令，找到与 runaway 程序关联的 TTY，然后在与该程序关联的 TTY 号上运行 kill 命令。
- b. 运行 ps auxl > grep runaway 命令，找到与 runaway 程序关联的 PID，然后在与该程序关联的 PID 号上运行 kill 命令。
- c. 运行 ps auxl | grep runaway 命令，找到与 runaway 程序关联的 TTY，然后在与该程序关联的 TTY 号上运行 kill 命令。
- d. 运行 ps auxl | grep runaway 命令，找到与 runaway 程序关联的 PID，然后在与该程序关联的 PID 号上运行 kill 命令。

## Question 46
你正在查看朋友的 /etc/printcap 打印机配置文件。使用以下摘录，你会在哪里找到打印机？

```
lp|LaserJet:lp=/dev/lp0:sd=/var/spool/lpd/lp\
:rm=rpp:rp=raw:af=/var/log/lp-acct\
:lf=/var/log/lp-errs:pl#66:pw#80:pc#150:mx#0\
:sh
```

- a. 在本地计算机上
- b. 在名为 raw 的计算机上
- c. 在名为 rpp 的计算机上
- d. 在名为 sh 的计算机上
