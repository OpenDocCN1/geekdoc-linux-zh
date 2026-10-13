
你可以更改 Netscape Navigator 的外观和行为。大多数更改都可以在偏好窗口进行，通过点击 `Edit` > `Preferences` 可以打开它。偏好窗口出现如图 9-6 所示。

在每个类别（导航、漫游用户、外观、高级、创作器以及邮件和新闻组）中，都有几个可以更改的偏好页面。（邮件和新闻组偏好将在在本章稍后描述。）点击每个类别旁边的箭头以查看每个类别可用的偏好页面。

> 当你设置个人偏好时，更改会写入 `$HOME/.netscape` 目录下的文件。不要直接编辑这里的文件！因为它们会从 Netscape 菜单和窗口更新，当你下次从 Netscape 窗口更改某些内容时，你所做的任何更改将被覆盖。

# 第 9 章 使用互联网和 Web 的工具

![](img/176fafece2d30daee750bc078e898ee4_330_0.png)

图 9-6：从首选项（Preferences）窗口更改 Netscape 的外观。

## 设置主页

主页是你点击 `Home` 按钮时 Netscape Navigator 窗口中显示的 Web Page。在 Red Hat Linux 中，Netscape Navigator 首次启动时默认会显示“Welcome to Red Hat Linux”。

大多数人会选择设置一个经常返回的主页（使用包含他们喜爱的标题、搜索引擎或天气预报的页面）。要从首选项窗口设置自己的主页，请点击 `Navigator` 类别。点击 `Browser starts with Home Page`。然后输入你想作为起始页的地址 URL 并点击 `OK`。

## 漫游访问

如果你在别人的计算机上使用互联网，可以利用漫游用户（Roaming User）功能让 Netscape 通过网络启动并加载属于你个人的偏设置。在使用此功能之前，必须在 LDAP 服务器中配置你的个人信息。LDAP 代表轻量级目录访问协议（Lightweight Directory Access Protocol）（网络管理员可以帮助你完成）。

要启用漫游访问，点击首选项窗口中的 `Roaming User` 类别。选择 `Enable Roaming Access for this Profile`，然后输入与漫游访问账户关联用户名。接下来，点击 `Roaming` 旁边的向下箭头并选择 `Server Information`。在此页面，你可以选择 LDAP 目录服务器并输入服务器地址和你的 User DN（即你的用户名）。接下来，点击 `Item Selection` 页面并选择要下载的用户配置项目。

## 更改 Netscape 的外观

要更改 Netscape 的外观，可以更改显示的工具栏，以及使用的字体和颜色。工具栏可以以 `Pictures and Text`、`Pictures Only` 或 `Text Only` 的形式出现。要更改工具栏显示，请在首选项窗口中选择 `Appearance` 类别，然后选择显示的一种外观类型。

Web 通常不是选择特定的字体，而是对标题、段落和特征（斜体、`粗体` 等）进行标记，从而使用浏览器的默认字体。你可以从 `Fonts Preferences` 页面更改 Netscape 窗口使用的默认字体。（要进入字体页面，点击 `Appearance` 菜单项旁边的向下箭头，然后选择 `Fonts`）。默认的可变宽度是 `Times (Adobe)`，默认的等宽字体是 `Courier (Adobe)`。你还可以更改每个字体的大小（默认为 12 磅）。

如果 Web 页面指明使用了特定字体，Netscape 将使用这些字体而不是默认字体。如果你想使用默认字体，可以在首选项页面上点击 `My Default Fonts`。你也可以通过选择该选项禁用动态字体（`Dynamic Fonts`）（动态字体加载速度较慢，因为它们必须经过渲染，而不仅仅是显示。）

Netscape 使用的默认颜色使文本为黑色，背景为白色。你尚未访问过的链接是浅蓝色，而访问过的是深蓝色。此外，链接带有下划线。你可以从 `Colors Preferences` 页面更改任何颜色（点击 `Appearance` 下向箭头然后选择 `Colors`）。点击你想更改的颜色，在 `Color Picker` 窗口中选择新颜色（从色板中或通过移动红、绿、蓝 (`RGB`) 滑块来制作你所需的颜色）。

