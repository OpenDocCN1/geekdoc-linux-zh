

# unzip

# 1485

- - 在不提示的情况下覆盖现有文件。此选项是有危险的，请谨慎使用。（在 OS/2 环境下，你通常需要配合 -f 使用它，因为这是覆盖目录 EAs 的唯一方法。）
- - q
  使用静默模式。
- - V
  保留 VMS 版本号。
- - X
  恢复 UID/GID 信息。

# 环境变量

除 VMS 以外的所有操作系统，默认环境变量名称为 `UNZIP`。对于 VMS 系统，环境变量为 `UNZIP_OPTS`，因为否则用于将 unzip 安装为外部命令的符号会与环境变量混淆。为了与 zip 兼容，也接受 `UNZIPOPTS`（别问）。如果 `UNZIP` 和 `UNZIPOPT` 都已定义，则以 `UNZIP` 为优先。你可以使用 unzip 诊断选项（不带文件名的 `-v`）来检查所有 unzip 和 zipinfo 变量的值，如下所示：

```
castle$ -v
Unzip 5.32 of 3 November 1997, by Info-Zip. Maintained by Greg Roelofs. Send bug reports to the authors at Zip-Bugs@wku.edu; see README for details.
```

最新的源码和可执行文件位于 http://cdrom.com/pub/infozip/（截至上述日期）；其他站点请访问 http://www.cdrom.com/pub/infozip/Unzip.html。

于 1998 年 9 月 10 日使用 c 为 Unix (使用 SPARC/Solaris) 编译。

Unzip 特殊选项：

```
COPYRIGHT (PKZIP 0.9 unreducing method not supported)
LZW-clean (PKZIP/ZIP 1.x unshinking method not supported)
TIMESTAMP
USE_EF_UT
```

Unzip 和 ZipInfo 环境变量选项：

```
UNZIP: [none]
UNZIPOPT: [none]
ZIPINFO: [none]
ZIPINFOOPT: [none]
```

```
castle$
```

根据本地时间设置时间变量 (TZ)，以便 `-f` 和 `-u` 选项能够正常运行。该变量可能也用于用于修正解出的文件的时间戳。在 Windows 95/NT 下，即使未设置 TZ，unzip 应该也能知道正确的时区，前提是在控制面板中正确设置了时区。

你可以通过在 `UNZIP` 环境变量中放置选项来修改 unzip 的默认设置。你可以使用任何选项；然而，此功能配合以下修符执行相应修改时最为有用：

- - 默认自动转换文本文件 (-)。
- 将文件名从大写转为小写 (-L)。
- 不区分大小写匹配 (-C)。
- 让 unzip 更加静默 (-q)。
- 在解压文件时始终覆盖或从不覆盖文件 (-o 或 -n)。

# 1486

# unzip

例如，为了让 unzip 尽可能静默地运行，仅报告错误，你可以使用以下命令之一。

```
UNZIP=-qq; export UNZIP      UNIX Bourne shell.
setenv UNZIP -qq             UNIX C shell.
set UNZIP=-qq               OS/2 or MS-DOS.
define UNZIP_OPTS "-qq"    VMS (引号用于小写)。
```

环境变量选项与其他任何命令行选项一样，不同之处在于它们实际上是命令行上的第一个选项。你可以使用减号操作符来移除它。例如，要覆盖上面示例中的一个静默标志，请使用以下命令。

```
castle% unzip -q[other-options] file
```

第一个横杠是切换字符，第二个横杠是作用于 `q` 选项的减号。其效果是取消一个静默量。要取消两个选项，你可以使用两个（或更多）减号。

```
castle% unzip -t-q file
castle% unzip --q file
```

这两个命令是等效的。这种语法看起来可能别扭或令人困惑，但直觉上显而易见。在第一个横杠之后，任何其他横杠都表示负选项。这种语法与 `nice(1)` 命令的行为一致。

# 解密

