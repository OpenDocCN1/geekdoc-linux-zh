# **LISTING 1.5**	Continued

```
conn.StartTransaction(TransDesc1);
conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = 'Trans 1' WHERE ID = 3');

TransDesc2.TransactionID := 2;
TransDesc2.IsolationLevel := xiREADCOMMITTED;
conn.StartTransaction(TransDesc2);
conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = 'Trans 2' WHERE ID = 2');
conn.Rollback(TransDesc2);
lbOutput.Items.Add('Second transaction rolled back');

conn.Commit(TransDesc1);
lbOutput.Items.Add('First transaction committed');
end;

procedure TfrmMain.btnOverlappingClick(Sender: TObject);
var
  TransDesc3: TTransactionDesc;
  TransDesc4: TTransactionDesc;
begin
TransDesc3.TransactionID := 3;
TransDesc3.IsolationLevel := xiREADCOMMITTED;

conn.StartTransaction(TransDesc3);
conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = 'Trans 3' WHERE ID = 3');

TransDesc4.TransactionID := 4;
TransDesc4.IsolationLevel := xiREADCOMMITTED;
conn.StartTransaction(TransDesc4);
conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = 'Trans 4' WHERE ID = 2');

conn.Rollback(TransDesc3);
lbOutput.Items.Add('Transaction 3 rolled back');

conn.Commit(TransDesc4);
lbOutput.Items.Add('Transaction 4 committed');
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnConnect.Enabled := False;
  btnDisconnect.Enabled := True;
  btnCommit.Enabled := True;
  btnRollback.Enabled := True;
  btnMultiLevel.Enabled := True;
```

![](bbox=[0.85, 0.14, 0.98, 0.28])