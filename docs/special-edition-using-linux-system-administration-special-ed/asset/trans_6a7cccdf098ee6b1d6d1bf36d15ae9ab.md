
3. 解压INN发行版归档：

    ```
    # tar xzvf inn-2.2.1.tar.gz
    ```

4. 将当前目录切换到解压归档时创建的目录：

    ```
    # cd inn-2.2.1
    ```

5. 创建组 news：

    ```
    # groupadd news
    ```

6. 创建用户 news 并将该账户的主目录设置为 `/usr/local/news/`：

    ```
    # useradd -g news -d /usr/local/news/ news
    ```

7. 使用以下命令配置INN源代码以进行编译：

    ```
    # ./configure --with-perl
    ```

8. 该配置脚本将根据你的系统构建一个用于编译的 Makefile。

9. 编译INN软件：

    ```
    # make
    ```

10. INN源代码将被编译成二进制文件。

11. 安装编译后的INN软件：

    ```
    # make install
    ```

12. 编译后的二进制文件以及INN手册页和其他文档将被安装到默认位置。

## INN总体概述

INN执行的操作可分为五个主要领域：

- 接收传入的新闻源
- 处理传出的新闻源
- 服务新闻阅读器，并促进文章的阅读和发布
- 让旧文章过期
- 记录所有活动

当运行INN的系统启动时，它会启动脚本 `/etc/rc.d/rc.news`。该脚本以 root 用户身份运行，并启动 INN 守护进程 innd，出于安全原因，innd 以 news 用户身份运行。`rc.news` 实际上通过 `innstart` 脚本启动 innd，该脚本打开 NNTP 端口，将端口的用户 ID 和组 ID 设置为 news 用户和组，然后使用 `-p` 标志启动 innd。

对 innd 进行多级启动以及切换用户的目的是防止安全问题。如果像INN这样的服务以 root 用户身份运行，那么该软件就拥有 root 权限，而如果有人破坏了该服务，他们就可能获得 root 权限。运行 rc.news 后不久执行的 ps 命令显示 innd 以 news 用户身份运行：

```text
# ps auxw|grep news
news       13735  0.3  4.6  6212 2932 ?        S    16:33  0:01 /usr/local/news/
➥bin/innd -d4
root       13737  0.0  1.5  1836  988 pts/0    S    16:33  0:00 sh /usr/local/news/
➥bin/rc.news
news       13741  0.0  0.9  1516  616 ?        SN   16:33  0:00 /usr/local/news/
➥bin/overchan
news       13742  0.0  1.2  1760  804 ?        SN   16:33  0:00 /usr/local/news/
➥bin/inndfeed
root       13761  0.0  1.5  1852 1008 pts/0    S    16:34  0:00 sh /usr/local/news/
➥bin/innfeed
news       13981  0.0  1.2  1756  772 pts/0    S    16:40  0:00 /usr/local/news/
➥bin/activated
```

innd 是主守护进程，负责执行某些任务，同时它会调用其他程序来完成其他任务。该守护进程处理所有传入的文章源，并将其写入磁盘。为了发送文章，它使用 nntpsend 或 innfeed 等外部程序。

启动时，innd 会读取三个配置文件：

- `~news/etc/active`
- `~news/etc/newsfeeds`
- `~news/etc/incoming.conf`

> **注意**
>
> news 前面的波浪号（`~`）是一个特殊的 shell 变量，它会导致 `~news` 被替换为 `/etc/passwd` 映射中指定的 news 用户的主目录。换句话说，如果 news 用户的主目录是 `/usr/local/news`，shell（csh、ksh 或 bash）会将 `~news` 替换为此路径。

加载配置后，innd 会监听 119 端口上的传入 NNTP 连接请求。

> **注意**
>
> 如果你使用的是 Red Hat Linux 6.2 附带的 INN 版本，则 INN 配置文件存储在 `/etc/news/` 中，而不是 `~news/etc`。

### 接收传入的新闻源

当收到来自 `incoming.conf` 文件中列出的授权新闻源站点的连接时，将接受文章源。

### 处理传出的新闻源

