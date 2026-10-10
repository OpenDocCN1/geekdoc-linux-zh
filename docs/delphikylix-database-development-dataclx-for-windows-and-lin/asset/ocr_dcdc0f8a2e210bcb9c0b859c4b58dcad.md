# **LISTING 9.4  Continued**

```
```text
cdsContactsADDRESS2: TStringField;
cdsContactsCITY: TStringField;
cdsContactsSTATE: TStringField;
cdsContactsPOSTALCODE: TStringField;
cdsContactsCOUNTRY: TStringField;
cdsContactsPHONE: TStringField;
cdsContactsFAX: TStringField;
cdsContactsCELLULAR: TStringField;
cdsContactsPAGER: TStringField;
cdsContactsEMAIL: TStringField;
cdsContactsIMAGE: TBlobField;
cdsContactsNOTES: TMemOField;
cdsContactssqlToDos: TDataSetField;
cdsTodosTODOID: TIntegerField;
cdsTodosCONTACTID: TIntegerField;
cdsTodosDESCRIPTION: TStringField;
cdsTodosSCHEDULED: TSQLTimeStampField;
cdsTodosCOMPLETED: TSQLTimeStampField;
cdsContactsFullName: TStringField;
procedure DataModuleCreate(Sender: TObject);
procedure SocketConnection1BeforeConnect(Sender: TObject);
procedure cdsContactsReconcileError(DataSet: TCustomClientDataSet;
E: EReconcileError; UpdateKind: TUpdateKind;
var Action: TReconcileAction);
procedure cdsContactsCalcFields(DataSet: DataSet);
procedure DataModuleDestroy(Sender: TObject);
procedure cdsContactsNewRecord(DataSet: TDataSet);
procedure cdsTodosNewRecord(DataSet: TDataSet);
private
{ Private declarations }
public
{ Public declarations }
function GetNextID(DataSet: TCustomClientDataSet;
const PrimaryKey: string): Integer;
end;
var
DM: TDM;
implementation
uses RecErrorForm;
```
```