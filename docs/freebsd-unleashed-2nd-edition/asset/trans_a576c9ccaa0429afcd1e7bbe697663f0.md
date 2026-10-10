
## **清单 9.2 续**

```
your account ''joe'' was created.
Have fun!

See also chpass(1), finger(1), passwd(1)

Add anything to default message (y/n) [n]:
Send message (y/n) [y]: Copy files from /usr/share/skel to /home/joe
Add another user? (y/n) [y]: n
Goodbye!
```

在每个提示符后按 Enter 键即接受默认值，该值显示在方括号中。许多提示符会提供以空格分隔的选项列表，例如 shell 的提示符。当这些选项包含 *no* 时，可以使用该选项来禁用或拒绝提示符提供的任何内容。例如，在 shell 提示符输入 *no* 会创建一个没有有效 shell 的用户，这意味着该用户无法登录系统。

> **注意**
> 从 FreeBSD 4.0 及以后版本开始，基础系统中内置的 "csh" 实际上是 tcsh，它是 csh（C shell）的扩展版本。你仍然可以指定 tcsh 作为 shell，但它与 csh 是同一回事。

如果你愿意，可以将一个文件放在 `/etc/adduser.message`，该文件会通过电子邮件发送给新的本地账户用户。用户首次登录系统并运行邮件程序时即可读取该文件（有关阅读邮件的更多信息见第 24 章“配置电子邮件服务”）。为了更便捷，如果你选择发送 adduser.message 文件，脚本会提示你输入第二个发送地址（例如该人员正在使用的其他地址），以确保用户能够收到该信息。

脚本中提到的“dotfiles”是指半隐藏的 shell 配置文件（仅在使用 ls 命令的 -a 选项时才可见）：

- `.cshrc`
- `.login_conf`
- `.mailrc`
- `.rhosts`
- `.login`
- `.mail_aliases`
- `.profile`
- `.shrc`

这些文件在第 11 章“定制 Shell”中题为“Shell 初始化文件”的章节中有更详细的说明。

每个用户和组都有一个与其名称对应的数字等效值，即用户 ID（UID）和组 ID（GID）。此 ID 列在文件或目录的所有权信息中，并用于控制进程。如果你从系统中移除某个用户，该用户的文件将由该用户留下的 UID 编号拥有。

移除用户是一件相当简单的事。这里使用的命令是 `rmuser`，它接受用户名作为参数（adduser 则不需要），如清单 9.3 所示。

## 清单 9.3 rmuser 会话示例

```
# rmuser joe
Matching password entry:

joe:IR8pIrE/nkDQo::1008:1008::0:0:Joe user:/home/joe:/bin/csh

Is this the entry you wish to remove? y
Remove user's home directory (/home/joe)? y
Updating password file, updating databases. done.
Updating group file: (removing group joe -- personal group is empty) done.
Removing user's home directory (/home/joe): done.
Removing files belonging to joe from /tmp: done.
Removing files belonging to joe from /var/tmp: done.
Removing files belonging to joe from /var/tmp/vi.recover: done.
```

关于“匹配密码条目”的那行描述存放所有用户信息的数据库，这引出了我们的下一个主题。

## `/etc/passwd` 和 `/etc/master.passwd` 文件

所有 Unix 风格的操作系统都有 `/etc/passwd` 文件，但该文件的具体角色因平台而异。在某些系统中，`/etc/passwd` 是用户信息（包括密码）的唯一存储库。在这种情况下，添加用户只需使用文本编辑器（`vi`、`pico`、`ex`、`emacs` 等）向文件中添加一行即可。然而，更现代的操作系统使用“shadow passwords”结构——一种将加密后的密码字符串存储在 `/etc/passwd` 之外的方法，而是存储在另一个仅 root 可读的文件中。该文件的名称因平台而异。在某些平台上，它是 `/etc/shadow`；在其他平台上，它是 `/etc/security/master.passwd`。在 FreeBSD 中，它是 `/etc/master.passwd`。

这两个 passwd 文件都是简单的文本数据库，每个用户一行，字段以冒号 (:) 分隔。文件包含用户名、用户 ID、主组的组 ID、主目录、登录 shell 以及全名（全名中还嵌有以逗号分隔的字段，如办公地点、办公电话和住宅电话）。

`/etc/passwd` 的权限是 `0644`；`/etc/master.passwd` 的权限是 `0600`。这种安全机制意味着任何用户都可以访问 `/etc/passwd` 中的信息，但只有 root 可以查看 `/etc/master.passwd`。`/etc/master.passwd` 与 `/etc/passwd` 的唯一区别在于，它的第二个字段包含用户的加密密码。FreeBSD 使用基于 MD5 算法的哈希方案对密码进行加密。以下是各自的示例：

