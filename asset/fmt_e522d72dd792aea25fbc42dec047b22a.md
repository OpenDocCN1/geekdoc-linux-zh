
## 打印当前页面
点击 `File`（文件）-> `Print`（打印）打印当前网页。打印对话允许你打印到特定的打印机或将打印输出保存为 PostScript。你还可以选择横向或竖向模式打印、选择打印顺序、选择灰度或彩色以及选择页面大小。

## 关闭 Navigator 窗口
点击 `File`（文件）-> `Close`（关闭）。或者你可以点击窗口框架右上角的 X。

## 复制文本
要复制页面文本，点击并拖动鼠标指针覆盖你想复制的文本。点击 `Edit`（编辑）-> `Copy`（复制）来复制文本。你可以点击 `Edit`（编辑）-> `Select All`（全选）来选择所有文本。

## 查找文本
要在 Web 页面查找文本，点击 `Edit`（编辑）-> `Find`（查找），填写要搜索的文本，然后点击 Find。再次查找相同的文本点击 `Edit`（编辑）-> `Find Again`（再次查找）。

## 搜索 Internet
你可以通过多种方式在 Internet 上搜索关键词短语。点击 `Edit`（编辑）-> `Search Internet`（搜索 Internet）。（`yahoo.com`, `altavista.com`, `hot.com`, `excite.com`, `lycos.com`, `snap.com`）。

## 显示工具栏
点击 `View`（视图）显示或隐藏工具栏。

## 刷新页面
如果页面加载过慢，点击 `View`（视图）-> `Reload`（刷新）。

## 停止页面
如果你想停止加载，点击 `View`（视图）-> `Stop`（停止）。

## 查看页面源码
要查看页面底层 HTML 代码，点击 `View`（视图）-> `Source`（源码）。

## 选择其他 Netscape Communicator 功能

除了 Netscape Navigator 浏览器，Netscape Communicator 还包含了其他客户端程序和功能。以下是这些功能的列表：

- `Messenger`：选择 Communicator Messenger 打开 Messenger 窗口以查看邮件和新闻组。Messenger 窗口将在章的 E-mail 和 Newsgroup 章节中描述。

### 第 9 章 ✦ 互联网和网页工具 295

安全信息（Security Info）窗口的第一页（此处所示）描述了当前页面是否加密。你可以配置证书作为验证他人及网站身份的手段，也可以向他们验证自己的身份。选择“密码”（Password）输入一个密码，当需要你的证书时会提示你输入该密码。

在“导航”（Navigator）下，选择在进入或离开加密的 Web 站点时是否应该接收警告。选择你的邮件是否被加密并签名。在“加密模块”（Cryptographic Modules）下，你可以添加模块来提供你的加密技术（默认使用 Netscape 内部 PKCS #11 模块）。

## 使用插件和辅助程序

虽然 Web 页面提供的主要类型是 HTML，但 Web 浏览器还可以显示、播放或呈现许多其他类型的内容。Netscape 遇到的大多数额外数据通过两种方式之一处理：插件（plug-ins）或辅助程序（helper apps）。

插件是自包含的程序，允许数据在 Netscape 窗口内播放。辅助程序可以是 Red Hat Linux 系统上可用的任何程序。当遇到特定类型的数据时，由你来决定启动 Netscape 浏览器时使用的插件或辅助程序。

## 添加辅助程序

要查看你的 Netscape 浏览器可以使用辅助程序和插件处理哪些类型的数据，请执行以下操作：

1. 点击 `编辑（Edit）` > `偏好（Preferences）`。出现 Netscape 偏好窗口。
2. 点击“导航”（Navigator）类别旁边的箭头。
3. 选择“应用程序”（Applications）。将出现你计算机上为 Netscape 配置的插件和辅助程序的描述，以及关于如何处理这些插件的信息。

如果你从未在在此 Netscape 实例中添加过任何插件或辅助程序，你将会发现插件非常少（事实上，可能只有默认插件）。大多数条目代表在遇到特定类型数据时启动的辅助程序。Netscape 根据以下标准之一来判断它遇到了什么种的数据（并随之决定启动何种辅助程序或插件）：

