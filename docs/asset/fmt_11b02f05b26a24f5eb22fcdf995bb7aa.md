
`-h`, `--help` 显示此帮助信息并退出

`-i`, `--interactive` 设置控制模式。

`-f`, `--force-mode` 设置强制解析模式以忽略错误。

`-l`, `--loose-mode` 设置宽松解析模式以捕获异常对象。

`-s SCRIPTFILE`, `--load-script=SCRIPTFILE` 加载存储在指定文件中的命令并执行它们。

### 示例
`/peepdf.py [options] PDF_file`

### 选项
`/peepdf.py [options] PDF_file`

## [73] 内存取证工具

- `volafox`
- `volatility`

**描述** 此工具将解析 PDF 文档，以识别分析文件中使用的基本元素。它不会渲染 PDF 文档。它提供了从 PDF 文档中提取原始数据（如压缩图像）的功能。`pdf-parser` 可以处理使用 PDF 语言混淆功能的恶意 PDF 文档。

# 用法
`pdf-parser.py [options] pdf-file`

- `-versions` 显示程序版本并退出
- `-h`, `--help` 显示此帮助信息并退出
- `-s SEARCH`, `--search:` 在间接对象（流除外）中搜索的字符串
- `-f`, `--filter` 将流对象通过过滤器处理（`FlateDecode`, `ASCIIHexDecode`, `ASIIBSDecode`, `LZWDecode` 和 `RunLengthLengthDecode`）
- `-o OBJECT`, `--object:OBJECT` 选择的直接对象（与版本无关）
- `-r REFERENCE`, `--reference:REFERENCE` 引用的对象（与版本无关）
- `-e ELEMENTS`, `--elements:ELEMENTS` 选择的元素类型 (`csv`)
- `-w`, raw 数据和过滤器的原始输出
- `-a`, `--stats` 显示 PDF 文档的统计信息
- `-t TYPE`, `--type TYPE` 选择的间接对象类型
- `-v`, verbose 显示格式异常的 PDF 元素
- `-x EXTRACT`, `--extract:EXTRACT` 提取到的文件名
- `-H`, `--hash` 对所有间接对象进行哈希
- `-n`, `--canonicalizedoutput` 不对输出进行规范化
- `-d DUMP`, `--dump:DUMP` 用于转储流内容的文件名
- `-d`, `--debug` 显示调试信息

# 示例

`pdf-parser.py http://example.com/doc.pdf`

# 示例

`pdf-parser.py maldoc.zip`

# peepdf

**描述** `peepdf` 是一个 Python 工具，用于探索 PDF 文件以确定该文件是否有害。该工具的目标是提供安全研究人员在 PDF 分析中可能的所有必要组件，而无需使用 3 或 4 个工具来完成所有任务。通过 `peepdf`，可以看到文档中显示可疑元素的所有对象，支持所有最常用的过滤器和编码，它可以解析不同版本的文件、对象流和加密文件。通过安装 `SpiderMonkey` 和 `Libemu`，它还提供了 JavaScript 和 Shell 代码分析封装器。此外，它能够创建新的 PDF 文件并修改现有的文件。

**用法** `/peepdf.py [options] PDF_file`

**选项**

```
-h, --help 显示此帮助信息并退出

-i, --interactive 设置控制模式。

-f, --force-mode 设置强制解析模式以忽略错误。

-l, --loose-mode 设置宽松解析模式以捕获异常对象。

-s SCRIPTFILE, --load-script=SCRIPTFILE 加载存储在指定文件中的命令并执行它们。
```
