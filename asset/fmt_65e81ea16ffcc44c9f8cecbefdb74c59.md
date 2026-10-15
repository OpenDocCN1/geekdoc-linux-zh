
```
-rw-r--r-- 1 root root       49 Nov 25 1997 .bash_logout
-rw-r--r-- 1 root root       49 Nov 25 1997 .bashrc
-rw-r--r-- 1 root root       49 Nov 25 1997 .bashprofile
-rw-r--r-- 1 root root       49 Nov 25 1997 .bashhistory
-rw-r--r-- 1 root root       49 Nov 25 1997 .vimrc
-rw-r--r-- 1 root root       49 Nov 25 1997 .profile
```

# 基础 Linux 系统管理 第4 章

## adduser

安全历史：版本 1.0（随 Red Hat 2.0 发布）包含一个缺陷算法，在某些情况下会错误地分配等同于 root 的 UID。如果你不幸地拥有 1.0 版本，请进行升级。更多信息请参阅《Linux 安全 FAQ 更新》（1995年10月17日），或访问 http://temp.redhat.com/linux-info/security/linux-security/1995-October/0020.html。

要使用 `adduser`，请执行 `adduser` 命令加上用户名：

```bash
$ adduser Nicole
```

```text
作为响应，adduser 执行了除设置密码以外的所有操作：
正在查找第一个可用的 UID... 508
正在查找第一个可用的 GID... 509
添加用户：Nicole...完成。
创建家目录：/home/Nicole...完成。
创建邮箱：/var/spool/mail/Nicole...完成。
不要忘记设置密码。
```

要设置密码，请运行 `passwd` 命令加上用户名。例如，在这种情况下，命令为：

```bash
$ passwd nicole
```

```text
作为响应，Linux 要求输入密码并确认：

输入新的 Unix 密码：
输入新的 Unix 密码：
```

`adduser` 会自动分配值，包括 UID 和 GID。如果你想要获得更精确的命令行控制，如果已安装了 Shadow Suite，请尝试使用 `useradd`。

# 4

> 注意
>
> Shadow Suite 是一套用于影子处理你的 `passwd` 文件的工具集。Linux 将所有用户信息（包括加密密码）都存储在 `/etc/passwd` 中。这是不安全的，因为它会将加密密码暴露给普通用户（`passwd` 必须是可读的）。在进行影子处理时，Linux 将密码存储在其他地方，并在 `/etc/passwd` 中留一个令牌。更多信息请参见第 5 章。

基础 Linux 系统管理

## 通过手动编辑 /etc/passwd 添加用户

你也可以通过手动编辑 `/etc/passwd` 来添加用户。为此有一个专门的工具：`vipw`。

## vipw

当你手动编辑 `/etc/passwd` 时，请使用 `vipw`（vi passwd 的缩写）。`vipw` 在编辑期间锁定密码文件，确保更改被安全地追加。`vipw` 的默认编辑器是 `vi`。表 4.2 描述了如何在 `vi` 中移动。

### 表 4.2 重要的 vipw 按键命令

| 命令 | 结果 |
| :--- | :--- |
| a | 告诉 `vi` 在光标后开始追加文本。在首次启动 `vipw` 时执行此命令。如果不执行，文本将一直出现直到你按下小写的 "a" 键。 |
| Ctrl+b | 一次向上滚动一页。 |
| Ctrl+f | 向向下一页。 |
| d | 按一次，删除一个字符或操作符；按两次，删除整行。 |
| D | 删除整行。 |
| I | 初始化插入模式，就像在 ed 中一样。 |
| x | 通知 `vi` 删除当前字符。 |
| X | 通知 `vi` 删除光标前的前一个字符。 |
| w | 允许你在单词之间跳转。 |
| w: | 将更改写入当前文件。 |
| Shift+p | 粘贴文本。 |
| Shift+h | 将光标置于文件开头（类似于文字处理器中使用的 Home 键）。 |
| Shift+l | 带你去文件的最后一行。 |
| w: filename | 将更改保存到新文件。 |
| :wq | 保存并退出命令。完成编辑后，按下 Esc 键并执行此命令，`vi` 将保存你的工作并返回 shell。 |

`vi` 屏幕被分为两个部分或区域。工作区域（你输入和编辑文本的地方）占据屏幕的 90%。相比之下，状态行（报告统计信息和回显命令的地方）是屏幕底部的单行。

当 `vi` 首次加载时，它进入命令模式。在命令模式下，`vi` 可以识别大量执行搜索、剪切、粘贴、删除和插入的命令。要在命令模式和编辑模式之间切换，请按 Esc 键。

# 基础 Linux 系统管理 第4 章 95

## 警告

如果你是 Linux 新手，在用 `vipw` 编辑 `/etc/passwd` 之前，尝试先用 `vi` 编辑一个丢弃或练习文件。原因如下：如果你犯了错并提交到 `/etc/passwd`，可能会发生可怕的事情。之一是 Linux 可能会拒绝你的登录。

如果你觉得使用很困难，可以更改 `vipw` 的默认编辑器。例如，也许你想用 `pico`。它友好得多，行为像 DOS 风格的编辑器。如果是这样，请更改你的 `EDITOR` 变量。在 C shell 中，执行此命令：

```bash
$ setenv EDITOR pico
```

这会将你的编辑器设置为 `pico`。现在，当你调用 `vipw` 时，它将使用 `pico`。若要在 bash 中将 `pico` 设置为默认编辑器，请执行此命令：

```bash
$ export EDITOR=pico
```

## 注意

根据你选择的安装类型，`pico` 可能已也可能未安装。它是 `pine` 邮件客户端包的一部分。

## 使用自己的工具添加用户

如果你很有野心，可以编写自己的用于账户创建和管理的工具。（许多人都这样做。）但是，除非你有丰富的 Linux 经验，否则我不建议这样做。

无论你的自制工具是前端（shell、Perl 或其他），

## 删除用户

如果你需要删除用户，请使用 `userdel` 命令。该命令从系统中删除用户。但是，它不会删除用户的家目录。若要同时删除家目录，请使用 `-r` 标记：

```bash
$ userdel -r username
```

## 管理任务

如果你需要更改用户信息，请使用 `usermod` 命令。例如，更改用户的主组：

```bash
$ usermod -g newgroup username
```

## 安全基础

如果你需要锁定用户账户，请使用 `passwd` 命令配合 `-l` 标记：

```bash
$ passwd -l username
```

要解锁账户，请使用 `-u` 标记：

```bash
$ passwd -u username
```

`sudo` 要求输入密码。如果用户提供了正确的密码，即可进入。否则，`sudo` 会记录该访问尝试。

> 注意
>
> `nsudo` 用户也可以指定一个要执行的命令。

`sudo` 允许你严格限制哪些用户可以调用它以及他们可以执行哪些命令。你可以在 `/etc/sudoers` 中指定这些设置。

`/etc/sudoers`

`/etc/sudoers` 的结构由多个部分组成：

- *`sudo` 用户可以运行的命令。*
- 主机别名（Host aliases），包括主机、网络组（netgroups）、IP 地址和网络（如果有）。
- 用户别名（User aliases）（如果有）。
- 用户规范，包括主机类型、主机 IP、授权用户列表，以及他们以什么种身份运行（通常是 root）。

列表用逗号分隔。这里有一个带有占位符的精简示例。
