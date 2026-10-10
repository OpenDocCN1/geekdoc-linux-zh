# **LISTING 6.1** Continued

```
procedure TfrmMain.cbAlwaysShowSelectionClick(Sender: TObject);
begin
    UpdateOption(dgAlwaysShowSelection, cbAlwaysShowSelection.Checked);
end;

procedure TfrmMain.cbConfirmDeleteClick(Sender: TObject);
begin
    UpdateOption(dgConfirmDelete, cbConfirmDelete.Checked);
end;

procedure TfrmMain.cbCancelOnExitClick(Sender: TObject);
begin
    UpdateOption(dgCancelOnExit, cbCancelOnExit.Checked);
end;

procedure TfrmMain.cbMultiSelectClick(Sender: TObject);
begin
    UpdateOption(dgMultiSelect, cbMultiSelect.Checked);
end;

// Grid event handlers

procedure TfrmMain.gridColExit(Sender: TObject);
begin
    lbEvents.Items.Add('OnColExit - Col ' + IntToStr(grid.SelectedIndex) +
         ', Field ' + grid.SelectedField.FieldName + '');

// By calling Abort here, you can prevent focus from leaving this column
// Abort;
end;

procedure TfrmMain.gridColEnter(Sender: TObject);
begin
    lbEvents.Items.Add('OnColEnter - Col ' + IntToStr(grid.SelectedIndex) +
         ', Field ' + grid.SelectedField.FieldName + '');
end;

procedure TfrmMain.gridEditButtonClick(Sender: TObject);
begin
    lbEvents.Items.Add('OnEditButtonClick - Col ' +
         IntToStr(grid.SelectedIndex) + ', Field ' +
         grid.SelectedField.FieldName + '');
end;
```