# **LISTING 8.1** Continued

```
{$R "dfm}

{ TfrmMain }

procedure TfrmMain.UMConnect(var Msg: TMessage);
begin
  FConnections := FConnections + Msg.WParam;
  UpdateConnections;
end;

procedure TfrmMain.UpdateConnections;
begin
  if FConnections = 1 then
    lblConnections.Caption := '1 connection'
  else
    lblConnections.Caption := IntToStr(FConnections) + ' connections';
end;

```

The remote data module then calls the main form's Connect and Disconnect methods on creation and destruction, as the following code snippet shows.

```
procedure TMethodsDM.RemoteDataModuleCreate(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, 1, 0); end;

procedure TMethodsDM.RemoteDataModuleDestroy(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, -1, 0);
end;

```

# **Preparing the Application Server for Testing**

When you have finished writing the application server, you should install it onto the server machine and register it for testing. I highly recommend that you test it on your development machine before moving it to another computer for testing, for a couple of very good reasons:

+   * When you first start creating application servers, you may find that you make numerous mistakes. You'll frequently need to modify, recompile, and redeploy the application server. It's a lot easier to do this on your local development machine.
+   * Your application server may be prone to hang up or crash before it is debugged. It's a much better practice to crash your development machine than to crash a production server.