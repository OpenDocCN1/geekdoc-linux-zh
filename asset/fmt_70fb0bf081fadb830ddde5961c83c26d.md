
保存单元并将项目重命名为 `SimpleCGI`。编译应用程序。修复任何错误，直到 CGI 应用程序成功编译。现在是时候测试此应用程序并看看会发生什么了。

找到 Apache 所在的文档根目录。对于某些发行版，它位于 `/var/www/` 目录。对于另一些发行版，它位于 `/home/~httpd` 目录。在文档根目录下，有一个名为 `cgi-bin` 的目录。将可执行文件复制到此目录。打开浏览器（如 Netscape 或 Conqueror），并使用以下 URL：`http://localhost/cgi-bin/SimpleCGI`。浏览器显示以下消息：

Hello from CGI World!
恭喜你！使用 Kylix 编写互联网应用程序就是如此简单。

> 提示：“localhost”是运行 CGI 应用程序的计算机 IP 地址的别名。要从另一台查看结果，请指定运行 CGI 应用程序的 IP 地址或域名。

# Kylix 2 开发第21 章：互联网应用程序 — NetCLX 513

> 提示：CGI 应用程序可以安装在上述目录以外的其他目录。有关如何添加额外的 cgi-bin 目录的详情，请参阅 Kylix README 文件。

# 简单示例 — DSO 版本

创建一个 DSO 版本的应用程序与 CGI 版本一样简单。但是，为了让 Apache 与 DSO 工作，需要一些额外的步骤。按照所示内容填入代码，只需将 CGI 应用程序中的引用替换为 DSO。

```go
unit;

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

保存单元并将项目重命名为 `SimpleDSO`。编译应用程序。修复任何错误，直到 DSO 应用程序成功编译。现在是安装并测试此应用程序了。配置 DSO 需要一些额外的步骤。为了执行这些步骤，需要 root 权限。

- 1. 停止 Apache。
对于某些发行版，通过使用位于 `/usr/bin` 的 `apache` 命令来实现，执行：
`/usr/sbin/apache`
其他发行版使用位于 `/etc/init.d/` 目录的 `httpd` 脚本。如果是这种情况，使用以下命令：
`/etc/init.d/httpd stop`

- 2. 将 Apache DSO 复制到 `httpd` 所在的位置，例如 `/usr/lib/apache/` 目录。

# Kylix 2 开发第21 章：互联网应用程序 — NetCLX 515

- 3. 编辑 `httpd.conf`，通常位于 `/etc/httpd/conf/httpd.conf`。需要两个项来通知 Apache DSO 模块。
a. `LoadModule` 部分的项所示：
`LoadModule SimpleDSO_module /usr/lib/apache/libDSO.so`
其中
`LoadModule` 是 Apache 命令
`SimpleDSO_module` 是项目 `dpr` 文件中的导出名称
`/usr/lib/apache/libDSO.so` 是使用 Kylix 构建的 DSO 路径。
b. 关联路径的项以绑定已安装的 DSO。对于示例，`/dso` 路径绑定到 `SimpleSO` 库。
# 引用 DSO 的位置
`<Location /dso>`
`SetHandler libsimpleso-handler`
`</Location>`

注意 `SetHandler` 的参数是全小写的，尽管 DSO 是混合大小格式。还要注意在 DSO 文件名后附加了 `-handler` 。

- 4. 启动 Apache。
使用 `apachectl` 或 `httpd` 命令启动 Apache：
`/usr/sbin/apachectl start`
或
`/etc/init.d/httpd start`

- 5. 打开浏览器并访问以下 URL：`http://localhost/dso`。
浏览器将显示 `Hello from DSO World!`

# 页面生产者

到为止，应用程序演示了如何直接在源代码中存储静态 HTML 页面。遗憾的是，还有其他有用组件可以更容易编写动态 Web 应用程序。这些非视觉组件被称为页面生产者，位于组件工具栏的 Internet 选项卡中。

# TPageProducer

简单的生产者是 `TPageProducer` 组件。该组件提供了将 HTML 模板存储在字符串列表或模板文件的方法。此外，可以在 HTML 文档中嵌入 HTML 透明标签，并在运行时动态替换为有效的 HTML 代码。

# 第 21 章：网络应用程序 — NetCLUX

不要在 WebBroker 程序中硬编码 HTML 代码，而是使用 PageProducer 组件，使 HTML 页面的维护变得简单得多。

## HTML 透明标签

页面生成器的一个优秀特性是透明 HTML 标签。这些是被页面生成器识别为标签的特殊标记字段。它们的格式如下：

```
<#TagName [Parameter1=Value1 Parameter2=Value2 ..>
```
