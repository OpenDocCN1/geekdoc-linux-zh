
```
dncompressing the file "pine-4.4.2.tar.gz"
```

*(注：由于原文文本后半部分存在大量重复的乱码字符，根据“一定不要重复输出原文”的原则，译文仅针对具有实际意义的指令进行翻译，乱码部分已忽略或过滤。由于用户提供的文本后半部分包含大量重复和格式错误，我仅对核心逻辑部分进行了翻译。)*

## 从其他服务器获取邮件

你可以使用 `fetchmail` 工具从远程服务器获取邮件。`fetchmail` 是一个取回和转发工具，支持所有从邮件服务器获取邮件的导入协议。这些包括最流行的 `POP3` 和 `IMAP`，以及其他对等协议：`RPOP`、`NNOP`、`AFOP`、`ETR` 和 `OMDAR`。

... 只有个人用户才能读取此文件。事实上，如果该文件的权限未设置为 `710`，`fetchmail` 会向你发出警告。这意味着所有者具有读取、写入和执行权限，而用户组仅具有执行权限，其他人都无法访问该文件。

与许多工具一样，`fetchmail` 使用一个名为 `.fetchmail` 的配置文件来存储你的账户信息。你可以向 `.fetchmail` 文件中添加以下行：

```
poll mail.mailserver.org protocol POP3 user
nick password wormx name john
```

在这个示例中，`nick` 是远程账户的用户名，而 `john` 是本地用户。你检查是否有可下载邮件的服务器被称为 `.mailserver.org`。如你所见，密码是以明文形式显示的。因此，你必须对 `.fetchmail` 文件设置权限，以便

将密码存储在文件中可以避免你每次使用 `fetchmail` 时都输入。这也允许 `fetchmail` 通过 `cron` 自动运行每日或更频繁的下载。

你的系统必须运行 `fetchmail` 才能正常工作。`fetchmail` 的原理是将邮件传输到你本地系统的 smtp 服务器。如果你不发送邮件，可以使用 `.fetchmail` 文件处理入站邮件，将其如下所示：

```
poll mail.mailserver.org protocol POP3 user
nick password wormx name "/usr/bin/fetchmail -d"
```

| 终端 | 文件 | 编辑 | 回滚内容 | 字体 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `[fetchmail:screenshots] user% fetchmail -v --keep -a >> /var/log/fetchmail 2>&1` | | | | | | |
| `[fetchmail]- * /home/users/user $ - user echo '11 23' * * /sw/bin/fetchmail -a >> /var/log/fetchmail 2>&1` | | | | | | |
| `[fetchmail]- * /home/users/user -a grep cron 338 77 Ss R. 0:00:00 grep cron` | | | | | | |
| `[fetchmail]- * /home/users/user exit` | | | | | | |
| `[fetchmail]- * /home/users/user cron 5 18 * */users/user/check_space * /dev/null 11 23 * /sw/bin/fetchmail -a >> /var/log/fetchmail 2>&1` | | | | | | |
| `[fetchmail]- user` | | | | | | |

### 在命令行上使用 FETCHMAIL

- 输入 `fetchmail -v` 后跟一个空格。
- 输入 `-keep -a` 后跟一个空格。
- Fetchmail 从远程服务器下载你的邮件。

### 通过 CRON 运行 FETCHMAIL

- 输入 `crontab -e` 来编辑你的文件。
- 你的 cron 文件打开后，fetchmail 将每晚 11:11 PM 运行。

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_232_0.png)

## 安装 PINE

Pine 是一个基于文本的电子邮件程序，在 UNIX 系统上已使用多年。你可以使用 Fink 或 FinkCommander 在你的 Mac OS 系统上安装 pine。否则，你可以从 https://www.washington.edu/pine 下载 pine。然后你可以按照第 12 章中的描述解压并安装安装文件。

当你第一次运行 pine 时，它会在你的主目录中创建一个名为 `pincerc` 的配置文件。该文件允许你修改许多配置参数，例如你在发送的消息中显示的名称。与大多数 UNIX 配置文件一样，任何以 `#` 开头的行都是注释。

要创建应用程序，你可以使用 `build os`。此命令取代了通常的 `make` 命令，并为你的 Mac OS X 构建一个二进制文件。当过程完成后，你将获得一个包含程序的目录，你可以将其复制到系统上的其他位置。你可以参考 `README` 获取可能你的系统相关的说明。

为了方便使用，请确保它在你的搜索路径中。这允许你通过在命令行输入 `pine` 来启动 pine。你可以通过输入 `pine` 来验证 pine 是否在搜索路径中。此命令会返回 pine 可执行文件的完整路径。