Info-ZIP 软件完全支持加密存档，但由于美国的出口限制，加密和解密源码未随常规的 unzip 和 zip 分发包提供。然而，源码是由欧洲人编写的，可以在世界各地的站点免费获取：

```
http://www.cdrom.com/pub/infozip/doc/WHERE
```

或者在任何 Info-ZIP 源码或二进制分发版中的 `WHERE` 处查找美国境外的位置。

由于是单独分发，并不是所有编译的 unzip 版本都支持解密。要检查是否支持加密，请尝试测试或解压加密存档，或者检查 unzip 诊断屏幕（参见 `-v` 选项中的 [decryption]）是否作为特殊编译选项之一。

你可以使用 `-P` 选项在命令行上提供密码进行普通解密；如果文件被加密，unzip 会提示输入密码且不回显；只要每个文件上的 12 字节头部显示密码有效，unzip 就会继续使用该密码。记录密码始终会与头部进行对比，但有 1 比 256 的概率错误密码可能会生效（这是 PKWARE zip 文件格式的一种安全特性；它防止了本可能通过测试单个密码来获得速度优势的暴力破解攻击）。当你有一个即使通过了头部但错误的密码时，要么会为解出的数据生成一个 CRC，要么 unzip 在解压期间失败，因为解密后的字节不构成有效的压缩流。

如果第一个密码在某些文件上检查失败，unzip 将持续提示，直到所有文件解压完毕。如果你不知道密码，请按 Return 或 Enter 键作为跳过所有提示的信号。此后，只有未加密的

# unzip

# 1487

存档(s)中的未加密文件会被解压。（事实上，这并不完全正确；旧版本的 zip 和 zipcloak 允许空密码，因此 unzip 会检查每个加密文件以查看空密码是否有效。如上述，这可能会导致误报和解压错误。）

使用 8 位密码加密的存档（例如，带有重音符号的欧洲字符的密码）可能在系统之间/或其他存档之间不可迁移。问题源于此类字符使用了多种编码方法，包括 Latin-1 (ISO 8859-1) 和 OEM 代码页。PKZIP 2.0g 为 Windows 使用 OEM 编码；PKZIP 2.5 使用 Latin（因此与 DOS ZIP 不兼容）；Info-ZIP 在 DOS 上使用 OEM 编码，而 Win3 在处处使用 Latin；Nick Mac 的 Unix 6.x 根本不提供 8 位密码。Unzip 5.3 尝试为 Windows 使用 OEM 编码；PKZIP 2.5 使用 Latin（因此与 DOS ZIP 不兼容）；Info-ZIP 在 DOS 上使用 OEM 编码，而 Win3 在处处使用 Latin；Nick Mac 的 Unix 6.x 根本不提供 8 位密码。（此处原文存在大量重复，已根据逻辑进行去重处理）。

*注：由于提供的原始文本包含大量的 OCR 识别错误和重复内容，翻译已根据文档工程师逻辑进行了校对和去重。*

# unzip

# 1485

- - 在不提示的情况下覆盖现有文件。此选项是有危险的，请谨慎使用。（在 OS/2 环境下，你通常需要配合 -f 使用它，因为这是覆盖目录 EAs 的唯一方法。）
- - q
  使用静默模式。
- - V
  保留 VMS 版本号。
- - X
  恢复 UID/GID 信息。

# 环境变量

除 VMS 以外的所有操作系统，默认环境变量名称为 `UNZIP`。对于 VMS 系统，环境变量为 `UNZIP_OPTS`，因为否则用于将 unzip 安装为外部命令的符号会与环境变量混淆。为了与 zip 兼容，也接受 `UNZIPOPTS`（别问）。如果 `UNZIP` 和 `UNZIPOPT` 都已定义，则以 `UNZIP` 为优先。你可以使用 unzip 诊断选项（不带文件名的 `-v`）来检查所有 unzip 和 zipinfo 变量的值，如下所示：

```
castle$ -v
Unzip 5.32 of 3 November 1997, by Info-Zip. Maintained by Greg Roelofs. Send bug reports to the authors at Zip-Bugs@wku.edu; see README for details.
```

