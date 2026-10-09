

## 第 8 课 实验 1

### 探索内核服务和配置

![](img/477ccb2f05b6ba1b2d563ea74f18c197_935_0.png)

你可以在学生数据文件中的 Managing_Kernel_Services\Solution 文件夹内的 Lesson 8 Lab 1 solution.html 文件中找到该活动的建议解决方案。

**开始前：**
将 grub.conf 文件复制为 grub.conf.bak，以备份 grub.conf 文件。

**场景：**
系统管理员负责监控内核的性能，以确保系统平稳运行。因此，你决定熟悉各种内核服务及其配置方法。

- 1. 创建一个新的 initrd 镜像。
- 2. 使用新的 initrd 镜像更新 GRUB 配置。
- 3. 查看新的 initrd 镜像并使用它启动系统。
- 4. 查看连接到系统的所有外围设备。
- 5. 使用 HAL 设备管理器查看连接到系统的所有硬件设备。
- 6. 监控系统当前正在运行的进程。

## 第 9 课 实验 1

### 使用基本 Bash Shell 操作管理文件

你可以在学生数据文件中的 Working_with_Bash_and_Shell_scripts\Solution 文件夹内的 Lesson 9 Lab 1 solution.html 文件中找到该活动的建议解决方案。

**数据文件：**
Software_List.txt, Software_Rules.txt, Software_Audit_Report_08.txt, Software_Audit_Report_09.txt

**开始前：**
确保所需的数据文件已复制到 /root 目录中。

**场景：**
你想查找几个月前创建的文件。你记得这些文件的文件名以“Software”开头。你需要找到这些文件，并在 /mybackup 目录中创建它们的备份。

- 1. 查找文件名以“Software”开头的文件。
- 2. 在 /mybackup 目录中创建这些文件的备份。

## 第 9 课 实验 2

### 使用变量配置 Shell 环境

![](img/477ccb2f05b6ba1b2d563ea74f18c197_937_0.png)

你可以在学生数据文件中的 Working_with_Bash_and_Shell_scripts\Solution 文件夹内的 Lesson 9 Lab 2 solution.html 文件中找到该活动的建议解决方案。

**场景：**
你的同事要求你按照以下要求配置他的 Linux 系统。

- 编写一个脚本，提醒他每天填写工作量跟踪表。
- 将 *root* 目录分配给系统中的本地路径。
- 命令提示符应反映公司名称“Our Global Company”。
- 自定义历史文件大小，使得运行 *history* 命令时仅显示 500 条记录。

- 1. 编写一个名为 Reminder 的脚本，以便在用户每次登录时提醒其填写工作量跟踪表。
- 2. 保存该文件并将其转换为可执行脚本。
- 3. 测试该脚本。
- 4. 自定义 *~/bashrc* 脚本文件中的环境变量，以满足你同事的需求。
- 5. 检查更改。

## 第 9 课 实验 3

### 应用基本脚本技术

![](img/477ccb2f05b6ba1b2d563ea74f18c197_938_0.png)

你可以在学生数据文件中的 Working_with_Bash_and_Shell_scripts\Solution 文件夹内的 **Lesson 9 Lab 3 solution.html** 文件中找到该活动的建议解决方案。

**场景：**
你希望跟踪每日任务，以便轻松填写每周工时卡。你决定在一个具有唯一文件名的文本文件中维护一份列表，记录已完成的工作（daily work-done）。你决定使用当前日期作为每个文件的文件名，并将日期添加为每个文件的第一行。你想编写一个名为 dailyupdate 的脚本来自动化此过程。

- 1. 使用 Vim 创建一个名为 dailyupdate 的脚本文件。
- 2. 编写代码，通过重定向用户的日期输入来创建文本文件。
- 3. 编写代码以确认使用唯一文件名创建文件。
- 4. 测试该脚本。

## 第 10 课 实验 1

### 执行进程管理

![](img/477ccb2f05b6ba1b2d563ea74f18c197_939_0.png)

你可以在学生数据文件中的 Managing_Jobs_and_Processes\Solution 文件夹内的 Lesson 10 Lab 1 solution.html 文件中找到该活动的建议解决方案。

