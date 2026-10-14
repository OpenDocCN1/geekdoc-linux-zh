
| Pid | Process | Base | LoadIn | InInit | Mem | MappedPage |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1928 | lsass.exe | 0x7c900000 | True | True | | WINDOWS\system32\ntdll.dll |
| 1928 | lsass.exe | 0x77f60000 | True | True | | WINDOWS\system32\shlwapi.dll |
| 1928 | lsass.exe | 0x77b10000 | True | True | | WINDOWS\system32\wininet.dll |
| 1928 | lsass.exe | 0x77c00000 | True | True | | WINDOWS\system32\version.dll |
| 1928 | lsass.exe | 0x01000000 | False | True | | `<name>` |

由于 `lsass.exe` 被取消映射，内存不再与 `0x01000000` 区域关联。由于 `lsass.exe` 被取消映射，内存不再与 `0x01000000` 区域关联。

# Hunting Malware in Process Memory 261

# 266 第二部分：Windows 内存取证

- **进程事件日志**：学习何时仅使用 Volatility 从内存中解析记录，以及何时提取事件日志并使用外部工具进行分析。
- **检测暴力破解日志**：学习如何通过分析事件日志中的失败消息来识别暴力破解登录尝试。
- **识别后门**：检测防火墙策略的更改和服务器端口冲突，这些可能预示着后门活动。
- **识别被清除的事件日志**：学习当事件日志被清除时会发生什么，以及如何判断恶意代码或攻击者是否尝试清除日志。

### 数据结构

输出显示了 Windows XP 和 2003 事件日志结构中特定成员的属性。Harlan Carvey 也曾在他的博客上记录了事件日志结构（http://windowsier.blogspot.com/2007/06/eventlog-analysis.html）。`EVTLogHeader` 是作为日志日志头的结构，而 `EVTRecordStruct` 是单个记录的结构。

```
dt("EVTLogHeader")
```

`'EVTLogHeader' (48 bytes)`

0x0 : `HeaderSize`             [`unsigned int'`]

0x4 : `Magic`                  [`'int'`]

0x10 : `OffsetDist`            [`'unsigned int'`]

0x14 : `OffsetNextToWrite`      [`'unsigned int'`]

0x18 : `NextID`                 [`'int'`]

0x1c : `OldestID`               [`'int'`]

0x20 : `MaxSize`               [`'unsigned int'`]

0x28 : `ExtensionTime`         [`'int'`]

0x2c : `RecordSize`            [`'unsigned int'`]

```
dt("EVTRecordStruct")
```

`'EVTRecordStruct' (56 bytes)`

0x0 : `RecordLength`         [`'unsigned int'`]

0x4 : `Magic`                [`'int'`]

0x8 : `RecordNumber`         [`'int'`]

0xc : `TimeGenerated`        [`'UnixTimeStamp'`, `{'is_utc': True}`]

0x10 : `TimeWritten`         [`'UnixTimeStamp'`, `{'is_utc': True}`]

0x14 : `EventID`              [`'unsigned short'`]

0x18 : `EventType`            [`'Enumeration'`, [snip]

0x1a : `NumStrings`          [`'unsigned short'`]

[snip]

### 关键点

关键点如下：

- **OldestID**：文件中最早的事件日志记录的 ID。

# 事件日志 267

- **Magic**：事件日志及其记录的签名。该签名是 `LfLe`。
- **NextID**：将写入的事件日志记录的 ID。
- **RecordLength**：事件日志记录的长度，根据记录而异，因为每种类型的消息都有对应的消息字符串。
- **RecordNumber**：事件日志内部记录的 ID。
- **TimeGenerated**：显示事件生成时间的时间戳（UTC）。
- **TimeWritten**：显示事件记录写入时间的时间戳（UTC）。
- **EventID**：描述发生了什么类型事件的 ID。
- **NumStrings**：记录中包含的消息数量，有助于描述事件。你可能需要相应的消息模板来正确解释字符串的含义。有关如何查找模板的更多信息，请参阅章节末尾“Windows 2000, XP 和 2003 事件日志”部分的注释。

# Windows 2000, XP, 和 2003 事件日志

在 Windows 2000、XP 和 2003 中，事件日志具有相同的二进制记录格式。默认日志包括 Application、System 和 Security，这些日志在磁盘上的默认存储位置为 `%systemroot%\system32\config`。这些日志也映射在 `services.exe` 进程的地址空间中。

# 查找事件日志文件

可以通过搜索 `services.exe` 进程并搜索事件日志名称（扩展名为 `.Evt`）来确定哪个内存段持有数据，如下所示：

```
$ python vol.py -f XPS3.vmem --profile=WinXSP3x86 plist | grep services
```

Volatility Volatility Framework 2.4

0x81d97020 services.exe 692 648 16 352 0 2010-12-27 21:34:32

```
$ python vol.py -f XPS3.vmem --profile=WinXSP3x86 vadinfo -p 692
```

[snip]

VAD node @82032fa40 Start 0x09c00000 End 0x09ffff Tag

Flags: 4 Protection: PAGE_READWRITE

ControlArea@82040f50 Dereference list: 0000000 0000000

NumberOfSectionReferences: 1 NumberOffnReferences: 1

NumberOfMappedViews: 2 NumberOfUserReferences: 2

WaitForDeletion: 0000000 Control: 1, File: 1

FileObject @82040ed8, Name:\system32\config\Event.Evt

# 268 第二部分：Windows 内存取证

你现在知道如何在内存中找到事件日志，但接下来要做什么？你可以转储 VAD 段并使用 Volatility 等工具进行解析，但你也可以直接从内存中解析事件日志。

注意 Windows XP/2003 事件日志有最大限制，并被视为环形缓冲区。这意味着当达到最大限制时，指向日志的指针将回到最早记录并用新数据覆盖它。这种方法可能会破坏某些工具，因为部分记录可能会损坏工具预期看到的内容——日志文件的块可能不可。

# 提取事件日志

`evlogs` 插件（仅限 Windows XP 和 2003）会自动查找并解析每条记录。该插件通过寻找 `services.exe` 进程并在内存中搜索事件日志，然后使用本章开头定义的结构解析每条记录。如果你想使用 Volatility 等外部工具处理原始日志，`evlogs` 插件还有一个转储原始日志的选项。以下显示了针对包含嵌入 Flash 漏洞的 Word 文档公共内存样本（http://persecurus.blogspot.com/2011/04/using-volatility-to-study-cve-2011-0611.html）后运行该插件的输出示例：

```
$ vol.py -f cve2011_0611.d --profile=WindowsXP386 evlogs -v -save -d output/
```

Volatility Foundation Framework 2.4

Saved .evt file to omission.evt
