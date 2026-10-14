

```
$ wget -m -r -l1 --no-parent -A.gz http://monash.edu.au/~rjh/indiepop-1/download/ RET
```

### 32.5.4 读取网页的头部

所有 Web 服务器在页面请求开始时都会输出特殊的头部信息，但当你用 Web 浏览器检索 URL 时通常看不到它们。这些头部包含诸如 Web 服务器主机的当前系统日期以及 Web 服务器和操作系统软件的名称和版本等信息。

使用 `-S` 选项与 wget 一起使用以在检索文件时输出这些头部；头部会输出到标准输出，或如果使用则输出到日志文件。

- 要检索 http://slashdot.org/ 上的文件并输出头部，请输入：

  ```
  $ wget -S http://slashdot.org/ RET
  ```

此命令将服务器响应头部写入标准输出，并将 http://slashdot.org/ 的内容保存到当前目录中的一个文件中，其名称与原始文件相同。

## 32.6 编写 HTML

```
@sf(Debian): `bluefish'
@sf(WWW): http://bluefish.openoffice.nl/
```

超文本标记语言（HTML）是 Web 的标记语言；HTML 文件只是用这种标记语言编写的纯文本文件。你可以在任何文本编辑器中编写 HTML 文件；然后，在 Web 浏览器中打开该文件以查看 HTML 标记以其生成的超文本外观呈现。

许多人推崇 Bluefish，这是一款功能齐全、用户友好的 X 平台 HTML 编辑器。

Emacs（参见 Emacs 部分）有一个主要模式来方便编辑 HTML 文件；要在缓冲区中启动此模式，请输入：

```
M-x html-mode RET
```

HTML 模式的功能包括插入“骨架”结构。HTML 模式函数的帮助文本包含一个非常简短的 HTML 编写教程——查看该函数的文档以显示教程。

- 要在 Emacs 中阅读简短的 HTML 教程，请输入：

  ```
  C-h f html-mode RET
  ```

> **注意：** 当你在 Emacs 缓冲区中编辑 HTML 文件时，你可以在另一个窗口中在 Web 浏览器中打开同一文件——Web 浏览器只读取而不写入它们打开的 HTML 文件，因此你可以在 Emacs 中创建的同时在浏览器中查看渲染后的文档。当你在 Emacs 缓冲区中进行更改并保存后，重新加载浏览器中的文件即可立即看到更改生效。

- [32.6.1 为图像标签添加参数](#32.6.1) — 为图像标签添加参数。
- [32.6.2 将 HTML 转换为其他格式](#32.6.2) — 将 HTML 转换为文本。
- [32.6.3 验证 HTML 文件](#32.6.3) — 验证 HTML。

### 32.6.1 为图像标签添加参数

```
@sf{Debian}: `imgsizer`
@sf{WWW}: `http://www.tuxedo.org/esr/software.html#imgsizer`
```

为了可用性，HTML 图像源标签应具有 `HEIGHT` 和 `WIDTH` 参数，它们指定该标签描述的图像的尺寸。通过在页面上的所有图像标签中指定这些参数，页面中的文本将在浏览器窗口中在图像加载之前显示。没有它们，浏览器必须在显示页面上的任何文本之前加载所有图像。

使用 imgsizer 自动确定正确的值并将其插入到 HTML 文件中。将要修复的 HTML 文件的名称作为参数给出。

- 要向文件 `index.html` 添加 `HEIGHT` 和 `WIDTH` 参数，请输入：

  ```
  $ imgsizer index.html RET
  ```

### 32.6.2 将 HTML 转换为其他格式

```
@sf(Debian): `unhtml`
@sf(Debian): `html2ps`
@sf(WWW): http://dragon.acadiau.ca/~013639/
@sf(WWW): http://www.tdb.uu.se/~jan/html2ps.html
```

有几种方法可以将 HTML 文件转换为其他格式。你可以将 HTML 转换为纯文本以便阅读、处理或转换为其他格式；你也可以将 HTML 转换为 PostScript，你可以查看、打印它，或将其转换为其他格式，例如 PDF。

要简单地从文本中删除 HTML 格式，请使用 unhtml。它从标准输入（或指定的文件名）读取，并将其输出写入标准输出。

- 要浏览已删除 HTML 标签的 `index.html` 文件，请输入：

  ```
  $ unhtml index.html | less RET
  ```

- 要从文件 `index.html` 中删除 HTML 标签并将输出写入名为 `index.txt` 的文件，请输入：

  ```
  $ unhtml index.html > index.txt RET
  ```

当你用 unhtml 从文件中删除 HTML 标签时，文本不会进行进一步的格式化。此外，它仅适用于文件，而不适用于 URL 本身。

使用 lynx 将 HTML 文件或 URL 保存为格式化的文本文件，以便生成的文本在 lynx 中查看时看起来像原始 HTML。它还可以保留原始 HTML 中的斜体和超链接信息。参见 从 Web 上浏览文本 部分。

你可以做的其中一件事是将此 lynx 输出通过管道传输到用于设置文本间距的工具，然后发送到 enscript 以设置字体。这对于以打字稿“手稿”形式打印网页很有用，其中图像和图形被移除，文本以 Courier 字体双倍行距设置。

- 要以打字稿手稿形式打印 URL http://example.com/essay/ 的副本，请输入：

  ```
  $ lynx -dump -underscore -nolist http://example.com/essay/ | pr -d | enscript -B RET
  ```

> **注意：** 在某些情况下，你可能希望在打印前编辑文件，例如当网页包含文本导航栏或其他你希望在将其转换为手稿前删除的文本时。在这种情况下，你会将 lynx 输出通过管道传输到文件，编辑该文件，然后对文件使用 pr 并将该输出通过管道传输到 enscript 以进行打印。

最后，你可以使用 html2ps 将 HTML 文件转换为 PostScript；这在你想要打印带有所有图形和图像的网页时很有用，或者当你想要将整个网站或其部分转换为 PDF 时很有用。

