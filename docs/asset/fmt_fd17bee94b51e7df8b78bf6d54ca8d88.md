
```
/*
** Hypertext link coloring
*/
a:link    { color: #FF0000 }
a:visited { color: #B22222 }
a:active  { color: #FF0000 }

/* W3-specific section for Emacs versions which
** can only display one size of font at a time
*/
@media unifont {
h1,h2,h3,
h4,h5,h6 { text-decoration: underline; }

	h1 { color: rgb(0,255,255); }  // cyan
	h2 { color: rgb(70,130,180); } // steelblue
	h3 { color: rgb(106,90,205); } // slateblue
	h4 { color: rgb(135,206,235); } // skyblue
	h5 { color: rgb(0,0,128); }    // navy
	h6 { color: rgb(173,216,230); } // lightblue

	strong,em { color: red        }
	dfn { font-style: italic       }
	s,strike { color: green        }
}
```

W3 信息手册中有好几章专门介绍样式表的内部机制。你将在其中找到本书范围之外的详细资料。你可以通过将 W3 示例样式表复制到 `~/w3/default.css` 并告知 W3 使用该文件来感受样式表的运作方式。通过按 `M-x` 并输入 `customize-group` 来完成此操作。

在迷你缓冲提示处，输入

`w3-files`

此时会出现一个类似于图 20.3 的缓冲区。需要更改的设置项是`默认样式表`。在输入字段中输入示例文件的路径和文件名。

通过从 State 按钮的菜单中选择`Save For Future Sessions`（为未来会话保存）来保存更改。

在启动 W3 之前，将新的样式表加载到一个 Emacs 会话中并通读一遍。颜色规格可以采用三种格式：RGB 数字三元组、X11 `rgb.txt` 文件中命名的颜色，或 8 位截断的 RGB。上述示例中使用了所有这三种格式。

作为第一个 CSS 实验，试着更改文件中的一些颜色，使它们在 Emacs 背景色下显示得清晰。X11 应用程序 `xcolsel` 是一个方便的工具，可用于浏览可用颜色并查找其各种格式的名称。

![](img/c8827ea52a0796def3f6891892ed9d3a_434_0.png)

如果你正在使用 XEmacs（可能还有 Emacs 21），可以更改不同标题的相对大小。不要一次做太多更改，以便能够追踪任何错误。

文件中看似晦涩的部分将在样式表信息章节中进行解释。

保存更改后，按 `M-x` 并输入以下命令来加载一个本地 HTML 文件：

`w3-open-local`

你所做的更改应在 W3 缓冲区中可见。如果不可见，请检查文件是否存在错误。

需要牢记的一点是，W3 在 Emacs 会话中首次启动时读取其配置文件。你可以按 `q` 关闭 W3，编辑配置文件或样式表，然后重新启动 W3，但更改不会生效。W3 似乎在其内存中保持配置变量，直到 Emacs 会话结束。这意味着当你希望 W3 注意到对配置所做的任何更改时，你需要关闭并重启 Emacs。

## 安全性

W3 在设计时已考虑安全性。你可以安装外部的 SSL（Secure Sockets Layer，安全套接字层）程序，W3 将通过 SSL 通道加密 HTTP 连接。Cookies 是许多服务器希望留在你硬盘上的文件，可能包含密码或身份验证信息。你可以禁用所有 cookies，或将其限制在特定的受信任服务器范围内。

### 使用 SSL

为了使用 W3 的 SSL 功能，你必须安装一个外部程序。目前唯一支持的程序是 SSLeay 0.6.6 或更高版本。SSLeay 的当前状况是它已被其原始开发人员弃用。该代码被一个名为 OpenSSL 的新项目所采用，该项目作为 SSLeay 的开源替代品正在积极开发中。W3 不支持直接集成 OpenSSL，但通过一些脚本，可以规避这一劣势。

警告：以下是针对某些人行之有效的 SSL W3 方法的一些建议，但很可能需要一些调整才能在你的系统上运行。进行一些背景阅读会有所帮助。你可以在 [OpenSSL 网站](http://www.openssl.org) 上找到参考资源和链接。

W3 信息手册也可以提供进一步的帮助。

首先，创建一个名为 `emacs-ssl` 的 shell 脚本：

```
#!/bin/sh
exec 2>/dev/null
exec openssl "$@"
```

此脚本启动 `openssl` 并将所有错误消息重定向到 `/dev/null`，以免 W3 因此感到困惑。确保使该脚本可执行，然后将其移动到 `/usr/local/bin` 或路径上的其他二进制目录。

下一步是更改几个 W3-SSL 变量的值。最简单的方法是使用 Customize（自定义）。

#### SSL 变量

通过按 `M-x` 并输入以下内容，启动 SSL 的 Customize 缓冲区：

```
customize-group
```

响应提示时输入

```
ssl
```

生成的缓冲区如图 20.4 所示，允许你设置 SSL 证书目录以及 SSL 程序的命令行选项等变量。

![](img/c8827ea52a0796def3f6891892ed9d3a_436_0.png)

默认的 `openssl` 命令行参数应该是适用的，但 Program Name 变量应设置为 `emacs-ssl` 而不是 `openssl`，以确保调用的是你的新 shell 脚本，而不是直接调用 `openssl`。保存新设置，并关闭 Customize 缓冲区。

SSL 的主题相当复杂；各国立法机构规定不一，且多家商业机构对证书收费。万维网（WWW）是关于这个快速变化领域的最新信息的最佳来源。前面部分提到的 OpenSSL 网站，以及 W3 Consortium 的网站（与 Emacs W3 无关）都是不错的起点：`http://www.w3.org`。

### Cookies

Cookies（Cookie）颇具争议。有些人认为它们是对隐私的恶性侵犯，而另一些人则认为无需担心。这些文件对你系统中的任何程序都没有意义，但用于在你下次访问时识别你之前访问过的 WWW 主机。注册和密码信息存储在 cookies 中。结果是，下次访问网站时你无需手动登录。

在 W3 中默认启用 Cookies。你可以在 `~/.w3/profile` 中添加以下代码行来阻止 W3 接受任何 cookies：

```lua
(set-q-default 'url-privacy-level 'paranoid)
```

你可以使用 Customize 以更细微的方式调整 W3 的 cookie 行为。图 20.5 显示了 Url Customize Group 缓冲区。Privacy Level 复选框提供了一系列级别供你选择。按 `M-x` 并输入 `customize-group` 即可调出此缓冲区。

在 minibuffer 提示符下，输入 `url`。

或者，响应提示符输入 `url-cookie`。

在这个新的 Customize 缓冲区中，你会看到 Trusted Urls 和 Untrusted Urls 两项旁边的 INS 按钮。用鼠标中键点击其中一个按钮，将打开一个新的文本输入字段。然后你可以输入正则表达式（可以包含或排除 URL 范围）或具体的实际 URL，如图 20.6 所示。

![](img/c8827ea52a0796def3f6891892ed9d3a_438_0.png)

**图 20.5 Url Customize Group 缓冲区**

![](img/c8827ea52a0796def3f6891892ed9d3a_438_1.png)

**图 20.6 更多 Cookie 自定义**

举个例子，许多 Linux 用户不希望他们的机器上有来自 doubleclick.com 的 cookies。你可以在“Untrusted Urls”输入字段中输入以下正则表达式：

```
http://\.*.doubleclick\.com\.*
```

注意表达式中的第二个和第三个点如何用反斜杠转义，以便将它们解释为点号，而不是正则表达式中代表任意单个字符的符号。

谨慎的调整应能为你提供一个适合你情况的 cookie 使用级别。

## Masquerading（伪装）
