
```
------------------------------------------------------
Sep 2 18:47:23 rh login(pam_unix)[11519]: authentication failure:
logname=LOGIN uid=0 eid=0 tty=tty3 ruser= host= user-bubba
Sep 2 18:47:25 rh login[11516]: FAILED LOGIN 1 FROM (null) FOR
bubba. Authentication failure
Unusual System Events
Sep 2 04:02:08 rh syslog 1.4.1: restart.
Sep 2 11:52:58 rh mc: /dev/gcmtl: No such file or directory
Sep 2 11:52:58 rh mc: /dev/gcmtl: No such file or directory
Sep 2 13:00:42 rh login(pam_unix)[2914]: session closed for user
bubba
Sep 2 16:58:44 rh login(pam_unix)[867]: session closed for user
root
Sep 2 18:44:58 rh su(pam_unix)[11519]: session opened for user
by wing_nut(uid=502)
Sep 2 18:45:02 rh mc: /dev/gcmtl: No such file or directory
Sep 2 18:45:02 rh mc: /dev/gcmtl: No such file or directory
Sep 2 18:47:23 rh login(pam_unix)[11196]: authentication failure:
logname=LOGIN uid=0 eid=0 tty=tty3 ruser= user-bubba
Sep 2 18:47:25 rh login[11516]: FAILED LOGIN 1 FROM (null) FOR
bubba. Authentication failure
Sep 2 18:47:32 rh login(pam_unix)[11196]: session opened for user
bubba by LOGIN(uid=0)
Sep 2 18:47:32 rh --[11196]: LOGIN ON tty3 BY bubba
Sep 2 18:50:46 clio login(pam_unix)[11439]: session opened for
user bubba by LOGIN(uid=0)
Sep 2 18:50:46 rh mc: /dev/gcmtl: No such file or directory
```

# 第 30 章：实施本地安全

## 第五部分：系统安全与问题解决

### 列表 30-1：logcheck 报告示例（续）

```
------------------------------------------------------
Sep 2 18:47:23 rh login(pam_unix)[11519]: authentication failure:
logname=LOGIN uid=0 eid=0 tty=tty3 ruser= host= user-bubba
Sep 2 18:47:25 rh login[11516]: FAILED LOGIN 1 FROM (null) FOR
bubba. Authentication failure
Unusual System Events
Sep 2 04:02:08 rh syslog 1.4.1: restart.
Sep 2 11:52:58 rh mc: /dev/gcmtl: No such file or directory
Sep 2 11:52:58 rh mc: /dev/gcmtl: No such file or directory
Sep 2 13:00:42 rh login(pam_unix)[2914]: session closed for user
bubba
Sep 2 16:58:44 rh login(pam_unix)[867]: session closed for user
root
Sep 2 18:44:58 rh su(pam_unix)[11519]: session opened for user
by wing_nut(uid=502)
Sep 2 18:45:02 rh mc: /dev/gcmtl: No such file or directory
Sep 2 18:45:02 rh mc: /dev/gcmtl: No such file or directory
Sep 2 18:47:23 rh login(pam_unix)[11196]: authentication failure:
logname=LOGIN uid=0 eid=0 tty=tty3 ruser= user-bubba
Sep 2 18:47:25 rh login[11516]: FAILED LOGIN 1 FROM (null) FOR
bubba. Authentication failure
Sep 2 18:47:32 rh login(pam_unix)[11196]: session opened for user
bubba by LOGIN(uid=0)
Sep 2 18:47:32 rh --[11196]: LOGIN ON tty3 BY bubba
Sep 2 18:50:46 clio login(pam_unix)[11439]: session opened for
user bubba by LOGIN(uid=0)
Sep 2 18:50:46 rh mc: /dev/gcmtl: No such file or directory
```

# 第 31 章：实施网络安全

## 本章内容

- 理解网络安全
- 限制网络服务
- 实现防火墙

第 30 章开始了保护 Red Hat 系统的讨论，侧重于适用于工作站的措施。本章继续该讨论，重点关注应在网络层应用的安全措施（即使用 Red Hat 系统作为保护的内部网络与意图破坏它的黑客之间的屏障或围栏）。

## 限制网络服务

保护 Red Hat 系统时的第一要工作是识别哪些服务正在运行，你需要哪些服务以及哪些服务是不需要的。然后，你应该禁用不需要的服务。在此语境下，“服务”指的是传统的服务器守护进程和程序，例如 `Apache`（Web 服务器）、`Sendmail`、`TELNET` 或 `FTP` 服务器，以及较为人知的访问点，例如用于 `daytime`、`finger` 的开放端口。从试图实施网络安全的管理员角度来看，限制网络服务还意味着确定谁在系统上做什么，特别是通过某种网络连接。本节以及后续对控制运行服务的配置文件和工具的审查，使你能够根据意愿开启或关闭服务，并使你能够发现系统上发生了什么样的系统活动、是谁在操作以及活动源自何。

## 总结

在本章中，你学习了主机安全，包括防止系统遭受未经授权的重启、配置显示管理器以提高安全性。在检查了日志检查工具后，你学习了配置和微调 `Tripwire`，这是一种基于主机的入侵检测系统。

## 运行了哪些服务？

与大多数 Linux 发行版一样，红帽（Red Hat）的默认安装程序留下了太多的网络服务。当然，某些服务是因为在安装过程中的选择而启用的。然而，其他服务似乎仅仅是默认启用的，也就是说，没有任何理由。“没有显而易见的理由”，这指的是什么呢？许多安装实际上根本不需要提供任何网络服务。典型的工作站可能属于此类群；它是服务的消费者，而不是服务的提供者。例如，工作站不需要提供 Web、电子邮件、`TELNET` 或 `FTP` 服务。在本章中，你将看到在实践中禁用不必要的服务的努力是如何起作用的。

限制这些服务可用性的第一步是找出哪些服务正在活动监听。这项工作具有双重性，因为运行在给定主机上的服务可能能够响应来自主机自身的请求，但可能无法响应来自连接到主机的其他系统的请求。安全漏洞的潜在产生源于该服务本身就是开启的。

即使你使用数据包过滤或 `TCP wrappers` 防止服务响应网络上的其他主机，这些访问控制方法也可能被绕过，并成为进入系统的可能点。因此，应该从内部和外部对服务的可用性进行检查，也就是说，从主机内部、从主机信赖网络内部以及从主机信赖网络外部。安全网络的过程的一部分（但不是全部）包括从你的网络外部运行端口扫描。接下来的几个章节将探索在执行这些端口扫描时用到的几个工具——`netstat`、`lsof` 和 `nmap`。

## 使用 netstat

`netstat` 是一个强大的工具，用于监控和报告内核网络功能和行为的几乎每一个方面。大多数用户熟悉使用 `netstat` 显示当前路由表，如下所示所示：

```
$ netstat -r
```

| 内核 IP 路由表 | | | | | | |
