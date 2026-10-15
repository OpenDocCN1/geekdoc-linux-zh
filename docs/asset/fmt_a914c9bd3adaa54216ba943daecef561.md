
master 程序启动并监控所有 Postfix 进程。它的配置文件 `master.cf` 列出了子程序以及关于如何启动它们的信息。该文件中设置的默认值涵盖了大多数需求；在

## 第 20 章 电子邮件

为了避免让接收主机负载过重（特别是在其宕机后），Postfix 使用了一种慢算法来控制尝试投递邮件的速度。延迟的邮件会被赋予一个重试时间戳，该时间戳呈指数级退避，以避免在无法投递的邮件上浪费资源。不可访问的状态缓存可以避免不必要的尝试。

### 发送邮件

`qmgr` 配合 `trivial-rewrite` 头部决定邮件应该发送到哪里。`trivial-rewrite` 的路由决策可以通过查找表（`transport_maps`）进行覆盖。

通过 SMTP 协议向远程主机投递由 `smtp` 程序执行。LMTP 使用 LMTP 投递邮件；这是 RFC2033 定义地邮件传输协议。LMTP 基于 SMTP，但该协议经过修改，邮件服务器不需要管理邮件队列。这种邮件器对于将电子邮件发送到如 Cyrus IMAP 套件之类的邮件服务器特别有用。

`local` 的工作是在本地投递电子邮件。它处理别名表中的地址，并遵循收件者转发文件中的指令。邮件可以被转发到另一个地址、传递给外部程序，或存储在邮件文件夹中。

`virtual` 程序将邮件投递到“虚拟邮箱”；即那些与 Linux 账户无关但仍代表有效邮件目的地的邮箱。`pipe` 实现了通过外部程序进行投递。

### 安全

Postfix 在多个级别实现安全防护。大多数 Postfix 服务器程序都可以在 `chroot`（禁闭根）环境中运行。它们是独立的程序，没有父子关系。它们中没有一个被设置了 `setuid`。邮件投递目录允许 `postdrop` 组组写，而 `postdrop` 程序被设置了 `setuid`。

令人印象深刻的是，在 Postfix 的任何版本中都没有发现任何可被远程利用的漏洞。

### Postfix 命令与文档

几个命令行工具允许用户与邮件系统进行交互：

- `sendmail`, `mailq`, `newaliases` – 兼容 sendmail 的替代品
- `postfix` – 启动和停止邮件系统（必须以 root 运行）
- `aliases` – 构建、修改和查询别名表
- `postcat` – 打印队列文件的内容
- `postconf` – 显示和编辑主配置文件 `main.cf`
- `postfix` – 构建、修改或查询查找表
- `newuper` – 管理邮件队列

### 基础设置

Postfix 分发包含一组 man 页面，描述了所有程序及其选项。`postfix.org` 上的文档解释了如何配置和管理 Postfix 的各个方面。这些文档也包含在 Postfix 分发的 `README_FILES` 目录中。

### Postfix 配置

`main.cf` 文件是 Postfix 的主配置文件。`master.cf` 文件配置服务器程序。它还定义了 `main.cf` 引用的各种查找表，并提供了不同类型的映射。

`postconf(5)` man 页面描述了可以在 `main.cf` 文件中设置的每一个参数。还有一个 `postconf` 程序，所以如果你只输入 `man postconf`，你得到的是程序的页面而不是 `postconf(5)`。使用 `man -s postconf` 获取正确的版本（在 HPUX 和 AIX 上使用 `man 5 postconf`）。

Postfix 配置语言看起来像一系列 sh 命令和赋值语句。在定义其他变量时，可以通过在变量前加上 `$` 来引用变量。变量定义按照它们在配置文件中出现的形式存储；在它们之前不会被扩展，替换在它们时发生。

你可以通过为变量赋值来创建新变量。注意选择不要与现有配置变量冲突的名称。

所有 Postfix 配置文件（包括查找表）都认为开头为空格的视为延续行。这种约定使得配置文件具有很高的读性，但你必须在第一列开始新行。

#### 在 main.cf 中放入什么

`main.cf` 文件可以指定超过 500 个参数。然而，在平均站点中，只需要设置其中几个。Postfix 的作者强烈建议在你的配置中仅包含非默认值的参数。如果某个参数的默认值在未来发生变化，你的配置将自动采用新值。

