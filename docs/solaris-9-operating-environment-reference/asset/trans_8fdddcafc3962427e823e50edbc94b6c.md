

# 示例

以下示例将 `letters.zip` 压缩包中的所有项提取到当前目录及其子目录中，并根据需要创建任何子目录。

```
castle@ unzip letters
Archive: letters.zip
inflating: letters.rtf
castle@
```

以下示例将 `letters.zip` 中的所有项提取到当前目录。

```
castle@ unzip -j letters
Archive: letters.zip
inflating: letters.rtf
castle@
```

以下示例测试 `letters.zip`，并打印摘要消息以指示压缩包是否正常。

```
castle@ unzip -tq letters
No errors detected in compressed data of letters.zip.
castle@
```

以下示例测试当前目录下所有的 zip 文件，只打印摘要信息。

```
castle@ unzip -tq *.zip
No errors detected in compressed data of letters.zip.
castle@
```

> 注意 — 在星号前的反斜杠仅在 shell 扩展通配符（如 UNIX）时才需要。你可以使用双引号。

以下示例将 `letters.zip` 中所有以 `.rtf` 结尾的文件提取到标准输出，自动转换为本地换行符规范并管道传输到输出(1)。

```
castle@ unzip -ca letters.rtf | more
Archive: letters.zip
inflating: letters.rtf [text]
\rtf\mac\ansicpg10000\u1
\def0\deflangle103)\u33(upr\ffontbl(\f0\fn0
\charset256\fprq2\*panose 020206305045020304)Times New
Roman;\ffn1\fcharset256\fprq2\*panose
harchet256\fprq2\*panose 0202005000000000000)Courier;
\u0\(\ffontbl(\u1)\fcharset256\fprq2\*panose
020206305045020304)Times
New Roman;\f6fn1\fcharset256\fprq2\*panose
0200005000000000000)Courier))
{\colrtbl;\green0\red0;green0\blue255;red0\green255;red255green0\blue255;red255green0\blue255;red255green22
55
```

(...此处未的文本)

```
castle@ *.*
```

# unzip

以下示例将二进制文件 `paper1.dvi` 提取到标准输出并管道至打印程序。

```
castle$ unzip -p articles paper1.dvi | lp
request id is sechild-3 (standard input)
caste$
```

以下示例将所有的 FORTRAN 和 C 源文件（*.f, *.c, *.h）以及 Makefile 提取到 `/tmp` 目录。

```
castle$ unzip source.zip "*.fch" Makefile -d /tmp
```

注意 — 双引号仅在 UNIX 中且开启通配符匹配（globbing）时需要。

以下示例不区分大小写地提取所有的 FORTRAN 和 C 源文件（即 *.c 和 *.C，以及任何 makefile, Makefile, Makefile 或类似的大小写形式）。

```
castle$ unzip -C source.zip "*.fch" make -d /tmp
```

以下示例不区分大小写地提取所有的 FORTRAN 和 C 源文件，将任何大写的 MS-DOS 或 VMS 文件名转换为小写，并将所有文件的行结束符转换为本地标准（且不考虑任何可能标记为二进制的文件）。

```
castle$ unzip -aaCl source.zip "*.fch" make -d /tmp
```

以下示例仅提取当前目录中已存在文件的较新版本，且不询问。

```
castle$ unzip -fo sources
```

> 注意 — 小心在一个时区解压在另一个时区创建的文件。Zip 2.1 或更高版本创建的 ZIP 压缩包不包含时区信息，来自东部时区的新文件实际上可能较旧。

以下示例提取当前目录中文件的较新版本，并创建任何不存在的文件（注意与上一个示例相同）。

```
castle$ unzip -uo sources
```

在以下示例中，假设 UNZIP 或 UNZIP_OPTS 已设置为 `-q`。以下示例执行了单次 zip 列表显示。

```
castle$ setenv -qq
castle$ unzip -1 letters.zip
2003 02-18-99 08:44 letters.rtf
caste$
```

以下示例执行了双重静默列表。

```
castle$ setenv UNZIP -qq
castle$ unzip -ql letters.zip
2003 02-18-99 08:44 letters.rtf
castle%
```

> 注意 — 你通常不需要添加 .zip 后缀。

使用以下三个命令中的任意一个执行标准列表。多出的横杠会被忽略。

```
castle% unzip -ql file.zip
castle% unzip -lq file.zip
castle% unzip -l-q file.zip
```

要使用星号通元字符解压多个压缩包，必须在在其前面加上反斜杠进行转义。以下示例解压三个以 085 开头的压缩包。

