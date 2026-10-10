# **LISTING 2.3**  Continued

```
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
```