**场景：**
作为系统管理员，你需要监控系统中正在运行的进程及其对系统资源的使用情况。你需要每天执行以下任务。

- 列出所有后台作业。
- 挂起或终止不必要的进程。

- 1. 将三个命令作为后台进程执行。
- 2. 终止最后一个作业。
- 3. 将第二个作业置于前台并挂起。
- 4. 输入 *jobs* 以查看在后台运行的进程列表。
- 5. 查看当前正在运行的进程以及所有其他正在运行的进程。

## 第 10 课 实验 2

### Linux 中的多任务处理

![](img/477ccb2f05b6ba1b2d563ea74f18c197_940_0.png)

你可以在学生数据文件中的 Managing\_Jobs\_and\_Processes\Solution 文件夹内的 Lesson 10 Lab 2 solution.html 文件中找到该活动的建议解决方案。

**场景：**
你收到了多起投诉，称进程完成所需的时间比平时更长。有一些以高优先级运行的命令，可以降低其优先级。请练习调整命令优先级，并延迟作业在不同时间运行。这应该能释放一些处理能力，以便关键进程得以运行。

- 1. 查看系统中的进程。
- 2. 发出将安装文件作为后台进程复制的命令。
- 3. 使用 top 命令调整复制进程的 nice 值。
- 4. 发出在后台运行的命令并注销系统。
- 5. 以 root 身份登录并验证作业已完成。

## 第 11 课 实验 1

### 配置系统服务

![](img/477ccb2f05b6ba1b2d563ea74f18c197_941_0.png)

你可以在学生数据文件中的 Configuring_System_Services\Solution 文件夹内的 Lesson 11 Lab 2 solution.html 文件中找到该活动的建议解决方案。

**场景：**
你是 OGC 系统中的系统管理员。你的组织有许多分支机构，并且已在服务器上启用了系统和网络服务，以允许不同分支的员工进行通信和共享信息。你需要监控服务器上发生的所有活动。

- 1. 在 srvA 上启用 SELinux。
- 2. 配置 syslogd，将系统设置为中央网络日志服务器。
- 3. 配置日志上的警报和警告。

## 第 12 课 实验 1

### 实现 DNS 服务

**开始前：**

- 1. 在标记为 srvB 的系统上，使用 vi 编辑器打开 /etc/sysconfig/selinux 文件。
- 2. 将 SELINUX=permissive 更改为 SELINUX=disabled。
- 3. 切换到命令模式。保存并关闭文件。
- 4. 重启系统。切换到 CLI。以 root 身份登录。
- 5. 输入 iptables -F 以刷新 IP 表。输入 iptables -F -t nat 以刷新 NAT IP 表。输入 service iptables save 以保存 IP 表的设置。
- 6. 重启系统。切换到 CLI。以 root 身份登录。
- 7. 输入 yum localinstall /rhelsource/Server/bind* 以安装 BIND 软件包。输入 y 以继续安装。清除屏幕。

**场景：**
你的组织开设了一个新分支。市场部使用一台服务器 srvB 和 50 台系统来管理其职能。为了便于通信和高效管理，你希望将所有系统置于同一个域名 ourglobalcompany.com 之下。

正向区域和反向区域的参数如表所示：

| | 正向区域 | 反向区域 |
| :--- | :--- | :--- |
| TTL 值 | 86400 秒 | 86400 秒 |
| 序列号 | 1001 | 1001 |
| 刷新周期长度 | 28800 秒 | 28800 秒 |
| 重试周期长度 | 7200 秒 | 7200 秒 |
| 从服务器响应查询的持续时间 | 3600000 秒 | 604800 秒 |
| 负缓存服务器的默认 TTL 值 | 86400 秒 | 86400 秒 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_942_0.png)

你可以在学生数据文件中的 Configuring_Network/Solution 文件夹内的 Lesson 12 Lab 1 solution.html 文件中找到该活动的建议解决方案。

- 1. 在 srvB 上为 ourglobalcompany.com 域名配置 DNS 服务器。

