
诚然，新用户可能希望有一个`zoxide`安装程序来替代复杂的配置过程。更高级的用户可能希望有更多功能，例如将目录与特定应用程序关联。然而，一旦设置好，`zoxide`目前的形式是一个仅稍复杂的`cd`替代方案。用户可能希望将`zoxide`设置为`cd`的别名，通过在`shell`配置文件中添加`alias z='cd'`。使用`zoxide`，用户将节省数千次按键，这是一个既高效又经济改进。

## 信息

[1] `zoxide`: `https://github.com/ajeetdsouza/zoxide`

## 作者

`Bruce Byfield`是一位计算机记者，也是专门从事自由和开源软件的自由撰稿人和编辑。除了他的写作项目外，他还教授免费和电子学习课程。在空闲时间，`Bruce`撰写关于西北海岸艺术的内容（`http://brucebyfield.wordpress.com`）。他也是`Preamble Pieces`的联合创始人，这是一篇关于写作和幻想的博客，位于`https://preamblepieces.com/`。

![img](img/d6d2a4cd4a2f445e8c9e8079857e2469_38_0.png)

图 1：当目录包含相似名称时，`zoxide`提供一个可选的列表。

## 通过特辑磨练你的技能！

在我们的特辑库中了解`Shell`、`LibreOffice`、`Linux`等内容。

*Linux Magazine*（`Linux`杂志）团队创建了一系列单册，让你深入探讨感兴趣的主题。

可提供印刷版或数字版。

**查看完整库：** `shop.linuxnewmedia.com`

![img](img/d6d2a4cd4a2f445e8c9e8079857e2469_39_0.png)
![img](img/d6d2a4cd4a2f445e8c9e8079857e2469_39_1.png)

## 创客的动手项目

**复古计算**

使用`Commodore OS`进行点击操作

基于`FPGA`的`Spectrum`测试

## 智能家居

- 自动化你的植物照料
- 低代码编程
- 学习`Node-RED`
- 并添加类型

## 构建信息显示屏

## 301 条最佳 Bash 命令

## LINUX SHELL 手册

## 提升你的 Linux 技能

指尖掌控强效

## 加入 Linux 革命！

你需要的所有软件

## Linux 入门

**了解如何设置**

- 听音乐
- 玩游戏
- 浏览网页

## 创客的动手项目

**TINY BITE**

色彩驱动的信息

构建电池舞蹈，使用带供电的`Pi`信息

...gation Innovation

...our plans without

## 创客空间

## 酷炫的 Linux 技巧

**给 Linux 极客的窍门和快捷键**

- 在你的 `Linux` 桌面上将 `macOS` 作为虚拟机运行
- 让 `AI` 帮助你执行 `Shell` 命令

**114 个技巧**

内含 DVD！

`LibreOffice`

完整版本

深入探索世界最棒的免费办公套件

## LibreOffice 专家

## Linux 最佳精选

## LINUX MAGAZINE

**来自 Linux 专家的高级技巧：**

- 更流畅的操作
- 更好的安全性
- 更智能的工具
- `Zint`
- 生成你自己的条形码
- `Node-RED`
- 无代码编程
- `C-Shell Genie`
- 使用自然语言和 `shell` 命令
- 拼贴画为 `Linux` 工具和照片添加内容
- `ChatGPT` 客户端全在 `Linux` 命令行上

## 编辑并保存为 Office 文件

## 替代 Microsoft Office 和 Google Docs！

**LibreOffice**

包含适用于`Windows`、`macOS`和`Linux`的完整版本

**全新！**

订阅 `Linux Magazine`
`www.linux-magazine.com`

![img](img/d6d2a4cd4a2f445e8c9e8079857e2469_40_0.png)
![img](img/d6d2a4cd4a2f445e8c9e8079857e2469_41_0.png)

## 使用 Tampermonkey 自定义网络内容

### 猴子生意

网页中微小的变化也能改善浏览体验。你首选的浏览器提供了注入`JavaScript`以调整页面所需的所有工具。你只需要一个带有调试工具的浏览器、一些脚本知识以及浏览器扩展`Tampermonkey`。

