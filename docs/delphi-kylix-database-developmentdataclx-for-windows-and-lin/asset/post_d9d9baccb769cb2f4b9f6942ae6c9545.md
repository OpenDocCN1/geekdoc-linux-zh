
```pascal
ShowMessage('The query took ' + IntToStr(OP) + 'ms and was executed on ' +
DateToStr(TimeQueried) + ' at ' + TimeToStr(TimeQueried));
end;
```

## Master/Detail Relationships

Back in Chapter 2, “dbExpress Datasets,” you learned how to create a master/detail relationship between two or more dbExpress datasets.

Later, in Chapter 4, you learned how to create nested TClientDataSets to create a master/detail relationship at the TClientDataSet level.

Using providers, you will establish the master/detail relationship on the server-side data module, using TSQLDataSet components. You will then connect a TDataSetProvider component to the master dataset only. Drop a single TClientDataSet component on the client-side data module and connect it to the master dataset’s provider. This will automatically create a nested dataset on the client side.

It is good practice to create one data module for the dbExpress components and dataset providers and another data module for the client datasets. I refer to these data modules as server-side data modules and client-side data modules. This is explained more fully in the section titled, “Connecting to a Local Database,” later in this chapter.

The MasterDetail sample application, included in the downloads for this book, illustrates this technique. I haven’t included a listing here, because almost no code is required—everything is done at design time.

Figure 7.4 shows the main form of the MasterDetail application at design time. For simplicity, I put the database components directly on the main form instead of creating separate data modules for the server and client.

![](img/fe651f295b5f960d5463c4fb581d2281_313_0.png)

**FIGURE 7.4**
Components needed for a master/detail relationship.

## Providing and Resolving Data from Stored Procedures and Joins

So far, the examples in this chapter focused on providing data from a single table using a simple select statement, such as `SELECT * FROM CONTACTS`. Frequently, data is provided from a stored procedure on the server or is generated as a join between multiple tables, as the following two snippets show:

```sql
// Stored procedure
SELECT * FROM CONTACTSBYSTATE('FL');

// Join
SELECT CONTACTS.FIRST, CONTACTS.LAST, TODOS.SCHEDULED, TODOS.DESCRIPTION
FROM CONTACTS, TODOS
WHERE CONTACTS.ID = TODOS.CONTACTID;
```

### Providing and Resolving Data from a Stored Procedure

In the preceding example, the stored procedure returns all contacts for a given state—in this case, Florida. **TDataSetProvider** attempts to intelligently determine what database table to update when resolving data, but in this case, **CONTACTSBYSTATE** is a stored procedure and not a table.

**TDataSetProvider** needs a little help to know what table should be updated with any data changes. To do this, you need to provide an event handler for the provider's **OnGetTableName** event. In the event handler, specify the name of the table to be updated, like this:

```pascal
procedure TForm1.DataSetProvider1GetTableName(Sender: TObject;
          DataSet: TDataSet; var TableName: String);
begin
    TableName := 'CONTACTS';
end;
```

In addition, you need to set the **ProviderFlags** to [] for all fields in the stored procedure dataset that are not updated.

### Providing and Resolving Data from a Join