如果你设置邮件服务器，某些与 pine 结合的其他工具非常有用。`imap`、`ipop2` 和 `ipop3` 是允许邮件客户端下载邮件的服务器。这些工具分别支持 IMAP、POP2 和 POP3 协议。

### 使用 PINE 阅读电子邮件

你可以使用 pine 阅读你的电子邮件。在习惯了 pine 的命令以及 pine 组织邮件的方式后，pine 并不困难。要启动 pine，你可以在命令行中输入 `pine`。此时你可以访问你的收件箱、读取和删除消息，以及撰写和发送邮件。

随后，你可以打开收件箱或其他文件夹。使用上方向和向下方向键可以在消息之间移动。按下回车键（Return）可以显示消息。要返回到消息索引，你可以输入字母 `i`。当消息被高亮时，按下字母 `d` 可以将消息标记为待删除。如果你改变了主意，pine 不会删除它，你可以通过回到该消息并输入字母 `u` 来取消删除。

启动 pine 时看到的第一个数据屏幕是一个上级菜单，允许你寻求帮助、编写消息、查看当前文件夹中的消息、列出文件夹、更新地址簿或退出 pine。你可以通过输入单个命令（如输入 `C` 编写消息）来访问这些选项中的。此屏幕被称为主菜单。主菜单的默认焦点是列出你的文件夹：如果你只需按下回车键，pine 会列出

虽然这些单命令菜单起初看起来可能晦懂，但 pine 在屏幕底部提供了常用命令列表。你可以通过一次或多次按下 `<` 键返回主菜单。在主菜单处按下 `?` 键可以帮助。要退出 pine，你可以输入 `q`。

![](img/8d9b2c31cb5ebc6571f0b2dfd7c634cf_235_0.png)

```
[ferro:~) user$ pine
PINE: 4:52  MAIN MENU
? HELP               Get help using pine
C COMPOSE MESSAGE   Compose and send a message
I MESSAGE INDEX     View messages in current folder
L FOLDER LIST       Select a folder to view
A ADDRESS BOOK      Update address book
S SETUP             Configure Pine Options
Q QUIT               Leave the pine program
```

输入 `pine` 并按下回车键。

pine 打开，显示主菜单。

## 安装和使用网络应用程序

## 额外说明

在 pine 中回复消息时，你在消息列表中选择消息或查看消息时，输入 `r`。pine 会将你的回复发送给原始消息的发送者，并询问你是否想在回复中包含原始消息。

你可以通过编辑 `.pinerc` 文件或从主菜单中选择 `SETUP` 来更改 pine 选项。如果你选择 `SETUP`，会出现另一个列表。选择 `C` 将带你进入一个包含多个场景的配置选项列表。尽管这些选项很多，但如果你像大多数用户一样，将保持默认设置。

要将消息移动到不同的文件夹，当 pine 显示消息列表或消息本身时，你可以输入 `s`。然后 pine 会询问你想要放置消息的文件夹名称。它默认为 `saved-messages` 文件夹。

| Terminal | File | Edit | Scrollback | Font | Edit | Scrollback | Font | Window | Help |
|---|---|---|---|---|---|---|---|---|---|
| PINE 4.52 Folder: INBOX Message 12 of 35 NEW | | | | PINE 4.52 MESSAGE TEXT Folder: INBOX Message 12 of 23 ESH | | | | | |
| | | | | | | | | | | |
|---|---|---|---|---|---|---|---|
| 1 May 21 Sandra-Ste | (328) saying hello | | | | | | |
| 2 May 22 Sandra-Ste | (362) lunch | | | | | | |
| 3 May 23 Sandra-Ste | (384) | | | | | | |
| 4 May 24 Sandra-Ste | (399) | | | | | | |
| 5 May 25 Sandra-Ste | (304) | | | | | | |
| 6 May 26 vanilla.com | (3042) | | | | | | |
| 7 Jan 07 Pharmacy | (1689) asking you regained | | | | | | |
| 8 Jan 08 Pharmacy | (1689) | | | | | | |
| 9 Jan 09 Pharmacy | (1575) Vigaro, Pentemerine,kenji | | | | | | |
| 10 Jan 10 bryjohn.com | (1682) Look at F.H.W.-002- | | | | | | |
| 11 Jan 11 briesjohn.com | (1683) | | | | | | |
| 12 Jan 12 masudomatsu.com | (1444) 12 pounds by February | | | | | | |
| 13 Jan 13 jack.com | (1344) | | | | | | |
| 14 Jan 14 peppermint | (1343) Merge Agreement .. get the home | | | | | | |
| 15 Jan 15 Donortz2gsms.com | (3218) | | | | | | |
| 16 Jan 16 Donortz2gsms.com | (3219) | | | | | | |
| 17 Jan 17 Donortz2gsms.com | (3220) | | | | | | |

