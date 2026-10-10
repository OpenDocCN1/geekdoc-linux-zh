# **LISTING 3.1** Continued

```
```pascal
    { Public declarations }
end;

var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  FCDS := TClientDataSet.Create(Self);
  FCDS.FieldDefs.Add('ID', ftInteger, 0, True);
  FCDS.FieldDefs.Add('Name', ftString, 20, True);
  FCDS.FieldDefs.Add('Birthday', ftDateTime, 0, True);
  FCDS.FieldDefs.Add('Salary', ftCurrency, 0, True);
  FCDS.CreateDataSet;
  DataSource1.DataSet := FCDS;
end;

procedure TfrmMain.Populate1Execute(Sender: TObject);
const
  FirstNames: array[0 .. 19] of string = ('John', 'Sarah', 'Fred', 'Beth',
                                         'Eric', 'Tina', 'Thomas', 'Judy', 'Robert', 'Angela', 'Tim', 'Traci',
                                         'David', 'Paula', 'Bruce', 'Jessica', 'Richard', 'Carla', 'James',
                                         'Mary');
  LastNames: array[0 .. 11] of string = ('Parker', 'Johnson', 'Jones',
                                         'Thompson', 'Smith', 'Baker', 'Wallace', 'Harper', 'Parson', 'Edwards',
                                         'Mandel', 'Stone');
var
  Index: Integer;
  t1, t2: DWord;
begin
  RandSeed := 0;

  t1 := GetTickCount;
  FCDS.DisableControls;
  try
    FCDS.EmptyDataSet;
    for Index := 1 to MAX_RECS do begin
      FCDS.Append;
      FCDS.FieldByName('ID').AsInteger := Index;
      FCDS.FieldByName('Name').AsString := FirstNames[Random(20)] + ' ' +
```
```