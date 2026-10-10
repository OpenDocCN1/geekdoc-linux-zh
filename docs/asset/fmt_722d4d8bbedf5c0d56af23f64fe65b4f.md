
DevAssistant 可以在开发过程中帮助您完成各种任务。这些任务由所谓的“助手 (`assistants`)”执行——共有四种助手：

- `create` - 创建新项目、安装依赖项并设置环境
- `modify` - 修改之前创建的项目（例如将其导入 Eclipse）
- `prepare` - 为上游项目准备开发环境
- `task` - 执行与特定项目相关的自定义任务

您可以将 `"create"` 缩写为 `"crt"`, `"modify"` 缩写为 `"mod"`, `"prepare"` 缩写为 `"prep"`。

每个助手类型都可以有许多关联助手（例如 `python`, `ruby`），每个助手都可以有许多关联子助手（例如 `django`, `flask`）。您可以通过运行例如 `devassistant crt -h` 和 `devassistant crt python -h` 来显示这些（以及其他选项）。一旦您选择了所需的助手（及其子助手），只需运行它即可，例如 `devassistant crt python django -n newproject`。

助手列表及其功能可能会根据您的安装情况而异——只需运行 `help` 即可查看当前可用的助手。（注意：`devassistant crt -h text` 在源码中重复出现并在此处合并）。

## 描述 - ACTION

DevAssistant 设计还旨在通过所谓的“操作 (`actions`)”提供自定义功能。

目前，这些包含：

- `help` - 显示详细帮助信息。
- `version` - 显示 `devassistant` 版本。

再次，要显示选项，只需在操作时使用 `-h`，例如 `devassistant version -h`。

## 通用选项

许多助手之间共享一些常用选项。它们的通常含义如下所示：

- `-h`
  打印助手的帮助信息。
- `-n`
  项目名称。
- `-e`
  将项目导入 eclipse。
- `-g`
  生成一个 SPEC 文件。
- `-b`
  构建 RPM
- `-v`
  vim 设置。

### 环境变量

`DEVASSISTANT_PATH`

一个用冒号分隔的目录列表，用于在其中搜索。如果找到多个同名的助手，将使用其中的第一个。

## 另请

`da(1)` `gui(1)`

## 名称

`df` - 报告文件系统磁盘占用

## 概要

```
df [OPTION]... [FILE]
```

### 描述

本帮助页文档了 GNU 版本的 `df`。`df` 显示文件系统上的可用空间。如果没有给出文件名，则显示所有当前挂载文件系统的空间。默认以 1K 块显示磁盘空间，除非设置环境变量 `POSIX_CORRECT`，则使用 512 字节块。

如果参数是包含挂载文件系统的绝对文件名，`df` 显示该文件系统的可用空间。此版本的 `df` 无法显示未挂载文件系统的可用空间，因为大多数此类操作需要对文件系统结构的非移植知识。

### 选项

显示文件所在文件系统的信息，默认显示所有。

长选项的强制参数对于短选项也是强制的。

- `-a`, `--all`
  包括伪文件、不可访问的文件系统
- `-B`, `--block-size=SIZE`
  打印前按 SIZE 缩放；例如‘BM’以 1048576 字节为单位打印；使用 SIZE 前缀
- `--direct`
  显示文件而非挂载点的统计信息
- `-h`, `--human-readable`
  以 1024 的幂打印大小（例如 1023M）
- `-H`, `--si`
  以 1000 的幂打印大小（例如 1.1G）
- `-i`, `--inodes`
  列出 inode 信息而不是块使用
- `-k`
  同 `--block-size=1K`
- `-l`, `--local`
  限制于本地文件系统
- `--no-sync`
  在获取使用信息时不调用同步（默认）
- `--output=[FIELD_LIST]`
  使用由 FIELD_LIST 定义的输出格式，如果省略则打印所有字段
- `-P`, `--portability`
  使用 POSIX 输出格式
