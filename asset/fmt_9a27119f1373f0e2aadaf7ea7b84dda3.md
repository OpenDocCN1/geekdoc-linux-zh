
对于每一对目录，用户目录 `~/.unison` 中都会维护一个同步日志。配置集如 `~/.unison/example.prefs` 也可以存储在该目录中：

```
root=/home/foobar/dir1
root=ssh://fbar@server//homes/fbar/dir2
batch=true
```

## 文件 49: 文件 `~/.unison/example.prefs`

要启动同步，请像 `unison example.prefs` 那样，将此文件指定为命令行参数。

## 更多信息

Unison 的官方文档非常有帮助。出于此原因，本节仅提供简要介绍。完整手册可以在 http://www.cis.upenn.edu/~bcpier/unison/ 以及 SuSE 的 unison 软件包中获得。

### CVS 简介

#### 用途

如果频繁编辑单个文件并以松散的文件格式（如 ASCII 文本或程序文本）存储，则 CVS 适用于同步。使用 CVS 进行同步需要一条注释。如果没有定义编辑器，CVS 会启动一个编辑器（环境变量中定义的编辑器）。可以通过在命令行上输入注释来跳过编辑器，例如所示：

```
cvs import -m 'this is a test' synrome newbie_0
```

## 配置 CVS 服务器

“服务器”是文件所在的地方。在配置服务器时，最好设置以下环境变量：

```
CVS_RSH=ssh CVS_ROOT=newbie@server
```

可能会用 C 标记出冲突。在这种情况下，请查看文件中的冲突标记（`»`）和 `<`），并在两个版本之间做出选择。由于这件工作可能相当不愉快，你可能会决定放弃更改、删除本地文件，并进入 CVS 以从服务器检索当前版本。

## 更多信息

本节仅对 CVS 的许多可能性提供简要介绍。可以通过以下 URL 获取详尽的文档：

```
http://www.cvshome.org/
http://www.gnu.org/manual/
```

### mailsync 简介

#### 用途

`mailsync` 主要适用于以下三个任务：

- 本地存储的电子邮件与存储在服务器上的电子邮件同步
- 将邮箱迁移到不同的格式或不同的服务器
- 邮箱的完整性检查或搜索重复项

## 配置与使用

`mailsync` 区分邮箱本身（“存储”，`store`）与两个邮箱之间的连接（“通道”，`channel`）。存储和通道的定义存储在 `~/.mailsync` 中。接下来的段落解释了若干存储示例。

简单的定义可能如下：

```
store saved-messages {
  pat Mail/saved-messages
  prefix Mail/
}
```

`Mail/` 是用户主目录下的子目录，包含电子邮件文件夹，包括 `saved-messages` 文件夹。如果使用以下命令启动 `mailsync`：

```
mailsync -m saved-messages
```

`saved-messages` 将列出所有消息索引。如果做了以下定义：

```
store localdir {
  pat Mail/
  prefix Mail/
}
```

则命令 `mailsync -m localdir` 将导致存储在 `Mail/` 下的所有消息列出来。相比之下，命令 `mailsync localdir` 将列出文件夹名称。IMAP 服务器上存储的规范如下：

```
store imapinbox {
  server {mail.edu.harvard.com/user=gulliver}
  ref {mail.edu.harvard.com}
  pat INBOX
}
```

上面的示例仅处理了 IMAP 服务器上的主文件夹。对于子文件夹，显示方式如下所示：

```
store imapdir {
  server {mail.edu.harvard.com/user=gulliver}
  ref {mail.edu.harvard.com}
  pat INBOX.*
  prefix INBOX.
}
```

如果 IMAP 服务器支持加密连接，则应将服务器规范更改为：

```
server {mail.edu.harvard.com/ssl/user=gulliver}
```

或者，如果服务器证书未知：

```
server {mail.edu.harvard.com/ssl/novalidate-cert/user=gulliver}
```

前缀稍后会解释。

现在，`Mail/` 下的文件夹应该连接到 IMAP 服务器的子目录：

