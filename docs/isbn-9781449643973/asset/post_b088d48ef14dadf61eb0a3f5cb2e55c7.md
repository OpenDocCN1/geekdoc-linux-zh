
### 配置Apache Web Server基本安全加固

```bash
[student@TargetFedora01 ~]$ sudo chkconfig --level 3 httpd on
[sudo] password for student:
```

Figure 33 – Configure Basic Security Hardening on an Apache Web Server

- 23. 输入命令：`sudo service httpd start`，按 `<enter>` 启动Web服务器。（如提示输入密码：ISS316Security）
- 24. 默认情况下，HTTP “Trace” 方法是启用的。该方法有潜在风险，可能会泄露关于服务器的不必要信息。请禁用 Trace 方法。
- 25. 输入命令：`su -c 'vi /etc/httpd/conf/httpd.conf'`，按 `<enter>`。
- 26. 密码：ISS316Security
- 27. 按 “i” 键进入 INSERT 模式。
- 28. 向下滚动至新行开始处。
- 29. 添加以下行：`# Disable some HTTP Methods we don't like`
- 30. 再添加一行：`TraceEnable off`

```text
#
# Disable some HTTP Methods we don't like
TraceEnable off
```

Figure 34 – Disable Some HTTP Connectivity Methods Using “httpd.conf” Trace Enable Off

- 31. 输入命令：`sudo service httpd configtest`，按 `<enter>` 以测试语法错误。如提示输入密码，请输入 student 用户账户的密码（ISS316Security）。寻找短语：Syntax OK。
- 32. 重新加载Web服务器配置文件。输入命令：`sudo service httpd reload`，按 `<enter>`。如提示输入密码，请输入 student 用户账户的密码（ISS316Security）。
- 33. 安装 telnet。输入命令：`sudo yum install telnet -y`，按 `<enter>`。如提示，请输入 student 账户的密码（ISS316Security）。
- 34. Telnet 到Web服务器端口 80。输入命令：`telnet localhost 80`，按 `<enter>`。
- 35. 向Web服务器发出命令。输入命令：`TRACE/HTTP/1.0`，按 `<enter>`。将呈现原始 HTML 输出。验证 HTML 中是否包含 "Method not implemented" 文本。

### 安装并配置 Sendmail 应用仅允许从本地主机中继

- 36. 安装 Sendmail 服务器。输入命令：`sudo yum install sendmail -y`，按 `<enter>`。如提示输入密码，请输入 student 用户的密码（ISS316Security）。
- 37. 配置 Sendmail 在运行级别 3 下启动。输入命令：`sudo chkconfig sendmail --level 3`，按 `<enter>`。如提示输入密码，请输入 student 用户的密码（ISS316Security）。
- 38. 验证 sendmail 是否仅通过本地主机（127.0.0.1）限制邮件中继。
- 39. 验证该行内容是否为：`DAEMON_OPTIONS(Port=smtp,Addr=127.0.0.1,NAME=mta) dnl`

输入命令：`grep DAEMON /etc/mail/sendmail.me`，按 `<enter>`。

### 配置 Secure Shell (SSH) 远程访问及当日 Banner 消息

- 40. 在 vi 编辑器中打开 sshd_config 文件。输入命令：`su -c 'vi /etc/ssh/sshd_config'`，按 `<enter>`。
- 41. 密码：ISS316Security
- 42. 按 “i” 键进入 **INSERT** 模式。
- 43. 通过将字段更改为以下适当设置来禁用密码登录：
- 44. 移除 `#PasswordAuthentication no` 行中的 `#`
- 45. 添加新行：`UsePam no`
- 46. 禁用 root 登录能力。将 `#PermitRootLogin yes` 替换为：`PermitRootLogin no`
- 47. 向所有尝试登录的人显示警告横幅：将 `#Banner none` 替换为：`Banner /etc/motd`

