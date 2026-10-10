# LISTING 4.1 Continued

```
procedure btnClearLogClick(Sender: TObject);
procedure btnDisconnectClick(Sender: TObject);
procedure ClientDataSet1BeforeCancel(DataSet: TDataSet);
procedure ClientDataSet1BeforeClose(DataSet: TDataSet);
procedure ClientDataSet1BeforeDelete(DataSet: TDataSet);
procedure ClientDataSet1BeforeEdit(DataSet: TDataSet);
procedure ClientDataSet1BeforeInsert(DataSet: TDataSet);
procedure ClientDataSet1BeforeOpen(DataSet: TDataSet);
procedure ClientDataSet1BeforePost(DataSet: TDataSet);
procedure ClientDataSet1BeforeScroll(DataSet: TDataSet);
procedure btnOptionsClick(Sender: TObject);
procedure FormCreate(Sender: TObject);
private
  { Private declarations }
  FLogScrollEvents: Boolean;
  FPromptOnDelete: Boolean;
  procedure Log(EventType: TLogEventType);
public
  { Public declarations }
end;
var
  frmMain: TfrmMain;
implementation
uses OptionsForm;
{$R *.dfm}
procedure TfrmMain.Log(EventType: TLogEventType);
const
  EventText: array[TLogEventType] of string = (
    'BeforeCancel', 'BeforeClose', 'BeforeDelete', 'BeforeEdit',
    'BeforeInsert', 'BeforeOpen', 'BeforePost', 'BeforeScroll',
    'AfterCancel', 'AfterClose', 'AfterDelete', 'AfterEdit',
    'AfterInsert', 'AfterOpen', 'AfterPost', 'AfterScroll');
var
  ListItem: TListItem;
begin
  ListItem := lvLog.Items.Add;
  ListItem.Caption := EventText[EventType];
end;
```