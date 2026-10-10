# **LISTING 7.1** *Continued*

```
Label: TLabel;
btnClearEventLog: TButton;
procedure FormCreate(Sender: TObject);
procedure Timer1Timer(Sender: TObject);
procedure btnApplyUpdatesClick(Sender: TObject);
procedure btnCancelUpdatesClick(Sender: TObject);
procedure ClientDataSet1ReconcileError(DataSet: TCustomClientDataSet;
  E: EReconcileError; UpdateKind: TUpdateKind);
var Action: TReconcileAction);
procedure DataSetProvider1BeforeUpdateRecord(Sender: TObject;
  SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
  UpdateKind: TUpdateKind; var Applied: Boolean);
procedure DataSetProvider1AfterApplyUpdates(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1BeforeExecute(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1AfterGetParams(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1AfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1AfterRowRequest(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1AfterUpdateRecord(Sender: TObject;
  SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
  UpdateKind: TUpdateKind);
procedure DataSetProvider1BeforeApplyUpdates(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1BeforeExecute(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1BeforeGetParams(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1BeforeGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
procedure DataSetProvider1BeforeRowRequest(Sender: TObject;
  var OwnerData: OleVariant);
function DataSetProvider1DataRequest(Sender: TObject;
  Input: OleVariant): OleVariant;
procedure DataSetProvider1GetData(Sender: TObject;
  DataSet: TCustomClientDataSet);
procedure DataSetProvider1GetDataSetProperties(Sender: TObject;
  DataSet: TDataSet; out Properties: OleVariant);
procedure DataSetProvider1GetTableName(Sender: TObject;
  DataSet: TDataSet; var TableName: String);
procedure DataSetProvider1UpdateData(Sender: TObject;
  DataSet: TCustomClientDataSet);
```