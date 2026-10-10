
# LISTING 4.8 Continued

```delphi
type
TfrmChangeLog = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    ClientDataSet1: TClientDataSet;
    DataSource1: TDataSource;
    DBGId1: TDBGid;
    btnClose: TButton;
    Label1: TLabel;
    procedure ClientDataSet1AfterScroll(DataSet: TDataSet);
private
    { Private declarations }
public
    { Public declarations }
    constructor Create(AOwner: TComponent;
        ADataSet: TCustomClientDataSet); reintroduce;
end;

implementation

{$R *.xfm}

{ TfrmChangeLog }

constructor TfrmChangeLog.Create(AOwner: TComponent;
    ADataSet: TCustomClientDataSet);
begin
    inherited Create(AOwner);

    ClientDataSet1.Data := ADataSet.Delta;
end;

procedure TfrmChangeLog.ClientDataSet1AfterScroll(DataSet: TDataSet);
begin
    case ClientDataSet1.UpdateDataSet of
        usUnmodified: Label1.Caption := 'Unmodified';
        usModified: Label1.Caption := 'Modified';
        usInserted: Label1.Caption := 'Inserted';
        usDeleted: Label1.Caption := 'Deleted';
    end;
end;

end.
```

Figure 4.6 shows the ChangeLog application at runtime as it views the change log for the EMPLOYEE.CDS dataset.

![](img/fe651f295b5f960d5463c4fb581d2281_197_0.png)

![](img/fe651f295b5f960d5463c4fb581d2281_198_0.png)

![](img/fe651f295b5f960d5463c4fb581d2281_198_1.png)

# Figure 4.6

*The ChangeLog application shows how modifications to a dataset are efficiently stored.*

Note the four lines in the change log. The first line shows the data for a newly added employee. The second line shows the data for a deleted employee. The third and fourth lines show modifications to an existing employee. The third line contains the employee data before any modifications were made, but the fourth line contains data for only those fields that were modified.

# Cloning Data from Another Client Dataset

Client datasets have the unique capability to clone data from another client dataset. When you clone a dataset, there is only one physical copy of the data, but there are two (or more) different datasets accessing the same copy of that data. Changes to one dataset immediately affect the other dataset's view of the data.

Why would you want to do this? I have run into several situations in my projects where cloning provides an elegant solution to an otherwise sticky situation. The following list outlines a few of the benefits:

- You can traverse a clone of a dataset without disturbing the original dataset’s current record pointer.
- When viewing a dataset in a grid, you can insert a new record in a dialog using data-aware controls that are connected to the clone (without temporarily opening a new, empty line in the grid).
- You can apply ranges or filters on the clone without affecting the display of the original dataset.

To clone a dataset, create a second client dataset, and then call the second dataset's CloneCursor method, like this:

```delphi
var
  cdsClone: TClientDataSet;
begin
  cdsClone := TClientDataSet.Create(nil);
  try
    cdsClone.CloneCursor(ClientDataSet1, False, False);

    // Perform some operations on the clone here.
  finally
    cdsClone.Free;
  end;
end;
```

This code snippet creates a clone of ClientDataSet1, performs some operation(s) on the clone, and then frees the clone. Any Insert, Edit, or Delete operations performed on the clone are automatically reflected in ClientDataSet1.

CloneCursor is defined like this:

```delphi
procedure CloneCursor(Source: TCustomClientDataSet; Reset: Boolean;
  KeepSettings: Boolean = False); virtual;
```

Source refers to the client dataset that you want to clone. You can't clone a nonclient dataset, such as a BDE dataset or a dbExpress dataset.

Reset and KeepSettings work hand in hand, and determine how the clone handles the following attributes:

- Filter, Filtered, FilterOptions, OnFilterRecord
- IndexName
- MasterSource, MasterFields
- ReadOnly
- RemoteServer, ProviderName

