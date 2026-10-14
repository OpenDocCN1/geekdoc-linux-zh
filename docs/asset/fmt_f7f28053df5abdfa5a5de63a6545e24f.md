
与 Apache HTTP 部署不同，Java Web 应用内容的请求通常被委托给另一个进程（例如 Tomcat Web Server），Web Server 7.0 中的 Java 容器嵌入在工作进程本身。这消除了使用进程通信协议（例如 Apache JSP 协议）和通道（例如套接字和管道）的需求。Web Server 与 Java 容器之间（通过编程 API）更紧密的集成使得服务器能够更高效地处理 Java 内容请求，并使 Java 容器能够利用 Web Server 中的子系统（如高性能文件缓存）。

## 2.5 多线程架构

多线程是一种高效的编程模型，多个线程存在于单个进程中共享共享资源但能够同时执行。同一进程中的线程共享地址空间。进程内线程之间的上下文切换通常比进程之间的上下文切换更高效。多线程程序在具有多个 CPU 的计算机上运行得更快。

Web Server 的多线程设计支持海量连接扩展性，且不会牺牲性能或不必要的浪费资源。根据服务器的负载，Web Server 7.0 会自动从低延迟模式切换到高并发模式。

`c++filt` 命令用于对 C++ 符号名称进行修饰（mangle），从而使其更易于读。

```
% /usr/bin/pstack 29472 | /opt/SUNWspro/bin/c++filt
29472: webserver-d -d /opt/webserver7/https-test/config -r /opt/webserver7
fe457c8 pollys (8d008, 3, ffbf460, 0)
fede124 pollys (8d008, 3, 2710, 10624c00, 0) + 7
0001923 int wdlSmanager::Wait_for_Message(2c45c, 0, 12c, 14c, 0)
+ 20
00017268 main (8, 1, 2c45c, 0, 2bc20, 2ff0) + 12a8
000130a0_start (0, 0, 0, 0, 0, 0) + 108
```

对主进程的检查显示，它只有一个线程：

```
% /usr/bin/pstack 29473 | /opt/SUNWspro/bin/c++filt
29473: webserver7 /opt/webserver7/https-test/config -r /opt/webserver7 -t /t
fd5c7c8 pollys (ffbf808, 4, ffbf798, 0)
f56d214 pollys (ffbf808, 4, 64, 10624, 17d784, 5fe5e10) + 7
fe85c70 void ParentAdmin::poll(unsigned) (64, ffbf808, 2710, 7eac, 4, 3) + 42c
ff197654 void poll(unsigned) (25ae88, 2710, ff2a3c0, 0)
ff2a3c0, ff2a3c0, ff2f440) + c
ff19e8ac PRStatus WebServer::() (25ae88, ff2a3f24, fffff
ff2a400, 6, 1) + 494
00010fd4 main (9, ffbfebc, ffbffebec, 21400, fd134fc0) + 1c
00010b98_start (0, 0, 0, 0, 0, 0) + 108
```

以下命令显示了工作进程中的各种线程：

```
% /usr/bin/pstack 29473 | /opt/SUNWspro/bin/c++filt
```

工作进程具有多个线程，请注意每个线程都用如下形式的行隔开：

```
lwp# 6 / thread# 6
```

其中 `lwp`（轻量级进程）标识操作系统层级，而线程数标识用户层级。

虽然 `pstack` 命令对工作进程的输出非常详尽，无法全部包含，但其余部分识别了对应于工作进程中子进程的线程。

以下 `lwp#1` 的堆栈跟踪显示了工作进程中主线程的调用栈，用于检测服务器何时关闭：

```
lwp#1 / thread#1
fd5c4a9c lwp_park (0, fff8f8, 0)
fd5eae8 cond_wait_queue (154c90, 25ae8, fff88d, 0, 0, 0) + 28
d5bef60 cond_wait_common (154c90, 25ae8, fff88d, 0, 0, 0) + 298
d5bbf0f8 pr_Thread_cond (154c90, 25ae8, ffffa60, 0, 0, 0) + 34
d5bfle6c cond_timedwait (154c90, 25ae8, ffffa60, b1a1300, 998660, 4e7e3650) + 14
d5bf22c thread_cond_timedwait (154c90, 25ae8, fffb84, 48c32a4, 0, 1ce6a8b) + c
fe85a1c pr_ThreadCond (154c88, 0, 827f20, 0, 1ce6a8b, 0) + 170
f19f77ac PR WebServer::Run() (ff2a4000, ff2a4000, 6, 2a5cf8, 3d, f22a6b4) + 1394
00010fd4 main (9, fffbc4c, ffeb210, 0, fd134fc0) + 1c
00010b9b_start (0, 0, 0, 0, 0, 0) + 108
```

此线程的后续堆栈跟踪用于动态配置服务器：

```
lwp#6 / thread# 6
fd5c4a9c lwp_park (0, 2af190, 32e368, 0, 0) + 0
fd5eae8 cond_wait_queue (2af190, 32368, 0, 0, 0) + 28
d5bf068 cond_wait_common (2af190, 32368, 0, 0, 0) + 298
d5bfb0a4 pr_Thread_cond (2af190, 32368, 0, 0, 0) + 34
d5bf0a4 cond_timedwait (2af190, 32368, 0, b1a1300, 998660, 4e7e3650) + 14
d5bf0a4 thread_cond_timedwait (2af190, 32368, 0, 48c32a4, 0, 1ce6a8b) + c
fe85a1c pr_ThreadCond (154c88, 0, 827f20, 0, 1ce6a8b, 0) + 170
f19f77ac PR WebServer::Run() (ff2a4000, ff2a4000, 6, 2a5cf8, 3d, f22a6b4) + 1394
00010fd4 main (9, fffbc4c, ffeb210, 0, fd134fc0) + 1c
00010b9b_start (0, 0, 0, 0, 0, 0) + 108
```

*(注：由于原文中存在大量重复的 OCR 错误干扰文本，翻译时已根据逻辑保留了核心堆栈结构。)*

`lwp12` 的以下调用栈是一个接收线程的：

```
fd5c57c8 polls (fcaf88, 1, fcaf08, 0)
fd561d2 poll (fcaf88, 1, 1388, 10624c0, 0, 0) + 7c
fd58658_pt_poll_now (fc4f34, 1, fcbd24, fcaf88, 028, fffffff) + 4c
fe85e9f8_pt_accept (230408, fcafbe58, fffffff, 13, 0, fffffff) + cc
ff77690 PRFileDesc::accept(PRNetAddr&, const unsigned) (1b9c48, fcafbe58, fffffff, ff00000, 0, fd5f478) + cc
f17c30 void Acceptor::run (128398, 7, 0, 2, fffffff) + 4c
fe6a2d4 ThreadMain (128398, 2531a8, 0, feb9c0, ff17be4, ff2a3a0) + 1c
fe85e04c pt_root (2531a8, fefa6cd8, 400, fe87bb8, 0, fe87914) + d4
fd5c9fc_lwp_start (0, 0, 0, 0, 0)
```

### 3. 练习

如果你同时拥有一台 Solaris 和 Linux 计算机，请在这两个操作系统上都安装 Web Server 7。在每台计算机上启动实例，并对比在 Solaris 和 Linux 上执行 `ps -ef` 命令的输出。为什么 Linux 上有这么多 `webserv` 进程呢？

注意：访问 `www.sunwebserver.com` 获取如何执行上述这些练习的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_66_0.png)
