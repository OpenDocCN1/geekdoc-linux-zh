
```
$FILE_NAME
创建：2013-03-11 04:59:52 UTC+0000
修改：2013-03-11 04:59:52 UTC+0000
MFT 更改：2013-03-11 04:59:52 UTC+0000
访问：2013-03-11 04:59:52 UTC+0000
名称/路径：\$Recycle.Bin\S-1-5-21-1131950431-3037184594-1082269-0$I12NGUY.docx

$DATA
00000000: 01000000000000005842000000000000.......XB...
00000010: 00c3b47812ece046103a00350655500.......x...C.:.\U.
00000020: 726000570700027300570049106000.......s.e.r.s..A.n.d
00000030: 72600057070005700054064006500073b0..r.e.w..D.e.s.k.
00000040: 740607f0070005700054064006500073b0..o.p..M.e.r.g.
00000050: 650072002000557000740640065000107400.......e.r..U.p.a.t.
00000060: 65072e0e6400f06037800000000000.......e..d.o.c.k.
```

在输出中你可以看到 `I12NGUY.docx` 文件于 2013-03-11 04:59:52 创建在（回收站）中，其 MFT 驻留数据包含 `Merger Update.docx` 的原始完整路径。如前所述，你也可以提取嵌入的时间戳进行比较。因为这只是一个原始数值，你可以使用 Volatility 将其转换为人类可读格式。

# 翻译嵌入的时间戳

以下示例展示了如何翻译 `$i` 文件中的时间戳。首先，进入插件：

```
$ python vol.py -f Win7SP164.vmem --profile=Win7SP64 volshell
```

接下来，将模块导入 `BufferAddressSpace`，这允许你使用原始数据实例化对象。你可以从 `mftparser` 输出中看到时间戳：

```
>>> import addressspace as addressspace
>>> buffers = addressspace.BufferAddressSpace(self,
      data = b'\x00\xc3\xb4\x78\xe\x01')
```

接下来，从缓冲区地址实例化 `Timestamp`。该对象具有适当的代码转换时间戳并显示为人类可读的时间。在打印值之前，确保设置了正确的时区（此情况下为 UTC）。

```
>>> itime = obj.Object("WinTimeStamp", offset = 0, vm = buffers)
>>> itime.is_utc = True
>>> str(itime)
'2013-03-11 04:39:52 UTC+0000'
```

最后一行将文件大小从十六进制转换为十进制（16984 字节），可以与原始文件大小进行比较：

```
0x42586984
```

通过枚举内存中的 MFT 记录，我们能够发现用户（或某人）访问了敏感文件并试图掩盖踪迹。即使用户在进行取证前清空了回收站，`$I12NGUY.docx` 的 MFT 条目可能仍然存在内存中。

> 注意

> 关于 `$I` 文件格式或利用回收站残留进行取证的更多信息，请参阅 http://www.forensicfocus.com/downloads/forensic-analysis-bin

# 数据泄露案例

Jack Crouch 创建了一个类似 APT 的挑战（https://docs.google.com/id=0B0eJOUKRbRU1USBW），展示了我们在案例中看到的类型。`mftparser` 插件非常有用，因为它显示了攻击者投放了哪些文件以及何时执行。

# 执行证明

当程序在机器上运行时，会创建一个 Prefetch 文件（或更新现有文件）。因此，一个很好的起点是寻找有趣的 Prefetch 文件以证明执行了什么。在后续输出中，针对内存导出运行 `mftparser`，然后通过 `grep` 语句进行过滤。每个语句如下（`-i` 忽略大小写）：

- `grep -i .pf`：返回扩展名为 `.pf` 的文件。

- `grep -i exe`：路径中包含 `exe` 的文件。

- `grep -d|f2`：通过管道 (`|`) 分割并打印第二个字段。

```
$ python vol.py -f mftcon.vmem mftparser --profile=Win7SP164 --output-body --output-file=mftcon_mft.body
```

Volatility Framework 扫描 MFT 条目并构建目录可能需要一些时间，你必须检查输出结果查看是否如下：

```
$ grep -i ".pf" mftcon.mft.body | \
  grep -i exe | \
  cut -d|f2
[MFT FILE_NAME] WINDOWS\Prefetch\EXPLORER.EXE-E2F38A9.pf (Offset: 0x14bc6800)
[MFT FILE_NAME] WINDOWS\Prefetch\SWING-MECHANICS.DOC1.EXE-01CEA10.pf (Offset: 0x14c4200)
[MFT FILE_NAME] WINDOWS\Prefetch\WODEX-1.pf (Offset: 0x1503dc00)
[MFT STD_INFO] WINDOWS\Prefetch\WODEX-1.pf (Offset: 0x1503dc00)
[MFT FILE_NAME] WINDOWS\Prefetch\MDX.EXE-186A9FD3.pf (Offset: 0x1503dc00)
```

你可以看到，输出中的某一行加粗看起来很奇怪。原始文件名 `SWING-MECHANICS.DOC1.exe` 看起来是一个 Word 文档，但实际上是一个执行文件。由于 Windows 默认隐藏扩展名，许多用户可能会误认为文件是 Word 文档，因为只可见 `.doc`。通过搜索其他 Prefetch 文件，你可以找到在 Windows 上未发现的可执行文件证据（如下所示）：

```
[MFT FILE_NAME] WINDOWS\Prefetch\SVCHOST.EXE-6BC8D2.pf (Offset: 0x2330d68)
[MFT FILE_NAME] WINDOWS\Prefetch\R.EXE-19EB34FB.pf (Offset: 0xd0c5430)
[MFT FILE_NAME] WINDOWS\Prefetch\Q.EXE-24B19A8.pf (Offset: 0x1914800)
[MFT FILE_NAME] WINDOWS\Prefetch\P.EXE-0450029.pf (Offset: 0x1b2dd00)
[MFT FILE_NAME] WINDOWS\Prefetch\R.EXE-19EB34FB.pf (Offset: 0x18e2b400)
```

然后你利用这些信息找到这些文件的原始路径。例如所示：

```
$ grep -i r.exe mftcon.mft.body | grep FILE_NAME | cut -d|f2
[MFT FILE_NAME] WINDOWS\Prefetch\R.EXE-19EB34FB.pf (Offset: 0xd6b4400)
[MFT FILE_NAME] WINDOWS\system32\systems\r.exe (Offset: 0x18229400)
```

# 内存中的磁盘残留

> 注意

> Prefetch 文件名中的哈值是基于文件路径的。因为每个可执行文件的哈值都是唯一的（`dllhost.exe` 除外），你可以轻松判断某个 Prefetch 文件是否与磁盘上的特定程序相关。有两个辅助工具：

> - Prefetch 脚本：https://raw.github.com/gleeda/misc/prefetch

> - Perl 脚本：http://www.hexorn.com/blog/2012/06/13

# 伪造 `systems` 目录

你有了路径，并且在 Windows 中没有发现 `systems` 文件夹，这使得文件非常可疑。在后续输出中，你还可以看到另一个用于部署“机密”文件的文件夹 `1`：
