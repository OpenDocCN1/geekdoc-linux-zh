

![](img/52a35759a0f10dade27a840504be5d82_362_0.png)

## 图 9.1
*ConMan 显示联系人信息，以及他们的照片、备注和计划待办事项。*

### 数据库结构

你已经在前面章节提供的示例程序中访问了 ConMan 数据库中的部分表。列表 9.1 包含了用于创建一个新的、空的 **CONMAN** 数据库的部分 SQL 脚本。

**contacts** 表用于存储公司名称、地址、电话号码等信息。为每个联系人创建一条记录，因此，如果同一家公司存在多个联系人，则公司数据会与每个联系人一起存储。

> #### 注意
> 实际上，这个数据库还应该包含一个 **Companies** 表，每个联系人持有对其所关联公司的反向引用。为了保持此应用程序规模的可管理性，我选择将公司和联系人数据都存储在 **contacts** 表中。

![](img/52a35759a0f10dade27a840504be5d82_362_1.png)

Todos 表存储每个联系人的提醒事项。例如，你可能希望存储一个提醒，在给定日期致电某位联系人以放置订单。Todos 表和 Contacts 表通过 Todos 表的 ContactID 字段进行链接。

除了表之外，数据库还包含一个名为 contactsByState 的存储过程。此过程是为在第 1 章和第 2 章中展示的示例应用程序中使用的；它不会在 ConMan 应用程序中使用。

最后，脚本创建一个生成器，用于填充 Contacts 和 Todos 表的主键，以及两个触发器，分别在输入新联系人和新待办事项时运行。触发器确保新联系人和待办事项总是获得唯一的主键。

## 列表 9.1 ConMan.SQL

```sql
/* Table: CONTACTS, Owner: SYSDBA */

CREATE TABLE CONTACTS
(
    CONTACTID    INTEGER NOT NULL,
    FIRST         VARCHAR(20),
    LAST          VARCHAR(30),
    DEAR          VARCHAR(40),
    TITLE         VARCHAR(30),
    COMPANYNAME   VARCHAR(50),
    ADDRESS1      VARCHAR(50),
    ADDRESS2      VARCHAR(50),
    CITY          VARCHAR(30),
    STATE         VARCHAR(20),
    POSTALCODE    VARCHAR(10),
    COUNTRY       VARCHAR(30),
    PHONE         VARCHAR(20),
    FAX           VARCHAR(20),
    CELLULAR      VARCHAR(20),
    PAGER         VARCHAR(20),
    EMAIL         VARCHAR(40),
    IMAGE         BLOB SUB_TYPE 0 SEGMENT SIZE 4096,
    NOTES         BLOB SUB_TYPE TEXT SEGMENT SIZE 4096,
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

/* Generators */
CREATE GENERATOR ID_GENERATOR;

SET TERM ^ ;

/* Stored Procedures */

CREATE PROCEDURE ID_GEN
RETURNS (
 AVALUE INTEGER
)
AS
BEGIN
 Avalue = GEN_ID(ID_GENERATOR, 1);
END ^

CREATE TRIGGER CONTACTS_INSERT FOR CONTACTS
ACTIVE BEFORE INSERT POSITION 0
AS
BEGIN
 IF (New.CONTACTID IS NULL) THEN
 New.CONTACTID = GEN_ID(ID_GENERATOR, 1);
END ^

CREATE TRIGGER TODOS_INSERT FOR TODOS
ACTIVE BEFORE INSERT POSITION 0
AS
BEGIN
 IF (New.TODOID IS NULL) THEN
 New.TODOID = GEN_ID(ID_GENERATOR, 1);
END ^

SET TERM ; ^
```

### 代码概述

ConMan 被分为应用程序服务器和客户端，提供真正的多筛选器功能。

ConMan 的完整源代码包含在七个单元中——其中两个是由 Delphi 自动为我们编写的。服务器端源单元包括以下内容：

- **MainForm.pas** 包含服务器主窗体的代码（它只是显示当前连接的客户端数量）。
- **RemoteDataModule.pas** 包含远程数据模块，数据库连接组件位于此处。
- **ConManServer_TLB.pas** 应用程序服务器的类型库导入文件。Delphi 自动创建并维护此单元。

客户端应用程序由以下单元组成：

