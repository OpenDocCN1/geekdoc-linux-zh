
```
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Run
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

# 290 第二部分：Windows 内存取证

针对用户登录：

`HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows`

`HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows\Run`

`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

`HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce`

如需更完整的启动项列表，可以使用 `RegRipper` (`https://code.google.com/p/reggripper/wiki/ASEPs`) 或 Sysinternals 的 `AutoRuns` 工具 (`http://technet.microsoft.com/en-us/sysinternals/bb96902.aspx`)。

> 注意
>
> `HKEY_CURRENT_USER`（大多数情况下为 `HKCU`）指的是特定于用户的注册表。`HKEY_LOCAL_MACHINE`（大多数情况下为 `HKLM`）指的是系统使用的注册表。

下面的输出显示了恶意软件持久化的示例。恶意可执行文件 `C:\Windows\system32\svchost.exe` 每次系统启动时运行。这立即引起了怀疑，因为干净 Windows 上的 `svchost.exe` 可执行文件——试图混入合 `svchost.exe`（不带“s”）。你不需要为 `HKEY\SOFTWARE` 定义前缀 `-K` 参数，因为它不是注册表路径的一部分，而是用来指示哪个注册表包含该键值（例如，`SOFTWARE` 蜂单元位于本地机器上）。

```
$ python vol.py -f grcoron.raw --profile=WinXP386 printkey
-K 'Microsoft\Windows\CurrentVersion'
Volatility Foundation Volatility Framework 2.4
Legend: (S) Stable (V) Volatile

----------------------------------------------------------------
Registry: \Device\HarddiskVolume1\WINDOWS\system32\config\
Key name: Run (S)
Last updated: 2012-04-28 01:59:22 UTC+0000

Subkeys:
(S) OptionalComponents

Values:
Adobe Reader Speed Launcher :
REG_SZ (S) "C:\Program Files\Adobe Reader 9.0\Reader\Reader_sl.exe"
Adobe ARM
REG_SZ (S) "C:\Program Files\Common Files\Adobe\ARM\1.0\AdobeARM.exe"
svchost =
(S) C:\WINDOWS\system32\svchost.exe
```

# 内存中的注册表 291

以下输出显示了用户登录时的持久化示例。在这种情况下，我们感兴趣的程序是一个键盘记录器，每当用户 Andrew（如注册表路径所示）登录系统时，该程序就会运行。注意 `printkey` 接收的是 `HKCU` 之后的整个路径：

```
$ python.py -f mswint --profile=Win7Sp1x4 printkey
- K "SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\RUN"
Volatility Foundation Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile
```

Registry: `\C:\Users\Andrew\ntuser.dat`

Key name: Run (S)

Last updated: 2013-03-10 22:47:09 UTC+0000

Subkeys:

Values:

REG_SZ (S) "C:\Users\Andrew\Desktop\mswint.exe"

--logfile.txt --encryption-index=4

恶意软件经常使用的另一种持久化方法是创建服务。当服务被创建时，注册表（特别是 `HKLM\SYSTEM\CurrentControlSet\Services`）会被修改以包含有关服务的信息。你可以打印此键并判断某个服务名称是否异常可疑。如果你像第 B8 章讨论的那样使用时间线，并检查服务注册表键，你可以根据最后写入时间快速识别出新添加的服务。以下是来自内存样本的输出，展示了这种持久化：

```
$ vol.py -f mswint.vexmem --profile=WinXSP386 printkey
- K "ControlSet01\services\MRNet"
Volatility Foundation Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile
```

Registry: `\Device\HardDiskVolume1\WINDOWS\system32\config\system`
Key name: MRNet (S)
Last updated: 2011-06-03 24:46:47 UTC+0000

Subkeys:
(S) Enum

| | Description | | | |
| --- | --- | --- | --- | --- |
| REG_SZ | DisplayName | : (S) | MRNET |
| REG_SZ | | (S) | MRNET |
| REG_DWORD | ErrorControl | : (S) | 0 |
| REG_SZ | Group | : (S) | Network |
| REG_SZ | ImagePath | : (S) | C:\WINDOWS\system32\Drivers\mrxnet.sys |
| REG_DWORD | Start | : (S) | 1 |
| REG_DWORD | Type | : (S) | 1 |

# 292 第二部分：Windows 内存取证

## 你可以通过查询以下 键获取 CurrentControlSet：

```
$ vol.py -f XPSSx86.vmem --profile=WinXSP386 printkey
-K currentcontrolset
```

Volatility Volatility Framework 2.4
Legend: (S) = Stable (V) = Volatile

```
--------------------------------
Registry: \HardDiskVolume1\WINDOWS\system32\config\system
Key name: CurrentControlSet (V)
Last updated: 2010-10-29 17:08:47 UTC+0000
```

Subkeys:
Values:
REG_SZ SymbolicLink (V) `\Registry\ControlSet01`

这一点很重要，因为可能有包含不同配置的集合（见 `http://support.microsoft.com/kb/1001`）。如果你使用了错误的集合，可能看不到当前的配置。虽然 `printkey` 插件很有用，但它只打印原始键，这对于整数或字符串值可以，但对于包含二进制数据的键（例如 `UserAssist` 键）是不够的。这些键在显示之前需要一些额外的十六进制处理。此外，`printkey` 插件一次只检查一个键。由于这些原因，创建了 Volatility Registry API。

## Volatility Registry API

Registry API 设计用于轻松处理复杂的或多个键。例如，可以使用它自动检查启动键，并根据最后写入时间进行排序。在下面的代码中，我们展示了如何从 `volshell` 插件导入并实例化 Registry API：

```
>>> import volatility.plugins.registryapi as registryapi
>>> regapi = registryapi.RegistryApi()
```
