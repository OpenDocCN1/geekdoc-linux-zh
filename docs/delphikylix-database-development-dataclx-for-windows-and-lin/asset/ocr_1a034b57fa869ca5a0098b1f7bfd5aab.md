# **LISTING 4.2 Continued**

```
btnOk: TButton;
btnCancel: TButton;
cblLogScrollEvents: TCheckBox;
cbPromotOnDelete: TCheckBox;

private
procedure SetLogScrollEvents(const Value: Boolean);
function GetLogScrollEvents: Boolean;
function GetPromotOnDelete: Boolean;
procedure SetPromotOnDelete(const Value: Boolean);
{ Private declarations }
public
{ Public declarations }
property LogScrollEvents: Boolean
read GetLogScrollEvents write SetLogScrollEvents;
property PromotOnDelete: Boolean
read GetPromotOnDelete write SetPromotOnDelete;
end;

implementation

{$R *.xfm}

{TfrmOptions}

function TfrmOptions.GetLogScrollEvents: Boolean;
begin
Result := cblLogScrollEvents.Checked;
end;

function TfrmOptions.GetPromotOnDelete: Boolean;
begin
Result := cbPromotOnDelete.Checked;
end;

procedure TfrmOptions.SetLogScrollEvents(const Value: Boolean);
begin
cblLogScrollEvents.Checked := Value;
end;

procedure TfrmOptions.SetPromotOnDelete(const Value: Boolean);
begin
 cbPromotOnDelete.Checked := Value;
end;

end.
```

![](bbox=[0.85, 0.65, 0.98, 0.78])