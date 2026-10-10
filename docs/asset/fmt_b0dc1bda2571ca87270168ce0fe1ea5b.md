
# perl5202delta - perl v5.20 哪些新特性

## 描述
不兼容更改
- 模块和指令集
- 已更新的模块和指令集

## 文档
- 新增文档
- 现有文档的更改

## 诊断
- 现有诊断的更改

## 测试
## 平台支持
- 回收的平台
- 特定于平台的说明：EBCDIC
- 已选的错误修复
- 错误
## 致谢
## 报告错误
## 参见另请

# perl5201delta - perl v5.20.1 哪些新特性

## 描述
不兼容更改
- 性能增强
- 模块和指令集
- 已更新的模块和指令集

## 文档
- 现有文档的更改

## 诊断
- 现有诊断的更改

## 配置与编译
## 平台支持
- 特定于平台的说明：Android, Solaris, VMS, Windows

## 内部更改
## 已选的错误修复
## 致谢

# perl5200delta - perl v5.20.0 哪些新特性

## 描述
## 核心增强
- 程序签名：`sub` 现在带有 `prototype` 属性
- 更一致的原型解析
- `rand` 现在使用一致的随机生成器
- 新的切片语法
- 后缀引用
- 现在支持 Unicode 6.3
- 正则表达式属性 `p}`
- 更好的 64 位支持
- `uselocate` 现在支持 UTF-8 区域设置
- `uselocate` 现在可以在没有区域设置的系统中编译
- 更多的区域设置初始化选项
- 添加了 `-DL` 运行选项用于跟踪设置
- `-F` 意味着 `-a` 和 `-n`

## 安全
- 避免在解析期间读取已释放的内存

## 不兼容更改
- `do` 不再能调用子程序
- 引用类的转义更改
- 污染发生的情况更多；现在符合文档
- 对于非 Unicode 代码点，`{p}, {P}` 匹配发生了变化
- `{p All}` 已扩展以匹配所有代码点
- `Data::Dumper` 的输出可能会 way
- 本地小数点字符不再泄漏到 `uselocal` 范围之外
- 将 Windows 套接错误代码赋值给 `$` 现在优先使用 `errno.h` 值而非 `WSAGLastError(0)` 值
- 函数 `PerIO_vsprint` 和 `PerIO_sprint`

## 弃用
- `/AC/` 字符类
- 变量名中的字面控制字符
- `$/` 中引用非整数和非正整数
- POSIX 中的字符匹配例程
- 解释器线程现在不再被鼓励

## 移除的模块
- CGI 及其相关的:: packages, inc::latest, Package::Constants, Module::Build
及其相关的 Module::Build:: packages

## 移除的工具
- find2perl, s2p, a2p
## 性能增强
## 模块和指令集
## 新增模块和指令集
## 已更新的模块和指令集
## 文档
- 新增文档
- 现有文档的更改

## 诊断
- 新增诊断
- 现有诊断的更改

## 工具类更改
## 配置与编译
## 测试
## 平台支持
- 新平台：Android, Bitrig, FreeMiNT, Synergy

# 已停止平台
- sfio, AT&T 3b1, DG/UX, EBCDIC

# 平台特定说明
- Cygwin, GNU/Hurd, Linux, Mac os, MidnightBSD, 混合字节平台, vms, Win32, WinCE

## 内部更改
选定的错误修复

## 正则表达式
Perl 5 调试器和 `-d`
词法子程序

## 其他所有
已知问题 遗嘱 鸣谢 报告错误 另请参 (SEE ALSO)

# perl5184-delta - perl v5.18.4 新特性

### 描述

### 模块与指令
- 更新的模块与指令

### 平台支持
### 平台特定说明
- Win32

选定的错误修复 致谢 报告错误 另请参 (SEE ALSO)

# perl5182-delta - perl v5.18.2 新特性

### 描述

### 模块与指令
- 更新的模块与指令

### 文档
- 现有文档的更改
选定的错误修复 致谢 报告错误 另请参 (SEE ALSO)

# perl5181delta - perl v5.18.1 新特性

### 描述

### 不兼容性更改
### 模块与指令
- 更新的模块与指令

### 平台支持
### 平台特定说明
- AIX, MidnightBSD

选定的错误修复 致谢 报告错误 另请参 (SEE ALSO)

# perl5180delta - perl v5.18.0 新特性

### 描述

### 核心增强
- 实验性功能的新机制
- 哈希重构

### 升级到 Unicode 6.2
- 字符别名现在可以包含非 Latin1 范围字符
- 新的 DTrace 探针

### `${LAST_FH}`
- 正则表达式集合操作
词法子程序
计算标签
更多 CORE：subs
- 带有负信号名称的 `kill`

## 安全
- 另请参：哈希重构
- 文档中的 `Storable` 安全警告
- `Locale::maketetext` 允许通过恶意模板注入代码
- 避免带有负数计数调用 mset

## 不兼容性更改
- 另请参：哈希重构
- 未知的字符名 `"\N{...}"` 现在是语法错误
- 对于 `"\N{...}"` 中正确废弃的字符，字符别名现在是错误
- `{BELL}` 指向 U+F514 而不是 U+0007