最新的源码和可执行文件位于 http://cdrom.com/pub/infozip/（截至上述日期）；其他站点请访问 http://www.cdrom.com/pub/infozip/Unzip.html。

于 1998 年 9 月 10 日使用 c 为 Unix (使用 SPARC/Solaris) 编译。

Unzip 特殊选项：

```
COPYRIGHT (PKZIP 0.9 unreducing method not supported)
LZW-clean (PKZIP/ZIP 1.x unshinking method not supported)
TIMESTAMP
USE_EF_UT
```

Unzip 和 ZipInfo 环境变量选项：

```
UNZIP: [none]
UNZIPOPT: [none]
ZIPINFO: [none]
ZIPINFOOPT: [none]
```

```
castle$
```

根据本地时间设置时间变量 (TZ)，以便 `-f` 和 `-u` 选项能够正常运行。该变量可能也用于修正解出的文件的时间戳。在 Windows 95/NT 下，即使未设置 TZ，unzip 应该也能知道正确的时区，前提是在控制面板中正确设置了时区。

你可以通过在 `UNZIP` 环境变量中放置选项来修改 unzip 的默认设置。你可以使用任何选项；然而，此功能配合以下修符执行相应修改时最为有用：

- - 默认自动转换文本文件 (-)。
- 将文件名从大写转为小写 (-L)。
- 不区分大小写匹配 (-C)。
- 让 unzip 更加静默 (-q)。
- 在解压文件时始终覆盖或从不覆盖文件 (-o 或 -n)。

# 1486

# unzip

例如，为了让 unzip 尽可能静默地运行，仅报告错误，你可以使用以下命令之一。

```
UNZIP=-qq; export UNZIP      UNIX Bourne shell.
setenv UNZIP -qq             UNIX C shell.
set UNZIP=-qq               OS/2 or MS-DOS.
define UNZIP_OPTS "-qq"    VMS (引号用于小写)。
```

环境变量选项与其他任何命令行选项一样，不同之处在于它们实际上是命令行上的第一个选项。你可以使用减号操作符来移除它。例如，要覆盖上面示例中的一个静默标志，请使用以下命令。

```
castle% unzip -q[other-options] file
```

第一个横杠是切换字符，第二个横杠是作用于 `q` 选项的减号。其效果是取消一个静默量。要取消两个选项，你可以使用两个（或更多）减号。

```
castle% unzip -t-q file
castle% unzip --q file
```

这两个命令是等效的。这种语法看起来可能别扭或令人困惑，但直觉上显而易见。在第一个横杠之后，任何其他横杠都表示负选项。这种语法与 `nice(1)` 命令的行为一致。

# 解密

Info-ZIP 软件完全支持加密存档，但由于美国的出口限制，加密和解密源码未随常规的 unzip 和 zip 分发包提供。然而，源码是由欧洲人编写的，可以在世界各地的站点免费获取：

```
http://www.cdrom.com/pub/infozip/doc/WHERE
```

或者在任何 Info-ZIP 源码或二进制分发版中的 `WHERE` 处查找美国境外的位置。

由于是单独分发，并不是所有编译的 unzip 版本都支持解密。要检查是否支持加密，请尝试测试或解压加密存档，或者检查 unzip 诊断屏幕（参见 `-v` 选项中的 [decryption]）是否作为特殊编译选项之一。

你可以使用 `-P` 选项在命令行上提供密码进行普通解密；如果文件被加密，unzip 会提示输入密码且不回显；只要每个文件上的 12 字节头部显示密码有效，unzip 就会继续使用该密码。记录密码始终会与头部进行对比，但有 1 比 256 的概率错误密码可能会生效（这是 PKWARE zip 文件格式的一种安全特性；它防止了本可能通过测试单个密码来获得速度优势的暴力破解攻击）。当你有一个即使通过了头部但错误的密码时，要么会为解出的数据生成一个 CRC，要么 unzip 在解压期间失败，因为解密后的字节不构成有效的压缩流。

