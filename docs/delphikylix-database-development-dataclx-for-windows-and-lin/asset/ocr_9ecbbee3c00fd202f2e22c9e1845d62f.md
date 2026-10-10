```
**LISTING 5.3** Continued

begin
FDataLink.Field.AsDateTime := Date;
end;

procedure TETHHDBDateTimePicker.CMExit(var Message: TCMExit);
begin
try
FDataLink.UpdateRecord;
except
SetFocus;
raise;
end;
end;

function TETHHDBDateTimePicker.ExecuteAction(Action: TBasicAction): Boolean;
begin
Result := inherited ExecuteAction(Action) or (FDataLink <> nil) and
FDataLink.ExecuteAction(Action);
end;

function TETHHDBDateTimePicker.UpdateAction(Action: TBasicAction): Boolean;
begin
Result := inherited UpdateAction(Action) or (FDataLink <> nil) and
FDataLink.UpdateAction(Action);
end;
end.
```

# Sample Application

Listing 5.4 is a sample application that makes use of many (but not all) of the data-aware components discussed in this chapter. As you can see from Listing 5.4, there is very little code in this application. Thanks to VCL/CLX, the data-aware components encapsulate almost everything needed to display and update datasets in your applications.

```
**LISTING 5.4** DataAware—MainForm.pas

unit MainForm;

interface

uses
SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, DB, DBClient,
QStdCtrls, QExtCtrls, OButtons, Mask, QComCtrls, QDBCtrls, OMask;
```