## 正则表达式中多字符不区分大小写匹配的新限制
### 括号字符类
- `given` 现在是全局 `$_` 的别名
- smartmatch 系列功能现在是实验性的
- 词法 `_`，现在是实验性的
- 带有 `$/ = \N` 的 `readline()` 现在读取 N 个字符，而不是 N 个字节
- 覆盖的 `glob` 现在传递一个参数
- Here-doc 解析
- 字母数字选项 at 处与正则表达式的结束分隔符分离
- `qw(...)` 不再可以用作括号
- 词法警告与默认警告的交互
- `state sub` 和 `our sub`
- 存储在 environ 中的定义值被强制转换为字节字符串
- `require` 对于无法访问的文件会报错
- `gv_fetch_th_*` 和 SUPER
- `split` 第一个参数的解释更具一致性

## 废弃
# 模块移除
- encoding, Archive::Exact, B::Lint, B::Lint::Debug, CPANPLUS 以及所有包含 CPANPLUS*: 的模块, Devel::InnerPackage, Log::Message, Log::Message::Config, Log::Message::Handlers, Log::Message::Item, Log::Message::Simple, Module::Pluggable, Module::Pluggable::Object, Object::Accessor, Pod::LaTeX, Term::UI, Term::UI::History

# 废弃实用工具
- cpang, cpan-run-perl, cpan2dist,pod2latest
- PL_sv_objcount
- 在带有 /x 的模式中应转义五个额外的字符
- 带有意外空格的用户定义字符
- 各种 XS 可调用函数现在已废弃
- 正则表达式中反斜杠的某些罕用用法已废弃
- 分割正则表达式中的标记 `?` 和 `*`
- PrePerIO 实现

## 未来废弃
DG/UX, 下一步性能增强模块与指令

## 新模块与指令
- 更新的模块与指令
- 已移除的模块与指令

## 文档
- 现有文档的更改
- 新诊断
- 现有诊断的更改

## 实用工具更改
配置与编译测试

## 平台支持
### 已停止平台
- BeOS, UTS Global, Vm/ESA, MPE/IX, EPOC, Rhapsody

# 平台特定说明
内部更改 选定的错误修复 已知问题 鸣谢 报告错误 另请参 (SEE ALSO)

# perl5163delta - perl v5.16.3 新特性

### 描述
### 核心增强
### 安全
- CVE-2013-1667: 任意哈希键导致的内存耗尽
- 长字符串上 io10 的回绕
- Encode 中的内存泄漏

## 不兼容性更改 废弃
### 模块与指令
- 更新的模块与指令

## 已知问题 鸣谢 报告错误 另请参 (SEE ALSO)

# perl5162delta - perl v5.16.2 新特性

### 描述

### 不兼容性更改
### 模块与指令
- 更新的模块与指令

### 配置与编译
- ls 不再会混淆配置
- 彩色化

### 平台支持
### 平台特定说明
- AIX

选定的错误修复 固定 /h/ 与 [\h/] 的等效性 已知问题 鸣谢 报告错误 另请参 (SEE ALSO)

# perl5161delta - perl v5.16.1 新特性

### 描述
### 安全
- Scalar-List-Util 中偏移二的错误已修复

## 不兼容性更改 模块与指令
- 更新的模块与指令
### 配置与编译
### 平台支持
### 平台特定说明
- VMS

选定的错误修复 已知问题 鸣谢 报告错误

# perl5160delta - perl v5.16.0 新特性

### 描述
## 注意
核心增强
- use VERSION

### 新内置
- Unicode 支持

### 更改
- 特殊变量
- 调试器

### 安全
- 文档中的 `Storable` 安全警告
- `Locale::maketetext` 允许通过恶意模板注入代码
- 避免带有负数计数调用 mset

## 不兼容性更改
- 未知的字符名 `"\N{...}"` 现在是语法错误
- 读取缓冲区末尾

### 废弃
- 使用 utf8_char 和 utf8-to
- 文件句柄
- utf8_to

## 未来废弃
# 核心模块
- 平台
未来废弃

### 不兼容性更改
- `overloading` 指令
- smartmatch 系列功能现在是实验性的
- Unicode 6.1 不兼容性
- 某些废弃属性
- Tied scalars
- 存储在 environ 中的定义值被强制转换为字节字符串
- `require` 对于无法访问的文件报错
- `gv_fetch_th_*` 和 SUPER
- `split` 第一个参数的解释更具一致性

### 性能增强
模块与指令

# 废弃模块
- Version::Requirements
- 警告，重定义
- 警告，`未初始化`
- 引用

## 其他显著修复
- 已知问题 鸣谢 报告错误 另请参 (SEE ALSO)

## 文档
- 新诊断
- 现有诊断的更改

## 诊断
- 新错误
### 实用工具更改
- 配置与编译

## 平台支持
### 平台特定说明
- 内部更改
选定的错误修复

## 正则表达式
- 词法子程序

## 安全
- 另请参：哈希重构
- 文档中的 `Storable` 安全警告
- `Locale::maketetext` 允许通过恶意模板注入代码
- 避免带有负数计数调用 mset

## 不兼容性更改
- 另请参：哈希重构
- 未知的字符名 `"\N{...}"` 现在是语法错误
- 对于 `"\N{...}"` 中正确废弃的字符，字符别名现在是错误
- `{BELL}` 指向 U+F514 而不是 U+0007
