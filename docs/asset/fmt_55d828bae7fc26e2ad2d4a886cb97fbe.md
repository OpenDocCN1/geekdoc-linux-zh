
# DynaLoader - 将 C 库动态加载到 Perl 代码中

## 用法
## 描述
`@dl_library_path`, `@dl_resolve_using`, `@dl_require_syols`, `@dl_libs`, `@dl_modules`, `@dl_shared_objects`, `$dl_error()`, `$dl_debug`, `$dl_dlext`, `$dl_($(` `$dl_expandspec()`, `$dl_load_file()`, `$dl_unload_file()`, `$dl_load_flags()`, `$dl_find_syol`, `$dl_find_syol_anywhere()`, `$dl_undef_syols()`, `$dl_install_xsub()`, `bootstrap()`
## 作者

# Encode - Perl 中的字符编码

## 用法
## 目录
`Encode::Alias` - 编码的别名定义，`Encode::Encoding` - 编码实现基类，支持的编码列表， `Encode::CN` - 简体中文编码，`Encode::JP` - 日语编码， `Encode::KR` - 韩语编码，`Encode::TW` - 繁中文编码

## 描述
## 术语
## Perl 编码 API
## 基本方法
## 列出可用编码
## 定义别名
## 查找 IANA 字符集注册
## 通过 PerlIO 编码处理错误数据
## 检查值
`perlqq` 模式 (`CHECK = Encode::FB_PERLQQ`), HTML 字符引用模式 (`CHECK = Encode::FB_HTMLCREF`), xml 字符引用模式 (`CHECK = Encode::FB_XMLCREF`)
## 检查的编码
## 定义编码
`UTF-8` 与 `utf8`, `UTF8` 标记 `#1`; 目标 `#2`; 目标 `#3`; 目标 `#4`:
## 干扰 Perl 内部机制
`UTF-8` 与 `utf8`, `UTF8` 另参见维护 版所有

## 用法
### 摘要
### 描述
### 另参见

# Encode::CJKConstants – 由 Encode::??::ISO_2022_* 内部使用

# Encode::CN - 基于中国的中文编码

## 用法
## 描述
## 备注
## 缺陷
## 另参见

# Encode::CN::HZ – 由 Encode::CN 内部使用

# Encode::Config – 由 Encode 内部使用

# Encode::EBCDIC - EBCDIC 编码

## 用法
## 摘要
## 描述
## 另参见

# Encode::Encoder – 面向对象的编码器

## 用法
## 摘要
## 描述

### 预定义方法

```
$e = Encode::Encoder->new([$data, $encoding]); encoder(), $e->data([$data]), $e->encoding($encoding); $e->bytes($encoding)
```

#### 示例：base64 转换器

### 运算符重载

## 另参见

# Encode::Encoding - Encode 实现基类

## 用法
## 描述

### 你应该实现的方法

```
->encode($string, [$check]), ->decode($octets, [$check]), ->cat_decode($destination, $octets, $offset, $terminator, [$check])
```

### Encode::Encodings 中定义的其他方法

```
->na, ->mi_na, ->renew, ->renewed, ->perlio_ok(), ->needs_lines()
```

#### 示例：Encode::ROT123

为什么 Encode API de这么不一样？

# 编译编码

## 另参见 Sche 1, Sche 2, Other S

# Encode::GSM0338 – ESTI GSM 03.38 编码

## 用法
## 描述
## 备注
## 缺陷
## 另参见

# Encode::Guess – 从数据猜测编码

## 用法
## 摘要
## 描述
`Encode::Guess->set_suspects`, `Encode::Guess->add_suspects`, `Encode::decode("Guess" ...)`, `Encode::Guess->guess($data)`, `guess_encoding($data, [, list of suspects])`

## 注意
## 待事项
## 另参见

# Encode::JP - 日语编码

## 用法
## 摘要
## 描述
## 关于 ISO-2022-JP(-1) 的说明
## 缺陷
## 另参见

# Encode::JP::H2Z – 由 Encode::JP::2022_JP* 内部使用

