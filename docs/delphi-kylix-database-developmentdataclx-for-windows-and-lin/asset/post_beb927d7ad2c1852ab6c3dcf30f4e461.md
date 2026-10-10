
## LISTING 8.2

```pascal
uses
  MainForm;

{$R "*.DFM"}

class procedure TMethodsDM.UpdateRegistry(Register: Boolean;
  const ClassID, ProgID: string);
begin
  if Register then
  begin
    inherited UpdateRegistry(Register, ClassID, ProgID);
    EnableSocketTransport(ClassID);
    EnableWebTransport(ClassID);
  end
  else
  begin
    DisableSocketTransport(ClassID);
    DisableWebTransport(ClassID);
    inherited UpdateRegistry(Register, ClassID, ProgID);
  end;
end;

function TMethodsDM.GetServerTime: TDateTime;
begin
  Result := Now;
end;

procedure TMethodsDM.TestCallbacks;
var
  Index: Integer;
begin
  if not VarIsEmpty(FCallback) then
    for Index := 1 to 3 do
      FCallback.Test;
end;

procedure TMethodsDM.SetCallback(Callback: OleVariant);
begin
  FCallback := Callback;
end;

procedure TMethodsDM.RemoteDataModuleCreate(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, 1, 0);
end;
```

## LISTING 8.2 Continued

```pascal
procedure TMethodsDM.RemoteDataModuleDestroy(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, -1, 0);
end;

initialization
  TComponentFactory.Create(ComServer, TMethodsDM,
    Class_MethodsDM, ciMultiInstance, tmApartment);
end.
```

Listing 8.3 contains the source code for the main form of the client application.

## LISTING 8.3 MethodsClient—MainForm.pas

```pascal
unit MainForm;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, DB, Grids, DBGrids, StdCtrls, MethodsServer_TLB, ComObj, ActiveX;

type
  TTest = class(TAutoIntfObject, ITestCallback)
  protected
    procedure Test; safecall;
  end;

  TfrmMain = class(TForm)
  DBGrid1: TDBGrid;
  DataSource1: TDataSource;
  btnGetServerTime: TButton;
  btnTestCallbacks: TButton;
  procedure FormCreate(Sender: TObject);
  procedure btnGetServerTimeClick(Sender: TObject);
  procedure btnTestCallbacksClick(Sender: TObject);
  private
    { Private declarations }
    FTest: TTest;
  public
    { Public declarations }
  end;
```

## LISTING 8.3 Continued

```pascal
var
  frmMain: TfrmMain;

implementation

uses
  DataModule;

{$R *.dfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  DM.cdsContacts.Open;
end;

procedure TfrmMain.btnGetServerTimeClick(Sender: TObject);
var
  D: TDateTime;
begin
  D := DM.SocketConnection1.AppServer.GetServerTime;
  ShowMessage(TimeToStr(D));
end;

procedure TfrmMain.btnTestCallbacksClick(Sender: TObject);
var
  typeLib: ITypeLib;
begin
  OleCheck(LoadRegTypeLib(LIBID_MethodsServer, 1, 0, 0, typeLib));
  FTest := TTest.Create(typeLib, ITestCallback);
  DM.SocketConnection1.AppServer.SetCallback(FTest as IDispatch);
  DM.SocketConnection1.AppServer.TestCallbacks;
end;

procedure TTest.Test;
begin
  ShowMessage('In callback');
end;

end.
```

## The Briefcase Model

Multitier applications lend themselves to something called the briefcase model. When in the office, the user is presumably connected to the server and is running an application using live data. Before leaving the office, the user downloads any data that may be needed onto the user’s local machine, for use while away from the office. The general overview of the briefcase model is as follows:

When in the office, the user works with live data directly from the application server. While on the road, the user works with a local copy of the data, making additions or modifications to the data as needed. Upon return to the office, the user reconnects to the server and reconciles all updates back to the server.

This magic is performed using the techniques you have already learned in this book. When connected to the server, dataset providers provide a live copy of the data to the client application’s client datasets. Before the user leaves the office, the data is saved locally by calling `TClientDataSet.SaveToFile`.

While on the road, the client is unable to connect to the application server; instead, it loads the local copy of the data by calling `TClientDataSet.LoadFromFile`. Changes are accumulated in the change log, which is persisted by calling `TClientDataSet.SaveToFile` before the user exits the application.