作者 `Reinhard E. Vogelmaier`

浏览器已成为与互联网交互的重要组成部分。近年来，浏览器已经从仅仅是一个交互静态`HTML`的工具，演变为基础设施的综合组成部分。现代浏览器是操作系统中的操作系统，拥有`JavaScript`、`HTML`和`CSS`的完整`SDK`，以及可视化调试器、代码检查器、网络和工作负载监控选项等功能。一个有趣的功能是，你可以使用自己的脚本修改已加载到浏览器中的页面。自定义网页的能力适用于：

- 内网应用的快速 `bug` 修复
- 修复网站或 `Web` 应用程序的恼人行为
- 为企业用户实现安全功能
- 为公共可用的网站添加便捷的新功能，如自动化工具或类似功能
- 提供对基于 `AI` 工具的轻松访问

这种灵活性和强大功能将浏览器推向了远超其原始角色（仅仅渲染 `HTML`）的领域。

**在我开始之前...**

本文仅用于教育目的。我的目标是向你展示所描述技术的威力。你将在这里找到的所有信息在互联网上已经可得 – 链接在文章末尾提供。与许多用于编程的工具一样，这些工具也可以用于非法活动。如果你决定进行实验，遵守所有适用法律并以符合网站预期使用方式的方式对待任何网站是你自己的责任。

**欢迎进入 DOM 世界**

当今网络的一个非常令人兴奋的功能是`HTML`文档与文档本身包含的脚本之间的连接。你可以将这个结构类比为鸡和蛋的问题：文档包含脚本，而脚本可以修改文档，包括脚本本身。允许这一点的技术是`DOM`（文档对象模型）[1] [2]。当网页加载时，浏览器构建一个`DOM`树，它是文档内容的层次表示。这种树结构允许高效地选择、添加、删除和修改网页上的元素。`DOM`不绑定到任何编程语言；然而，`JavaScript`通常用于与`DOM`交互。

样式表（`CSS`）也是`DOM`的一部分。样式表描述了文档在浏览器中如何显示（字体、颜色等）。浏览器最有趣的功能之一是用户可以向`DOM`注入代码。这段代码可以与文档的`HTML`和`CSS`部分交互。这一功能开启了一个充满可能性的世界。

### Tampermonkey

**列表 1: manifest.json**

```json
{
  "manifest_version": 2,
  "version": "1.0",
  "name": "Hello World!",
  "content_scripts": [
    {
      "matches": ["*://*.per1.org/*"],
      "js": ["main.js"]
    }
  ]
}
```

**列表 2: main.js**

```javascript
const btn =
document.createElement('button');
btn.textContent = "ClickMe";
btn.onclick = function() {
alert("Hello World!");
}
alert("JavaScript loaded!");
document.body.appendChild(btn);
```

被称为 `main.js`（列表 2）。脚本位于与 `manifest` 文件相同的目录中。

这个脚本并没有做太多事情，但它很好地说明了什么是可能的。你为所有匹配域名 `per1.org` 的页面添加一个按钮。你还定义了当按钮被按下时要执行的新 `JavaScript` 函数。为了简单起见，该函数仅执行 `alert` 函数。

现在你只需要将扩展加载到你的浏览器中。打开链接 `about:debugging#/runtime/this-firefox`。点击“`Load Temporary Add-on`”按钮并加载 `manifest.json` 文件。从现在开始，在此浏览器实例中打开的所有来自 `per1.org` 域名的页面都将包含一个全新的 `ClickMe` 按钮。你成功地修改了 `DOM`，并添加了一个在用户点击 `ClickMe` 按钮时执行的功能。如果你有兴趣了解有关创建扩展的更多信息，请在线查找 [3] [4]。

### 扩展浏览器

将代码集成到 `DOM` 中很容易。考虑经典的“`Hello World`”示例来演示这一过程。你需要一个名为 `manifest.json` 的文件（列表 1）和至少一个程序文件。`manifest.json` 概述了若干细节，如插件的名称、版本，以及对我们来说重要的，插件应插入的网页 URL（在这种情况下，`per1.org` 域名的所有 URL）。