```
channel folder localdir imapdir {
  msinfo .mailsync.info
}
```

`mailsync` 使用 `msinfo` 文件来跟踪已经同步的消息。

命令 `mailsync folder` 执行以下操作：

- 在两端扩展邮箱模式
- 从结果文件夹名称中删除前缀
- 成对对文件夹进行同步（如果它们不存在则创建）

因此，IMAP 服务器上的文件夹 `INBOX.sent-mail` 将与本地文件夹 `Mail/sent-mail` 同步（前提是上述定义存在）。各个文件夹之间的同步按如下方式进行：

- 如果消息在双方都已存在，则什么都不发生
- 如果消息在某一方侧缺失且是新的（未列在 `msinfo` 文件中），则将将其传输到那里
- 如果消息仅存在于一方且是旧的（已列在 `msinfo` 文件中），则将从那里删除（因为另一侧的消息显然已被删除）

若要预先知道在同步期间哪些消息将被传输，哪些将被删除，请带通道和存储启动 `mailsync`：

```
mailsync folder localdir
```

此命令产生一个本地主机上所有新消息的列表，以及一个在同步期间将在 IMAP 侧被删除的所有消息列表。同样，命令

```
mailsync folder imapdir
```

产生一个 IMAP 侧所有新消息的列表，以及一个在同步期间将在本地主机被删除的所有消息列表。

### 可能的问题

在发生数据丢失的情况下，最安全的方法是 `netinfo`。网络上的任何机器都可以预留任意数量的名称，只要这些名称未被使用。NetBIOS 接口现在可以在不同的网络架构实现。与网络硬件工作得较紧密的实现被称为 `NetBEUI`，但它通常被称为 `NetBIOS`。通过 `NetBIOS` 实现的网络协议是 Novell 之 IPX（通过 TCP/IP 的 NetBIOS）和 TCP/IP。

通过 TCP/IP 使用的 NetBIOS 名称与 `/etc/hosts` 中的名称或由 DNS 定义的名称没有任何共同点。NetBIOS 使用它自己的、完全独立的命名规范。然而，建议使用与 DNS 主机对应的名称以便简化管理。这是 Samba 使用的默认值。

## 更多信息

`/share/doc/packages/mailsync` 中的 README 提供了额外信息。对此，RFC 2076 值得关注。

## 异构网络

除了连接到其他系统外，Linux 还能连接到 Windows 和 Macintosh 计算机。本章展示了异构网络的要求和配置。

- Samba . . . . . . . . . . . . . . . . . . . . . . . . . 400
- Netatalk . . . . . . . . . . . . . . . . . . . . . . . . . . . 408
- Netware Emulation with MARSNWE . . . . . . . . . . . . . . . . . . . . . 415

## Samba

通过 Samba 程序，可以将 UNIX 机器转换为 DOS、Windows 和 OS/2 的文件和打印服务器。Samba 项目由 Samba 团队运行，最初由 Andrew Ridgell 开发。

Samba 现在已成为一个成熟且相当复杂的产品。本节介绍了其基本功能的概述。Samba 提供了大量的在线文档。在命令行中输入 `apropos samba` 可以显示某些帮助页面，或者如果安装了 Samba，只需浏览 `/share/doc/packages/samba` 目录。在示例子目录下可以找到一个带注释的配置示例 (`smb.conf.SUSE`)。

Samba 使用基于 NetBIOS 服务的 SMB 协议（服务器消息块）。由于 IBM 的压力，微软发布了该协议，以便其他软件制造商能够建立到微软 域网络的连接。Samba 将 SMB 协议建立在 TCP/IP 协议之上，因此所有客户端也必须安装 TCP/IP 协议。

## 客户端

所有常用的操作系统（如 Mac OS X、Windows 和 OS/2）都支持 SMB 协议。所有计算机必须安装 TCP/IP 协议。

Samba 自 UNIX 版本开始就提供了客户端。对于 Linux，有一个用于 SMB 的文件系统内核模块，允许在 Linux 系统层级集成 SMB 资源。