> To add an attachment, you must supply the name of the file, including the pathname if it is not in your Home directory.

> To change the format of your message to a richer header, you can press Control + R. This adds additional fields to your message header, such as Bcc and Newsgroups. If you have defined a directory, the contents of your signature file appear at the bottom of your message text.

> When you are ready to send your message, you can press Control + X. Pine asks if you want to send your message.

> To add an attachment, you can type the name of the file. Pine attaches the file to the message when you send it. You can add attachments by pressing Ctrl + j.

> Pine allows you to add carbon copy (cc) recipients to your messages and to include attachments.

> To compose and send e-mail with pine, you can press c while the main menu. This moves you into a simple-editor in which you pre-inserts message parts as the To and Subject.

> As you type your message, the form area grows to accommodate your message.

> To move a message to a different folder, you can type s when pine displays the message list or the message itself. Then pine asks you for the name of the folder where you want to place the message.

## Mac 上的 UNIX

## APACHE 简介

Apache 是如今互联网上最流行的 Web 服务器。它约占 60% 的 Web 服务器，并可能占了 80% 的现有 Web 服务器书籍，Apache 是成为互联网基础部分的开源产品之一。它被广泛使用、易于理解且实现良好。

### Web 服务器的工作原理

Apache Web 服务的目的是来自来自浏览器的请求并提供请求的页面。与任何重要的互联网服务一样，Apache 运行在专用端口上。这个端口不是为 Apache 专用，而是用于 Apache 和浏览器之间通信的 HTTP 协议。

当 Web 服务器接收到请求时，它查看某些配置变量来确定应该向客户端发送哪个页面。对于 Apache 服务器，该页面通常被称为 index.html，尽管由于 Java 和其他工具在 Web 上的流行，它可能只是一个静态页面。如果是一个静态 HTML 文件，服务器会立即将其传输给客户端。在请求到达服务器后，还会创建许多类型的页面，其信息是从客户端计算机的 Cookie 中读取的或存储在服务器上的。这些信息允许为每个用户创建自定义页面。无论何种情况，当页面准备好后，就会发送给客户端。即使服务器在地球的另一端，也会在几秒钟内完成。

安装并运行 Web 服务后，好奇的访问者可能会在 Web 浏览器中输入您的 URL，您的网站可能输出各种类型的内容。在 Web 浏览器中输入如 www.dragonfly.com 的地址，地址首先会被传递给 DNS 服务器进行翻译。然后，向远程系统的 80 端口发送请求。该请求本质上是 GET /，即对您网站主页或默认文档的请求。

### 免费且可配置

Apache 之受欢迎是因为它对任何用户都是免费的，尽管这不是唯一的原因。Apache 还可以通过模块set进行扩展，并可以根据预期用途进行定制。你可以在构建时添加或删除模块，因此生成的二进制文件仅包含你需要的特性。Apache 还支持人们可能在 Web 服务器中期望的所有功能。为 Apache 配置基于名称的虚拟服务器（即多个站点在同一机器上运行，但看起来是独立的）是很容易。配置安全以及针对预期流量对服务器进行调也是简单的过程。

## 融入互联网

### 使用 APACHE 提供 Web 页面

Web 服务器与其他互联网服务一样，依赖域名系统（DNS）来运行。当你输入如 http://www.dragonflyditch.com 的 URL 时，你同时指定了多项内容。你指定了 HTTP 是协议——描述客户端和服务器之间通信的有限语言——用于与服务器进行通信。这是 Web 使用的首要协议，但不是唯一的协议。通过输入 dragonflyditch.com，你正在识别特定的服务器，并依靠 DNS 服务将此文本名称翻译为 IP 地址，以便 DNS 可以使用该 IP 地址定位并与该服务器通信。通过什么都不输入，你表示你想要与运行在 Web 服务器默认端口 80 上的服务器通信，并且你确保了你想要该站点的主页或默认文档。

### APACHE 配置

服务器端的配置决定了服务器上的哪个目录包含可查看的文档和文件。对于 Apache 来说，该目录被称为文档根目录（document root）。在配置良好的 Web 服务器上，访问者可以查看或下载此目录之外的文件。

服务器端的配置还决定了当你在 URL 名称中输入 http://dragonflyditch.com 时，文件服务器向你传输什么。每当你输入不包含文件名的 URL 时，Apache 都会在默认文档列表中查找与请求目录中的文档匹配的项。如果文档列表包含 index.html 和 index.jsp，而文档中不包含其中任何一个，Apache 将返回两种结果之一：错误代码或目录列表。该服务取决于是否启用了目录浏览。

## 幕后故事
