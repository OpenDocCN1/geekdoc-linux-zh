
如果你需要优雅地重启 IIS，此脚本可能会非常有用。

# Web 应用黑客攻击防御

## 调整 UrlScan 优先级

最后，当 UrlScan 过滤器加载后，如有需要你需要调整优先级。返回 IISAdmin 工具中的 ISAPI 过滤器（图 D-8 所示的场景）。如果 UrlScan 不在列表顶端，且优先级没有设置为“高”（High），你应该考虑一下。UrlScan 将在请求传递给任何其他 DLL 之前拦截所有传入的请求。使用屏幕左侧的箭头按钮调整 UrlScan 的优先级，直到它看起来像图 D-9 一样。

取决于你在 Web 服务器上运行了哪些产品，在某些情况下 UrlScan 不应该被首选加载。关于这一点，我们所知道的唯一例外是发生在你使用 FrontPage 服务器扩展（FPSE）。在这种情况下，你可能需要将 UrlScan 过滤器移动到 FPSE ISAPI 过滤器 (`fpsexed.dll`) 之下，并将其优先级更改为“低”（Low）。

![](img/2c61c2d28445b774d9266972920f432d_390_0.png)

图 D-9. 成功加载的 UrlScan ISAPI 过滤器

> 注意：UrlScan 优先级也可以通过 `UrlScan.ini` 中的 `AllowLateScanning` 设置来设定。

## 移除 UrlScan

如果你需要禁用或移除 UrlScan，你有几种选择。如果在安装 UrlScan 后，你的应用程序开始丢弃某些客户端请求，你可以将 UrlScan 设置为“仅日志”模式，该模式允许所有请求，但会记录任何通常会被拒绝的请求。这对于排故障很有帮助。要将 UrlScan 设置为仅日志模式，在 `UrlScan.ini` 的 `RejectResponseUrl` 行中添加值 `/*`（斜杠-波浪线-星号），使其如下：

```
RejectResponseUrl=*
```
