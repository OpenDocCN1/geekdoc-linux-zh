
# 数据库优化第 18 章

这将为 `mydatabase.gdb` 设置缓冲区为 10,000 个数据库页。这意味着第一次连接到此数据库将导致 InterBase 向其缓存中添加 10,000 个数据库页内存。第二个及后续用户将增加零缓冲区。

缓冲区的范围在 0 到 65,535 之间。Rob 的实证测试显示，缓冲区从 10,000 增加到 20,000 性能提升微乎其微，因此我通常使用 10,000。

# 在 InterBase 上使用单处理器机器

InterBase（SuperServer 架构）不知道如何正确使用多个处理器。在 NT 上，如果你有多个处理器，InterBase 进程会在处理器之间切换。这看起来像 InterBase 正在使用多个处理器，但实际上并没有。经验证据表明，由于 InterBase 进程的切换，性能可能会下降高达 30%。

如果你有一台多处理器机器并在上面运行 InterBase，你可以将 InterBase 作为应用程序运行，并将其亲和性设置为一个处理器，以防止 InterBase 在处理器之间切换。InterBase 的未来版本应该会提供多处理器支持，但在 InterBase 6.0 或更低版本中还没有。

## 总结

在本章中，你看到了各种数据库优化技术。大多数 SQL 服务器的讨论都使用了 InterBase，但许多专门提到 InterBase 的信息也适用于你的数据库。当你设计查询时，你可以使用像你用过的工具工具来查看发生了什么，并相应地优化你的查询。

# Web 第五部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_845_0.png)

图 19.1
Netscape Navigator 浏览器中的 CGI 表单。

但 Web 服务器知道对于发送过来的数据应该启动哪个 CGI 应用程序吗？对于这一点，你需要查看表单本身的 `ACTION` 参数（代码的第一行）。`ACTION` 指定了 CGI 程序的确切位置，在此例中为 `http://www.drbob42.co.uk/cgi-bin/hello`。

## Apache Web 服务器

Apache Web 服务器可以配置为使用 CGI 协议来处理 Web 服务器应用程序。然而，CGI 的缺点之一是，在每次请求后，Web 服务器应用程序都会再次被卸载。这消耗了大量不必要的时间，如果你能找到一种加载 Web 服务器应用程序并使其保持在内存中的方法（就像 Web 服务器本身，它也是一个持续运行的进程），就可以避免这一点。新的客户端请求将只需路由到 Web 服务器应用程序，从而获得快得多的响应。

当然，如果这不可行，我就不会提到它。通过 Apache Web 服务器，你可以构建所谓的“动态共享对象”，这些对象可以在 Apache Web 服务器的上下文中加载，它们只需要加载一次（并且在后续请求中不需要卸载）。

## Kylix 与 CGI

你可以使用任何版本的 Kylix 编写 CGI 应用程序，尽管 Web-Broker 组件的 NetCLX 支持在 Kylix Server Developer 及更高版本中可用（而 Kylix Desktop Developer 没有）。然而，你仍然可以使用 Kylix Desktop 编写 Web 服务器应用程序——无需 WebBroker——前提是自己编写所有必要的 CGI 技术（查看环境变量、读取标准输入、写入标准输出）。一个控制台应用程序完全可以，但为了避免需要自己编写所有的 CGI 细节，我有一个名为 `DrBobCGI` 的小单元，可用于 Kylix（或者说 Delphi）的 CGI 应用程序开发，而无需 WebBroker；Linux 版本显示在列表 19.1 中。

# Apache 服务器应用程序 第 19 章

请在自担风险的情况下使用（它对我有效），请参阅我的网站 `http://www.drbob42.com/DrBobCGI` 以获取更多信息以及完整的 Windows/Linux 版本。

# unit DrBobCGI

```
=================================================================
{ DrBobCGI © 1999 by Bob Svart (aka Dr.Bob - www.drbob42.com) }
{ version 1.0 - 通过 "value()" 获取标准 CGI 变量 }
{ version 2.0 - 获取 CGI 值、cookies 和 IP/UserAgent 值 }
{ version 2.1 - 获取 Authorisation 值（base64 编码的字符串） }
{ version 3.0 - 移植到 Kylix 1.0，同样支持 Delphi 4+ }
{   注意：DrBobCGI 不兼容 Delphi 3 或更低版本 }
{ version 3.1 - 将 GET 和 POST 字段合并到一个 Data 字段中 }
=================================================================
```

```
interface
```

```
type TRequestMethod = (Unknown,Get,Post);
var RequestMethod: TRequestMethod = Unknown;
```

```
var ContentLength: Integer = 0;
RemoteAddress: String[16] = ''; { IP }
HttpUserAgent: String[128] = ''; { 浏览器, 操作系统 ... }
Authorization: String[255] = ''; { 授权 }
ScriptName: String[128] = ''; { scriptname URL }
```

```
function Value(const Field: ShortString; Count: Boolean = True); ShortString;
function CookieValue(const Field: ShortString); ShortString;
```

```
implementation
uses
{$IFDEF LINUX
Libc;
{$ENDIF}
SysUtils;
```

```
function _Value(const Field: ShortString; Sep: Char = '&');
const Data: AnsiString;
```

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_845_0.png)

列表 19.1 继续

```
Convert: Boolean = True): ShortString;
```

```
var
  i: Integer;
  Str: String[3];
  len: absolute Result;
begin
  len := 0; { Result := '' }
  i := Pos(Sep+Field='',Data);
  if i = 0 then
    begin
      i := Pos(Field+='',Data);
      if i > 1 then i := 0
    end
    Else Inc(i); { skip '&' }
  if i > 0 then
    begin
      Inc(i,Length(Field)+1);
      while Data[i] <> Sep do
        begin
          Inc(len);
          if (Data[i] = '%') and Convert then
            begin
              Str := 'S00';
              Str[2] := Data[i+1];
              Str[3] := Data[i+2];
              Inc(i,2);
              Result[len] := Chr(StrToInt(Str))
            end
            else
              if (Data[i] = ' ') and not Convert then Result[len] := '+'
              else
                Result[len] := Data[i];
          Inc(i)
        end
    end
  else Result := ''
end;
```
