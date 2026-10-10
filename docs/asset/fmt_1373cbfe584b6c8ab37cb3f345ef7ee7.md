
在 Perl 5.8.0 中，这种缓慢程度通常非常惊人；在 Perl 5.8.1 中引入了缓存方案，改善了这种情况。通常情况下，对 UTF-8 编码字符串的操作仍然较慢。例如，Unicode 属性（字符类）如 `\p{Nd}` 已知比其简单的 `[0-9]` 慢得多（5-20 倍，尽管如此，有数百个 Unicode 字符匹配 Nd，而匹配 [0-9] 的只有 10 个 ASCII 字符）。

## 另见 (SEE ALSO)

`perlunitut`, `perluniintro`, `perluniprops`, `Encode`, `open`, `utf8`, `bytes`, `perlretut`, `perlvar` 中的 `"${^UNICODE}"`, `<>`.

## Perl 菜谱 (PERLUNICOOK)

> 名称

`perlunicook` - 在 Perl 中处理 Unicode 的菜谱示例

## 描述 (DESCRIPTION)

此手册页包含了演示如何在 Perl 中处理常见 Unicode 操作的短食谱，末尾还有一个完整的程序。单个食谱中的任何未声明的变量都被假设在之前已有适当的值。

## 示例 (EXAMPLES)

### X 0: 标准导言 (Standard preamble)

除非另有说明，下面的所有示例都需要此标准导言才能正常工作：

```
#!/usr/bin/perl
use strict;
use warnings;
use utf8;

# 这是一个 Unicode 字符串
my $str = "你好，世界";
print $str, "\n";

# 使用 Unicode 转义序列
my $unicode_str = "\u4f60\u597d\u7446\u754c\u7e46\u724d";
print $unicode_str, "\n";
```

（注：根据示例逻辑翻译为：除非另有说明，下面的所有示例都需要此标准导言才能正常工作：`my $str = "你好，世界"; print $str, "\n";`。使用 Unicode 转义序列：`my $unicode_str = "\u4f60\u597d\u7446\u754c\u7e46\u724d"; print $unicode_str, "\n";`）

### X 1: Unicode 属性 (Unicode properties)

```perl
use utf8;
my $char = "7";
if ($char =~ /\p{Nd}/) {
    print "这是一个数字\n";
}
```

### X 2: 归一化 (Normalization)

```perl
use utf8;
use Unicode::Normalize;

my $str = "e\x0301"; # e + 分音符号
my $nfc = nfc($str);
my $nfd = nfd($str);

print "NFC length: " . length($nfc) . "\n"; # 2
print "NFD length: " . length($nfd) . "\n"; # 3
```

### X 3: Unicode 转义 (Unicode escapes)

```perl
use utf8;
my $str = "你好";
print $str, "\n";
```

### X 4: 字符编码 (Character encoding)

```perl
use utf8;
my $str = "你好";
print "Characters length: " . length($str) . "\n"; # 2
print "Bytes length: " . length(encode($str)) . "\n"; # 6
```

### X 5: Unicode 字量 (Unicode literals)

```perl
use utf8;
my $str = "你好";
print $str, "\u4f60\u597d", "\n";
```

### X 6: 字符类 (Character classes)

```perl
use utf8;
my $str = "你好";
if ($str =~ /\p{Han}/) {
    print "这是一个汉字\n";
}
```

### X 7: Unicode 匹配 (Unicode matching)

```perl
use utf8;
my $str = "你好";
if ($str =~ /[\p{L}]/) {
    print "这是一个字母\n";
}
```

### X 8: Unicode 排序 (Unicode sorting)

```perl
use utf8;
my $str = "你好世界";
my @chars = split //, $str;
sort @chars;
print join // @chars, #;
```

### X 9: Unicode 解码 (Unicode decoding)

```perl
use utf8;
my $data = "\xe4\xbd\xa0\xe5\xa5\xbd";
my $str = decode("utf-8", $data);
print $str, "\n";
```

### X 10: Unicode 编码 (Unicode encoding)

```perl
use utf8;
my $str = "你好";
my $data = encode("utf-8", $str);
print $data, "\n";
```

使用 `:alias` 为现有字符赋予词法作用内的别名，甚至可以为无名的私用字符赋予有用的名称。

## X 11: CJK 编码器的别名

汉字会以 CJK UNIFIED IDEOGRAPH-6771 和 CJK UNIFIED IDEOGRAPH-4EAC 的字符名称返回，因为它们的 Xnames 各不相同。CPAN 的 `Unicode::Unihan` 模块拥有一个巨大的解码字典（以及更多），你只需提供已知的方法来理解其输出。

```perl
# cpan -i Unicode:Unihan Unicode::Unicode; my $str = "XX"; my $unhan = new Unicode::Unihan; for my $lang (qw(Mandarin Cantonese Korean Japaneseekun)) { printf "CJK str in %-2s is ", $lang; say $unhan->($str); }
```

打印：

CK XX in Mandarin is DONGJING1CK XX in Cantonese is dung1ging1 CK XX in Korean is Japaneseon is TOKOUEI KIN CK XX in JapaneseEkun is HIGASHI AZUMAMYIKO

如果你正在使用特定的罗马化方案，请使用特定的模块：

```perl
# cpan -i Lingua::JA::Romanize: Japanese use
Lingua::JA::Romanize::Japanese; my $k2r = new Lingua::JA::Romanize::Japanese; my $str = "XX"; say "Japanese for str is ", $k2r->chars($str)
```

打印：

Japanese for XX is toukou

## X 12: 显式编码/解码

在少数情况下（例如数据库读取），你可能需要解码。

```perl
use Encode qw(encode); my $chars = decode("shiftjis", $bytes, 1);
OR my $bytes = encode("MIME-Header-ISO_2022-JP", $chars, 1);
```

对于所有编码相同的流，不要使用 `encode`/`decode`；相反，请在打开文件时或打开后立即通过下文的 `binmode` 设置文件编码。

## X 13: 将程序参数解码为 utf8

```perl
# perl -CA., or export PERL_UNICODE=A or use Encode qw(decode_utf8); @ARGV map { decode_utf8(\$, 1) } @ARGV;
```

## X 14: 将程序参数解码为 locale 编码

```perl
# cpan -i Unicode::Locale use Encode qw(locale); use Encode::Locale; # use "locale" as an arg to encode/decode @ARGV = map { decode(locale = \$, 1) } @ARGV;
```

## X 15: 声明 STD(IN,OUT,ERR) 为 utf8

使用命令行选项、环境变量，或者显式调用 `binmode`：
