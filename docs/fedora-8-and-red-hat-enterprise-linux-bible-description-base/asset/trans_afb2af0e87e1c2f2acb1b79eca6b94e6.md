
- Linux 文档项目 (www.tldp.org/LDP/LDP-Author-Guide)
- GNOME 文档 (developer.gnome.org/projects/gdp/handbook/gdp-handbook)
- KDE 文档项目 (www.kde.org/documentation)
- FreeBSD 文档项目 (www.freebsd.org/docproj)

如果您想为上述任何文档项目做出贡献，请参阅每个组织的网站。在所有情况下，它们都会发布作家指南或风格指南，其中描述了它们所支持的 DocBook 标签，用于其写作工作。

## 创建 DocBook 文档

您可以使用任何文本编辑器创建文档，使用的标签在外观上类似于 HTML 标签（开始标签和结束标签出现在小于号和大于号之间）。还有一些文字处理程序允许您创建 DocBook 标记。例如，您可以从 OpenOffice.org Writer 将文档导出为 DocBook 格式。

下面的步骤提供了一个示例，该示例是使用纯文本编辑器生成的简单 DocBook 文档，并使用随 Fedora 和 RHEL 提供的工具输出为 HTML。（要执行以下操作，您需要安装 DVD 上的一组 docbooks 软件包。）

1.  在您的主目录中创建一个目录作为工作目录，并进入该目录。例如，您可以在终端窗口中输入以下内容：
    - `mkdir $HOME/doctest`
    - `cd $HOME/doctest`
2.  打开一个文本编辑器以容纳您的 DocBook 文档。例如，您可以输入：
    - `gedit cardoc.sgml`
    - （像 jedit 这样的文本编辑器，您可以从 www.jedit.org 获取，对于处理 DocBook 中使用的长标签名也很有用。）
3.  输入您希望在文档中出现的标签和文本。大多数 DocBook 文档要么是 `<book>` 类型（大型多章节文档），要么是 `<article>` 类型（单章节文档）。要尝试 DocBook 文档，请输入以下内容：
    - `<xml version="1.0">`
    - `<article>`
    - `<title>Choosing a new car</title>`
    - `<articleheader>`
    - `<abstract>`
    - 在本文中，您将学习如何定价、
    - 谈判并购买一辆汽车。
    - `</abstract>`

    ```xml
    <articleheader>
      <section>
        <title>Getting Started</title>
        <para>
          您首先要学习的是如何确定
          您的承受能力。
        </para>
      </section>
      <section>
        <title>The Next Step</title>
        <para>
          在您了解自己的能力后，您可以开始
          寻找。
        </para>
      </section>
    </article>
    ```

您应该注意这个文档的几点内容。整个文档都包裹在 article 标签中（`<article>`、`</article>`）。文章标题在 title 标签中（`<title>`、`</title>`）。section 标签（`<section>`、`</section>`）指示具有标题和段落的文本部分。这些部分以后可以在目录中单独处理。

4.  保存文件并退出文本编辑器。
5.  接下来，您可以尝试将刚刚创建的文档转换为几种不同的格式。例如，要创建 HTML 输出，您可以输入以下内容：
    - `db2html cardoc.sgml`

结果是名为 cardoc 的新目录。cardoc 目录中 db2html 的结果是：stylesheet-images 目录、t2.html 文件和 x12.html 文件。

6.  要查看刚刚创建的 HTML 文件，我输入了以下内容：
    - `firefox $HOME/doctest/cardoc/t2.html`

图 6-11 展示了由 db2html 命令创建的输出示例。左侧屏幕显示第一页。点击页面顶部的“Next”链接。您看到的第二页显示在右侧。在转换为 HTML 时，db2html 命令会在每个页面上添加“Next/Previous”按钮。它还将每个部分的标题放在第一页的目录中，并放在浏览器的标题栏中。

从这一点开始，您可以继续添加内容和不同类型的标签。如果您正在为特定项目（如上文中提到的 Linux 项目）编写文档，您应该获取有关他们所需的特定标签和其他样式问题的信息。

## 第 6 章：使用 Fedora 和 RHEL 发布

![](img/fb202c163797a743c3c6cf236316bc96_310_0.png)

图 6-11：DocBook 文件使用 db2html 命令输出为 HTML。

### 转换 DocBook 文档

前面的示例展示了如何创建简单的 DocBook 文档并将其转换为 HTML 输出。以下 Fedora 和 RHEL 实用工具将 DocBook 转换为其他格式：

- **docbook2dvi** — 将 DocBook 文件转换为设备独立文件格式。
- **docbook2html** — 将 DocBook 文件转换为 HTML 格式。
- **docbook2man** — 将 DocBook 文件转换为 man 页面格式。
- **docbook2pdf** — 将 DocBook 文件转换为便携式文档格式 (PDF)。
- **docbook2rtf** — 将 DocBook 文件转换为富文本格式 (RTF)。
- **docbook2tex** — 将 DocBook 文件转换为 TeX 格式。
- **docbook2texi** — 将 DocBook 文件转换为 GNU TeXinfo 格式。
- **docbook2txt** — 将 DocBook 文件转换为纯文本格式。