- `--sync`
  在获取使用信息前调用同步
- `--total`
  忽略所有对可用空间不重要的条目，产生总计
- `-t`, `--type=TYPE`
  限制为类型 TYPE 文件系统
- `-T`, `--print-type`
  打印文件系统类型
- `-x`, `--exclude-type=TYPE`
  限制为非类型 TYPE 文件系统
- `-v`
  （被忽略）
- `--help`
  显示此帮助并退出

## 版本

输出版本信息并退出

显示值的单位取决于 `--block-size` 以及 `DF_BLOCK_SIZE`、`BLOCK_SIZE` 和 `BLOCKSIZE` 环境变量中的第一个可用值。否则，单位默认为 1024 字节（如果设置了 `POSIXLY_CORRECT`，则为 512）。

SIZE 参数是一个整数和一个可选单位（例如：10K 是 10*1024）。单位有 K、M、G、T、P、E、Z、Y（1024 的幂）或 KB、MB,...（1000 的幂）。

FIELD_LIST 是一个用逗号分隔的列列表，表示要包含的列。有效的字段名有：'source'、'ftype'、'itotal'、'iused'、'iaval'、'ipcent'、'size'、'used'、'avail'、'pcent'、'file' 和 'target'

### 作者

由 Torbjorn Granlund、David MacKenzie 和 Paul Eggert 编写。

## 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 将 `df` 的翻译错误报告到 <http://translationproject.org/team/>

## 版权

Copyright © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是一个自由软件：你可以自由地更改和重新发行它。在法律允许的范围内不提供任何保证。

## 另请

完整文档位于：<http://www.gnu.org/software/coreutils/df> 或通过本地信息可用：info ‘(coreutils)’ `df` 调用

## 名称

`dgst`, `sha`, `sha1`, `mdc2`, `ripemd160`, `sha224`, `sha256`, `sha384`, `sha512`, `md2`, `md4`, `md5`, `dss1` - 消息摘要

### 概要

```
openssl digest [-sha1|-mdc2|-ripemd160|-sha224|-sha256|-sha384|-sha512|-md2|-md4|-md5|-dss1] [-c] [-d] [-hex] [-binary] [-r] [-hmac arg] [-non-fips-allow] [-filename] [-sign filename] [-keyform arg] [-passin arg] [-verify filename] [-prverify filename] [-signature filename] [-hmac key] [-non-fips-allow] [-fips-fingerprint] [file...]
openssl [digest] [...]
```

### 描述

摘要函数以十六进制格式输出提供的文件的消息摘要。

摘要函数还使用消息摘要生成并验证数字签名。

### 选项

- `-c`
  仅在使用十六进制格式输出时，以冒号分隔的两位一组形式打印摘要。
- `-d`
  打印 BIO 调试信息。
- `-hex`
  以十六进制转储输出摘要。这是“正常”摘要（相对于数字签名）的默认情况。参见下方的数字签名 -hex。
- `-binary`
  以二进制形式输出摘要或签名。
- `-r`
  以 sha1sum 等程序使用的“coreutils”格式输出摘要。
- `-hmac arg`
  将 HMAC 密钥设置为“arg”。
- `-non-fips-allow`
  在 FIPS 模式下允许使用非 FIPS 摘要。这在非 FIPS 模式下没有影响。
- `-out filename`
  输出的文件名，默认为标准输出。
- `-sign filename`
  使用“filename”中的私钥对摘要进行数字签名。
- `-keyform arg`
  指定用于签名摘要的密钥格式。支持 DER、PEM、P12 和 ENGINE 格式。
- `-engine id`
  使用引擎进行操作（包括私钥存储）。此引擎不作为摘要算法的源，除非在配置文件中也指定。
- `-sigopt nm:v`
  在签名或验证操作期间将选项传递给签名算法。这些选项的名称和值取决于算法。
- `-passin arg`
