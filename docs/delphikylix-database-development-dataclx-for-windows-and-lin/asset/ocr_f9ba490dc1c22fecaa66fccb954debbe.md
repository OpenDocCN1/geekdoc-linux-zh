# LISTING 7.1 Continued

```
procedure TfrmMain.Log(const s: string);\nbegin\n\tIoEvents.Items.Add(s);\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterApplyUpdates(Sender: TObject;\n\tvar OwnerData: OleVariant);\nbegin\n\tLog('TDataSetProvider.AfterApplyUpdates');\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterExecute(Sender: TObject;\n\tvar OwnerData: OleVariant);\nbegin\n\tLog('TDataSetProvider.AfterExecute');\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterGetParams(Sender: TObject;\n\tvar OwnerData: OleVariant);\nbegin\n\tLog('TDataSetProvider.AfterGetParams');\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterGetRecords(Sender: TObject;\n\tvar OwnerData: OleVariant);\nbegin\n\tLog('TDataSetProvider.AfterGetRecords');\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterRowRequest(Sender: TObject;\n\tvar OwnerData: OleVariant);\nbegin\n\tLog('TDataSetProvider.AfterRowRequest');\nend;
```

```
procedure TfrmMain.TDataSetProvider1AfterUpdateRecord(Sender: TObject;\n\tSourceDS: TDataSet; DeltaDS: TCustomClientDataSet;\n\tUpdateKind: TUpdateKind);\nbegin\n\tLog('TDataSetProvider.AfterUpdateRecord');\nend;
```

```
procedure TfrmMain.TDataSetProvider1BeforeApplyUpdates(Sender: TObject;\n\tvar OwnerData: OleVariant);
```

![](bbox=[0.85, 0.24, 0.95, 0.4])