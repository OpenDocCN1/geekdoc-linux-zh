

事物程序必须在两者之间切换执行——必须进行初始化。受控守护进程首先为每个线程的所有全局变量设置值。然后它将配置文件 /etc/gated.conf 读入内存。由于 gated 是模块化的，它不会加载运行其支持的每个协议的能力。相反，它会在 /etc/gated.conf 中查找已启用的协议，并为每个协议设置运行框架，包括加载适当的代码模块。

当你配置 gated 的行为时，你要做的一件事是设置它从外部源导入路由的规则。在这一点上，这些规则被加载到内存中。之后，gated 加载你希望它处理向其他路由器和协议导出路由的规则。

此时所有初始化都已完成。gated 守护进程进入程序员所称的 forever loop，这意味着它进入实际运行状态——并且它将一直保持在那里，直到你告诉它做其他事情。它首先设置不同协议行为所需的所有计时器。然后守护进程查看 gated 感兴趣的套接字，即程序之间传输信息的文件，并从中加载任何相关数据。如果有任何由此产生的任务需要运行，它们将被排队以便在轮到它们时开始。

最后，gated 运行在前台和后台发生的任务。前台任务对管理员可见，并且是只需要运行一次的项目。它们通常是协议模块发出的请求，以便在有 CPU 时间时处理某事。相比之下，后台任务是隐藏的，可能会不断运行或按固定间隔运行。

## 配置公共 gated

gated 配置文件是 gated.conf。此文件中的语句可以跨越一个或多行，因此以分号 (;) 终止。这里你还会遇到两种不同的注释。一种是标准的井号 (#)，它注释掉整行。另一种是类似 C 的配对：/* 开始注释，*/ 结束注释。现在，基础知识讲完后，让我们看看这个文件是如何构建的。

需要牢记的最重要事情之一是语句类型顺序。有许多主要语句类型必须按正确顺序使用，还有两种额外的语句类型可以根据需要随意散布在各处。语句类型及其内部的项目在表 5.3 中简要定义，供参考。

## 表 5.3 gated.conf 可用的语句类型，按顺序要求排序

| Type | Order | Statements |
|---|---|---|
| options | First | options |
| definition | Second | autonomoussystem, martians, routerid |
| control | Third | aggregate, export, generate, import |
| directives | Third | \directory, \include |
| interfaces | Third | interfaces |
| protocol | Third | bgp, egp, icmp, isis, kernel, ospf, redirect, rip, snmp |
| static | Third | static |
| trace | Third | traceoptions |

## The options Statement

典型的 gated.conf 文件以 options 语句开始，该语句设置适用于其后所有内容的全局值。如果你不需要，可以完全没有 options 语句。这些项目在整体语句中不需要任何特定顺序。

## 表 5.4 gated.conf options 语句中可用的值

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| mark | 每隔指定间隔向 gated 日志文件写入时间戳。 | mark time | 时间戳之间等待的秒数。 |
| noresolv | 指定不尝试将 IP 地址转换为 host.domain.extension。 | noresolv | N/A |
| nosend | 指定不发送数据包。仅监听网络流量。仅用于避免 RIP 流量。 | nosend | N/A |
| syslog | 设置 gated 应通过 syslog 记录的数据量。有两种不同的语法选项。第一种仅记录所列级别，第二种记录从最低到指定级别的所有级别。 | syslog level
syslog upto level | 日志级别，从最少到最严重列出：debug, info, notice, warning, err, crit, alert, 和 emerg。你决定记录的级别越低，生成的数据就越多。 |

