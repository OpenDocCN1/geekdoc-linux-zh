
一旦怀疑机器遭受了 Rootkit 攻击，你可以做几件事来验证这一点。最简单的方法是尝试使用 `-`/` 选项运行 `du`、`ls`、`ps` 和 `netstat`。如果其中任何一个接受此选项，则说明已安装了 Rootkit。此外，掩码列表处理中没有短路；即使使用掩码规范命中，检查仍会继续。因此，较大的规范列表可能会导致程序出现明显的减速。在 `/dev` 中使用 `file` 找到的文本文件（尤其是名称形式为 `/dev/pty` 且没有设备号的文件）也值得怀疑。

验证入侵的另一种方法是使用其完整性已知的系统程序。将 `ps`、`ls`、`du`、`ifconfig` 和 `netstat` 的原始副本放在写保护软盘上是个好主意。这些可在硬盘上的系统程序完整性存疑的情况下使用。在以下文本中描述的这些情况下，还可以使用许多第三方（即非标准）实用程序。

### `top(1)`

一个系统监控实用程序，结合了 `ps(1)`、`uptime(1)`、`renice(8)` 和 `kill(1)` 的功能。它可以在 `ftp://eecs.nwu.edu/pub/top/` 找到，并可用于可靠地检查 SunOS 主机上是否存在 rogue 程序，因为 SunOS 版本的 Rootkit 不包含 `top(1)`。

### `lsof`

List Open Files (`ftp://vic.cc.purdue.edu/pub/tools/unix/lsof/`) 列出所有打开的文件，包括打开的网络套接字。

### 表 19.2 Linux Rootkit II v1.0 中的程序

| Tool | Description |
|------|-------------|
| `chfn` | 如果在提示输入姓名时输入魔术密码，你将被放入 uid 0 `/bin/sh` shell，而不是被提示输入密码以提交对你的 finger 信息的任何更改。 |
| `chsh` | 如果在提示输入新 shell 时输入魔术密码，你将被放入 uid 0 `/bin/sh` shell。 |
| `inetd` | 当你连接到 rfe 服务（Radio Free Ethernet）时运行 `/bin/sh -i` 作为服务器。许多 Linux 发行版在 `/etc/services` 中不列出此服务，且 Rootkit 的安装程序也不会添加它。 |
| `login` | 允许在关闭所有日志记录的情况下以 root 登录。有两种触发方式：魔术用户 ID `rewT`，允许即使在未受保护的终端上也以 root 登录且用户永远不会被查询密码；或任何用户 ID 配合魔术密码 `lrkroX`。 |
| `ls/du` | 这些与 SunOS 附加组件相同。注意，由于 Linux 发行版是 POSIX，使用 `fnmatch()` 而不是 `strcmp()` 来允许掩码文件中使用正则表达式将非常容易（GNU 的 `ls`，即 Linux 中使用的 `ls`，已经使用 `fnmatch`）。 |
| `ifconfig` | 这与 SunOS 版本相同。 |
| `netstat` | 基于 UID 和 UNIX 套接字路径添加了掩码。`netstat` 包含“showall”(`-a`) 选项。 |
| `passwd` | 如果输入 Rootkit 魔术密码而不是用户密码，则以 UID、EUID、GID 和 EGID 设为 0 的方式运行 `/bin/bash`。 |
| `ps` | 这与 SunOS 版本相同。 |

- **`tcplist`**：以漂亮的表格列出所有打开的网络连接，包括协议/端口号、远程主机名、本地服务器/客户端的 UID，以及对于运行 ident 服务器的远程站点的远程用户（`ftp://ftp.cdf.toronto.edu/pub/tcplist`）。

- **`cpm`**：可用于 SunOS 和 Solbourne 主机，以确定机器的以太网接口是否运行在混杂模式（`ftp://info.cert.org/pub/tools/cpm/cpm1.0.tar.Z`）。为了检查文件完整性，还应该将加密校验和程序 `md5` 加入这个工具库。

- **`zap`**：这可能也有用，因为它不是从 `utmp`/`wtmp`/`lastlog` 文件中删除用户，而是用二进制零覆盖这些条目。这样的条目可能表明主机已遭到攻击。

## Rootkit 攻击后的清理工作

一旦发现主机遭到入侵，你必须确定攻击的范围。你必须假定在入侵期间，网络上任何“可见”主机的所有进出网络事务都已被监视，入侵者可能掌握了因此暴露的任何或全部信息。你应该按照下文所述进行恢复并防止未来攻击。

