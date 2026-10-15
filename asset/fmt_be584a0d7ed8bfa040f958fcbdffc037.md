
图 1.4 显示了 Windows 上 chrome 目录的典型示例。

![](img/319913ee3703286e2c03d285f49c7_57_0.png)

图 1.4. Windows chrome 目录。

此截图显示了带有 `en-US`（美国英语，默认）和 `fr-FR`（标准法语）本地化的 Mozilla 安装。Mozilla 自动生成了 `overlayinfo` 目录和单独的文本文件；这些也可以手动编辑。

- `chrome.rdf` 是所有 JAR 文件的文本数据库。
- `toolkit.jar` 包含了构成“全局” chrome 内容的通用工具。
- `classic.jar` 包含经典皮肤（skin）。
- `messenger.jar` 包含 Mail & News 客户端。
- `comm.jar` 包含普通 Web 窗口和 HTML 编辑器的 chrome。

这些文件名称似乎暗示了某种模式，但并非严格如此。这仅仅是一种 JAR 命名规范，将包和组件分开。并不是强制使用 JAR 文件——文件可以以未压缩和未归档的形式存储在 `chrome` 目录的任何地方。第二种命名规范适用于 `chrome` 下的目录结构。如果不，平台的某些功能将无法工作，因此该规范更为重要。图 1.5 显示了这种种规范的示例。

此 `chrome` 目录包含两个应用程序包，`packageA` 和 `packageB`。最重要的目录带有下划线：`content`、`locale` 和 `skin`。`content` 包含应用程序。`locale` 包含语言特定的

### 1.6 动手实践：启动平台

![](img/319913ee3703286e2c03d285fbfc49c7_58_0.png)

图 1.5 跨平台的 Chrome 子目录。

应用程序的元素。`Skin` 包含应用程序中特定主题的元素（装饰性信息）。通过将应用程序拆分为这三个组件，应用程序可以在不同的语言和主题之间复用。在这些目录下，子目录可以像 `subdir` 示例那样根据你的需要进行深层嵌套。

如果你检查任何 JAR 归包内部的文件，你会发现它们分布在这个标准的目录布局中。因此，`modern.jar`（一个包含现代皮肤的 JAR 文件）仅持有 `skin` 子目录的文件，而 `locale.jar`（JavaScript 引擎）则贡献于所有顶层 chrome 目录。JAR 文件内部的目录略有反转，因此与图 1.5 的层次结构不匹配。这样做是为了加快搜索 JAR 文件的速度。如有必要，Mozilla 会自动将这些标准目录转换回图 1.5 所示的结构。

所有这些命名和结构约定都可以完全忽略，但代价是两个：首先，你的应用程序可能会变成一团乱麻。Chrome UI 经过了彻底修改以获取当前主题和当前区域。如果你的 `MyTheme` 和 `Locale` 文本不在正确的目录中，它们可能会因为硬编码而显示，但当当前主题或区域切换到 `MyTheme` 或 `Locale` 时，它们不会对 chrome 系统做出响应。

关于此，图 1.6 显示了应用程序内部的一个片段。

从这张截图可以明显，chrome 应用程序可能很大——这个 JAR 文件扩展到 1.5 MB（兆字节）源代码。该 JAR 文件中的 JavaScript 脚本几乎有 100 KB（字节）。这些文件中的任何一个都不需要编译；它们在 Mozilla 中按原样运行。

### 基础概念 第 1 章

`WinZip`: `messenger.exe`

| 名称 | 类型 | 大小 | 比例 | 签出 | 向导 | 路径 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| messenger.exe | 应用程序 | 81,512 | 62% | | | messenger(address_book) |
| addressbook.exe | 应用程序 | 13,328 | 10% | | | messenger(address_book) |
| CertDecl.dll | 库 | 1,702 | 47% | | | messenger(address_book) |
| CertOverlay.dll | 库 | 3,227 | 53% | | | messenger(address_book) |
| CertVerify.dll | 库 | 6,507 | 76% | | | messenger(address_book) |
| CryptoFile.dll | 库 | 5,134 | 51% | | | messenger(address_book) |
| CrashProg.exe | 应用程序 | 5,577 | 67% | | | messenger(address_book) |
| DataFile.dll | 库 | 2,368 | 56% | | | messenger(address_book) |
| EditDlg.dll | 库 | 1,518 | 47% | | | messenger(address_book) |
| EmailEngine.dll | 库 | 16,972 | 72% | | | messenger(address_book) |
| EncrEngine.dll | 库 | 2,523 | 58% | | | messenger(address_book) |
| FileMenu.dll | 库 | 4,968 | 65% | | | messenger(address_book) |
| GetAddress.dll | 库 | 12,519 | 71% | | | messenger(address_book) |
| GetAddress.exe | 应用程序 | 10,516 | 86% | | | messenger(address_book) |
| Help.exe | 应用程序 | 28,312 | 96% | | | messenger(address_book) |
| Info.dll | 库 | 3,468 | 70% | | | messenger(address_book) |
| HtmlFile.dll | 库 | 1,118 | 35% | | | messenger(address_book) |
| HtmlStyle.dll | 库 | 5,885 | 80% | | | messenger(address_book) |
| Post.exe | 应用程序 | 3,101 | 60% | | | messenger(address_book) |
| RegFile.dll | 库 | 3,434 | 75% | | | messenger(address_book) |
| RegisterFiles.exe | 应用程序 | 2,480 | 60% | | | messenger(address_book) |

地址录中与 `main.exe` 最相对应的文件是 `addressbook.xml` 文件。它是 Mozilla 功能发挥作用的良好示例。如果你查看此文件，获得 XML 经验，并发现以下通用项目：使用 `<xml-overlay>`、`<xml-stylesheet>` 和 `<script>` 的 XML 标记来包含其他文件；对 DTD 和实体处理程序的使用。

#### 1.7 调试角：从外部调试

设置 NoteTaker 所需的步骤是创建一些目录并将名称 `notetaker` 注册为官方的 Mozilla chrome 程序包。作为一个官方包，它可以通过 `chrome:` URL 方案进行访问。以下是关于目录的说明：

- 1. 在 Mozilla 安装区域，将当前工作目录更改为 `chrome` 目录。
- 2. 创建名为 `notetaker` 的子目录并进入该目录。
- 3. 创建名为 `chrome`、`locale` 和 `skin` 的子目录。
- 4. 在 `locale` 内部创建一个 `en-US` 子目录。
- 5. 在 `skin` 内部创建一个 `classic` 或 `modern` 子目录，或者两者都要。

包注册在 `chrome/install-chrome.txt` 文件中完成。要将 NoteTaker 注册为 chrome 包“notetaker”，请在该文件的末尾添加此行并重启程序。

```
content,install.url:://chrome/notetaker/content/
```

此语法非常脆弱，必须按照所示完全添加。在应用程序端，此时不需要进行其他操作，尽管我们将会经常访问这些目录。建议你也遵循后续“调试角”部分中的建议。

#### 1.7 调试角：从外部调试

Mozilla 是一个相当复杂的系统。如果你没有正确配置它，实现运行的应用程序将变得困难。每一个 bug 的修复都会减少神秘问题的数量，但最好从一开始就为成功做好准备。
