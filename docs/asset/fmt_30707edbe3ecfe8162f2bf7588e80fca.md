
# IRC 和非 IRC 用户集成
IRC 和非 IRC 用户集成允许你将 IRC 服务器链接到 Scrollback 房间并接触非 IRC 用户，为他们提供进入你社区的入口。要配合 IRC 服务器使用 Scrollback，前往“房间设置 -> IRC 集成”。填入你 IRC 服务器的详细信息，然后点击完成保存。使用通道名称，将 `#` 替换为你输入的名称。完成后，你就可以在聊天窗口中看到消息了。

![](img/f2545dac69fdd8c1433ae8405b11b8_37.png)

## 房间设置

- 普通设置
- IRC 集成
- Twitter 集成
- 权限
- 垃圾信息控制
- 搜索可见性
- 讨论
- 分享与嵌入

## Twitter 集成
完成

取消

| 标签 | Scrollback 源 |
| :--- | :--- |
| 账户 | 取消 |

![](img/f2545dac69fdd8c1433ae8405b11b8_38.png)

Scrollback 与你的 Twitter 账户紧密集成。你可以直接从聊天窗口推文并分享聊天房间。首先通过 Twitter 集成标签，输入你想查看的标签并点击 Twitter 按钮。这就足够了：你现在可以在浏览器中查看所有标签。

简单来说，Scrollback 提供了这种最小化的聊天房间。

> 可能会发生不同的情况下讨论不同的事情。如果你关注 IRC 频道，这在那里是一个非常常见的场景。

如果聊天中有一个你想查看的消息，只需悬停在消息上显示右侧的菜单图标 - 你可以选择显示或隐藏消息。要分享你的房间视图，前往“分享”选项卡并点击“分享你的房间”下的按钮。

仅限单词，将显示预定义的词。你可以通过在“自定义屏蔽词/词汇”文本区域输入绝对词汇来列表进行添加。即使人们在聊天中输入绝对词汇，也不会打扰任何人。

将标签添加到你的设置以查看相关的邀请聊天房间

## 管理功能
你可以在普通设置下看到房间描述。Scrollback 的设计非常易于搜索，当你可以在聊天中发布时，非常适合描述房间属性。你可以选择任何一个、已登录的用户或聊天中的其他人。

## 讨论
聊天管理员有效地防止侵入性垃圾邮件和攻击行为。Scrollback 允许管理员轻松控制此类问题——启用“垃圾信息控制”标签，Scrollback 将自动阻止消息发布到你的房间。在账户标签中，你也可以设置屏蔽词列表。如果你启用“英语授权”

# Archon 教程

## 在 Linux 中运行 Android 应用
在您的常规 Linux 桌面中直接工作、游戏并享受丰富的 Android 应用。

![](img/f32545dac69fddf8c1433ae8405b11b8_39_0.png)

尽管 Google 的 Android 操作系统与桌面系统共享几乎相同的内核，但这些系统之间仍然存在巨大差异。如果不经过移植，Linux 应用无法在 Android 上运行，反之亦亦然。但得益于 Chrome 的商业成功，官方 Play 商店中有许多实用、酷炫引人注目的软件——其中许多是免费的。要在未运行 Chrome 的桌面电脑上运行这些应用并非易事。

## 01 安装一个合适的浏览器
从理论上来说，不仅是 Chrome，Chromium（开源基础）以及 Opera 或 Vivaldi 等衍生版本的效果也和 Chrome 一样好。Chrome 的开发速度非常快，这些浏览器可以基于不同的 Chrome 版本，带有不同的补丁集、Chrome 选项等。在现实生活中，你可能会遇到问题，这就是为什么我们建议在 Linux 上使用完全稳定的 Google Chrome 版本。

不久前，运行 Android 应用的技术出现了——这项允许通过 Chrome 浏览器运行无限数量的 Android 应用，前提是将它们转换为 Android 运行时支持的 `chrome-APK`。

Archon 最初被开发为将 Android 应用引入 Chrome OS 的解决方案，但后来被认为这已经足够了。当然，要运行这些应用，需要一些手动操作、技术调整以及对命令的熟悉。如果你遵循以下步骤操作，该程序将提供：

以下 Archon 将 Android 应用转换为 Chrome 浏览器的扩展。

![](img/f32545dac69fddf8c1433ae8405b11b8_39_1.png)

## 准备您的浏览器

![](img/f32545dac69fddf8c1433ae8405b11b8_40_0.png)

# 获取 Android 运行时
自 2014 年以来，Android 发布了从 1.0 到 2.1 的版本。多年来，Android Mif 处于不断变化的状态，而硬件保持不变。因此，不同的 Android 组合或 Android 版本可能并不是你需要的。默认情况下，选择是从 Google 提供的构建中安装 Android 运行时。对于当前的 Chrome 版本，作者已更新到 41.0 版本。

## 准备您的浏览器
Android 以 Chrome 扩展的形式分发，允许你获取一个带有扩展文件夹的 ZIP 文件。为了能够安装 Android 开发者模式，你需要找到最新版本，点击“扩展”选项。点击并导航到你下载 Android 程序包的文件夹。一旦你点击确定，它将启用 Android 开发者模式。下一步是在 Chrome 中配合 WebGL 使用它，这可以利用硬件加速图形并获得更好的浏览器性能。前往 `chrome://flags` 并查看是否有任何“software”字符串。如果有，请切换到 `chrome://flags` 并启用“Override software rendering list”（覆盖软件渲染列表）参数。

## 故障排除
Android 运行结果不符合预期？这里是发现问题所在并修复它的方法。

从用户的角度来看，你可以按照这些步骤轻松进行设置。首先，确保你正在 Chrome 中使用 Android 运行时。之后，确保在设置中已启用 Google Client。如果仍然失败，请检查以下项：

某些应用可能缺失或运行失败。要修复此问题，请转到扩展文件夹中的文件：`/locales/message.json` 并编辑它。它现在看起来应该是这样的：

```
{
  "notSupported": {
    "extensionName": "",
    "description": "Extension name",
    "message": "Whatever you like"
  }
}
```

另一个常见的警告消息是关于扩展目录的。尝试通过删除上面的 `key` 参数来修复它。

更多修复方法可以在 Android 项目的 issues 页面找到。Chrome 版本 - 在此处查找二进制文件：bit.ly/TecWu。

一旦你获得了应用程序的 Google Play 链接，你就可以启用导出其 API 文件。

## Archon 教程

```
atostoy: bash — Konsole
File Edit View Bookmarks Settings Help
atostoy@linux:~$ sudo npm install -g chromos-apk@latest
/usr/bin/chromos-apk -> /usr/lib/node_modules/chromos-apk/chromos-apk
chromos-apk@4.0.2/usr/lib/node_modules/chromos-apk
ncc@6.0.0
ncc-node-loader@0.0.1 (debug@0.4.7, adm-zip@0.4.7)
commander@2.7.1 (ansi-styles@1.0.0, escape-string@1.0.3, supports-color@
0.2.0,strip-ansi@3.0, has-ansi@1.0.0)
mkdir -p /home/atostoy/com.mapswithme.maps.prod.apk
Directory "com.mapswithme.maps.prod" created. 将该目录复制到 Chrome 并使用 "unpack extension" 加载应用。
atostoy@linux:~$ 
```

![](img/f32545dac69fddf8c1433ae8405b11b8_41_0.png)

## 06 将 APK 转换为浏览器
上面的 `chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。

`chromos-apk` 显示了用于转换（或解包）APK 并显示的节点。
