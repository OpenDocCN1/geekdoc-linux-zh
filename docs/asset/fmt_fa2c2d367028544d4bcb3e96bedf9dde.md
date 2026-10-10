
## API 版本 2
`_1ex(N)`, `_nok(OBJ1, OBJ2)`, `_alen(OBJ2)`

## API 可选方法
`_signed_or(OBJ1, OBJ2, SIGN1, SIGN2)`, `_signed_and(OBJ1, OBJ2, SIGN1, SIGN2)`, `_signed_xor(OBJ1, OBJ2, SIGN1, SIGN2)`

## 包装你的缺陷
支持 回复: `CPAN` 的请求跟踪器，`AnnoCPAN`: 注释 `CPAN` 文档，`CPAN` 评分, 搜索 `CPAN`, `CPAN` 测试矩阵，`The Bum` 邮件列表，发送到邮件列表， 查看邮件列表， 订阅/取消 许可证 作者 另请参考

# Math::BigInt::Calce - 使用 BigInt 代码的 El 级数学

## 概要
描述
方法
`__e_bxor`, `__e_band`, `__e_bior`

## 缺陷
支持
`RT`: `CPAN` 的请求跟踪器，`AnnoCPAN`: 注释 `CPAN` 文档，`CPAN` 评分, 搜索 `CPAN`, `CPAN` 测试矩阵，`The Bignum` 邮件列表，发送到邮件列表， 查看邮件列表， 订阅/取消

许可证 作者 另请参考

# Math::BigInt::FastCalc - 为了更快速度而使用 xs 的 Math::BigInt::Calc

## 概要
描述
存储
方法
许可证
作者
另请参考

# Math::BigRat - 任意大有理数

## 概要
描述

## 数学库
`new()`
`nurator()`
`denominator()`
`parts()`
`numify()`
`as_int()`/`as_nuer()`
`as_float()`
`as_hex()`
`as_bin()`

`as_oct()`

`from_hex()`/`from_bin()`/`from_oct()`

`length()`

`digit()norm()`

`bfac()`

`bround()`/`round()`/`bfround()`

`bmod()`

`neg()`

`is_one()`

`is_zero()`

`is_pos()`/`is_positive()`

`is_neg()`/`is_negative()`

`is_int()`

`is_odd()`/`is_even()`

`bceil()`

`bfloor()`

`bsqrt()`

`broot()`

`badd()`/`bbl()`/`bsub()`/`bdiv()`/`bdec()`/`binc()`

`copy()`

`bstr()`/`bssstr()`

`bcmp()`/`bcmp()`

`blsft()`/`brsft()`

`bpow()`

`bexp()`

`nbexp()`

`nbok()`

`config()`

`objectify()`

`BUGS SUPPORT: CPAN’s请求跟踪器，AnnoCPAN: 注释 CPAN 文档，CPAN 评分, 搜索 CPAN, CPAN 测试矩阵，The Bigum 邮件列表，发送到邮件列表， Viewing mailing, 订阅/取消 许可证 另参考 作者`

# Math::Complex - 复数和相关的数学函数

## 概要
描述
操作
创建
显示
变更于 Perl 5.6

## 使用常量
`PI`
`Inf`

除以零或对数为零导致的错误
无法处理参数导致的错误
错误请另参见作者许可协议

# Math::Trig - 三角函数

用法摘要 `SYNOPSIS`
描述 `DESCRIPTION`
三角函数
`tan`
除以零导致的错误
简单（实数）参数，复数结果

平面角转换
`deg2rad`, `grad2rad`, `rad2deg`, `grad2deg`, `deg2grad`, `rad2grad`, `rad2rad`, `deg2deg`, `gradgrad`
极坐标转换
坐标系

# 3 维角度转换

`cartesian_to_cylindrical`, `cartesian_to_spherical`, `cylindrical_to_cartesian`, `cylindrical_to_spherical`, `spherical_to_cartesian`, `spherical_to_cylindrical`
大圆距离与方向

- `great_circle_distance`
- `great_circle_direction`
- `great_circle_bearing`
- `great_circle_destination`
- `great_circle_midpoint`
- `great_circle_waypoint`

示例 `EXAMPLES`
大圆公式注意事项 `CAVEAT FOR GREAT CIRCLE FORMULAS`
实值 `asin` 和 `acos`
`as_real`, `acos_real`

错误 作者 许可协议

# Memoize - 通过空间换时间提高函数速度

用法摘要 `SYNOPSIS`
描述 `DESCRIPTION`
详情 `DETAILS`
选项 `OPTIONS`
安装 `INSTALL`
规范化 `NORMALIZER`
`SCALAR_CACHE`, `"LIST_CACHE"`
`MEMORY`, `HASH`, `TIE`, `FAULT`, `MERGE`

其他功能 `OTHER FACILITIES`
`unmemoize`
`flush_cache`
注意事项 持久化缓存支持 过期支持 错误 邮件列表 作者
版权与许可 感谢

# Memoize::AnyDBM_File - 为 Storable 使用提供 AnyDBM_File EXISTS 的粘接代码

描述 `DESCRIPTION`

# Memoize::Expire - 用于自动过期缓存值的插件模块

用法摘要 `SYNOPSIS`
描述 `DESCRIPTION`
接口 `INTERFACE`
`TIEHASH`, `EXISTS`, `STORE`
替代方案 `ALTERNATIVES`
注意事项 `CAVEATS`
作者
另参见 `SEE ALSO`

# Memoize::ExpireFile - 用于 Memoize 过期语义测试

描述 `DESCRIPTION`

# Memoize::ExpireTest - 用于 Memoize 过期语义测试

描述 `DESCRIPTION`

# Memoize::NDBM_File - 为 Storable 使用提供 NDBM_File EXISTS 的粘接代码

描述 `DESCRIPTION`

# Memoize::SBM_File - 为 Storable 使用提供 SDBM_File EXISTS 的粘接代码

描述 `DESCRIPTION`

# Memoize::Storable - 将 Memoized 数据存储在 Storable 数据库中

描述 `DESCRIPTION`

# Module::CoreList - 随 perl 版本分发的模块列表

用法摘要 `SYNOPSIS`
描述 `DESCRIPTION`
函数 API
`first_release( MODULE )`, `first_release_by_date( MODULE )`, `find_modules( REGEX, [ LIST OF PERLS ] )`, `find_version( PERL_VERSION )`, `is_core( MODULE, [ MODULE_VERSION, [ PERL_VERSION ] )`, `is_deprecated( MODULE, PERL_VERSION )`, `deprecated( MODULE )`, `removed( MODULE )`, `removed_from_by_date( MODULE )`, `changes_between( PERL_VERSION, PERL_VERSION )`
数据结构 `DATA STRUCTURES`

```
%Memoize::CoreList::version, %Memoize::CoreList::delta, %Memoize::CoreList::released, %Memoize::CoreList::families, %Memoize::CoreList::deprecated, %Memoize::CoreList::upstream, %Memoize::CoreList::bug_tracker
```
