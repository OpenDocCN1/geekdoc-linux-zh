

如果你有朋友给你发送 HTML 格式的邮件，而你无法方便地用你的 MUA 阅读，那么这个鲜为人知的技巧会让你感到高兴。

⇒ 要将选定的 HTML 源代码作为渲染后的文本查看，请执行以下操作：

+   1. 通过左键单击并拖动鼠标指针来选择要渲染的源代码（参见 Recipe 10.3 [Manipulating Selections of Text]，第 253 页）。
+   2. 在终端中启动 Lynx，使其从标准输入读取：
+      $ lynx -stdin RET
+   3. 通过在该终端中单击鼠标中键，将文本粘贴到正在运行 Lynx 的终端中。
+   4. 通过在该终端中输入 CTRL-D 来结束向 Lynx 的输入。

这样做时，Lynx 将渲染并显示 HTML 代码。

NOTES：Lynx 在显示代码后仍会继续运行，然后你必须输入 Q 退出并退出 Lynx。或者，包含 -dump 选项以使 Lynx 将渲染后的 HTML 显示到其标准输出然后立即退出。

每当 HTML 代码从流中输出时，你都可以将其通过管道传输到 lynx -stdin -dump 以将渲染后的代码显示到标准输出。

这种技术也适用于测试任意选择的 HTML 代码。

## 33.2.7 Specifying Key Bindings in Lynx

你可以在 Lynx 中指定特殊的键绑定，以便移动命令就像在你最喜欢的编辑器中一样工作：使用 -emacskeys 选项启用 Emacs 风格的键绑定，并使用 -vikeys 选项启用 Vi 风格的键绑定。

⇒ 要使用 Vi 风格的键绑定用于移动来启动 Lynx 并打开 URL http://nostarch.com/，请输入：

```
$ lynx -vikeys http://nostarch.com/ RET
```

## 33.2.8 Using Lynx with a Mouse

要使用鼠标使用 Lynx，请向 lynx 提供 -use_mouse 选项。如果你的 Lynx 版本启用了鼠标支持，提供此选项将允许你仅通过左键单击即可跟随链接；右键单击窗口中的任意位置即可返回到上次访问的页面。

⇒ 要使用鼠标浏览 /usr/share/doc 目录中的文件，请使用 lynx 输入：

```
$ lynx --use_mouse /usr/share/doc RET
```

## 33.3 Accessing the Web in Emacs

W3
DEB: w3-el-e21
RPM: w3
WWW: http://www.cs.indiana.edu/elisp/w3/docs.html

你可以在 Emacs 中获取网络。目前速度相当慢，但它可能有其用途。为此，使用 w3-mode。它的功能很多——你可能唯一会错过的是 ssl 支持（尽管这可能即将到来）和 JavaScript 和 Java 支持（好吧，你可能不会错过它，但它会使一些网站变得有点难以使用）。它可以处理框架、表格、样式表以及许多其他 HTML 功能。

![](img/be7f02611e5cefde1a18c788fede22f7_682_0.png)

Figure 33-2. w3-mode in Emacs.

⇒ 要在 Emacs 中加载 w3-mode，请输入：ALT -X w3 RET

要在一个新缓冲区中打开 URL，请输入 CTRL -O，并在 minibuff er 中给出要打开的 URL（留空则打开 w3-mode 主页）。中键单击链接以跟随它，在新缓冲区中打开 URL。

⇒ 以下是两种使用方法。

+   - 要打开 URL http://emacs.org/，请输入：
+     <CTRL>-<Q> http://emacs.org/ <RET>
+   - 要打开 w3-mode 主页的 URL，请输入：
+     <CTRL>-<Q> <RET>

最后一个示例在自己的缓冲区中打开 w3-mode 主页，如 Figure 33-2 所示。

下表描述了在 w3-mode 中使用时一些特殊命令。

| Command | Description |
|---|---|
| <RET> | Follow the link at point. |
| <SPACEBAR> | Scroll down in the current buffer. |
| <BKSP> | Scroll up in the current buffer. |
| <ALT>-<TAB> | Insert the URL of the current document into another buffer. |
| <ALT>-<S> | Save a document to the local disk (you can choose from HTML Source, Formatted Text, LaTeX Source, or Binary). |
| <CTRL>-<O> | Open an URL. |
| B | Move backward in the history stack of visited URLs. |
| F | Move forward in the history stack of visited URLs. |
| i | View information about the document in the current buffer (the information opens in new buffer called Document Information). |
| I | View information about the link at point in the current buffer (the information opens in new buffer called Document Information). |

