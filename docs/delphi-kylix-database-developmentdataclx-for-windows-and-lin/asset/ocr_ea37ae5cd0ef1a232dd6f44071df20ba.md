# **LISTING 4.2** Continued

```
btnOk: TButton;
btnCancel: TButton;
cbLogScrollEvents: TCheckBox;
cbPromptOnDelete: TCheckBox;

private
procedure SetLogScrollEvents(const Value: Boolean);
function GetLogScrollEvents: Boolean;
function GetPromptOnDelete: Boolean;
procedure SetPromptOnDelete(const Value: Boolean);
{ Private declarations }

public
{ Public declarations }
property LogScrollEvents: Boolean
read GetLogScrollEvents write SetLogScrollEvents;
property PromptOnDelete: Boolean
read GetPromptOnDelete write SetPromptOnDelete;

end;

implementation

{$R *.xfm}

{ TfrmOptions }

function TfrmOptions.GetLogScrollEvents: Boolean;
begin
Result := cbLogScrollEvents.Checked;
end;

function TfrmOptions.GetPromptOnDelete: Boolean;
begin
Result := cbPromptOnDelete.Checked;
end;

procedure TfrmOptions.SetLogScrollEvents(const Value: Boolean);
begin
cbLogScrollEvents.Checked := Value;
end;

procedure TfrmOptions.SetPromptOnDelete(const Value: Boolean);
begin
cbPromptOnDelete.Checked := Value;
end;
end.
```