If Reset and KeepSettings are set to False, all the previous properties are copied from the original dataset to the clone. If Reset is False and KeepSettings is True, the previous properties are not changed for the clone. If Reset is True (regardless of the value of KeepSettings), the previous properties are cleared on the clone. Table 4.5 depicts this relationship.

# TABLE 4.5 Relationship between Reset and KeepSettings

| Reset | KeepSettings | Behavior |
| :--- | :--- | :--- |
| False | False | Properties are copied from the original dataset to the clone. |
| False | True | Properties are not changed for the clone. |
| True | N/A | Properties are cleared on the clone. |

If you want the clone to copy some of the listed properties from the original dataset, but not to copy others, you have to write some code. One way to handle this situation is to set both **Reset** and **KeepSettings** to **False** copying all the properties listed previously from the original dataset to the clone. Then, reset the clone’s properties that were overwritten by the original dataset. Alternately, you could set Reset and KeepSettings to True, and then set the appropriate properties on the clone.

> **NOTE**
>
> After cloning a client dataset, the clone does not contain any persistent fields types. This means that you’ll typically use FieldByName to access fields in the clone. Also, the clone does not inherit any standard calculated fields (internal calculated fields are inherited) from the original dataset, so be careful not to try accessing any calculated fields in the clone.

The following example program shows how to effectively use a cloned dataset in the situations listed at the beginning of this section. Listing 4.9 contains the complete source code for the Clone application.

# LISTING 4.9 Clone—MainForm.pas

```delphi
unit MainForm;

interface
uses
  SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, QGrids, QDBGrids, DB, DBClient, ExtCtrls, QStdCtrls;

type
  TFormMain = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    ClientDataSet1: TClientDataSet;
    DataSource1: TDataSource;
    DBGId1: TDBGid;
    btnUpdate: TButton;
    btnInsert: TButton;
    btnRange: TButton;
    btnInsert2: TButton;
    procedure FormCreate(Sender: TObject);
    procedure FormDestroy(Sender: TObject);
    procedure btnUpdateClick(Sender: TObject);
    procedure btnInsertClick(Sender: TObject);
    procedure btnRangeClick(Sender: TObject);
    procedure btnInsert2Click(Sender: TObject);
  private
    { Private declarations }
    FCloneDS: TClientDataSet;
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation
{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.cds');
  ClientDataSet1.AddIndex('byID', 'ID', [ixPrimary, ixUnique]);
  ClientDataSet1.IndexName := 'byID';
  FCloneDS := TClientDataSet.Create(nil);
  FCloneDS.CloneCursor(ClientDataSet1, False, False);
end;

procedure TfrmMain.FormDestroy(Sender: TObject);
begin
  FCloneDS.Free;
end;

procedure TfrmMain.btnUpdateClick(Sender: TObject);
begin
  Screen.Cursor := crHourglass;
  try
    FCloneDS.First;
    while not FCloneDS.EOF do begin
      FCloneDS.Edit;
      FCloneDS.FieldName('Salary ').AsFloat :=
        FCloneDS.FieldName(' Salary ').AsFloat * 1.10;
      FCloneDS.Post;

      FCloneDS.Next;
    end;
  finally
    Screen.Cursor := crDefault;
  end;
end;

procedure TfrmMain.btnInsertClick(Sender: TObject);
begin
  if FCloneDS.State <> dsBrowse then
    Exit;

  FCloneDS.Append;
  FCloneDS.FieldName('ID').AsInteger := 99999;
  FCloneDS.FieldName('Name').AsString := 'Eric Harmon';
  FCloneDS.FieldName(' Birthday ').AsString := '1/1/1967';
  FCloneDS.FieldName('Salary ').AsFloat := 1.00;
end;

procedure TfrmMain.btnInsert2Click(Sender: TObject);
begin
  if FCloneDS.State <> dsInsert then
    Exit;

  try
    FCloneDS.Post;
    ClientDataSet1.GotoCurrent(FCloneDS);
  except
    FCloneDS.Cancel;
    raise;
  end;
end;

procedure TfrmMain.btnRangeClick(Sender: TObject);
begin
```
