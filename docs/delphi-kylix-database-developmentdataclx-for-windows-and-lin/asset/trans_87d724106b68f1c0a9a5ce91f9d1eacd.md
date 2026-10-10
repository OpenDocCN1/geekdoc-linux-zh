

### 1.1 建立连接

**表 1.1 续**

| **属性** | **描述** |
| :--- | :--- |
| `LoadParamsOnConnect` | 当设置为 `True` 时，dbExpress 会在运行时从 `dbxconnections.ini` 配置文件中加载 `DriverName`、`GetDriverFunc`、`LibraryName`、`Params` 和 `VendorLib`。当设置为 `False` 时，所有属性必须在设计时进行设置。 |
| `LoginPrompt` | 当设置为 `True` 时，dbExpress 在连接到数据库时会提示用户输入用户名和密码信息。当设置为 `False` 时，应用程序必须通过 `Params` 属性直接提供用户名和密码信息。 |
| `Params` | 允许你在设计时或运行时设置特定于数据库的参数。有关更多信息，请参阅“设置数据库参数”一节。 |
| `TableScope` | 指定由 `GetTableNames` 返回的信息类型。有关此属性的更详细讨论，请参阅“检索数据库元数据”一节。 |
| `VendorLib` | 指用于连接数据库服务器的数据库厂商客户端库。例如，InterBase 提供了 `gds32.dll` 客户端库。 |

要连接到数据库，请设置适当的连接属性并执行以下两个语句之一：

```delphi
SQLConnection1.Connected := True;
```

或者

```delphi
SQLConnection1.Open;
```

这两个语句的作用相同，至于选择设置属性还是调用方法来连接数据库，取决于你的偏好。

你需要设置的属性取决于你选择使用命名连接还是未命名连接。以下两节将讨论这两种连接类型。

### 1.2 命名连接

命名连接是指在 `dbxconnections.ini` 文件中设置连接属性并为其指定名称。例如，以下示例说明了如何为会计软件包设置命名连接：

![](img/fe651f295b5f960d5463c4fb581d2281_21_0.png)

```ini
[Accounting]
BlobSize=-1
CommitRetain=False
Database=D:\InterbaseData\Accounting.gdb
DriverName=Interbase
LocaleCode=0
Password=masterkey
RoleName=Admin
ServerCharSet=ASCII
SQLDialect=1
Interbase TransIsolation=ReadComitted
User_Name=sysdba
WaitOnLocks=True
```

实际上，你可以在两个地方建立命名连接：在你的开发机器上，或最终用户的机器上。要在你的开发机器上创建命名连接，请将 TSQLConnection 组件放置到窗体或数据模块中。然后双击该组件，或右键单击组件并从弹出菜单中选择 `Edit Connection Properties`。此时将出现如图 1.1 所示的 `dBExpress Connection Editor`。

![](img/fe651f295b5f960d5463c4fb581d2281_22_0.png)

**图 1.1**  
连接编辑器帮助你轻松创建命名连接。

在连接编辑器的左侧，你会看到一个 `Driver Name` 组合框和一个 `Connection Name` 列表框。默认情况下，列表框显示你开发机器上所有现有的命名连接。如果你只想查看 Interbase、Oracle 或其他数据库服务器的命名连接，请从 `Driver Name` 组合框中选择合适的服务器。

点击列表框中的连接名称以查看该命名连接的设置，或点击工具栏上的 `Add Connection` 按钮（图标类似加号）来创建新的命名连接。

dbExpress 连接编辑器会在右侧的 Connection Settings 部分显示所选命名连接的设置。你应该为你的数据库引擎设置适当的参数。例如，对于 InterBase 连接，你至少需要设置 Database 属性。你可能还需要为 RoleName、SQLDialect 和 User_Name 输入值。

对于 Oracle 连接，你通常希望设置 Database，也可能需要为 User_Name 设置值。

> **注意**  
> 虽然你可以在命名连接中设置 Password，但我通常建议你不要这样做。如果你正在处理生产数据库，任何人都可以在你的电脑上打开连接编辑器（或简单地查看 dbxconnections.ini）来确定特定数据库的密码。因此，通常建议在运行时提供数据库密码。

如果你希望最终用户能够创建自己的命名连接，你应该将 dbxconnections.ini 与应用程序一起重新分发。你的用户可以手动编辑 dbxconnections，或者你可以编写并分发一个类似于 dbExpress 连接编辑器的实用程序，以帮助最终用户创建命名连接。

### 1.3 未命名连接

命名连接对于支持多种不同数据库服务器的应用程序很有用。然而，许多数据库应用程序是为单个数据库后端编写的。例如，你可能通过 CD 分发一个应用程序，该应用程序附带一个预创建的 InterBase 数据库，如零件列表或客户列表。在这些情况下，你的最终用户无需创建自己的数据库。他们只需访问你通过 CD 提供的数据库即可。

对于这些情况，命名连接并非必要。相反，你在设计时设置连接属性（如果你的应用程序需要在运行时让用户登录，则不包括 User_Name 和 Password）。

### 1.4 设置数据库参数

TSQLConnection 的 Params 属性包含特定于你所连接数据库服务器的设置。表 1.2 中列出的几个属性是所有数据库共有的。有关其他特定于数据库的属性的信息，请查阅你的数据库服务器文档。

**表 1.2** 通用数据库参数

| 属性 | 描述 |
| :--- | :--- |
| Database | 指定要连接的数据库。对于 InterBase 数据库，这指的是实际文件名，例如 `\SERVER\D:\RemoteData.gdb`。对于 Oracle 数据库，这指的是 TNSNames.ora 中唯一标识该数据库的条目。 |
| Password | 密码对应于 User_Name。通常不希望在设计时设置此项，因为这会绕过数据库安全性。 |
| User_Name | 在建立连接时使用的用户名。通常希望用户在运行时提供此信息。 |

你还可以在运行时访问 Params 属性来设置数据库参数，例如：

```delphi
SQLConnection1.Params.Values['Database'] := 'D:\Interbase\LocalDatabase.gdb';
```

对于 InterBase 连接，你可以用三种方式指定数据库：作为本地路径、作为 UNC 路径或作为 TCP 路径。以下是这三种结构的示例：

- `D:\Interbase\LocalDatabase.gdb`
- `\\SERVER\D:\Data\RemoteDatabase.gdb`
- `192.168.0.1:D:\Data\RemoteDatabase.gdb`

在连接数据库时，通常建议使用 UNC 路径或 TCP 路径，因为 InterBase 在某些情况下（例如从服务应用中连接数据库）使用本地路径连接数据库时会遇到困难。你可以通过使用 127.0.0.1 作为 IP 地址，使用 TCP 路径连接到本地数据库，如下所示：

`127.0.0.1:D:\Interbase\LocalDatabase.gdb`

### 1.5 控制登录

如前所述，连接的 LoginPrompt 属性决定 VCL/DataCLX 是否在运行时自动提示用户输入用户名和密码。如果你将 LoginPrompt 设置为 True，运行时将显示默认的登录对话框，如图 1.2 所示。

你可以通过处理连接的 OnLogin 事件并在那里设置适当的参数，来覆盖默认的登录对话框并自行提供获取用户名和密码的方式。以下代码片段展示了如何实现：

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