# Encode::JP::JIS7 – 由 Encode::JP 内部使用

# Encode::KR - 韩语编码

## 用法
## 描述
## 缺陷
## 另参见

# Encode::KR::2022_KR – 由 Encode::KR 内部使用

# Encode::MIME::Header – MIME ‘B’ 和 ‘Q’ 头部编码

## 用法
## 摘要
## 描述
## 缺陷
## 另参见

# Encode::MIME::, Encode::MIME::NAME – 由 Encode 内部使用

## 另参见

# Encode::PerLIO – 关于 Encode 和 PerLIO 的详细文档

## 概述

### 它是如何工作的？
### 行缓冲
### 我该如何判断我的编码是否完全支持 PerlIO？

## 另参见

# Encode::Supported – Encode 支持的编码

## 描述
## Encoding Nas

### 支持的编码
#### 内置编码
- `Encode::Unicode` – 其他 Unicode 编码
- `Encode::Byte` – 扩展 ASCII
- ISO-8859 及相应的厂商映射，KOIB - 西里尔语字母的事实标准
- `gsm0338` - Hentai Latin 1
- CJK: 中文、日语、韩语（多字节）
- `Encode::CN` – 中国大陆，`Encode::JP` – 日本，`Encode::KR` – 韩国，`Encode::TW` – 台湾，`Encode::HanExtra` – 通过 CPAN 的更多中文，通过 CPAN 的 `Encode::JIS2KX 0213` 编码

### 杂编码
- `Encode::EBCDIC`, `Encode::Syols`, `Encode::MIME::Header`, `Encode::Guess`

### 不支持的编码
- ISO-2022-2 [RFC1554], ISO-2022-CC [RFC1922], 各种 HPU-UX 编码，西里尔语编码 `Encode::IR-IR-111`, ISO-8859-8-1 [希伯来], ISIRI 3342 Iran系统，ISIRI 2900 [波斯语]，泰国编码 TCVN，越南语编码 VPS，各种 Mac 编码 (Mac) 印度编码对比

### 字符集 – 分类（由 Anton 和 Dan Kogai 提供）
#### 微软相关命名
- `KS_5601-1987`, `GB2312`, `Big5`, `Shift_JIS`
- 字符集，编码集 (CCS), 编码（在 MIME 上下文中）, EUC, ISO-2022, UCS, UCS-2, Unicode, UTF, UTF-16

## 参考文献
ECMA-35 (ISO2022), IANA, 分配字符集, ISO, RFC, UC, 其他注意
- `czyborra.com`
- `CJK.inf`
- `debian.org`: Ken 写的 CJK 信息处理简介

# Encode::Syol - 编码

## 用法
## 摘要
## 描述
## 另参见

# Encode::TW - 基于台湾的中文编码

## 用法
## 描述
## 备注
## 缺陷
## 另参见

# Encode::Unicode – 各种转换格式

## 用法
## 摘要

### 快速参考
以网络字节序获取的大小、字节序和 BOM，在代理对中

# Encode::Unicode::UTF – UTF-7 编码

## 用法
## 摘要
## 在实践中

# English - 使用 nice (或 awk)
## 用法
## 描述
## 性能

# Env - 将变量导入为标量或数组的 perl 模块

## 用法
## 描述
## 局限性
## 作者

# Errno - 系统 errno 常量

## 用法
## 描述
## 注意事项
## 作者

# Exporter - 模块的默认导入方法

## 用法
## 描述
## 如何导出
## 导入什么

```
use YourModule; use YourModule qw(...);
```

## 高级功能
### 特殊导入列表
### 在不使用 Exporter 方法的情况下导出
### 在不继承 Exporter 的情况下导出
### 版本检查
### 管理未知符号
### 标签处理实用函数
### 生成常量
### 良好实践
### 声明 @EXPORT_OK 及其
### 安全起见
### 不应导出的

# Exporter::Heavy 内部实现

## 用法
## 描述

# ExtUtils::CBuilder - 为 Perl 模块编译和链接 C 代码

## 用法
## 描述

### 方法
```
