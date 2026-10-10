
# Locale::Currency - 货币的标准代码

**作者**
**版权**

## 摘要
## 描述
## 支持的代码集

`alpha`, `LOCALE_CURR_ALPHA`, `num`, `LOCALE_CURR_NUMERIC`

## 程序

`code2currency (CODE [CODESET], ['retired'])`, `currency2code (NAME [CODESET], ['retired'])`, `currency2code (CODE, CODESET, CODESET2)`

`all_currency_codes ([CODESET], ['retired'])`, `all_currency_nas ([CODESET] ['retired'])`, `Locale::Currency::rena_currency (CODE,NEW_NAME [,CODESET])`

`Locale::Currency::add_currency (CODE, NAME, [CODESET])`

`Locale::Currency::delete_currency (CODE, [CODESET])`,

`Locale::Currency::add_country_alias (NAME, NEW_NAME)`,

`Locale::Currency::delete_currency_alias (NAME)`

`Locale::Currency::rena_currency (code, NEW_CODE, [CODESET])`,

`Locale::Currency::add_currency_alias (CODE, NEW_CODE, [CODESET])`

`Locale::Currency::delete_currency_alias (CODE, [CODESET])`

另另
`Locale::Codes`, `Locale::Codes::API`,

**作者**
**版权**

# Locale::Codes::Language - 语言的标准代码

## 摘要
## 描述
## 支持的代码集

`alpha-2`, `LOCALE_LANG_ALPHA_2`, `alpha-3`, `LOCALE_LANG_ALPHA_3`, `term`, `LOCALE_LANG_TERM`

## 程序

`code2lang (CODE [, CODESET], ['retired'])`, `language2code (NAME [CODESET], ['retired'])`, `language_code2 (CODE, CODESET, CODESET2)`,

`all_language_codes ([CODESET]`, `all_language_nas ([CODESET ['retired'])`, `Locale::Codes::Language::rename_langvar (CODE ,NEW_NAME [CODESET])`, `Locale::Codes::Language::add_langvar (CODE ,NAME [CODESET])`, `Locale::Codes::Language::delete_langvar (CODE [, CODESET])`,

`Locale::Codes::Language::add_language_alias (NAME ,NEW_NAME)`,

`Locale::Codes::Language::delete_langvar_alias (NAME)`,

`Locale::Codes::Language::rename_lang_code (CODE ,NEW_CODE [, CODESET])`,

`Locale::Codes::Language::add_language_code_alias (CODE ,NEW_CODE [CODESET])`, `Locale::Codes::Language::delete_language_code_alias (CODE [,CODESET])`

另另
`Locale::Codes`, `Locale::Codes::API`, ,

**作者**
**版权**

## 概要
描述

## 快速概览
方法

### 构造方法
`"maketext"` 方法
`$l1h->fail_with(PARAM)`, `$l1h->failure_handler_auto`

### 实用方法
`$language->quant($nuer, $singular)`, `$language->quant($nuer, $plural)`, `$language->quant($nuer, $singular, $plural, $negative)`, `$language->numf($nuer)`, `$language->nurate($nuer, $singular, $plural, $plural, $negative)`, `$language->sprintf($format, @items)`, `$language->language_tag()`, `$language->encoding()`

## 处理属性与内部
语言类层级 每一个词典中的条目 括号表示法 自动词典 只读词典 控制 查找失败 如何使用 MAKETEXT 另另版权与免责声明 作者

# Locale::Maketext::Cookbook - 使用 Locale::Maketext 的食谱

## 序言
单侧词典
数字格式中的小数

# Locale::Maketext::Guts - 已废弃的用于加载 Locale::Maketext utf8 的模块

## 概要
描述

# Locale::Maketext::GutsLoader - 已废弃的用于加载 Locale::Maketext utf8 代码的模块

## 概要
描述

# Locale::Maketext::Simple - Locale::Maketext::Lexicon 的简单接口

## 版本
概要
描述
选项
类
路径
样式
导出
子类
解码
编码

# 致谢 另请参考 作者 版权

“MIT” 许可证

# Locale::Maketext::TPJ13 – 关于软件本地化的文章

## 概要
描述
本地化与 Perl：gettext 崩溃了，Maketext 修复了它
一个本地化惊悚故事：它也可能发生在你身上
语言学视角
拆解 gettext
替换 gettext
术语：抽象与封装
术语：同构
术语：继承
术语：简洁
细节中的魔鬼
证据在结果中：网站的本地化
参考文献

# Locale::Script - 脚本识别的标准代码

## 概要
描述

### 支持的字符集
`alpha`, `LOCALE_SCRIPT_ALPHA`, `num`, `LOCALE_SCRIPT_NUMERIC`

### 例程
`code2script ( CODE, [CODESET], ['retired'])`, `script2code ( NAME, [CODESET], ['retired'])`, `script_code ( CODE, CODESET, CODESET2)`, `all_script_code ( [CODESET], ['retired'])`, `all_script_nas ( [CODESET], ['retired'] )`

`Locale::Script::rena_script ( CODE,NEW_NAME, [CODESET] )`, `nLocale::Script::add_script ( CODE, NAME, [CODESET] )`, `nLocale::Script::delete_script ( CODE, [CODESET] )`, `nLocale::Script::add_code_alias ( NAME, NEW_NAME )`,

`Locale::Script::rena_script_code ( CODE,NEW_CODE, [CODESET] )`, `Locale::Script::add_code_alias ( CODE,NEW_CODE, [CODESET] )`, `Locale::Script::delete_script_alias ( CODE,NEW_CODE, [CODESET] )`

## 另请参考
`Locale::Codes`, `Locale::Codes::API`, ,

**作者**
**版权**

# MIME::Base64 - base64 字符串的编码与解码

## 概要
描述

`encode_base64($ bytes )`, `encode_base64($ bytes, $eol )`, `decode_base64($str )`,

```
encode_base64url($ bytes ), decoded_base64url($ str ), encoded_base64_length(
$bytes ), encoded_base64_length($bytes, $eol ), decoded_base64_length($str )
```
