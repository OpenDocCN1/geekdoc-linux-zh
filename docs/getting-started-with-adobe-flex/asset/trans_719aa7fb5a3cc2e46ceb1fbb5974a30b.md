

在上面的代码清单中，可以看到在一些数据网格列中，使用 **labelFunction** 代替了 **dataField**。labelFunction 为用户提供了一个函数，用于处理显示在特定列中的数据格式。

此外，为了以更易读的格式显示日期，使用了 **dateFormatter**。

- **3.** 在数据网格列中调用了 **displayLow()** 函数。它包含对 **row** 对象的引用，该对象包含当前行的数据。这使得用户能够在在对应列中显示信息之前执行格式化、命名空间和其他与 XML 相关的任务。**代码清单 7.20** 展示了该函数的代码。

```javascript
protected function displayLow(row:Object, column:DataGridColumn): String {
    return row.Temperatures.MorningLow;
}

protected function displayHigh(row:Object, column:DataGridColumn): String {
    return row.Temperatures.DaytimeHigh;
}

public function getURL(description:String): String {
    var url:String = "images/" + description + ".gif";
    return url;
}

protected function displayDate(row:Object, column:DataGridColumn): String {
    var dates:String = dateFormatter.format(row.Date);
    return dates;
}
```

**代码清单 7.20 – displayLow 函数**

- **4.** 为了调用 Web 服务，服务器必须在 **crossdomain.xml** 文件中有一个适当的条目，以允许调用 Web 服务。在此处，必须在运行时调用 Web 服务，因此使用 ActionScript 在运行时调用该 Web 服务。使用 **代码清单 7.21** 中所示的方法在运行时加载 WSDL。

```actionscript
private function invokeService():void {
    var loginWS:WebService = new WebService();
    loginWS.useProxy = false;
    loginWS.GetCityForecastByZIP.addEventListener("result", result);

    loginWS.LoginOperation.resultFormat = 'e4x';
    loginWS.addEventListener("fault", fault);
    loginWS.loadWSDL('http://ws.cdyne.com/WeatherWS/Weather.asmx?wsdl');
    loginWS.GetCityForecastByZIP(zipcode, text);
}
```

**代码清单 7.21 – invokeService 函数**

- **5.** 当 Web 服务调用完成时，Web 服务操作将分发结果事件或错误事件。

- **6.** 如果发生结果事件，则调用下方代码清单 7.22 中的 result 函数。

```actionscript
private function result(evt:ResultEvent):void {
    var myObj:Object = evt.result as Object;
    cityName.text = "City: " + evt.result.City;
    forecastGrid.dataProvider = evt.result.ForecastResult;
}
```

**代码清单 7.22 – result 函数**

- **7.** 如果发生错误事件，则调用下方代码清单 7.23 中的 fault 函数：

```actionscript
private function fault(evt:FaultEvent):void {
    Alert.show(evt.fault.message);
}
```

**代码清单 7.23 – fault 函数**

- **8.** 当用户输入邮政编码并点击获取天气预报按钮时，Web 服务将得到调用。该按钮定义如下：

```xml
<mx:Button label="Get Weather Forecast" id="getWeather" click="invokeService()"/>
```

- **9.** 现在你的应用程序已准备好运行。当你使用给定的邮政编码运行该应用程序时，屏幕外观如 [图 7.20] 所示。

![](img/c4119654311ebf24679359ca105ee6_174_0.png)

**[图 7.20 – 应用程序的输出]**

### 7.6.2 练习 2 - 用于翻译文本的桌面应用程序

在这个练习中，让我们创建一个桌面小部件，将英语单词翻译为您选择的语言，同时也练习使用 HTTPService 调用。

为了进行翻译，您可以使用 Google Ajax 语言 API，这是一个开发者常用的开放源 API。您可以在 http://code.google.com/apis/ajaxlanguage/ 查看此 API，以进一步扩展它或为应用程序添加更多语言。请按照以下步骤操作：

- **1.** 创建一个新的 Flex 项目，作为桌面应用程序。

