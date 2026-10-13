
## 第 12 章：基础系统管理

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_393_0.png)

图 12-3：为新用户输入信息。

> 注意：图 12-3 中的“为用户创建私有组”（Create a private group for the user）复选框默认勾选的，这意味着每个新用户都在一个独立的私有用户组中。然而，有时你希望用户位于某个特定的组中，以便用户访问该组创建的文件。将用户添加到另一个组非常简单。例如，假设我想将用户名 `naba` 的用户添加到名为 `wheel` 的组中，我只需在终端窗口中输入以下命令即可：

```
usermod -G wheel naba
```

如果你只是取消勾选“为用户创建私有组”复选框（见图 12-3），新用户将被分配到名为 `users` 的组。输入 `more /etc/group` 来查看组名和组 ID。

## 使用命令管理用户账户

如果你在测试控制台上操作，可以使用 `useradd` 命令创建新用户账户。按照以下步骤为新用户添加账户：

- 1. 以 root 身份登录。（如果尚未以 root 身份登录，输入 `su -` 成为 root）。
- 2. 输入带有 `-c` 选项的 `useradd` 命令来创建账户：`/usr/sbin/useradd -c "Ashley Barkarkati" ashley`
- 3. 使用 `passwd` 命令设置 Ashley 的密码，如下：`passwd ashley`

正在更改用户 `ashley` 的密码。

新 UNIX 密码：（输入密码并按回车）。

再次输入新 UNIX 密码：（再次输入密码并按回车）。

`passwd: 所有身份验证令牌已成功更新。`

请注意，如果你输入的密码容易被别人猜到，密码程序将拒绝它。

## 第二部分：探索 Linux

`useradd` 命令会查询 `/etc/default/useradd` 和 `/etc/login.defs` 以获取新用户账户各种参数的默认信息。例如，`/etc/default/useradd` 文件指定了默认 shell（`/bin/bash`）和默认主目录位置（`/home`）。`/etc/login.defs` 提供了自动组和用户 ID 的系统默认值，以及密码过期参数。

你可以使用 `userdel` 命令删除用户账户。在命令提示符处输入 `userdel username` 即可删除用户账户。要同时删除该用户的主目录，请输入 `userdel -r username`。

要修改用户账户中的任何信息，请使用 `usermod` 命令。例如，如果我想让我的用户名 `naba` 的用户以 root 作为主组，我将输入：

`usermod -g root`

要了解更多关于 `useradd` 和 `userdel` 命令的信息，请在终端窗口中输入 `man useradd` 和 `man userdel`。

## 理解 `/etc/passwd` 文件

`/etc/passwd` 文件是所有用户账户的列表。它是一个文本文件，任何用户都可以读取；不需要特殊权限。`/etc/passwd` 中的每行都有七个字段，用冒号（`:`）分隔。

以下是 `/etc/passwd` 中的一个典型条目：

```
naba:x:500:10:Naba Barkakati:/home/naba:/bin/bash
```

图 12-4 使用这个典型条目来解释七个字段的含义。

![](img/3b3329dddbc9c0857ad4f2ef1c0db305_394_0.png)

如示例所示，`/etc/passwd` 中每行的格式如下：
