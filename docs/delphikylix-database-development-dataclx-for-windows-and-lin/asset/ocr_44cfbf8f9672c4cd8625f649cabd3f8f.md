# **LISTING 3.6** Continued

```
begin
Result := StrToFloat(ecLower.Text);
end;

procedure TfrmRange.btnOkClick(Sender: TObject);
var
LowValue: Double;
HighValue: Double;
begin
try
LowValue := StrToFloat(ecLower.Text);
HighValue := StrToFloat(ecUpper.Text);

if LowValue > HighValue then begin
ModalResult := mrNone;
ShowMessage('The upper salary must be >= the lower salary');
end;
except
ModalResult := mrNone;
ShowMessage('Both values must be a valid number');
end;
end.
```

Figure 3.8 shows the RangeFilter application in operation.

![](bbox=[0.28, 0.65, 0.6, 0.83])

**FIGURE 3.8**
RangeFilter applies both ranges and filters to a dataset.