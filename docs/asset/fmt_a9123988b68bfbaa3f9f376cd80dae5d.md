
- Windows 字符集是从原始的旧版日语标准（JIS X 0208）扩展而来的，并且没有标准化。这意味着严格标准化的实现无法支持完整的 Windows 字符集。
- 主要出于历史原因，日语中存在几种编码方法，它们之间并不完全兼容。主要有两种编码方法。一种是用于 Windows 和部分 UNIX 系统的 `Shift_JIS` 系列。另一种是用于大多数 UNIX 和 Linux 系统的 `EUC-JP` 系列。此外，Samba 以前还提供了几种名为 `CAP` 和 `HEX` 的独特编码方法，以保持与 `CAP/NetAtalk` 以及无法使用日语文件名的 UNIX 系统的互操作性。`EUC-JP` 系列的一些实现无法支持完整的 Windows 字符集。
- 在 Unicode 和旧版日语字符集之间存在一些代码转换表。一种与 Windows 兼容，另一种基于 Unicode 联盟的参考，还有一些是混合实现。Unicode 联盟并未正式定义 Unicode 和旧版字符集之间的任何转换表，因此它们不能成为标准之一。
- `iconv()` 中可用的字符集和转换表取决于可用的 iconv 库。除此之外，日语区域名称在不同系统上可能不同。这意味着字符集参数的值取决于你正在使用的 `iconv()` 实现。

尽管 Windows 内部使用 2 字节固定 UCS-2 编码，但在日语环境中通常使用 `Shift_JIS` 系列编码，就像英语环境中的 ASCII 编码一样。

### 29.5.1 基本参数设置

`dos charset` 和 `display charset` 应设置为与 Windows 上使用的字符集和编码方法兼容的区域设置。这通常是 `CP932`，但有时会有不同的名称。

`unix charset` 可以是 `Shift_JIS` 系列、`EUC-JP` 系列或 `UTF-8`。`UTF-8` 始终可用，但其他区域设置的可用性及其名称本身取决于系统。

此外，通过 `vfs.cap` 模块，你可以考虑使用 `Shift_JIS` 系列作为 `unix charset` 参数的值，这与在 Samba 2.2 系列中设置 `coding system = CAP` 执行相同操作。

在哪里设置 `unix charset` 是一个困难的问题。以下是使用特定值时的详细列表、优点和缺点。

#### Shift_JIS 系列

`Shift_JIS` 系列意味着等同于 `Shift_JIS` 的区域设置，它在日语 Windows 上作为标准使用。以 `Shift_JIS` 为例，如果一个日语文件名由 `0x88a4` 和 `0x974e` 组成（一个 4 字节的日语字符串，意为“共享”），并从 Windows 写入 Samba 的 `.txt`，那么 UNIX 上的文件名变为 `0x88a4`、`0x974e`、`.txt`（一个 8 字节二进制字符串），与 Windows 相同。

由于 *Shift_JIS* 系列通常作为某些基于商业的 UNIX 系统的日语区域设置使用：`hp-ux` 和 `AIX`（不过，也可以使用 `EUC-JP` 区域设置系列）。要在这些平台上使用 *Shift_JIS* 系列，从 Windows 创建的日语文件名也可以在 UNIX 上引用。

如果你的 UNIX 已经在使用 *Shift_JIS*，并且有用户需要使用从 Windows 写入的日语文件名，那么 *Shift_JIS* 系列是最佳选择。但是，可能会显示损坏的文件名，并且一些无法处理非 ASCII 文件名的命令在解析文件名时可能会中止。特别是，文件名中可能包含 `"\`（`0x5c`），需要小心处理。最好在 UNIX 上不要触碰从 Windows 写入的文件名。

请注意，大多数日本化的免费软件实际上仅支持 `EUC-JP`。验证日本化免费软件是否支持 *Shift_JIS* 是一个好习惯。

#### EUC-JP 系列

`EUC-JP` 系列意味着等同于称为 `EUC-JP` 的行业标准的区域设置，广泛用于日语 UNIX（尽管 EUC 包含其他语言（如 `EUC-KR`）的规范）。以 `EUC-JP` 系列为例，如果一个日语文件名由 `0x8ba4` 和 `0x974c` 组成，并从 Windows 写入 Samba 的 `.txt`，那么 UNIX 上的文件名变为 `0xb6a6`、`0xcedd`：`.txt`（一个 8 字节二进制字符串）。

由于 `EUC-JP` 通常作为日语区域设置用于开源 UNIX、Linux、FreeBSD，以及基于商业的 UNIX、Solaris、IRIX 和 Tru64 UNIX（不过，Solaris 上也可以使用 *Shift_JIS* 和 `UTF-8`，Tru64 UNIX 上可以使用 *Shift_JIS*）。使用 `EUC-JP` 系列，大多数从 Windows 创建的日语文件名也可以在 UNIX 上引用。此外，大多数日本化免费软件主要支持 `EUC-JP`。

建议在 UNIX 上使用日语文件名时选择 `EUC-JP` 系列。虽然不需要像 `"\`（`0x5c`）那样小心处理的字符，但可能会显示损坏的文件名，并且一些无法处理非 ASCII 文件名的命令在解析文件名时可能会中止。

