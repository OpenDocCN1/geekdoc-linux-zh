# LISTING 8.3 Continued

```
var
    frmMain: TfrmMain;
implementation
uses
DataModule;
{$R *.dfm}
procedure TfrmMain.FormCreate(Sender: TObject);
begin
DM.cdsContacts.Open;
end;
procedure TfrmMain.btnGetServerTimeClick(Sender: TObject);
var
D: TDateTime;
begin
D:= DM.SocketConnection1.AppServer.GetServerTime;
ShowMessage(TimeToStr(D));
end;
procedure TfrmMain.btnTestCallbacksClick(Sender: TObject);
var
typeLib: ITypeLib;
begin
OleCheck(LoadRegTypeLib (LIBID_MethodsServer, 1,0,0, typeLib));
FTest : = TTest. Create(typeLib, ITestCallback);
DM.SocketConnection1.AppServer.SetCallback (FTest as IDispatch);
DM.SocketConnection1.AppServer.TestCallbacks;
end;
procedure TTest.Test;
begin
ShowMessage('In callback');
end;
end.
```