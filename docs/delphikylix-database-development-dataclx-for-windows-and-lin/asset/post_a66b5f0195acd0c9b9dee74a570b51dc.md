
## Intercepting Data Packets

Some *applications* may deal with sensitive data, such as account numbers, and the like. By default, data transmitted between the server and client *applications* is not encrypted or compressed in any way, meaning that anyone bright enough to figure out how to listen in on the socket server port could obtain this data for himself.

When using sockets, you can write a COM object that intercepts data being sent over the socket connection. This object can compress, encrypt, or otherwise modify the data to keep it from prying eyes.

To implement an interceptor object, you need to perform the following steps:

- 1. Write a COM object that implements the `IDataIntercept` interface. Because Delphi ships with a demo that shows how to write this object (located in `C:\Program Files\Borland\Delphi6\Demos\Midas\Inteapt`), I won't duplicate that example in this book.
- 2. Register the COM object on both the server machine and all client machines.
- 3. Set the `TSocketConnection`'s `ServerName` property to the name of the application server.
- 4. Inside the socket server, set the `Intercept` Name to the same name.
- 5. Run the application as usual.

You should debug your application without the interceptor to make sure it works correctly before adding the interceptor into the mix.

## DCOM Connections

A `TDCOMConnection` uses Distributed COM (DCOM) as its underlying protocol, tying it to the Windows operating system. DCOM is a little tricky to set up properly, especially if the application server isn't running on a Windows domain server.

I assume at this point that if you're going to use `TDCOMConnection`, you know how to set up and use DCOM. If you need additional information on configuring DCOM, you can look in my COM book or see Dan Miser's Web page at www.distribucon.com.

Table 8.4 lists the most important properties for `TDCOMConnection`.

**Table 8.4** TDCOMConnection Properties

| Property | Description |
| :--- | :--- |
| ComputerName | Specifies the name of the remote computer to connect to. If `ComputerName` is blank, `TDCOMConnection` assumes that the application server is located on the local machine. |
| ServerGUID | Specifies the GUID of the application server that the client will connect to. You can set the server name using the `ServerName` property instead of `ServerGUID`. |
| ServerName | Specifies the name of the application server that the client will connect to. You can set the server GUID using the `ServerGUID` property instead of `ServerName`. |

![](img/52a35759a0f10dade27a840504be5d82_346_0.png)

## HTTP Connections

TWebConnection uses HTTP as its transport protocol, which makes it useful for writing applications that run over the Internet. HTTP offers some additional features over a socket connection so that you can take advantage of SSL security. Also, you can connect to a server computer that is located behind a firewall.

When using a TWebConnection, you must be sure to redistribute the Web server application (httpsrvr.dll) along with the server application. httpsrvr.dll is an ISAPI extension that brokers the HTTP call from the client to the COM object on the server application. In addition, the client machine must contain a copy of wininet.dll. Wininet.dll is included with Internet Explorer version 3 and later.

Table 8.5 lists the most important properties for TWebConnection.

**Table 8.5** TWebConnection Properties

| Property | Description |
| :--- | :--- |
| Password | Valid password used for authentication on the host machine. This may be left blank if the host does not require authentication. |
| Proxy | Semicolon-delimited list of proxy servers that can be used to resolve the IP address of the host machine. |
| ServerGUID | Specifies the GUID of the application server that the client will connect to. You can set the server name using the `ServerName` property instead of `ServerGUID`. |
| ServerName | Specifies the name of the application server that the client will connect to. You can set the server GUID using the `ServerGUID` property instead of `ServerName`. |
| URL | The URL used to locate httpsrvr on the host machine. |
| UserName | Valid username used for authentication on the host machine. This may be left blank if the host does not require authentication. |

## SOAP Connections

TSOAPConnection uses SOAP to communicate between the client and server applications. TSOAPConnection is similar to TWebConnection in that it uses HTTP as the underlying protocol.

As with TWebConnection, the client machine must contain a copy of wininet.dll.

Table 8.6 lists the most important properties for TSOAPConnection.

**Table 8.6** TSOAPConnection Properties

| Property | Description |
| :--- | :--- |
| Password | Valid password used for authentication on the host machine. This may be left blank if the host does not require authentication. |
| Proxy | Semicolon-delimited list of proxy servers that can be used to resolve the IP address of the host machine. |
| URL | The URL used to locate the application server on the host machine. |
| UserName | Valid username used for authentication on the host machine. This may be left blank if the host does not require authentication. |

## CORBA Connections

TCORBAConnection uses CORBA, or IIOP, as its underlying protocol. To establish a CORBA connection to an application server, you must be running a CORBA Smart Agent somewhere on your network.

Table 8.7 lists the most important properties for TCORBAConnection.

**Table 8.7** TCORBAConnection Properties

| Property | Description |
| :--- | :--- |
| HostName | Specifies the machine where the application server is located. If this property is blank, the connection component will connect to the first available machine that supports the interface specified by the RepositoryID property. |
| ObjectName | Set this property if the interface specified by RepositoryID must be implemented by a specific instance of the object. Leave this property blank if only one object supports the specified interface. |
| RepositoryID | Specifies the CORBA data module to connect to. May take one of two forms: `IDL:ProjectName/CorbaDataModuleName:1.0` or `ProjectName/CorbaDataModuleName` |

## A Complete Example

The following example uses a TSocketConnection to connect to the application server remotely. Also, it demonstrates how to call additional methods on the server and how the server can use a callback interface to call methods on the client or fire events back to the client application.

Listing 8.2 contains the source code for the server’s remote data module.

```pascal
### LISTING 8.2 MethodsServer—ServerDataModule.pas

unit ServerDataModule;

{ $WARN SYMBOL_PLATFORM OFF }

interface

uses
    Windows, Messages, SysUtils, Classes, ComServ, ComObj, VCLCom, DataBkr, DBClient, MethodsServer_TLB, StdVcl, DBXpress, FMTBcd, DB, SqlExpr, Provider, Variants;

type
    TMethodsDM = class(TRemoteDataModule, IMethodsDM)
        conn: TSQLConnection;
        sqlContacts: TSQLDataSet;
        pvContacts: TDataSetProvider;
        procedure RemoteDataModuleCreate(Sender: TObject);
        procedure RemoteDataModuleDestroy(Sender: TObject);
    private
        { Private declarations }
        FCallback: OleVariant;
    protected
        class procedure UpdateRegistry(Register: Boolean;
            const ClassID, ProgID: string); override;
        function GetServerTime: TDateTime; safecall;
        procedure SetCallback(Callback: OleVariant); safecall;
        procedure TestCallbacks; safecall;
    public
        { Public declarations }
    end;

implementation

uses
  MainForm;

{$R *.DFM}

class procedure TMethodsDM.UpdateRegistry(Register: Boolean;
  const ClassID, ProgID: string);
begin
  if Register then
    begin
      Inherited UpdateRegistry(Register, ClassID, ProgID);
      EnableSocketTransport(ClassID);
      EnableWebTransport(ClassID);
    end else
    begin
      DisableSocketTransport(ClassID);
      DisableWebTransport(ClassID);
      Inherited UpdateRegistry(Register, ClassID, ProgID);
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
