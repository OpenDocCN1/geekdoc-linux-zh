
| 属性类型 | 属性值 |
| ------|
| 可用性 | SUNWcu4 |

## 参见

`cp(1)`, `cpio(1)`, `ln(1)`, `rm(1)`, `setfac(2)`, `attributes(5)`, `environ(5)`, `largefile(5)`, `XPG4(5)`

# native2 — 原生转ASCII

## 概要
`/usr/xpg4/bin/native2ascii [-encoding] [inputfile]`

## 描述
`javac(1)` 和其他工具可以处理 Latin-1 文件。如果省略 input，则使用标准输出。如果省略 encoding，则使用标准输入。

## 选项

- `-encoding` 指定可以传递的编码。

| 转换器类 | 描述 |
| --- | ---
| 8859 | ISO 8859-1 |
| 8859 | ISO 8859-2 |
| 8859 | ISO 8859-3 |
| 8859 | ISO 8859-4 |
| 8859 | ISO 8859-5 |
| 8859 | ISO 8859-6 |
| 8859 | ISO 8859-7 |
| 8859 | ISO 8859-8 |
| Big5 | Big5 |
| CNS1643 | CNS1643 |
| Big5 | 繁中文 |
| EUCJP | 日语 (5050 的超集) |
| CNS1643 | 繁中文 |
| 838 | IBM 扩展 SBCS |
| 1026 | IBM AIX |
| 1097 | IBM 伊朗/波斯 |
| 1098 | IBM 伊朗/波斯 |
| 1112 | IBM 拉脱维亚 |
| 1122 | IBM 爱沙尼亚 |
| 1123 | IBM 乌克兰 |
| 1124 | IBM 乌克兰 |
| 1250 | Windows 东欧 |
| 1251 | Windows Latin-1 |
| 1252 | Windows 希腊 |
| 1253 | Windows 土耳其 |
| 1254 | Windows 希伯来 |
| 1255 | Windows 阿拉伯 |
| 1256 | Windows 波罗的海 |
| 1257 | Windows 越南语 |
| 1381 | IBM OS/2 中国 |
| 1383 | IBM AIX 中国 |
| 273 | IBM 奥地利、德国 |
| 277 | IBMm 丹麦、挪威 |
| 278 | IBM 芬兰、瑞典 |
| 280 | IBM 意大利 |
| 284 | IBM 加泰罗尼亚/西班牙、拉丁美洲西班牙 |
| 285 | IBM 英国、爱尔兰 |
| 297 | IBM 法国 |
| 33722 | IBM-EUCJP - 日语 (5050 的超集) |
| 420 | IBM 阿拉伯 |
| 424 | IBM 希伯来 |
| 437 | MS-DOS 美国、澳大利亚、新西兰、南非 |
| 500 | EBCDIC 500V1 |
| 737 | PC 希腊 |
| 775 | PC 波罗的海 |
| 850 | MS-DOS Latin-1 |
| 852 | MS-DOS Latin-2 |
| 855 | IBM 西里尔 |
| 857 | IBM 土耳其 |
| 860 | MS-DOS 葡萄牙语 |
| 861 | MS-DOS 冰语 |
| 862 | PC 希伯来 |
| 863 | MS-DOS 加拿法语 |
| 864 | PC 阿拉伯 |
| 865 | MS-DOS 北欧 |
| 866 | MS-DOS 俄罗斯 |
| 868 | MS-DOS 巴基斯坦 |
| 869 | IBM 现代希腊 |
| 870 | IBM 多语言 Latin-2 |
| 871 | IBM 冰岛 |

# 848

# native2ascii

| 转换类 | 说明 |
| --- | --- |
| Cp874 | IBM 泰语。 |
| Cp875 | IBM 腊语。 |
| Cp918 | IBM 巴基斯坦（乌尔都语）。 |
| Cp921 | IBM 拉脱维亚、立陶宛（AIX, DOS）。 |
| Cp922 | IBM 爱沙尼亚（AIX, DOS）。 |
| Cp930 | 日语片假名混合混合4370 UDC，5026 的超集。 |
| Cp933 | 韩语混合1880 UDC，5029 的超集。 |
| Cp935 | 简体中文主机混合1880 UDC，5031 的超集。 |
| Cp937 | 传统中文主机混合6204 UDC，5033 的超集。 |
| Cp939 | 日语拉丁字混合4370 UDC，5035 的超集。 |
| Cp942 | 日语（OS/2），932 的超集。 |
| Cp948 | OS/2中文（台湾），938 的超集。 |
| Cp949 | PC 韩语。 |
| Cp950 | PC中文（香港、台湾）。 |
| Cp964 | AIX中文（台湾）。 |
| Cp970 | AIX 韩语。 |
| EUJCIS | JIS, EUC 编码，日语。 |
| GB2312 | GB2312, EUC 编码，简体中文。 |
| GBK | GBK，简体中文。 |
| ISO2022CN | ISO 2022 CN，中文。 |
| ISO2022CN_CNS | ISO-2022-CN 格式的 CN 11643，繁体中文。 |
| ISO2022CN_GB | ISO-2022-CN 格式的 GB 2312，简体中文。 |
| ISO2022KR | ISO 2022 KR，韩语。 |
| JIS | JIS，日语。 |
| JIS0208 | JIS 0208，日语。 |
| KOI8_R | KOI8-R，俄语。 |
| KSC5601 | KS C 5601，韩语。 |
| MS874 | Windows 泰语。 |
| MacArabic | Macintosh 阿拉语。 |

# nawk

| 转换类 | 说明 |
| --- | --- |
| MacCentralEurope | Macintosh 拉丁语-2。 |
| MacCroatian | Macintosh 克罗地亚语。 |
| MacCyrillic | Macintosh 西里尔语。 |
| MacDingbat | Macintosh 符号字。 |
| MacGreek | Macintosh 腊语。 |
| MacHebrew | Macintosh 希伯来语。 |
| MacIceland | Macintosh 冰岛语。 |
| MacRoman | Macintosh 罗马语。 |
| MacRomania | Macintosh 罗马尼亚语。 |
| MacSymbol | Macintosh 符号。 |
| MacThai | Macintosh 泰语。 |
| MacTurkish | Macintosh 土耳其语。 |
| MacUkraine | Macintosh 乌克兰语。 |
| SJIS | Shift-JIS，日语。 |
| UTF8 | UTF-8。 |

- `-reverse` 执行反向操作：将使用 Latin-1 或 Unicode 编码的文件转换为原生编码的文件。

## 属性

请参阅 `attributes(5)` 获取以下属性的说明：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWjvdev |

### 另请

`attributes(5)`

# nawk — 新模式扫描与处理语言

## 语法概要

```
/usr/bin/nawk [-F ERE][-v assignment] 'program' | -f profile argument...
/usr/xpg4/bin/awk [-F ERE][-v assignment 'program' | -f profile [argument...]
```
