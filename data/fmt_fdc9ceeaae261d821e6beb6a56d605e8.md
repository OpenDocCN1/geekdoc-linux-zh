
`Label11`: `TLabel`;

`cbCountry`: `TComboBox`;

`btnRetrieve`: `TButton`;

`conn`: `TSQLConnection`;

`sqlContacts`: `TSQLDataSet`;

`sqlContactsFIRST`: `TStringField`;

`sqlContactsLAST`: `TStringField`;

`sqlContactsDEAR`: `TStringField`;

`sqlContactsTITLE`: `TStringField`;

`sqlContactsCOMPANYNAME`: `TStringField`;

`sqlContactsADDRESS1`: `TStringField`;

`sqlContactsADDRESS2`: `TStringField`;

`sqlContactsCITY`: `TStringField`;

`sqlContactsSTATE`: `TStringField`;

`sqlContactsPOSTALCODE`: `TStringField`;

`sqlContactsCOUNTRY`: `TStringField`;

`sqlContactsPHONE`: `TStringField`;

`sqlContactsFAX`: `TStringField`;

`sqlContactsCELLULAR`: `TStringField`;

`sqlContactsPAGER`: `TStringField`;

`sqlContactsEMAIL`: `TStringField`;

`sqlContactsIMAGE`: `TloblField`;

`sqlContactsNOTES`: `TmemoField`;

`DataSource1`: `TDataSource`;

`sqlActivities`: `TSQLDataSet`;

`sqlActivitiesCONTACTID`: `TIntegerField`;

`sqlActivitiesDESCRIPTION`: `TStringField`;

`sqlActivitiesSCHEDULED`: `TSQLTimeStampField`;

`sqlActivitiesCOMPLETED`: `TSQLTimeStampField`;

`sqlContactsCONTACTID`: `TIntegerField`;

`sqlActivitiesTODOID`: `TIntegerField`;

`procedure btnConnectClick(Sender: TObject);`

`procedure btnNextClick(Sender: TObject);`

`procedure btnDisconnectClick(Sender: TObject);`

`procedure btnRetrieveClick(Sender: TObject);`

`procedure connAfterDisconnect(Sender: TObject);`

`procedure connAfterConnect(Sender: TObject);`

`procedure FormClose(Sender: TObject; var Action: TCloseAction);`

`procedure sqlContactsAfterScroll(DataSet: TDataSet);`

private

{ Private declarations }

public

{ Public declarations }

end;

![](img/fe651f295b5f960d5463c4fb581d2281_89_0.png)

```pascal
var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.btnConnectClick(Sender: TObject);
begin
  conn.Open;
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  sqlContacts.Close;
  conn.Close;
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnConnect.Enabled := False;
  btnDisconnect.Enabled := True;
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
  btnConnect.Enabled := True;
  btnDisconnect.Enabled := False;
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
  btnDisconnectClick(btnDisconnect);
end;

procedure TfrmMain.btnRetrieveClick(Sender: TObject);
begin
  sqlContacts.Close;
  sqlContacts.ParamByName('CountryName').Value := cbCountry.Text;
  sqlContacts.Open;
end;

procedure TfrmMain.BtnNextClick(Sender: TObject);
begin
  sqlContacts.Next;
end;

procedure TfrmMain.sqlContactsAfterScroll(DataSet: TDataSet);
var
  ListItem: TListItem;
begin
  lvActivities.Items.BeginUpdate;
  try
    lvActivities.Items.Clear;
    while not sqlActivities.EOF do begin
      ListItem := lvActivities.Items.Add;
      ListItem.Caption := DateTimeToStr(sqlActivitiesSCHEDULED.AsDateTime);
      ListItem.SubItems.Add(sqlActivitiesDESCRIPTION.AsString);
      if not sqlActivitiesCOMPLETED.IsNull then
        ListItem.Data := Pointer(1);
      sqlActivities.Next;
    end;
  finally
    lvActivities.Items.EndUpdate;
  end;
end;
```

图 2.4 展示了高级程序的实际运行效果。

## 获取模式信息

前一章介绍了如何获取数据库的基本模式信息（例如表名、索引名和存储过程名）。本节将解释如何使用 `TSQLDataSet` 来获取有关表和列的更详细信息。

要从数据库中获取全面的模式信息，请调用 `TSQLDataSet.SetSchemaInfo`，它指定要获取模式的目标对象以及要返回的模式数据类型。`SetSchemaInfo` 接受三个参数，定义如下：

```pascal
procedure SetSchemaInfo(SchemaType: TSchemaType; SchemaObjectName,
  SchemaPattern: string);
```