此外，如果你使用不同安装的 `libconv` 构建 Samba，`libconv` 中包含的 `eucJP-ms` 区域设置和操作系统中包含的 `EUC-JP` 系列区域设置可能不兼容。在这种情况下，你可能需要避免在文件名中使用不兼容的字符。

#### UTF-8

`UTF-8` 意味着等同于 Unicode 联盟定义的国际标准 `UTF-8` 的区域设置。在 `UTF-8` 中，一个字符使用 1 到 3 个字节表示。对于日语，大多数字符使用 3 个字节表示。由于 Windows 上使用 *Shift_JIS* 来表示日语，其中字符用 1 或 2 个字节表示，基本上 `UTF-8` 字符串的字节长度是原始 *Shift_JIS* 字符串的 1.5 倍。以 `UTF-8` 为例，如果一个日语文件名由 `0x8ba4` 和 `0x974c` 组成，并从 Windows 写入 Samba 的 `.txt`，那么 UNIX 上的文件名变为 `0xe585`、`0xb1b6`、`0x9e89`：`.txt`（一个 10 字节二进制字符串）。

> ² <http://www.unicode.org/>
> ³ <default://j3se.de/linux/convmv/>

对于 `iconv()` 不可用或其 `iconv()` 区域设置与 Windows 不兼容的系统，`UTF-8` 是唯一的可用区域设置。

没有系统使用 `UTF-8` 作为日语的默认区域设置。

一些损坏的文件名可能会被显示，并且一些无法处理非 ASCII 文件名的命令可能在解析文件名期间终止。特别地，文件名中可能包含 `\`（`0xfc`），这必须被仔细处理，因此你最好不要在 UNIX 上触碰从 Windows 写入的文件名。

此外，虽然这与 Samba 没有直接关系，但由于在 UNIX 上通常使用的 `iconv()` 函数与其他平台（如 Windows 和 Java）使用的函数之间存在细微差异，因此在处理 `Shift_JIS` 与 Unicode `UTF-8` 之间的转换时必须小心，并认识到该过程中涉及的局限性。

尽管 Mac OS X 使用 `UTF-8` 作为其文件名的编码方式，但它使用了一种 Samba 无法处理的扩展 `UTF-8` 规范，因此 Mac OS X 不可用 `UTF-8` 区域设置。

### Shift_JIS 系列 + vfs_cap (CAP 编码)

`CAP` 编码是指在 `CAP` 和 `NetAtalk`（Macintosh 文件服务器软件）中使用的规范。在 `CAP` 编码的情况下，例如，如果一个日语文件名由 `0x8baa` 和 `0x9f4c` 组成，并且在 Samba 上从 Windows 写入 `txt`，那么 UNIX 上的文件名将变成 `:8baa:9f4c.txt`（一个 14 字节的 ASCII 字符串）。

对于 `CAP` 编码，无法表示为 ASCII 字符（`0x80` 及以上）的字节会以 `:xx` 形式编码。你需要小心文件名中包含的 `\`（`0x5c`），但在无法处理非 ASCII 文件名的系统中，文件名不会被破坏。

`CAP` 编码的最大优点是与 `CAP` 或 `NetAtalk` 的文件名编码的兼容性。它们分别是 Columbia Appletalk Protocol 和 NetAtalk 开源软件项目。由于这些软件应用程序使用 `CAP` 编码在 UNIX 上写入文件名，如果目录同时由 Samba 和 NetAtalk 共享，你需要使用 `CAP` 编码以避免非 ASCII 文件名被破坏。

然而，最近在一些系统中，`NetAtalk` 已打过补丁，使用 `EUC-JP` 写入文件名（例如，日本原版 Vine Linux）。在这种情况下，你需要选择 `EUC-JP` 系列而不是 `CAP` 编码。

`vfs_cap` 本身可用于无法处理非 ASCII 字符的系统或与 NetAtalk 共享文件的系统的非 `Shift_JIS` 系列区域设置。

要在 Samba-3 上使用 `CAP` 编码，你应该如示例 29.5.1 所示，使用 `unix charset` 参数和 VFS。

如果 `unix charset` 使用 GNU `libiconv`，你应该设置 `CNF42`。有了这个设置，`cap-share` 共享中的文件名将以 `CAP` 编码写入。