By definition, a join returns data from more than one table. In many cases, the user will be able to update data from only one of the tables. For example, in the select statement shown previously, data is retrieved from the **CONTACTS** table and the **TODOS** table. On the client side, the user may add a new **TODO** to the list, but the only table that is affected is the **TODOS** table. (Presumably, if the user wants to add a new contact, he would not do so on the same screen that he's viewing todos on).

If this is the case, you can specify the **TODOS** table name in the OnGetTableName event handler, as explained earlier.

Sometimes, though, the user will be able to update multiple tables at once. To handle this situation, you will need to write some code. Again, we turn to TDataSetProvider’s **BeforeUpdateRecord** event handler. The trick is to apply the necessary updates to the individual tables themselves inside the event handler.

The following code snippet shows the general outline that you will follow to apply updates to multiple tables at once. It is not compilable code.

```pascal
procedure TForm1.SQLClientDataSet1BeforeUpdateRecord(Sender: TObject;  
    SourceDS: TDataSet; DeltaDS: TCustomClientDataSet; UpdateKind: TUpdateKind;
    var Applied Boolean);
var
    SQL: string;
    Connection: TSQLConnection;
begin
    // Obtain a pointer to the connection from the source dataset
    Connection := (SourceDS as TCustomSQLDataSet).SQLConnection;
    
    case UpdateKind of
    ukInsert: begin
        // Insert into the first table
        SQL := // SQL INSERT STATEMENT FOR TABLE 1
        Connection.Execute(SQL, nil, nil);
        
        // Insert into the second table
        SQL := // SQL INSERT STATEMENT FOR TABLE 2
        Connection.Execute(SQL, nil, nil);
    end;
    
    ukModify: begin
        // Update the first table
        SQL := // SQL UPDATE STATEMENT FOR TABLE 1
        Connection.Execute(SQL, nil, nil);
        
        // Update the second table
        SQL := // SQL UPDATE STATEMENT FOR TABLE 2
        Connection.Execute(SQL, nil, nil);
    end;
    
    ukDelete: begin
        // Delete from the first table
        SQL := // SQL DELETE STATEMENT FOR TABLE 1
        Connection.Execute(SQL, nil, nil);
        
        // Delete from the second table
        SQL := // SQL DELETE STATEMENT FOR TABLE 2
        Connection.Execute(SQL, nil, nil);
    end;
end;

Applied := True;
end;
```

![](img/fe651f295b5f960d5463c4fb581d2281_315_0.png)

As you can see from the preceding listing, the general idea is to determine what kind of operation is taking place (Insert, Modify, or Delete) and then call the TSqlConnection component to execute the appropriate SQL statements directly. At the end of the method, set **Applied** to True so the provider knows that you’ve already handled the update manually.

This process works equally well for three-, four-, or *n*-table joins.

The following example shows how you can resolve updates in a simple two-way join.

**Listing 7.2** contains the source code for the main form of the Joins application.

### Listing 7.2 Joins—MainForm.pas

```pascal
unit MainForm;
interface
uses
  SysUtils, Types, Classes, Graphics, Controls, Forms, Dialogs,
  StdCtrls, DBXpress, FMTBcd, DB, SQLExpr, Grids, QDBGrids, Provider,
  DBClient, Variants;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    DBGrid1: TDBGrid;
    SQConnection1: TSqlConnection;
    SQLDataSet1: TSQLDataSet;
    DataSetProvider1: TDataSetProvider;
    ClientDataSet1: TClientDataSet;
    sqLID: TSQLDataSet;
    btnApplyUpdates: TButton;
    procedure FormCreate(Sender: TObject);
    procedure DataSetProvider1BeforeUpdateRecord(Sender: TObject;
      SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
      UpdateKind: TUpdateKind; var Applied: Boolean);
    procedure btnApplyUpdatesClick(Sender: TObject);
    procedure ClientDataSet1NewRecord(DataSet: TDataSet);
```

**LISTING 7.2 Continued**

```pascal
private
    { Private declarations }
    FNextID: Integer;
    function GetNextID: Integer;
public
    { Public declarations }
end;

var
    TfrmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    ClientDataSet1.Open;
end;

procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
begin
    Dec(FNextID);
    DataSet.FieldByName('CONTACTID').AsInteger := FNextID;
end;

function TfrmMain.GetNextID: Integer;
begin
    sqlID.ExecSQL;
    Result := sqlID.ParamByName('AValue').AsInteger;
end;

procedure TfrmMain.DataSetProvider1BeforeUpdateRecord(Sender: TObject;
    SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
    UpdateKind: TUpdateKind; var Applied: Boolean);
var
    SQL: string;
    Connection: TSQLConnection;
    ID: Integer;
begin
    // Obtain a pointer to the connection from the source dataset
    Connection := (SourceDS as TCustomSQLDataSet).SQLConnection;

case UpdateKind of
    ukInsert: begin
        ID := GetNextID;
```

![](img/fe651f295b5f960d5463c4fb581d2281_317_0.png)