- **DataModule.pas** 客户端数据模块，包括 DataSnap 组件和 TClientDataSets。
- **RecErrorForm.pas** 处理协调错误的窗体。此窗体由 Delphi 自动生成（有关处理协调错误的更多信息，请参阅第 7 章）。
- **MainForm.pas** 应用程序的主窗体。
- **TodoForm.pas** 便于添加或编辑待办事项的窗体。

以下各节更详细地描述服务器端和客户端应用程序。

### 服务器应用程序

正如前一节所述，应用程序服务器由三个源文件组成，其中你只需要为两个文件编写代码。

列表 9.2 包含应用程序服务器远程数据模块的源代码。从图 9.2 中可以看到，远程数据模块包含六个组件。它们是

- **conn** 用于连接数据库的 TSQLConnection 组件。
- **sqlContacts** 用于从 Contacts 表检索数据的 TSQLDataSet 组件。
- **sqlTodos** 用于从 Todos 表检索数据的 TSQLDataSet 组件。
- **sqlID** 调用数据库中存储过程 ID_GEN 以检索每个插入记录的唯一 ID 的 TSQLDataSet。
- **prgContacts** 用于在 `sqlContacts` 和 `sqlTodos` 之间建立服务器端主/从关系的 TNameDataSource 组件。
- **prgServerApps** 用于向客户端应用程序提供远程联系人数据节点的 TServerProvider 组件。由于联系人和待办事项以主/从关系连接，因此在主级别只需要一个提供程序（参阅第 7 章“如果你需要重温服务器端主/从关系”）。

图 9.2 展示了设计时的远程数据模块。

![](img/52a35759a0f10dade27a840504be5d82_366_0.png)

## 图 9.2
*远程数据模块及其数据访问组件。*

## **列表 9.2** ConManServer\RemoteDataModule.pas

```pascal
unit RemoteDataModule;

{$IFDEF SYMBOL_PLATFORM_OFF}

uses
  Vcl.Forms;

uses
  Windows, Messages, SysUtils, Classes, ConvServ, ComDef, VclCom, DataBkr,
  DBClient, CommandServer_TLB, DsDvI, DBAccess, FMXDb, DB, SqlExpr,
  Provider;

type
  TCommandDataServer = class(TRemoteDataModule, ICommandDataServer)
    conn: TSQLConnection;
    tblContacts: TSQLDataSet;
    tblTodos: TSQLDataSet;
    tblContacts: TDataModule;
    po1Contacts: TDatabaseProvider;
    sqlin: TSQLDatabase;
    tblContactsToSQLDataSet: TOnesToFields;
    sqlinContactsToFIED: TOnesToFields;
    sqlinContactsToSQLDataSet: TOnesToFields;

    sqlContactsTITLE: TStringField;
    sqlContactsCOMPANYNAME: TStringField;
    sqlContactsADDRESS1: TStringField;
    sqlContactsADDRESS2: TStringField;
    sqlContactsCITY: TStringField;
    sqlContactsSTATE: TStringField;
    sqlContactsPOSTALCODE: TStringField;
    sqlContactsCOUNTRY: TStringField;
    sqlContactsPHONE: TStringField;
    sqlContactsFAX: TStringField;
    sqlContactsCELLULAR: TStringField;
    sqlContactsPAGER: TStringField;
    sqlContactsEMAIL: TStringField;
    sqlContactsIMAGE: TBlobField;
    sqlContactsNOTES: TMemoField;
    sqlTodosTODOID: TIntegerField;
    sqlTodosCONTACTID: TIntegerField;
    sqlTodosDESCRIPTION: TStringField;
    sqlTodosSCHEDULED: TSQLTimeStampField;
    sqlTodosCOMPLETED: TSQLTimeStampField;

    procedure RemoteDataModuleCreate(Sender: TObject);
    procedure RemoteDataModuleDestroy(Sender: TObject);
    procedure pvContactsBeforeUpdateRecord(Sender: TObject);
    SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
    UpdateKind: TUpdateKind; var Applied: Boolean);

  private
    { Private declarations }
    function GetNextID: Integer;

  protected
    class procedure UpdateRegistry(Registry: Boolean;
      const ClassID, ProgID: string); override;

  public
    { Public declarations }
  end;

implementation

uses MainForm;

resourcestring
  $DatabaseIsOpen = 'Cannot perform this operation on an open database';

{$R *.DFM}
```

