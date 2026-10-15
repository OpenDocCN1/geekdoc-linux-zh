
- `-x`: 转储 XML
- `-X`: 文件是 XMP
- `-w`: 原地写入。仅限 `-s`。与 `-o` 不兼容。
- `-o <file>`: 写入输出的文件。
- `-n <ns> <prefix>`: 设置命名空间的名称前缀。
- `-g <prop_name>`: 检索 `prop_name` 的值。
- `-s <prop_name> -v <value>`: 检索或获取值
- `<files>`: 要读取的文件。

## 安全性

源代码尚未进行安全审计。命令行工具缺乏严格的输入有效性检查。

请小心不要以超级用户身份运行该工具。如果您决定在线（Web）应用程序中使用它，也请务必谨慎。

欢迎提交补丁和建议。

### 作者

`Exempi` 由 Hubert Figuiere 编写。

它包含了由 Adobe Systems Inc. 编写的 XMP SDK。

## 许可证

`Exempi` 在 BSD 许可证下授权。

## EXPAND

### 名称

`expand` - 将制表符转换为空格

### 概要

```
expand [OPTION]... [FILE]...
```

### 描述

将每个 `FILE` 中的制表符转换为空格，并写入标准输出。

如果没有指定 `FILE`，或者 `FILE` 为 `-`，则从标准输入读取。

长选项的必需参数对于短选项也是必需的。

- `-i`, `--initial`

  不转换非空白字符之后的制表符

- `-t`, `--tabs=NUMBER`

  使制表符间距为 `NUMBER` 个字符，而非 8

- `-t`, `--tabs=LIST`

  使用逗号分隔的列表指定明确的制表符位置

- `--help`

  显示此帮助信息并退出

- `--version`

  输出版本信息并退出

### 作者

由 David MacKenzie 编写。

### 报告错误

GNU coreutils 在线帮助： <http://www.gnu.org/software/coreutils/> 请将 `expand` 翻译错误报告至 <http://translationproject.org/team/>

### 版权

版权所有 © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 第 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：您可以自由地修改和重新分发它。在法律允许的范围内，没有担保。

### 另见

`unexpand(1)`

完整文档位于： <http://www.gnu.org/software/coreutils/expand> 或者可通过本地访问：info ‘(coreutils) expand invocation’

## EXPR

### 名称

`expr` - 求值表达式

### 概要

```
expr EXPRESSION
expr OPTION
```

### 描述

- `--help`

  显示此帮助信息并退出

- `--version`

  输出版本信息并退出

将 `EXPRESSION` 的值打印到标准输出。下面的一行空白分隔了优先级递增的组。`EXPRESSION` 可以是：

- `ARG1 | ARG2`

  如果 `ARG1` 既不是空也不是 0，则为 `ARG1`，否则为 `ARG2`

- `ARG1 & ARG2`

  如果两个参数都不是空或 0，则为 `ARG1`，否则为 0

- `ARG1 < ARG2`

  `ARG1` 小于 `ARG2`

- `ARG1 <= ARG2`

  `ARG1` 小于或等于 `ARG2`

- `ARG1 = ARG2`

  `ARG1` 等于 `ARG2`

- `ARG1 != ARG2`

  `ARG1` 不等于 `ARG2`

- `ARG1 >= ARG2`

  `ARG1` 大于或等于 `ARG2`

- `ARG1 > ARG2`

  `ARG1` 大于 `ARG2`

- `ARG1 + ARG2`

  `ARG1` 和 `ARG2` 的算术和

- `ARG1 - ARG2`

  `ARG1` 和 `ARG2` 的算术差

- `ARG1 * ARG2`

  `ARG1` 和 `ARG2` 的算术积

- `ARG1 / ARG2`

  `ARG1` 除以 `ARG2` 的算术商

- `ARG1 % ARG2`

  `ARG1` 除以 `ARG2` 的算术余数

- `STRING : REGEXP`

  在 `STRING` 中锚定的 `REGEXP` 模式匹配

