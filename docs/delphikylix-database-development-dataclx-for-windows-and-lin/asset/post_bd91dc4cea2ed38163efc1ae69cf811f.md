
## **LISTING 6.1** *Continued*

```pascal
begin
  UpdateOption(dgEditing, cbEditing.Checked);
end;

procedure TfrmMain.cbAlwaysShowEditorClick(Sender: TObject);
begin
  UpdateOption(dgAlwaysShowEditor, cbAlwaysShowEditor.Checked);
end;

procedure TfrmMain.cbTitlesClick(Sender: TObject);
begin
  UpdateOption(dgTitles, cbTitles.Checked);
end;

procedure TfrmMain.cbIndicatorClick(Sender: TObject);
begin
  UpdateOption(dgIndicator, cbIndicator.Checked);
end;

procedure TfrmMain.cbColumnResizeClick(Sender: TObject);
begin
  UpdateOption(dgColumnResize, cbColumnResize.Checked);
end;

procedure TfrmMain.cbColLinesClick(Sender: TObject);
begin
  UpdateOption(dgColLines, cbColLines.Checked);
end;

procedure TfrmMain.cbRowLinesClick(Sender: TObject);
begin
  UpdateOption(dgRowLines, cbRowLines.Checked);
end;

procedure TfrmMain.cbTabsClick(Sender: TObject);
begin
  UpdateOption(dgTabs, cbTabs.Checked);
end;

procedure TfrmMain.cbRowSelectClick(Sender: TObject);
begin
  UpdateOption(dgRowSelect, cbRowSelect.Checked);
end;

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

```pascal
procedure TfrmMain.gridCellClick(Column: TColumn);
begin
  lbEvents.Items.Add('OnCellClick - Col ' + IntToStr(grid.SelectedIndex) +
    ', Field ' + grid.SelectedField.FieldName + '');
end;

procedure TfrmMain.gridColumnMoved(Sender: TObject; FromIndex,
  ToIndex: Integer);
begin
  lbEvents.Items.Add('Column moved from ' + IntToStr(FromIndex) +
    ' to ' + IntToStr(ToIndex));
end;

// Command buttons

procedure TfrmMain.btnClearEventLogClick(Sender: TObject);
begin
  lbEvents.Items.Clear;
end;

procedure TfrmMain.btnShowSelectionsClick(Sender: TObject);
var
  Index: Integer;
  s: string;
begin
  if not (dgMultiSelect in grid.Options) then
    raise Exception.Create('dgMultiSelect not set');

  if grid.SelectedRows.Count = 0 then
    raise Exception.Create('No rows selected');

  for Index := 0 to grid.SelectedRows.Count - 1 do
  begin
    ClientDataSet1.Bookmark := grid.SelectedRows[Index];
    if s <> '' then
      s := s + #13;
    s := s + Format('%d: %s', [ClientDataSet1.FieldByName('ID').AsInteger,
      ClientDataSet1.FieldByName('Name').AsString]);
  end;

  ShowMessage(s);
end;
end.
```

Figure 6.3 shows the Options application at runtime.

![](img/52a35759a0f10dade27a840504be5d82_265_0.png)

### FIGURE 6.3
The Options application lets you experiment with the TDBGrid component's options.

## Custom Drawing

As you can see from Figure 6.2, the grid's default appearance is pleasing to look at, but not especially eye-catching. Using custom drawing, we can spruce up the look of the grid considerably.

To implement custom drawing in your grid, you need to handle the grid's OnDrawColumnCell event. You might notice that the grid contains a similarly named event, OnDrawDataCell. OnDrawDataCell is an obsolete event that is included for backward compatibility with early versions of Delphi. You should not use it in any new programming efforts.

A newly created handler for the OnDrawColumnCell event looks like this:

```pascal
procedure TForm1.DBGrid1DrawColumnCell(Sender: TDBGrid; const Rect: TRect;
  DataCol: Integer; Column: TColumn; State: TGridDrawState);
