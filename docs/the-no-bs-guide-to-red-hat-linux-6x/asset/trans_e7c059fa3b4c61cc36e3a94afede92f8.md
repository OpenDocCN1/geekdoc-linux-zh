
here). 来自邮件列表管理器或垃圾邮件发送者的邮件通常会有通用的（或虚假的）收件人地址。

与邮件不同，Pine 不会把收件邮件和已读邮件完全分开存放。所有邮件都会显示在这块屏幕上，无论它们是全新还是六个月前的。

```
PINE 4.10 MESSAGE INDEX          Folder: INBOX Message 1 of 3

+ A 1  Feb  8  Joe Kramer        (1,116) Let's do lunch
N 2   Feb 10  Dave Rhodes        (7,264) MAKE MONEY FAST!!!
+ N 3  Feb 11  davey@surfer.com  (1,220) My new Toyota...

[Folder "INBOX" opened with 3 messages]

? Help    < FldList   P PrevMsg   - PrevPage   D Delete   R Reply
O OTHER CMDS > [ViewMsg]   N NextMsg   Spc NextPage   U Undelete   F Forward
```

## 使用 PINE 管理邮件

你可以通过在查看 FOLDER INDEX 屏幕时按下 > 或 ENTER 键来显示当前邮件（该邮件要么有下划线，要么为反显）。下面是你在 Pine 中查看邮件时的示例：

```
PINE 4.10 MESSAGE TEXT          Folder: INBOX Message 1 of 3  ALL

Date: Sat, 8 Feb 1997 13:57:22 -0800
From: Joe Kramer <JoeK@asdf.com>
To: hermie@fritz.com
Subject: Let's do lunch

Hey, howzabout we do a "power lunch" on Monday to work out the details of that Amorphous contract? Call me at 555-0317...

? Help    < MsgIndex   P PrevMsg   - PrevPage   D Delete   R Reply
O OTHER CMDS > ViewAttch   N NextMsg   Spc NextPage   U Undelete   F Forward
```

从 MESSAGE TEXT 屏幕或 FOLDER INDEX 屏幕，你可以按下以下其中一个键来对当前邮件进行操作。 （Pine 在输入命令时不区分大小写。）

- **R** 回复当前邮件。
- **D** 删除邮件。 （当你要求删除邮件时，邮件实际上并不会消失——它们只是被标记为 D，并在你退出 Pine 时稍后被清除，以防你改变主意不想删除邮件。）
- **U** 恢复邮件（移除 D 标记）。

如果你按下 O 来显示更多 Pine 命令，屏幕底部的图例将更改为以下内容：

```
? Help    M Main Menu    L ListFldrs    C Compose    % Print    S Save
O OTHER CMDS    Q Quit Pine    G GotoFld    W whereIs    T TakeAddr    E Export
```

从这里，你可以使用以下功能：

- **C** 撰写新邮件。
- **<** 返回 FOLDER INDEX 屏幕。
- **W** 在当前邮件中搜索文本。
- **%** 打印邮件。
- **T** 将发件人添加到你的地址簿。
- **S** 将邮件保存在文件夹中。

## PINE 邮件文件夹

文件夹对于组织邮件很有用。当你按下 S 将邮件保存在文件夹中时，Pine 会要求你选择一个文件夹。如果该文件夹已存在，Pine 会将邮件复制到该文件夹，并在你的收件箱中将其标记为“已删除”。如果文件夹不存在，Pine 会询问你是否要创建它。

你可能希望将来自邮件列表的所有邮件保存在与列表同名的文件夹中，或创建一个名为 URGENT 的文件夹用于高优先级项目。我为我经常通信的人创建文件夹，这样我的收件箱保持整洁，我在需要时仍能找到旧邮件。

你可以使用 L 命令显示所有文件夹的列表，然后查看所选文件夹中的邮件。无论是处理 INBOX 文件夹还是你创建的其他文件夹，都使用相同的 FOLDER INDEX 和 MESSAGE TEXT 屏幕。

## 面向高级用户的 PINE

Pine 是管理邮件的绝佳工具，因为它速度快、易于学习且易于配置。但它也为高级用户提供了许多高级功能。一旦你熟练掌握了基本邮件处理，请尝试以下功能。 （所有功能均可从 FOLDER INDEX 屏幕访问。）

### 搜索

使用 W（“where is”）命令在 FOLDER INDEX 屏幕中搜索主题行中包含特定单词的邮件。你也可以在查看邮件时使用 W 命令在邮件正文中搜索文本。

### 排序

使用 $ 命令以多种方式对邮件进行排序，包括按主题、发件人、大小和到达时间。

### 地址簿

使用 T 命令“获取”发件人的地址并将其存储在 Pine 地址簿中。你还可以为地址分配昵称，并在撰写新邮件时使用昵称代替完整地址。

### 邮件头

使用 H 命令查看通常隐藏的邮件头行。乍一看，这是一堆乱码，但 Received 行会告诉你邮件到达你的系统所经过的路径。这对于识别伪造的发件人地址很有用。再次按下 H 可关闭邮件头行的显示。
