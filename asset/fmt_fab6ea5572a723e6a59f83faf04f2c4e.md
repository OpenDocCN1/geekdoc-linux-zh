
```javascript
var Includ = {
  QueryInterface : function(iid) {
    var ci = Components.interfaces;
    if (iid.equals(nsSupports) && iid.equals(mozIJScriptLoader))
      throw Components.NS_ERROR_NO_INTERFACE;
    return this;
  },

  // interface mozIJScriptLoader
  loadSubscript : function (url) {
    // 加载脚本
    return;
  }
};
```

该对象支持 `nsISupport` 和 `nsISScriptLoader`。

列表 5.8 使用 XPCOM 接口创建 JavaScript 对象。

```javascript
var final_obj = {
  QueryInterface : function(iid) {
    var ci = Components.interfaces;
    if (iid.equals(nsSupports) && iid.equals(mozIJScriptLoader))
      throw Components.NS_ERROR_NO_INTERFACE;
    return this;
  },

  // interface mozIJScriptLoader
  loadSubscript : function (url) {
    // 加载脚本
    return;
  }
};
```

该对象支持 `nsISupport` 和 `nsISScriptLoader`。

如果我们确定没有对 `QueryInterface()` 的调用，那么该对象的 `nsSupports` 接口就可以被使用。

### 5.5.4.4 插件与 DOM

- *- 插件从 3.0 版本起就可以编写脚本。那时，Netscape 增强了 1.1 版本的 NPAPI 插件使其可脚本化，并创建了许多插件与其工作。Mozilla 支持此，但...

- *- 对于插件存在系列可脚本 XIDPL 接口。使用这些接口可以直接从 JavaScript 驱动插件。处理插件最简单的方法是使用 HTML `<embed>`（已弃）或 `<object>`（推荐）标签以及 DOM 0 `plugins` 数组。

- *- 对于 DOM 标准也存在系列可脚本接口。可以通过 `Component` 对象检索 DOM。这并没有太大必要，因为接口自动在 `window` 对象上以及在由 `window` 对象获取的 DOM 对象上可用。

###### 5.5.4.5 Java

- Web 浏览器从 3.0 版本起就支持脚本 Java applet：Mozilla 也支持脚本化 Java。Mozilla 1.x 平台使用的架构与 Netscape Communicator 4,x 使用的不同，但对脚本编写者是向后兼容的。

## 5.5 Mozilla 的可脚本接口

在 Mozilla 中，这种 Java 依赖已经消失了。Netscape 管理自己的安全性。不再需要 Java，Java 也不再紧密集成到平台中。在原始意义上不再有 LiveConnect；只有 XPConnect。LiveConnect 提供的集成功能仍然存在，但它们隐藏在 XPCOM 后面的代码中。Mozilla 可视的 Java 支持现在由一组 XPCOM 接口组成。Mozilla 提供了两种适配 Java 的技术。第一个是 OJI（开放 Java 接口）：这是一个类似于 NXPAPI（插件）API 的接口，旨在与任何厂商的 Java 平台配合。XPCOM 提供了对 OJI 的访问。第二项技术是用于后兼容的 LiveConnect 仿真器。它也是一个 XPCOM 接口，定义在接口 `nsIJRLiveConnectPlugin` 中。以前请求发送到 Netscape 4.x 的 Java JVM。

至于插件，在 Mozilla 内部使用 Java 最简单的方法是在 HTML 文件中使用 `<applet>` 或 `<object>` 标签。同样，请参阅第 10 节“窗口与页面”中关于构建 HTML 和 XUL 的讨论。

一些从 Java 背景进入 Web 的程序员。如果你有一套复杂的 Java 环境并想将其与 Mozilla 集成，请谨慎行。一方面，JavaScript 和 Java 之间最简单直接的交互运行良好。另一方面，JavaScript、Java 和 Mozilla 都是复杂的系统，在每一点上实现完美交互是一个巨大的目标。复杂的交互仍然存在问题，鼓励你仔细研究 Mozilla Bugzilla 数据库中剩余的 Java 相关 Bug。

