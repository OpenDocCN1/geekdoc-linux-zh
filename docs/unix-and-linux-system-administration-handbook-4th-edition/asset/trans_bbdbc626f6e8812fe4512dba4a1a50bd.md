

## 17.2 DNS 如何工作

使用 DNS 的每个主机要么是该系统的客户端，要么同时是客户端和服务器。如果你不打算运行任何 DNS 服务器，那么阅读接下来的几节并不是必需的。只需跳到第 561 页，了解如何将一台机器配置为 DNS 客户端的详细信息。

### 资源记录

每个站点都维护着构成全球 DNS 系统的分布式数据库中的一个或多个部分。你的数据库部分由文本文件组成，其中包含每个主机的记录；这些被称为“资源记录”。每条记录都是一行，由一个名称（通常是主机名）、记录类型和一些数据值组成。如果名称字段的值与上一行的相同，则可以省略名称字段。

例如，以下行

```text
nubark      IN  A     63.173.189.1
            IN  MX  10 mailserver.atrust.com.
```

在“正向”文件（称为 atrust.com）中，以及以下行

```text
1   IN  PTR  nubark.atrust.com.
```

在“反向”文件（称为 63.173.189.rev）中，将 nubark.atrust.com 与 IP 地址 63.173.189.1 关联起来。MX 记录将发往该机器的电子邮件重定向到主机 mailserver.atrust.com。

资源记录是 DNS 的通用语言，与控制任何给定 DNS 服务器实现操作的配置文件无关。它们也是在 DNS 系统中流动并在各处被缓存的数据片段。

### 委派

所有名称服务器都从本地配置文件读取根服务器的身份，或将其内置于代码中。根服务器知道 com、net、edu、fi、de 等顶级域的名称服务器。往下走，edu 知道 colorado.edu、berkeley.edu 等。每个域都可以将对其子域的权限委派给其他服务器。

让我们检查一个真实的例子。假设我们想从机器 lair.cs.colorado.edu 查出机器 vangogh.cs.berkeley.edu 的地址。主机 lair 向其本地名称服务器 ns.cs.colorado.edu 请求找出答案。以下插图（图 A）显示了随后的事件。

**图 A：vangogh.cs.berkeley.edu 的 DNS 查询过程**

![](img/14d78e3cecac4581d37024baf1e94cca_604_0.png)

服务器之间箭头上的数字显示了事件的顺序，而字母表示事务的类型（查询、引用或答案）。我们假设在查询之前所需的信息都没有被缓存，除了根域的服务器名称和 IP 地址。

本地服务器不知道 vangogh 的地址。事实上，它对 cs.berkeley.edu 或 berkeley.edu 甚至 edu 一无所知。它确实知道根域的服务器，因此它向根服务器查询 vangogh.cs.berkeley.edu 并收到对 edu 服务器的引用。

本地名称服务器是一个递归服务器。当查询的答案由对另一服务器的引用组成时，本地服务器会将查询重新提交给新服务器。它会继续跟踪引用，直到找到拥有所需数据的服务器为止。

在这种情况下，本地名称服务器将其查询发送给 edu 域的一台服务器（询问的始终是 vangogh.cs.berkeley.edu），并得到对 berkeley.edu 服务器的引用。本地名称服务器随后在 berkeley.edu 域中重复查询。如果伯克利服务器没有缓存答案，它会返回对 cs.berkeley.edu 服务器的引用。cs.berkeley.edu 服务器对所请求的信息具有权威性，会在其区域文件中查找答案并返回 vangogh 的地址。

尘埃落定后，ns.cs.colorado.edu 已缓存了 vangogh 的地址。它还缓存了 edu、berkeley.edu 和 cs.berkeley.edu 的服务器数据。

你可以使用 `dig +trace` 或 `drill -T` 详细查看查询过程。[^1]

### 缓存与效率

缓存提高了查询效率：缓存的答案几乎是免费的，而且通常是正确的，因为主机名到地址的映射很少更改。一个

[^1]: dig 和 drill 都是 DNS 查询工具：dig 来自 BIND 发行版，drill 来自 NLnet Labs。

