

# 《Linux  cookbook：日常使用的技巧与技术》：

连接到它，它可以被不同的人在不同时间共享，使得用户工作区的分离仍然是一个有效的问题。

这种分离是通过为每个个人用户在系统上分配一个*账户*来实现的。你需要一个账户才能使用系统；有了账户，你将获得一个单独的工作区供使用，以及一个唯一的*用户名*来标识你自己给系统和其他人。它是系统（以及使用它的人）将永远认识你的名字；它是一个单词，全为小写字母。

在安装过程中，系统管理员应该为你创建了一个账户。（系统管理员有一个特殊的账户，其用户名为 `root`；该账户可以完全访问整个系统，因此通常被称为 *超级用户*。）

直到 1990 年代中期，用户名通常由你的名字首字母加上你的全姓组成，总共不超过 12 个字符。例如，按照这种约定，用户 Samuel Clemens 的用户名将是 sclemens；然而，这并不是硬性规定，尤其是在家庭系统上，你可能是唯一的系统用户。有时可能会使用中间名首字母（`djkohnson`），有时甚至使用昵称或首字母（`zenboy`，`xibo`）。但无论你为自己选择什么用户名，请确保这是你能接受的，并且你能忍受系统和其他用户这样称呼你（你的用户名也将成为你的电子邮件地址的一部分，如我们在 [Email](#) 中将看到的）。

除了用户名之外，你还应该有一个*密码*，你可以保密以便只有你能使用你的账户。好的密码是别人不太可能猜到的文本字符串（即不是像 `secret` 这样明显的词，或像 `Ruski` 这样具有识别性的名字，如果那恰好是你的宠物猫的名字）。好的密码是你自己非常容易记住的，这样你就不必写下来，但在构造上足够复杂，以至于其他人永远无法猜到。例如，`t39sAH` 可能是一个不错的密码，对于某个人来说，他的第一次约会是去看阿尔弗雷德·希区柯克执导的电影 *《第三十九级台阶》*。

**NOTE：** 虽然用户名始终为小写，但密码区分大小写；密码 `Secret`、`secret` 和 `SECRET` 都被视为不同。

- [3.2.1 Logging In to the System](#) — How to log in to the system.
- [3.2.2 Logging Out of the System](#) — How to log out of the system.

![](img/8bf3d083d04b4cc3d79bd39657ac711a_37_0.png)

+ [<] [>] [<<] [Up] [>>] [Top] [Contents] [Index] [?]

## 3.2.1 Logging In to the System

要开始在 Linux 系统上的会话，你需要 *登录*。在终端的 `login:` 提示符下输入你的用户名，然后在被要求时输入你的密码即可完成此操作。

系统启动后，`login:` 提示符会出现在终端上。如果你的系统配置为在启动时启动 X Window System，你将看到 X 登录屏幕而不是标准的登录提示。如果发生这种情况，请按 **CTRL–ALT–F1** 切换到文本登录屏幕；这在 [Console Basics](#) 中有进一步解释。

典型的 `login:` 提示符如下所示：

```
Debian GNU/Linux 2.2 bardo tty1

bardo login:
```

每个 Linux 系统都有自己的名称，称为系统的 *主机名*；Linux 系统有时被称为 *主机*，它在 `login:` 提示符处用其主机名标识自己。给你的系统命名很重要——与用户账户的用户名不同，主机会为你使用的系统命名（当将系统放到网络上时它变得尤其重要）。系统管理员通常在系统初始配置时为系统命名（主机名可以随时更改；其名称保存在文件 `/etc/hostname` 中）。与用户名一样，主主机名是一个全小写字母的单词。人们通常会给他们的系统起一个他们喜欢的名字，例如 `darkstar` 或 `shiva`。

在此示例中，`bardo` 是此特定 Linux 系统的主机名。

你连接的终端的名称显示在主机名之后。在此示例中，终端是 `tty1`，这意味着这是该特定系统的第一个终端。（顺便说一下，`tty` 是 “teletype” 的缩写，历史上这是大多数基于 Unix 的系统默认使用的终端硬件类型。）

要登录系统，请在 `login:` 提示符下输入你的用户名（后跟 **RET**），然后在被要求时输入你的密码（也后跟 **RET**）；出于安全原因，输入密码时屏幕上不会显示。

- 要使用用户名为 `kurt` 且密码为 `empathy` 登录系统，请输入：

```
Debian GNU/Linux 2.2 bardo tty1

bardo login: kurt RET
Password: empathy RET
Linux bardo 2.0.30 #1 Tue Jul 29 10:01:26 EDT 1997 i586 unknown

Copyright (C) 1993-1998 Software in the Public Interest, and others

Most of the programs included with the Debian Linux system are
freely redistributable; the exact distribution terms for each
program are described in the individual files in
/usr/doc/*/copyright

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Apr  5 12:03:47 on tty1.
No mail.
~ $ 
```

一旦你输入了用户名和密码，你就“登录”到系统了。你可以随后使用系统并运行命令。

一旦你登录，系统会显示 `/etc/motd` 的内容，即“每日消息”文件。然后系统会显示你上次登录的时间和日期，并报告你是否有电子

