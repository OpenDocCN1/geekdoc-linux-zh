
| `vsprintf`, `vsnprintf` | `vsprintf`, `vsnprintf` | 打印参数列表的格式化输出。 |

| `vscanf`, `vscanf`, `vsscanf` | `vscanf`, `vscanf`, `vsscanf` | 格式化输入转换为参数。 |

| HP-UX 库调用 | Linux 等效 | 描述 |

| :--- | :--- | :--- |

| `vwprintf`, `vwfprintf`, `vswprint` | `vwprintf`, `vwfprintf`, `vswprint` | 输出格式化输出。 |

| `vwprintw` | `vwprintw` (`libncurses`) | 在窗口中打印格式化输出。 |

| `vwscanw` | `vwscanw` (`libncurses`) | 从窗口中转换格式化输入。 |

| `wborder` | `wborder` (`libncurses`) | 从单字节字符和渲染绘制边界。 |

| `wcrtomb` | `wcrtomb` | 将宽字符代码转换为字符。 |

| `wcsftime` | `wcsftime` | 将日期和时间转换为宽字符串。 |

| `wctob` | `wctob` | 在单字节和宽字符之间转换。 |

| `wcsrtombs` | `wcsrtombs` | 将宽字符串转换为字符串。 |

| `wcstod` | `wcstod` | 将宽字符串转换为双精度数字。 |

| `wcstoimax`, `wcstoumax` | `wcstoimax`, `wcstoumax` | 将宽字符串转换为长整型。 |

| `wcstol`, `wcscoll`, `wcstoul`, `wctoull` | `wcstol`, `wcscoll`, `wcstoul`, `wctoull` | 将宽字符串转换为整数。 |

| `wcscat`, `wscat`, `wcscmp`, `wscncmp`, `wcscpy`, `wscnpy` | `wcscat`, `wscat`, `wcscmp`, `wscncmp`, `wcscpy`, `wscnpy` | 宽字符串操作。 |

| `wcslen`, `wschr`, `wcsrchr`, `wcsstr`, `wcspbrk`, `wcsspn`, `wcscpn`, `wcstok`, `wcstok_r`, `nl_wcsncmp` | `wcslen`, `wschr`, `wcsrchr`, `wcsstr`, `wcspbrk`, `wcsspn`, `wcscpn`, `wcstok` | |

## 附录 C • HP-UX 到 Linux 的参考表

| HP-UX 库调用 | Linux 等效项 | 描述 |

|---|---|---|

| `iswalpha`, `isupper`, `iswlower`, `iswdigit`, `iswxdigit`, `iswalnum`, `iswspace`, `iswpunct`, `iswprint`, `isgraph`, `iswcntrl`, `isctype` | `iswalpha`, `isupper`, `iswlower`, `iswdigit`, `iswxdigit`, `iswalnum`, `iswspace`, `iswpunct`, `iswprint`, `isgraph`, `iswctype` | 宽字符分类函数。 |

| `wmemchr`, `wmemcmp`, `wmemcpy`, `wmemmove`, `wmemset` | `wmemchr`, `wmemcmp`, `wmemcpy`, `wmemmove`, `wmemset` | 基于宽字符的内存操作。 |

| `wordexp`, `wordfree` | `wordexp`, `wordfree` | 执行单词扩展。 |

| `wcntrl` | `wcntrl` | 生成宽字符的可打印表示。 |

| `xdr_control`, `xdr_getpos`, `xdr_inline`, `xdrrec_endofrecord`, `xdrrec_eof`, `xdrrec_readbytes`, `xdrrec_skiprecord`, `xdr_setpos`, `xdr_sizeof` | `xdr_getpos`, `xdr_setpos`, `xdr_inline`, `xdrrec_endofrecord`, `xdrrec_skiprecord`, `xdrrec_eof` | 外部数据表示的库程序。 |

