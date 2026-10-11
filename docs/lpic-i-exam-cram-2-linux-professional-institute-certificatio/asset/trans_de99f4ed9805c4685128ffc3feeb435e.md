

## 附加文档

在 `/usr/share/doc` 目录树中会显示一组附加文档。在 `/usr/share/doc` 目录结构中，有时会出现以下可选目录：

- `/usr/share/doc/program1` — program1 的文档
- `/usr/share/doc/FAQ` — 程序的常见问题解答
- `/usr/share/doc/HTML` — HTML 格式的文档
- `/usr/share/doc/HOWTO` — 所有操作指南（HOWTOs）
- `/usr/share/info` — info 命令使用的文件

> **警告**
> 在考试中，`info` 命令仅短暂出现，其角色是作为 FSF（自由软件基金会）首选的文档阅读器或文档呈现方式。

## 网络与第三方文档

LPI 对第三方文档颇为重视，无论是 Linux 文档项目、新闻组还是邮件列表。

### Linux 文档项目

Linux 的主要文档站点是 Linux 文档项目（[http://www.tldp.org](http://www.tldp.org)）。该站点被视为引导新手的第一个去处，但许多老手也会访问该站点以寻找解决资源、学习新主题或为该项目做出贡献。

LDP 提供的服务包括

- **HOWTOs** — 常规 HOWTO 是关于 Linux 内核、网络等主题的中等到详尽的文档。Mini-HOWTO 是较短的，有时甚至非常简练的文档，专注于诸如三键鼠标配置等更具体的主题。
- **指南（Guides）** — 较长、更具书籍风格的文档，对特定主题（如系统管理、bash 脚本等）进行深度覆盖。
- **FAQs** — 关于 Linux 主题的常见问题汇总。这些比 HOWTO 更具互动性。然而，目前可用的这类资源很少。

> **警告**
> 你很可能会看到关于 LDP 站点 URL 的问题，代表 Web 上 Linux 信息存储库的缩写（LDP），以及该站点的完整名称（Linux 文档项目）的问题。

### Usenet 资源

关于 Usenet 资源，考试中的内容似乎很少，但关于 LPIC 考试与此主题相关的两件事是：

- `www.deja.com` — 这曾是允许通过搜索引擎访问 Usenet 文本的站点，这对那些无法访问新闻源的人来说非常有用。它现在是 `groups.google.com`，你可能会在考试中看到关于此资源的问题。
- `comp.os.linux` — 许多人将其视为 Linux Usenet 资源的根源，这个组是潜伏并获取大量良好信息的好地方。

> **警告**
> 预计会有关于这些资源的考题。彻底研究它们，在这个过程中你会学到很多关于 Linux 的知识，并在考试中表现得更好。

## 与用户沟通

系统中文档的最后部分是关于通过多个程序和文件通知用户系统事件（除了说“离开系统，它要停机了！”之外）。

### Issue 文件

当用户查看文本模式登录屏幕时，他们正在查看 `/etc/issue` 文件的内容。`/etc/issue` 文件通常包含如下所示类型的信息：

```
Red Hat Linux release 7.3 (Valhalla)
Kernel \r on an \m
```

用户通常看到的输出如下所示：

```
Red Hat Linux release 7.3 (Valhalla)
Kernel 2.4.18-3 on an i686
delibert login:
```

修改 */etc/issue* 文件以包含标准法律免责声明，并通知所有未授权使用系统是非法的，这不仅是一个好主意，而且还能从法律上保护系统管理员免受审计员和调查人员的麻烦。

*/etc/issue.net* 文件在功能上等同于 */etc/issue* 文件，但它仅用于在用户通过 Telnet 连接到系统时显示信息。此文件不会显示给 SSH 用户或通过 NFS 或其他网络文件共享协议（如 SMB/CIFS）连接到系统的用户。

> **警告** 在考试中，注意 **issue** 和 **issue.net** 文件。如果你不知道它们包含什么内容，或者什么类型的远程客户端会显示其内容，你就会错过相关题目。

### 当日信息（Message of the Day）

*/etc/motd* 文件通常是一个纯文本文件，在用户通过 Telnet 或 SSH 客户端连接到控制台或远程控制台并登录后显示给他们。

修改 */etc/motd* 后登录，会显示类似以下内容：

```
Red Hat Linux release 7.3 (Valhalla)
Kernel 2.4.18-3 on an i686
login: rbrunson
Password: xxxxxxxxx
This is the motd file
[rbrunson@delibert rbrunson]
```

将此作为与用户沟通系统事件、帮助台电子邮件和电话号码等方法。

### 写入用户

*write* 命令用于与已登录到系统的用户直接通信，其语法如下：

```
write rbrunson /dev/pts/2
```

在此语法中，用户名 *rbrunson* 是一个已登录的用户（可通过 *w* 或 *who* 命令验证），*/dev/pts/2* 代表你可以与他们通信的用户控制台或端口。

当你按 Enter 执行命令时，一条消息会出现在 rbrunson 的控制台上，提示他正在接收来自位于控制台 /dev/tty1 上的 root 用户在 15:51 发送的消息。然后，当 root 用户输入消息并按 Enter 时，该文本会显示在用户的控制台上。当发送方按下 Ctrl+D 时，对话结束。

### 与用户交谈

*talk* 命令适用于与用户的双向通信，允许在两个用户之间进行实质上的聊天会话。

*talk* 命令在机器本地与已登录用户之间工作，或者在机器之间工作，只要用户使用目标用户名登录即可。

要与登录到服务器/机器控制台的 *snuffy* 用户发起 *talk* 会话，你需要以 root 用户身份输入以下命令：

```
talk snuffy tty1
```

这会在 *snuffy* 的控制台上弹出一条消息，提示来自该机器的 root 用户请求连接，并告诉 *snuffy* 输入 `talk root@localhost` 并按 Enter。这将使 root 用户和 *snuffy* 进入聊天模式，root 用户的信息显示在屏幕顶部，*snuffy* 的回复显示在屏幕底部。

你可能需要设置 `mesg` 选项以允许消息显示在你的屏幕上。`mesg y` 命令将控制台设置为允许连接和消息。然而，这会导致各种系统和其他用户垃圾邮件出现，因此你可能希望将其设置为 `mesg n`。

此外，你还必须通过 `chkconfig` 实用程序启用 `ntalk` 守护进程。或者，你可能需要编辑 `/etc/xinetd.d/talk` 脚本，使包含 `disabled = yes` 的行变为 `disabled = no`。这将启用守护进程以开始 talk 会话请求。

> 你将在考试中看到 *motd* 和 *issue* 文件，据报道 *write*、*talk* 和 *mesg* 会偶尔出现。

最后，*wall* 或 *write all* 命令将消息发送到所有位于系统控制台和远程控制台的用户。

要发送 *wall* 消息通知所有用户系统将在 5 分钟后停机，你会使用

```
wall "System going down in 5 minutes"
```

## 备考问题

1. 哪个带选项的命令显示出与 **man -k** 命令相同的输出？在下面的空白处填入显示相同输出的命令及任何选项和参数：

______

正确答案是 **apropos program**。没有替代答案。

2. 由于你所在机构作为国防承包商的身份发生变化，你现在必须拥有包含特定法律文本的警告和登录消息，并显示给任何以登录会话连接到系统的用户。以下哪项可以实现此目的？（选择所有适用项。）

- [ ] A. `/etc/login.defs`
- [ ] B. `/etc/issue`
- [ ] C. `/etc/motd`
- [ ] D. `/etc/issue.net`

答案 B、C 和 D 是正确的，因为它们旨在在登录系统之前或之后向用户显示文本。答案 A 是错误的，因为 `/etc/login.defs` 文件的内容不会在登录之前或之后显示给用户。

3. **man** 页第 1 节所在目录的完整路径是什么？在下面的空白处填入该目录的完整路径和名称：

______

正确答案是 `/usr/share/man/man1`。没有替代答案。

4. 以下哪些资源被认为是 Linux 文档项目的一部分？（选择所有适用项。）

- [ ] A. HOWTOs
- [ ] B. Guides
- [ ] C. OpenDoc
- [ ] D. FAQs
- [ ] E. Usenet

答案 A、B 和 D 是正确的，因为它们都是 Linux 文档项目的一部分。答案 C 是错误的，因为 OpenDoc 是一种编程接口，允许文档的独立部分作为一个整体运行。答案 E 是错误的，因为 Usenet 不是 LDP 的一部分。

