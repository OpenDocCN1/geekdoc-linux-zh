
# 第 33 章：万维网

该命令下载给定的 URL，并在当前工作目录中写入一个与原始 URL 同名的文件 `garbo20.gif`。

如果你在下载完成前中断了下载，正在检索的文件内容将仅包含中断前检索的部分。使用带有 `-c` 选项的 `wget` 可以从中断的地方继续下载。

- ⇒ 要恢复上一个示例中 URL 的下载，输入：

```
$ wget -c ftp://garbo.uwasa.fi/garbo-gifs/garbo20.gif (RET)
```

注意：为了使 `-c` 选项产生预期效果，你应该在之前运行 `wget` 的相同目录下运行它，部分检索的文件应该仍然存在。

### 33.5.2 归档整个网站

要归档单个网站，请使用带有 `"mirror"` 选项的 `wget`，如果可能，它将按原始时间戳保存文件，并设置“递归检索”选项下载所有内容。在检索发生错误时指定重试次数，使用带有数字参数的 `-t` 选项——`-t3` 通常对于安全地跨网检索很好；使用 `-t0` 指定无限次重试，适用于连接非常糟糕但你确实想归档某些东西的情况，无论需要多久。最后，使用带有文件名作为参数的 `-o` 选项将进度日志写入文件——如果在归档过程中发生故障，检查它将很有用；一旦归档过程完成且你确定成功，就可以删除日志文件。

- 要镜像 `http://www.example.org/` 网站，允许最多重试三次检索文件，并将错误信息写入名为 `mirror.log` 的日志文件，输入：

```
$ wget -m -t3 http://www.example.org/-o mirror.log
```

此命令在当前目录的子目录 `www.example.org` 中创建 `http://www.example.org/` 网站的归档。日志消息写入当前目录中名为 `mirror.log` 的文件中。

