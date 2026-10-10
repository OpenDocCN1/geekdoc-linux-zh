
## 作者

本手册页由 Patrick Lam <plam@csail.mit.edu> 更新。

## 名称

fc-pattern - 解析并显示模式

## 概要

```
fc-pattern [ -cdVh ] [ --config ] [ --default ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ]
[ pattern [ element... ] ]
```

## 描述

**fc-pattern** 解析*模式*（默认为空模式）并显示解析结果。如果指定了 **--config**，则在对模式进行显示之前执行配置替换。如果指定了 **--default**，则在对模式进行显示之前执行默认值替换。

如果指定了任何元素，则仅打印这些元素。

## 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- `-c` 对模式执行配置替换。
- `-d` 对模式执行默认值替换。
- `-f` 根据格式说明符 `format` 格式化输出。
- `-V` 显示程序版本并退出。
- `-h` 显示选项摘要。
- `pattern` 解析并显示 `pattern`（默认使用空模式）。
- `element` 如果设置，则显示解析模式的 `element` 属性。

## 参见

**FcNameParse(3) FcConfigSubstitute(3) FcDefaultSubstitute(3) FcPatternPrint(3)**
**FcPatternFormat(3) fc-cat(1) fc-cache(1) fc-list(1) fc-match(1) fc-query(1) fc-scan(1)**

fontconfig 用户指南（HTML 格式）：*/usr/share/doc/fontconfig/fontconfig-user.html*。

## 作者

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

## 名称

fc-query - 查询字体文件

## 概要

```
fc-query [ -Vh ]
```

```
[ [ -b ] [ --ignore-blanks ] [ [ -i index ] [ --index index ] ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ] font-file...
```

## 描述

**fc-query** 使用标准的 fontconfig 规则查询 *font-file*（文件），并打印出每个找到的字体的字体模式。如果指定了 **--index**，则仅查询每个文件的一个字面（face），否则查询所有字面。

## 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- `-b` 忽略空白以计算语言
- `-i` 仅查询每个文件索引为 *index* 的字面。
- `-f` 根据格式说明符 *format* 格式化输出。
- `-V` 显示程序版本并退出。
- `-h` 显示选项摘要。
- *font-file* 查询 *font-file* 中的字体字面。

## 返回代码

**fc-query** 在成功解析时返回错误代码 0，如果发生任何错误或者至少有一个字体字面无法打开则返回 1。

## 参见

**fc-scan**(1) **FcFreeTypeQuery**(3) **FcPatternFormat**(3) **fc-cat**(1) **fc-cache**(1) **fc-list**(1) **fc-match**(1) **fc-pattern**(1)

fontconfig 用户指南（HTML 格式）：*/usr/share/doc/fontconfig/fontconfig-user.html*。

## 作者

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

## 名称

fc-scan - 扫描字体文件或目录

## 概要

```
fc-scan [ -Vvh ]
[ [ -b ] [ --ignore-blanks ] ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ] file…
```

## 描述

**fc-scan** 递归扫描 *file*（文件）并打印出每个找到的字面的字体模式。

## 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- **-b** 忽略空白以计算语言
- **-f** 根据格式说明符 *format* 格式化输出。
- **-V** 显示程序版本并退出。
- **-h** 显示选项摘要。
- ***file*** 递归扫描 *file* 中的字体字面。

## 返回代码

如果至少找到一个字体，**fc-scan** 返回错误代码 0，否则返回 1。

## 参见

fc-query(1) FcFileScan(3) FcDirScan(3) FcPatternFormat(3) fc-cat(1) fc-cache(1) fc-list(1) fc-match(1) fc-pattern(1)

fontconfig 用户指南（HTML 格式）：/usr/share/doc/fontconfig/fontconfig-user.html。

## 作者

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

## 名称

fc-validate - 验证字体文件

## 概要

**fc-validate** [ **-Vhv** ] [ [ **-i** *index* ] [ **--index** *index* ] [ [ **-l** *lang* ] [ **--lang** *lang* ] ] [ **--verbose** ] [ **--version** ] [ **--help** ] *font-file*...

## 描述

**fc-validate** 验证 *font-file*（文件），检查每个字体是否满足 fontconfig 中正字法文件规定的语言覆盖。如果指定了 **--index**，则仅验证每个文件的一个字面，否则验证所有字面。

## 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- `-i` 仅查询每个文件索引为 *index* 的字面。
- `-l` 将 *lang* 设置为语言，而不是当前区域设置。这用于 -m。
- `-v` 显示更详细的信息。
- `-V` 显示程序版本并退出。
- `-h` 显示选项摘要。
- *font-file* 查询 *font-file* 中的字体字面。

## 返回代码

**fc-validate** 在成功解析时返回错误代码 0，如果发生任何错误或者至少有一个字体字面无法打开则返回 1。

## 作者

本手册页由 Akira TAGOH <akira@tagoh.org> 更新。

## FGCONSOLE

## 名称

fgconsole - 打印活动虚拟终端的编号。

## 概要

**fgconsole** [—*help*|—*version*|—*next-avalable*]

## 描述

如果活动的虚拟终端是 /dev/ttyN，则向标准输出打印 N。
如果控制台是串行控制台，则打印 “serial”。

- —*next-available*
  显示下一个未分配的虚拟终端。通常分配 6 个虚拟终端，编号 7 用于 X；在这种情况下，将返回 “8”。

## 备注

在 *devfs* 下，控制台位于 /dev/vc/N。*devfsd* 可能维护符号链接以保持兼容性。

## 参见

**chvt**(1)。

## 名称

grep, egrep, fgrep - 打印匹配模式的行

## 概要

```
grep [OPTIONS] PATTERN [FILE...]
grep [OPTIONS] [-e PATTERN | -f FILE] [FILE...]
```

## 描述

**grep** 在指定的输入 *FILES* 中搜索包含与给定 *PATTERN* 匹配的行。如果未指定文件，或者给定了文件“-”，则 **grep** 搜索标准输入。默认情况下，**grep** 打印匹配的行。

此外，变体程序 **egrep** 和 **fgrep** 分别等同于 **grep -E** 和 **grep -F**。这些变体已弃用，但为了向后兼容性而保留。

## 选项

### 通用程序信息

- —**help**
  输出用法信息并退出。
- -V, —**version**
  输出 **grep** 的版本号并退出。

### 匹配器选择

- -E, —**extended-regexp**
  将 *PATTERN* 解释为扩展正则表达式（ERE，见下文）。
- -F, —**fixed-strings**
  将 *PATTERN* 解释为以换行符分隔的固定字符串列表，其中任何字符串都将被匹配。
- -G, —**basic-regexp**
  将 *PATTERN* 解释为基本正则表达式（BRE，见下文）。这是默认设置。
- -P, —**perl-regexp**
  将 *PATTERN* 解释为 Perl 正则表达式。这是高度实验性的，**grep** -P 可能会警告未实现的功能。

### 匹配控制

- -e *PATTERN*, —regexp=*PATTERN*
  使用 *PATTERN* 作为模式。这可用于指定多个搜索模式，或保护以连字符 (-) 开头的模式。
- -f *FILE*, —file=*FILE*
  从 *FILE* 获取模式，每行一个。空文件包含零个模式，因此不匹配任何内容。
- -i, —**ignore-case**
  在 *PATTERN* 和输入文件中忽略大小写区别。
- -v, —**invert-match**
  反转匹配逻辑，以选择不匹配的行。
- -w, —**word-regexp**
  仅选择包含形成完整单词的匹配的行。测试方法是匹配的子串必须位于行的开头，或者由非单词组成字符前置。同样，它必须位于行的末尾或者
