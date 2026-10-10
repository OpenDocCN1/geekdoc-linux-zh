
```pascal
unit RemoteDataModule;

{$WARN SYMBOL_PLATFORM OFF}

interface

uses
  Windows, Messages, SysUtils, Classes, ComServ, ComObj, VCLCom, DataBkr,
  DBClient, ConManServer_TLB, StdVcl, DBXpress, FMVCbd, DB, SqlExpr,
  Provider;

type
  TConManDataServer = class(TRemoteDataModule, IConManDataServer)
    conn: TSQLConnection;
    sqlContacts: TSQLDataSet;
    sqlTodos: TSQLDataSet;
    dsContacts: TDataSource;
    pvContacts: TDataSetProvider;
    sqlID: TSQLDataSet;
    sqlContactsCONTACTID: TIntegerField;
    sqlContactsFIRST: TStringField;
    sqlContactsLAST: TStringField;
    sqlContactsDEAR: TStringField;
    sqlContactsTITLE: TStringField;
    sqlContactsCOMPANYNAME: TStringField;
    sqlContactsADDRESS1: TStringField;
    sqlContactsADDRESS2: TStringField;
    sqlContactsCITY: TStringField;
    sqlContactsSTATE: TStringField;
    sqlContactsPOSTALCODE: TStringField;
    sqlContactsCOUNTRY: TStringField;
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
    procedure pvContactsBeforeUpdateRecord(Sender: TObject;
      SourceCDS: TDataSet; DeltaCDS: TCustomClientDataSet;
      UpdateKind: TUpdateKind; var Applied: Boolean);

  private
    { Private declarations }
    function GetNextID: Integer;
  protected
    class procedure UpdateRegistry(Register: Boolean;
      const ClassID, ProgID: string); override;
  public
    { Public declarations }
  end;

implementation

uses MainForm;

resourcestring
SDatabaseIsOpen = 'Cannot perform this operation on an open database';

{$R *.DFM}

class procedure TConManDataServer.UpdateRegistry(Register: Boolean;
  const ClassID, ProgID: string);
begin
  if Register then
    begin
      inherited UpdateRegistry(Register, ClassID, ProgID);
      EnableSocketTransport(ClassID);
      EnableWebTransport(ClassID);
    end
  else
    begin
      DisableSocketTransport(ClassID);
      DisableWebTransport(ClassID);
      inherited UpdateRegistry(Register, ClassID, ProgID);
    end;
end;

procedure TConManDataServer.RemoteDataModuleCreate(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, 1, 0);
end;

procedure TConManDataServer.RemoteDataModuleDestroy(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, -1, 0);
end;

procedure TConManDataServer.pvContactsBeforeUpdateRecord(Sender: TObject;
  SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
  UpdateKind: TUpdateKind; var Applied: Boolean);
begin
  if UpdateKind = ukInsert then
    if SourceDS = sqlContacts then begin
      if DeltaDS.FieldByName('CONTACTID').OldValue <= 0 then
        DeltaDS.FieldByName('CONTACTID').NewValue := GetNextID;
      end
    else begin
      if DeltaDS.FieldByName('TODOID').OldValue <= 0 then
        DeltaDS.FieldByName('TODOID').NewValue := GetNextID;
    end;
end;

function TConManDataServer.GetNextID: Integer;
begin
  sqlID.ExecSQL;
  Result := sqlID.ParamByName('AValue').AsInteger;
end;

end;

initialization

  TComponetFactory.Create(ComServer, TConManDataServer,

    Class_ConManDataServer, ciMultiInstance, tmApartment);

end.
```

请注意，`RemoteDataModuleCreate` 和 `RemoteDataModuleDestroy` 方法会向主窗体发送 `UM_CONNECT` 消息。我们将在清单 9.3 中看到主窗体如何响应该消息并相应地更新其用户界面。

`pvContactsBeforeUpdateRecord` 会在对数据库进行更新之前自动调用。由于 `sqlContacts` 和 `sqlTodos` 以主/从关系连接，因此该方法会为这两个数据集调用。如果正在插入新记录，代码将检查该记录的主键是否小于或等于零（你将看到客户端侧生成的主键为负值，我将在讨论客户端代码时解释这一点）。如果是这样，代码将调用 `GetNextID` 方法，该方法执行 `GEN_ID` 存储过程以获取记录的下一个可用 ID。

### 清单 9.3

清单 9.3 包含应用程序服务器主窗体的源代码。如第 8 章所述，应用程序服务器通常不显示主窗体，但我发现显示一个小的主窗体来显示活动连接数通常很有用。
