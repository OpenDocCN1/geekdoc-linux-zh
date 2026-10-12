
`mime1` 和 `mime2` 是 MIME 类型。这些组件支持 `nsISStreamConverter` 接口。如果一个对象读取给定的输入流并

## 表 16.6 Mozilla 支持的流转换

| 原始 MIME 类型 | 转换后的 MIME 类型 |
|---|---|
| application/http-index-format | text/html |
| application/mac-binhex40 | */* |
| application/x-unknown-type-type | */* |
| compress | uncompressed content |
| deflate | uncompressed content |
| gzip | uncompressed content |
| message/rfc822 | application/vnd.mozilla.xul-xml |
| message/rfc822 | */* |
| message/rfc822 | text/html |
| multipart/byteranges | */* |
| multipart/mixed | */* |
| text/ftp-dir | application/http-index-format |
| text/gopher-dir | application/http-index-format |
| text/plain | text/html |
| x-compress | uncompressed content |
| x-gzip | uncompressed content |

转换其内容。它提供了一个新的输入流，可以从该流读取转换后的内容。表 16.6 列出了平台提供的转换。此类转换器也可以用纯 JavaScript 实现 `ns2Streamconverter` 的 XPIDL 描述解释了如何使用两个 `nsEventListener` 对象而不是整个流来完成转换。这种方法允许转换器作用于任何流，而不仅仅是输入流。

## 16.3.3 传输 (Transports)

传输层 XPCOM 对象负责将内容从 Mozilla 平台内部传输到外部，反之亦然。因此，传输器不仅仅是流，流受限于平台和本地磁盘。流通常以同步和异步方式直接从给定的源提供数据，而传输器可以从任何地方以异步和同步的方式提供数据。传输器还可以在用户请求之间处理并缓冲数据。

目前当前可用的传输层如图 16.7 所示。

## 表 16.7 支持的 XPCOM 传输层

| 实现 | 接口 (Interface) |
| :--- | :--- |
| `@mozilla.org/network/stream-transport-service;1` | `nsStreamTransportService` |
| `@mozilla.org/network/socket-transport-service;1` | `nsSocketTransportService` |
| `@mozilla.org/network/storage-transport:1` | `nsITTransport` |
| `@mozilla.org/mlextras/soap-transport:1?protocol=http` | `nsISOAPTransport` |
| `@mozilla.org/mlextras/soap-transport:1?protocol=https` | `nsISOAPTransport` |

表 16.7 中的五个传输器负责：所有流（包括本地文件）；域套接字；浏览器缓存；用于 SOAP 请求的 HTTP 传输绑定；以及用于 SOAP 请求的安全（基于 SSL）HTTP 传输绑定。

`stream-transport-service` 的实现相当新（自 1.3 版本开始），并取代了已不可用的 `file-transport-service`。请注意，某些代码示例可能在使用该旧对象。

## 16.3 通道 (Channels)

通道是一种获取 URL 内容的只读机制。虽然通道可以与文件对象配合，但对于通道来说，使用 URL 更为自然。通道负责 Mozilla 在检索文档时执行的大部分特定内容的工作。只读规则的唯一例外是上传通道，它用于提交表单、上传文件和发布 Web 页面。

在通常编程情况下，通道是独立处理的。与 `nsFile` 对象和流一样，通常是系统创建一个通道，而不是由你自己创建一个。就像文件和流是紧密关联的对象对一样，URL 和通道也是如此。这种类比并不完美。虽然流可以直接被创建，但通道很少被直接创建，因为通道大多位于协议之后。第二个区别是，通道是一个增强的请求（一个 `nsRequest` 对象），反过来又是一个增强的 URL。因此，通道及其 URL 并不是严格分离的。

通道的 XPCOM 对使用：
`@mozilla.org/network/io-service;1` `nsIIOService`

此组件通过 `getServer()` 提供 `nsIIOService` 接口。作为传输器，此接口实际上是 URL 方案（schemes）的名称。记住，URL 方案取完全引用的 URL 中第一个冒号之前的字符。该组件获取方案名称并返回软件对象。`nsIIOService` 接口是检索 URL 内容的基础起点。

`nsIOService` 接口可以使用 `nsIURI` 对象或 `nsIURL` 接口创建新的 URI。这些对象描述给定的 URL，就像 `nsFile` 对象描述文件一样。这些接口还暴露了协议处理器为给定的方案或 URL 实现的方法。每个协议处理器支持一种类型的通道；有些支持更多。在从用户输入或纯 JavaScript 字符串构建出任何 URL 对象后，可以使用它来查找该 URL 的协议处理器，并从该处理器处构建出有用的通道。
完成所有这些操作的快捷方法是调用 `newChannelFromURI()`。

当通道被启用时，它可以产生一个流对象并启动所需的进程。流对象被用于处理检索到的内容。`nsIOService` 接口有许多便利方法，因此可以完全忽略协议处理器。

通道会代表 URL 请求者执行大量处理——定位并检索资源；执行内容转换；以及记录 MIME 类型和其他配置详细信息。表 16.8 列出了平台提供的通道。

## 表 16.8 支持的 XPCOM 通道

| 通道接口 (Channel interface) | URL 方案及实现 |
|---|---|
| `nsIChannel` | 以下所有条目 |
| `nsICachingChannel` | http: |
| `nsIDChannel` | data: |
| `nsEncodedChannel` | http: |
| `nsFileChannel` | file: |
| `nsIFTPChannel` | ftp: |
| `nsHTTPChannel` | http: |
| `nsIMapChannel` | imap: |
| `nsInputStreamChannel` | `@mozilla.org/network/input-stream-service;1` |
| `nsIJarChannel` | jar: |
| `nsMultiPartChannel` | internal use |
| `nsResumableChannel` | ftp. (不支持) |
| `nsUploadChannel` | file. |
| `nsIViewSourceChannel` | view-source: |
| `nsIWiwygChannel` | wysiwyg: (不支持) |

从表 16.8 可以看出，大多数通道与 URL 方案相关。所有通道都支持 `nsIChannel` 核心功能，主要包括

## 16.3 数据传输 (Data Transfer)

转换其内容。所有通道支持 `nsIChannel` 核心功能，主要包括

`open()` 和 `asyncOpen()` 方法。这些方法产生流对象。其他通道接口为通道对象增强了额外信息。它们并不代表本质上不同的通道。

`nsUploadChannel` 面向桌面而非桌面。它消耗一个输入流，而不是提供流，以便向服务器提供内容。`nsResumableChannel` 用于被中断的 FTP 下载。经典浏览器的下载管理器并不使用此功能。

第二个异常情况是协议。通道无法与复杂的协议（如 HTTP 或 FTP）关联。它可以关联任何简单的传输任务。现有通道支持简单的内存到磁盘传输（文件访问）以及更简单的内存到内存传输（使用流对象）。这两种协议都不需要与 URL 交互，因此它们的通道可以手动管理。这就是表 16.8 中 InputStreamchannel 的来源。

列表 16.6 有内存到磁盘传输的示例

## 16.3.5 数据源 (Data Sources)

数据源为 XUL 模板和 RDF 存储的操作提供了面向事实的支持。Mozilla 平台包含大量将数据源对象连接到此类 URL 代码。对于事实存储的操作，直接通过 XPCOM 接口访问，且平台已经有了执行此操作的代码。最明显的例子是用于激活模板的默认构建器内容视图。应用程序程序员可以使用这些数据源构建等或不同的支持。

单个事实可以基于 `nsRDFSource` 和 `nsRDFLiteral` 对象的简单 XPCOM 对象检索。通常，数据源是易读易写的，提供简单的查询-插入-更新-删除功能，有时称为获取和设置。

数据源的概念由 `nsRDFDataSource` 接口表达。该接口提供了处理 RDF 事实的所有语义。约 20 个 XPCOM 对象实现了此接口。本章的“动手操作”部分尝试分类和识别这些接口。

数据源接口分为三类：

辅助工具和实用程序。这些是为了实现某些功能而需要的。

创建性扩展。某些接口以新颖的方式扩展了 `nsIRDFDataSource` 接口提供的功能。

内容源。数据源的某些方面决定了内容——即可以访问的事实类型和数量。最后一类分为普通数据源和内部数据源。普通数据源从 RDF 文件提取事实。内部数据源从 Mozilla 平台提取事实。

如果选择了此组错误的数据源，可能会花费小时、几天甚至几周的时间来思考为什么不起作用。因此，对每种内容支持都有良好的了解是非常重要的。

`nsIRDFDataSource` 对“source”（源）一词的使用并不恰当。在该接口中，source 和 target 分别用于生成平均事实和事实对象——用于 `get()`。Source 在 Mozilla 的其他地方也指代源代码。不要自动假设 source 指的是数据源。

## 16.3.5 工厂对象和辅助对象

如果涉及 XUL 模板，那么模板的 DOM 对象将提供对 `nsIRDFDataSource` 对象的访问。如果不存在模板，则数据源的脚本化使用从一开始就需要工厂对象。表 16.9 列出了用于纯 RDF 操作的组件。

在 16.9 中，符号 `(arg)` 表示可能有多种可选方案。查看所有方案的最简单方法是列出 `window.Components.classes` 数组的内容。表 16.9 分为四个部分。

第一部分是应用程序使用 RDF 的起点。`nsRDFService` 接口用于从 URI 创建 `nsIRDFDataSource` 对象，包括基于 `rdf:` 方案的 URL。此类 URL 列在表 16.11 中。如果需要一个事实的主体（subject）、谓语（predicate）或对象（object）的对象，也可以此接口从 JavaScript 字符串创建。`nsRDFService` 接口可以通过 `getService()` 访问，而不是通过 `create()`。

表 16.9 的第二部分提供了创建和操作 RDF 容器的接口。提供的两个接口提供了使用 RDF 资源对象创建数据结构的简单方法。该部分还包括资源工厂（resource-factory）组件。使用资源工厂组件时创建的事实项具有额外的功能。取决于所选的名称——例如，创建的对象可能包含基础的主体、谓语或对象资源外，还包含地址、电子邮件、新闻或文件信息。这些信息及其相关方法会在资源在事实中操作时随之移动。

## 16.3 数据传输

表 16.9 针对 RDF 的 XPCOM 组件

| 组件名称 | 接口 | 目的 |
| :--- | :--- | :--- |
| `@mozilla.org/rdf/rdf-service:1` | `nsRDFService` | 起点；创建 `nsIRDFDataSource` 源以及 `nsRDFNode` 对象、谓语和对象 |
| `@mozilla.org/rdf/container:1` | `nsRDFContainer` | 创建标签；`<Seq>` 或其他标记对象 |
| `@mozilla.org/rdf/container-utils:1` | `nsRDFContainerUtils` | 操作 RDF 容器对象 |
| `@mozilla.org/rdf/resource-factory:1?name=[arg]` | various | 创建表示事实部分的对象 |
| `@mozilla.org/rdf/content-sink:1` | `nsExpatSink` | 将基于 RDF 的 XML 对象转换为事实存储 |
| `@mozilla.org/rdf/xml-parser:1` | `nsRDFXMLParser` | 将 RDF 文档转换为基于 RDF 的 XML 对象 |
| `@mozilla.org/rdf/xml-serializer:1` | `nsRDFXMLSerializer` `nsRDFXMLSource` | 将事实存储转换为 RDF 文档 |
| `@mozilla.org/rdf/delegate-factory:1?key=[arg]&scheme=[arg]` | `nsRDFDelegateFactory` | 将资源（一个事实）绑定到自定义对象，该对象根据该资源同步其他内容 |

只有与电子邮件相关的组件才被 XPCOM 完全公开；其他组件对脚本来说是完全不可用的。已公开的组件 `name=` 设置为以下值：
imap mailbox moz-adirectory moz-ablddirectory moz-almbddirectory moz-aboutlookupdirectory

表 16.9 的第三部分仅用于直接解析 RDF 文档。这是 Mozilla 的深度定制，对于普通操作并非特别需要。反向操作（即从事实存储器生成 RDF 文档）适用于任何意图持久化其操作数据的应用程序。这些接口中没有一个是用于操作事实。

最后，表 16.9 中的 `nsRDFDelegateFactory` 项需要对平台架构有深入理解。它提供了一种在事实使用的资源被创建或销毁时挂载副作用（side effect）的方法。使用这种代理（delegate）可以将事实与为之设计的任何系统绑定。

这类似于 Perl 中的函数。对于单个资源对象，一个代理就足够。接口的使用超出了本书的范围。

### 16.3.5.2 结构选项

Mozilla 提供了扩展数据源功能的选项。这些选项使得数据源比仅提供内容访问更加灵活。这些选项以 XPCOM 接口的形式存在，为存储数据源中数据的因素存储添加额外功能。16.10 描述了这些接口。

XUL 系统不仅使用复合数据源，还提供了一系列提供给 XUL 数据源的属性列表。复合数据源本质上是一个包含其他数据源的容器。相应，它实现了 `nsIRDFDataSource` 接口。该接口的每个方法都会使用包含的数据，并在需要时对其中调用相同的方法。

内存数据源是几个较复杂数据源的核心。事实存储的内容需要手动构建，而不是从某个处构建，内存数据源是起点。清理数据源（purging）是将其置为空的方法。

`nsIRDFDataSource` 接口提供了从位置保存和加载事实存储。本地或远程，但在两种情况下支持都有限。`Flush()` 仅支持文件；`Refresh()` 仅支持文件。

## 16.3.5.3 内容选项

数据源并不相同。它们在内容以及访问内容方面存在差异。这些差异是数据源难以使用的主要原因。从应用程序程序员的角度来看，并不清楚哪些数据源产生事实或如何检索这些事实。所有基于 XPCOM 的数据源遵循此模式：

`@mozilla.org/rdf/datasource?name=(arg)`

`(arg)` 的合法值列在表 16.12 左侧列。数据源为应用程序提供对于普通 RDF 文件是显而易见的。然而，可以直接查看的内部数据源，除了通过 (a) 使用数据源、(b) 研究平台源或 (c) 在用户配置文件查找示例外，无法查看。书签、历史、搜索和本地存储内部数据源都会在用户配置文件产生示例文件；其他则不会。即使有示例文件，这些文件通常也不是 RDF 文档。

表 16.10 扩展 `nsIRDFDataSource` 功能的接口

| 接口名称 | 实现类 | 目的 |
| :--- | :--- | :--- |
| `nsIRDFDataSource` | 所有数据源，但局限性见表 16.12 | 对数据源的基本数据操作 |
| `nsIRDFCompositeDataSource` | `@mozilla.org/rdf/datasource;name=composite-datasource` | 提供一个作为其他数据源并集的数据源；其他者的交集 |
| `nsIRDFInMemoryDataSource` | `@mozilla.org/rdf/datasource;name=in-memory-datasource` | 提供一个独立于其他事实的内存数据源 |
| `nsIRDFDPurgeableDataSource` | `@mozilla.org/rdf/datasource;name=in-purgeable-datasource` | 允许清理数据源事实 |
| `nsIRDFPPropagatableDataSource` | `@mozilla.org/rdf/datasource;name=in-propagatable-datasource` | 开启向任何观察者广播事实更改 |
| `nsIRDFRemoteDataSource` | `@mozilla.org/rdf/datasource;name=remote-datasource` | 提供协调原始事实数据源的方法。XML 数据源约定是本地或纯 RDF 文件 |

这种内容的匿名性对于尝试导航内部数据源的 XML 模板和脚本来说是一个大问题。在这两种情况下，都需要预先知道数据源的结构。幸运的是，这种内部数据源仅用于一小少数用例。

“调试角层（Debug Corner）”包含一些可以显示数据源的代码。表 16.1 列出了大多数内部数据源最核心且最常见的属性。特殊值 `rdf:null` 表示完全没有数据源。它并不代表空数据源。

除了内容之外，Mozilla 的许多数据源具有有限或受限的功能。这意味着，即使你知道数据源的内容，该数据对象可能也没有足够的实现来实现访问该内容。这意味着，即使一个 XPCOM 组件可能声称它使用 `RDFData` 作为源接口，但实际上，它的许多方法可能简单地返回错误或异常，而不执行任何操作。此类数据源对象尚未完成。

表 16.12 标识了每个已实现数据源的可用支持水平。表 16.12 基于 Mozilla 1.4，应仅作为可用性的索引使用。不为人知的数据源在使用之前需要晦涩的准备步骤。本文未涵盖这些步骤。

没有 URI 的数据源不能在使用 XML 属性的 XML 模板中使用。它们仍然可以通过脚本附加到模板上。在平台默认构建中未向 XPCOM 注册的数据源完全无法从 XUL 或 JavaScript 使用。`composite-data-source` 只有在其收集的数据源之一可以直接通过单个数据源插入，而不是直接通过复合数据源的接口工作时，才能被插入其中。

## 16.4 Web 脚本

浏览器执行的任务在一个与传统 3GL 程序不同的环境中运行。在 Web 世界中，不存在所谓的“文件”或“名称”。相反，存在 URL 和代表这些 XUL 资源的文档。通常，此类文档具有复杂的结构并且基于 XML。这种环境需要一种不同于“文件和文件夹”以及“流”章节下描述的脚本方法。

浏览器也是新兴的 Web 协议栈的参与者，这可以更准确地识别为 XML 协议栈。这套栈是一组标准，使用 HTTP 或另一种协议，是系列启用应用和特定应用程序协议集的第一步。XML 协议栈提供了一个面向数据的事务系统，而不是 Web 浏览所需的简单的文档请求和响应-带检索的系统。

### 表 16.11 内部数据源的起点

| rdf:URI | 顶层 URN / URI | 用于包含事实的谓词 |
| :--- | :--- | :--- |
| rdf/addressdirectory | moz-addressdirectory | http://home.netscape.com/NC-rdf#child 和 http://home.netscape.com/NC-rdf#CardChild |
| rdf/bookmarks | NC:BookmarksRoot | RDF 容器 |
| rdf/charset-name | NC:PersonalToolbarFolder | http://home.netscape.com/NC-rdf#child |
| rdf/files | 多（例如，NC:BrowserChartMenu） | RDF 容器 |
| rdf/history | NC:FilesRoot | http://home.netscape.com/NC-rdf#child |
| rdf/httpindex | NC:HistoryRoot | http://home.netscape.com/NC-rdf#child |
| rdf/internetsearch | NC:HistoryDate | http://home.netscape.com/NC-rdf#child |
| rdf/Searchengine | NC:SearchEngineRoot | 无容器；每个 URI 仅有一组属性 |
| rdf/SearchRoot | NC:SearchRoot | 无容器；每个 URI 仅有一组属性 |
| rdf/SearchURNRoot | NC:SearchURNRoot | http://home.netscape.com/NC-rdf#child |
| rdf/FilterSearchSitesRoot | NC:FilterSearchSitesRoot | http://home.netscape.com/NC-rdf#child |
| rdf/SearchCategoryRoot | NC:SearchCategoryRoot | RDF 容器 |
| rdf/SearchMode | NC:SearchMode | RDF 容器 |
| rdf/isdefaults | | 无使用任何 URI |
| rdf/localstore | | 每次：URI 是根 |
| rdf/localsearch | | 无根；使用服务器 URL |
| rdf/mailnewfolders | | msgacounts/ |
| rdf/msgaccountmanager | | 无根；使用服务器 URL |
| rdf/infilters | | NC-ntservers |
| rdf/sntp | | |
| rdf/window-mediator | NC:WindowMediatorRoot | |

### 表 16.12 nsIRDFDataSource 接口对每个数据源的支持

| 在 Contract ID 中使用的名称 | 是否有 refd: URI? | 在默认构建中已注册到 XPCOM？ | 内容特定：XPCOM 接口？ | 支持 assert()? | 支持 ArcLabelsOut()? | 支持 GetIResources()? | 支持命令？ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| addressdirectory | ✓ | | | | | | |
| bookmarks | ✓ | | | | | | |
| charset-menu | ✓ | | | | | | |
| files | ✓ | | | | | | |
| history | ✓ | | | | | | |
| httpindex | ✓ | | | ✓ | | ✓ | |
| internetsearch | ✓ | | | | | | |
| ispdefaults | ✓ | | | | | | |
| localstore | ✓ | | | | | | |
| localsearch | ✓ | | | | | | |
| mailnewsletter | ✓ | | | | | | |
| msgaccountmanager | ✓ | | | | | | |
| msgfilters | ✓ | | | | | | |
| smtp | ✓ | | | | | | |
| subscribe | ✓ | | | | | | |
| window-mediator | ✓ | | | | | | |
| chrome | ✓ | | | | | | |
| mailsounds | | | | | | | | |
| registry | | | | | | | | |
| relatedlinks | | | | | | | | |
| inmemory-datasource | | ✓ | | | ✓ | | |
| composite-datasource | | ✓ | | | ✓ | | |
| xml-datasource (RDF files) | ✓ | ✓ | 仅限 file: URLs | ✓ | ✓ | | |

从低到高的核心标准如下：

- XML 和 XML Schema。这些标准用于定义所有其他标准的语法。Mozilla 实现了 XML 并提供了一些实用程序。
- HTTP 可以充当传输层。Mozilla 实现了 HTTP。
- SOAP 提供了一种消息格式。Mozilla 实现了它。
- WSDL 是一种基于 SOAP 的功能。Mozilla 从 1.4 版本开始支持 WSDL。
- UDDI 是一种发现 Web 服务的机制。Mozilla 并没有实现 UDDI。
- ebXML（XML 业务模型）。由 OASIS 定义。Mozilla 并没有实现 ebXML。
- 业务流程建模。这些标准由工作管理委员会和应用小组开发。Mozilla 并没有实现这些标准。

#### 16.4.1 URL、URN 和 URN

URI，以及 URL 和 URN 的特殊子集在 IETF 的 RFC 2396 中有所描述。目标或至少希望 URI 是与媒体无关且高度移植的。它们没有文件和路径那样的移植性问题。相反，URI（尤其是 URN）还有另一个问题：它们经常被类型错误、别名或缩写。

在 Mozilla 中，URI 可以表示为纯 JavaScript 字符串而不丢失移植性。如果该字符串要可供 XPCOM 接口使用，则需要将其转换为对象。此解析器提供了最基础的对象：

`@mozilla.org/network/simple-uri:1` `nsIURI`

URI 是 URI 的特定形式，并有一个专门的对象，适用于常见的 URN 方案，如通过 http: 和 ftp:。此解析器提供了一个广泛使用的示例：

`@mozilla.org/network/standard-url:1` `nsURL`

此接口也支持 nsURI。事实上，大多数在 Contract ID 中包含 uri 或 urn 的 XPCOM 组件都支持一个或两者。如果用户输入了 URI，可能需要某些验证。有几种针对语法错误的防御措施。此解析器对修复用户输入的 URI 出了最大的尝试：

`@mozilla.org/docshell/urifexup:1` `nsURIPufix`

此接口拥有一个 `fixUPRI()` 方法，可以处理编码为 URI 的关键字以及以文本或而非 http://www.test.com 输入的文本。此类 docshell 组件在 Mozilla 浏览器窗口中暴露为 AOM 对象；其结构在第 10 章“窗口和窗格”的“iframe”中讨论。

解析字符串的第二种方案是依赖此 XPCOM 解析器：

`@mozilla.org/network/parser:7~auth=maybe` `nsIURIParser`

## 16.4 Web 脚本

最后，基础接口 `nsURI` 支持一个 `resolve()` 方法。该方法将提供的相对 URI 与对象的 URI 进行比较，并返回一个与所提供的相对 URI 等效的完全解析（未缩短）URI。

没有专门用于 URN 的 XPCOM 对象。
URL 正确性的终极测试（取决于你的选择）是获取它所定位的资源。

## 16.4.2 下载文件

要从远程位置下载文件或文档，您可以使用通道（channel）、URI 以及由此产生的流（stream）。这是“内容处理概念”中涵盖的直接方法。还有一种高级别的替代方案，即使用此 XPCOM 组合对：
