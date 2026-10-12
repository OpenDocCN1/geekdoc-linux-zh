
```cpp
// vSendUdpMessage 方法调用继承自
// XPCUdpSocket 的 sendMessage 来向特定的主机和 socket 编号发送消息。
void vSendUdpMessage(void *_vMessage, int _iMsgLen, char *_sHost, int _iPort = 0)
{
    sendMessage(_vMessage, _iMsgLen, _sHost, _iPort);
}

// vReply 方法调用继承自
// XPCUdpSocket 的 sendMessage
// 来向特定的主机和 socket 编号发送消息。
void vReplyReply(void *_vMessage, int _iMsgLen, char *_sHost, int _iPort = 0)
{
    reply(_vMessage, _iMsgLen, _sHost, _iPort);
}
```

## 与 Windows 集成接字

### `CStockPositionDlg` 类的 `OnInitDialog()` 方法

`OnInitDialog()` 在客户端界面显示之前执行所有必要的应用程序设置。此应用程序设置包括 `XPCAsyncUdpSocket` 实例，调用 `vBindAsyncSocket()` 将接字绑定到其指定的端口号，并将接字文件描述符附加到继承的 `AsyncSocket` 类中。这种附加操作允许接收 UDP 消息。

### 列表 5.53 `CStockPositionDlg` 的 `OnInitDialog()` 方法

```cpp
BOOL CStockPositionDlg::OnInitDialog()
{
    CDialog::OnInitDialog();
    ...
    // 窗口接字库已初始化。
    AfxSocketInit();

    // 创建 XPCAsyncUdpSocket 实例。向它传递了应用程序类
    // (CStockPositionDlg) 的指针以及 UDP 接字绑定的接字端口号。
    // 接字被绑定到该端口号并附加到
    // AsyncSocket 类。当接字上检测到数据时，会调用 XPCAsyncUdpSocket 类的 OnReceive 方法。
    try {
        portfolioSocket = new XPCAsyncUdpSocket<CStockPositionDlg>(this, PORT_NUM);
        portfolioSocket->BindAsyncSocket();
    }
    catch(XPCException&exceptObject) {
        // 如果创建和绑定接字时失败，将抛出异常
        // 并退出应用程序。
        MessageBox(exceptObject.GetException(), "Socket Error", MB_OK);
        CDialog::OnOK();
    }

    // 投资组合中的持仓数量初始化为 0。
    iTotalPositions = 0;
    return TRUE; // 你将焦点设置到某个控件
}
```

## 第 5 章：接字 — 跨平台通信构建模块

### `CStockPositionDlg` 类的 `vProcessMessage()` 方法

`vProcessMessage()` 由 `XPCAsyncUdpSocket` 的 `OnReceive()` 调用，`vProcessMessage()` 接收 UDP 接字收到的缓冲区。该缓冲区被强制转换回原始的 `XPTransaction` 对象，其值被传递给 `vUpdatePositionList()` 以更新股票代码位置列表。

### 列表 5.54 `CStockPositionDlg` 的 `vProcessMessage()` 方法

```cpp
void CStockPositionDlg::vProcessMessage(char *_sMsg, int _iNumBytes)
{
    if (_iNumBytes != sizeof(XPTransaction))
    {
        MessageBox("Error receiving XPTransaction Object", "Receive Error", MB_OK);
        return;
    }

    // 接收到的缓冲区被强制转换为 XPTransaction 实例。
    XPTransaction *incomingTransaction = (XPTransaction*)_sMsg;

    // 使用持仓更新的值调用 vUpdatePositionList。
    vUpdatePositionList(incomingTransaction);
}
```
