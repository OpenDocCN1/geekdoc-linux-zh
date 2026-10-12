
#include <XPcpSocket.h>             // XPcpSocket 定义

#include <XPCException.h> // XPCException 定义

#include <XPCTTransaction.h> // XPTransaction 定义

// CStockPositionClientDlg 是一个 Windows NT 对话框应用程序，

// 继承自 MFC 的 CDialog 类。

class CStockPositionClientDlg : public CDialog

{

    // 构造函数

public:

    CStockPositionClientDlg(CWnd* pParent = NULL); // 标准构造函数

    // 析构函数

    ~CStockPositionClientDlg() { if (positionSocket) delete positionSocket; }

    void vUpdatePositionList(CTTransaction *) // 更新股票

                            // 仓位列表

    XPcpSocket *positionSocket; // 指向 XPcpSocket

                                // 实例的指针

    // 类定义的其余部分与列表 5.41 相同

};

## 使用 TCP 的 CStockPositionClientDlg 的 OnInitDialog() 方法

`OnInitDialog()` 在客户端界面显示之前执行所有必要的应用程序设置。这包括创建 `XPcpSocket` 实例并创建一个连接到服务器的线程。在创建服务器连接线程之前，会禁用 Windows 接口。创建用于接收服务器数据的线程也是在 `OnInitDialog` 中完成的。

### 列表 5.47 CStockPositionClientDlg 的 OnInitDialog() 方法

```cpp
BOOL CStockPositionClientDlg::OnInitDialog()

{

    CDialog::OnInitDialog();

// 在 socket 连接到服务器之前，禁用所有 CStockPositionClientDlg 数据输入 Windows 窗口。

// 这防止了在未连接的 TCP socket 上发送数据。

m_TickerEdit.EnableWindow(FALSE);

m_UserEdit.EnableWindow(FALSE);

m_QuantEdit.EnableWindow(FALSE);

m_BsEdit.EnableWindow(FALSE);

// 初始化 socket 库。

AfxSocketInit();

// 将记录数初始化为 0

iTotalPositions = 0;

// 创建并连接 positionSocket。

try {

    // 创建 TCP socket 并在 PORT_NUM 定义

    // 指定端口上进行通信。

    positionSocket = new XPCTcpSocket((long int)PORT_NUM);

    // 所有与 socket 相关的错误都会捕获，并在消息框中显示给

    // 用户。应用程序在检测到错误时会终止。

} catch(XPCException&socketExcept) {

    MessageBox(socketExcept.GetException("Socket Error", MB_OK);

    CDialog::OnOK();

}

// 初始化 iConnectThread 并传递当前 CStockPositionDlg 类

// 实例的指针。iConnectThreadProc 连接到

// UNIX 服务器并设置所有 CStockPositionDlg 输入窗口启用。

AfxBeginThread(iConnectThreadProc, (void*)this);

}
```

## CStockPositionDlg 类的 iConnectProc() 线程

`iConnectProc()` 是连接客户端到 UNIX 仓位追踪服务器的函数。它使用作为参数传递的 `CStockPositionDlg` 类地址，并调用 `positionSocket` 成员变量的 `vConnect()` 成员函数。如果连接成功，“股票交易区域”内的 Windows 窗口将被启用，并产生一个线程用于接收来自服务器的传输。

### 列表 5.48 CStockPositionDlg 的 iConnectThreadProc() 方法

```cpp
UINT iConnectThreadProc(void *param)

{

  // 将接收到的参数转换回原始 CStockPositionDlg 类

  CStockPositionDlg *positionDlg = (CStockPositionDlg*)param;

  // 尝试连接到 UNIX 服务器

  try

  {

    positionDlg->vConnect(UNIX_SERVER_HOSTNAME);

  }

  catch(XPException &ex)

  {

    // 如果连接失败，将显示包含错误的消息框

    positionDlg->MessageBox(ex.GetException(), MB_OK);

    return 0;

  }

  // 当 socket 连接时启用所有 CStockPositionDlg 输入窗口。

  positionDlg->m_TickerEdit.EnableWindow(TRUE);

  positionDlg->m_UserEdit.EnableWindow(TRUE);

  positionDlg->m_QuantEdit.EnableWindow(TRUE);

  positionDlg->m_BsEdit.EnableWindow(TRUE);

  return 1;

}
```

## 使用 TCP 的 CStockPositionDlg 类 iReceiveProc() 函数

`iReceiveProc()` 函数的大部分与列表 5.45 相同。唯一的变化是在发送数据时检查客户端/服务器连接。如果连接断开，“股票交易区域”窗口组件将被禁用。

### 列表 5.49 使用 TCP 的 CStockPositionDlg iReceiveProc() 函数

```cpp
UINT iReceiveThreadProc(void *param)

{

    CStockPositionDlg *positionDlg = (CStockPositionDlg*)param;

    // 循环接收 UNIX 服务器的股票仓位传输。

    while(1)

    {

        try{

            // 等待接收服务器传输。由于这

            // 是线程，阻塞不会影响主应用程序。

            int nNumBytes = positionDlg->positionSocket->iReceiveMessage((void *)&newTransaction, sizeof(newTransaction));

            // 如果调用 iReceiveMessage 方法导致 socket 

            // 客户端/服务器连接断开，则禁用“股票

            // 输入”窗口组件并返回线程。

            if ((nNumBytes == 0) || (WSAGetLastError() == WSAGECONRESET))

            {

                positionDlg->m_TickerEdit.EnableWindow(FALSE);

                positionDlg->m_UserEdit.EnableWindow(FALSE);

                positionDlg->m_QuantEdit.EnableWindow(FALSE);

                positionDlg->m_BsEdit.EnableWindow(FALSE);

                return 0;

            }

        } catch(XPCException &socketEx)

        {

            // 处理错误

        }

    }

}
```

# 430 第 5 章：套字 — 跨平台通信构建模块

## 列表 5.50 CStockPositionDlg 的 OnExecuteButton() 方法

```cpp
