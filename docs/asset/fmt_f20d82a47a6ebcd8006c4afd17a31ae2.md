
`-Level`, `-Method`, `-WindowBits`, `-MemLevel`, `-Strategy`, `-Dictionary`, `-Bufsize`

`($out, $status) = $d->deflate($buffer)`

`($Out, $status) = $d->flush`
`head2($out, $status) = $d->flush($flush_type)`

`$status = $d->deflateParams([OPT])`

`-Level`, `-Strategy`

`$d->dict_adler()`

`$d->msg()`

`$d->total_in()`

`$d->total_out()`

### 示例

Inflate 接口
`(Si, $status) = inflateInit()`
`-WindowBits`, `-Bufsize`, `-Dictionary`
`(Sout, $status) = $i->inflate($buffer)`

```c
$status = $i->inflateSync($status)

$i->dict_adler()

$i->msg()

$i->total_in()

$i->total_out()
```

### 示例

校验和(CHECKSUM) 函数(FUNCTIONS) 其他
`my $version = Compress::Zlib::zlib_version();`
常量请参见另、作者、修改历史、版权和许可

## Config - 访问 Perl 配置信息

### 摘要 (SYNOPSIS)

### 描述 (DESCRIPTION)

```perl
my_config(), config_sh(), config_re($regex), config_vars(@nas)
```
