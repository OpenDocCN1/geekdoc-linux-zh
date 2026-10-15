
mailx `[-dinVF] [-h number] [-r address] [-s subject] user ...`

Mail `[-dinVF] [-h number] [-r address] [-s subject] user ...`

下面的邮件会话显示了如何向三个用户系统 jar、kls 和 sjg 发送消息，并向 ske 发送抄送。

### 示例 1-3：发送邮件

```
$ mailx jar kls sjg
Subject: Book Modification <Return>
We need to get together sometime very soon to discuss the modifications necessary if the book is going to be published.
I sent a copy to the publishers last week to see if they are at all interested, but obviously we have to make a lot of changes to make it conform somewhat to industry standards. How's Friday at 2 pm for a meeting:
<Return>
<Ctrl/D>
Cc: ske <Return>
$
```

### 尝试一下！

向你自己发送消息：

1. 在系统提示符 (`$`) 下，输入：`mailx username Return`，使用你的用户名。
2. 邮件随后提示 `Subject:`：输入消息的主题并按 Return。
3. 邮件现在正等待你输入消息。输入消息正文，然后按 Return 将光标移到行首。然后按 `Ctrl/D` 结束消息。
4. 如果邮件提示 `Cc:`：输入要发送抄送副本/额外副本的用户名（用逗号或空格分隔），并按 Return。
5. 系统随后提示：`$`。这表示你已成功发送了邮件消息。

## 编辑消息

当您输入邮件正文时，行式编辑器允许您输入消息的每一行。您按 Return 获得新行。要编辑某行，您必须在按 Return 之前进行更改。有高效的方法可以创建和编辑消息，包括：

- 使用 mail 创建文件
- 在 mail 运行期间调用编辑器
- 使用 `~r` 发送文件

### 在发送邮件前创建文件

使用现有文件发送消息：

- 使用文本编辑器创建并编辑文件，输入您想要发送邮件的信息。保存文件。
- 使用 Mail 命令将文件发送到分发列表。

下面的示例显示了向用户 dan、kls、ar 和 rln 发送文档 letter.mail。消息文件 `letter.mail` 是在输入 mail 命令之前使用文本编辑器创建的。注意重定向符号 (`<`)。这表示邮件程序从文件 `letter.mail` 读取输入。

### 示例 11-4：使用 Mail 发送文件

```
$ mailx dan kls ar rln < letter.mail
```

### 在 Mail 中调用编辑器

要在 mail 内部调用编辑器，请在单独的一行输入 `~v` 或 `~e`。

下面的示例显示了如何使用波浪号序列创建消息，当您单独的一行输入 `~v` 时，mail 会调用由环境变量 `VISUAL` 定义的编辑器。

### 示例 11-5：使用 ~v 编辑消息

```
$ mailx smith
Subject: <Return>
~s Send Mail Editing Session
~v
(注意：输入 ~i 会导致 vi 进入插入模式)
这是一个使用 vi 的示例编辑会话。
注意当到达行尾时文本是如何自动换行的。
不要忘记按 Esc 停止编辑。
然后输入 :w 返回到发送邮件会话。
<Esc>
:wq
```

与其他用户通信 11-15

## 介绍邮件实用程序 (CLI)

```
/tmp/Re0120 4 lines, 242 characters
(continue)
<Ctrl/D>
Cc: <Return>
You have new mail.
```

下面的表描述了您用来调用编辑器的波浪号转义序列。

### 表 11-6：在 Mail 中选择您的编辑器

| 波浪号转义序列 | 描述 |
| --- | --- |
| `~e` | 使用由环境变量 `EDITOR` 定义的编辑器。如果未定义 `EDITOR`，默认编辑器是 `ed` 行编辑器。 |
| `~v` | 使用由环境变量 `VISUAL` 定义的编辑器。如果未定义 `VISUAL`，默认是 `vi`。 |

### 现在尝试一下！

1. 在 mail 中通过调用文本编辑器来编辑消息：
2. 输入 mail 命令并提供主题。
3. 在空白行的开头输入 `~e` 或 `~v` 波浪号转义序列来调用编辑器。
4. 按通常方式退出编辑器。

### 需要帮助吗？

如果预期的编辑器没有运行，请检查环境变量 `VISUAL` 和/或 `EDITOR` 的值。

如果文件已存在，可以使用 `~r` 将其读取到消息缓冲区，如下例所示。

### 示例 11-6：使用 ~r 邮件文件

```
$ mailx msg
Subject: Here are the prices! <Return>
~r pricelist.txt <Return>
.
file contents are displayed
.
<Ctrl/D>
Cc: sjk <Return>
$
```

## 波浪号转义序列

下面是其他常用的波浪号转义。

### 表 11-7：波浪号功能

| 选项 | 功能 |
| --- | --- |
| `~b` | 将用户名添加到盲抄 |
| `~c` | 将用户名添加到抄送（Cc）列表 |
| `~p` | 打印包含头信息的消息 |
| `~r` | 将指定的文件读取到消息 |
| `~s` | 使用字符串作为主题 |
| `~t` | 将用户名添加到接收者列表 |
| `~w` | 将消息写入文件 |
| `~!` | 启动 shell 命令 |
| `~?` | 显示波浪号列表 |