在恢复期间，断开主机与网络的连接，或以单用户模式运行系统。这将防止用户和入侵者访问系统。

### 表 19.2（续）

| 工具 | 描述 |
| --- | --- |
| `top` | 这与 Linux 的 `ps` 程序相同。 |
| `rshd` | 当本地用户（相对于 `rshd` 服务器）是 Rootkit 魔法口令时，通过 `/bin/sh` 以 root 身份运行命令。例如，`rsh -l lrk0x victim.org /bin/sh -i` 会提供一个交互式 root shell。 |
| `syslogd` | 过滤包含指定子字符串的日志消息（通过掩码文件）。这可以大大减少入侵者需要在后续访问中掩盖其踪迹所需的工作量。 |
| `bindshell` | 当你连接到该端口时，将 `/bin/sh` 绑定到一个套接字（默认为端口 31337）（命令需要以分号 `;` 结尾）。 |

定位标准系统程序的特洛伊木马版本可能很困难，你在这样做时应保持谨慎。入侵者可能安装了不属于 Rootkit 的其他特洛伊木马程序；因此，除非从发行介质或软盘备份副本恢复，否则不应信任任何系统实用程序，如前所述。这尤其适用于 `sum`、`cmp` 和 `ls`。

我建议从只读发行介质执行整个系统安装。如果不可行，则应使用已知良好的 `md5` 副本将所有系统二进制文件与只读发行介质进行比较。由于 Rootkit 安装的特洛伊程序与合法版本具有完全相同的校验和和时间戳，因此这些属性不能用于查找特洛伊程序。然而，加密校验和几乎不可能被伪造。因此，可以信任来自只读软盘备份的 `md5`，将已安装程序与发行介质或已知正确的校验和进行比较。有关各种 SunOS 版本的加密校验和的详细列表，请参阅 CIAC 公告 E-12 的附录 B。Linux 发行版中流行的“活动文件系统”CD-ROM 也可以使用。

除非明确知道备份是在特洛伊木马安装之前制作的，否则要抵制从备份恢复的诱惑。否则，备份包含特洛伊木马程序而不是合法程序的可能性太大。

预防和消除 Rootkit 攻击的唯一有效的长期解决方案是在协议层使用加密。尽管存在 IP 欺骗，但只要不在网络上传输可重复使用的明文密码，可能就足够了。实现这些目标的相关软件包包括连接加密软件包 `ssh`（`ftp://ftp.cs.hut.fi/pub/ssh/`）以及一次性密码软件包 `S/KEY`（`ftp://thumper.bellcore.com/pub/skey/`）和 `OPIE`（`ftp://ftp.nrl.navy.mil/pub/security/opie/`）。

有几种短期解决方案。简单的方案包括在非开发机器上禁用 C 编译器。事实上，人们普遍认为这对关键服务器是有益的，因为它大大减少了可能被利用的漏洞数量。正确安装和运行 `Tripwire`（`http://coast.cs.purdue.edu/pub/tools/unix/Tripwire/`）是一条极好的防线。另一种方法是删除 SunOS 和 Solbourne 主机上的 `/dev/nit` 设备。这可以通过在注释掉以下几行后重建内核来完成。

```
# The following are for streams NIT support. NIT is used by etherfind,
# traffic, rarpd, and nboot. As a rule of thumb, NIT is almost always
# needed on a server and almost never needed on a diskless client.
#pseudo-device snit        # streams NIT
pseudo-device pf           # packet filter
pseudo-device nbuf         # NIT buffering module
```

有关如何重建内核的详细信息，请参阅你的《系统与网络管理手册》中的“重新配置系统内核”一节。

## 对您所有系统管理问题的答案 UNIX

- 崩溃恢复
- 互联性
- 性能调优
- 备份
- Web 集成
- NT 集成
- 安全
- 以及更多

获取唯一 100% 致力于 UNIX 系统管理的杂志——扎实的技术信息以及提高系统性能和扩展系统功能的方法。常规栏目和部门还为您提供了对重要书籍、新产品发布、升级和职业机会的深入了解。报道涵盖多种平台，包括 Solaris、AIX、HP-UX、SCO、Linux 等。如果您管理系统，Sys Admin 可以为您和您的组织节省时间和金钱。

## Sys Admin UNIX 系统管理员 Linux 的杂志

立即致电获取免费试刊！

一年的及时有效提示和技巧汇聚于一处。

您所需的一切，让您的系统运行得比以往更好！