`/etc/passwd:`
```
joe:*:1008:1008:Joe User:/home/joe:/bin/csh
```

`/etc/master.passwd:`
```
joe:$1$32i2knXsSTnjUWjj9LzYgWfRZOnOu/10:1008:1008:Joe User:/home/joe:/bin/csh
```

不过，这两个文件并非存储用户信息的唯一文件。对于数量较少的用户，平面文本数据库就足够了，但随着用户基数的增长，对基于哈希表的更快查找数据库的需求变得越来越明显。在拥有 25,000 个用户的线性文本数据库系统中，查找用户信息可能需要大量时间——而此时用户正等待登录！

因此，FreeBSD 还有 `/etc/pwd.db` 和 `/etc/spwd.db`。这些文件是 db 格式的哈希表，分别对应“非安全的” `/etc/passwd` 和“安全的” `/etc/master.passwd`。它们也具有与其对应的纯文本文件相同的权限。这些文件为大型用户数据库提供了快速查找机制，并且每次使用 `chfn`、`passwd` 或 `adduser`/`rmuser` 命令修改用户信息时，都会由 `pwd_mkdb` 程序自动生成。

说到这个，`chfn`（change full name）命令是用于修改用户信息的工具。与我们上一章中研究的 `edquota` 命令类似，`chfn` 通过调用 `EDITOR` 环境变量中指定的编辑器来运行（默认为 `vi`）。然后你可以修改任何文本字段。保存并退出后，`/etc/master.passwd` 文件会被重写，并自动运行 `pwd_mkdb -p` 以重建其他三个文件。

理解 `/etc/master.passwd` 是真正的“master”用户数据库文件非常重要。如果你想重建用户列表或将用户列表从另一台 FreeBSD 机器移植过来，只需将新的 master.passwd 文件放入 /etc（或 / 分区内的任何位置），然后发出以下命令：

```
# pwd_mkdb -p /etc/master.passwd.new
```

此示例假设你的新 master.passwd 文件位于 /etc 中，名为 master.passwd.new。`/etc/master.passwd` 文件将被你的新文件替换，并且 `/etc/pwd.db`、`/etc/spwd.db` 和 `/etc/passwd` 会被重建。-p 选项告诉 `pwd_mkdb` 生成新的 `/etc/passwd` 文件；如果省略此选项，则 `/etc/passwd` 保持不变。你最好始终使用 -p 选项以保持这两个文件同步。

> **注意**
> 在 FreeBSD 中，`/etc/passwd` 文件本身从未被查询；它的存在主要是为了与第三方应用程序兼容。大多数现代实用程序从 `/etc/pwd.db` 中查找用户信息。

## `/etc/group` 文件

组的处理方式与用户非常相似——在 `/etc` 中有一个文本数据库。但由于组通常没有密码，因此 `/etc/group` 文件（`/etc/passwd` 的组等价物）无需特殊的安全保护，只需确保只有 root 可以写入即可。

以下是来自 `/etc/group` 的示例行。注意只有四个字段：组名、“dummy”字段（如果存在密码，则会放置在此处）、组 ID，然后是组内用户的逗号分隔列表：

```
wheel:*:10:root,bob,frank
```

`/etc/group` 没有哈希数据库，因为该文件的信息通常比 `/etc/passwd` 中的信息引用频率低得多，而且大多数系统的组数远少于用户数。不过，FreeBSD 的“唯一组”策略使后者变得无关紧要。未来的开发可能会为组生成哈希文件。

## 管理组

在没有密码、用户访问权限和哈希文件需要担心的情况下，向系统添加组比添加用户容易得多。你可以简单地在任何文本编辑器中打开 `/etc/group` 文件，并按照前面列出的格式创建新的一行（确保为新组指定一个尚未使用的组 ID）。

当 `adduser` 脚本创建唯一的每用户组时，新组会自动添加。组 ID 通常与对应的用户 ID 匹配，但这并非必需。你通常只关心添加系统范围的组——例如，用于运行 Web 服务器或数据库后端等任务。这些组通常应具有 100 到 1000 范围内的组 ID。1000 以上的数字通常用于唯一的每用户组，以匹配对应的用户 ID。100 以下的数字通常由操作系统核心部分的系统组占用。

要将用户添加到组中，只需将用户名输入到第四个字段中。如果第四个字段中已经有用户名，请像前面所示那样用逗号将它们分隔开。移除用户也很容易——只需删除该名称即可。

![](img/48eec858cce7dfb89da36a4d40b7daf3_244_0.png)