最好的方法是这样的：坚持使用 Sun Microsystems 的 Java 实现，并仅使用 1.4 或更高版本。建议使用较新版本的 Mozilla 以将突出的问题减少到最低。

除了第 10 节“窗口与页面”中的一些说明外，本书关于 Java 就没有其他内容了。

### 5.5.5 脚本库

Mozilla 依赖 XPCOM 系统从其他地方获取功能，但存在一些完全用 JavaScript 编写的小型库。这些库试图简化 XPCOM 系统的某些方面。

这些库中最用的是 JSLib 和 RDFLib。RDFLib 实际上只是 JSLib 的一个子集。JSLib 让处理文件和文件夹变得不那么痛苦。RDFLib 子部分让处理 RDF 数据变得不那么痛苦。该库创建 JavaScript 对象，用以简化它们所基于的 XPCOM 对象。

此库可以从 `http://jslib.mozdev.dev` 下载。该库中的文件以 ASCII 格式（UNIX 格式）编写。

注意，这些库仅偶尔更新。下载时请检查头文件以查看它们是否最近维护过。

要使用该库，请包含顶层的 `jslib.js` 文件，它提供了实用例程和常量。这些例程中最重要的是 `include()` 函数，它的作用类似于 Perl 的 `require`（或 c++ 的 `#include`）。然后根据需要包含其他 `jslib` 功能。该库包含近十个子库，但最重要的是 `io`（用于文件处理）和 `rdf`（用于 rdf 处理）。图 5.2 显示了这些库之间的依赖关系。

带有增长箭头的脚本是这些箭头的目标，将被首先加载。显示了没有依赖关系的文件。显然，该库被分为两个主要部分，我们称之为 RDFLib 和 JSLib。它们是 RDF 文件访问的不同实现：`rdf/rdfFile.js` 和 `io/RDF.js`。它们为几乎相同的任务提供了不同的接口；`rdfFile.js` 是最原生的接口也是最常用的子库。

该库使用 `window.constructor()` 方法为 XPCOM 组件创建对象构造函数（请参见包含“对象创建替代方案”的章节中的对象构造以获取如何操作的说明）。它还使用 JavaScript 原型系统实现了 JavaScript 构造函数。使用基于原型的构造函数来创建新的 JavaScript 对象。在构建过程中，使用 XPCOM 对象构造函数在新的 JavaScript 对象上设置属性。这些属性持有每一个

# jslib.js

![](img/319913ee3703286e2c03d285fbfc49c7_209_0.png)

图 5.2 JSLib 和 RDFlib 文件依赖关系。

XPCOM 对象。因此，最终的 JavaScript 对象包含（或）一个或多个 XPCOM 对象，并且这些 XPCOM 对象的封装或 Fac面。这是一种简单且广泛的技术。

新的此类 JavaScript 对象包含了错误检查、协调和翻译代码，使得 XPCOM 对象更容易使用。它们代表了 XPCOM 系统组件的简化或特殊视图，用于常用任务。表 5.5 显示了该库创建的对象。

在表 5.5 中，'data-source' 参数是一个 `iRDFDataSource` 对象，而不是引用 URL。JSLib 库包含其他几个有用对象，它们没有像表 5.5 中的对象那样详尽或完整。例如，定义在 `zip.js` 文件中的 `zipob` 仅执行解压压缩文件所需工作的一半。

JSLib 中的大部分文件都有以序言注释形式存在的详尽文档。这些序言注释显示了如何使用所请求的对象。

| 构造函数 | 源文件 | 使用的对象 | 目的 |
| :--- | :--- | :--- | :--- |
| `include()` 方法 | `jslib.js` | | 包含 .js 文件。 |
| `Dir(filePath)` | `io/dir` | `FileSystem()` | 管理本地磁盘上的文件夹。 |
| `DirUtils()` | `io/dirUtils` | | 查找目录。 |
| `File(filePath)` | `io/file` | `FileSystem()` | 管理本地磁盘上的文件。 |
| `FileSystem(filePath)` | `io/filesystem.js` | | 管理本地磁盘上的文件系统。 |
