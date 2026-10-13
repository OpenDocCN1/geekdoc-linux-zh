
附加信息：
源上下文 `system_u:system_r:httpd:t:0`
目标上下文 `unconfined_u:object_r:default:t`
目标对象 `/custom/index.html`
源 `httpd`
源路径 `/usr/sbin/httpd`
主机 `servera.example.com`
源 RPM 包 Linux Enabled `selinux-policy-3.14.el8`
策略 True
类型 `targeted`
强制模式 Enforcing

## SELinux 详情

| 字段 | 数值 |
| :--- | :--- |
| 主机 | server.lab.example.com |
| 平台 | Linux RHEL 8.0 x86_64 |
| 警报时间 | Sat Feb 9 12:44:00 UTC 2019 |
| 计数 | |
| 首次出现 | 2019-03-25 |
| 最后出现 | 2019-03-28 |
| 本地 ID | bicc9cc8f-a953-4625-b79b-82c4f4f1ee3 |

原始审计消息 (Raw Audit Messages)
`type=AVC msg=audit(1553767170:651:1700): avc: denied { } for pid=15066 comm="httpd" path="/custom/index.html" dev="vda1" ino=4280311 context=system_u:system_r:httpd_t:s0 t=unconfined_u:object_r:default_t:s0 class=file permissive=0`

`sealert` 命令的 Audit Messages 部分包含 `/var/log/audit.log` 的信息。使用 `ausearch` 命令搜索 `/var/log/audit.log`。`-m` 选项搜索相关消息。`-type` 选项识别引起警报的进程和文件。进程是 `httpd`，文件是 `/custom/index.html`，上下文是 `system_r:httpd_t`。

`time Mar 28 13:30:39 2019 type=PROCT msg=audit(1553767170:651:1700) type=SYSCALL msg=audit(1553767170:651:1700) arch=c000003 syscall=15 success=no exit=13 auid=177bfffc0 aid=4294625 a=8000 items=0 pid=15063 pid=15065 auid=4294625 uid=48 eid=48 suid=48 egid=48 fid=48 s=/usr/sbin/httpd subj=system_r:httpd_t exe=(null) type=AVC msg=audit(1553767170:651:...`

- 7. 使用 `semanage` 和 `restore` 命令解决问题。要管理的上下文是 `httpd_sys_content_t`。

```
[root@servera]# semanage fcontext -a -t httpd_sys_content_t '/custom(/.*)'
```

```
[root@servera]# restorecon -Rv /custom
```

Relabeled `/custom` from `unconfined_u:object_r:default_t:s0` to `unconfined_u:object_r:httpd_sys_content_t:s0`

Relabeled `/custom/index.html` from `unconfined_u:object_r:default_t:s0` to `unconfined_u:object_r:httpd_sys_content_t:s0`

- 8. 再次尝试访问 `http://servera/index.html`。你应该看到消息“This is SERVERA”。

- 9. 退出 `servera`。

```
[root@servera]# exit
logout
[student@servera]# exit
logout
Connection to servera closed.
[student@workstation -]
```

## 完成

在工作站上，运行 `lab selinux-issues finish` 脚本完成此练习。

```
[student@workstation -]$ selinux-issues finish
```

引导式练习结束。

## 管理 SELINUX 安全

## 性能检查
在实验中，你将解决一个 SELinux 访问拒绝问题。系统管理员在 SELinux 处于强制模式时，难以让新的 Web 服务器向客户端交付内容。

## 学习成果
你应该能够：

- 识别系统文件中的问题。
- 调整 SELinux 配置。

## 开始之前
以 `student` 用户身份登录工作站，密码为 `student`。

在工作站上，运行 `lab selinux-review start` 命令。该命令运行一个启动脚本，确定服务器是否在网络上可访问。它还安装了 Apache 服务器，为 Apache 创建新的 DocumentRoot 并更新配置文件。

```
[student@workstation ~]$ $ lab selinux-review start
```

- 1. 以 root 用户身份登录服务器。
- 2. 在工作站上启动 Web 服务器并访问 `http://server/lab/lab.html`。你将看到错误消息：没有权限在服务器服务器上访问 `/lab.html`。
- 3. 研究并识别阻止 Apache 交付网页内容的 SELinux 问题。
- 4. 显示新的 HTTP 文档根和原始 HTTP 文档根的 SELinux 上文。解决阻止 Apache 交付网页内容的 SELinux 问题。
- 5. 验证 SELinux 问题已解决，且 Apache 能够交付网页内容。
- 6. 退出 serverb。

## 评估
在工作站上，运行 `lab selinux-review grade` 脚本以确认完成此练习。

## 完成实验

在工作站上，运行 `lab selinux-review finish` 脚本以完成实验。

```
[student@workstation -]$ lab selinux-review finish
```

本实验到此结束。

## 管理 SELINUX 安全

## 性能检查清单
在本次实验中，你将解决一个 SELinux 访问拒绝的问题。当 SELinux 处于强制模式（enforcing mode）时，系统管理员在让新的 Web 服务器向客户端交付内容时遇到了困难。

## 预期结果
你应该能够：

- 识别系统日志文件中的问题。
- 调整 SELinux 配置。

### 在开始之前
以 `student` 用户身份登录到工作站，密码为 `student`。

在工作站上，运行 `lab selinux-review start` 命令。该命令会运行一个启动脚本，用于判断 `serverb` 机器在网络上是否可用。它还安装了 `httpd` Apache 服务器，该服务器为 Apache 创建了新的 `DocumentRoot` 并更新配置文件。

```
[student@workstation ~]$ lab selinux-review start
```

- 1. 以 `root` 用户身份登录服务器。

- 1.1. 使用 `ssh` 命令以 `student` 用户身份登录服务器。系统配置为使用 SSH 密钥进行验证，因此不需要密码。

```
[student@workstation ~]$ ssh serverb
...输出已省略...
[student@serverb ~]$
```

- 1.2. 使用 `sudo -i` 命令切换到 `root` 用户。`student` 用户的密码为 `student`。

```
[student@serverb ~]$ sudo -i
[sudo] password for student: student
[root@serverb ~]#
```

- 2. 在工作站上启动 Web 服务器并访问 `http://server/lab.html`。你将看到错误信息：You do not have permission to access /lab.html on this server（你没有权限访问此服务器上的 /lab.html）。

- 3. 研究并识别阻止 Apache 提供 Web 内容的 SELinux 问题。

- 3.1. 使用 `less` 命令查看 `/var/log/messages` 的内容。使用 `/` 键搜索 `sealert`。使用 `q` 键退出 `less` 命令。

```
[root@serverb ~]# less /var/log/messages
```
