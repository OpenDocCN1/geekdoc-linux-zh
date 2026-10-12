
## 通讯簿
Netscape 内置了一个通讯簿，您可以使用它来记录人们的电子邮件地址和其他个人信息。选择 Communicator → 通讯簿 以打开通讯簿。

## 安全性
如果您在处理敏感材料，可以利用内置于 Netscape 中的几种安全功能。点击工具栏上的“安全”图标。图 9-4 显示了出现的安全信息页面。

![](img/1744bde8c889adfab3fc911e1687fecf_350_0.png)

图 9-4：通过安全信息窗口检查 Web 内容的安全性。

安全信息窗口的第一页（如所示）描述了当前页面是否已加密。您可以配置证书，作为一种验证其他人或网站身份以及向他们验证您身份的手段。选择“密码”以输入一个密码，如果需要您的证书，系统将提示您输入该密码。

在 Navigator 部分，选择当进入或离开加密网站时是否应收到警告。选择您的邮件是否应被加密和签名。在“加密模块”部分，您可以添加模块来提供您的加密技术（默认情况下，使用 Netscape 的内置 PKCS #11 模块）。

## 使用插件和辅助应用程序
虽然 Web 页面提供的主要内容类型是 HTML，但许多其他内容类型也可以由 Web 浏览器显示、播放或呈现。Netscape 遇到的大多数附加数据通过两种方式之一处理：插件或辅助应用程序。

插件是独立的程序，允许数据在 Netscape 窗口内播放。辅助应用程序可以是您在 Red Hat Linux 系统上可用的任何程序。由您决定在遇到特定类型的数据时要启动哪个插件或辅助应用程序。

**提示：** 阻碍我将小儿子电脑迁移到 Linux 的一件事是，他喜欢玩那些需要 Shockwave Director 插件的互联网游戏。由于目前 Linux 没有 Shockwave Director 插件，我购买了 CodeWeavers 的 CrossOver 插件（www.codeweavers.com）。

尽管 CrossOver 插件仍有一些不足之处，但它允许我运行 Shockwave Director、QuickTime 5 以及用于微软文件格式的各种查看器。CrossOver 的费用为 24.95 美元。对我来说，这是一笔很小的花费，因为它消除了一些阻碍我将电脑迁移到 Linux 的障碍。CrossOver 也提供演示版本。

## 添加辅助应用程序
要查看您的 Netscape 浏览器可以使用辅助应用程序和插件处理哪些类型的数据，请执行以下操作：

1. 选择 Edit → Preferences。出现 Netscape 首选项窗口。
2. 点击 Navigator 类别旁边的箭头。
3. 选择 Applications。显示已为计算机上的 Netscape 配置的插件和辅助应用程序的描述，以及有关插件如何处理的信息。

如果您从未在此实例的 Netscape 中添加任何插件或辅助应用程序，您可能已经注意到插件非常少。大多数条目代表在遇到特定类型数据时启动的辅助应用程序。Netscape 根据以下标准之一决定启动哪个辅助应用程序或插件：

- **后缀：** 如果浏览器正在读取的文件名附带特定后缀（例如应用程序的 *exe* 或压缩 zip 文件的 *gz*），它可以使用该后缀来确定文件的内容。当文件后缀与为特定辅助应用程序或插件配置的后缀匹配时，该辅助应用程序或插件将用于播放或显示数据。
- **MIME 类型：** 因为数据可能以流的形式到达浏览器或不带后缀，Netscape 可以使用附加在数据上的 MIME 类型来确定使用哪个插件或辅助应用程序。（MIME 代表 Multipurpose Internet Mail Extensions。）

按照前面所述步骤，打开 Netscape 首选项窗口至 Applications 页面后，您可以添加自己的辅助应用程序来自动处理浏览器中的特定类型数据。方法如下：

1. 点击 **New**。出现一个对话框，允许您添加有关辅助应用程序及其可处理数据的信息。
2. 输入数据描述、MIME 类型以及包含该类型数据的文件后缀（如果有）。

