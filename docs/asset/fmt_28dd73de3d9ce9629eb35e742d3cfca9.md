
- 介绍了 Applware 办公效率套件。Applware 提供了文字处理、电子表格和演示图表等日常功能。随书附带的 CD-ROM 中包含演示版本，以便你可以尝试它的功能。

- 详细描述了 Applware Words。介绍了它的基本功能，任何文字处理用户都应该熟悉这些功能。这本书的大部分是使用 Words 编写的。

- 介绍了其他 Applware 应用程序。Applware 拥有创建幻灯片和图形、使用电子表格以及发送电子邮件的应用程序。

- 给出了使用 PostgreSQL 创建 SQL 数据库的简单示例。该数据库用于演示如何使用 Applware Data 。Data 用作 SQL 数据库的接口。

- 介绍了 Netscape Navigator。该程序是世界上最常用的 Web 浏览器。它包含在 Red Hat 发行版中，并贯穿于本书的示例。

- 描述了配置和使用 Netscape Messenger。如果你想直接通过 ISP 发送和接收电子邮件，那么配置 Netscape 是简单的。然而，如果你想使用第 13 章描述的基于 Linux 的电子邮件服务器，则需要进一步的配置。本章介绍了这两个系统。

# 第 15 章

## 配置局内网 Web 服务器

本章内容

- 介绍 HTTP 协议
- 介绍 Apache Web 服务器
- 安装 Apache
- 创建简单的局内网 Web 页面
- 为简单的 Web 页面添加信息
- 通过你的 Web 页面访问
- 安全你的局内网 Web 页面

### 介绍 Apache Web 服务器

Apache 代表 patch server（补丁服务器）。它基于现有软件和一系列补丁文件（解释请参见 FAQ），因此得名。它是 RPM 格式的 Red Hat 发行版的一部分。世界上大多数 Web 服务器都使用 Apache。Apache 的核心是 HTTP 守护进程，它在后台运行并监听 80 端口的 HTTP 数据包。

HTTP 协议定义了 Web浏览的工作方式。当 `httpd` 接收到 HTTP 数据包时，它会尝试解释该数据包。如果成功，它默认会查找 `/home/httpd/html` 目录。你可以创建 `Hypertext Markup Language (HTML)` 文件并将它们存储在 `/home/httpd/html` 目录中。`httpd` 将与这些文件交互，并显示其中包含的信息。

### 安装和配置 Apache Web 服务器

本章的示例使用 Linux 个人工作站 `veracruz` 作为 Apache 服务器，其 IP 地址为 `192.168.1.1`。