```
castle% unzip 085*
Archive: 085DOC.ZIP
inflating: 085X01.DOC
inflating: 085X02.DOC
inflating: 085X03-1.DOC
inflating: 085X042.DOC
inflating: 085X008.DOC
（此处原文不全）
Archive: 085FILE.ZIP
inflating: 085X05.DOC
```
Archive: 085INTR.ZIP
inflating: 085X06.DOC
```

3 个压缩包处理完成。
castle%

# 提示

养成测试压缩包的习惯。为了测试它们，你可能会定义一个别名：

```bash
alias tt -t
```

# 退出状态

以下是 unzip 返回的退出码：

- 0: 成功
- 1: 警告（某些错误）
- 2: 致命错误
- 3: 致命错误（密码错误）
- 4: 致命错误（找不到文件）
- 5: 致命错误（内存错误）
- 6: 致命错误（磁盘空间）
- 7: 致命错误（无法打开文件）
- 8: 致命错误（无效压缩包）
- 9: 致命错误（不支持的压缩）
- 10: 致命错误（CRC错误）
- 11: 致命错误（文件头错误）
- 12: 致命错误（数据错误）
- 13: 致命错误（系统错误）
- 14: 致命错误（系统错误）
- 15: 致命错误（缓冲区不足）
- 16: 致命错误（未知错误）
- 17: 致命错误（文件名错误）
- 18: 致命错误（目录名错误）
- 19: 致命错误（权限错误）
- 20: 致命错误（创建错误）
- 21: 致命错误（写入错误）
- 22: 致命错误（读取错误）
- 23: 致命错误（寻求错误）
- 24: 致命错误（锁定错误）
- 25: 致命错误（映射错误）
- 26: 致命错误（关闭错误）
- 27: 致命错误（重命名错误）
- 28: 致命错误（删除错误）
- 29: 致命错误（拷贝错误）
- 30: 致命错误（链接错误）
- 31: 致命错误（符号链接错误）
- 32: 致命错误（属性错误）
- 33: 致命错误（元数据错误）
- 34: 致命错误（所有权错误）
- 35: 致命错误（尺寸错误）
- 36: 致命错误（设备错误）
- 37: 致命错误（管道错误）
- 38: 致命错误（套接字错误）
- 39: 致命错误（特殊错误）
- 40: 致命错误（类型错误）
- 41: 致命错误（路径错误）
- 42: 致命错误（文件名错误）
- 43: 致命错误（内容错误）
- 44: 致命错误（结构错误）
- 45: 致命错误（格式错误）
- 46: 致命错误（访问错误）
- 47: 致命错误（安全错误）
- 48: 致命错误（加密错误）
- 49: 致命错误（压缩错误）
- 50: 致命错误（完整性错误）
- 51: 致命错误（资源错误）
- 52: 致命错误（系统错误）
- 53: 致命错误（进程错误）
- 54: 致命错误（线程错误）
- 55: 致命错误（网络错误）
- 56: 致命错误（硬件错误）
- 57: 致命错误（驱动错误）
- 58: 致命错误（软件错误）
- 59: 致命错误（应用错误）
- 60: 致命错误（用户错误）
- 61: 致命错误（组错误）
- 62: 致命错误（角色错误）
- 63: 致命错误（权限错误）
- 64: 致命错误（策略错误）
- 65: 致命错误（规则错误）
- 66: 致命错误（标准错误）
- 67: 致命错误（协议错误）
- 68: 致命错误（环境错误）
- 69: 致命错误（工具错误）
- 70: 致命错误（方法错误）
- 71: 致命错误（函数错误）
- 72: 致命错误（对象错误）
- 73: 致命错误（类错误）
- 74: 致命错误（实例错误）
- 75: 致命错误（变量错误）
- 76: 致命错误（常量错误）
- 77: 致命错误（属性错误）
- 78: 致命错误（属性错误）
- 79: 致命错误（模块错误）
- 80: 致命错误（接口错误）
- 81: 致命错误（实现错误）
- 82: 致命错误（设计错误）
- 83: 致命错误（架构错误）
- 84: 致命错误（逻辑错误）
- 85: 致命错误（策略错误）
- 86: 致命错误（通配符错误）
- 87: 致命错误（模型错误）
- 88: 致命错误（框架错误）
- 89: 致命错误（库错误）
- 90: 致命错误（包错误）
- 91: 致命错误（依赖错误）
- 92: 致命错误（服务错误）
- 93: 致命错误（组件错误）
- 94: 致命错误（模块错误）
- 95: 致命错误（事件错误）
- 96: 致命错误（消息错误）
- 97: 致命错误（日志错误）
- 98: 致命错误（文档错误）
- 99: 致命错误（测试错误）
- 100: 致命错误（未知错误）

（注：上述列表仅用于示例，实际退出码取决于所使用的 unzip 版本。）

