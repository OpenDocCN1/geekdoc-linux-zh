
`USB\VID_1B4F&PID_9208`

为了自动化此过程，你还可以利用日志监控系统来搜索之前提到的值并触发某些警报。

### 58 威胁、漏洞与风险管理

```
ProcessCreationEvents
| where ProcessCommandLine contains "powershell" or
ProcessCommandLine startwith "cmd"
| project ProcessCommandLine, ComputerName, EventTime,
ReportID, MachineID
| join kind=inner MalPnDevices on ComputerName
| where (Event-PluginTime) between (Omin..10s)
```

你还记得 `WHID` 设备吗？你可以通过设备 ID 添加一行代码来检测该设备：

```
where DeviceID == "@USB_VID_1B4F&PID_9208\HDFG"
```

记住，这种防御机制是基于攻击的可预测性；然而，它存在一些缺陷。在提供的代码中，它会监听接下来 10 秒内是否打开了命令提示符窗口，但如果攻击者在脚本中添加了 11 秒的延迟，你就完蛋了。

如果你想了解更多关于使用 `Windows Defender` 高级威胁防护 (ATP) 的额外安全设置，请参阅 `https://docs.microsoft.com/en-us/security/threat-protection/device-control/control-usb-devices-using-intune`。

### DuckHunt

这是一个由 Pedro Sosa 创建的非常酷的脚本，它以非常巧妙的方式解决了上述问题。本质上，他修改了他自己开发的一个按键程序，以便在检测到每次按键后添加一个时间戳。

通过这些信息，你可以判断打字速度，以及打字速度何时高于正常水平（例如，每秒 10 到 20 个字符之间）。然后，系统将将其标记为注入攻击并阻止所有的 `USB HID` 输入。

以下是 `Ducky Script` 攻击的样子：

```
C:\Users\Robin>这是一次脚本攻击，现在我可以以闪电速度注入我的载荷了...AHAHAHA
```

这是 `DuckHunt` 如何停止 `Ducky Script` (`USB HID` 注入) 攻击的示例：

```
C:\Users\Robin>This is a sc_
```