## 使用 Fedora 和 RHEL 打印文档

Red Hat Linux 中的打印由通用 UNIX 打印系统 (CUPS) 服务提供。LPRng 服务不再包含在 Fedora 或 RHEL 中，但仍可从 www.lprng.com/downloads.html 获取。然而，这两种服务都允许您使用本节中描述的一组基本打印命令进行打印。

> **交叉引用**：有关配置 Fedora 和 RHEL 的本地和远程打印机的信息，请参阅第 17 章。

作为非管理用户，您对打印机的配置没有太多控制权。但是，您可以检查哪些打印机可用于打印，检查打印队列的状态（等待打印的文档），并删除您自己的排队打印作业。

### 打印到默认打印机

当您的系统管理员（或您自己）为计算机配置打印机时，其中一台打印机被定义为默认打印机。如果您不确定哪台是您的默认打印机，请输入 `system-config-printer` 并查找旁边带有勾选标记的打印机。

大多数图形文字处理程序，如 StarOffice 和 OpenOffice.org，允许您从可用打印机中选择一台。然而，一些较不复杂的从命令行运行的 Linux 实用程序仅使用默认打印机。例如，`dvips`（用于打印 PostScript 文件）和 `groff -l`（用于打印 troff/nroff 文件）会自动将输出发送到默认打印机。

作为普通用户，您可以使用 `PRINTER` 环境变量来覆盖默认打印机。例如，如果您的计算机上的默认打印机是 `lp0`，而您想经常打印到 `lp1`，请通过设置 `PRINTER` 变量来更改您的默认打印机，如下所示：

```
$ export PRINTER=lp1
```

若要使其始终生效，您可以将此行添加到其中一个 shell 配置文件中（例如，如果您使用 bash shell，则添加到 `$HOME/.bashrc`）。

### 从 shell 打印

`lpr` 命令用于从 shell 打印文件。无论使用 LPRng 还是 CUPS 打印服务，您都可以使用 `lpr` 进行打印。如果您已经有一个格式化好的文件，请使用 `lpr` 打印它。例如，如果您有一个 PostScript 输出文件（`file.ps`）并且想将其打印到 PostScript 打印机，请使用以下命令行：

```
$ lpr file.ps
```

如果您想指定特定打印机（非默认），请添加 `-P*printer*` 选项。例如，要打印到 `lp0` 打印机，您可以输入以下内容：

```
$ lpr -Plp0 file.ps
```

如果您想打印多份文档副本，请使用 `-#*num*` 选项，其中 `num` 替换为您想要的副本数量。例如，要打印文件的五份副本，请使用：

```
$ lpr -#5 file.ps
```

lpr 命令还可以接受标准输出进行打印。例如，您可以通过将 groff 命令的输出管道传输到 lpr 来打印该输出，如下所示：

```
$ groff -Tps -man /tmp/chown.l | lpr -Plp0
```

> **提示**：enscript 命令（在 enscript 软件包中）是打印纯文本文件的另一个实用工具。它将文件转换为 PostScript 并将其发送到打印机或指定文件。

### 检查打印队列

要检查排队的打印作业的状态，您可以使用 lpq 命令。单独使用 lpq 会打印出默认打印机队列中作业的列表。例如：

```
$ lpq
hp is ready and printing
Rank Owner Job Files Total Size
active root 3 hosts 1024 bytes
1st root 7 (stdin) 625 bytes
2nd root 8 mem01.ps 12273 bytes
3rd chuck 9 bixes.ps 10880 bytes
```

lpq 的输出显示了打印机状态和等待打印的文件。Rank 列出了它们在队列中的顺序。Owner 是排队作业的用户。Job 显示作业编号。Files 列显示文件名或标准输入（如果文件是管道传输或定向到 lpr 的）。Total Size 显示每个文件以字节为单位的文件大小。

您可以向 lpq 添加选项以打印不同类型的信息。通过添加 -Pprinter，您可以查看任何可用打印机的队列。您还可以添加作业编号（以查看特定打印作业的状态）或用户名（以查看用户的所有排队作业）。

### 删除打印作业

如果您曾经错误地打印了大型文档，您就会明白从队列中删除打印作业的价值。同样，如果打印机将停机一段时间，而所有人都已将他们的作业打印到另一台打印机上，当打印机恢复在线时，有时清除所有打印作业也是好的。

在 Fedora 或 RHEL 中使用 lprm 删除打印作业。例如，要删除名为 bill 的所有作业（假设您是 bill 或 root 用户），请输入以下内容：

```
$ lprm -U bill
```

root 用户可以从队列中删除所有打印作业（虽然如果您经常这样做，可能会有些不高兴的用户）。为此，您需要在 lprm 命令行中添加一个破折号 (-)，如下所示：

```
$ lprm -
```

