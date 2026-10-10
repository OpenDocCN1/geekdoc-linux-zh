# **LISTING 5.1** Continued

```
```
if I >= 0 then
    Exit;
end;

if Style in [csDropDown, csSimple] then
    Text := Value;
end;

procedure TETHDBComboBox.DataChange(Sender: TObject);
begin
    if not (Style = csSimple) and DroppedDown then
        Exit;

    if FDataLink.Field <> nil then
        SetComboText(FDataLink.Field.Text)
    else if csDesigning in ComponentState then
        SetComboText(Name)
    else
        SetComboText('');
end;

procedure TETHDBComboBox.UpdateData(Sender: TObject);
begin
    FDataLink.Field.Text := GetComboText;
end;

end.
```
```

Listing 5.1 contains some code that you might not be familiar with, so I’ll examine some of the individual routines in more detail.

*Create* and *Destroy* simply create and free the new *FValues* property, and then pass control onto TDBComboBox’s constructor and destructor.

*CreateWnd* sends a CM_GETDATALINK message to the component to obtain a reference to the component’s internal FDataLink field. Because TETHDBComboBox derives from TDBComboBox, we’re actually retrieving TDBComboBox’s FDataLink. TDBComboBox.FDataLink is private and TDBComboBox doesn’t provide a property to access the value, so there’s no way to directly get a hold of the data link. Fortunately, TDBComboBox supports the CM_GETDATALINK message, which accomplishes the same thing.

![](bbox=[0.92, 0.82, 0.98, 0.88])