### 示例 11-7：发送邮件时使用波浪号

```
$ mailx jls sjg
~s current thoughts on the project
We need to get together soon to discuss the modifications necessary if the book is going to be published. I sent a copy to the publishers last week to see if they are all interested, but obviously we have to make a lot of changes to make it conform somewhat to industry standards. How's Friday at 2 pm for a meeting?
~t pnh
~c ard
~p
Message contains:
To: jls sjg
Subject: current thoughts on the project
(continue)
$ <Ctrl/D
```

### 现在尝试一下！

使用波浪号序列添加主题字段和额外接收者来发送消息：

1. 在系统提示符处，带用户 ID 输入 mailx 命令。
2. 在消息正文的单独行中，输入 `~s` 和主题文本字符串。
3. 在另一个单独行中，输入 `~t` 和用户列表以添加接收者。
4. 在另一个单独行中，输入 `~p` 查看头部和正文。
5. 按 `Ctrl/D` 发送消息。

### 需要帮助吗？

参考 mailx(1) 中的“发送邮件”章节。

## 解决方案

```
$ mailx msg
~s The equipment has arrived!
~t evt tlb
~p
------
Message contains:
To: evt tlb
告诉 Tom 什么时候可以安装驱动器和调制解调器！
.
EOT
```

## 阅读邮件

要阅读邮件，请使用 mail 或 mailx 命令并按 Return，如下所示。

### 示例 11-8：邮件菜单

```
$ mailx
Mail $Revision: 4.2.4 $ Type ? for help.
/usr/spool/mail/self: 3 messages 2 new
U 1 sj Wed Feb 9 13:25 11/295 "Do not forget"
>N 2 dan Wed Feb 9 22:04 11/302 "current thoughts about the book"
N 3 ard Thu Feb 10 06:35 11/273 "pls rspnd asap"
```

在阅读邮件时，屏幕上将显示当前邮件的数量，随后是邮件的提示符。

## 介绍 Mail 实用 (CLI)

Mail 在显示邮件列表时会使用这些符号。

### 表 11-8：Mail 符号

| 符号 | 含义 |
| :--- | :--- |
| `?` | 邮件提示 |
| `N` | 新消息；邮件没有记录你之前查看过该消息 |
| `U` | 未读消息；你在邮件菜单中查看过邮件标头，但当时没有阅读正文 |
| `>` | 指向当前消息；在你调用 mail 之后，`>` 提示将指向列表上的第一条消息 |

要读取特定的邮件消息，请使用此表中的命令。

### 表 11-9：读取邮件命令

| 命令 | 结果 |
| :--- | :--- |
| `<Return>` | 显示当前消息 |
| `p`, `t` | 显示或重新显示当前消息 |
| `n`, `+` | 显示下一条消息 |
| `数字` | 显示之前的指定编号消息 |

## 发送邮件命令

下表包含了发送邮件时需要的大部分命令。

### 表 11-10：发送邮件命令

| 功能 | 命令 | 结果 |
| :--- | :--- | :--- |
| 发送消息 | `m user_list` | 向消息列表 user_list 中的所有用户发送邮件。可以使用 `-f` 转义字符来转发消息。`-f` 转义字符会将指定文件的内容读取到你正在发送的消息中。 |
| | `file#` | 返回到你的邮箱箱。 |
| 保存消息 | `RET`, `s`, `w` | 消息被保存在家目录下的 dropbox 目录文件中。 |
| 回复消息 | `R` | 允许你回复发送消息的用户。消息的主题字段包含你正在回复的消息的主题，并带有 RE: 前缀。你可以像发送邮件时一样使用转义字符。 |
| | `r` | 与 `R` 相同，但会向原始消息的所有收件者以及发送者发送回复。 |

与其他用户通信 11-19

## 介绍 Mail 实用 (CLI)

## 删除邮件

你可以使用 `d` 和 `u` 命令删除消息，并找回误删的消息，如下表所示。

### 表 11-11：删除和取消删除命令

| 命令 | 功能 |
| :--- | :--- |
| `d msg_list` | 删除编号在 msg_list 中的所有消息；如果没有给出列表，则只删除最近读取的一条消息 |
| `u msg_list` | 取消删除编号在 msg_list 中的消息并将其放回你的邮箱箱；只有当前邮件会话中的消息可以取消删除 |

## 退出和帮助命令

Mail 提供以下命令来获取帮助并退出邮件程序。

### 表 11-12：退出和帮助命令

| 功能 | 命令 | 结果 |
| :--- | :--- | :--- |
| 帮助 | `?`, `help` | 显示命令列表及其含义摘要 |
| 退出邮件 | `q` | 退出邮件；对你的邮箱箱进行的所有更改（例如删除）都将最终生效 |
| | `x`, `ex` | 退出邮件并返回到 `$` 提示符；你的邮箱箱将保持邮件会话开始时的状态 |
| 列出邮件变量 | `set` | 列出邮件变量 |

## 自定义 Mail (CLI)

