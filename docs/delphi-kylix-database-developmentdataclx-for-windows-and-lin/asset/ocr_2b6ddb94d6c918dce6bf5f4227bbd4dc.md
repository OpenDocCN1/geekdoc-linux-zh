# **LISTING 1.6**  Continued

```
    procedure btnDisconnectClick(Sender: TObject); 
    procedure btnExecSQLClick(Sender: TObject); 
    procedure connAfterConnect(Sender: TObject); 
    procedure connAfterDisconnect(Sender: TObject); 
    procedure FormClose(Sender: TObject; var Action: TCloseAction); 
    procedure cbUseCallBackClick(Sender: TObject); 
    procedure monitorTrace(Sender: TObject; CBIInfo: pSQLTRACEDesc;
      var LogTrace: Boolean);
  
  private
    { Private declarations }
  public
    { Public declarations }
  end;
  
  var
      frmMain: TfrmMain;
  
  implementation
  
  {$R *.xfm}
  
  function MySQLCallBack(CallType: TRACECat; CBIInfo: Pointer): CBRTtype; stdcall;
  var
      CBI: pSQLTRACEDesc;
  begin
    Result := cbruSEDEF;
    if CBIInfo <> nil then begin
      CBI := pSQLTRACEDesc(CBIInfo);
      frmMain.lbTrace.Items.Add('CallBack: ' + CBI.ps2Trace);
    end;
  end;
  
  procedure TfrmMain.btnConnectClick(Sender: TObject);
  begin
    conn.Open;
    
    cbUseCallBackClick(cbUseCallBack);
  end;
  
  procedure TfrmMain.btnDisconnectClick(Sender: TObject);
  begin
    conn.Close;
  end;
```