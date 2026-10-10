

## 显示在图标旁边的提示行会打开一个新的 VM 帧，其中包含一个新创建的摘要缓冲区，该缓冲区填充了摘要邮件的内容。

您可以创建标记邮件或整个文件夹的摘要，然后将其发送出去。Mark 菜单中有多种标记命令，它们都以 `M` 开头，其中 `MM`（标记当前邮件）可用于标记准备用于摘要的邮件。`@` 字符会将标记的邮件打包成摘要并发送。

# 虚拟文件夹

虚拟文件夹是您的邮件文件夹的一个子集，由共享相同主题行、发件人、标签或任何其他若干标准的邮件组成。这不是一个真实的文件夹或文件；它只是 VM 用来选择性显示部分邮件的一种方法。这类似于 Rmail 的标签和选择性标记邮件视图。

您可以使用 Virtual 菜单中的命令创建其中一个，但它仅会在 VM 会话活动期间保持有效。创建永久虚拟文件夹需要在您的 `~/.vm` 文件中包含一个 Lisp 语句。该语句可以参照以下示例：

```lisp
(setq vm-virtual-folder-alist
      '(("First-virtual-folder"
        ((/path/file-name))
        (header "Duroc"))
       ("Second-virtual-folder"
        ((/path/file-name2 /path/filename3))
        (and (header "Bulletin") (author "Benson"))))
)
```

这个语句创建了一个关联列表，这是一种在本书前文讨论过的 Emacs Lisp 变量类型。还记得 `auto-mode-alist` 吗？它是一个文件名后缀与主要模式之间的对应列表。可以把这个看作 Emacs 将几个相关变量归到一个名称下的方式。

上述关联列表只有两个成员，每个成员都定义了一个虚拟文件夹。要使用此模板，请用虚拟文件夹名称替换 `First-virtual-folder` 和 `Second-virtual-folder`。路径部分应指向任何 VM 邮件箱文件。定义的最后一部分是说明符，其中可以包含正则表达式。第一个说明符（`header "Duroc"`）指示 VM 在邮件箱文件中查找主题行或头部行中任何位置包含单词 Duroc 的邮件。第二个使用了条件关键字，在此上下文中意味着只有当所有后续说明符都为真时，邮件才有资格被包含在该文件夹中。

`and` 说明符行（关联列表中的最后一条语句）可以这样理解：邮件必须在某个头部行中包含单词 Bulletin，并且必须在 From: 头部中包含单词 Benson。

这个关联列表可以包含任意数量的虚拟文件夹定义。在处理像这样的嵌套语句时，开启闪烁或高亮括号模式会很有帮助。

有关在此关联列表变量定义中可用的许多不同说明符的更多详细信息，请参阅 VM 模式帮助或 VM Info 文件。

诚然，这可以更轻松地实现，但与其他涉及 Lisp 的 Emacs 配置任务一样，你可以一次完成工作并多年使用其结果。

# VM 和 MIME 附件

VM 可以使用内部（尽管较慢的）Lisp 例程或外部程序来解码和编码 BASE64 和 Quoted-Printable MIME 类型。如果您希望 VM 使用外部解码器或编码器，您需要更改几个变量。VM 源码分发版包含四个此类程序的 C 源码——`gp-encode`、`gp-decode`、`base64-encode` 和 `base64-decode`。如果使用提供的 makefile 安装 VM，二进制文件将被构建并安装在 `/usr/bin` 中。以下 `~/.vm` 文件中的四行代码告诉 VM 优先使用这些程序而非内置的 Lisp 解码器和编码器：

```lisp
(setq vm-mime-gp-encoder-program "gp-encode")
(setq vm-mime-gp-decoder-program "gp-decode")
(setq vm-mime-base64-encoder-program "base64-encode")
(setq vm-mime-base64-decoder-program "base64-decode")
```

XEmacs VM 包不包含这些小型 C 程序，但在任何较新版本的 XEmacs 中，您都可以在 `/usr/[local]/lib/xemacs-[version-number]/[4,5 or 6]86-pc-linux` 目录中找到一个 base64 编码器/解码器，该目录是安装各种非 Lisp 实用程序的地方。该程序名为 `mmmencode`，以下 `~/.vm` 中的这些行将使它成为 VM 的默认 base64 编码器/解码器：

