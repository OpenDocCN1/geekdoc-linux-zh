# TABLE 8.3 TSocketConnection Properties

| Property | Description |
|---|---|
| Address | Specifies the IP address of the remote machine to connect to. You may specify the name of the remote machine instead of the IP address by setting the Host property rather than the Address property. |
| Host | Specifies the name of the remote machine to connect to. You may specify the IP address of the remote machine instead of the name by setting the Address property rather than the Host property. |
| InterceptGUID | Specifies the GUID of a COM object that intercepts data packets sent between the client and the application server. You may specify the ProgID of the COM object rather than the GUID by setting the InterceptName property instead of InterceptGUID. Data interceptors are discussed in the section titled “Intercepting Data Packets,” later in this chapter. |
| InterceptName | Specifies the ProgID of a COM object that intercepts data packets sent between the client and the application server. You may specify the GUID of the COM object rather than the ProgID by setting the InterceptGUID property instead of InterceptName. Data interceptors are discussed in the section titled “Intercepting Data Packets,” later in this chapter. |
| Port | Specifies the port that the socket server uses to listen to socket requests. By default, this is set to 211. |
| ServerGUID | Specifies the GUID of the application server that the client will connect to. You can set the server name using the ServerName property instead of ServerGUID. |
| ServerName | Specifies the name of the application server that the client will connect to. You can set the server GUID using the ServerGUID property instead of ServerName. |
| SupportCallbacks | Set to True if your server supports callbacks to the client application. If this property is True, WinSock 2 must be present on the server machine. When False, the server machine does not require WinSock 2 to operate properly, but it also doesn’t support callbacks. |

# The Socket Server

To connect to a remote application server using sockets, you must run a socket server on the server machine. Although you can write your own socket server if you want, Delphi ships with a prewritten server named ScktSrvr. Source code for the server is included with the VCL source, so you can modify it or use it as a basis for writing your own server.

+   *   8
+   *   DataSnap