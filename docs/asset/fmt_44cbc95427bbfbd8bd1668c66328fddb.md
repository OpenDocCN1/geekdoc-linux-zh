
@mozilla.org/registry:1 `nsRegistry`

@mozilla.org/registry-viewer:1 `nsRDFDataSource`

@mozilla.org/chrome/chrome-registry:1 `nsIXULChromeRegistry`:1

对于 Microsoft Windows 开发者来说，有对 XPCOM 项目特别受关注：

@mozilla.org/winhooks:1 `nsWindowsRegistry`

@mozilla.org/winhooks:1 `nsWindowsHooks`

这些接口提供了许多低级接口，以及第 16 章“XPCOM 对象”中涵盖的主要文件和网络管理接口，包括可以解压 ZIP 归包的接口。

剩下的只是关于 XPInstall 自身的对象的观察。Web 端对象 `InstallTrigger` 和 `installVersion` 没有实用的 XPIDL 接口定义。它们恰好与 XPCOM 基础设施一起注册了合约 ID（Contract IDs）。

@mozilla.org/xpinstall/installtrigger:1

@mozilla.org/xpinstall/installversion:1

@mozilla.org/xpinstall:1

在脚本中使用这些合约 ID 没有意义，因为没有可用的接口。`install.js` 脚本环境中提供的对象也没有暴露给 XPCOM。事实上，在后的情况下，这些对象甚至不存在合约 ID。

## 17.4 动手实践：打包 NoteTaker

本次“实操”环节将已经运行良好的 NoteTaker 打包成一个 XPI 文件，可以使用 XPInstall 进行安装。理论上，该工具可以直接从远程 Web 服务器运行，但将本地内容与基于服务器的叠加合并是一种混乱且违背常识的方法。从某种来看，它可能运行得不好。我们将坚持下载安装的方式。

尽管工具的运行代码已经完整，但还必须添加一些小细节。我们将它们全部整合在一起的策略是本章中提出的问题的总和。这意味着：

- 确定工具的名称。
- 确定发布文档的内容。
- 确定最终工具的内容。
- 创建下载页面、安装脚本和支持文件。
- 创建最终的 XPI 文件。

让我们过一遍这些任务。

### 17.4.1 发布准备

首先，我们为工具选择合适的名称：

- **文本名称。** 我们选择了“NoteTaker Web Notes”。我们将广告和推广工作留给提供该工具的 Web 页面。
- **包名。** 在一整本书中，我们一直使用“notetaker”，我们将继续沿用。这超过了极小 Windows 电脑支持的八个字符，但也许只是针对小电脑的问题。
- **注册应用名称。** 那是“Nigel McFarland/Note-Taker”。如果此工具被并入 Mozilla 浏览器的主开发流，名称可能仅仅是“NoteTaker”，会被附加到类似“mozilla.org/Browser/”的路径之后。在这种情况下，全称将是“mozilla.org/Browser/Note-Taker。”目前还没有这种关联。
- **版本号。** 到目前为止，该工具缺乏现实测试，但它看起来运行良好。将其称为版本 0.9。在详细说明时，该版本为 0.9.0.0。可以进行许多增强和修改，但可能会将版本推过 1.0。

我们还审查了要交付的软件。

- **基准。** 本书中讨论的所有内容都是该工具版本的基础。我在每个章节的目录下保留了与每个章节相关的代码副本，并进行每日增量备份、每周全备和每月备份。由于我在 30 号完成，今晚的备份将冻结一切。我的基准将是本书的源文件（第 1 版，作者最终定稿）、最终的可安装 XPI 文件以及一个备份日期。该备份还将包含任何测试文件和数据，这非常方便。

- **占用空间。** NoteTaker 工具的占用空间非常小。它包含三个项目：chrome 目录；Mozilla ；以及当前用户配置中的 `notetaker.rdf` 文件。

