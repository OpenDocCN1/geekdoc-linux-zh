
For example, given the previous INSERT statement, TSQLConnection changes it to INSERT INTO EMPLOYEE VALUES (?, ?, ?, ?)

The dbExpress driver may replace the question marks with some other construct that is specific to the database server.

# NOTE

> Parameters do not need to have the same name as the underlying column in the table. Notice in the preceding code snippet that I named the parameter EmpNumber instead of EmpNo, and Hired instead of DateHired.

After you create the SQL statement, you need to fill in the value of each parameter before executing. The following code snippet shows how this is done:

```
Params := TParams.Create(nil);
try
// Create the parameters
Params.CreateParam( ftInteger , 'EmpNumber' , ptInput );
Params.CreateParam( ftString , 'Name' , ptInput );
Params.CreateParam( ftSQLDateTime , 'Hired' , ptInput );
Params.CreateParam( ftFloat , 'Salary' , ptInput );

// Assign values to the parameters
Params.ParamByName('EmpNumber').Value := 123;
Params.ParamByName('Name').Value := 'John Doe';
Params.ParamByName('Hired').Value := '5/15/1994';
Params.ParamByName('Salary').Value := 35000;

// Execute the statement
SQLConnection1.Execute('INSERT INTO EMPLOYEE VALUES (:EmpNumber, :Name, '
' :Hired, :Salary)', Params);
finally
Params.Free;
end;
```

You might be wondering why you would ever want to do this rather than simply executing each statement directly. After all, creating the parameters and assigning them takes a lot more effort. In addition, time tests on my development machine show that the second method takes about twice as long as the first.

In cases where I need to repeatedly execute the same statement, I still prefer using a parameterized query for the following reasons:

# 1
## ESTABLISHING AND USING DATABASE CONNECTIONS

- Simplicity. Given a long, complicated SQL statement, it’s often difficult to form the SQL statement manually. Getting the quotes lined up correctly can be prone to errors, considering that you must double up on single quotes in the Pascal language.
- Robustness. Say for the sake of argument that one of the employee names has a quote in it, such as Frank O’Donnell. If you don’t use parameters, the quote looks as if it were the terminating quote on the name. The parameterless SQL statement would look like this:
  INSERT INTO EMPLOYEE VALUES (123, `Frank O'Donnell`, '5/15/1994', 35000)
  In this case, the name appears to be Frank O, and the following character (D) in the statement is in error. You can solve this problem by double quoting the name, like this:
  INSERT INTO EMPLOYEE VALUES (123, `Frank O''Donnell`, '5/15/1994', 35000)
- When using parameters, a true relational database can compile the prepared statement, and then use that compiled version for all subsequent calls to the SQL statement. When repeatedly issuing the same SQL statement, this more than compensates for the additional time required to prepare the SQL statement.

The use of QuotedStr to automatically quote strings helps to alleviate the first two “problems.”

## SQL Statements That Return a Cursor

In the previous two sections, I discussed simple and parameterized SQL statements, but so far, no statements have returned any data from the database server. The SELECT statement is the most commonly used DML statement. So, why am I shying away from it?

It’s because SELECT statements return data, and you need to have a place to put the resulting data. For dbExpress, that place is a TCustomSolDataSet, which I don’t discuss in detail until the next chapter. For now, I’ll just give a quick overview of how to retrieve data from a TSQLConnection.

The Execute method, which I discussed in the previous section, actually takes a third parameter: a pointer to a result set.

```
function Execute(const SQL: string; Params: TParams; ResultSet: Pointer = nil): Integer;
```

If you don’t pass a third parameter to Execute, it defaults to nil, which means that the statement doesn’t return a result set.

> **NOTE**
> If you pass a nil value for the ResultSet and the SQL command actually does return a result set, the result set is simply discarded. No exception is raised, and no error is returned.

The following code snippet shows one way to execute an SQL statement that returns a result set. In the following chapter, you'll see easier ways to do this.

