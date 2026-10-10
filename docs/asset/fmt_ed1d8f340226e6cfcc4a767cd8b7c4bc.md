
| Database | 指定要连接的数据库。对于 InterBase 数据库，这指实际的文件名，例如 `\\SERVERID:\RemoteData.gdb`。对于 Oracle 数据库，这指 `TNSNames.ora` 中唯一标识数据库的条目。 |

| Password | 密码对应 `User_Name`。你通常不希望在设计时设置此项，因为这会绕过数据库安全机制。 |

| User_Name | 建立连接时使用的用户名。通常你希望用户在运行时提供此信息。 |

你还可以在运行时访问 `Params` 属性来设置数据库参数，例如：

```
SQLConnection1.Params.Values['Database'] := 'D:\Interbase\LocalDatabase.gdb';
```

对于 InterBase 连接，你可以用三种方式指定数据库：作为本地路径、作为 UNC 路径或作为 TCP 路径。以下是这三种结构方式的示例：

```
D:\Interbase\LocalDatabase.gdb
\\SERVERID:\Data\RemoteDatabase.gdb
192.168.0.1:D:\Data\RemoteDatabase.gdb
```

在连接数据库时，通常建议使用 UNC 路径或 TCP 路径，因为在某些条件下（例如在服务应用内部连接数据库时），InterBase 使用本地路径连接数据库会遇到困难。你可以使用 `127.0.0.1` 作为 IP 地址通过 TCP 路径连接到本地数据库，例如：

```
127.0.0.1:D:\Interbase\LocalDatabase.gdb
```

## 控制登录

如前所述，连接的 `LoginPrompt` 属性决定了 VCL/DataCLX 是否自动在运行时提示用户输入用户名和密码。如果将 `LoginPrompt` 设置为 `True`，运行时将显示默认的连接对话框，如图 1.2 所示。

你可以通过处理连接的 `OnLogin` 事件并在那里设置适当的参数，来覆盖默认登录对话框并提供获取用户名和密码的自定义方式。以下代码片段展示了如何操作：

```
procedure TForm1.SQLConnection1Login(Database: TSQLConnection;
LoginParams: TStrings);
var
TheUserName: string;
ThePassword: string;
begin
// 显示自定义对话框以获取 TheUserName 和 ThePassword
LoginParams.Values[ssUSERNAME] := TheUserName;
LoginParams.Values[ssPASSWORD] := ThePassword;
end;
```

![](img/52a35759a0f10dade27a840504be5d82_26_0.png)

**图 1.2**

Delphi 的默认数据库登录对话框。

## 断开数据库连接

当你完成应用程序中的数据库访问后，你应该断开连接。这将释放客户端和服务端的资源。你可以手动或自动断开数据库连接。

### 手动断开数据库连接

手动断开数据库连接很简单。只需发出以下两个命令之一：

```
SQLConnection1.Connected := False;
```

或者

```
SQLConnection1.Close;
```

使用哪种方法取决于你偏好设置属性还是调用方法来断开数据库连接。

### 自动断开数据库连接

如果你希望当没有打开的数据集时让 dbExpress 自动断开数据库连接，你应该将 `TSQLConnection.KeepConnection` 设置为 `False`。VCL/DataCLX 会监控连接上打开的数据集数量，当最后一个数据集关闭时，连接会自动断开。

**注意**

在连接建立时间较长的情况下，或在频繁打开和关闭数据集的应用程序中，你不应该将 `KeepConnection` 设置为 `False`。反复连接和断开数据库（特别是在连接耗时较长的情况下）可能会严重影响程序性能。

## 连接和断开事件

`TSQLConnection` 公开了一组在连接/断开过程中在适当时机触发的事件。这些事件及其用法列于表 1.3 中。

### 表 1.3 *TSQLConnection* 事件

| 事件 | 描述 |

| :--- | :--- |

| AfterConnect | 在数据库连接成功建立后触发。 |

| AfterDisconnect | 在数据库连接断开后触发。 |

| BeforeConnect | 在尝试连接数据库之前立即触发。你可以在此事件处理程序中引发异常以防止连接建立。 |

| BeforeDisconnect | 在断开数据库连接之前立即触发。你可以在此事件处理程序中引发异常以防止连接断开。 |

| OnLogin | 在建立连接之前触发，以便你可以在运行时提供用户名和密码。 |

列表 1.1 包含了一个应用程序的源代码，演示了这些事件在何时以及何种情况下触发。它还展示了如何防止用户连接或断开数据库。

**列表 1.1** 事件——MainForm.pas

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, DBXpress,
  ExtCtrls, DB, SqlExpr, QStdCtrls, QExtCtrls;
```

# **清单 1.1**（续）