- `match STRING REGEXP`

  与 `STRING : REGEXP` 相同

- `substr STRING POS LENGTH`

  `STRING` 的子串，`POS` 从 1 开始计数

- `index STRING CHARS`

  在 `STRING` 中找到任意 `CHARS` 的索引，或为 0

- `length STRING`

  `STRING` 的长度

- `TOKEN`

  将 `TOKEN` 解释为字符串，即使它是像 ‘match’ 这样的关键字或像 ‘/’ 这样的运算符

- `( EXPRESSION )`

  `EXPRESSION` 的值

请注意，许多运算符在 shell 中需要转义或加引号。如果两个 `ARG` 都是数字，则比较是算术比较；否则是字典序比较。模式匹配返回 `\( ` 和 `\)` 之间匹配的字符串，或者为空；如果未使用 `\( ` 和 `\)`，则返回匹配的字符数或 0。

如果 `EXPRESSION` 既不是空也不是 0，则退出状态为 0；如果 `EXPRESSION` 为空或 0，则退出状态为 1；如果 `EXPRESSION` 语法无效，则退出状态为 2；如果发生错误，则退出状态为 3。

### 作者

由 Mike Parker, James Youngman 和 Paul Eggert 编写。

### 报告错误

GNU coreutils 在线帮助： <http://www.gnu.org/software/coreutils/> 请将 `expr` 翻译错误报告至 <http://translationproject.org/team/>

### 版权

版权所有 © 2015 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 第 3 版或更高版本 <http://gnu.org/licenses/gpl.html>。这是自由软件：您可以自由地修改和重新分发它。在法律允许的范围内，没有担保。

### 另见

完整文档位于： <http://www.gnu.org/software/coreutils/expr> 或者可通过本地访问：info ‘(coreutils) expr invocation’

## EXTLINUX

### 名称

`extlinux` - 在 ext2/ext3 文件系统上安装 SYSLINUX 引导加载程序

### 概要

```
extlinux [*options*] *directory*
```

### 描述

`EXTLINUX` 是一个新的 syslinux 衍生版本，可以从 Linux ext2/ext3 文件系统启动。它与 `SYSLINUX` 的工作方式相同，但有一些细微的修改。旨在简化 Linux 的初次安装，并用于创建救援和其他特殊用途的引导磁盘。

安装程序设计为在挂载的目录上运行。例如，如果您将一个 ext2 或 ext3 USB 密钥挂载在 `/mnt` 上，您可以运行以下命令：

```
extlinux --install /mnt
```

### 选项

- `-H`, `--heads=#`

  强制指定磁头数量。

- `-i`, `--install`

  覆盖当前的引导扇区。

- `-O`, `--clear-once`

  清除一次性启动命令。

- `-o`, `--once=command`

  在启动时执行一次命令。

- `-M`, `--menu-save=label`

  设置下一次启动时默认选择的标签

- `-r`, `--raid`

  在启动失败时回退到下一个设备。

- `--reset-adv`

  重置辅助数据。

- `-S`, `--sectors=#`

  强制指定每道扇区数。

- `-U`, `--update`

  更新之前的 EXTINUX 安装。

- `-Z`, `--zip`

  强制软盘几何参数 `-H 64 -S 32`。

- `--device=devicename`

  覆盖设备名称的自动检测。此选项仅适用于特殊环境，普通用户不应使用。滥用此选项可能会导致磁盘损坏和数据丢失。

### 文件

`extlinux` 配置文件必须命名为 `syslinux.cfg` 或 `extlinux.conf`，并且必须存储在 `extlinux` 安装目录中。有关 `extlinux.conf` 内容的更多信息，请参阅 `syslinux(1)` 手册页的 files 部分。

### 缺陷

如果您在使用 `SYSLINUX` 时遇到任何问题，我将不胜感激能听到您的反馈。如果您成功使用了 `SYSLINUX`，我也希望能得到您的反馈，特别是如果您正在将其用于某个发行版。
