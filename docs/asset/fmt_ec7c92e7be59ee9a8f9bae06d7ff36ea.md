
具有此接口的对象接受 DOM 树或子树作为参数：三个 XSLT 标签之一是处理指令的集合；另一个是待转换的内容。返回一个包含输出的第三棵树或子树。XSLT 参数也可以作为参数提供。该系统无法原地工作——如果需要，必须将结果附加到现有的 DOM 层结构中。

## 16.5 平台配置

某些脚本任务负责插入、管理和更新 Mozilla 平台本身的状态。为了做到，必须通过 XPCOM 接口暴露平台的内部特性。本主题涵盖了缓存、文件系统目录、偏好、安全和用户配置。

### 16.5.1 缓存控制

Mozilla 浏览器旨在对所有操作保持透明，但必要时也可以与其交互。缓存对于平台执行的所有 URL 请求都起着作用，除非它被显式调用或关闭。可以通过此 XPCOM 对对缓存进行低级访问：

```
@mozilla.org/network/cache-service;1 nsICachesService
```

基于此构建的对象还需要访问由 `nsICache` 接口提供的常量。这些接口出奇地复杂，因为缓存支持带有“单写-多加载”模式的并发访问请求。这意味着对缓存的低级访问可能会成为资源竞争的源头。最好避开细节，让高层服务使用传输层并管理交互。该接口的唯一用途是 `evictEntries()` 方法，可用于清空缓存。

缓存的一个非常简单的用法是预取（Prefetching）。预取将 http: URL 从其原始位置引入缓存，但并不一定会显示它。预取仅对非 HTTP GET 请求的 http: URL 起效（请求不能包含 `?param=` 部分）。预取通过这对 XPCOM 对象完成：

```
@mozilla.org/prefetch-service;nsIPrefetchService
```

类似的，`nsIRequest` 接口也提供了更精细的控制，它是通道和传输层的基础。`loadFlags` 属性可以基于 URI 使用，控制获取的 URI 与缓存之间的交互。

### 16.5.2 文件系统目录

`nsIFileDirectory` 接口提供了一种导航文件系统的方法。它允许你创建、删除和列出文件及目录。目录结构组织为树的形式，每个节点都是文件或目录。树的根节点是根目录。

## 16.5 Platform配置

如果平台正在显示 Web 页面，且该页面包含插件或 Java applet，则会添加第三个提供者，但仅在该页面存在时有效。该提供者与插件管理器关联。它向目录添加了特定特定的别名。这些别名的处理方式与其他别名（稍后将描述）不同，但如果存在匹配别名的文件，仍然会返回。

目录实现中有一个相当困惑的地方：实现目录服务的对象也实现了一个提供者。该提供者由 XPCOM 对指定：

```
@mozilla.org/file/directory_service;nsIDirectoryServiceProvider
```

此提供者是上述三个提供者之外的。它从未（很少）注册到任何目录服务中。相反，它可以直接创建。它不像其他提供者那样被隐藏。最后一个提供者为 XPCOM 系统添加了符合平台核心的别名。这些别名用于平台所需的底层文件和文件夹，并包含了许多特定操作系统的位置。

可以通过列表 16.8 所示的方法获取最后一个提供者。

```
Listing 16.8 使用别名从提供者检索文件系统资源。

var Cc = Components.classes;

var Ci = Components.interfaces;

var prov = Cc("mozilla.org/file/directory_service;1");

prov = prov.GetService(Ci.nsIDirectoryServiceProvider);

var result = {}; // 一个空对象

var file = prov.getFile("alias", result);

if (file == null) alert("No such location");

alert(result.value);
```
