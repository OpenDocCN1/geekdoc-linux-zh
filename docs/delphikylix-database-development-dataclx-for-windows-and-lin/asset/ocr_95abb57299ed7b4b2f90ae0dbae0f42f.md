# LISTING 6.1  Continued

```
var
    TfrmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    CliendDataSet1.LoadFromFile ('C:\Employee.CDS');

    RetrieveOptions;
end;

// Options set/get methods

procedure TfrmMain.RetrieveOptions;
begin
    cbEditing.Checked := (dgEditing in grid.Options);
    cbAlwaysShowEditor.Checked := (dgAlwaysShowEditor in grid.Options);
    cbTitles.Checked := (dgTitles in grid.Options);
    cbIndicator.Checked := (dgIndicator in grid.Options);
    cbColumnResize.Checked := (dgColumnResize in grid.Options);
    cbColLines.Checked := (dgColLines in grid.Options);
    cbRowLines.Checked := (dgRowLines in grid.Options);
    cbTabs.Checked := (dgTabs in grid.Options);
    cbRowSelect.Checked := (dgRowSelect in grid.Options);
    cbAlwaysShowSelection.Checked := (dgAlwaysShowSelection in grid.Options);
    cbConfirmDelete.Checked := (dgConfirmDelete in grid.Options);
    cbCancelOnExit.Checked := (dgCancelOnExit in grid.Options);
    cbMultiSelect.Checked := (dgMultiSelect in grid.Options);
end;

procedure TfrmMain.UpdateOption (Option: TDBGridOption; Active: Boolean);
begin
    if Active then
        grid.Options := grid.Options + [Option]
    else
        grid.Options := grid.Options - [Option];

    RetrieveOptions;
end;

procedure TfrmMain.cbEditingClick (Sender: TObject);
```