
示例
方法
`print`
`printf`
`syswrite`
`write`
`flush`
`tell`
`eof`
`seek`
`binmode`
`opened`
`oflush`
`input_line_nuer`
`fileno`
`close`
`newStream([OPTS])`
`deflateParams`
导入 `:all`, `:constants`, `:flush`, `:level`, `:strategy` 示例

# IO::Compress::FAQ – 关于 IO::Compress 的常见问题

## 描述

### 通用

与 Unix `compress`/`uncompress` 的兼容性
访问 `.tar.Z` 文件
如何使用不同的压缩进行重新压缩？

### ZIP

`IO::Compress::Zip` & `IO::Compress::Unzip` 支持哪些压缩类型？
`Store (thod 0)`, `Deflate (thod 8)`, `Bzip2 (thod 12)`, `Lzma (thod 14)`
我可以读写大于 4GB 的 Zip 文件吗？
我可以在一个 Zip 文件中写入超过 64K 个条目吗？
Zip 资源

### GZIP

Gzip 资源
处理合并的 gzip 文件

### ZLIB 资源

### Bzip2

Bzip2 资源
- 处理合并的 bzip2 文件
- 与 Pbzip2 交互

### HTTP & 网络
- 重新回顾 Apache::GZip
- 压缩文件与 Net::FTP

### 杂
- 使用 “InputLength”解压缩较大文件/缓冲区中需要的数据。

另见 作者 修改历史 版权与许可协议

# IO::Compress::Gzip - 写入 RFC 1952 文件/缓冲区

## 摘要

### 描述
函数式接口

`gzip $input_filename_or_reference => $output_filename_or_reference [ , OPTS]`
一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输入 FileGlob 字符串, 一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输出 FileGlob

### 备记
可选参数
`AutoClose => 0|1`, `BinModeIn => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄

### 示例
OO 接口
构造函数
一个文件名, 一个文件句柄, 一个标量引用

构造函数选项
`AutoClose => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄, `Merge => 0|1`, `-Level`, `-Strategy`, `Minimal => 0|1`, `Comnt => $comnt`, `Name => $string`, `Type => $number`, `TextFlag => 0|1`, `HeaderCRC => 0|1`, `OS_Code => $value`, `ExtraField => $data`, `ExtraFlags => $value`, `Strict => 0|1`

### 示例
方法
- `print`
- `printf`
- `syswrite`
- `write`
- `flush`
- `tell`
- `eof`
- `seek`
- `binmode`
- `opened`
- `autoflush`
- `input_line_number`
- `fileno`
- `close`
- `newStream[OPTS]`
- `deflateParams`

导入 `:all` `:constants` `:flush` `:level` `:strategy` 示例
- 重新回顾 Apache::GZip
- 与 Net::FTP 配合使用

另见 2 作者 修改历史 版权与许可协议

# IO::Compress::RawDeflate - 写入 RFC 1951 文件/缓冲区

## 摘要

### 描述
函数式接口

`rawdeflate $input_filename_or_reference => $output_filename_or_reference [, OP]`
一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输入 FileGlob 字符串, 一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输出 FileGlob

