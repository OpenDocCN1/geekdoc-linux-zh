
| `Password` | 密码对应于 `User_Name`。通常不希望在设计时设置此项，因为这会绕过数据库安全性。 |
| `User_Name` | 在建立连接时使用的用户名。通常希望用户在运行时提供此信息。 |

你还可以在运行时访问 `Params` 属性来设置数据库参数，例如：

```delphi
SQLConnection1.Params.Values['Database'] := 'D:\Interbase\LocalDatabase.gdb';
```

对于 InterBase 连接，你可以用三种方式指定数据库：作为本地路径、作为 UNC 路径或作为 TCP 路径。以下是这三种结构的示例：

- `D:\Interbase\LocalDatabase.gdb`
- `\\SERVER\D:\Data\RemoteDatabase.gdb`
- `192.168.0.1:D:\Data\RemoteDatabase.gdb`

在连接数据库时，通常建议使用 UNC 路径或 TCP 路径，因为 InterBase 在某些情况下（例如从服务应用中连接数据库）使用本地路径连接数据库时会遇到困难。你可以通过使用 `127.0.0.1` 作为 IP 地址，使用 TCP 路径连接到本地数据库，如下所示：

`127.0.0.1:D:\Interbase\LocalDatabase.gdb`

### 1.5 控制登录

如前所述，连接的 `LoginPrompt` 属性决定 VCL/DataCLX 是否在运行时自动提示用户输入用户名和密码。如果你将 `LoginPrompt` 设置为 `True`，运行时将显示默认的登录对话框，如图 1.2 所示。

你可以通过处理连接的 `OnLogin` 事件并在那里设置适当的参数，来覆盖默认的登录对话框并自行提供获取用户名和密码的方式。以下代码片段展示了如何实现：

![](img/fe651f295b5f960d5463c4fb581d2281_25_0.png)

```delphi
procedure TForm1.SQLConnection1Login(Database: TSQLConnection;
  LoginParams: TStrings);
var
  TheUserName: string;
  ThePassword: string;
begin
  // 显示自定义对话框以获取 TheUserName 和 ThePassword

  LoginParams.Values[szUSERNAME] := TheUserName;
  LoginParams.Values[szPASSWORD] := ThePassword;
end;
```

### 1.6 断开数据库连接

当你完成对应用程序中数据库的访问时，应该断开连接。这将释放客户端和服务端的资源。你可以手动或自动断开数据库连接。

#### 手动断开数据库连接

手动断开数据库连接很简单。只需发出以下两个命令之一：

```delphi
SQLConnection1.Connected := False;
```

或者

```delphi
SQLConnection1.Close;
```

使用哪种方法取决于你偏好于设置属性还是调用来断开数据库连接。

#### 自动断开数据库连接

如果你希望 dbExpress 在没有打开的数据集时自动断开数据库连接，你应该设置 `SQLConnection.KeepConnection := False`。VCL/DataCLX 会监视连接上打开的数据集数量，当最后一个数据集关闭时，连接会自动断开。

## 注意

当连接建立耗时较长，或在需要频繁打开和关闭数据集的应用中，不应将 `KeepConnection` 设置为 `False`。反复连接和断开数据库（尤其是在连接耗时的情况下）会严重影响程序性能。

## 连接和断开连接事件

`TSQLConnection` 提供了一组事件，这些事件在连接/断开连接过程中的关键时刻触发。这些事件及其用法列表见表格 1.3。

**表 1.3 TSQLConnection 事件**

- **AfterConnect**  
  在数据库连接成功建立后触发。
- **AfterDisconnect**  
  在数据库连接断开后触发。
- **BeforeConnect**  
  在尝试建立数据库连接之前立即触发。您可以在此事件处理程序中引发异常，以阻止连接建立。
- **BeforeDisconnect**  
  在断开数据库连接之前立即触发。您可以在此事件处理程序中引发异常，以阻止连接断开。
- **OnLogin**  
  在建立连接之前触发，以便您可以在运行时提供用户名和密码。

列表 1.1 包含一个应用程序的源代码，演示了这些事件何时以及在什么情况下触发。它还展示了如何阻止用户连接或断开与数据库的连接。

### 列表 1.1 事件—MainForm.pas
