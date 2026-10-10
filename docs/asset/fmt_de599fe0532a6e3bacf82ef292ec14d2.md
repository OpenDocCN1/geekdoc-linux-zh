
`$position`), `match_ref = $Collator->match($string, substring)`, `($match)`

`= $Collator->match($string, substring)`, `@match = $Collator->match($string, $substring)`, `$count = $Collator->subst($string, $substring, $replacent)`, `$count = $Collator->gsubst($string, $substring, $replacent)`

# 其他方法

```perl
%old_tailoring = $Collator->change(%new_tailoring)
$modified_collator = $Collator->change(%new_tailoring)
$version = $Collator->version()
CA_version()
Base_Unicode_Version()
```

EXPORT CAVAT Normalization, Conformance Test AUTHOR, COPYRIGHT AND LICENSE 另见 `Unicode Collation Algorithm - UTS #10`, `The Default Unicode Collation Element Table for the U`, `Hangul Syllable Type`, `Unicode Normalization Forms - UAX #15`, `Unicode Locale Data Markup Language (LDML) - UTS #35`

# Unicode::Collate::CJK::Big5 - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 另见
CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJKGB2312 - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 注意事项

## 另见
CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJK::JISX208 - 为 Unicode::Collate 对 JIS KJI 进行加权

## 摘要

## 描述

## 另见
`Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJK::Korean - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 另见
CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJK::Pinyin - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 注意事项

## 另见
- CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJK::Stroke - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 注意事项

## 另见
- CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::CJK::Zhuyin - 为 Unicode::Collate 对 CJK 统一字符进行加权

## 摘要

## 描述

## 注意事项

## 另见
- CLDR - Unicode 通用区域数据库, `Unicode Locale Data Language (LDML) - UTS #35`, `Unicode::Collate`, `Unicode::Collate::Locale`

# Unicode::Collate::Locale - 通过 Unicode::Collate 对 DUCET 进行语言学定制

## 摘要

## 描述

## 构造函数

## 方法

```perl
$Collate->getlocale
$Collate->locale_version
```

一个可定制的区域设置（tailorable locales）列表

安装 CAVE 定制 AUTHOR 另见 `Unicode Collation Algorithm - UTS #10`, `The Default Unicode Collation Element Table (DUCET)`, `Unicode Locale Data Markup Language (LDML) - UTS #35`, CLDR - Unicode 通用区域数据库, `Unicode::Collate`, `Unicode::Normalize`

# Unicode::Normalize - Unicode 规范化形式

## 摘要

## 描述

# 规范化形式

`$NFD_string = NFD($string)`, `$NFC_string = NFC($string)`, `$NFKD_string = NFKD($string)`, `$NFKC_string = NFKC($string)`, `$FCD_string = FCD($string)`, `FCC_string = FCC($string)`, `$normalized_string = normalize($form_name, $string)`

# 分解与组合

```perl
$decomposed_string = decompose($string, [$useCompatMapping])
reordered_string = reorder($string)
$composed_string = compose($string)
($processed, $unprocessed) = splitOnLastAfter($normalized)
$processed = normalize_partial($form, $unprocessed)
$processed = NFD_partial($unprocessed)
$processed = NFC_partial($unprocessed)
$processed = NFKD_partial($unprocessed)
$processed = NFKC_partial($unprocessed)
```

# 快速检查

```perl
$result = checkNFD($string)
$result = checkNFC($string)
$result = checkNFKD($string)
$result = checkNFKC($string)
$result = checkFCD($string)
$result = checkFCC($string)
$result = check($form_na, $string)
```

# 字符

```perl
$canonical_decomposition = getCanon($code_point)
$compatibility_decomposition = getCompat($code_point)
$code_point_composite = getComposite($code_point_here, $code_point_next)
coining_class = getCoinClass($code_point)
```