## Netscape 的行为

有若干项偏好可以控制 Netscape 在某些情况下的反应（例如包含某些类型的数据或获取接受 cookie 的请求）。如果你拨互联网连接非常慢，或者对安全有所疑虑，可以在 `Advanced Preferences` 页面更改其中一些设置。要进行此操作，点击高级向下箭头进入 `Advanced Preferences` 页面。以下是可以更改的一些安全设置：

- `Automatically load images and other data types` ——通常勾选此项后，页面上的图像将会显示。如果你互联网连接很慢，点击此项取消勾选。
- `Enable JavaScript` ——通过 Java 和 JavaScript，Web 作者可以添加更像程序（表单、计算和其他功能）而不是文档（标题、图像和文本）的内容。尽管 Java 是安全的（这些程序无法获取 `/etc/passwd` 文件），但它可以访问计算机的更多区域。此外，Java 有时运行缓慢。你可以通过取消选择那两个按钮来禁用 Netscape 窗口中的 Java 和 JavaScript。

![](img/176fafece2d30daee750bc078e898ee4_332_0.png)

如果你禁用了 Java 和 JavaScript，你将丢失 Web 页面上的大量内容。然而请注意，JavaScript 代表安全风险。在输入密码或个人信息之前，请确保 JavaScript 内容来自可靠源。
- `Enable JavaScript for Mail and News` ——JavaScript 也可以包含在邮件和新闻组消息中。你可以通过取消选择此按钮来关闭它。
- `Enable Style Sheets` ——样式表可以为 Web 设计师创建一个模板，使一组页面具有相同的样式，而无需为每个页面创建大量的 HTML。我可能
- `Wait for images to load` ——启用后，Netscape 将等待所有图像下载完成后显示页面。如果你的连接缓慢，你可能想取消选择此项以便立即查看文本。
- `Check for software updates` ——这允许 Netscape 检查浏览器的版本。如果你不想被频繁提示，可以禁用此项。
- `Cookies` ——Cookie 是网站放在你计算机上的小文件，用于存储你访问的信息。你可以在隐私设置中启用、禁用或删除 cookie。

## 使用互联网和 Web 的工具

如果你不介意文本界面，或者你是一个喜欢使用 `sort`、`grep`、`troff`、`col` 并能够接收电子邮件的 UNIX 用户，那么仍然有很多类 UNIX 的邮件工具。`mail` 命令本身为发送给你 UNIX 系统上或局域网内其他用户的纯文本消息提供了一个易用的界面。还有基于文本的邮件应用程序，例如 `mut` 命令，它可以让你能够处理邮件附件。

在介绍了一些电子邮件基础知识后，本节将引导你完成使用 Netscape Messenger 电子邮件的步骤。如果你对基于文本、命令行驱动的邮件工具感兴趣（其中某些工具已经在 UNIX 系统中存在了多年），本节也包含了对其中许多命令的描述。

### 电子邮件基础知识

电子邮件是计算机网络最古老的用途之一——比 Web 早了 20 多年。事实上，当互联网仅连接了几台计算机时，电子邮件就是用于在互联网上传输信息的最早应用程序之一。

今天，全球有数百万用户拥有电子邮件地址。尽管有几种不同的电子邮件地址格式，但目前为止最流行的电子邮件地址格式是域名风格地址（用于互联网和其他 TCP/IP 协议）。电子邮件地址由用户名和域名组成，用 `@` 符号隔开。以下是一个示例：

```
webmaster@handsonhistory.com
```

作为电子邮件的使用者，你需要一个程序（如 Netscape Messenger）让你能够获取邮件、管理邮件并发送消息。虽然邮件消息最初只是纯文本，而且在今天大多数情况下仍然如此，但有一些较新的功能可以让你增强可以发送和接收的内容类型。增强邮件消息有两种方法：

- `Attachments` ——你可以向邮件消息中添加信息文件。这些附件可以包含你通常无法在邮件消息中保存的数据，例如二进制程序、文字处理文件或图像。邮件附件的接收者可以将文件保存到本地磁盘，也可以在设计用于读取附件的程序中打开它。
