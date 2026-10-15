
# Socket API 函数

## getservbyport (LibC.pas)

### 语法

```pascal
function getservbyport(
  __port: Integer;
  __proto: PChar
): PServ;
```

### 描述

`getservbyport` 函数在已知服务的端口号和协议时返回服务器的详细信息。该函数扫描 `/etc/services` 文件以查找有关服务的信息，并返回结构体信息，例如服务名称、端口号、使用的协议以及任何可用于服务的别名。

### 参数

- `__port`: 这是应该查找服务的端口号，以网络字节序值传递。
- `__proto`: 这是服务的协议，通常是 `tcp`、`udp` 或 `/etc/protocols` 文件中的其他协议。

### 返回值

如果可以找到该服务，函数返回一个指向 `TServ` 结构的指针。如果无法找到该服务，函数返回 `nil` 值。`TServ` 详情如下：

```pascal
type
  servent = record
    s_name: PChar;
    s_aliases: PPChar;
    s_port: Integer;
    s_proto: PChar;
  end;

  TServ = servent;
  PServEnt = ^TServ;
```

`s_name` 代表服务名称，`s_aliases` 指向表示服务的备用名称，`s_port` 表示网络字节序端口号，`s_proto` 表示使用该端口的协议字符串。

### 另见

`setserv`, `enderv`, `getservbyname`

### 示例

> 列表 7.26 - 使用 `getservport` 函数

```pascal
uses
  Libc, HelperFunctions;

procedure TformService.btnClick(Sender: TObject);
var
  Service: PServEnt;
  Aliases: TString;
  Proto: array[0..100] of char;
begin
  StrCopy(Proto, cbProtocol.Text);
  Service := getservport(htons(edPort.Text), Proto);
  if Service <> nil then
  begin
    mmDetails.Lines.Add('ServiceName: ' + Service^.s_name);
    mmDetails.Lines.Add('Port: ' + intostr(ntohs(Service^.s_port)));
    mmDetails.Lines.Add('Protocol: ' + Service^.s_proto);
    Aliases := TStringList.Create;
    try
      PPCharToStringToList(Service^.s_aliases, Aliases);
      mmDetails.Lines.Add('Aliases: ' + Aliases.CommaText);
    finally
      Aliases.Free;
    end;
  else
    MessageDlg('Service could not be found.', mtInformation, [mbOK], 0);
end;
```

---

## getservent (LibC.pas)

### 语法

```pascal
function getservent: PServEnt;
```

### 描述

`getservent` 函数返回从 `/etc/services` 文件中读取的下一行，该行包含服务的列表。此函数通常在调用 `setservent` 之后重置 `/etc/services` 文件的位置。该函数返回指向 `TServEnt` 的指针，包含服务的名称、端口和协议。

### 另见

`setservent`, `endservent`, `getservbyport`, `getservbyname`

### 示例

> 列表 7.27 - 使用 `getservent` 函数

```pascal
uses
  Libc, HelperFunctions;

procedure TfrmServices.DisplayServices;
var
  Service: PServEnt;
  Item: TListItem;
  Aliases: TStringList;
begin
  lvServices.Clear;
  Aliases := TStringList.Create;
  try
    // 遍历所有服务
    setservent(0);
    Service := getservent;
    while Service <> nil do
    begin
      Item := lvServices.Items.Add;
      Item.Caption := StrPas(Service^.s_name);
      Item.SubItems.Add(intostr(ntohs(Service^.s_port)));
      PPCharToStringToList(Service^.s_aliases, Aliases);
      Item.SubItems.Add(Aliases.CommaText);
      Service := getservent;
    end;
  finally
    Aliases.Free;
  end;
end;
```

---

## getsockname (LibC.pas)

### 语法

```pascal
function getsockname(
  __fd: TSocket;
  var __addr: sockaddr;
  var __len: socklen_t
): Integer;
```

### 描述

`getsockname` 函数返回套接字的名称。当套接字通过调用 `bind` 函数绑定到特定的地址/端口组合时，它就有了名称。通常在应用程序内部，你已经设置了套接字名称。`getsockname` 函数通常用于在已知套接字文件描述符时获取地址信息。

### 参数

- `__fd`: 此参数是已经绑定到地址的套接字描述符。
- `__addr`: 这是一个指向 `TSockAddr` 结构的指针，在函数调用成功后，它将包含套接字所绑定的地址。
- `__len`: 此参数是一个 `socklen_t` 变量，定义了 `__addr` 参数中结构的大小。当函数返回时，该变量将实际持有 `__addr` 函数返回的结构的大小。

### 返回值

