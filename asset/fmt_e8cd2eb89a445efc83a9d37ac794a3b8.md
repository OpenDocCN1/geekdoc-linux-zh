
# 高级方法

`->peek(LIST)`, `->peek(INDEX)`, `->insert(INDEX, LIST)`, `->extract()`, `->extract(INDEX)`, `->extract(INDEX, COUNT)`

### 注释

# 局限性

# 相关

# 维护者

# 许可

# Thread::Semaphore - 线程安全的信号量

## 版本

## 摘要

### 描述

# 方法

`->new()`, `->new(NUMBER)`, `->down()`, `->down(NUMBER)`, `->down_nb()`, `->down_nb(NUMBER)`, `->down_force()`, `->down_force(NUMBER)`, `->up()`, `->up(NUMBER)`

### 注释

# 相关

# 维护者

# 许可

# Tie::Array - 绑定数组的基类

## 摘要

### 描述

```
TIEARRAY classna, LIST, STORE this, index, value, FETCH this, index, FETCHSIZE,
SIZIZE this, count, EXTEND this, count, EXISTS this, key, DELETE this, CLEAR
this, DESTROY this, PUSH this, POP this, SHIFT this, UNSHIFT this, LIST, SPLICE this,
offset, length, LIST
```

## 注意事项

# 作者

# Tie::File - 通过 Perl 文件句柄访问磁盘文件的行

## 摘要
描述
recsep
autchomp
mode
mory_size
选项格式
公共方法
flock
autchomp
defer, “flush”, andautodefer
到已打开的文件句柄
并发访问
注意事项
作者
许可

# Tie::Handle - 绑定句柄的基类

## 摘要
描述
TIEHANDLE classna, LIST, WRITE this, scalar, length, PRINT this, LIST, PRINT this,
scalar, length, OPEN this, BINMODE this, TELL this, SEEK this, whence, DESTROY
this
更多信息
兼容性

# Tie::Hash, ExtraHash - 绑定哈希的基类

## 摘要
描述
TIEHASH classna, LIST, STORE this, key, value, FETCH this, key, FIRSTKEY
this, EXISTS this, key, DELETE this, key
继承自 Tie::StdHash
SCALAR, Tie::Hash::Capture - 正则缓冲区

## 摘要
描述
相关

# Tie::Memoize - 需要时向哈希添加数据

## 摘要
描述
继承自 Tie::Memoize
示例
缺陷
作者

# Tie::RefHash - 使用引用作为键

## 摘要
描述
线程支持
可存储支持
许可
维护者
相关

# Tie::Scalar, StdScalar - 绑定标量的基类

## 摘要
描述
TIESCALAR classna, LIST, STORE this, value, FETCH this, key, DELETE this, key
继承自 Tie::StdScalar
更多信息

# Tie::SubstrHash - 固定大小、固定键的哈希

## 摘要
描述
注意事项

# Tie::HiRes - 高分辨率闹钟、sleep、getofday、interval

## 摘要
描述
`gettofday()`, `usleep($seconds)`, `nanosleep(nanoseconds)`, `ualarm($seconds) [$interval_seconds]`, `tv_interval`, `sleep($floating_seconds)`, `alarm($floating_seconds])`, `getir($which)`, `clock_getres($which)`, `clock_nanosleep($which, nanoseconds, $flags = 0)`, `clock()`, `stat FH`, `stat EXPR`, `lstat`, `Lstat FH`, `Lstat EXPR`
示例
C API
诊断信息

useseconds 或 interval 大 ...
尚未发明
内部错误: useseconds < 0 (unsigned ... signed ...)
interval 等于 1000000
在此平台未实现
注意事项 相关 作者 版权所有

# Tie::Local - 从本地和 GMT 高效计算

## 摘要
描述
函数
timocal() 和 "time"
timocal_nocheck() 和 "nocheck"
年份解释
time_t 的限制
模拟本地 (DST)
不存在的本地 (DST)
负 epoch 值
实现 支持 版权 作者

# Tie::Piece - 面向对象

## 摘要
描述
用法
本地区域
日期计算
日期比较
日期解析
YYYY-MM-DDThh:mm:ss
周数
全局覆盖

注意事项
在 Win32 线程中设置 `$ENV{TZ}`
epoch 秒的使用
作者 版权所有 相关 缺陷

# Tie::Seconds - 将秒转换为日期的简单 API

## 摘要
描述
方法
作者
版权与许可
缺陷

# Tie::gmtime - 对 Perl 内置 gmtime() 函数的接口

## 摘要
描述
注释
作者

# Tie::localtime - 对 Perl 内置 localtime() 函数的接口

## 摘要
描述
注释
作者

# Tie::tm - 被 gmtime 和 localtime 使用的内部对象

## 摘要
描述
作者

# UNIVERSAL - 所有类的基类（已祝福引用）

## 摘要
描述

```
$obj->isa(TYPE), CLASS->isa(TYPE), eval { VAL->isa(TYPE) }, TYPE,
$obj, CLASS, VAL, $obj->DOES(ROLE), CLASS->DOES(ROLE), $obj->can(METHOD
CLASS)->can(METHOD), eval { VAL->can(METHOD) }, VERSION(REQUIRE)
```

警告
导出

# Unicode::Collate - Unicode 排序算法

## 摘要
描述
构造函数和定制

UCA_Version, alternate, backwards, entry, hangul_terminator, highestFFFF,
identical, ignoreChar, ignoreNa, ignore_level2, katakana_before_hiragana, level,
long_contraction, minimalFFF, normalization, overrideCJK, overrideHangul,
overrideOut, preprocess, rewrite, suppress, undefChar, undefNa,
upper_lower_variable

创建的方法

```
@sorted = $Collation->sort(@not_sorted), $result = $Collation->cmp($a, $b),
$result = $Collation->eq($a, $b), $result = $Collation->ne($a, $b), $result =
$result = $Collation->lt($a, $b), $result = $Collation->le($a, $b), $result =
$Collation->gt($a, $b), $result = $Collation->ge($a, $b), $sortKey =
$Collation->getSortKey($string), $sortKeyForm = $Collation->viewSortKey($string)
```

搜索的方法

```
$position = $Collation->index($string, $substring[, $position]),
$position, $length) = $Collation->index($string, $substring,
```

```perl
```