对于传出的新闻源，innd 使用 `nntpsend` 或 `innfeed` 将已发布的文章发送到新闻源站点。这些进程由 cron 按计划运行（如第7章“计划任务”所述），以定期扫描并发送传出文章。

### 服务新闻阅读器并促进文章的阅读与发布

如果请求来自 `~news/etc/nnrp.access` 文件中标识的授权新闻阅读器，innd 将启动一个 nnrpd 进程来处理该阅读器的连接。这使 innd 可以空闲出来处理传入的新闻源连接。

### 文章过期

在INN模型中，文章不会永久保留在新闻组中。相反，它们会按照计划过期，以确保新闻组不会增长到难以管理的大小。文章的过期由脚本 `news.daily` 处理，该脚本由 cron 调度（如第7章所述）；通常 `news.daily` 计划每天运行一次。`news.daily` 脚本读取 `~news/etc/expire.ctl` 配置文件，该文件定义了文章过期的策略。

### 记录所有活动

大多数INN日志消息都会写入 `/usr/local/news/log` 目录中的日志文件。此外，一些日志消息会写入 `/var/log/messages`。当然，这取决于系统 `/etc/syslog.conf` 文件中如何配置新闻消息的日志记录。

## 配置INN

INN通常将其配置文件存储在 `~news/etc/` 中。随 Red Hat Linux 6.2 一同发布的INN版本将这些文件存储在 `/etc/news/` 中。

这些文件用于完成多个配置任务。我们将考虑以下任务：

- 为新闻文章选择存储方法
- 编辑 `inn.conf`
- 编辑 `newsfeeds` 文件
- 编辑 `incoming.conf`
- 将 `cycbuff.conf` 文件用于 CNFS
- 为 CNFS 和 timehash 编辑 `storage.conf`
- 将 `overview.ctl` 文件与 CNFS 和 timehash 存储一起使用
- 使用 `nnrp.access` 文件控制客户端访问
- 使用 `expire.ctl` 控制文章过期
- 为 CNFS 存储创建文章缓冲池
- 使用 `nntpsend.stl` 文件指定要供稿的站点
- 使用 `news.daily` 工具控制每日维护
- 使用 `rc.news` 在引导时启动INN

### 选择新闻文章的存储方法

有三种方法可用于在INN中存储新闻文章：

- **传统方法：** 此方法由旧版INN使用。文章以单独的文件存储，文件名按文章编号命名。这些文件存储在基于新闻组名称的目录层次结构中。例如，`comp.os.linux.networking` 中的文章 12345 存储在 spool 目录中；通常位于 `/usr/local/news/spool/comp/os/linux/networking/12345`。传统方法基于久经考验的代码，与第三方INN应用程序具有广泛的兼容性。该方法还提供对文章过期时间的精细控制。但其代价是在单个目录中存储大量文件，这会产生性能瓶颈。此方法要求极为快速的计算机、磁盘和磁盘控制器，才能支持大型新闻源站点。
- **Timehash：** 此方法是传统方法的一种变体。文章仍以单独的文件存储，但目录层次结构基于文章的到达时间。这避免了包含大量文件的目录（很容易出现这种情况）带来的瓶颈。目录按组名结构化。该方法还允许对文章过期时间进行精细控制，但代价是仍然需要非常快的计算机、磁盘和磁盘控制器来处理基于文件的文章存储的性能要求。
- **CNFS：** 此方法按顺序将文章存储在预先配置的循环缓冲区文件中。当达到缓冲区末尾时，新文章会从缓冲区开头开始存储，覆盖缓冲区中最旧的文章。此方法提供了极快的性能：操作期间无需创建或删除文件，也无需运行过期流程，因为文章会随着缓冲区填满而自动覆盖。此外，INN使用的磁盘空间保持不变，将它们分配到不同大小的固定缓冲区可以控制各个组的大小。这些好处的代价是对文章过期的控制较少。但是，如果你希望某个组的保留时间更长，而该组突然开始接收非常大的流量，则CNFS存储方法可能会造成问题。

一般来说，经验丰富的新闻管理员会选择CNFS而非其他存储方法，因为CNFS方法的优点远远超过其唯一的缺点。I/O性能极快，而且永远不必担心文件系统被填满，这两点足以成为考虑使用此方法的理由。