```text
# no default banner path
Banner /etc/motd
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_60_0.png)

- 48. 保存更改并退出文件。按 Esc 键退出插入模式，然后按 “shift &” 键进入命令模式。在命令模式的冒号提示符处，输入 `wq` 以退出并保存更改。
- 49. 在 vi 编辑器中打开 `/etc/motd`。输入命令：`su -c 'vi /etc/motd'`，按 `<enter>`。
- 50. 密码：ISS316Security
- 51. 按 “i” 键进入 **INSERT** 模式。
- 52. 向文件中添加以下行。

PROPERTY OF FIRST WORLD BANK SAVINGS AND LOAN. AUTHORIZED USERS ONLY!

- 53. 保存更改并退出文件。按 Esc 键退出插入模式，然后按 “shift” & “:” 键进入命令模式。在命令模式的冒号提示符处，输入 `wq` 以退出并保存更改。
- 54. 检查 openssh 服务器状态。输入命令：`service sshd status`，按 `<enter>`。
- 55. 如果处于运行状态，则重新加载 openssh 配置文件。输入命令：`sudo service sshd reload`，按 `<enter>`。如提示，请输入 student 用户的密码（ISS316Security）。

![](img/73be0eef2ceb12f43f3eb92c420134f5_61_0.png)

Figure 36 – Status check of the openssh server

- 56. 如果未处于运行状态，则启动 openssh 服务器。输入命令：`sudo service sshd start`，按 `<enter>`。如提示，请输入 student 用户的密码（ISS316Security）。
- 57. 确保对本地主机的安全访问。输入命令：`ssh localhost`，按 `<enter>`。如果出现消息提示：the authenticity host localhost(127.0.0.1) can't be established. Are you sure you want to continue connecting (yes/no)? _ ，请输入 'yes' 以继续。

![](img/73be0eef2ceb12f43f3eb92c420134f5_61_1.png)

Figure 37 – Verifying Banner message for SSH login

## 交付物

完成实验 #5：对 Linux 服务应用加固安全后，学生需要提供以下交付物：

- 1. 实验 #5 - 以下文件的截图：
    - a. /etc/my.cnf 文件的输出
    - b. /etc/httpd/conf/httpd.conf 文件的输出
    - c. /etc/ssh/sshd_config 文件的输出
    - d. SSH 会话 MOTD 横幅
- 2. 实验 #5 – 评估问题与答案

## 评估标准与评分细则

以下是学生必须执行的实验 #5 的评估标准和评分细则：

- 1. 学生是否能够在启用和安装 Linux 服务器服务时对其进行加固，并在配置过程中保持安全视角 – [20%]
- 2. 学生是否能够创建 Apache Web Server 安装，并执行基本安全配置以确保系统在托管网站前已加固 – [20%]
- 3. 学生是否能够配置 MySQL 数据库并执行基本安全设置，理解默认安装的后果并为数据库实例推荐加固步骤 – [20%]
- 4. 学生是否能够安装、设置 Sendmail 并执行基本安全配置，以利用 Linux 系统内置的消息功能 – [20%]
- 5. 学生是否能够为 Linux 服务器系统启用并实现安全的 SSH 加密远程访问（通过网络或互联网） – [20%]

# 实验 #5 – 评估工作表

# 对 Linux 服务及应用应用加固安全

课程名称及编号： _________________________

学生姓名： _________________________

讲师姓名： _________________________

实验截止日期： _________________________

# 概述

本实验是前几项基于设备的实验的延伸，涉及物理服务器中加载的 Linux 服务和应用程序的安全加固。在本实验中，学生将配置安全并加固服务和应用程序，以确保这些服务的 C-I-A。他们将采取步骤配置并保护 Apache Web 服务器和 MySQL 数据库以及安全加固两者实施所需的组件。学生还将展示如何使用并配置 Sendmail 应用程序进行安全的本地消息传递，并启用使用 Secure Shell (SSH) 的安全加密远程访问。

# 实验评估问题与答案

- 1. 在配置服务时，通常哪个 Linux 目录包含服务器配置文件？

本实验涵盖了一些非常基本的 MySQL 数据库服务器和应用的安全加固设置。

- 2. 什么命令禁用了 MySQL 数据库的远程访问？这是安全加固的最佳实践吗？
- 3. 特定服务或应用的 Linux 运行级别（runlevel）是什么？什么命令允许你为服务或应用唯一地定义运行级别？
- 4. Apache Web 服务器是什么？查看 /etc/httpd/conf/httpd.conf 配置文件，并指出一个可以增强安全的设置。
- 5. OpenSSH 是远程访问 Linux 系统的事实标准方法。解释为什么不建议使用 telnet。
- 6. 什么是符号链接（Symbolic links）？
- 7. 为什么建议在 MySQL 中禁用符号链接？