要继续已停止的归档，使用 `-nc` (“no clobber”，不覆盖）选项；它不会检索已经下载的文件。为了让此选项按你的预期工作，请确保你处于最初开始归档网站的相同目录。

- 要继续对 `http://www.example.org/` 网站中断的归档，允许最多重试三次检索文件，并将错误信息写入名为 `mirror.log` 的日志文件，输入：

```
$ wget -nc -t3 http://www.example.org/-o mirror.log
```

## 33.7 设置起始页

备注：更多关于 `zgrep` 的信息，请参阅菜谱 14.7.2 [在压缩文件中匹配行]，第 349 页。

起始页是浏览器在启动时，如果没有提供 URL 作为参数，会自动加载的 Web 页面。如果你点击浏览器的“主页”按钮（如果有的话），它也会加载该页面。

你可以定义自己浏览器的起始页。有些人将其设置为喜喜的新闻源或出版物的 URL，而另一些人则编写自己的起始页，其中列有经常访问的链接列表、搜索引擎表单等内容。

要创建自己的起始页，只需将其编写为 HTML 文件；你可以将其保存在主目录的任何地方并提供完整路径；或者，如果你在本地系统上运行了 Web 服务器，可以将其放在服务器 HTML 目录树的某处，并通过 HTTP URL 访问。

以下是在 Mozilla 和 Lynx 中定义起始页的方法。

### 方法 #1

```
Mozilla
DEB: mozilla-browser
RPM: mozilla
WWW: http://www.mozilla.org/
```

要在 Mozilla 中定义起始页，请在“Mozilla 偏好...”菜单中定义“主页”。
⇒ 要将 Mozilla 的默认起始页更改为你自己的 `http://localhost/start/` 起始页，请执行以下操作：

- 1. 从菜单栏的“编辑”菜单中选择“偏好...”。
- 2. 在“位置”框中点击左键。
- 3. 将其内容替换为你想要的起始页：
   `http://localhost/start`
- 4. 点击“确定”按钮。

备注：在 Mozilla 中，每当你不带参数启动它、点击“主页”按钮或输入 (ALT)-(HOME) 时，起始页就会加载。

### 方法 #2

```
Lynx
DEB: lynx
RPM: lynx
WWW: http://lynx.browser.org/
```

Lynx 的起始页定义在 `/etc/lynx.cfg` 中的 `STARTFILE`，它可以是任何 URL，包括指向系统本地文件的 `file:////` URL。你需要超级用户权限来编辑此文件。

- 要将 Lynx 的起始页更改为 url `http://localhost/start/`，请使用文本编辑器编辑 `/etc/lynx.cfg`，使其包含以下行：

```
STARTFILE:http://localhost/start/
```

备注：Linux 发行版通常会重新定义 Lynx 的起始页为该发行版的页面。例如，在 Debian 系统上，起始文件被定义为 Debian 主页 [`http://www.debian.org/`]。

## 33.8 列出文本中的 URL

使用以下两种方法之一列出文本中的 URL——Web 页面的 HTML 源码、Web 页面的文本或任何文本文件。

要列出某些 Web 页面源码中的 URL，首先使用 `wget` 配合 `-q` 和 `-O` 选项将源代码导出到标准输出（参见菜谱 33.5 (从网络获取文件)，第 653 页），然后将其传递给上述方法之一。

要列出 Web 页面文本（而非源码）中的 URL，首先使用 `lynx` 配合 `-dump` 选项将页面内容导出到标准输出，然后将其传递给上述方法之一。

为了确保不列出重复的 URL，将输出传递给 `sort` 仅保留唯一行（参见见菜谱 13.5 (过滤重复文本行)，第 319 页中的方法 #2）。

一种方法使用 `grep` 查找 URL。另一种使用 `sed`，两者使用的相同正则表达式都相当长，并且包含了两个字面空格和两个制表符；如果你使用这些方法中的任何一种，你肯定想选择一个命令在脚本中运行它（参见菜谱 3.7 [使用 Shell 脚本]，第 84 页）。

### 方法 #1

要单行输出 URL 列表，使用带有 `-o` 选项的 `grep`，并将匹配 URL 的正则表达式作为参数。要搜索文本文件，请提供文件名作为第二个参数。
⇒ 以下是使用此方法的几种方式。

- 要输出 `/etc/lynx.cfg` 文件中包含的所有 URL 列表，输入（全部在一行）：

```
$ grep -o '\\(http(s)?\/\|ftp\\/gopher\\|telnet\\:news\\):\\\\/\\\|mailto\\\).*' (空格键) ;; (CTRL-V) (TAB)*/ /etc/lynx.cfg (RET)
```

- 要输出 `http://news.example.com/` HTML 源码中包含的所有 URL 列表，输入（全部在一行）：

```
$ lynx -dump http://news.example.com/ | grep -o '\\(http(s)?\/\|ftp\\/gopher\\|telnet\\:news\\):\\\\/\\\|mailto\\\).*' (空格键) ;; (CTRL-V) (TAB)*/' (RET)
```

- 要输出 `http://news.example.com/` HTML 源码中包含的所有 URL 列表，输入（全部在一行）：

```
$ wget -q -O http://news.example.com/ | grep -o '\\(http(s)?\/\|ftp\\/gopher\\|telnet\\:news\\):\\\\/mailto\\\\).*' (空格键) ;; (CTRL-V) (TAB)*/' (RET)
```

### 方法 #2

要单行输出 URL 列表，请使用以下命令的 `sed`。要搜索文本文件，请提供文件名作为参数。
⇒ 以下是使用此方法的几种方式。

- 要输出 `/etc/lynx.cfg` 文件中包含的所有 URL 列表，输入（全部在一行）：

```
$ sed -n '/.*\\http(s)?\/\|ftp\\/gopher\\|telnet\\:news\\):\\\\/\|mailto\\).*/' (空格键) ;; (CTRL-V) (TAB)*/ /etc/lynx.cfg (RET)
```

- 要输出 `http://news.example.com/` 文本中包含的所有 URL 列表，输入（全部在一行）：

```
$ lynx -dump http://news.example.com/ | grep -o '\\(http(s)?\/\|ftp\\/gopher\\|telnet\\:news\\):\\\\/\|mailto\\).*/ (空格键) ;; (CTRL-V) (TAB)
```

