

## ICMP 回显实用程序代码

```vb
timeout
Text3.Text = Text3.Text + "ICMP Request Timeout" + Chr$(13) + Chr$(10)
End If
Next NbOfPkts
End Sub

Sub vbWSACleanup()
' 子程序，执行 WSACleanup
iReturn = WSACleanup()
If iReturn <> 0 Then ' 如果出现 WSock32 错误，则报告错误。
    sMsg = "WSock32 错误 - 在 Cleanup 中发生 " & Trim$(Str$(iReturn))
    MsgBox sMsg, vbOKOnly, "VB4032-ICMPEcho"
    End
End If
End Sub

Sub vbWSAStartup()
iReturn = WSAStartup(&H101, WSAData)
If iReturn <> 0 Then ' 如果出现 WSock32 错误，则报告错误
    MsgBox "WSock32.dll 无响应！", vbOKOnly, "VB4032-ICMPEcho"
End If
If LoByte(WSAData.wVersion) < WS_VERSION_MAJOR Or (LoByte(WSAData.wVersion) = WS_VERSION_MAJOR And HiByte(WSAData.wVersion) < WS_VERSION_MINOR) Then
    sHighByte = Trim$(Str$(HiByte(WSAData.wVersion)))
    sLowByte = Trim$(Str$(LoByte(WSAData.wVersion)))
    sMsg = "WinSock 版本 " & sLowByte & "." & sHighByte
    sMsg = sMsg & " 不受支持 "
    MsgBox sMsg, vbOKOnly, "VB4032-ICMPEcho"
    End
End If
If WSAData.iMaxSockets < MIN_SOCKETS_REQD Then
    sMsg = "此应用程序至少需要 "
    sMsg = sMsg & Trim$(Str$(MIN_SOCKETS_REQD)) & " 个受支持的套接字。"
    MsgBox sMsg, vbOKOnly, "VB4032-ICMPEcho"
    End
End If
MaxSockets = WSAData.iMaxSockets
If MaxSockets < 0 Then
    MaxSockets = 65536 + MaxSockets
End If
MaxUDP = WSAData.iMaxUdpDg
If MaxUDP < 0 Then
    MaxUDP = 65536 + MaxUDP
End If
description = ""
For i = 0 To WSATYPEDESC_LEN
    If WSADATA.szDescription(i) = 0 Then Exit For
    description = description + Chr$(WSADATA.szDescription(i))
Next i
Status = ""
For i = 0 To WSATYPESTATUS_LEN
    If WSADATA.szSystemStatus(i) = 0 Then Exit For
    Status = Status + Chr$(WSADATA.szSystemStatus(i))
Next i
End Sub

Private Sub Command1_Click()
    Text3.Text = ""
    vbWSAStartup                ' 初始化 Winsock
    If Len(Text1.Text) = 0 Then
        vbGetHostName
    End If
    If Text1.Text = "" Then
        MsgBox "未指定主机名！", vbOKOnly, "VB4032-ICMPEcho"
        ' 如果未识别出主机名则发出警告
        vbWSACleanup
        Exit Sub
    End If
    vbGetHostByName             ' 获取主机的 IPAddress
    vbIcmpCreateFile            ' 获取 ICMP 句柄
    ' 以下代码确定 ICMPEcho 的 TTL
    If IsNumeric(Text2.Text) Then
        If (Val(Text2.Text) > 255) Then Text2.Text = "255"
        If (Val(Text2.Text) < 2) Then Text2.Text = "2"
    Else
        Text2.Text = "255"
    End If
    pIPo.TTL = Trim$(Text2.Text)
    vbIcmpSendEcho              ' 发送 ICMP 回显请求
    vbIcmpCloseHandle           ' 关闭 ICMP 句柄
    vbWSACleanup                ' 关闭 Winsock
End Sub

Private Sub Command2_Click()
    Text3.Text = ""
End Sub

Private Sub Command3_Click()
    Text3.Text = ""
    vbWSAStartup                ' 初始化 Winsock
    If Len(Text1.Text) = 0 Then
        vbGetHostName
    End If
    If Text1.Text = "" Then
        MsgBox "未指定主机名！", vbOKOnly, "VB4032-ICMPEcho"
        ' 如果未识别出主机名则发出警告
        vbWSACleanup
        Exit Sub
    End If
    vbGetHostByName             ' 获取主机的 IPAddress
    vbIcmpCreateFile            ' 获取 ICMP 句柄
    ' 以下代码确定 TRACE 功能中 ICMPEcho 的 TTL
    TraceRT = True
    Text3.Text = Text3.Text + "Tracing Route to " + Label3.Caption + ":" + Chr$(13) + Chr$(10) + Chr$(13) + Chr$(10)
    For TTL = 2 To 255
        pIPo.TTL = TTL
        vbIcmpSendEcho          ' 发送 ICMP 回显请求
        DoEvents
        If RespondingHost = Label3.Caption Then
            Text3.Text = Text3.Text + Chr$(13) + Chr$(10) + "Route Trace has Completed" + Chr$(13) + Chr$(10) + Chr$(13) + Chr$(10)
            Exit For            ' 停止 TraceRT
        End If
    Next TTL
    TraceRT = False
    vbIcmpCloseHandle           ' 关闭 ICMP 句柄
    vbWSACleanup                ' 关闭 Winsock
End Sub
```