```
SQLDataSet1 := TSQLDataSet.Create(nil);
try
SQLConnection1.Execute('SELECT * FROM EMPLOYEE', nil, SQLDataSet1);

// Do something with SQLDataSet1 here...
finally
SQLDataSet1.Free;
end;
```

The preceding code also shows the correct way to execute a nonparameterized SELECT statement: Simply pass nil for Params.

The following example program, DDLSQL, shows how to create a test table, fill it with data, and destroy the table programmatically. It also demonstrates how to retrieve data from the table using the Execute method. Listing 1.4 shows the complete code for DDLSQL.

## **Listing 1.4 DDLSQL—MainForm.pas**

```
unit MainForm;

interface

uses
SysUtils, Types, Classes, QGraphics, QControls, QForms, QDialogs, QStdCtrls, QExtCtrls, DBXpress, DB, SqlExpr;

type
TfrmMain = class(TForm)
pnClient: TPanel;
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
procedure btnParametersClick(Sender: TObject);
procedure btnDropClick(Sender: TObject);
procedure connAfterConnect(Sender: TObject);
procedure connAfterDisconnect(Sender: TObject);
procedure FormClose(Sender: TObject; var Action: TCloseAction);
private
  { Private declarations }
public
  { Public declarations }
end;

var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.btnConnectClick(Sender: TObject);
begin
  conn.Open;
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  conn.Close;
end;

procedure TfrmMain.btnCreateClick(Sender: TObject);
begin
  conn.ExecuteDirect('CREATE TABLE TESTING (NAME VARCHAR(20) NOT NULL, '
    + 'AGE INTEGER, PRIMARY KEY (NAME))');
  lbOutput.Items.Add('Created TESTING table');
end;

procedure TfrmMain.btnPopulateClick(Sender: TObject);
begin
  conn.ExecuteDirect('INSERT INTO TESTING VALUES ('Eric', 34)');
  conn.ExecuteDirect('INSERT INTO TESTING VALUES ('Tina', 33)');
  lbOutput.Items.Add('Added Eric and Tina to TESTING table');
end;

procedure TfrmMain.btnDeleteClick(Sender: TObject);
begin
  conn.ExecuteDirect('DELETE FROM TESTING WHERE NAME = 'Tina''');

  lbOutput.Items.Add('Deleted Tina from TESTING table');
end;

procedure TfrmMain.btnParametersClick(Sender: TObject);
const
  SQL = 'INSERT INTO TESTING VALUES (:Name, :Age)';
var
  Params: TParams;
begin
  Params := TParams.Create(nil);
  try
    Params.CreateParam(ftString, 'PName', ptInput);
    Params.CreateParam(ftInteger, 'Page', ptInput);

    // Add first name
    Params.ParamByName('PName').AsString := 'Mike';
    Params.ParamByName('Page').AsInteger := 34;
    conn.Execute(SQL, Params);

    lbOutput.Items.Add('Added Mike to TESTING table');
  finally
    Params.Free;
  end;
end;

procedure TfrmMain.btnDropClick(Sender: TObject);
begin
  conn.ExecuteDirect('DROP TABLE TESTING');

  lbOutput.Items.Add('Removed TESTING table');
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnConnect.Enabled := False;
  btnCreate.Enabled := True;
  btnPopulate.Enabled := True;
  btnDelete.Enabled := True;
  btnParameters.Enabled := True;
  btnDrop.Enabled := True;
  btnDisconnect.Enabled := True;

  lbOutput.Items.Add('Connected');
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
    btnConnect.Enabled := True;
    btnCreate.Enabled := False;
    btnPopulate.Enabled := False;
    btnDelete.Enabled := False;
    btnParameters.Enabled := False;
    btnDrop.Enabled := False;
    btnDisconnect.Enabled := False;

    lbOutput.Items.Add('Disconnected');
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
    conn.Close;
end;

end.
```

Figure 1.6 shows the DDLSQL program at runtime.

![](img/fe651f295b5f960d5463c4fb581d2281_48_0.png)

## **FIGURE 1.6**

*DDLSQL after running the gamut of buttons.*