在 `veracruz` 上以 `root` 登录并安装 Apache 软件包。

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/apache*
```

按照如下方式启动 `httpd` 守护进程：

```
/etc/rc.d/init.d/httpd start
```

检查是否正在运行：

```
ps x | grep http
```

你应该看到正在运行：

```
2187      S    0:00    httpd
```

接下来，使用你的浏览器查看是否可以访问你的新服务器。在位置字段输入以下 URL：

```
http://localhost
```

你应该在浏览器中看到图 15-1 所示的内容

## 第 15 章：配置互联网 Web 服务器

| 文件 编辑 视图  帮助 |

|---|---|

| 通信 打印 搜索 选项 |

| 地址：http://localhost/ 位置 |

### 成功了！

如果你能看到这个，说明在 Red Hat 系统上安装 Apache 软件成功了。你现在可以向目录添加内容并替换此页面。

如果你对预期内容不确定，请联系站点管理员。向 Apache 软件或 Red Hat Software 的作者发送邮件将被忽略。

Apache 文档已包含在此发行版中。

有关 Red Hat Linux 的管理和信息，请访问 Red Hat Software 网站。Red Hat Linux 手册位于。

### 使用 Lynx 查看你的 Web 页面

如果你没有安装 X，仍然可以使用文本版本的 `lynx` 程序查看你的新 Web 页面。输入以下命令。

```
lynx http://localhost
```

你应该能看到显示的 Web 页面文本部分。按 H 键显示帮助说明。使用上下箭头在页面内的链接之间移动光标。右、左箭头跳转链接。

## 设置简单服务

如果你点击 Red Hat 测试页面上的文档链接，你会看到图 15-2所示所示所示。

![](img/715fe99ccd2f8b7e4f2f45952c4ba42f_361_0.png)

图 15-2：Apache 1.3 文档

页面不仅为你提供了丰富的信息，还说明了 Apache 存储和访问信息的位置以及方法。默认目录为 `/home/httpd/html`。当你指定 `localhost` 位置时，`http` 会查看默认目录下的 `index.html` 文件。文档 URL 指向 `/home/httpd/html/manual` 目录下的 `index.html` 文件。图 15-2 中显示的信息包含在该文件中。

## 创建你自己的内网网页

下一步是创建你的内部 Web 页面。打开 Applixware Words，输入一些你想显示给公司内部计算机用户的信息。图 15-3 显示了在 Words 中输入的关于“小型企业中的 Red Hat Linux”的信息。

![](img/715fe99ccd2f8b7e4f2f45952c4ba42f_362_0.png)

图 15-3：在 Words 中创建的“小型企业中的 Red Hat Linux”页面

诚然这是一个单调的页面，但它足够简单，一眼就能理解。使用导出功能以 HTML 格式保存页面，选择 `/home/http/index.html` 文件进行保存，并选择 HTML 文件类型。点击导出保存新文件。

在 Netscape Navigator 中打开 `http://localhost/index.html` 文件，你应该就能看到新的 Web 页面。显示 `/home/httpd/html/index.html` 文件，你就可以看到组成新页面的 HTML 代码。

```
<HTML>
<HEAD>
<TITLE>Title</TITLE>
<!---Created by Applix HTML Author, Release 4.4 on Thu Apr 22
22:01:03 1999-->
```

```
<!-Ax:WP:DocVar:HTMLOriginalPath@"/tmp/ex01127d.aw---
</HEAD>
<BODY>
<H1>Red Hat Linux in Small Business resource page</H1>
<P></P>
<P></P>
</BODY>
</HTML>
```

- 第一行指定了使用的语言是 HTML。
- 接下来的五行是 Applixware Words 创建的模板代码。
- `<body>` 表示重要 HTML 代码的开始。
- `<P>` 和 `</P>` 组合创建一个段落分隔符。在这个示例中，它的效果是创建一个空行。
- `<P>` 和 `</P>` 参数还隔开了所创建的每行文本。

你可以点击 `Help -> Words` 然后双击 `HTML Author`，阅读更多关于在 Words 中理解和使用 HTML 的信息。

## 添加一些有用信息

图 15-3 中的页面只显示文本。要向内网 Web 页面添加一些内容，请挂载 CD-ROM，点击 `Insert -> Hyperlink`。接下来，点击 `File`，输入 `file:mnt/cdrom/doc/HOWTO/INDEX.html` 并点击 `Open`。在 `Enter Text` 字段中，输入你想用于链接的文本。这就是用户在 Web 页面上看到的内容，也是他们点击跟随链接的地方。最后，点击 `OK` 按钮。`INDEX.html` 文件指向随书附带 CD-ROM 上的 Linux HOWTO 文档。图 15-4 显示了 `Insert Hyperlink` 对话框。

![](img/715fe99ccd2f8b7e4f2f45952c4ba42f_364_0.png)

图 15-4：向 CD-ROM 上的小型 HOWTO 添加链接

接下来，添加指向外部 Web 页面的链接。再次打开 `Insert -> Hyperlink` 菜单，但在 `Target` 字段中如图 15-5 所示添加指向 `http://www.swcp.com/~paunchy/RHBIZ` 的链接。

![](img/715fe99ccd2f8b7e4f2f45952c4ba42f_365_0.png)

图 15-5：向我的书籍页面添加链接。

最后，添加指向 SWAT 接口（Samba 的配置 GUI，在第 8 章讨论）的链接。如图15-6所示，在 `Target` 字段中添加链接 `http://localhost:901`。

![](img/715fe99ccd2f8b7e4f2f45952c4ba42f_365_1.png)
