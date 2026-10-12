
此行通常放在主文档的顶部，`<?xml?>`头之后。如果添加了这样一个标签，则指定的文件将按相同的顺序合并。如果重复指定同一个文件，它会被合并两次。指定的覆盖层文件不需要位于`chrome`中。

自上而下覆盖层的简单示例可以在 JavaScript 控制台的代码中找到。查看`chrome`中`toolkit.jar`中的`console.xul`。一个更复杂的示例是`chrome`中`comm.jar`中的`navigator.xul`。它是整个 Classic Browser 的主文档。这些示例中包含的并非覆盖层都是自上而下指定的，但有几个是。

## 12.1 覆盖层 (Overlays)

如果使用`<?xul-overlay?>`来加载非覆盖层文档，Mozilla 可能会产生混乱并冻结或崩溃。

### 12.1.2 自底而上 (Bottom Up)

自底而上的覆盖层方法不使用`<?xul-overlay?>`处理指令。相反，Mozilla 通过查询`chrome`中的数据库来决定合并哪些文档。自底而上的系统要求主文档和覆盖层文档都安装在`chrome`中。

这种替代方案使得 Mozilla 应用程序具有可扩展性。添加到`chrome`中的 Mozilla 应用程序包可以为其他已存在的程序包贡献内容。

自底而上设计最常见的例子是经典浏览器（Classic Browser），它在`chrome`中包含一个名为`installed`的包（`comm.jar`）。许多程序员都了解这个包。当他们开发浏览器插件时，他们会包含覆盖层，自底而上的系统会将这些覆盖层与经典浏览器窗口合并。这些覆盖层包含在该窗口中显著显示的 GUI 元素。这些插件将作为熟悉界面的一部分暴露给用户。

一个简单的例子是 DOM 检查器（DOM Inspector）。它是 Mozilla 默认提供的，但在 Netscape 7 中没有。在 Netscape 7.0 中，Netscape 浏览器任何地方都没有 DOM 检查器菜单项。DOM 检查器可以稍后安装。安装后，“工具 | Web 开发”窗口上会出现一个菜单项。该菜单项是一个新覆盖层的内容，由 DOM 检查器提供。

并不是强制要求将覆盖层与经典的 Mozilla 应用程序套件集成。任何已知的 XUL 窗口都可以作为主文档并成为集成点。

对于自底而上的方法，处理 RDF 事实的方法如下。

#### 12.1.2.3 读取覆盖层数据库

覆盖层数据库是一组目录和 RDF 文件。数据库位于平台安装目录下的`chrome/overlayinfo`目录。该目录由其他文件生成，如果平台关闭，可能会被删除。Mozilla 每次启动时都会读取此数据库，如果不存在则重新创建它。

此生成的数据库是一个子目录集合。每个子目录都是一个以自底而上方式定义了覆盖层的`chrome`包名称。例如，`editor`是包含 Chrome 编辑器（Chrome Composer）的包名，因此`overlayinfo/editor`目录包含了该工具指定的所有覆盖层。此信息不包括任何自顶而下的覆盖层。

每个`overlayinfo`包内部都有一个`content`子目录，其中有一个`overlays.rdf`文件。该文件等同于单个包的`make(1)`Makefile。它作用类似于针对该包的一组`<?xul-overlay?>`处理指令。它是关于每个具有自底而上覆盖层的`chrome`URL 的事实集。

![](img/319913ee3703286e2c03d285fbfc49c7_444_0.png)

例如，`overlayinfo/editor/content/overlays.rdf`文件可能包含列表 12.6 所示的事实集。

**列表 12.6** Mozilla 编辑器的 RDF 覆盖层事实。

```xml
<xml version="1.0"?>
<RDF xmlns="http://www.w3.org/1999/02-rdf-syntax-ns#">
  <Seq about="chrome:///editor/content/editor.xml">
    <li chrome://messenger/content/mailEditorOverlay.xml</li>
    <li chrome://cascades/content/cascadesOverlay.xml</li>
  </Seq>
</RDF>
```

在许多情况下，此文件中引用的主文档本身也是一个覆盖层，它以自顶而下的方式包含在真正的主文档中。有一种分组技术设计用于排除用于覆盖层内容的中间层，这些 id 会合并到一个专门为该目的构建的中间覆盖层中。该中间层就是有时在`overlays.rdf`中指定的。整个中间覆盖层可以使用单个 id 包含在主 XML 中。当合并时，它会带入所有其他覆盖层。

独立于覆盖层数据库但仍位于`chrome`中的是`chrome/chrome.rdf`文件。该文件由`chrome`注册表维护，注册表负责覆盖层系统。它可以包含几个特定的覆盖层配置事实。三个特定的覆盖层谓词是：

```
hasStylesheets
disabled
hasOverlays
```

`hasOverlays`表示该包存在覆盖层 XUL 和 CSS 文件。`disabled`表示此包不应接受来自包之外的覆盖层。换句话说，无法从另一个包将覆盖层导入该包的任何文档中。

使用这些谓词时，主语必须是包名称 URI（如`urn:mozilla:package:editor`），对象字面量为`"true"`。这些属性中没有`"false"`的子集。要使它们变为 false，必须完全移除匹配的事实。示例事实是：

```
urn:mozilla:package:editor,hasOverlays,"true" ->
```

因此，`chrome.rdf`文件中的典型行可能如下：

```xml

<Description about="urn:mozilla:package:editor" hasOverlays="true"/>

```

#### 12.1.2.4 更改覆盖层数据库

Mozilla 的覆盖层数据库旨在支持自动检测新的覆盖层。它与第 17 章“部署”中 de XPIInstall 安装系统密切配合。尽管如此，手动使用它也非常容易。

对 XPIInstall 的展望显示了如下：

- 应用程序包在安装时会在`installed-chrome.txt`文件中添加行。
- 当 Mozilla 在处理包后必须重启时，它会读取`installed-chrome.txt`。
- 如果主文档没有覆盖层，它将创建一个新的。
- 如果主文档已经有了覆盖层，它将新的覆盖层合并到现有的覆盖层中。

### 12.1 覆盖层复用

这个系统的美之处在于它可以被重复使用。一个覆盖层可以包含多个文档片段，每个片段都标记有一个`id`。这些片段被插入到主文档中不同的位置，即匹配的`id`所在之处。因此，覆盖层系统比 C/C++ 的`#include`或 Perl 的`use`强大得多。后者只在单点插入内容（代码）。

这里是列表 12.7，一个包含两个目标`id`的主文档。列表 12.8 和 12.9 显示了利用这些位置的两个覆盖层。省略了样式表，原因如下：

```xml

Listing 12.7 包含两个覆盖层的主文档。

<?xml version="1.0"?>

<xul-overlay href="part1.xul?>

<xul-overlay href="part2.xul?>

<window xmlns="http://www.mozilla.org/keymaster/gatekeeper/there.is.only">

  <vbox id="osite1">

    <description>Main Box A</description>

  </vbox>

  <vbox id="osite2">

    <description>Main Box B</description>

  </vbox>

</window>

```

主文档有两个框，每个框包含一个单一标签。

```
Listing 12.8 包含包含片段的第一个覆盖层。
```

```xml
<?xml version="1.0"?>
<overlay xmlns="http://www.mozilla.org/keymaster/gatekeeper/there.is.only">
  <vbox id="osite1">
    <description>Box C</description>
  </vbox>
  <vbox id="osite2">
    <description>Box D</description>
  </vbox>
</overlay>
```
