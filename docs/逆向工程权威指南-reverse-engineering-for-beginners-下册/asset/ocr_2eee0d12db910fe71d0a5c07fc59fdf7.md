# view ntoskrnl.exe - Far 2.0.1807 x64 Administrator

```
C:\IDA\Windows 7 x64\ntoskrnl.exe
0V4 VS_VERSION_INFO ÿ 00400
StringFileInfo � 0040904B0 L-0
ft Corporation N!@FileDescript
tem 1&@FileVersion 6.1.7600.
13-1255) :)@InternalName ntkrn
yright ý Microsoft Corporation
d. B\@0OriginalFilename ntkrnlm
e Microsofto Windowso Operati
tVersion 6.1.7600.16385 D @Va
ation ✦PADDINGXXPADDINGXXXXPADDINGPADDINGPADDINGXXP
```

在IDA的提示信息中，严格采用双字节字符对字符进行编码的编码方式称为Unicode。

例如：

```
.data:0040E000 aHelloWorld:
.data:0040E000 unicode 0, <Hello, world!>
.data:0040E000 dw 0Ah, 0
```

而图57.5所示的是俄语的字符串，它采用的是UTF-16编码方式。

![](bbox=[0.439, 0.592, 0.558, 0.611])