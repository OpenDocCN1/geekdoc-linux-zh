

您在 Internet 上进行搜索。或者在位置框中输入一个或多个关键字，然后单击搜索。当然，您还可以使用侧边栏进行搜索，如前文所述。

**查看页面信息** — 通过选择**查看 → 页面信息**，您可以查看有关 Web 页面位置、其各个组成部分的位置、页面修改日期以及其他信息。图 9-4 显示了一个 Web 页面的页面信息窗口。单击链接选项卡，以查看该页面上指向 Web 上其他内容的链接。单击安全选项卡，以查看有关页面上使用的验证和加密的信息。

![](img/b22364e57409c2481ba806e4e6b9309c_347_0.png)

### 改进 Mozilla 浏览体验

并非您用 Mozilla 访问的每个网站都能完美运行。有些网站不符合标准、使用难以阅读的字体、选择难以辨认的颜色，或要求您使用特定类型的浏览器来查看其内容。为了改善浏览体验，您可以向 Mozilla 添加若干功能。

### 添加 CrossOver 插件

QuickTime 5 电影、Shockwave Director 多媒体内容以及各种 Microsoft 电影、文件和数据格式无法在 Mozilla Navigator 中直接播放。CodeWeavers（www.codeweavers.com）利用基于 x86 处理器上 Linux 系统 WINE 构建的软件，创建了 CrossOver 插件。虽然该产品不再单独提供（您必须购买整套 CrossOver Office 产品，价格为 39.95 美元），但 CrossOver 插件允许您播放一些在 Linux 中原本无法使用的内容。（可从 www.codeweavers.com/site/products/download_trial 下载演示版。）

安装 CrossOver 插件后，您将看到一个插件设置窗口，可以选择性地安装 QuickTime 6、Windows Media Player 6.4、Shockwave 8.5、Flash 6 以及 Microsoft Word、Excel 和 PowerPoint 查看器的插件。（在您阅读此文档时，可能已支持这些内容格式的后续版本。）您还可以安装其他多媒体插件，以及多种可与这些插件配合使用的字体。

> 提示：虽然我在早期版本的 Red Hat Linux 中运行 CrossOver 插件一切正常，但在撰写本文时，它尚未在当前的 Fedora Core 版本中正常工作。请查询 CodeWeavers，看他们是否已修正 CrossOver 插件以在最新版本的 Fedora Core 中运行。

### 添加首选项工具栏

您是否曾遇到过要求使用特定类型或版本浏览器的网页，或者拥有使页面难以阅读的字体或颜色的网页？称为 PrefBar2 的 Mozilla 首选项工具栏可以试图欺骗网站，使其认为您正在运行不同的浏览器。它还可以让您选择可能改善难以阅读的页面上颜色、字体和其他属性的设置。

您可以从 Mozdev.org 网站（prefbar.mozdev.org）安装这个小巧的工具栏。单击安装链接；安装后，重启 Mozilla。

> 提示：要使安装链接生效，您必须对 /usr/lib/mozilla-1.7.3 具有写入权限。这可能需要您以 root 身份登录，启动 Mozilla，安装首选项工具栏，然后注销 root 用户。

默认的一组按钮允许您执行以下操作：

- **颜色** — 在默认颜色和网页上设置的颜色之间进行切换。
- **图像** — 在加载图像和不加载图像之间切换，适用于您显示的页面。
- **JavaScript** — 允许或禁止 JavaScript 内容在 Mozilla Navigator 中播放。
- **清除缓存** — 删除内存和磁盘上的所有缓存内容。
- **终止 Flash** — 终止当前页面上所有嵌入的 Flash 内容。
- **真实 UA** — 选择将您的浏览器标识为其本身（当前版本的 Mozilla）或以下任一身份：Mozilla 1.0（在 Windows 98 中）、Netscape Navigator 4.7（在 Macintosh 中）、Netscape 6.2（在 Linux 中）、Internet Explorer 5.0（在 Macintosh 中）或 Internet Explorer 6.0（在 Windows XP 中）。

用户代理（UA）设置在处理要求 Internet Explorer（IE）的网站（通常是在 Windows 而非 MacOS 上的 IE）时非常有用。IE 6.0 WinXP 设置足以让 Mozilla 登录到 Microsoft Exchange webmail 服务，该服务通常设置为要求使用 IE。如果您希望在以 Windows 为主组织中使用 Linux，请安装首选项工具栏。

单击自定义按钮，为可添加其他按钮到首选项工具栏。您可以添加用于清除历史记录或位置栏条目的按钮。您甚至还可以添加弹出窗口按钮，以阻止页面从 Mozilla 打开弹出窗口。