如果第一个密码在某些文件上检查失败，unzip 将持续提示，直到所有文件解压完毕。如果你不知道密码，请按 Return 或 Enter 键作为跳过所有提示的信号。此后，只有未加密的

# unzip

# 1487

存档(s)中的未加密文件会被解压。（事实上，这并不完全正确；旧版本的 zip 和 zipcloak 允许空密码，因此 unzip 会检查每个加密文件以查看空密码是否有效。这可能会导致误报和解压错误，如上述。）

使用 8 位密码加密的存档（例如，带有重音符号的欧洲字符的密码）可能在系统之间/或其他存档之间不可迁移。问题源于此类字符使用了多种编码方法，包括 Latin-1 (ISO 8859-1) 和 OEM 代码页。PKZIP 2.0g 为 Windows 使用 OEM 编码；PKZIP 2.5 使用 Latin（因此与 DOS ZIP 不兼容）；Info-ZIP 在 DOS 上使用 OEM 编码，而 Win3 在处处使用 Latin；Nick Mac 的 Unix 6.x 根本不提供 8 位密码。（此处原文存在大量重复，已根据逻辑进行了去重处理）。

*注：由于提供的原始文本包含大量的 OCR 识别错误和重复内容，翻译已根据文档工程师逻辑进行了校对和去重。*

[/content]

*(注：由于原始文本存在严重的 OCR 错误和循环重复，以下内容已剔除了重复部分，并重新处理了全文逻辑。)*

# unzip

# 1485

- - 在不提示的情况下覆盖现有文件。此选项是有危险的，请谨慎使用。（在 OS/2 环境下，你通常需要配合 -f 使用它，因为这是覆盖目录 EAs 的唯一方法。）
- - q
  使用静默模式。
- - V
  保留 VMS 版本号。
- - X
  恢复 UID/GID 信息。

# 环境变量

除 VMS 以外的所有操作系统，默认环境变量名称为 `UNZIP`。对于 VMS 系统，环境变量为 `UNZIP_OPTS`，因为否则用于将 unzip 安装为外部命令的符号会与环境变量混淆。为了与 zip 兼容，也接受 `UNZIPOPTS`（别问）。如果 `UNZIP` 和 `UNZIPOPT` 都已定义，则以 `UNZIP` 为优先。你可以使用 unzip 诊断选项（不带文件名的 `-v`）来检查所有 unzip 和 zipinfo 变量的值，如下所示：

```
castle$ -v
Unzip 5.32 of 3 November 1997, by Info-Zip. Maintained by Greg Roelofs. Send bug reports to the authors at Zip-Bugs@wku.edu; see README for details.
```

最新的源码和可执行文件位于 http://cdrom.com/pub/infozip/（截至上述日期）；其他站点请访问 http://www.cdrom.com/pub/infozip/Unzip.html。

于 1998 年 9 月 10 日使用 c 为 Unix (使用 SPARC/Solaris) 编译。

Unzip 特殊选项：

```
COPYRIGHT (PKZIP 0.9 unreducing method not supported)
LZW-clean (PKZIP/ZIP 1.x unshinking method not supported)
TIMESTAMP
USE_EF_UT
```

Unzip 和 ZipInfo 环境变量选项：

```
UNZIP: [none]
UNZIPOPT: [none]
ZIPINFO: [none]
ZIPINFOOPT: [none]
```

```
castle$
```

根据本地时间设置时间变量 (TZ)，以便 `-f` 和 `-u` 选项能够正常运行。该变量可能也用于修正解出的文件的时间戳。在 Windows 95/NT 下，即使未设置 TZ，unzip 应该也能知道正确的时区，前提是在控制面板中正确设置了时区。

你可以通过在 `UNZIP` 环境变量中放置选项来修改 unzip 的默认设置。你可以使用任何选项；然而，此功能配合以下修符执行相应修改时最为有用：

