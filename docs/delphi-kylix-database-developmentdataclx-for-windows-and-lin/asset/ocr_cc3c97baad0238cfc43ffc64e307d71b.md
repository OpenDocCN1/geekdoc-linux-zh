# # Optional Parameters

Optional parameters are custom data that pertain to the dataset passed to the client. Optional parameters relate to the dataset as a whole, rather than to individual records. You can use an optional parameter to pass data back to the client, such as the date and time the data was provided, the length of time required to run the query on the server, or any other data.

To pass optional parameters to the client, provide an event handler for TDataSetProvider’s OnGetDataSetProperties event. Within this event handler, use the Properties parameter to set the values to send back to the client. The following code snippet shows how to send both the time required to execute the query and the time the query was executed.

```
procedure TForm1.DataSetProvider1GetDataSetProperties(Sender: TObject;
DataSet: TDataSet; out Properties: OleVariant);
begin
Properties := VarArrayCreate([0, 1], varVariant);
Properties[0] := VarArrayOf(['TimeQueried', Now, True]);
Properties[1] := VarArrayOf(['QueryPerformance', FTimeToQuery, True]);
end;
```

Properties is a variant array of variant arrays. This code snippet creates an array of two variants. Each variant in the array is an array of three values: the name of the optional parameter, the value of the parameter, and a Boolean value that indicates whether the optional parameter should be sent back to the server as part of the delta.

In this example, FTimeToQuery is a private variable that is calculated using the following code:

```
procedure TForm1.SQLDataSet1BeforeOpen(DataSet: TDataSet);
begin
FTimeToQuery := GetTickCount;
end;

procedure TForm1.SQLDataSet1AfterOpen(DataSet: TDataSet);
begin
FTimeToQuery := GetTickCount - FTimeToQuery;
end;
```

SQLDataSet1 is the underlying dataset for the TDataSetProvider.

On the client, you can retrieve these values by using the following code:

```
procedure TForm1.btnGetPropertiesClick(Sender: TObject);
var
QP: Word;
TimeQueried: TDateTime;
begin
QP := ClientDataSet1.GetOptionalParam('QueryPerformance');
TimeQueried := ClientDataSet1.GetOptionalParam('TimeQueried');
```