许多首选项会立即生效。其他首选项可能需要您重启 Mozilla。

### 添加 Java 支持

如果您想显示某些 Java 内容，但只看到一个破碎的拼图块和一条失败消息，提示您需要插件来查看 application/x-java-whatever 内容，您可以从 Sun Microsystems Java 网站（www.java.com）安装所需的软件。方法如下：

1. 访问 www.java.com 并选择免费下载来下载 Java 2 运行时环境包。（寻找 Java RE 的 Linux RPM 包。我下载了 j2re-1_4_2-linux-i586-rpm.bin。）

2. 使该包可执行并执行它以提取 RPM，操作如下：

   ```bash
   $ chmod 755 j2re*-rpm.bin
   $ ./j2re*-rpm.bin
   ```

3. 以 root 用户身份安装 j2re* 包，就像安装任何软件 RPM 包一样。

   ```bash
   # rpm -Uvh j2re*rpm
   ```

4. 切换到 Java 插件目录，并从 Java 插件到 Mozilla 插件目录创建链接。（代替 *，您可以输入完整的 j2re 目录名称。）

   ```bash
   $ cd /usr/java/j2re1.4.2_05/plugin/i386/ms10-gcc32
   $ ln -s libjavaplugin_oji.so /usr/lib/mozilla/plugins/
   $ cd /usr/java/j2re*/plugin/i386/ms60/
   $ ln -s libjavaplugin_oji.so /usr/lib/mozilla/plugins/
   ```

5. 关闭任何打开的 Mozilla 窗口，然后打开一个新的 Mozilla 窗口。

6. 单击帮助 → 关于插件。您应该能看到 Java 插件的列表以及许多受支持的 Java MIME 类型。

7. 若要查看 Java 插件是否正常工作，您可以尝试 Java.com 网站（http://java.com/en/lifestyle/games/）上的一些游戏。

### 使用 Mozilla 进行酷操作

Mozilla 内置了一些很棒的便利功能，可以让您的浏览更加愉悦。以下是您可以尝试的一些功能：

### 使用标签式浏览

如果您在多个 Web 页面之间来回切换，可以使用标签式浏览功能同时在浏览器窗口中显示多个页面。您可以通过选择文件 → 新建 → 导航器选项卡或按 Ctrl+T 来打开新的选项卡。您还可以从 Web 页面或位置框调整标签式浏览的工作方式。方法如下：

1. 单击编辑 → 首选项。将出现首选项窗口。
2. 在导航器类别下单击标签式浏览。
3. 根据您希望使用标签式浏览的方式，单击以下一个或两个复选框：
   - **在 Web 页面链接上中键单击、Ctrl+单击或 Ctrl+Enter** — 选择此复选框可让您可以在新选项卡中打开指向其他 Web 页面的链接。若要使其生效，请在链接上中键单击，或在点击链接时按住 Ctrl 键并左键单击，或者（在选中链接时）按住 Ctrl 键并按下 Enter 键。
   - **在位置栏中按 Ctrl+Enter** — 在位置框中输入 Web 地址（URL）后，按住 Ctrl 键并按下 Enter 键，以便在选项卡中打开新页面。
4. 单击确定。您可以开始从 Mozilla Navigator 使用标签式浏览器功能。

每个带标签页面的选项卡都显示在导航器窗格顶部。若要关闭选项卡、创建新选项卡、书签一组选项卡或重新加载选项卡，请在窗格顶部的任一选项卡上右键单击。下拉菜单可让您选择所需的功能。

在新选项卡中打开链接的最简单方法之一是在 HTML 页面上的链接上右键单击。选择在新选项卡中打开链接选项。

### 使用 DOM 检查器

如果您正在调试正在创建的 Web 页面，文档对象模型（DOM）检查器对于检查页面结构非常有用。若要打开 DOM 检查器，请从 Mozilla 窗口中单击工具 → Web 开发 → DOM 检查器。

从 DOM 检查器窗口，输入要查看的 Web 页面的 URL。代表头部、主体、表格、字体等的节点将显示在左列中。每个节点的值显示在右列中。单击节点名称，下方页面上选定的区域会被高亮显示，节点值则显示在右侧。

### 调整 Web 页面大小

Mozilla 中有一个很棒的键盘快捷键，可以快速调整大多数 Web 页面上的文本大小。按住 Ctrl 键并按加号（+）或减号（–）键。网页上的文本在大多数情况下会相应地变大或变小。那个字体小得难以置信的页面突然变得可读起来。

### 使用 Mozilla Firefox

借助 Firefox Web 浏览器（见图 9-5），Mozilla 直接挑战了微软的 Internet Explorer。Firefox 轻量级（因此运行速度快），包含许多易用性