## ICMP.bas

```vb
Type Inet_address
    Byte4 As String * 1
    Byte3 As String * 1
    Byte2 As String * 1
    Byte1 As String * 1
End Type
Public iPLong As Inet_address

Type WSADATA
    WVersion As Integer
    wHighVersion As Integer
    szDescription(0 To 255) As Byte
    szSystemStatus(0 To 128) As Byte
    iMaxSockets As Integer
    iMaxUdpDg As Integer
    lpVendorInfo As Long
End Type

Type Hostent
    h_name As Long
    h_aliases As Long
    h_addrtype As Integer
    h_length As Integer
    h_addr_list As Long
End Type

Type IP_OPTION_INFORMATION
    TTL As Byte          ' 生存时间（用于 traceroute）
    Tos As Byte          ' 服务类型（通常为 0）
    Flags As Byte        ' IP 头标志（通常为 0）
    OptionsSize As Long  ' 选项数据大小（通常为 0，最大 40）
    OptionsData As String * 128 ' 选项数据缓冲区
End Type

Public pIPo As IP_OPTION_INFORMATION

Type IP_ECHO_REPLY
    Address(0 To 3) As Byte       ' 响应地址
    Status As Long                ' 响应状态
    RoundTripTime As Long         ' 往返时间（毫秒）
    DataSize As Integer           ' 响应数据大小
    Reserved As Integer           ' 供系统使用
    data As Long                  ' 指向回显数据的指针
    Options As IP_OPTION_INFORMATION ' 响应选项
End Type

Public pIpe As IP_ECHO_REPLY

Declare Function gethostname Lib "ws2_32.dll" (ByVal hostname$, HostLen&) As Long
Declare Function gethostbyname Lib "ws2_32.dll" (ByVal hostname$) As Long
Declare Function WSAGetLastError Lib "ws2_32.dll" () As Long
Declare Function WSAStartup Lib "ws2_32.dll" (ByVal wVersionRequired&, lpWSAData As WSAData) As Long
Declare Function WSACleanup Lib "ws2_32.dll" () As Long
Declare Sub CopyMemory Lib "kernel32" Alias "RtlMoveMemory" (hpvDest As Any, hpvSource As Any, ByVal cbCopy As Long)
Declare Function IcmpCreateFile Lib "icmp.dll" () As Long
Declare Function IcmpCloseHandle Lib "icmp.dll" (ByVal HANDLE As Long) As Boolean
Declare Function IcmpSendEcho Lib "icmp.dll" (ByVal IcmpHandle As Long, ByVal DestAddress As Long, ByVal RequestData As String, ByVal RequestSize As Integer, RequestOpts As IP_OPTION_INFORMATION, ReplyBuffer As IP_ECHO_REPLY, ByVal ReplySize As Long, ByVal TimeOut As Long) As Boolean
```

## 拒绝服务攻击

**概要：** SmartSwitch 路由器 (SSR) 中存在一个 DoS 漏洞。

**入侵状态：** 通过洪泛进行干扰处理。

**脆弱性：** 运行 2.x 固件版本的 SSR 8000。

**突破：** 此瓶颈似乎出现在 SSR 的 ARP 处理机制中。发送大量 ARP 请求会限制 SSR，导致路由器停止处理。匿名攻击者通过定制诸如 icmp.c（可从本书 CD 上的 Tiger Tools 仓库获取）等程序来使 SSR 崩溃。

## 思科

在接入路由器市场顶端，思科（www.cisco.com）是全球互联网互连的领导者，为小型、中型和大型办公室及 ISP 提供模块化和多服务接入平台产品线。思科是大约 115 个国家的供应商，这些地区由直接销售团队、分销商、增值经销商和系统集成商提供服务。思科还托管了互联网上最大的电子商务站点之一，占整体订单交易量的 90%。这些接入产品为数据、语音、视频、拨入接入、VPN 以及多协议 LAN 到 LAN 路由提供了解决方案。凭借高性能的模块化架构，思科已将多个设备的功能集成到一个安全、可管理的单一解决方案中。

## 劣势

### 通用拒绝服务攻击

**概要：** 思科系列接入产品中存在 DoS 漏洞。

**入侵状态：** 未经授权访问和/或系统崩溃。

**脆弱性：** 以下产品：

- AS5200、AS5300 和 AS5800 系列接入服务器
- 7200 和 7500 系列路由器
- uxr7200 系列电缆路由器
- 7100 系列路由器
- 3660 系列路由器
- 4000 和 2500 系列路由器
- SC3640 系统控制器
- AS5800 系列语音网关产品
- AccessPath LS-3、TS-3 和 VS-3 接入解决方案产品

