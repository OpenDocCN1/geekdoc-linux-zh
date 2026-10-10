```
LISTING 9.5  Continued

{$R *.dfm}

// Form event handlers

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  DM.SocketConnection1.AfterConnect := DoConnectDisconnect;
  DM.SocketConnection1.AfterDisconnect := DoConnectDisconnect;
end;

procedure TfrmMain.FormCloseQuery(Sender: TObject; var CanClose: Boolean);
begin
  if DM.cdsContacts.State <> dsBrowse then begin
    case MessageDlg(SChangesPending, mtWarning, [mbYes, mbNo, mbCancel], 0) of
      mrYes:    DM.cdsContacts.Post;
      mrNo:     DM.cdsContacts.Cancel;
      mrCancel: CanClose := False;
    end;
  end;
end;

procedure TfrmMain.DoConnectDisconnect(Sender: TObject);
begin
  // Repaint the status bar to reflect the new connection status
  StatusBar1.Invalidate;
end;

// Status bar event handlers

procedure TfrmMain.StatusBar1DrawPanel(StatusBar: TStatusBar;
  Panel: TStatusPanel; const Rect: TRect);
begin
  if Panel.Index = 0 then begin
    if DM.SocketConnection1.Connected then begin
      StatusBar.Canvas.Font.Color := clGreen;
      StatusBar.Canvas.TextRect(Rect, Rect.Left + 2, Rect.Top + 1, 0
      StatusBar.Canvas.Font.Color := clRed;
      StatusBar.Canvas.TextRect(Rect, Rect.Left + 2, Rect.Top + 1, 0
    end;
  end;
end;
```