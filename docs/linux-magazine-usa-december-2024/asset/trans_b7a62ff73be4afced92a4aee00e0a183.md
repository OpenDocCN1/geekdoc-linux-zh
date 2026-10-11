
以及其他操作系统上。如果您的浏览器支持，您还可以使用不同的浏览器扩展。

## 安装 Tampermonkey 扩展

Tampermonkey 的安装非常简单。在 Firefox 中，选择**添加扩展和主题**，然后在左侧菜单中选择*扩展*。搜索 Tampermonkey，点击 Tampermonkey 图标进行安装。扩展的提供商会要求您接受关于隐私的必要条款（图 1）；您应该仔细阅读该文本，然后选择授予提供商哪些权限。通过监控网络流量，您会注意到，扩展提供商不仅会收到您安装了其扩展的通知，还会收到您每次使用它时的通知。一旦您接受这些条款，扩展就会安装。

## 让我们开始吧

当您第一次打开 Tampermonkey 时，它会礼貌地询问您是否允许将其使用情况的匿名统计数据发送回其开发者。是否允许这取决于您。之后，您可以编写一个新的用户脚本。点击**创建新脚本...**。Tampermonkey 会为您的新用户脚本创建一个骨架，并在 Tampermonkey 编辑器中显示它。您会发现与之前示例中在清单文件中配置的相同元信息。我将重用之前创建的“`Hello World`”示例作为插件。在图 2 中，您可以看到该脚本，您只需在点击*文件*时弹出的菜单中保存它即可。结果与之前相同，这让人对之前操作的正确性有一定信心。

## 同样的玩法与 AI . . .

对于更具挑战性的示例，有些人更喜欢使用 Invidious 前端 [7] 来访问 YouTube 视频。当然，谷歌对 YouTube 存在一个不允许谷歌追踪的替代开源前端并不高兴，他们已要求开发者下架 Invidious。在过去几个月里，谷歌一直在积极致力于关闭 Invidious，因此当您阅读此内容时，这个示例可能不会给出这里所示的结果。在这种情况下，我仅仅是用这个示例作为展示如何在搜索结果列表中用其他内容替换搜索引擎链接的一种方式。

假设您不想花时间自己编写代码。您可以使用您喜欢的 AI 聊天工具（在本例中为 www.phind.com），并要求友好的机器人执行以下操作：“请编写一个用户脚本，在 DuckDuckGo 的所有搜索结果中将 YouTube 替换为站点名称 invidious.private.coffee。” Phind 提供了一个整洁的小脚本（列表 3），其中包含了让 Tampermonkey 正常工作所需的所有信息。Tampermonkey 执行语法检查，如果检测到语法错误会抱怨。保存脚本并使用 DuckDuckGo 进行搜索；例如，查找 Tampermonkey 安装教程。

我尝试这个任务的第一次似乎没有成功；所有指向 YouTube 的视频链接均未改变。事实证明，时序至关重要：当脚本执行时，页面尚未完全加载，因此无法替换其中包含的链接。添加一个简单的监听器解决了这个问题：

```
window.addEventListener('load', replaceYouTubeLinks);
```

当我再次尝试时，搜索显示的是指向 Invidious 的链接，而不是 YouTube。该脚本的更新版本见列表 4。

您甚至可以将链接替换为在用户点击时执行的功能。例如，此功能可以查询应避免的链接黑名单，并在找到匹配项时通知用户。同样，请向您喜欢的 AI 聊天机器人索取代码。

请允许我发表评论：您的浏览器、JavaScript 和 Tampermonkey 是非常强大的工具。您应该知道自己在做什么 - 否则事情可能会迅速变得复杂。

### 列表 3：替换 YouTube 链接

```javascript
// ==UserScript==
// @name		Replace YouTube Links on DuckDuckGo
// @namespace	http://tampermonkey.net/
// @version		0.1
// @description	Replaces YouTube links with invidious.private.coffee in DuckDuckGo search results
// @author	Your Name
// @match	https://*.duckduckgo.com/*
// @grant	none
// ==/UserScript==

(function() {
'use strict';

// Function to replace YouTube URLs with invidious.private.coffee
function replaceYouTubeLinks() {
const links = document.querySelectorAll('a[href*="www.youtube.com"]');
links.forEach(link => {
link.href = link.href.replace(
"www.youtube.com", "invidious.private.coffee");
});
}
})();
```

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_43_0.png)

### 列表 4：替换 YouTube 链接 2.0

```javascript
// ==UserScript==
// @name        Replace YouTube Links on DuckDuckGo
// @namespace    http://tampermonkey.net/
// @version      0.2
// @description  Replaces YouTube links with invidious.private.coffee in DuckDuckGo search results
// @author       Your Name
// @match        https://*.duckduckgo.com/*
// @grant        none
// ==/UserScript==

(function() {
    "use strict";

    // Function to replace YouTube URLs with invidious.private.coffee
    function replaceYouTubeLinks() {
        const links = document.querySelectorAll("a[href*='www.youtube.com']");
        links.forEach(link => {
            link.href = link.href.replace(
                ("www.youtube.com", "invidious.private.coffee")
            );
        });
    }

    // Wait until the page has been loaded
    window.addEventListener('load', replaceYouTubeLinks);
})();
```

## 另一种方法

