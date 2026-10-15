
# 534 附录 A • Solaris 到 Linux 参考表

|  |  |  |
|---|---|---|
| `towlower` | `towlower` | 将大写宽字符转换为小写。 |
| `toupper` | `toupper` | 将小写宽字符转换为大写。 |
| `truncate` | `truncate` | 将文件设置为指定的长度。 |
| `tsearch` | `tsearch` | 管理二叉查找树。 |
| `ttypename` | `ttypename` | 获取终端路径名称。 |
| `ttypename_r` | `ttypename_r` | 获取终端路径名称。 |
| `ttyslot` | `ttyslot` | 在用户统计数据库中查找当前槽位。 |
| `twalk` | `twalk` | 管理二叉查找树。 |
| `tzset` | `tzset` | 将日期和时间转换为字符串。 |
| `ualarm` | `ualarm` | 在微秒后调度信号。 |
| `ucred_free, ucred_get_get, ucred_getegid, ucred_geteuid, ucred_getgroups, ucred_getflags, ucred_getpid, ucred_getprivset, ucred_getprojid, ucred_gettrgid, ucred_getuid, ucred_getsid, ucred_getuid, ucred_getzone, ucred_size` | None | 用户凭据函数。 |
| `ulckpwdf` | `ulckpwdf` | 操作影子密码数据库锁文件。 |
| `ulltollstr` | None | 字符串转换例程。 |
| `umem_alloc, umem_cache_alloc, umem_cache_create, umem_cache_destroy, umem_cache_free, umem_debug, umem_free, umem_nofail_callback, umem_zalloc` | None | 快速、可扩展的内存操作。 |

| Solaris 函数 | Linux 函数 | 说明 |
|---|---|---|
| `ungetc` | `ungetc` | 将字节推回输入流。 |
| `ungetwc` | `ungetwc` | 将宽字符代码推回输入流。 |
| `unlockpt` | `unlockpt` | 解锁伪终端主/从设备对。 |
| `unordered` | 无 | 确定浮点数的类型。 |
| `unsetenv` | `unsetenv` | 移除环境变量。 |
| `updwtmp` | `updwtmp` | 用户计费数据库函数。 |
| `updwtmpx` | `updwtmpx` | 用户计费数据库函数。 |
| `usleep` | `usleep` | 暂停执行微秒间隔。 |
| `utmpname` | `utmpname` | 用户计费数据库函数。 |
| `utmpxname` | `utmpxname` | 用户计费数据库函数。 |
| `valloc` | `valloc` | 内存分配器。 |
| `valloc` | `valloc` | 内存分配器。 |
| `fprintf` | `fprintf` | 可变参数列表的格式化输出。 |
| `fprintf` | `fprintf` | 格式化输出转换。 |
| `vsscanf` | `vsscanf` | 转换格式化输入。 |
| `vfwprintf` | `vfwprintf` | stdarg 参数的宽字符格式化输出。 |
| `vfwscanf` | `vfwscanf` | 转换格式化宽字符输入。 |
| `vlfmt, vpfmt` | 无 | 标准格式显示错误消息并传递给日志和监控服务。 |

## A.3 基础库函数

| Solaris 函数 | Linux 函数 | 说明 |
|---|---|---|
| `printf` | `printf` | 打印可变参数列表的格式化输出。 |
| `printf` | `printf` | 格式化输出转换。 |
| `scancf` | `scanf` | 转换格式化输入。 |
| `vsprintf` | `vsprintf` | 打印可变参数列表的格式化输出。 |
| `vsprintf` | `vsprintf` | 打印可变参数列表的格式化输出。 |
| `vsprintf` | `vsprintf` | 格式化输出转换。 |
| `vsscanf` | `vsscanf` | 转换格式化输入。 |
| `vswprintf` | `vswprintf` | stdarg 参数列表的宽字符输出。 |
| `vswcanf` | `vswcanf` | 转换格式化宽字符输入。 |
| `vsyslog` | `vsyslog` | 使用 stdarg 参数列表记录日志消息。 |
| `vwprintf` | `vwprintf` | stdarg 参数列表的宽字符格式化输出。 |
| `vwscanf` | `vwscanf` | 转换格式化宽字符输入。 |
| `wait` | `wait` | 等待子进程停止或终止。 |
| `wait3` | `wait3` | 等待进程终止或停止。 |
| `wait4` | `wait4` | 等待进程终止或停止。 |
| `waitpid` | `waitpid` | 等待子进程状态改变。 |
| `waitpid` | `waitpid` | 等待进程终止或停止。 |
| `walkcontext` | 无 | 遍历 ucontext 指向的栈。 |
| `watchmalloc` | 无 | 内存分配器。 |