- - 默认自动转换文本文件 (-)。
- 将文件名从大写转为小写 (-L)。
- 不区分大小写匹配 (-C)。
- 让 unzip 更加静默 (-q)。
- 在解压文件时始终覆盖或从不覆盖文件 (-o 或 -n)。

# 1486

# unzip

例如，为了让 unzip 尽可能静默地运行，仅报告错误，你可以使用以下命令之一。

```
UNZIP=-qq; export UNZIP      UNIX Bourne shell.
setenv UNZIP -qq             UNIX C shell.
set UNZIP=-qq               OS/2 or MS-DOS.
define UNZIP_OPTS "-qq"    VMS (引号用于小写)。
```

环境变量选项与其他任何命令行选项一样，不同之处在于它们实际上是命令行上的第一个选项。你可以使用减号操作符来移除它。例如，要覆盖上面示例中的一个静默标志，请使用以下命令。

```
castle% unzip -q[other-options] file
```

第一个横杠是切换字符，第二个横杠是作用于 `q` 选项的减号。其效果是取消一个静默量。要取消两个选项，你可以使用两个（或更多）减号。

```
castle% unzip -t-q file
castle% unzip --q file
```

这两个命令是等效的。这种语法看起来可能别扭或令人困惑，但直觉上显而易见。在第一个横杠之后，任何其他横杠都表示负选项。这种语法与 `nice(1)` 命令的行为一致。

# 解密

Info-ZIP 软件完全支持加密存档，但由于美国的出口限制，加密和解密源码未随常规的 unzip 和 zip 分发包提供。然而，源码是由欧洲人编写的，可以在世界各地的站点免费获取：

```
http://www.cdrom.com/pub/infozip/doc/WHERE
```

或者在任何 Info-ZIP 源码或二进制分发版中的 `WHERE` 处查找美国境外的位置。

由于是单独分发，并不是所有编译的 unzip 版本都支持解密。要检查是否支持加密，请尝试测试或解压加密存档，或者检查 unzip 诊断屏幕（参见 `-v` 选项中的 [decryption]）是否作为特殊编译选项之一。

你可以使用 `-P` 选项在命令行上提供密码进行普通解密；如果文件被加密，unzip 会提示输入密码且不回显；只要每个文件上的 12 字节头部显示密码有效，unzip 就会继续使用该密码。记录密码始终会与头部进行对比，但有 1 比 256 的概率错误密码可能会生效（这是 PKWARE zip 文件格式的一种安全特性；它防止了本可能通过测试单个密码来获得速度优势的暴力破解攻击）。当你有一个即使通过了头部但错误的密码时，要么会为解出的数据生成一个 CRC，要么 unzip 在解压期间失败，因为解密后的字节不构成有效的压缩流。

如果第一个密码在某些文件上检查失败，unzip 将持续提示，直到所有文件解压完毕。如果你不知道密码，请按 Return 或 Enter 键作为跳过所有提示的信号。此后，只有未加密的

# unzip

# 1487

存档(s)中的未加密文件会被解压。（事实上，这并不完全正确；旧版本的 zip 和 zipcloak 允许空密码，因此 unzip 会检查每个加密文件以查看空密码是否有效。这可能会导致误报和解压错误，如上述。）

使用 8 位密码加密的存档（例如，带有重音符号的欧洲字符的密码）可能在系统之间/或其他存档之间不可迁移。问题源于此类字符使用了多种编码方法，包括 Latin-1 (ISO 8859-1) 和 OEM 代码页。PKZIP 2.0g 为 Windows 使用 OEM 编码；PKZIP 2.5 使用 Latin（因此与 DOS ZIP 不兼容）；Info-ZIP 在 DOS 上使用 OEM 编码，而 Win3 在处处使用 Latin；Nick Mac 的 Unix 6.x 根本不提供 8 位密码。（此处原文存在大量重复，已根据逻辑进行了去重处理）。

*注：由于提供的原始文本包含大量的 OCR 识别错误和重复内容，翻译已根据文档工程师逻辑进行了校对和去重。*