When the user returns to the office, the client application again calls `TClientDataSet.LoadFromFile` to load the local copy of the data, but then calls `TClientDataSet.ApplyUpdates` to resolve any updates back to the application server.

Note that the server application does not change in any way—only the client application contains code to support the briefcase model.

Because Delphi ships with a useful briefcase demo application, I won’t duplicate its functionality here. Instead, I encourage you to take a look at the Delphi demo. For a typical Delphi installation, look at `C:\Program Files\Borland\Delphi6\Demos\Midas\Briefcase`.

> NOTE
> Rather than calling LoadFromFile and SaveToFile in your application, you can simply assign the client dataset’s FileName property to the name of the local file to save to and load from. Delphi will then take care of loading and saving the data at the appropriate times.

## Stateless Servers

In the last chapter, I showed you how you can limit the amount of data returned at a given time from the application server. The catch with limiting the amount of data returned from the server is that you must let the server know from where to start retrieving data each time it fetches a new data packet. Delphi database applications are *stateless*, meaning that the server-side database components don't keep track of their current location in the dataset. When the provider retrieves data from a TSQLDataSet or other dataset component, the dataset is opened, data is sent to the provider, and then the dataset is closed. Because the dataset is accessed only for a short period of time, a single server-side dataset can service multiple client applications, reducing memory load and increasing performance. This isn't much of an issue with a local connection, but it becomes an important consideration when using remote connections. Conceptually, incremental data fetching on a stateless server works like this:

- The provider fetches a set of records, remembering the ID of the last record in the batch.
- The provider notifies the client application of the last record.
- The client remembers the last record fetched.
- When the client fetches the next batch of records from the server, it notifies the server of the last record previously retrieved.
- The server retrieves the next batch of records that occurs after the last record previously retrieved.

To implement a stateless server, you need to supply event handlers for three provider events on the server, as well as for two client dataset events on the client. Let's start with the server:

In the application server, you need to set up the TSQLDataSet as a parameterized query, like this:

```sql
SELECT * FROM CONTACTS WHERE ID > :MinID ORDER BY ID
```

This will select only contacts with an ID greater than the last ID that has already been fetched. Now, provide an event handler for the provider's GetData event. In this event, you'll save the last ID retrieved from the contact table.

```pascal
procedure TStatelessServerData.pvContactsGetData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  DataSet.Last;
  pvContacts.Tag := DataSet.FieldByName('ID').AsInteger;
end;
```

The call to **DataSet.Last** does not operate directly on the **TSQLDataSet** component. Instead, it moves to the last record of the batch of records that is about to be sent back to the client application. The ID of that last fetched record is then saved temporarily in the **Tag** property of the provider.

Next, write an event handler for the provider’s **AfterGetRecords** event handler. In this handler, you’ll pass the last retrieved ID back to the client application via the **OwnerData** parameter.

```pascal
procedure TStatelessServerData.pvContactsAfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  OwnerData := pvContacts.Tag;
end;
```

Finally, on the server, you need to handle the provider’s **BeforeGetRecords** event handler. In this event, you’ll set the value of the **MinID** parameter so that the query knows what record to fetch next. The following code snippet shows how to accomplish this:

```pascal
procedure TStatelessServerData.pvContactsBeforeGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  if not VarIsEmpty(OwnerData) then begin
    sqlContacts.Params.ParamValues['MinID'] := OwnerData;
    sqlContacts.Refresh;
  end;
end;
```

That’s all you need to do on the server. In the client application, you need to first provide an event handler for the client dataset’s **AfterGetRecords** event. In this event handler, you’ll save the last ID retrieved from the server, as the following code snippet illustrates:

```pascal
procedure TForm1.cdsContactsAfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  cdsContacts.Tag := OwnerData;
end;
```

In this example, the last retrieved ID (provided in the **OwnerData** parameter) is again stored in the client dataset’s **Tag** property. You could also set up a form variable named **FLastContactID** to save the ID.

Finally, provide an event handler for the client dataset’s **BeforeGetRecords** event. In this event handler, you’ll pass the last retrieved ID back to the server so that it knows where to start fetching data from.