| `xdr_array`, `xdr_bytes`, `xdr_opaque`, `xdr_pointer`, `xdr_reference`, `xdr_string`, `xdr_string`, `xdr_vector`, `xdr_wrapping` | `xdr_array`, `xdr_bytes`, `xdr_opaque`, `xdr_pointer`, `xdr_reference`, `xdr_string`, `xdr_string`, `xdr_vector`, `xdr_wrapping` | 外部数据表示的库程序。 |

| `xdr_destroy`, `xdrmem_create`, `xdrrec_create`, `xdrstdio_create` | `xdr_destroy`, `xdrmem_create`, `xdrrec_create`, `xdrstdio_create` | 外部数据表示流创建的库程序。 |

## HP-UX 和 Linux 库 API 比较表

| HP-UX 库调用 | Linux 等效项 | 描述 |

|---|---|---|

| `xdr_bool`, `xdr_char`, | `xdr_bool`, `xdr_char`, | 外部数据表示的库程序 |

| `xdr_double`, | `xdr_double`, | 表示。 |

| `xdr_enum`, | `xdr_enum`, `xdr_float`, | | |

| `xdr_float`, `xdr_free`, | `xdr_free`, `xdr_int`, | | |

| `xdr_hyper`, `xdr_int`, | `xdr_long`, `xdr_u_int`, | | |

| `xdr_long`, | `xdr_u_long`, | | |

| `xdr_longlong_t`, | `xdr_u_char`, | | |

| `xdr_quadruple`, | `xdr_short`, | | |

| `xdr_short`, | `xdr_u_short`, | | |

| `xdr_u_char`, | `xdr_void` | | |

| `xdr_u_hyper`, | | | |

| `xdr_u_int`, | | | |

| `xdr_u_long`, | | | |

| `xdr_u_longlong_t`, | | | |

| `xdr_u_short`, | | | |

| `xdr_void` | | | |

| `y0`, `y0f`, `y1`, `y1f`, | `y0`, `y0f`, `y1`, `y1f`, | 第二类 Bessel 函数。 |

| `yn`, `nyf` | `yn`, `nyf` | | |

| `yp_all`, `yyp_bind`, | `yp_all`, `yyp_bind`, | 网络信息服务客户端 |

| `yp_first`, | `yp_first`, | 接口。 |

| `yp_get_default_` | `yp_get_default_` | | |

| `domain`, | `domain`, | | |

| `yp_master`, | `yp_master`, | | |

| `yp_match`, `yp_next`, | `yp_match`, `yp_next`, | | |

| `yp_order`, | `yp_order`, | | |

| `yp_unbind`, | `yp_unbind`, | | |

| `yperr_string`, | `yperr_string`, | | |

| `yyprot_err` | `yyprot_err`^22 | | |

| `yppasswd` | `yppasswd`^23 | 在网络信息服务 (NIS) 中更新用户密码。 |

| `yupdate` | `yupdate`^24 | 修改 NIS 信息。 |

## 附录 C • HP-UX 到 Linux 的参考表

13 Linux 上最接近等效项是 `crypt`。

14 查看 `readelf` 或 `objdump` 工具。

15 在 `glibc` 中声明为 `volatile int`。

16 查看 `rpm/db.h`。

17 查看 `http://josefsson.org/gss/manual/`

18 `ndbm.h`

19 查看 `lsof` 源码以获取 `nlist_private` 示例。

20 `www.openslp.org/`

21 通过 `libncurses` 库支持。

22 未成文档的 Linux 调用。查看 `/usr/include/rpcscvc/ypclint.h`。

23 未成文档的 Linux 调用。查看 `/usr/include/rpcscvc/ypasswd.h`。

24 未成文档的 Linux 调用。查看 `/usr/include/rcpsvc/ypupd.h`。

# 附录 D • POWER on Linux

## Linux on POWER

当前的 IBM POWER 微处理器是 64 位架构，运行 64 位操作系统。然而，Linux on POWER 提供了与现有 32 位应用程序的完全兼容，并支持 64 位应用程序。

- Linux on POWER 使用 `ELF` 格式。
