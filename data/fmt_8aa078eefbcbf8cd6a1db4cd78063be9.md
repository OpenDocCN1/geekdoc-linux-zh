
## 解码移动应用

你现在已经通过蓝牙日志完成了解码，能够发送命令来设置时间，但仍然存在一些问题。我将反编译 `Android Pro` 传感器并尝试使用以下方法解决这些问题：

你已经下载了该文件的 `apk`。如果你通过 `USB` 连接并启用了调试连接，你可以使用 `adb` 使用该包。首先列出所有可用包：

```
adb shell pm list -
```

然后在结果列表中搜索应用名称。遗憾的是，`Termo-Pro` 不在列表中。在 `Google Play` 商店中搜索并查看应用网页的 URL，它显示该包名为 `humuro`。

如果获取 `apk` 文件不起作用，你可以从第三方 `apk` 反编译器下载，例如 `apk`。

此 `APK` 文件包含正在执行的 `Dalvik` 代码，但你可以使用强大的 `jadx` 反编译器将其反编译为 `Java` 源码，该工具既有命令行版本，也有图形界面版本。你需要 `Java 8` 或更高版本来运行。

从 `GitHub` 下载 `jadx` 的最新发布版本并使用 `ZIP` 文件。然后启动图形界面。

在 `Navigation`（导航） | `Search`（搜索）菜单中，`jadx` 开始反编译应用。当你准备就绪时，在搜索字段中使用其中一个 `UUID`。你可能无法两个 `UUID` 都找到结果，但只需使用 `0001`，`UUID` 就会以字符串常量的形式定义。

在逆向工程 `BLE` 连接时，特征（`characteristics`）比服务（`services`）更有趣，因为特征是数据的实际容器。如果你理解了特征：

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_47_0.png)

| Handle | Protocol | Length | Data (offset to start) | Sent Write Command, Response, Handle: (Unknown) | Client Characteristic | Configuration |
|---|---|---|---|---|---|---|
| 01 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0001` (`Unknown`: `Unknown`) | | |
| 02 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0002` (`Unknown`: `Unknown`) | | |
| 03 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0003` (`Unknown`: `Unknown`) | | |
| 04 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0004` (`Unknown`: `Unknown`) | | |
| 05 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0005` (`Unknown`: `Unknown`) | | |
| 06 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0006` (`Unknown`: `Unknown`) | | |
| 07 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0007` (`Unknown`: `Unknown`) | | |
| 08 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0008` (`Unknown`: `Unknown`) | | |
| 09 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0009` (`Unknown`: `Unknown`) | | |
| 10 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0010` (`Unknown`: `Unknown`) | | |
| 11 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0011` (`Unknown`: `Unknown`) | | |
| 12 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0012` (`Unknown`: `Unknown`) | | |
| 13 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0013` (`Unknown`: `Unknown`) | | |
| 14 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0014` (`Unknown`: `Unknown`) | | |
| 15 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0015` (`Unknown`: `Unknown`) | | |
| 16 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0016` (`Unknown`: `Unknown`) | | |
| 17 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0017` (`Unknown`: `Unknown`) | | |
| 18 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0018` (`Unknown`: `Unknown`) | | |
| 19 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0019` (`Unknown`: `Unknown`) | | |
| 20 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0020` (`Unknown`: `Unknown`) | | |
| 21 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0021` (`Unknown`: `Unknown`) | | |
| 22 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0022` (`Unknown`: `Unknown`) | | |
| 23 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0023` (`Unknown`: `Unknown`) | | |
| 24 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0024` (`Unknown`: `Unknown`) | | |
| 25 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0025` (`Unknown`: `Unknown`) | | |
| 26 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0026` (`Unknown`: `Unknown`) | | |
| 27 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0027` (`Unknown`: `Unknown`) | | |
| 28 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0028` (`Unknown`: `Unknown`) | | |
| 29 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0029` (`Unknown`: `Unknown`) | | |
| 30 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0030` (`Unknown`: `Unknown`) | | |
| 31 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0031` (`Unknown`: `Unknown`) | | |
| 32 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0032` (`Unknown`: `Unknown`) | | |
| 33 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0033` (`Unknown`: `Unknown`) | | |
| 34 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0034` (`Unknown`: `Unknown`) | | |
| 35 | `ATT` | 02 | | Sent Write Command, Response, Handle: `0035` (`Unknown`: `Unknown`) | | |