### 概述
你可以通过以下方式自定义你的邮件会话：
- 使用 `.mailrc` 文件来覆盖 mail 的初始配置
- 创建文件夹以组织保存的邮件
- 使用别名来简化邮件分发

### 系统邮件文件 /usr/share/lib/mail.rc
`/usr/share/lib/mail.rc` 文件：
- 包含设置初始邮件配置的命令，适用于所有用户
- 在 mail 实用程序将控制权交给你之前由执行
- 由系统管理员维护
个人用户可以通过更改或增加设置来修改配置。

### 创建 .mailrc 文件
`.mailrc` 文件：
- 必须位于家目录下
- 包含 `set`, `ignore` 命令
如果在登录时没有 `.mailrc` 文件，请使用 `cat` 命令创建一个。
该 `.mailrc` 文件包含以下命令：
- `set ask` 在发送邮件时提示显示主题
- `set askcc` 在发送邮件时提示显示抄件人

#### 示例 11-9：创建 .mailrc

```bash
$ cat > .mailrc
set ask
```

与其他用户通信 11-21

## 自定义 Mail (CLI)

### 选项文件

两种类型的选项：二进制和值。

### 表 11-13：二进制选项 (on or off)

| 选项 | 功能 |
| :--- | :--- |
| `set ask` | mailx 在发送消息时提示主题 |
| `set askcc` | mailx 在发送消息时提示抄件人 |
| `set header` | mailx 在发送消息时提示所有收件者 |
| `set folder` | mailx 将消息包含在指定的邮箱箱中 |

### 表 11-14：值选项 (value)

| 选项 | 功能 |
| :--- | :--- |
| `set header=number` | 指定 mailx 使用的行数 |
| `set EDITOR=pathname` | 指定使用的文本编辑器 |
| `set folder=pathname` | 指定存储邮件的文件夹 |
| `set VISUAL=pathname` | 指定使用的可视化编辑器 |

## 解决方案

+ 1. `$ vi .profile`

```
set ask
set askcc
```

## 文件夹

一旦你开始使用，就会积累很多消息。你可能需要保存它们以便于访问。Mail 提供了一个名为文件夹的简单功能来组织消息。当你第一次将消息保存到文件夹时，mail 会创建该文件夹。

## 解决方案

+ 1. `$ mkdir evt_mail`

## 使用文件夹

在任何需要 mailx 命令期望文件名的地方，都可以使用带加号 (`+`) 的文件夹名。下表显示了处理文件夹的各种命令。

### 表 11-15：使用文件夹

| 操作： | 在提示符处输入 |
| :--- | :--- |
| 选择 folder_name | `folder +folder_name` |
| 选择上一个文件夹 | `folder #` |
| 选择系统邮箱 | `folder %` |
| 选择你的个人邮箱 | `folder &` |
| 确定当前文件夹及其消息数量 | `folder` |
| 显示所有文件夹名称 | `folders` |
| 将当前消息复制到 folder_name | `copy [msg_list] +folder_name` |
| 将当前消息保存到 folder_name | `save [msg_list] +folder_name` |

## 现在尝试！

读取来自 practice 的文件夹中的邮件：

+ 1. 进入 mailx并将邮件保存到 practice 文件夹。Mail 会自动创建该文件夹。
+ 2. 将你收到的邮件复制到 practice 文件夹。
+ 3. 使用退出命令离开 mailx，并使用以下命令重新进入：

```
$ mailx -f +practice
```

这将以 practice 为当前文件夹启动 mailx。

### 需要帮助吗？

查看 mailx(1) 中的示例。

## 解决方案

+ 1. `$ mkdir folder_directory`
2. 编辑你的 `.mailrc` 文件并输入以下行：
   `set folder=folder_directory`
   其中 folder_directory 是你起的名称。
3. 输入 mailx 命令并选择一条新消息。
4. 使用 mailx save 命令将消息保存到文件夹中。
- 4. 使用常规邮件命令读取你在练习文件夹中的消息。

### 需要帮助吗？

查看 mailx(1) 中的示例。

## 解决方案

- 1. `$ mailx`

```
Message 1:
From evt Mon Feb 23 13:09:00 1998
Date: Mon, 23 Feb 1998 13:08:59 -0500
From: Evan Tyler <evt>
Subject: The equipment has arrived!
```

告诉 Tom 他什么时候可以安装驱动器和调制解调器！

- 2. `$ save 1 +practice`
"practice" [新文件] 11/385
- 3. `$ q`
- 4. `$ mailx -f +practice`

```
From evt Mon Feb 23 13:09:00 1998
Received: by loner.decom.com (5.65v3.2/1.1.10.5/23Jan97-07-0140AM)
id AA07212; Mon, 23 Feb 1998 13:08:59 -0500
From: Evan Tyler <evt>
Message-Id: <980231808.AA07212@loner.decom.com>
To: evt msg tlb
Subject: The equipment has arrived!
Status: R
```

告诉 Tom 他什么时候可以安装驱动器和调制解调器！

- `$ q`

## 使用别名 (Aliases)

别名是一个代表一个或多个用户名称，并提供了一种快速方法：
- 向分发列表发送邮件。
