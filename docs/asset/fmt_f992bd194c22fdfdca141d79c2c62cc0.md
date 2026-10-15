
## `rpc_svc_err`：服务器侧过程调用错误的库程序。

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `sverr_auth` | `sverr_auth` | |
| `sverr_decode` | `sverr_decode` | |
| `sverr_noproc` | `sverr_noproc` | |
| `sverr_noprog` | `sverr_noprog` | |
| `sverr_progvers` | `sverr_progvers` | |
| `sverr_systemerr` | `sverr_systemerr` | |
| `sverr_weak_auth` | `sverr_weak_auth` | |

## `rpc_svc_reg`：注册服务器的库程序。

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `svc_reg` | `svc_register` | |
| `svc_unreg` | `svc_unregister` | |
| `svc_auth_reg` | | |

## `rpc_xdr`：远程过程调用的 XDR 库程序。

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `xdr_accepted_reply` | `xdr_accepted_reply` | |
| `xdr_authsys_parms` | `xdr_authsys_parms` | |
| `xdr_callhdr` | `xdr_callhdr` | |
| `xdr_callmsg` | `xdr_callmsg` | |
| `xdr_opaque_auth` | | |
| `xdr_rejected_reply` | `xdr_rejected_reply` | |
| `xdr_replmsg` | `xdr_replmsg` | |

## RPC 绑定服务的库程序。

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `rpcb_getmaps` | `pmap_set` | |
| `rpcb_getaddr` | `pmap_unset` | |
| `rpcb_gettime` | `pmap_rmtcall` | |
| `rpcb_rmtcall` | `pmap_getport` | |
| `rpcb_set` | `pmap_getports` | |
| `rpcb_unset` | | |

## 其他函数

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `sqrt`, `sqrtf`, `sqrtl` | 无 | 倒数函数。 |
| `rstat`, `havedisk` | 无 | 从远程机器获取性能数据。 |
| `ruserok` | `ruserok` | 返回指向远程命令的流。 |
| `rwall` | | 写入指定的远程。 |

## HP-UX 调用 Linux 等效函数描述

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `scalb`, `scalbf`, `scalbl` | `scalb`, `scalbf`, `scalbl` | 进制无关的浮点数指数比例。 |
| `scalbln`, `scalblnf`, `scalblnl` | `scalbln`, `scalblnf`, `scalblnl` | 进制无关的浮点数指数。 |
| `scalbn`, `scalbnf`, `scalnl` | `scalbn`, `scalbnf`, `scalnl` | 进制无关的浮点数指数比例。 |
| `scandir`, `alphasort` | `scandir`, `alphasort` | 扫描目录。 |
| `scancf`, `fscanf`, `scanf` | `scancf`, `fscanf`, `scanf` | 格式化输入，从流文件读取。 |
| `scr_dump`, `scr_init`, `scr_restore`, `scr_set` | `scr_dump`, `scr_init`, `scr_restore`, `scr_set` | 屏幕输入/输出函数。 |
| `scrl`, `wscrl` | 无 | 增强的滚动窗口函数。 |
| `scroll` | `scroll` | 滚动 curses。 |
| `scrolok` | `scrolock` | 终端输出控制函数。 |
| `secdef` | 无 | 安全默认配置程序。 |
| `secure_rpc`, `authdes_getucred`, `authdes_secreate`, `getname`, `host2name`, `key_decryptssession`, `key_encryptssession`, `key_geqq`, `key_setsecret`, `key_secretkey_is_set`, `netname2host`, `netname2user`, `user2name` | `secure_rpc`, `authdes_getucred`, `getname`, `host2name`, `key_decryptssession`, `key_encryptssession`, `key_geqq`, `key_setsecret`, `key_secretkey_is_set`, `netname2host`, `netname2user`, `user2name` | 安全过程调用的库程序。 |
| `set_term` | `set_term` (`libncurses`) | 切换屏幕。 |

## C4 HP-UX 与 Linux 库 API 比较表

| HP-UX 调用 | Linux 等效函数 | 描述 |
|---|---|---|
| `setaclentry`, `fsetaclentry` | | 添加、修改或删除访问列表列表。 |
| `setbuf`, `setvbuf`, `setbuf_unlocked` | `setbuf`, `setvbuf` | 为流文件分配缓冲区。 |
| `setbwent` | 无 | 向新的 wtmps 和 btmps 数据库写入记录。 |
| `setcat` | 无 | 设置默认消息目录。 |
| `setcchar` | `setcchar` | 从宽字符和变体设置 `char_t`。 |
| `setclock` | 无 | 设置系统时钟值。 |
| `setkey`, `setkey_r` `setlabel` | 无 | 生成哈希加密。 |
| `setlocale_r`, `getocale`, `getocale_r` | `setocale` | 为格式化程序定义标签。设置和获取程序的区域。 |
| `shl_load`, `shl_definesym`, `shl_findsym`, `shl_get`, `shl_get_r`, `shl_gethandle_r`, `shl_getsymbols`, `shl_unload`, `dldgetenv` | `dladdr`, `dlclose`, `dlerror`, `dlopen`, `dlsym`, `dlvsym` | 显式加载共享库。 |
| `signbit` | `signbit` | 浮点数符号判定。 |
| `sigpause` | `sigpause` | 原子地释放阻塞的信号并等待中断。 |
| `sigset`, `signhold`, `sigrelse`, `sigignore`, `sigpause` | `sigset`, `sighold`, `sigrelse`, `sigignore`, `sigpause` | 信号管理。 |

## HP-UX 库调用

| HP-UX 库调用 | Linux 等效 | 描述 |
|---|---|---|
| `sigemptyset` | `sigemptyset` | POSIX 信号集操作 |
| `sigfillset` | `sigfillset` | |
| `sigaddset` | `sigaddset` | |
| `sigdelset` | `sigdelset` | |
| `sigismember` | `sigismember` | |
| `sin`, `sinf`, `sinl` | `sin`, `sinf`, `sinl` | 正弦函数。 |
| `sinw`, `sinq` | | |
| `sincos`, `coscof` | `sincos`, `coscof` | 同时计算正弦和余弦。 |
| `sincos`, `sincosw` | `sincos` | |
| `sincosq` | | |
| `sind`, `sindf` | None | 角度作为参数的正弦函数。 |
| `sinh`, `sinhf`, `sinhhl` | `sinh`, `sinhf`, `sinhhl` | 双曲正弦函数。 |
| `sleep` | `sleep` | 暂停执行一段间隔。 |
| `slk_attroff` | `slk_attroff` | 软标签程序。 |
| `slk_attr_off` | `slk_attr_off` | |
| `slk_attron` | `slk_attron` | |
| `slk_attr_on` | `slk_attr_on` | |
| `slk_attrset` | `slk_attrset` | |
| `slk_attr_set` | `slk_attr_set` | |
| `slk_clear`, `slk_color` | `slk_clear`, `slk_color` | |
| `slk_init`, `slk_label` | `slk_init`, `slk_label` | |
| `slk_noutrefresh` | `slk_noutrefresh` | |
| `slk_refresh` | `slk_refresh` | |
| `slk_restore` | `slk_restore` | |
