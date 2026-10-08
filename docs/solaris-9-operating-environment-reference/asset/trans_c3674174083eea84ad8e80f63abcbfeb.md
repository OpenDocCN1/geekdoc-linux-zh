

## 文件

/usr/share/man/windex

目录内容和关键字数据库。

## 属性

关于以下属性的描述，请参阅 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWdoc |
| CSI | Enabled |

## 参见另

man(1), whatis(1), catman(1M), attributes(5)

## 诊断信息

/usr/share/man/windex: 不存在此文件或目录
该数据库不存在。你必须运行 catman(1M) 来创建它。

## ar — 维护可移植归档或库

## 概要

```
/usr/ccs/bin/ar -d [-Vv] archive file...
/usr/ccs/bin/ar -m [-abivV] [posname] archive file...
/usr/ccs/bin/ar -p [-sVw] archive [file...]
/usr/ccs/bin/ar -q [-cV] archive file...
/usr/ccs/bin/ar -r [-abciuV] [posname] archive file...
/usr/ccs/bin/ar -t [-sVw] archive [file...]
/usr/ccs/bin/ar -x [-CstV] archive [file...]

```

/usr/pg4/bin/ar -d [-Vv] archive file...
/usr/pg4/bin/ar -m [-abivV] [posname] archive file...
/usr/pg4/bin/ar -p [-sVw] archive [file...]
/usr/pg4/bin/ar -q [-cV] archive file...
/usr/pg4/bin/ar -r [-abciuV] [posname] archive file...
/usr/pg4/bin/ar -t [-sVw] archive [file...]
/usr/pg4/bin/ar -x [-CstV] archive [file...]
```

## 描述

该命令维护组合成单个归档文件的文件组。其主要用途是创建和更新库文件；然而，你也可以将其用于任何类似的目的。`ar` 使用的魔术字符串和头部由可打印 ASCII 字符组成。如果归档是由可打印文件组成的，则整个归档都是可打印的。

在创建归档时，它会以跨所有机器可移植的格式创建头部。归档格式和结构在 art(4) 中详细描述。

归档符号表（在 ar(4) 中描述）供链接编辑器使用，以便高效地对对象文件库进行多次处理。只有当归档中至少有一个对象文件时，`ar` 才会创建并维护归档符号表。归档符号表位于一个特殊命文件中，该文件始终是归档中的第一个文件。用户永远无法提及或也无法访问该文件。每当你使用该命令创建或更新此类归档的内容时，符号表都会重新构建。你可以使用 `-s` 选项强制重新构建符号表。

注意 — 如果你在参数列表中多次提到同一个文件，该文件可能会被多次放入归档中。

按照惯例，归档以 `.a` 字符结尾。

## 选项

- -a 将新文件放在归档中指定位置之后。
- -b 将新文件放在归档中指定位置之前。
- -c 在创建归档时，默认向标准输出打印诊断信息。
- -C 切换到包含归档的目录。
- -d 从归档中删除文件。
- -i 将文件插入到归档的指定位置。
- -m 写入符号表。
- -p 从归档提取文件。
- -q 静默模式创建归档。
- -r 更新归档中的文件。
- -s 强制重新构建符号表。
- -t 列出归档内容。
- -V 打印版本信息。
- -u 更新归档中的文件，如果文件较新则进行更新。
- -v 详细输出模式。
- -x 从归档中提取文件。

## 参数

- archive 归档文件的路径。
- file 文件路径。在与归档中的文件名进行比较时，仅使用最后部分。
- posname 归档中的文件名称，用于相对定位。

## 示例

以下示例显示了哪些模块组成了 libexample.archive。

```
castle$ t libexample.a
```

以下示例显示了如何从共享对象中提取模块。如果 module.o 是 libexample.a 归档库的一部分，你可以可以使用命令提取它。

```
castle$ x libexample.a module.o
```

Solaris 4.X 中的 ranlib 命令用于为归档库添加目录。现在 ranlib 命令已集成到 /usr/ccs/bin/ar 中。当 ar 归档对象文件时，它会自动创建一个符号表，如下所示：

```
castle$ rcv libfoo.a foo bar.o
```

以下命令强制重建归档库的符号表。

```
castle$ ts libfoo.a
```

