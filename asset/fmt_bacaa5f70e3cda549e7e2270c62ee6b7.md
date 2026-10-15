
************************************************************

`server.lab.example.com` : `ok=8` `changed=2` `unreachable=0` `failed=0`

`skipped=1` `rescued=0` `ignored=0`

+ 8. 使用即时命令（ad hoc command），检查防火墙服务器 `server.lab.example.com` 现在是否配置了 `smtp` 服务。

```
[student@workstation troubleshooting-host]$ ansible server.lab.example.com \
-u devops -b "firewall-cmd --list-services"
server.lab.example.com | CHANGED | rc=0 >>
cockpit dhcpv6-client samba smtp ssh
```

+ 9. 使用 `telnet` 测试 `SMTP` 服务是否在 `server.lab.example.com` 的 `TCP/25` 端口上监听。完成后断开。

```
[student@workstation troubleshooting-host]$ telnet server.lab.example.com 25
Trying 172.25.258.10...
Connected to server.lab.example.com.
Escape character is '^'.
220 server.lab.example.com SMTP Postfix
quit
221 2.0.0 Bye
Connection closed by foreign host.
```

## 结束

在工作站上，运行 `lab troubleshooting-host` 脚本以清理本次练习。

```
[student@workstation -]$ lab troubleshooting-host finish
```

引导性练习结束。

# 第 9 章 | Ansible 故障排除

## 实验

### Ansible 故障排除

#### 性能检查清单

在本实验中，你将对尝试运行提供的 `playbook` 时出现的问题进行故障排除。

#### 学习目标

你应当能够：

- 故障排除 `playbook` 问题。
- 故障排除托管主机问题。

#### 准备工作

以 `student` 用户登录工作站，密码为 `student`。运行 `lab troubleshoot-review start` 命令。

```
$student@workstation -$ lab troubleshoot-review start
```

该脚本会验证工作站上是否安装了 `Ansible`，并创建 `secure-troubleshoot-review/html/` 目录结构。它从 `http://materials.example.com/labs/troubleshoot-review/` 下载 `ansible.cfg`、`inventory-lab`、`secure-web.yml` 和 `hosts.conf` 文件到 `/home/student/troubleshoot-review/` 目录。它还将 `index.html` 文件下载到 `/home/student/troubleshoot-review/html/` 目录。

+ 1. 从 `~/troubleshoot-review` 目录检查 `secure-web.yml` `playbook` 的语法，该 `playbook` 为 `webservers` 组中的主机配置带 `TLS/SSL` 的 `Apache HTTPD`。修复报告的问题。
+ 2. 再次检查 `secure-web.yml` `playbook` 的语法。修复报告的问题。
+ 3. 第三次检查 `secure-web.yml` `playbook` 的语法。修复报告的问题。
+ 4. 第四次检查 `secure-web.yml` `playbook` 的语法。它不应显示任何语法错误。
+ 5. 运行 `secure-web.yml` `playbook`。`Ansible` 无法连接到 `server.lab.example.com`。修复此问题。
+ 6. 再次运行 `secure-web.yml` `playbook`。`Ansible` 应该在托管主机上以 `devs` 远程用户的身份身份验证。修复此问题。
+ 7. 第三次运行 `secure-web.yml` `playbook`。修复报告的问题。
+ 8. 再次运行 `secure-web.yml` `playbook`。它应该成功完成。使用即时命令验证 `httpd` 服务正在运行。

#### 评估

在工作站上，运行 `lab troubleshoot-review grade` 脚本以确认本次练习成功。

```
$student@workstation ~$ lab troubleshoot-review grade
```

#### 结束

在工作站上，运行 `lab troubleshoot-review finish` 脚本以清理本次实验。

```
$student@workstation ~$ lab troubleshoot-review finish
```

实验结束。

## Ansible 故障排除

### 性能检查清单

在本实验中，你将对尝试运行提供的 `playbook` 时出现的问题进行故障排除。

### 学习目标

你应当能够：

- 故障排除 `playbook` 问题。
- 故障排除托管主机问题。

### 准备工作

以 `student` 用户登录工作站，密码为 `student`。运行 `lab troubleshoot-review start` 命令。

```
$student@workstation ~$ lab troubleshoot-review start
```

该脚本会验证工作站上是否安装了 `Ansible`，并创建 `student/troubleshoot-review/html/` 目录。它从 `http://examples.com/labs/troubleshoot-review/` 下载 `ansible.cfg`、`inventory-lab`、`secure-web.yml` 和 `hosts.conf` 文件到 `/home/student/troubleshoot-review/` 目录。它还将 `index.html` 文件下载到 `/home/student/troubleshoot-review/html/` 目录。

+ 1. 从 `~/troubleshoot-review` 目录检查 `secure-web.yml` `playbook` 的语法。该 `playbook` 包含一个 `play`，为 `webservers` 组中的主机配置带 `TLS/SSL` 的 `Apache HTTPD`。修复报告的问题。

+ 1.1. 在工作站上，切换到 `/home/student/troubleshoot-review` 目录。

```
$student@workstation ~$ cd ~/troubleshoot-review/
```

+ 1.2. 检查 `secure-web.yml` `playbook` 的语法。该 `playbook` 为 `webservers` 组中的主机配置带 `TLS/SSL` 的 `Apache HTTPD`。修复报告的问题。

+ 1.3. 第三次纠正 `secure-web.yml` `playbook` 的语法。修复报告的问题。

+ 2. 再次检查 `secure-web.yml` `playbook` 的语法。修复报告的问题。

+ 2.1. 使用 `ansible-playbook --syntax` 检查 `secure-web.yml` 的语法。

```
$student@workstation troubleshoot-review]$ ansible-playbook --syntax
> secure-web.yml
```

+ 2.2. 纠正缩进中的任何语法问题。删除 `start` 和 `enable services` 任务开头的额外空格。

+ 3. 第三次检查 `secure-web.yml` `playbook` 的语法。修复报告的问题。

+ 3.1. 检查 `secure-web.yml` `playbook` 的语法。

+ 3.2. 纠正 `install web server packages` 任务中的 `item` 变量。为 `{{ item }}` 添加双引号。

+ 4. 第四次检查 `secure-web.yml` `playbook` 的语法。它不应该显示任何语法错误。

+ 4.1. 审视 `secure-web.yml` `playbook` 的语法。它不应该显示任何语法错误。

```
[student@workstation troubleshoot-review]$ ansible-playbook --syntax-check \
> secure-web.yml
```

```
playbook: secure-web.yml
```

# 第 9 章 | Ansible 故障排除
