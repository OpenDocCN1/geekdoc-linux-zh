
```actionscript
private function callGoogleLanguageTranslator():void {
    var lang1 = 'en';
    var lang2 = languageArray[language.selectedIndex];
    var service:HTTPService = new HTTPService();
    service.url = 'http://ajax.googleapis.com/ajax/services/language/translate';
    service.request.v = '1.0';
    service.request.q = textToTranslate.text;
    service.request.langpair = lang1 + '|' + lang2;

    service.addEventListener(ResultEvent.RESULT, onResultFunction);
    service.addEventListener(FaultEvent.FAULT, onFaultFunction);
    service.send();
}
```

### 代码清单 7.25 - 发起 `HTTPService` 调用的函数

- **5.** 响应格式是 API 返回的 JSON 编码结果。为了支持 JSON，您必须将 Flex corelib swc 文件添加到项目中。可以从 Adobe 网站下载该 corelib 文件，并将其作为库文件添加到项目的 Flex 构建路径中，如下所示

![](img/c4119654311ebf24679359ca105ee6_176_0.png)

- **6.** 可以在 http 服务调用的 `ResultEvent` 处理程序中处理响应，如 **代码清单 7.26** 所示

```actionscript
private function onResultFunction(event:ResultEvent) {
    try {
        var rawData:String = String(event.result);
        var jsonObject = JSON.decode(rawData);
        json.responseData.translatedText;
    } catch (ignored:Error) {
        Alert.show("Error during JSON decoding");
    }
}
```

### 代码清单 7.26 – `ResultEvent` 函数

- **7.** 您还可以为 http 服务请求过程中可能发生的 Fault Event 提供处理程序。我们留给读者自行编写这部分代码。

- **8.** 是时候运行应用程序并查看如何将单词翻译为您选择的语言了。*图 7.22* 展示了运行应用程序后的输出。

![](img/c4119654311ebf24679359ca105ee6_177_0.png)

**图 7.22 – 语言翻译桌面应用程序**

- **9.** 您可以创建这个酷小部件的可分发包，并将其分享给您的朋友，他们可以将其安装在自己的桌面上。

### 7.7 摘要

在本章中，您学习了无论使用什么协议，与远程服务器进行通信是多么简单。

首先，您了解到如果远程服务器使用 SOAP 进行通信，则可以使用 Web 服务与之通信。如果使用的协议是 HTTP，则可以使用 `HttpService`。要访问位于服务器上的远程对象，可以使用 `RemoteObject` 配合 AMF 协议绕过任何网关。

然后您了解到，从服务器获得的响应可以不顾及类型而得到处理，因为 Flex 为我们提供了多种手段来处理它们（对象或 XML）。

最后，本章讨论了如何与 DB2 等数据库进行交互，并提供了一个详细的示例。

从这里开始，您将使用所学的概念来构建带有图表和数据网格的实时仪表板。

### 7.8 复习题

- 1. `HttpService` 和 `Dataservice` 之间的区别是什么？

- 2. 什么时候使用 `RemoteObject` 服务？

- 3. Adobe LifeCycle 数据服务的其他替代方案是什么？

#### 4. 使用 E4X 的优势是什么？

#### 5. `HttpService` 如何知道返回结果的数据格式？

#### 6. 通过 `HttpService` MXML 标签发送请求的默认方法是什么？

- A. GET

- B. POST

- C. PUT

- D. HEAD

- E. 以上都不是

#### 7. 你在 MXML 文档中有以下 http 服务标签。

`<mx:HTTPService id="myHS" url="data/fruits.xml" useProxy="false"/>`

以下选项中，你会选择哪一个来在代码的其他位置发起远程数据调用？

- A. `myHS.getData()`

- B. `myHS.getRemote()`

- C. `myHS.send()`

- D. `myHS.sendAndReceive()`

- E. 以上都不是

#### 8. 你已在应用程序中实现了 `<mx:WebService>` 标签。以下哪个 MXML 标签可以插入到 Web 服务标签内部，以便调用远程服务器的多个方法并相应地分离结果？

- A. `<mx:method>`

- B. `<mx:operation>`

- C. `<mx:RemoteObject>`

- D. `<mx:request>`

- E. 以上都不是

#### 9. 可以在 `WebService` 上指定的不同 `resultFormat` 包括

- A. object

- B. xml

- C. e4x

- D. 以上所有

- E. 以上都不是

#### 10. 对于以下哪种远程服务，你可以在组件本身上指定 result 和 fault 事件处理程序？

- A. `HttpService`

- B. `WebService`

- C. `RemoteObject`

- D. 以上所有

- E. 以上都不是

![](img/c4119654311ebf24679359ca130a5ee6_180_0.png)

### 第 8 章 - 数据可视化

在本章中，你将学习如何使用 Flex 3 SDK 创建美观且实用的图表。尽管图表制作通常被视为高级主题，但本章将向你介绍这一功能，以展示其强大功能和潜力。

在本章中，你将了解以下内容：

- Flex 3 中的不同图表

- 创建流行的 Flex 图表

- 图表样式

> 注意：
>
> 图表功能是用户购买 **Flex Builder Professional** 时获得的关键功能之一 - 它不是免费 Flex SDK 或 Flex Builder Standard 的一部分。

#### 8.1 Flex 图表：概览

图表是一种展示变化项之间关系的图形。常见的图表使用条形、折线或圆的部分来显示数据。

在 Flex IDE 中，你可以转到主菜单并选择 Window -> Show View -> components -> Charts。点击 + 号展开并查看 Flex 中可用的图表。这在下面的图 8.1 中有所说明。每个图表选项旁边的小图标让你可以快速了解要创建的图表类型。

![](img/c4119654311ebf24679359ca130a5ee6_181_0.png)

**图 8.1 – Flex 3 SDK 组件窗口中的图表选项**

#### 8.2 Flex 3 中的不同图表

本节描述了你可以在 Flex 中使用的不同类型的图表及其用法：

##### 8.2.1 面积图 [`AreaChart`]

- 面积图将系列显示为由线连接的一组点。使用它来：

    - 显示随时间（或其他维度）变化的信息

    - 确定一组数据如何累加成整体（累计总和）

    - 理解整体中每个元素所占的比例。

##### 8.2.2 条形图 [`BarChart`]

条形图将系列显示为水平条形组。普通条形图与柱状图密切相关，柱状图将系列显示为垂直条形组；还与范围条形图相关，范围条形图将系列显示为具有不同起点和终点的水平条形组。使用它来：

- 呈现随时间或在不同条件下（例如，国家、测试条件）的观察值

- 提供区间缩放（例如，时间）。

##### 8.2.3 气泡图 [`BubbleChart`]

在气泡图中，值由气泡在垂直和水平轴上的位置以及气泡的大小表示。可以通过在图表中使用不同颜色的气泡来引入额外的类别。

##### 8.2.4 蜡烛图 [`CandlestickChart`]

蜡烛图是一种主要用于描述股票随时间价格变动的条形图样式。它是折线图和条形图的结合，其中每个条代表给定时间间隔内的价格波动范围。它最常用于股票和货币价格形态的技术分析。

##### 8.2.5 柱状图 [`ColumnChart`]