# 附录 A • Solaris 到 Linux 参考表

| Solaris 函数 | Linux 函数 | 说明 |
|---|---|---|
| `watof, watoi, watol, watoll` | 无 | 宽字符字符串操作。 |
| `wcrctomb` | `wcrctomb` | 将宽字符代码转换为字符（可重启动）。 |
| `wscat` | `wscat` | 宽字符字符串操作。 |
| `wcschr` | `wcschr` | 宽字符字符串操作。 |
| `wscmp` | `wscmp` | 宽字符字符串操作。 |
| `wscoll` | `wscoll` | 使用排序信息的宽字符字符串比较。 |
| `wscpy` | `wscpy` | 宽字符字符串操作。 |
| `wcsspn` | `wcsspn` | 宽字符字符串操作。 |
| `wcsetno` | 无 | 获取 EUC 编码信息。 |
| `wcsftime` | `wcsftime` | 将日期和时间转换为宽字符字符串。 |
| `wcslen` | `wcslen` | 宽字符字符串操作。 |
| `wcsncat` | `wcsncat` | 宽字符字符串操作。 |
| `wcsncmp` | `wcsncmp` | 宽字符字符串操作。 |
| `wcsnpy` | `wcsnpy` | 宽字符字符串操作。 |
| `wcspbrk` | `wcspbrk` | 宽字符字符串操作。 |
| `wcsrchr` | `wcsrchr` | 宽字符字符串操作。 |
| `wcsrtombs` | `wcsrtombs` | 将宽字符字符串转换为字符字符串（可重启动）。 |

## A.3 基础库函数

| Solaris 函数 | Linux 函数 | 说明 |
|---|---|---|
| `wcsspn` | `wcsspn` | 宽字符字符串操作-n |
| `wcsstr` | `wcsstr` | 查找宽字符子字符串 |
| `wcstod` | `wcstod` | 将宽字符字符串转换为浮点数 |
| `wcstof` | `wcstof` | 将宽字符字符串转换为浮点数 |
| `wcstoimax` | `wcstoimax` | 将宽字符字符串转换为整数类型 |
| `wcstok` | `wcstok` | 宽字符字符串操作 |
| `wcstol` | `wcstol` | 将宽字符字符串转换为长整数 |
| `wcstold` | `wcstold` | 将宽字符字符串转换为浮点数 |
| `wcstoll` | `wcstoll` | 将宽字符字符串转换为长整数 |
| `wcmstombs` | `wcmstombs` | 将宽字符字符串转换为字符字符串 |
| `wcstol` | `wcoul` | 将宽字符字符串转换为无符号长 |
| `wcstoll` | `wcstoll` | 将宽字符字符串转换为无符号长 |
| `wcstumax` | `wcstumax` | 将宽字符字符串转换为整数类型 |
| `wcstring` | `wcstring` | 宽字符操作 |
| `dcswcs` | `dcswcs` | 宽字符字符串操作 |
| `wcswidth` | `wcswidth` | 宽字符宽度 |
| `wcsxfrm` | `wcsxfrm` | 宽字符转换 |
| `wctob` | `wctob` | 字节转换 |

## A.3 基础库函数

| Solaris 函数 | Linux 函数 | 说明 |
|---|---|---|
| `wctomb` | `wctomb` | 字节转换。 |
| `wctrans` | `wctrans` | 定义映射。 |
| `wctype` | `wctype` | 定义字符类。 |
