
# 重新分发 dbExpress 应用程序

## 附录 A

### 本附录内容

- 可重新分发文件 376
- 许可问题 378
- 基于 CD-ROM 的应用程序 378

本附录将告知您在编写完数据库应用程序后，重新分发该应用程序所需了解的注意事项。由于本书假设您正在使用 dbExpress 作为应用程序背后的数据访问技术，因此我不会解释如何重新分发 BDE 或 ADO。相反，我将专门关注 dbExpress 和 DataSnap。

### 可重新分发文件

重新分发使用 dbExpress 和 DataSnap 构建的应用程序非常简单——特别是如果您习惯于处理庞大的基于 BDE 或 ADO 的安装集时。为了支持 dbExpress 和 DataSnap，您只需与应用程序一起重新分发两个文件。

**注意**

嗯，这指的是除了您的应用程序可能需要的其他文件之外的两个文件。例如，如果您启用运行时包构建应用程序，还需要重新分发应用程序所需的运行时包。

### 重新分发 Windows 应用程序

对于在 Microsoft Windows 下运行的 VCL 或 CLX 应用程序，您需要重新分发应用程序所使用的数据库后端的驱动程序。数据库引擎及其相关的 Windows 驱动程序列在表 A.1 中。

**表 A.1 dbExpress Windows 驱动程序**

| 数据库 | Windows 驱动程序 |
| :--- | :--- |
| InterBase | Dbxepint.dll |
| Oracle | dbxepora.dll |
| DB2 | dbxepdb2.dll |
| MySQL | Dbxepmys.dll |

除了 dbExpress 驱动程序外，您还需要重新分发 MIDAS.DLL，其中包含客户端数据集技术所需的代码。

您可以将 dbExpress 驱动程序和 MIDAS.DLL 放置在应用程序能够找到它们的任何位置，即应用程序目录或 SYSTEM32 目录。这两个文件都不需要在 Windows 中注册。

如果您愿意，可以通过将 MidaSLib 包含在项目的 uses 子句中并重新编译，将 DataSnap 静态链接到客户端应用程序中。如果您这样做，则不需要与客户端应用程序一起重新分发 MIDAS.DLL（但是，必须与服务器应用程序一起重新分发）。

还可以通过链接相应的文件（如表 A.2 中列出的那样），将 dbExpress 驱动程序静态链接到应用程序中。

**表 A.2 dbExpress 静态链接驱动单元**

| 数据库 | 单元 |
| :--- | :--- |
| InterBase | Dbexpint |
| Oracle | Dbexpora |
| DB2 | dbexpdb2 |
| MySQL | Dbexpmy |

> **注意**
> 尽管 Delphi 6 支持将 dbExpress 和/或 DataSnap 静态链接到应用程序中，但您应该意识到，静态链接是一项新技术，与所有 DataSnap 代码并不完全兼容。例如，尝试调用 TClientDataSet.SaveToFile 将客户端数据集保存为 XML 文件时，静态链接时的保存格式与动态链接时不同。总之，如果您决定静态链接应用程序，请在发布给客户端之前进行彻底测试。

### 重新分发 Linux 应用程序

对于在 Linux 下运行的 CLX 应用程序，您需要重新分发相应的 Linux dbExpress 驱动程序。表 A.3 列出了 dbExpress 当前支持的数据库引擎及相关 Linux 驱动程序。

**表 A.3 dbExpress Linux 驱动程序**

| 数据库 | Linux 驱动程序 |
| :--- | :--- |
| InterBase | libsqlb.so |
| Oracle | libqor.so |
| DB2 | libsqldb2.so |
| MySQL | libsqlmy.so |

除了 dbExpress 驱动程序外，您还需要重新分发 LTBMMIDAS.SO。可重新分发的文件应放置在 /home/<usrname>/delphidir/bin 中。

### 许可问题

如果您编写的数据库应用程序处理本地数据（即数据不在不同机器之间传输），则无需担心应用程序的许可费。然而，如果数据包在不同机器之间传输，您需要向 Borland 支付少量的重新分发费，以使用 DataSnap 技术。

关于何时需要支付重新分发费以及费用多少的具体细节，请访问 Borland 网站 http://www.borland.com/midas。

### 基于 CD-ROM 的应用程序

许多数据库应用程序的一个常见需求是，它们需要能够访问 CD 上的（只读）数据库。这些应用程序（如电话簿、零件数据库等）通常与 CD 上的大型数据库一起重新分发。最终用户不需要更新数据——用户只需从 CD 访问数据即可。

