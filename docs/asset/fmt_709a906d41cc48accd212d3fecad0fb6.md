
- 5. 使用 `mount -a` 执行挂载。
- 6. 输入 `ls /share` 以查看挂载情况。
- 7. 输入 `touch /share/lara/testfile`。
- 8. 输入 `ls /share/lara` 验证文件已创建。
- 9. 使用 `umount -l /share` 卸载挂载。
- 10. 再次执行 `mount -a` 并使用 `ls /share` 验证挂载。

7. 用户连接到该服务器后，需要执行什么操作才能访问配置为多用户共享的共享？

8. 如何将 Samba 共享挂载为多用户共享，并定义用户 `lisa` 定义为最小用户账户？

9. 如何防止用户在 `/etc/fstab` 文件中看到 Samba 挂载凭据？

10. 哪条命令允许你列出特定服务器上所有用的 Samba 共享？

## 章节末实验

配置 Samba 是你作为 RHCE 应该具备的技能的重要部分。因此，本章的章节末实验相对复杂。

### 实验 37.1

+ 1. 在 `server1` 上创建两个 Samba 共享。为这些共享配置组访问权限。为此，请使用你在第 6 章“用户和组管理”中创建的用户和组。如果你没有这些用户和组，可以创建组并分配一些随机用户作为成员：

+ - `sales` 共享（销售）应该对 `sales` 组的所有成员具有写权限，并对 `account` 组的成员具有只读权限。其他用户不应有权访问此共享。

+ - `account` 共享（账户）应该对 `account` 组的所有成员具有写权限，并对 `account` 组的成员具有只读权限。其他用户不应有权访问此共享。

+ 2. 配置防火墙和 SELinux 以允许对 Samba 共享完全访问。

+ 3. 在 `server2` 上，为这两个共享都配置多用户共享。创建一个对两个共享具有最小权限的 Samba 用户账户。配置 `/etc/fstab` 以自动挂载这些共享。

+ 4. 通过以每个组成员的身份访问共享，测试多用户挂载的工作情况。验证对共享的读、写权限。

![](img/5a30005f195700270765e15ffa2b199b_880_0.png)

本章涵盖了以下主题：

* 了解电子邮件基础
* 配置 Postfix 参数
* 验证工作正常的邮件配置

本章涵盖了以下 RHCE 考试目标：

* 配置系统将所有邮件转发到中央邮件服务器

# 第 38 章

# 设置 SMTP 服务器

邮件处理是许多 Linux 服务器上需要执行的一项基本任务，无论它们提供什么具体服务。在许多情况下，这些服务通常需要发送邮件。这就是为什么 RHCE 需要能够配置服务器将邮件转发到中央邮件服务器的原因。在本章中，你将学习如何实现这一点。

## “我已经掌握了吗？”测试题

“我已经掌握了吗？”测试题可以让你评估自己是应该仔细读完整个章节，还是跳到“考试准备任务”部分。如果你对这些问题的答案或对你自己对这些主题知识的评估有疑虑，请阅读整个章节。表 38.1 列出了本章的主要标题及其对应的“我已经掌握了吗？”测试题。你可以在附录 A，“‘我已经掌握了吗？’测试题答案和复习题”中找到答案。

| 基础主题章节 | 题目 |
| --- | --- |
| 了解电子邮件基础 | 3, 5 |
| 配置 Postfix 参数 | 1, 2, 4, 8 |
| 验证工作正常的邮件配置 | 6, 7, 9, 10 |

+ 1. 下面哪一个参数允许你指定 Postfix 邮件服务器应该在哪个网卡上监听入站连接？
    a. `inet_interfaces`
    b. `myorigin`
    c. `relayhost`
    d. `mynetworks`

+ 2. 下面哪一个 Postfix 参数允许你指定邮件应该转发到哪里？
    a. `inet_protocols`
    b. `relayhost`
    c. `myydestination`
    d. `mymynetworks`

3. 下面哪一个邮件处理角色描述了配置中负责与收方邮件服务器通信的部分？
    a. MUA
    b. MSA
    c. MTA
    d. MDA

