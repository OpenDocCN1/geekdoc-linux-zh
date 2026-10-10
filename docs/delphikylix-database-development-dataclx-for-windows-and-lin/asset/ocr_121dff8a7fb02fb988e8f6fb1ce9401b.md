The following code snippet shows one way to execute an SQL statement that returns a result set. In the following chapter, you’ll see easier ways to do this.

```
```
SQLDataSet1 := TSQLDataSet.Create(nil);
try
  SQLConnection1.Execute('SELECT * FROM EMPLOYEE', nil, SQLDataSet1);

// Do something with SQLDataSet1 here...
finally
  SQLDataSet1.Free;
end;
```
```

The preceding code also shows the correct way to execute a nonparameterized SELECT statement: Simply pass nil for Params.

The following example program, DDLSQL, shows how to create a test table, fill it with data, and destroy the table programmatically. It also demonstrates how to retrieve data from the table using the Execute method. Listing 1.4 shows the complete code for DDLSQL.

# **LISTING 1.4** DDLSQL—MainForm.pas

```
```
unit MainForm;

interface

uses
  SysUtils, Types, Classes, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, QExtCtrls, DBExpress, DB, SQLExpr;

type
  TfrmMain = class(TForm)
    pnlClient: TPanel;
    conn: TSQLConnection;
    btnCreate: TButton;
    btnPopulate: TButton;
    btnConnect: TButton;
    btnDelete: TButton;
    btnDisconnect: TButton;
    btnParameters: TButton;
    btnDrop: TButton;
    lbOutput: TListBox;
    procedure btnCreateClick(Sender: TObject);
    procedure btnConnectClick(Sender: TObject);
    procedure btnPopulateClick(Sender: TObject);
    procedure btnDisconnectClick(Sender: TObject);
    procedure btnDeleteClick(Sender: TObject);
```
```

![](bbox=[0.88, 0.11, 0.99, 0.29])