- 后缀名（Suffixes）：如果浏览器正在读取一个文件名后带有特定后缀名的文件（例如应用程序的 `.exe` 或压缩 zip 文件的 `.gz`），它可以使用该后缀名来确定文件内容。当文件的后缀名与特定辅助程序或插件配置的后缀名匹配时，将使用该辅助程序或插件来播放或显示数据。

![](img/176fafece2d30daee750bc078e898ee4_326_0.png)

### 296 部分 + 使用 Red Hat Linux

MIME 类型：因为数据可能以流的形式到达浏览器，或者没有后缀名。Netscape 可以使用数据附带的 MIME 类型来确定使用哪个插件或辅助程序。（MIME 代表多用途互联网扩展。）

如上一个步骤所述，当 Netscape 偏好窗口打开到“应用程序”页面时，你可以添加你的辅助程序来自动处理浏览器中的特定类型数据。方法如下：

1. 点击“新建”（New）。出现一个对话框，允许你添加有关辅助程序及其能处理的数据的信息。
2. 输入数据的描述、MIME 类型（如果有）以及包含该类型数据的文件的文件后缀名（如果有）。
3. 根据你想要添加的辅助程序类型，选择以下项之一：
   - 导航（Navigator）——如果你希望 Netscape Navigator 处理此类类型的数据，点击此处。除了 HTML 之外，Navigator 还可以处理各种类型（如 GIF、JPEG 和 BMP 文件）。
   - 插件（Plug-in）——如果你希望使用已安装的插件来处理数据，点击此处。点击插件字段旁边的向下箭头，从可用插件列表中选择。
   - 应用程序（Application）——点击此处选择一个应用程序来处理该数据类型。如果应用程序需要终端（Terminal）窗口来运行，输入 `x -e`，后跟你需要输入的命令行。这将在 xterm 窗口中执行命令，根据需要读取数据。
   - 保存到磁盘（Save to Disk）——点击此处，当你在 Netscape 浏览器中遇到该数据时提示下载数据。
   - 未知提示用户（Unknown Prompt User）——点击此处，当遇到此类数据时，提示你该如何处理。

![](img/176fafece2d30daee750bc078e898ee4_327_0.png)

注意窗口中有很多数据类型显示为“未知：提示用户”（Unknown: Prompt User）。这些条目中的许多代表你可能会遇到的常见数据类型。如果你知道可以处理这些数据类型之一的应用程序，点击它，选择“编辑”（Edit），在应用程序中指定处理数据的程序，并点击“确定”（OK）。

4. 完成后点击“确定”。

## 添加插件

在 Red Hat Linux 自带的 Netscape Communicator 版本中，可用的插件并不多。要查看与你的 Netscape Navigator 浏览器关联的插件列表，点击帮助 > 关于插件（Help About Plug-ins）。将出现一个与图 9-5 类似的窗口。

### 第 9 章 ✦ 互联网和网页工具 297

![](img/176fafece2d30daee750bc078e898ee4_328_0.png)

图 9-5：关于插件

### 298 部分 + 使用 Red Hat Linux

- Real Audio (`http://www.real.com`) — 播放 Real Audio。该插件来自 Real Networks。
- Macromedia Flash Player (`http://www.macromedia.com/shockwave/alternates/`) —— 显示动画。该插件来自 Macromedia, Inc.
- Ump (`http://pub.bnl.org/~caolan`) —— 一个 midi 播放器。基于 Timidity 公有领域软件。
- Xswallow (`http://csn.ie/~docs/Xswallow`) —— 允许将 X 窗口内联。
- MPEG TV (`http://www.mpeg.com`) —— 显示视频。该插件来自 MPEG。
- Acrobat Plug-in (`http://www.adobe.com`) —— 显示 PDF（便文档格式）。该插件来自 Adobe Systems。
- DJVu Plug-in (`http://www.att`) —— 显示图像。该插件来自 AT&T。
- Gig Plug-in (`http://www.genlogic.com`) —— 处理数据类型。该插件来自 Generic Logic。
- Plugger (`http://fredrik.net/plugin`) —— 播放数据。该插件来自 AT&T。
- Browserwitch-Plaza (`http://browser..com/plugin.html`) —— 按类别或仅针对 Linux 显示插件。

## 设置 Netscape 偏好