begin
end;
```

As with all grid events, the Sender parameter references the grid object. Rect refers to the bounding rectangle of the cell that is about to be drawn. DataCol is a zero-based index into the absolute position of the column that is about to be drawn. State is a set containing one or more of the values listed in Table 6.6.

**TABLE 6.6 TGridDrawState Values**

| Value | Description |
| :--- | :--- |
| gdSelected | The cell is selected. |
| gdFocused | The cell has the focus. |
| gdFixed | The cell is fixed (that is, it's the indicator cell). |

The difference between gdSelected and gdFocused can get confusing (especially because these values change meaning slightly as the Options property changes), so I'll clarify it here. When dgRowSelect is not set (the default), only the current cell has the gdSelected value set. If the grid currently has focus, the current cell has gdFocused set in addition to having the gdSelected value set.

When dgRowSelect is set, all cells in the current row have the gdSelected value set. In addition, if the grid has focus, the first cell in the row (excluding the indicator) has gdFocused set. You probably want to ignore the gdFocused value when using dgRowSelect, as it has no useful meaning.

## The DefaultDrawing Property

The grid's DefaultDrawing property determines how drawing is performed in the grid. When this property is True (the default), VCL/CLX draws each cell in the grid as usual, and then passes control to the OnDrawColumnCell handler that you set up. OnDrawColumnCell is called for every cell in the grid, so you want to make sure that whatever code you write in that event handler executes quickly.

When DefaultDrawing is False, Delphi paints the cell with the appropriate background color, and sets the grid's Brush and Font properties in readiness to draw the cell. Then, it calls OnDrawColumnCell so that you can draw the contents of the cell yourself.

In practice, you will often find that when you implement custom drawing, Delphi's default drawing code does about 90% of what you need. You might simply want to change the color of selected cells, draw an image in a given column, or perhaps draw negative values in red.

It might seem that the DefaultDrawing property goes to extremes. On the one hand, if it is True, the cell is drawn using its default settings, and then you turn around and draw over the top of it. On the other hand, if it is False, you need to draw every single cell manually—even those that you don't need any special drawing for.

Fortunately, this isn't the case. The solution is to set DefaultDrawing to False, and then inside the OnDrawColumnCell event handler, call the grid's DefaultDrawColumnCell, like this:

```pascal
procedure TForm1.DBGrid1DrawColumnCell(Sender: TDBGrid; const Rect: TRect;
  DataCol: Integer; Column: TColumn; State: TGridDrawState);
begin
  if Column.FieldName = 'Salary' then
  begin
    if Column.Field.AsFloat > 50000.0 then
    begin
      DBGrid1.Canvas.Brush.Color := clYellow;

      if gfFocused in State then
        DBGrid1.Canvas.Font.Color := clRed;
    end;
  end;

  DBGrid1.DefaultDrawColumnCell(Rect, DataCol, Column, State);
end;
```

This code snippet only changes the way the Salary column is drawn. If the salary is greater than $50,000, the background of the cell is drawn in yellow. If the cell is focused, the salary is drawn in red.

For all other cells, and for salaries that are less than or equal to $50,000, the cell is drawn normally. The call to DefaultDrawColumnCell takes care of drawing the cell after the appropriate changes (if any) are made to the brush and font colors.

The way that Delphi’s internal VCL/CLX painting code works, all you need to do in this handler is to set the canvas’ Brush and Font properties so that they reflect the color and font that you want to use when painting the cell. The call to DefaultDrawColumnCell then uses the settings that you specified when drawing the cell contents.

> **NOTE**
> Notice, in the preceding code snippet, that I checked the FieldName property of the column to see if the code is drawing the Salary column. You might be tempted to use the DataCol parameter to check for this. However, DataCol is the zero-based absolute index of the cell being drawn. If the user reorders the columns at runtime, this value changes.

The following sample program demonstrates several ways to custom draw grid cells. Listing 6.2 contains the complete source code for the CustomDraw application.

## LISTING 6.2 CustomDraw—MainForm.pas

```pascal
unit MainForm;

interface
```