```lisp
(setq vm-mime-base64-decoder-program "mmmencode"
      vm-mime-base64-decoder-switches (list "-u")
      vm-mime-base64-encoder-program "mmmencode"
      vm-forwarding-digest-type "mime")
```

`mmmencode` 程序不在您的可执行文件搜索路径中，为了避免在前面的 Lisp 代码行中输入 `mmmencode` 的完整路径，您可以从 XEmacs 安装目录中的 `mmmencode` 文件到 `/usr/local/bin` 创建一个软链接：

```bash
cd / [directory where mmincode is installed] [Enter]
ln -s mmincode /usr/local/bin/mmincode [Enter]
```

除非您经常发送和接收大量 MIME 编码消息，否则您可能不需要费心更改这些变量。

有很多与 VM MIME 相关的变量——本章无法详尽介绍。VM FAQ 可以在本书 CD-ROM 中与 VM 源码相同的目录中找到，其中有关于 MIME 变量的信息章节。

# VM 工具栏

如果您正在运行 XEmacs 或 GNU Emacs 21（或更高版本），VM 会在窗口侧边或顶部显示工具栏，替换标准工具栏。当您使用 VM 一段时间后，您可能希望收回被工具栏占用的窗口空间，因为所有图标命令都可以从菜单和键盘命令中获取。以下是一些可以放入 `~/.vm` 文件的工具栏相关变量：

```lisp
(setq vm-use-toolbar nil)
```

此变量关闭工具栏。

```lisp
(setq vm-toolbar-orientation 'top)
```

如果您希望将工具栏放置在窗口的不同边缘，请在此语句中将 `top` 替换为 `bottom`、`left` 或 `right`。

如果您喜欢工具栏，但想更改图标及其运行的命令，您需要阅读 VM Info 文件，其中包含有详细说明的章节。

# 配置显示：帧和窗口

不可否认，VM 就是喜欢创建新的帧。新打开的文件夹、摘要爆发、新的邮件撰写缓冲区——所有这些都在新帧中打开。您可以通过将这些帧相关变量设置为 `nil` 来控制这种情况：

```lisp
(setq vm-frame-per-folder nil)
(setq vm-frame-per-composition nil)
```

如果您希望 VM 在任何情况下都不创建新帧，请在 `~/.vm` 中插入一行将此变量设置为 `nil`：

```lisp
(setq vm-mutable-frames nil)
```

设置此变量后，VM 将始终使用当前帧来创建新的 VM 缓冲区。

您有一个选择：您是否希望有一个摘要窗口以及一个显示第一封未读邮件的窗口？这种行为由一个变量的值控制，您的特定 VM 安装可能将其设置为某种方式。更改初始窗口布局涉及更改此变量：

```lisp
(setq vm-startup-with-summary t)
```

此语句使 VM 在新打开文件夹时始终生成摘要窗口。如果您希望第一封未读邮件全屏显示，请将值设置为 `nil`。

# 从服务器检索邮件

您可以配置 VM 使其能够登录您的 POP 或 IMAP 邮件服务器并下载新消息。许多用户更倾向于使用 Fetchmail 等外部程序，以避免被 Emacs 和 VM 束缚进行邮件检索，但如果这种方法适合您，以下是详细信息。

您需要将服务器信息作为条目插入 VM 的 spool 文件列表中。当您从主收件箱移动邮件到 VM 的 `~/INBOX` 时，VM 不需要这样一个列表，但如果您想告诉 VM 在其他位置查找新邮件，您需要使用类似于以下这样的语句：

```lisp
(setq vm-spool-files ('(/var/spool/mail/layerns "/~/Mail")))
```

通过修改语句使其类似于以下内容，将其中一个 spool 文件替换为服务器，包含端口、用户名和密码：

```lisp
(setq vm-spool-files '("mail.server.net:110:pass:username:password " ~/"Mailbox"))
```

如果您希望在 VM 将邮件“吸”入后从服务器删除这些邮件（除非您从多个位置访问，否则您可能希望这样做），您需要将服务器信息添加到另一个关联列表中：

```lisp
(setq vm-pop-auto-expunge-alist
      ('"mail.server.net:110:pass:username:*" . nil)
)
```

此语句中不需要包含密码，因为星号指示 VM 应使用在 `vm-spool-files` 变量中设置的值。