在编程世界中，有一句话：“完成一件事的方法不止一种！”我将向您展示让脚本运行的第三种方法。如果您打开 Tampermonkey 扩展，您会在菜单中看到“查找新脚本”选项。此选项打开一个新菜单，其中包含指向提供大量现成用户脚本的网站链接。您可以进行搜索以查找符合您需求的脚本。但请做好准备：这些脚本可能有效，也可能无效。可能有人是面向不同的扩展（例如 Greasemonkey）或您正在使用的扩展的不同版本编写的脚本。此外，正如前面的示例所示，时序可能会影响操作。因此，在使用这些脚本之一之前，您应该理解您正在做什么。

## 探索 DOM

当您查看从 Web 服务器获取的文本时，您肯定会因某些页面的复杂性而感到困惑。浏览器 SDK 可以帮助您。在 Firefox 中，导航到您计划更改的 Web 页面上的元素，并用鼠标右键点击。菜单弹出；菜单中的最后一个选项是检查。点击“检查”，此时会打开此 SDK 的界面（图 3）。当您将鼠标悬停在页面本身的 HTML 代码上时，相应的元素会被突出显示。此功能帮助您找到想要在 DOM 中更改的元素。

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_44_0.png)

## 测试您的代码

浏览器 SDK 有助于测试您的代码。考虑一下“Hello, World”示例。按 F12 打开 SDK。SDK 打开后，点击控制台选项卡。现在，您可以在控制台中输入想要测试的代码。从列表 2 中的程序开始输入。当您在 `const btn = document.create(‘element’‘button’);` 这一行输入时，您会注意到（在输入 `document` 后的点后）SDK 为您提供自动完成，这非常有帮助。完成按钮的定义后，您可以使用 JavaScript 探索您创建的内容，或者使用以下一行将新创建的按钮插入网页：`‘document.body.appendChild(btn);’`（图 4）。新创建的按钮将弹出在网页上。

## 3D 家具模型

建模您的家可能有点棘手。您会发现一些优秀的开源程序可以帮助您，例如 Blender。但是，许多家具供应商也提供其产品的 3D 模型。例如，IKEA 提供大量产品的 3D 模型以及在线可视化工具。

如果您探索这些页面的 DOM，您会发现使用了一个小的 JavaScript 程序（列表 5）来打开扩展名为 .gltb 的 3D 文件 – 这是一种免版税的编码 3D 数据的方法。像 Blender 这样的工具可以轻松使用此数据来帮助您建模您的家。查看带有 3D 建模的 IKEA 产品网页，您会发现*查看 3D*按钮调用一个脚本，其中包含您想要下载的 3D 模型作为参数。

凭借这些信息，您可以轻松下载模型。然后，您可以直接将模型导入 Blender。

但是，要在 SDK 的 HTML 区域中右键点击以找出 .gltb 文件的 URL 并不是很方便。一个简单的用户脚本可以协助您。您知道函数的名称，并且可以在函数的帮助下在 DOM 中搜索它 `document.querySelector`。一旦找到该函数，您只需使用其参数中的 URL 来发现获取 3D 模型的位置。

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_45_0.png)

**图 4：在控制台中执行 JavaScript 示例。**

既然您已经知道如何获取 3D 模型的 URL，您只需要创建一个可点击的按钮来让您下载此 URL（图 5）。您可以使用 JavaScript 函数 `‘create(‘element’‘button’ )’` 来完成这一步。执行此奇迹的用户脚本在 GitHub 上可用 [8]。我建议您下载该脚本并仔细阅读 – 您将从一个非常短的代码片段中学到很多。

## 网络安全

将您在互联网上找到的用户脚本下载到 Tampermonkey 可能相当危险。正如我之前提到的，您安装的用户脚本可以在您加载到浏览器的每个页面上运行。每个脚本都可以控制您的浏览器和所联系服务器之间的所有通信。它们代表您行事，可以代表您做您可能甚至注意不到的事情。

显然，这同样适用于您安装到浏览器的任何扩展。因此，重要的是只安装您信任的脚本，以及只安装您信任的浏览器扩展。扩展应只从您的浏览器提供商的官方发行版安装。

您会在互联网上找到这样的声明：Tampermonkey 等工具允许没有编码经验的人使用强大的脚本。这是一个非常不好的主意。只有当您完全理解这些脚本在做什么时，才安装用户脚本。不要使用包含您不完全理解的代码的脚本。代表您执行有害操作的脚本代码可能被混淆，除非您仔细查看并知道您正在看什么，否则很难察觉。最安全的脚本是您自己开发和测试的脚本。同样的建议也适用于扩展。

与其信任浏览器发行版网站上的脚本，为什么不创建自己的扩展呢？这比您想象的要容易。您可以像使用用户脚本一样用 JavaScript 编写代码。

您还可以选择将 Tampermonkey 用作开发目的的沙箱，一旦您开发了健壮的用户脚本，然后将整个应用程序转换为扩展的形式。

顺便说一句：我希望您不要使用常规浏览器进行在线银行业务，而是为此目的使用专门加固的浏览器。

### 列表 5：获取 3D 模型

```html
<script type="application/json" id="pip-xz-viewer-model">
{  "productId":"<productId>",
"productName":"<productName>",
"url":"<URL 3D Model1>"}
</script>
```