### 备记
可选参数
`AutoClose => 0|1`, `BinModeIn => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄

### 示例
OO 接口
构造函数
一个文件名, 一个文件句柄, 一个标量引用
构造函数选项
`AutoClose => 0|1`, `Append => 0|1`, 一个缓冲区, 文件名, 一个文件句柄, `Merge => 0|1`, `-Level`, `-Strategy`, `Strict => 0|1`

### 示例
方法
- `print`
- `printf`
- `syswrite`
- `write`
- `flush`
- `tell`
- `eof`
- `seek`
- `binmode`
- `opened`
- `autoflush`
- `input_line_n`
- `fileno`
- `close`
- `newStream([{OPTS])`
- `deflate_all`, `:constants`, `:flush`, `:level`, `:strategy` 示例

- 重新回顾 Apache::GZip
- 与 Net::FTP 配合使用

另见 所有的 作者 修改历史 版权与许可协议

# IO::Compress::Zip - 写入 zip 文件/缓冲区

## 摘要

### 描述
函数式接口

`zip $filena_or_reference => $filena_or_reference [, OPTS]`
一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输入 FileGlob 字符串, 一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输出 FileGlob

### 备记
可选参数
`AutoClose => 0|1`, `BinModeIn => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄

### 示例
OO 接口
构造函数
一个文件名, 一个文件句柄, 一个标量引用
构造函数选项
`AutoClose => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄, `Merge => 0|1`, `-Level`, `-Strategy`, `Minimal => 0|1`, `Comnt => $comnt`, `Name => $string`, `Type => $number`, `TextFlag => 0|1`, `HeaderCRC => 0|1`, `OS_Code => $value`, `ExtraField => $data`, `ExtraFlags => $value`, `Strict => 0|1`

方法
方法 , , , ,,,,,, , , ,,,, ,,,,, 0 1, `TextFlag => 0|1`, `ExtraFieldLocal => $data`, `Minimal => 0`, `BlockSize 100K => number`, `WorkFactor => number`, `Preset => number,,Level, Strategy,,,  0 1`

### 示例
方法
- `print`
- `printf`
- `syswrite`
- `write`
- `flush`
- `tell`
- `eof`
- `seek`
- `binmode`
- `opened`
- `autoflush`
- `input_line_number`
- `fileno`
- `close`
- `newStream([OPTS])`
- `deflateParams`

另见 2 作者 修改历史 版权与许可协议

# IO::Dir - 为目录句柄提供对象方法

## 摘要

### 描述
构造函数
`new [ DIRNAME ]`, `open ( DIRNAME )`, `seek ( POS )`, `tell ( )`, `rewind ( )`, `close ()`
`tie,'IO::Dir', OPTIONS ]`

另见 作者
版权

# IO::File - 为文件句柄提供对象方法

## 摘要

### 描述
构造函数
`new ( FILENAME [,MODE,PERMS]] )`, `new_file`
方法
`open([ FILENAME [,MODE,PERMS]] )`, `open(FILENAME, LAYERS )`, `binmode([LAYER] )`

# IO::Handle - 为 I/O 句柄提供对象方法

## 摘要

### 描述
构造函数
`new ()`, `new_from_fd ( FD, MODE )`
方法
`io->fdopen ( FD, MODE )`, `io->opened`, `io->getline`, `io->getline ( ORD )`, `io->error`, `io->clear`, `io->sync`, `io->flush ( ARGS )`, `io->blocking ( BOOL )`

# IO::Pipe - 为管道提供对象方法

## 摘要

### 描述
构造函数
`new ( [READER, WRITER] )`
方法
`reader ([ARGS])`, `writer ([ARGS])`, `handles ()`

另见 作者
版权

# IO::Poll - poll 的对象接口

## 摘要

### 描述
方法
`mask ( IO [, EVENT_MASK ] )`, `poll ( TIMEOUT ] )`, `events ( IO )`, `remove ( IO )`, `handles ( EVENT_MASK )`

另见 作者
版权

# IO::Seekable - 为 I/O 对象提供 seek 方法

## 摘要

### 描述
`$io->getpos`, `io->setpos`, `io->seek ( POS, WHENCE=0 (SEEK_SET), WHENCE=1 (SEEK_CUR), WHENCE=2 (SEEK_END)`, `$io->sysseek(POS, WHENCE )`,
`io->tell`

另见 历史

# IO::Select - select 用的对象接口

## 摘要

### 描述
构造函数
`new ( [ HANDLES ] )`
方法
`add ( HANDLES )`, `remove ( HANDLES )`, `exists ( HANDLE )`, `handles`, `can_read ( TIMEOUT )`, `can_write ( TIMEOUT ] )`, `has_exception ( TIMEOUT ] )`, `count ( )`, `select ( READ, WRITE, EXCEPTION [, TIMEOUT ] )`

作者

# IO::Socket - socket 通信的对象接口

## 摘要

### 描述
构造函数
`new ([ARGS])`
方法
`accept((IP)`, `socketpair(DOMAIN, TYPE, PROTOCOL)`, `atmark`, `connected`, `protocol`, `sockdomain`, `socketopt(OPT [ VAL])`, `getsockopt(LEVEL, OPT)`, `ssetsopt(LEVEL, OPT, VAL)`, `socktype`, `timeout([VAL])`

限制
另见
作者
版权

# IO::Socket::INET - 用于 AF_INET 域套的对象接口

## 摘要

### 描述
构造函数
`new ([ARGS])`
方法
`sockaddr ()`, `sockport ()`, `sockhost ()`, `peerraddr ()`, `peerport ()`, `peerhost ()`

另见 作者
版权

# IO::Socket::IP, IO::Socket::IP - 同时支持 IPv4 和 IPv6 的家族无关 ip socket

## 摘要

### 描述
替换 "IO::Socket" 默认行为的构造函数
`$sock = IO::Socket::IP->new(%args)`
`PeerHost = string`, `PeerService = string`, `PeerAddr = string`, `PeerPort => string`, `PeerAddrInfo => array`, `LocalHost = string`, `LocalService = string`,
`LocalAddr = string`, `LocalPort = string`, `LocalAddrInfo = string`, `Family = int`,
`Type = int`, `Proto = string or int`, `GetAddrInfoFlags = int`, `Listen = int`,
`ReuseAddr = bool`, `ReusePort = bool`, `Broadcast = bool`, `V6Only = bool`,
`Multi`, `Blocking = bool`, `timeout = num`

`$sock = IO::Socket::IP->new($peeraddr)`
方法
`host`, `$service = $sock->sockhost_service($name)`
`$addr = $sock->sockhost`
`$port = $sock->sockport`
`$host = $sock->sockname`
`$service = $sock->sockservice`
`$addr = $sock->sockaddr`
`($host, $service) = $sock->peerhost($name)`
`$addr = $sock->peerport`
`$port = $sock->peerport`
`$host = $sock->peerhost`
`$service = $sock->peerservice`
`$addr = $peer->peeraddr`
`$inet = $sock->as_inet`

非阻塞
"PeerHost" 和 "LocalHost" 解析
`($host, $port ) := IO::Socket::IP->split_addr($addr )`
`$addr = IO::Socket::IP->join_addr(host, $port)`

### IO::Socket::INET 不兼容性

# IO::Socket::UNIX - 用于 AF_UNIX 域套的对象接口

## 摘要

### 描述
构造函数
`new ([ARGS])`
方法
`hostpath()`, `peerpath()`

另见 作者
版权

# IO::Uncompress::AnyInflate - 解压缩基于 zlib 的 (zip, gzip) 文件/缓冲区

## 摘要

### 描述
RFC 1950, RFC 1951 (可选的 gzip (RFC 1952), zip

函数式接口
`anyinflate $filena_or_reference => $output_filename_or_reference [, OPTS]`
一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输入 FileGlob 字符串, 一个文件名, 一个文件句柄, 一个标量引用, 一个数组引用, 一个输出 FileGlob

### 备记
可选参数
`AutoClose => 0|1`, `BinModeOut => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄, `MultiStream => 0|1`, `TrailingData => $scalar`

`RawInflate => 0|1`, `ParseExtra => 0|1` 如果 zip FEXTRA 头部字段存在且设置了此选项，它将强制模块检查其是否符合 RFC 1952 中定义的子结构。

### 示例

- 方法
- `read`
- `read`
- `getline`
- `getc`
- `ungetc`
- `inflateSync`
- `getHeaderInfo`
- `tell\eof`
- `seek`
- `binmode`
- `opened`
- `autoflush`
- `input_line_number`
- `fileno`
- `close`
- `nextStream`
- `trailingData`

### 导入: :all

### 示例
与 Net::FTP 协作

另请参见 (SEE ALSO) 属性 (AUTHOR) 修正历史 (MODIFICATION HISTORY) 版权所有 (COPYRIGHT) 和许可 (AND LICENSE)

## IO::Uncompress::Any - 解压 gzip, zip, bzip2 或 lzip 文件/缓冲区

## 概要
描述
DESCRIPTION
RFC 1950, RFC 1951 (可选), gzip (RFC 1952), zip, bzip2, lzop, lzma, xma
功能接口 (Functional Interface)

`anyuncompress $filena_or_reference => $output_filena_or_reference [, OPTS]`
文件名、文件句柄、一个标量引用、一个数组引用、一个输入 FileGlob 字符串、文件名、文件句柄、一个标量引用、一个数组引用、一个输出 FileGlob

## 注意事项

- 可选参数
- `AutoClose => 0|1`, `BinModeOut => 0|1`, `Append => 0|1`, 一个缓冲区, 一个文件名, 一个文件句柄, `MultiStream => 0|1`, `TrailingData => $scalar`

### 示例

- oo 接口
- 构造函数
- 一个文件名, 一个文件句柄, 一个标量引用

### 构造函数选项

```
```