4. 最重要的 Postfix 配置文件的名称是哪个？
    a. `/etc/postfix/postfix.conf`
    b. `/etc/postfix/master.cf`
    c. `/etc/postfix/conf`
    d. `/etc/postfix/main.cf`

5. 下面哪一个不是 Postfix 进程？
    a. `qmgr`
    b. `pickup`
    c. `postfix`
    d. `sendmail`

6. 在修复了导致邮件服务器无法到达目标邮件服务器的问题后，你注意到消息没有再次立即发送。你可以使用哪条命令标记邮件队列中的所有消息，以便它们立即投递？
    a. `postmaster`
    b. `postqueue -p`
    c. `postqueue -f`
    d. `sendmail`

+ 7. 哪一个日志文件包含关于邮件投递成功和失败的详细信息？
    a. `/var/log/postfix/maillog`
    b. `/var/log/maillog`
    c. `/var/log/mail`
    d. `/var/log/messages`

+ 8. 哪条命令允许你修改 Postfix 参数？
    a. `postfix -e`
    b. `postconf -e`
    c. `postman -e`
    d. `postqueue`

+ 9. 在发送消息时，你发现消息没有被接受。你应该更改下面哪一个参数？
    a. `inet_interfaces`
    b. `myorigin`
    c. `relayhost`
    d. `mynetworks`

+ 10. 如果目标邮件服务器配置为接收，下面哪一个项反映了这一点？
    a. `inet_interfaces`
    b. `myorigin`
    c. `relayhost`
    d. `mynetworks`

3. 本地 Postfix 进程被配置为空客户端（null client），并将消息转发到 `smtp.example.com`，后者作为中继主机。

4. `smtp.example.com` 执行 DNS 记录查找，发现 `server2 example.org` 配置为处理 `example.org` 的入站邮件。

5. 消息被转发到 `server2.example.org`。

6. `server2.example.org` 将消息投递到用户的本地邮箱，路径位于 `/var/spool/mail/$USER`。

7. 用户使用 MUA（邮件代理客户端），该客户端配置为使用 IMAP 从本地邮箱中获取消息。

![](img/5a30005f195700270765e15ffa2b199b_886_0.png)

**图 38.1** RHEL 7 邮件服务器解决方案

# RHEL 7 邮件服务器解决方案

在 Linux 上，有多种邮件服务器解决方案。过去，Sendmail 邮件服务是最常见的 Linux 邮件服务器。然而，它非常复杂，使用的语法也很难以理解。尽管它很复杂，Sendmail 仍成为 Linux 邮件处理的标准。Postfix 的开发是为了兼容 Sendmail 且更易配置。

在 RHEL 7 中，Postfix 被用作邮件服务。Postfix 由多个处理特定任务的进程组成。这些进程由 Postfix master 服务引导，该服务通过读取 `/etc/postfix/master.cf` 配置文件来确定使用哪些服务处理特定任务。这种方法使得 Postfix 具有模块化和可插性；如果需要，很容易用另一个特定服务替换它。表 38.2 列出了一些 Postfix 进程的示例，列表 38.1 显示了 `/etc/postfix/master.cf` 配置文件的部分内容。

# 表 38.2 Postfix 服务器进程概览

| 进程 | 目的 | 关键主题 |
|---|---|---|
| `master` | 控制所有 Postfix 进程的进程。 | |
| `smtp` | 负责 Postfix 节点之间的 SMTP 通信。 | |
| `pickup` | 在消息放入消息队列后捡取消息。 | |
| `cleanup` | 在消息投递后清理消息队列。 | |
| `rewrite` | 如果使用 postfix map 重写消息头部的部分，则由 rewrite 进程处理。 | |
| `sendmail` | 用于发送消息的标准程序，并由 Postfix 实现。 | |
| `qmgr` | 管理消息队列内容的通用进程。 | |

> 提示：你不需要背诵所有 Postfix 进程的名字。但是，如果你在阅读日志以理解为什么无法发送消息时，能够识别出这些 Postfix 进程，那是很有用的。

列表 38.1 `/etc/postfix/master.cf` 配置文件的部分列出

```
[root@server1 postfix]# head -n 20 master.cf

#

# Postfix master 进程配置文件。
```