- **目标。** 软件的目标有几个部分。由于最近 XPCOM 对象（基于文件的流）的更改，这要求平台版本至少为 1.4。在 Mozilla Classic Browser 上经过测试是可移植的，因此操作系统并不那么重要；然而，注会有一些我们尚未识别的限制。平台版本和 Classic 应用程序套是整个目标，我们注意到未来版本不会被自动支持。

这就是所有所需的后勤工作。

### 17.4.2 创建支持文件和脚本

NoteTaker 0.9 版本需要应用程序代码之外的文件。
我们将为探索源码的开发者包含一个 `README.txt` 文件。
我们将根据上一个主题中的信息创建一个。
我们需要为 `notetaker/contents` 目录准备一个 `.rdf` 文件，并注册 NoteTaker 包。我们将使用第 2 章“XUL 布局”中指定的那个，并包含第 12 章“叠加层与 Chrome”中做的增强。
我们想展示本地化支持的试用。为此，我们需要 `contents .rdf` 文件和一个用于示例本地化的 DTD 文件。我们将使用第 3 章“静态内容”中的 `contents.rdf` 文件，并创建一个试用的 DTD 文件——这没有效果。
我们还想展示皮肤安装的试用。为此，我们需要一个 `.rdf` 文件和一个用于示例皮肤（主题）的 CSS 文件。我们将使用第 4 章“第一个小部件和主题”中的 `contents.rdf` 文件，并创建一个试用的样式表——这没有效果。
最后，我们需要安装支持。这等于一个 HTML 文件和两个脚本。NoteTaker 工具很小，几乎完全依赖平台和 Classic 应用程序。我们预计安装脚本是轻量级的而非复杂的。

```javascript
if ( schedule_files() != SUCCESS ) return getLastError();

if ( register_chrome() != SUCCESS ) return getLastError();
```

```javascript
return SUCCESS;
```

```javascript
rv = prepare();

if (rv == SUCCESS) {
  performInstall();
} else {
  alert("Installation failed. (Error = " + rv + ")\ncancelInstall(rv);
}
```

至于安装触发器，`install.js` 脚本是根据列表 17.2 的框架简化而来的。它没有需要检查的参数。我们假设只有在平台条件允许的情况下，安装触发器才会下载。由于 NoteTaker 工具是一个浏览器扩展程序，我们不需要添加菜单项或快捷键。NoteTaker 是一个如此小的工具，检查可用磁盘空间是没有意义的。由于该工具完全是用 JavaScript 编写的，我们没有任何需要管理的二进制可执行文件或二进制库。我们需要做的只是正确放置 XPI 文件的内容，并调整新 chrome 存在的平台。

为了完成最后几个步骤，我们需要知道 XPI 的内容。提前查看“最终绑定”，我们看到 XPI 包含：

```
install.js
notetaker.jar
extras/README.txt
extras/notetaker.rdf
```

整个应用程序位于 `notetaker.jar` 归文件中。`extras` 虚拟目录中的文件永远不会在运行时使用。`README.txt` 文件供好奇的程序员查找和阅读；`notetaker.rdf` 文件是用户数据库的初始副本。它需要被复制到用户配置文件中。

列表 17.7 显示了列表 17.6 中缺失的两个函数。它们对 XPI 文件和 chrome 注册执行所需的操作。

## 列表 17.7 从 install.js 部署文件并注册 chrome。

```javascript
function schedule_files() {
  addFile(TEXT_NAME, VERSION, "notetaker.jar",
  getFolder("Chrome", "notetaker.jar", true));
  addFile(TEXT_NAME, VERSION, "extras/notetaker.rdf",
  getFolder("Profile", "notetaker.rdf", true));
}
```

## 17.4 动手实践：打包 Note Taker

```javascript
return SUCCESS;
function register_chrome() {
  var jar_root = getFolder("Chrome", "notetaker.jar");
  registerChrome(PACKAGE | DELAYED_CHROME, jar_root, "content/notetaker/");
```