执行成功时，该函数返回 `0`，信息将存储在 `__addr` 参数中，且 `__addr` 中结构的大小将通过 `__len` 参数返回。如果函数失败，则返回 `-1`，可以通过调用 `errno` 获取错误代码。

### 参见

`bind`, `getpeername`

### 示例

> 列表 7.28 - 使用 `getsockname` 函数

```pascal
procedure DisplaySocketAddress(SocketFD: integer);
var
  addr: TSockAddr;
  addrSize: Cardinal;
begin
  // 此函数显示套接字绑定的名称（地址/端口）。
  // 此函数仅用于 IPv4 套接字。
  addrSize := sizeof(TSockAddr);
  if getsockname(SocketFD, addr, addrSize) = 0 then
  begin
    // 我们获得了套接字的名称
    if addr.sin_family = AF_INET then
    begin
      writeln('The socket is bound to:');
      write(' IP Address: ');
      if addr.sin_addr.s_addr = htonl(INADDR_ANY) then
        writeln('All local ip addresses.')
      else
        with addr.sin_addr.S_un_b do
        begin
          writeln(Format('%d.%d.%d.%d', [b1, b2, b3, b4]));
        end;
      writeln(' Port: ', ntohs(addr.sin_port));
    end;
    writeln('This function works only for the IPv4 sockets:');
  end
  else
    perror('Error in retrieving socket name: ');
end;
```

---

## getsockopt (LibC.pas)

### 语法

```pascal
function getsockopt(
    fd: TSocket;
    level: Integer;
    optname: Integer;
    optval: Pointer;
    var __optlen: socklen_t
): Integer;
```

### 描述

`getsockopt` 函数返回现有套接字的当前选项。该函数可以返回诸如发送和接收缓冲区的大小、套接字类型、生命周期、路由选项和其他可用选项。

### 参数

- `fd`: 用于检索选项的文件套接字描述符。
- `level`: 这是套接字选项的级别，代表选项的类别，例如你想检查的是套接字选项还是 TCP 选项。Kylix 的 `LibC.pas` 实现仅包含了套接字选项 `SOL_SOCKET`，用于检查套接字选项。虽然此参数还有其他可用值，但它们在 Kylix 实现的 `LibC` 中并未声明。
- `optname`: 此参数是将被检查的选项名称，其值来自以下列表。这些选项中的大多数将返回一个非零值表示真、0 假的值，或者返回一个指定选项的整数值。
  - `SO_REUSEADDR`: 此选项指定服务器是否可以多次绑定到特定端口。
  - `SO_KEEPALIVE`: 使用此选项将导致连接的套接字定期发送消息，以确保连接活跃。
  - `SO_LINGER`: 此选项检索当套接字仍有数据等待发送时，可靠套接字所发生的结果。
  - `SO_BROADCAST`: 此选项指定此套接字是否可以进行 UDP 广播。
  - `SO_OOBBAND`: 此选项指定应用程序是否可以像读取普通数据一样，使用 `write` 或 `recv` 函数读取带外数据。
  - `SO_SNDBUF`: 此选项将返回套接字发送缓冲区的大小。
  - `SO_RCVBUF`: 此选项将返回套接字接收缓冲区的大小。
  - `SO_TYPE`: 此选项将返回套接字类型，TCP 可能为 1，UDP 套接字为 2。
  - `SO_ERROR`: 读取此选项将清除套接字的错误状态，并返回调用之前的套接字错误状态。
  - `SO_DONTROUTE`: 读取此选项将指定套接字是否允许路由出本地网络。
- `__optval`: 此参数指向记录结构的指针，用于根据 `level`/`optname` 参数组合检索的特定选项的信息。例如，当使用整数时，该字段将是指向有效整数的指针。
- `__optlen`: `__optlen` 参数是传递给 `__optval` 参数的结构的字节长度。通常，对于整数，这将是 `sizeof(integer)`。

### 返回值

当函数执行成功时，返回 `0`。如果函数由于任何原因失败（通常是因为 `level` 或 `optname` 字段中的无效值），它将返回 `-1`。

### 参见

`setsockopt`

### 示例

> 列表 7.29 - 使用 `getsockopt` 函数

```pascal
procedure TfrmSocketOptions.DisplaySocketOptions(fdSocket: integer);
var
  optVal: integer;
  optLen: socklen_t;
begin
  optLen := sizeof(optVal);
  // 注意：OCR 中的实现逻辑是碎片化的；
  // 这代表了调用函数的标准结构。
  if getsockopt(fdSocket, SOL_SOCKET, SO_REUSEADDR, @optVal, optLen) = 0 then
  begin
    // 处理选项
  end;
end;
```

---

## htons (LibC.pas)

### 语法

