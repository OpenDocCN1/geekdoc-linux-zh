
与所有事件一样，第一个参数指示哪个对象调用了事件。`Request` 和 `Response` 参数将在下一节中讨论。最后，将 `Handled` 参数设置为 `true` 以表示该操作已处理。如果 `Handled` 为 `false`，将调用默认操作项。

# Kylix 开发第21章：Internet 应用 — NetCLX 509

## TWebRequest

封装在 `Request` 参数（类型 `TWebRequest`）中包含了可以从客户端获取的所有信息。这包括关于浏览器、cookies 等更多信息。使用各种属性可以方便地访问这些信息。下表显示了最常用的属性。其他属性和事件，请参阅 Kylix 帮助文件。

### 表 21-1

| TWebRequest 属性 | 描述 |
|---|---|
| ContentFields | 字符串集合，代表在提交表单时使用 HTTP POST 命令（`MethodType = mtPost`）发送的内容。 |
| CookieFields | 字符串集合，包含拆分为各个独立字符串的 cookie 内容。 |
| MethodType | 指示数据如何发送到服务器。选项有 `mtAny`, `mtPost`, `mtGet`, `mtPut` 和 `mtHead`。更多信息请参阅帮助文件。 |
| QueryFields | 字符串集合，代表在提交表单时使用 HTTP GET 命令（`MethodType = mtGet`）发送的内容。 |
| UserAgent | 识别发起请求的用户使用的浏览器及其版本。 |

大多数 WebBroker 应用程序将不需要调用 `TWebRequest` 的所有方法。

## TWebResponse

同样，`Response` 参数（类型 `TWebResponse`）封装了需要返回给用户的信息。设置适当的属性可以响应请求。表 21-2 显示了常用的属性。更多信息请咨询 Kylix 帮助文件。

### 表 21-2

| TWebResponse 属性 | 描述 |
|---|---|
| Content | 返回给客户端的数据字符串。 |
| Cookies | 给客户端的 cookie 集合。 |
| Expires | 设置信息的过期日期。主要供浏览器和缓存判断何时需要重新获取页面。 |

`TWebResponse` 的两个最常用方法如下所示。

# 第21章：Internet 应用 — NetCLX

### 表 21-3

| TWebResponse 方法 | 描述 |
|---|---|
| SendRedirect | 将网络客户端重定向到新的 URL。 |
| SendResponse | 立即发送响应。使用此方法将跳过 AfterDispatch 事件。 |

操作是 WebBroker 应用程序的核心。一旦理解，编写复杂的 Internet 应用程序就会变得简单。

## AfterDispatch 事件

`AfterDispatch` 提供在发送到客户端之前检查响应的方法。它只有在请求被操作项处理（例如使用 `TWebResponse.SendResponse`）时才会被调用。对响应的任何修改都是有效的。如果 `Handled` 参数设置为 `false`，则不会发送响应。

## BeforeDispatch 事件

`BeforeDispatch` 是一个事件处理器，允许在任何操作尝试处理请求之前对请求进行处理。如果 Dispatch 修改了响应，务必将 `Handled` 参数设置为 `true` 以跳过操作。`BeforeDispatch` 可以通过使用 `Response.SendResponse` 方法立即发送响应，如果使用了该方法，将跳过 `AfterDispatch` 事件的触发。

> `AfterDispatch` 和 `BeforeDispatch` 方法的签名类似于 `TWebAction` 的 `OnAction` 事件。它们的定义为：`procedure (Sender: TObject; Request: TWebRequest; Response: TWebResponse; var Handled: Boolean) of object;`

## OnCreate

`OnCreate` 事件通常用于初始化 Internet 应用程序。通常是打开数据库连接以及初始化其他使用的变量的好地方。

## OnDestroy

`OnDestroy` 事件用于清理任何打开的数据库连接并释放不属于 Web 模块的组件。

# 简单示例 — CGI 版本

让我们来看一个功能完备的 CGI 应用程序。在此示例中，创建一个 Web Server 应用程序，选择 CGI Standalone 独立执行文件。打开 WebModule 表单视图，并切换到 Events（事件）选项卡。双击 `AfterDispatch` 和 `BeforeDispatch` 事件。切换到 Properties（属性）选项卡并打开 Actions（动作）项编辑器。添加一个新项，通过将 `Default`（默认）属性设置为 `true`（真）将其设为默认句句处理程序。现在点击 Events 选项卡并双击 `OnAction` 事件。按照所示内容为这三个事件方法填入代码。

```go
unit Unit1;

interface

uses

Variants, SysUtils, Classes, HTTPApp;

type

TWebModule = class(TWebModule)

procedure TWebModule.WebActionItemAction(Sender: TObject;

Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);

procedure TWebModuleBeforeDispatch(Sender: TObject;

Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);

procedure TWebModuleAfterDispatch(Sender: TObject; Request: TWebRequest;

Response: TWebResponse; var Handled: Boolean);

private

  { Private declarations }

public

  { Public declarations }

end;

var

TWebModule: TWebModule;

implementation

uses WebReq;

{$R *.xfm}

procedure TWebModule.WebModuleBeforeDispatch(Sender: TObject;

Request: TWebRequest; Response: TWebResponse; var Handled: Boolean);

begin

  // BeforeDispatch
  Response.Content := '<html><title>My First CGI app with
Kylix</title><body>';
```

```go
// 在这种情况下，我们希望动作项触发，所以我们将 handled 设置为 false
Handled := false;
end;
```

```go
procedure TwebModule.TwebModuleWebActionItem1Action(Sender: TObject;
Request: TwebRequest; Response: TwebResponse; var Handled: Boolean);
begin
// Default Action Item
Response.Content := Response.Content + 'Hello from CGI World!';
// 为了让 AfterDispatch 事件触发，将 Handled 设置为 true
Handled := true;
end;
```

```go
procedure TwebModule.TwebModuleAfterDispatch(Sender: TObject);
Request: TwebRequest; Response: TwebResponse; var Handled: Boolean);
begin
// AfterDispatch
Response.Content := Response.Content + '</body></html>';
// 为了将此内容发回客户端，将 Handled 设置为 true
Handled := true;
end;
```

```go
initialization
WebRequestHandlerClass := TwebModule;
end.
```
