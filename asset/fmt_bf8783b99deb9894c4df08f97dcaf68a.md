
DSO 模块生成的源代码似乎与 CGI 应用生成的源代码非常相似。将之前的代码（用于 CGI 独立可执行文件）与以下代码（Apache DSO 模块）进行比较，你就能亲自看到差异：

```pascal
library Project1;

uses
WebBroker,
HTTPApp,
ApacheApp,
Unit1 in 'Unit1.pas' {WebModule1: TWebModule};

exports
apache_module name 'Project1_module';
```

# Web 服务器开发 第 20 章

```pascal
begin
Application.Initialize;
Application.CreateForm(TWebModule, TWebModule);
Application.Run;
end.
```

第一个区别是 CGI 应用是一个程序（带有额外的 `{APP CONSOLE}` 设置），而 DSO 模块是一个库。第二个区别是 CGI 应用使用 `CGI` 单元，而 DSO 模块使用 `HTTP` 和 `ApacheApp` 单元。第三也是最后一个区别是，DSO 模块必须导出一个名为 `apache_module` 的单一入口点（它似乎缺少了 `(*res)` 资源标识符）。

# Apache CGI 和 DSO

它们共同的点当然是类型为 `TWebModule` 的 `WebModule`（以防你没有选择名称或类型）。我们可以利用这一点：两个项目可以使用同一个 Web 模块！一旦你通过让两个项目属于同一个项目组来实现这一点，你就可以通过选择正确的项目作为活动项目，在 CGI 应用和 DSO 模块之间进行切换。你仍然可以使用项目共享的同一个 Web 模块。

创建此类具有两个项目（但目标不同）和一个单一共享 Web 模块的项目组所需的步骤如下：

- 1. 启动 Kylix 并关闭默认项目。
- 2. 选择文件（File）、新建（New）并选择 Web 服务器应用程序（Web Server Application）。
- 3. 选择 CGI 并点击 OK。
- 4. 保存项目和 Web 模块。指定正确的文件名——以后无法重命名 Web 模块，因为它将被两个项目共享。
- 5. 启动项目管理器（Project Manager）。
- 6. 右键点击项目组并选择添加新项目（Add New Project）。
- 7. 再次选择 Web 服务器应用程序。
- 8. 这次选择 DSO 作为选项，并点击 OK。
- 9. 从 DSO 项目中移除 Web 模块。
- 10. 保存 DSO 项目（如果已给定名称）。
- 11. 在项目管理器中右键点击 DSO 项目并选择添加（Add）。
- 12. 将 Web 模块的单元文件名添加到 DSO 项目。

现在，CGI 项目和 DSO 项目将共享同一个 Web 模块。如果你也保存了项目组，你就可以在这两个目标之间切换。否则，你只需要为特定目标加载正确的项目。

这种配置的益处是不言而喻的：你可以使用简单的 CGI 应用对 Web 模块进行原型设计和测试，但之后可以在现实世界中将其部署为 DSO 共享模块，因为它具有许多额外优势。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_858_0.png)

# Web

## 第五部分

在本章中，我将选择并处理一个 CGI 应用，它不需要进一步配置。如果你想选择并处理 DSO 模块，你需要确保 Apache Web 服务器已为 DSO 模块进行了配置（参见第 19 章）。除此之外，只有极少数情况编写 DSO 应用与编写 CGI 应用有所不同，当出现这种情况时我会予以说明。

# WebBroker 组件

在“新建 Web 服务器应用程序”对话框中做出选择（CGI 或 DSO）后，Kylix 会生成一个 Web 模块项目和一个空的 Web 模块。让我们查看 `WebBap42` 下的此新项目以及 `webmod42` 下的 Web 模块，因为它将是整个本章（以及下一章）要使用的项目。

模块是放置特殊 WebBroker 组件（例如 `PageProducers` 和 `TableProducers`）的地方。WebBroker 组件可以在组件面板板（Component Palette）的 Internet 标签卡中找到（仅限 Kylix 服务器开发者）；请参见图 20.3。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_859_0.png)

## 图 20.3

组件面板板的 Internet 标签卡包含 WebBroker 组件；从左到右为：`WebDispatcher`、`TableProducer`、`Producer`。其他组件（`TCPClient`、`TCPServer`）不在 Internet 标签卡中，但在 General 标签卡中。

# TDispatcher

`WebDispatcher` 组件是你需要放到 Web 模块的组件。事实上，此组件已经内置在 Web 模块中了，稍后你会看到。通过添加 `TDispatcher` 将你的数据模块转换为 Web 模块。注意，当应用程序是 Web 服务器时，调度器才会被使用（因此对于桌面应用程序，它是非活跃的）。

# TWebModule

正如我解释过的，Web 模块基本上是一个带有 `TDispatcher` 组件的数据模块。你问调度什么？嗯，Web Dispatcher 将输入的请求分发到特定的 Action 项。

Web 模块最重要的属性是类型为 `TActionItems` 的 `Actions` 属性。这是 Web 服务器可以执行的操作集合。为了维护 WebActionItems，你需要使用 Actions Editor。你可以通过多种方式启动 Actions Editor。首先，你可以在对象检查器中点击 `Actions` 属性值旁边的省略号 `...`。你也可以右键点击 Web 模块并选择 Actions Editor，以指定 Web 模块响应的不同请求。

最初，Actions Editor 会非常小，列宽不可读（见图 20.4）；你必须调整对话框和列的大小使其可读（遗憾的是，新的大小不会保存，因此下次你使用 Actions Editor 时它会再次变小）。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_860_0.png)

**图 20.4**

Web 模块和 Actions Editor

在 Actions Editor 内部，你可以定义多个类型为 `TActionItem` 的 Web 操作项（只需点击 `Ins` 向列表添加新项）。这些项目中的每一个都可以通过 `PathInfo` 属性区分开。`PathInfo` 包含了在查询字段之前添加到请求中的额外信息。这意味着单个 Web 服务器应用程序可以响应不同的 Web 操作项。

对于本章中使用的示例，你必须定义五个不同的 `TWebActionItems`，这些将用于说明 Web 模块组件的不同用法和功能（见图 20.5）。下一章将使用更多的操作项展示一些高级功能。

## Web

### 第五部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_861_0.png)

#### 图 20.5

Web 操作项编辑器（Action Item Editor）。

注意，第一个项目没有指定 `PathInfo`，它是（唯一的）默认 Web 动作项。这意味着当没有提供 `PathInfo`，或者没有其他 `PathInfo` 匹配给定的 `PathInfo` 时（即需要默认动作时），被选中的将是该 `TWebWidgetItem`。这个 `TWidgetItem` 将被主要用于演示某种效果。其他四个 `PathInfo` 值必须为 `/hello`、`/records` 和 `/query`，并将将用于整个章节的示例。

要为特定的 `TWebWidgetItem` 编写事件处理程序，你首先需要在 Actions 编辑器中选择该 `WebListItem`（见图 20.5）。然后转到对象检查器（Object Inspector）的标签页，并双击 Event（事件）操作。这将带你代码编辑器，你将在其中看到以下代码：

```
procedure TWebModule1.WebModule1WebActionItem1Action(Sender: TObject;
Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);
begin

end;
```

在在这里编写任何事件处理代码之前，你必须先学习参数的细节。`OnAction` 事件有四个参数：`Sender`、`Request`、`Response` 和 `Handled`。`Sender` 是 `TWebWidgetItem` 本身。`Handled` 可指定处理（此动作）是否已完成。然而，`Request` 和 `Response` 参数尤其重要，需要更多的关注。

## TWebResponse
