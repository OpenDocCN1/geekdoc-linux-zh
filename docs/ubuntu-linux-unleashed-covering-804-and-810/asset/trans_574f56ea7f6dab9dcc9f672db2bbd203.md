

## NOTE

Ubuntu 允许访问 Firefox 3，但仅作为预览。你可以使用 synaptic 下载它，如果你好奇的话。

寻找和获取这些插件和扩展变得非常容易，因为 Mozilla 开发者友好地创建了一个专门帮助你从 Firefox 中获得更多功能的网站。特别受欢迎的是 Adblock Plus 和 StumbleUpon 插件。Adblock Plus 允许你清除那些令人讨厌的横幅和动画，它们在浏览时占用了大量带宽。StumbleUpon 是一个很棒的插件，它会根据你的偏好带你到网页上。但要警告一下，StumbleUpon 可能非常上瘾，你会浪费掉许多小时点击 stumble 按钮！

## Flash

你可以通过安装 flashplugin-nonfree 包轻松在浏览器中启用 Flash，可以使用 synaptic 或使用 apt-get。无论哪种方式，Ubuntu 都会下载其软件包，该软件包会进一步从 Adobe 获取官方软件包然后在你的系统上安装它。在尝试访问任何 Flash 启用内容之前，需要重新启动浏览器。

我们经常使用的另一个插件是 Google BrowserSync。如果你像我们一样在多台计算机上工作，那么你一定不得不在每台不同的计算机上重新创建书签并尝试保持它们一致。Google 通过允许你同步不仅书签，还包括 cookie、浏览器历史记录以及最终在多个浏览器中保存的密码，使整个过程变得容易得多。请记住你可以选择想要同步的内容，使其只需复制你的书签就变得容易。

## Konqueror

KDE 用户可以选择使用 Konqueror，它是 KDE 的默认浏览器（见图 5.2）。除了处理文件系统导航外，Konqueror 还可用于冲浪网络。它同样基于 Firefox 中找到的 Gecko 渲染引擎。

## Choosing an Email Client

在 Unix 的时代，有各种基于文本的邮件客户端，如 elm 和 pine（Pine Is Not Elm）。虽然它们看起来很基础，但它们使普通用户能够与他的邮件交互，既用于撰写也用于阅读通信。随着主流计算的到来以及人们需要友好 GUI 界面来提高生产力的认识，出现了大量邮件客户端，其中一些是跨平台的并且在 Linux、Windows 和 Mac OS X 之间兼容，更不用说 Unix 了。

![](img/8f9e74e2b343ff525bebfb720a3d8441_145_0.png)

**FIGURE 5.2** Konqueror, the standard KDE web browser.

## Evolution

Evolution 是随 Ubuntu 一起提供的标准邮件客户端，而称它为邮件客户端则严重低估了它作为应用程序的实用性。它不仅处理邮件，还可以负责联系人和日历管理，以及管理你的任务（见图 5.3）。下一节演示如何配置 Evolution 来处理邮件。

![](img/8f9e74e2b343ff525bebfb720a3d8441_145_1.png)

**FIGURE 5.3** With Evolution you can handle all your email and contacts, as well as make appointments and track tasks.

要成功配置 Evolution，你需要有以下信息：

- 你的电子邮件地址
- 你的传入邮件服务器名称和类型（即 pop.email.com，POP 和 IMAP）
- 传入服务器的用户名和密码
- 你的传出邮件服务器名称（即 smtp.email.com）

在你拥有所有信息后，你可以启动 Evolution。你呈现的第一屏是 Account Setup Assistance 屏幕，因此点击 Next 进入 Identity 屏幕（见图 5.4）。

![](img/8f9e74e2b343ff525bebfb720a3d8441_146_0.png)

**FIGURE 5.4** You can launch and configure Evolution with just a few simple commands. The Identity screen, the first of several screens, asks you to enter your information. Click Forward to proceed.

下一个屏幕允许你配置 Evolution 使用你的 Mail Transfer Agent。你可以选择 POP、IMAP、`/var/mail` 中找到的本地 spool 以 mbox 或 maildir 格式、本地 MTA，或 None 如果你只是想使用 Evolution 的其他功能。如图 5.5 所示，你也可以设置你的密码。