分发带的示例 `main.cf` 文件包含许多被注释的示例参数，并附有简短文档。原始版本最好保留原样参考。从任何一个文件开始你的配置，这样你的设置就不会在命令的海洋中丢失。

### 基础设置

让我们从尽可能简单的配置开始。惊讶的是，这是一个完全合理的 Postfix 配置。它产生了一个邮件服务器，可以在本地主机名相同的本地域内本地投递电子邮件，并将任何发往非本地地址的邮件直接发送到相应的远程服务器。

![](img/9b33263d3e7e36cd43da7756018c8735_879_0.png)

## 第 20 章

## 电子邮件

另一个简单的配置是“空客户端”`null client`；即一个系统不在本地投递任何电子邮件，而是将出站邮件转发到指定的服务器。为了实现此配置，我们定义了几个参数，从 `mydomain` 开始（它定义主机名的域名部分），以及 `myorigin`（附加到未限定邮件地址末的邮件域）。如果这两个参数相同，我们可以写类似这样的代码：

```
mydomain = cs.colorado.edu
myorigin = $mydomain
```

我们应该设置的另一个参数是 `mydestination`，它指定邮件域。如果邮件的收件者的邮件域是 `mydestination`，邮件将通过本地程序传递给相应的用户（假设没有找到相关的别名或 .forward 文件）。如果 `mydestination` 中包含多个邮件域，它们都被视为同一域的别名。

对于空客户端，我们不需要本地投递，所以此参数应该是空的：

```
mydestination =
```

最后，`relayhost` 参数告诉 Postfix 将所有非本地邮件发送到指定的服务器：

```
relayhost = [mail.colorado.edu]
```

方括号告诉 Postfix 将字符串视为主机（DNS A 记录）而不是域名（DNS MX 记录）。由于空客户端不应该接收邮件，最后要做的是注释掉 `master.cf` 文件中的 `smtpd` 行。通过这几行，我们定义了一个功能完整的空客户端！

对于“真正的”服务器，你还需要一些配置选项以及映射表。我们将在后续章节中介绍这些。

### postconf 的用法

`postconf` 是一个帮助配置 Postfix 的方便工具。不带参数运行时，它会打印当前配置的所有参数。如果你将特定参数作为参数，`postconf` 会打印该值。`-d` 选项让 `postconf` 默认值而不是当前配置。例如：

```
$ postconf mydestination
mydestination =
$ postconf -d mydestination
mydestination = $mydomain, localhost
```

### 查找表

Postfix 的许多方面通过使用查找表来塑造，表可以将键映射到值或实现简单的列表。例如，默认的 `alias_maps` 表是

```
alias_maps = dbm:/etc/aliases, nis:mail.aliases
```

数据源使用 `type:path` 符号指定。注意这个特定的表实际上使用了两个信息源：`dbm` 数据库和 NIS 映射。多个值可以用逗号、空格或其他分隔。表 20.21 列出了可用的数据源；`postconf -m` 显示这些。

#### 表 20.21 Postfix 查找表的信息源

| 类型 | 描述 |
|---|---|
| `dbm`/`sdbm` | dbm 或组数据库文件 |
| `cidr` | CIDR 格式的网络地址 |
| `hash`/`btree` | Berkeley DB 哈希或 B树文件（替换 dbm） |
| `ldap` | LDAP 服务 |
| `mysql` | MySQL 数据库 |
| `nis` | NIS 服务 |
| `pcre` | Perl 兼容正则表达式 |
| `pgsql` | PostgreSQL 数据库 |
| `proxy` | 通过 proxymap 访问，例如转义 |
| `regexp` | POSIX 正则表达式 |
| `static` | 无论键如何都返回指定的值 |
| `unix` | `/etc/passwd` 和 `/etc/group` 文件；使用 NIS 语法* |

a. `unix:passwd` 是密码文件，`unix:group` 是组文件。

`alias_database` 指定由 `newaliases` 重建的表，并应该与你在 `alias_maps` 中指定的表对应。之所以有两个参数是因为 `alias_maps` 可能包含不需要重建的非数据库源（如 `mysql` 或 `nis`）。如果兼容性不是问题，请使用：
