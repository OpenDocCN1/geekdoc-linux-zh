
```
[snip]
2007-02-17 19:19:26 UTC+0000 | `\C:\WINDOWS\system32\lsrastas.exe`
2007-02-17 19:26:19 UTC+0000 | `\C:\WINDOWS\system32\iisreset.exe`
2007-02-17 19:54:00 UTC+0000 | `\C:\WINDOWS\Program Files\Outlook\setup50.exe`
2009-03-08 11:32:52 UTC+0000 | `\C:\WINDOWS\system32\ieinit.exe`
2010-07-22 07:47:49 UTC+0000 | `\C:\XXX\nv.exe`
2010-07-22 08:40:57 UTC+0000 | `\C:\XXX\123.exe`
2010-07-22 07:44:57 UTC+0000 | `\C:\XXX\dl.exe`
2010-07-22 07:46:41 UTC+0000 | `\C:\XXX\ow.exe`
[snip]
2010-02-06 23:45:26 UTC+0000 | `\C:\WINDOWS\PSEXSVC.EXE`
[snip]
2010-01-19 09:21:41 UTC+0000 | `\E:\E\sample.exe`
2010-01-19 09:02:26 UTC+0000 | `\E:\E\X\s.exe`
[snip]
```

> 注意
> 关于 `Shimcache` 的一点是，当键达到最大尺寸时，旧条目会被新条目覆盖（大小随系统而异）。因此，在运行了一时间的机器上，你可能会看到残留数据（类似于硬盘上的空隙）。

## 使用 Shellbags 重构活动

`Shellbags` 是一个常用术语，描述一组允许“Windows 操作系统跟踪特定于窗口偏好”的注册表键

# 内存中的注册表

“Windows 资源管理器”（参见 http://www.dfrws.org/2009/proceedings/p69-zhu.pdf）。这些键包含大量与取证调查相关的丰富信息。你可以包含的示例伪迹包括：

- Windows 尺寸和偏好
- 图标和文件夹视图设置
- 元数据，如 MAC 时间戳（修改、访问、创建时间）
- 最近使用过的（MRU）文件和文件类型（zip、目录、安装程序）
- 系统中曾存在过的文件、文件夹、zip 文件和安装程序（即使已删除）
- 网络共享以及共享内的文件夹
- 与上述任何类型相关的元数据，其中可能包括时间戳和绝对路径
- 关于 TrueCrypt 卷的信息

> 注意
> 有关 Shellbag 数据结构、相应注册表以及及其在取证调查中使用的更多信息，请参考以下资源：
>
> - Harlan Carvey 的 Shellbag 分析：http://windowsisir.blogspot.com/2012/08/shellbag-analysis.html
> - Will Ballentin 的 Windows Shellbag 取证：http://www.willballenthin.com/forensics/shellbags
> - Shellbags 取证：解决误区：http://www.4nk.com/2013/12/shellbags-forensics-addressing.html

# 内存中的 Shellbags

`Volatility` 的 `shellbags` 插件使用注册表 API 从相应的键中提取数据。然后它使用 Shellbag 数据类型解析数据并输出格式化版本，以及 MRU 信息。通过 MRU 详情，你可以将注册表键的最后时间与最后更新的 shellbags 项关联。以下是使用 shellbags 插件的示例：

```
$ python vol.py -f XPSP3.vmem --profile=WinXSP386 shellbags

Volatility Foundation Framework 2.4

Registry:\Device\HarddiskVolume1\Documents and Settings\User\NTUSER.DAT

Key: Software\Microsoft\Windows\ShellNoRoam\BagMRU\0\0
```

最后更新: 2011-06-03 04:24:36
Value: 1
Mru: 0
File Name: DOCUMENT-1
Modified Date: 2010-08-22 17:38:04
Create Date: 2010-08-22 13:32:26
Access Date: 2010-08-26 01:04:52
File Attribute: DIR
Path: C:\Documents and Settings

Value: 0
Mru: 1
File Name: PROGRA-1
Modified Date: 2010-08-25 23:04:02
Create Date: 2010-08-22 13:32:48
Access Date: 2010-08-25 23:04:22
File Attribute: RO, DIR
Path: C:\Program Files

Value: 4
Mru: 2
File Name: WINDOWS
Modified Date: 2010-08-26 00:06:24
Create Date: 2010-08-22 12:29:34
Access Date: 2010-10-08 03:27:40
File Attribute: DIR
Path: C:\WINDOWS

文件被删除后，关于 Shellbags 条目需要注意以下几点：

- 文件删除后，`SHELLITEM` 项仍保留在注册表中。
- 与 `SHELLITEM` 相关的时间戳不会更新，即使文件在稍后的某个时间被修改或访问。
- 如果文件被移动、删除或访问，`ITEMPOS` 项会被更新。
- 如果在获取内存样本时用户未登录系统，则该用户的配置单元（hive）在内存中不可用，因此 Shellbag 数据不会被处理。

# 使用 Shellbags 查找 TrueCrypt 卷

TrueCrypt 卷也出现在 Shellbags 键中，通常以 `ITEMPOS` 项的形式。由于 `ITEMPOS` 项是更新的，如果 TrueCrypt 卷被移动或删除，其项将被更新或移除以反映这些变化。然而，从该卷访问的文件的 Shellbags 项将保持完好。在以下输出中，你可以看到机器在 T 驱动器上挂载了一个 TrueCrypt 卷，并且它在 2012-09-25 11:48:46 被访问过。

```
$ python vol.py -f XPSP3.vmem --profile=WinXSP3x86 shellbags

Volatility Framework 2.4

Registry: \Device\HarddiskVolume\Documents and Settings\user\NTUSER.DAT

Key: \Microsoft\Windows\ShellNoRoam\BagMRU\0

Last updated: 2012-09-25 13:22:43

| Value | Mru | Entry Type | Path |
| :--- | :--- | :--- | :--- |
| 1 | 0 | Volume Name | C:\ |
| 3 | 1 | Volume Name | Z:\ |
| 4 | 2 | Volume Name | T:\ |
```