- **2.** 添加两个文本输入框，一个用于要翻译的英语单词，另一个用于翻译后的文本。您可以添加一个组合框，列出您希望将文本翻译成的语言，以及一个按钮，点击该按钮将触发翻译过程。代码清单 7.24 展示了您可以使用的代码。

```xml
<mx:TextInput x="157" y="59" id="textToTranslate"/>
<mx:Button x="116" y="200" label="Translate" click="callGoogleLanguageTranslator()" width="104"/>
<mx:Label x="10" y="61" text="Text to be translated" width="128" height="47"/>
<mx:Label x="10" y="105" text="Translated text" width="119"/>
<mx:TextInput x="157" y="103" id="translatedText"/>
<mx:ComboBox x="189" y="151" width="128" id="language">
    <mx:dataProvider>
        <mx:Array>
            <mx:String>Chinese</mx:String>
            <mx:String>Italian</mx:String>
            <mx:String>Arabic</mx:String>
            <mx:String>Hindi</mx:String>
        </mx:Array>
    </mx:dataProvider>
</mx:ComboBox>
<mx:Label x="10" y="155" text="Language to be translated" width="158"/>
```

**代码清单 7.24 – 定义用户界面**

- **3.** 用于翻译的 Google 语言 API 接受符合 ISO 639 标准的语言代码，例如英语的 'en'。因此，对于放入组合框中的语言，请在下方所示的数组中提供这些代码，以便相应地映射并发送。

```actionscript
var languageArray:Array = new Array("zh", "it", "ar", "hi");
```

- **4.** 现在您可以使用 ActionScript 发起 http 服务请求。请求的 url 将是对 Google 翻译 API 的调用。您应该传递三个参数：API 版本、要翻译的文本以及语言对（源语言 | 目标语言）。*代码清单 7.25* 展示了要使用的代码。

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

**代码清单 7.25 - 发起 HTTPService 调用的函数**

- **5.** 响应格式是 API 返回的 JSON 编码结果。为了支持 JSON，您必须将 Flex corelib swc 文件添加到项目中。可以从 Adobe 网站下载该 corelib 文件，并将其作为库文件添加到项目的 Flex 构建路径中，如下所示

![](img/c4119654311ebf24679359ca105ee6_176_0.png)

- **6.** 可以在 http 服务调用的 ResultEvent 处理程序中处理响应，如 **代码清单 7.26** 所示

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

**代码清单 7.26 – ResultEvent 函数**

- **7.** 您还可以为 http 服务请求过程中可能发生的 Fault Event 提供处理程序。我们留给读者自行编写这部分代码。

- **8.** 是时候运行应用程序并查看如何将单词翻译为您选择的语言了。*图 7.22* 展示了运行应用程序后的输出。

![](img/c4119654311ebf24679359ca105ee6_177_0.png)

**图 7.22 – 语言翻译桌面应用程序**

- **9.** 您可以创建这个酷小部件的可分发包，并将其分享给您的朋友，他们可以将其安装在自己的桌面上。

## 7.7 摘要

在本章中，您学习了无论使用什么协议，与远程服务器进行通信是多么简单。

首先，您了解到如果远程服务器使用 SOAP 进行通信，则可以使用 Web 服务与之通信。如果使用的协议是 HTTP，则可以使用 HttpService。要访问位于服务器上的远程对象，可以使用 RemoteObject 配合 AMF 协议绕过任何网关。

然后您了解到，从服务器获得的响应可以不顾及类型而得到处理，因为 Flex 为我们提供了多种手段来处理它们（对象或 XML）。

最后，本章讨论了如何与 DB2 等数据库进行交互，并提供了一个详细的示例。

从这里开始，您将使用所学的概念来构建带有图表和数据网格的实时仪表板。

## 7.8 复习题

- 1. HttpService 和 Dataservice 之间的区别是什么？

- 2. 什么时候使用 RemoteObject 服务？

- 3. Adobe LifeCycle 数据服务的其他替代方案是什么？

