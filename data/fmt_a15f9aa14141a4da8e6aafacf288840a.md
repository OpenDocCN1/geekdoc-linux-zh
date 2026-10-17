
信号列表
正常信号, 错误信号, 旧接口信号

`OTHER\untrapped`, any, signal, nuer

示例

# `sort` - 用于控制 `sort()` 行为的 Perl 编译指令

## 用法
## 描述
## 注意事项

# `strict` - 用于限制不安全构造的 Perl 编译指令

## 用法
## 描述

`strict refs`, `strict vars`, `strict subs`
## 历史
`threads->tid` `threads->handle()`

# 用于预声明子程序的 Perl 编译指令

## 用法
## 描述

# `threads` - 基于解释器的线程

## 版本
## 警告
## 用法
## 描述

```
$thr = threads->create(FUNCTION, args), $thr->join(), $thr->->join(), $thr->detach(), threads-
detetach(), threads->self(boolean), $thr->tid($tid), threads->tid(all), "$thr", threads->object($tid),
thrs->yield(boolean), threads->list($list), threads->list(threads::all), threads-
list(threads:running), threads->list(joinable), $thr1->equal($thr2), async
BLOCK; $thr->error(), $thr->_handle(), threads->_handle()
```

## 退出线程
`threads->exit()`, `threads->exit(status)`, `die()`, `exit(status)`, `use threads 'exit' = 'threads_only'`, `threads->create({'exit' = 'thread_only'})`, `$thr-set_thread_exit_only(boolean)`, `threads->set_thread_exit_only(boolean)`

## 线程状态
`$thr->is_running()`, `$thr->is_joinable()`, `$thr->is_detached()`, `threads-is_detached()`

## 线程上下文
### 显式上下文
### 隐式上下文
`$thr->wantarrray()`
`threads->wantarray()`

## 线程栈
`threads->get_stack_size()`, `$size = $thr->get_stack_size()`, `use threads ('stack_size' = VALUE)`,
`$old_size = threads->set_stack_size($new_size)`, `use threads ('stack_size' = VALUE);`
`ENV{'PERL_5_THREAD_STACK_SIZE'} = threads->create({'stack_size' = VALUE}, FUNCTION, ARGS)`, `$thr2 = $thr1->create(FUNCTION, args)`

## 线程信号
`$thr->kill('SIG...')`

## 警告
Perl 在带有活动线程的情况下退出；线程创建失败：pthread create 返回
#, 线程异常终止：... 使用最小栈大小 #, 线程创建 pheiled：pthread_set_stack_size(size) 返回 22 错误 此 perl 编译不支持
无法更改执行的栈大小，在没有信号的情况下无法创建线程，
未识别的信号 : 缺陷与局限 线程安全模块，使用非线程安全模块，内存管理，父子线程，当前工作目录，Environ\Variables，在特殊块内部创建线程，
不安全的信号，Perl 编译时使用了 `PERL_OLD_SIGNALS`（见 `perl -V`），环境变量 `PERL_SIGNAL` 设置为不安全（见 `perlrun` 中的 "PERL_SIGNALS"），使用了 `Perl::Unsafe::is` 模块，从线程返回闭包，从线程返回对象，
线程中的 `END` 块，打开目录句柄，Perl 缺陷和 CPAN 版本的 `threads` 要求另见 作者 致谢

# `threads::shared` - 用于在线程间共享数据结构的 Perl 扩展

## 版本
## 用法
## 描述
## 导出
## 函数

```
share VARIABLE, shared_clone REF, is_shared VARIABLE, lock VARIABLE, cond_wait
VARIABLE, cond_wait CONVAR, LOCKVAR, cond_tidwait VARIABLE, ABS_TIMEOUT,
cond_tidwait CONVAR, ABS_TIMEOUT, LOCKVAR, cond_signal VARIABLE,
cond_broadcast VARIABLE
```

## 对象
## 注释
## 警告
## 缺陷与局限
## 另见
## 作者
## 许可证

在未锁变量上调用了 `cond_broadcast()`，在未锁变量上调用了 `cond_signal()`

# `utf8` - 用于在源代码中启用/禁用 UTF-8（或 UTF-EBCDIC）的 Perl 编译指令

## 用法
## 描述
## 工具函数

```
$num_octets = utf8::upgrade($string), $success =
utf8::downgrade($string, $fail_ok], utf8::encode($string), $success =
utf8::decode($string), $unicode = utf8::native_to_unicode($code_point),
$num_octets = utf8::upgrade($string), $success =
utf8::downgrade($string, $fail_ok], utf8::encode($string), $success =
utf8::decode($string), $unicode = utf8::native_to_unicode($code_point),
```

# `strict` - 用于限制不安全构造的 Perl 编译指令

# ..._ets = utf8::::ng

`($string, $fail_ok`

`$8 = utf8::decode`

## 用法

## 描述

`strict refs`, `strict vars`, `strict subs`

## 历史

`threads->tid` `threads->handle()`

# 用于预声明子程序的 Perl 编译指令

## 用法

## 描述

# `threads` - 基于解释器的线程

## 版本

## 警告

## 用法

## 描述

`trap PLUGINS`

## 示例插件

## 另请

# `App::Prove::State` - 用于 `prove` 命令的状态存储。

## 版本

## 描述

## 摘要

## 方法

### 类方法

`store`, `extensions`（可选）, `result_class`（可选）

`result_class` `extensions` `result` 实例方法 `last`, `failed`, `passed`, `all`, `hot`,

`todo`, `slow`, `fast`, `new`, `old`, `save`

# `App::Prove::Result` - 单个测试套件的结果。

## 版本

## 描述

## 摘要

## 方法

### 类方法

`state_version` `test_class`

# `App::Prove::State::Test` - 单个测试结果。

## 版本

## 描述

## 摘要

## 方法

### 类方法

### 实例方法

# `Archive::Tar` - 用于操作 tar 归档的模块

## 摘要

## 描述

## 对象方法

`Archive::Tar->new([$file, $compressed])`