要在 CD 上重新分发只读 InterBase 数据库，您需要首先对数据库运行 gfix 命令，如下所示：

```
gfix -read-only mydata.gdb
```

这将数据库标记为只读。

在您的应用程序中，您应该为所有数据集提供程序设置 poReadOnIy 选项，并为任何 TClientDataSets 设置 ReadOnly 为 True。这将确保任何数据库相关组件不会尝试更新数据库中的任何数据。

# 附录 B

## 本附录内容

- 什么是 dbExpress Plus？ 380
- 更多资讯 384

本附录简要介绍了 dbExpress Plus，这是 Thomas Miller 为 dbExpress 开发的开源附加库。可以从 CodeCentral 的 codecentral.borland.com 下载 dbExpress Plus。其 ID 为 #15945。

### 什么是 dbExpress Plus？

dbExpress Plus 是一项通过引入新组件来扩展 dbExpress 的开源努力，涵盖三个关键领域：

- 脚本
- 增强元数据
- 数据泵

以下章节对这些组件提供了简要概述。

#### 脚本

TSQLScript 提供了一种通过所谓的脚本一次执行多条 SQL 语句的方法。您可能熟悉 SQL 脚本文件。以下片段显示了一个简单的脚本文件。这实际上是用于创建 CONMAN 数据库的 SQL 脚本的一部分。

```sql
CREATE TABLE CONTACTS
(
    CONTACTID INTEGER NOT NULL,
    FIRST     VARCHAR(20),
    LAST      VARCHAR(30),
    DEAR      VARCHAR(40),
    TITTLE    VARCHAR(30),
    COMPANYNAME VARCHAR(50),
    ADDRESS1  VARCHAR(50),
    ADDRESS2  VARCHAR(50),
    CITY      VARCHAR(30),
    STATE     VARCHAR(20),
    POSTALCODE VARCHAR(10),
    COUNTRY   VARCHAR(30),
    PHONE     VARCHAR(20),
    FAX       VARCHAR(20),
    CELLULAR  VARCHAR(20),
    PAGER     VARCHAR(20),
    EMAIL     VARCHAR(40),
    IMAGE     BLOB SUB_TYPE 0 SEGMENT SIZE 4096,
    NOTES     BLOB SUB_TYPE TEXT SEGMENT SIZE 4096,
    PRIMARY KEY (CONTACTID)
);

CREATE UNIQUE INDEX IX_CONNAME ON CONTACTS (LAST, FIRST);

CREATE TABLE TODOS
(
    TODOID INTEGER NOT NULL,
    CONTACTID INTEGER NOT NULL,
    DESCRIPTION VARCHAR(50),
    SCHEDULED TIMESTAMP,
    COMPLETED TIMESTAMP,
    PRIMARY KEY (TODOID),
    FOREIGN KEY (CONTACTID) REFERENCES CONTACTS (CONTACTID) ON DELETE CASCADE
);
```

通常，您需要通过调用 TSQLConnection.ExecuteDirect 三次来分别执行这三条语句（创建表、创建索引、创建表），每条语句一次。

使用 TSQLScript，您可以使用以下两行代码：

```pascal
SQLScript1.SQL.LoadFromFile(ScriptFile);
SQLScript1.ExecuteDirect;
```

此代码片段假设 ScriptFile 是一个包含 SQL 脚本文件名的字符串变量。

#### 增强元数据

TSQLMetadata 提供了额外的、易于使用的方法来从数据库检索元数据信息。由于它继承自 TSQLConnection，您可以将在项目中需要使用增强元数据的地方用 TSQLMetadata 替代 TSQLConnection。

##### 检索表、视图和字段名称

TSQLMetadata 允许通过 GetTableNames、GetSysTabNames、GetViewNames 和 GetSynonymNames 方法轻松检索表名、系统表名、视图名和同义词名。这些方法中的每一个都接受一个参数，该参数指定返回结果的字符串列表。

```pascal
SQLMetaData1.GetTableNames(ListBox1.Items);
```

TSQLMetadata.GetFieldNames 检索构成表的字段。传入表名以检索字段名称的字符串列表作为结果，以及一个标志，指示是否应按声明顺序或按字母顺序返回字段。

TSQLMetadata.GetFieldNames 定义如下：

```pascal
procedure GetFieldNames(const ATableName: string; AList: TStrings;
    ASortOrder: TMetaDataSortOrder = soPosition); overload;
```

