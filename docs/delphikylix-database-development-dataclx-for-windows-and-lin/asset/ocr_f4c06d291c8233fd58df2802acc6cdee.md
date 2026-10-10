SqLDataset1.Fields[0].AsString);

You can also use the `FieldCount` property to determine the number of fields in the result set and to loop through them, as the following code illustrates:

```
```pascal
for Index := 0 to SqLDataset1.FieldCount - 1 do
    // Do something with SqLDataset1.Fields[Index]
```
```

# ## Navigating a Dataset

Because dbExpress datasets are unidirectional, there isn't a lot of navigation that is supported. The only two operations that you can perform are moving to the beginning of the dataset, and moving to the next record in the result set. These operations are illustrated in the following code snippet:

```
```pascal
while not SqLDataset1.EOF do begin
    for Index := 0 to SqLDataset1.FieldCount - 1 do begin
        // Do something with SqLDatasets.Fields[Index]
        SqLDataset1.Next;
    end;
end;
```
```

The following code listing is an example of all the concepts discussed so far in this chapter. It illustrates how to use the TSQLTable, TSQLQuery, TSQLStoredProc, and TSQLDataSet components to retrieve data from the ConMan database. The code listing also shows how to use these components to loop through the results, and to do something with the data. (In this case, it simply loads a TListView component with some of the field contents.)

Listing 2.1 shows the complete source code for the main form of the application.

```
**LISTING 2.1    Basic—MainForm.pas**

```pascal
unit MainForm;

interface
uses
    SysUtils, Variants, Classes, QGraphics, QControls, QForms,
    QDialogs, DBXpress, DB, SqlExpr, QStdCtrls, QComCtrls, QExtCtrls, FMTBcd,
    QDBCtrls;

type
    TfrmMain = class(TForm)
        pnlClient: TPanel;
        pnlBottom: TPanel;
        btnConnect: TButton;
```
```