```pascal
function htons(
  _hostshort: uint16_t
): uint16_t;
```

### 描述

此函数将主机字节序值转换为网络字节序值。有关网络字节序的更多信息，请参阅本章中的“Socket Addresses”章节。

### 参数

- `_hostshort`: `_hostshort` 参数是待转换的主机字节序整数值。

### 返回值

函数返回一个字节序与网络标准排序方式相同的整数值。

### 另见

`htohl`, `ntohl`, `ntohs`

### 示例

> 列表 7.31 - 使用 `htons` 函数

```pascal
var
  SocketAddress: TSockAddr;
begin
  with SocketAddress do
  begin
    sin_family := AF_INET;
    sin_addr.S_addr := inet_addr('127.0.0.1');
    // 连接到端口 80。
    sin_port := htons(80);
  end;
end;
```

---

## inet_addr (LibC.pas)

### 语法

```pascal
function inet_addr(
  _cp: PChar
): in_addr_t;
```

### 描述

`inet_addr` 函数将形式如 `203.11.32.41` 的 IPv4 地址转换为 `in_addr_t` 记录，该记录可用于定义要连接的机器时将地址传递到地址结构中。

### 参数

- `_cp`: `cp` 参数是一个 IPv4 地址格式的以空结尾的字符串，它将转换为有效的 `in_addr_t` 结构，例如 `203.16.80.50`。

### 返回值

如果传递给 `_cp` 参数的 IP 地址是有效的，函数将返回一个有效的 `in_addr_t` 记录，其中包含 IPv4 地址对应的值，以便通过网络传输。如果传递给 `_cp` 参数的值不是有效的 IP 地址，则函数将返回 `-1`。

### 参见

`inet_ntoa`

### 示例

参见列表 7.4 - 定义用于网络使用的地址。

---

## inet_ntoa (LibC.pas)

### 语法

```pascal
function inet_ntoa(
  in: in_addr
): PChar;
```

### 描述

`inet_ntoa` 函数将定义网络字节序的给定主机地址的 `in_addr` 结构转换为标准 IPv4 数字格式的值。

### 参数

- `__in`: 这是网络字节格式化值的主机地址。

### 返回值

成功时，此函数返回一个指向以空结尾字符串的指针，该字符串包含传递给 `__in` 参数的地址的 IPv4 地址。所使用的值存储在内存中，应该立即复制，因为对 `inet_ntoa` 函数的其他调用会更改它所指向的数据。

### 参见

`inet_addr`

### 示例

参见列表 7.32 - 使用 `ntohs` 函数。

---

## listen (LibC.pas)

### 语法

```pascal
function listen(
  __fd: TSocket;
  __n: Cardinal
): Integer;
```

### 描述

一旦创建了 socket 并绑定到地址，它就需要监听该 socket 上的客户端 socket 连接。`listen` 函数在服务器上创建一个队列，以便客户端 socket 能够连接到服务器，并定义了在客户端开始被 socket 拒绝之前可以连接到 socket 的客户端连接数。

### 参数

- `__fd`: 这是将用作服务器 socket 的 socket 文件描述符。此参数通常是 `socket` 函数成功调用的返回值。
- `__n`: 此参数是客户端连接等待队列的大小。一旦达到队列大小，客户端将不再接受连接到服务器 socket。

### 返回值

成功时，此函数返回 `0`。如果函数失败，则返回 `-1`。

### 参见

`socket`, `bind`, `accept`

### 示例

参见列表 7.11 - 使用该函数。

---

## ntohl (LibC.pas)

### 语法

```pascal
function ntohl(
  _netlong: uint32_t
): uint32_t;
```

### 描述

此函数将网络字节序值转换为主机系统上有效的整数值。有关网络字节序的更多信息，请参阅本章中的“Socket Addresses”章节。

### 参数

- `_netlong`: `_netlong` 参数是待转换的网络字节序整数值。

### 返回值

函数返回一个字节序与主机系统排序方式相同的整数值。

### 参见

`htohl`, `htons`, `ntohs`

---

## ntohs (LibC.pas)

### 语法

```pascal
function ntohs(
  _netshort: uint16_t
): uint16_t;
```

### 描述

此函数将通常用于网络端口地址的网络字节序短整数值转换为与主机系统兼容的值。有关网络字节序的更多信息，请参阅本章标题为“Socket Addresses”的章节。

### 参数

- `__netshort`: `__netshort` 参数是一个网络字节序值。

### 返回值

函数返回一个字节序与主机系统排序方式相同的短整数值。

### 参见

`htohl`, `htons`, `ntohl`

### 示例

> 列表 7.32 - 使用 `ntohs` 函数