**注意：** 添加后缀时，不要包含点。

3. 根据您要添加的辅助应用程序类型，选择以下一项：
   - **Navigator** — 如果希望 Netscape Navigator 处理此类型数据，请点击此处。除了 HTML，Navigator 还可以处理各种图像类型（如 GIF、JPEG 和 BMP 文件）。
   - **插件** — 如果希望已安装的插件处理数据类型，请点击此处。点击插件字段旁边的向下箭头，从可用插件列表中进行选择。
   - **应用程序** — 点击此处以选择处理数据类型的应用程序。如果应用程序需要终端窗口才能运行，请输入 `xterm -e`，后接您需要输入的命令。这将在 xterm 窗口中执行命令，并按需读取数据。
   - **保存到磁盘** — 点击此处，以便在 Netscape 浏览器中遇到数据时提示下载数据。
   - **未知：提示用户** — 点击此处，以便在遇到此类型数据时提示如何处理。

**提示：** 请注意窗口中有很多数据类型被设置为未知：提示用户。许多条目代表您可能遇到的常见数据类型。如果您知道处理这些数据类型之一的应用程序，请单击它，选择 Edit，点击 Application，输入处理数据的应用程序，然后点击 OK。否则，当遇到此类型数据时，系统将提示您下载它或选择应用程序。

4. 完成后点击 OK。

## 添加插件
随 Red Hat Linux 提供的 Netscape Communicator 版本中，可用的插件并不多。要查看与您的 Netscape Navigator 浏览器关联的插件列表，请选择 Help → About Plug-ins。应出现类似于图 9-5 所示的窗口。

很可能您只配置了默认插件、Shockwave Flash 插件和 Plugger 插件。Linux 中可用的 Netscape 插件非常少。在 Windows 9x/2000 中，每个在 Red Hat Linux 中运行的插件大概有 20 个对应的插件。大多数插件由销售创建 Web 内容产品的公司编写，然后免费赠送插件，以便任何人可以播放该内容。因此，目前可能没有太多经济动机来创建 Linux 插件。

![](img/1744bde8c889adfab3fc911e1687fecf_353_0.png)

图 9-5：About Plug-ins 显示安装在 Netscape 中的插件。

尽管如此，有一些适用于 Netscape 的插件可以在您的 Red Hat Linux 系统上正常工作。以下是我能找到的插件：

- **Adobe Acrobat 插件**（www.adobe.com）— 显示 Adobe Systems 的 PDF（Portable Document Format）文件。（您可以从 Red Hat contrib 网站搜索 acroread 和 acroread-plugin RPM 软件包。）
- **Cult3D 插件**（www.cult3d.com）— 在 Web 上显示高质量的交互式实时 3D 图像。此插件来自 Cycore Computers。（点击 Download 以查找插件。有可用的 cult3d RPM。）
- **DjVu 插件**（www.djvu.sourceforge.net）— 显示使用 DjVu 图像压缩技术的图像。此插件来自 AT&T。
- **Gig 插件**（www.genlogic.com）— 在您的 Netscape 窗口中播放数据驱动的交互式图形。此插件来自 Generic Logic。
- **Plugger**（http://fredrik.hubbe.net/plugger.html）— 一种多媒体插件，通过依赖外部程序来播放数据，处理 QuickTime、MPEG、MP2、AVI、SGI-movie、Tiff、DL、IFF-anim、MIDI、Soundracker、AU、WAV 和 Commodore 64 音频文件。这是少数可能已安装在您电脑上的插件之一。
- **Real Audio**（www.real.com）— 播放 Real Audio 和 Video 内容。此插件来自 Real Networks。（我在此处找到一个 Real Audio RPM：http://scopes.real.com/real/player/unix/unix.html。）
- **Macromedia Flash Player**（www.macromedia.com/shockwave/download）— 显示多媒体矢量图形和动画。此插件来自 Macromedia, Inc.。Flash Player 随 Red Hat Linux 提供，但 Macromedia 的 Shockwave 插件尚未在 Linux 上可用。

