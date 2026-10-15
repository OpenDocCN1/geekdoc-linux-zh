
## 429

`system-var` 配置变量的名称，其值可以通过 `confstr(3)` 或 `sysconf(3)` 获取。下表中的值都受支持。

| 变量 | 支持 |
| :--- | :--- |
| ARG_MAX | POSIX2_C_BIND |
| BC_BASE_MAX | POSIX2_C_DEV |
| BC_DIM_MAX | POSIX2_C_VERSION |
| BC_SCALE_MAX | POSIX2_CHAR_TERM |
| BC_STRING_MAX | POSIX2_COLL_WEIGHTS_MAX |
| CHAR_BIT | POSIX2_EXPR_NEST_MAX |
| CHAR_MAX | POSIX2_FORT_DEV |
| CHAR_MIN | POSIX2_FORT_RUN |
| CHARCLASS_NAME_MAX | POSIX2_LINE_MAX |
| CHILD_MAX | POSIX2_LOCALEDEF |
| CLK_TCK | POSIX2_RE_DUP_MAX |
| COLL_WEIGHTS_MAX | POSIX2_SW_DEV |
| CS_PATH | POSIX2_UPE |
| EXPR_NEST_MAX | POSIX2_VERSION |
| INT_MAX | RE_DUP_MAX |
| INT_MIN | SCHAR_MAX |
| LFS64_CFLAGS | SCHAR_MIN |
| LFS64_LDFLAGS | SHRT_MAX |
| LFS64_LIBS | SHRT_MIN |
| LFS64_LINTFLAGS | SSIZE_MAX |
| LFS_CFLAGS | STREAM_MAX |
| LFS_LDFLAGS | TMP_MAX |
| LFS_LIBS | TZAME_MAX |
| LFS_LINTFLAGS | UCHAR_MAX |
| LINE_MAX | UINT_MAX |
| LONG_BIT | ULONG_MAX |
| LONG_MAX | USHR_MAX |
| LONG_MIN | WORD_BIT |
| MB_LEN_MAX | XBS5_ILP32_OFF32 |
| NGROUPS_MAX | XBS5_ILP32_OFF32_CFLAGS |
| NL_ARGMAX | XBS5_ILP32_OFF32_LDFLAGS |
| NL_LANGMAX | XBS5_ILP32_OFF32_LIBS |
| NL_MSGMAX | XBS5_ILP32_OFF32_LINTFLAGS |
| NL_NMAX | XBS5_ILP32_OFFBIG |
| NL_SETMAX | XBS5_ILP32_OFFBIG_CFLAG |
| NL_TEXTMAX | XBS5_ILP32_OFFBIG_LDLFAG |
| NZERO | XBS5_ILP32_OFFBIG_LIBS |
| OPEN_MAX | XBS5_ILP32_OFFBIG_LINTFLAGS |
| _POSIX_ARG_MAX | XBS5_LP64_064 |
| _POSIX_CHILD_MAX | XBS5_LP64_064_CFLAG |
| _POSIX_JOB_CONTROL | XBS5_LP64_064_LDLFAG |
| _POSIX_LINK_MAX | XBS5_LP64_064_LIBS |
| _POSIX_MAX_CANON | XBS5_LP64_064_LINTFLAGS |
| _POSIX_MAX_INPUT | XBS5_LPBIG_OFFBIG |
| _POSIX_NAME_MAX | XBS5_LPBIG_OFFBIG_CFLAG |
| _POSIX_NGROUPS_MAX | XBS5_LPBIG_OFFBIG_LDLFAG |
| _POSIX_OPEN_MAX | XBS5_LPBIG_OFFBIG_LINTFLAGS |
| _POSIX_PATH_MAX | XBS5_LPBIG_OFFBIG |
| _POSIX_PIPE_BUF | _XOPEN_CRYPT |
| _POSIX_SAVED_IDS | _XOPEN_ENH_I18N |
| _POSIX_SSIZE_MAX | _XOPEN_LEGACY |
| _POSIX_STREAM_MAX | _XOPEN_SHM |
| _POSIX_TZNAME_MAX | _XOPEN_VERSION |
| _POSIX_VERSION | _XOPEN_XCU_VERSION |
| POSIX2_BC_BASE_MAX | _XOPEN_XPG2 |
| POSIX2_BC_DIM_MAX | _XOPEN_XPG3 |
| POSIX2_BC_SCALE_MAX | _XOPEN_XPG4 |
| POSIX2_BC_STRING_MAX | |

符号 `PATH` 也被识别，其产生的值与 `conf()` 名称 `CS_PATH` 相同。

## Usage

关于 `getconf` 在遇到大于或等于 2 GB (2^31 字节) 文件时的行为描述，请参见 `largfile(5)`。

## Examples

以下示例显示了 `getconf` 输出的前几行：

```
-a getconf -a

AIO_LISTIO_MAX:      256

AIO_MAX:               undefined
```

## getconf

```
AIO_PRIO_DELTA_MAX: 0

ARG_MAX: 1048320

ATEXIT_MAX: 32

BC_BASE_MAX: 99

BC_DIM_MAX: 2048

BC_SCALE_MAX: 99

BC_STRING_MAX: 1000

CHARCLASS_NAME_MAX: 14

CHAR_BIT: 8

CHAR_MAX: 127

CHAR_MIN: -128

...
```

以下示例返回 `NGROUPS_MAX` 的值：
```
getconf NGROUPS_MAX

16
```

以下示例返回特定目录的 `NAME_MAX` 值：
```
getconf NAME_MAX /usr

255
```

以下示例显示了如何谨慎地处理未指定的结果：
```
value=$(getconf PATH_MAX /usr);

if [ "$value" = "undefined" ]; then

  echo PATH_MAX in /usr is infinite.

else

  echo PATH_MAX in /usr.

fi
```

> 注意 — `sysconf(_SC_POSIX_BIND)` 和 `systemconf(_SC_POSIX_BIND)` 在 C 程序中根据编译或执行情况给出不同的答案。

## Environment Variables

关于影响 `getconf` 执行的变量，参见 `environ(5)`：`LC_TYPE`、`LC_MESSAGES` 和 `NL_PATH`。

## Exit Status

- 0：指定的变量有效且已成功写入其状态信息。
- >0：发生了错误。

## Attributes

关于以下属性，参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability | SUN |

## See Also

`pathconf(2)`, `sysconf(3)`, `attributes(5)`, `environ(5)`, `getfacl(5)`

## getfacl — 显示任意权限文件信息

### Synopsis

`/usr/bin/getfacl` [-ad] file ...

## Description

访问控制列表 (ACL) 是标准 UNIX 权限的扩展。ACL 信息单独与每个文件关联。你可以确定文件是否有 ACL。对于每个普通文件、特殊文件或管道，`getfacl` 显示所有者、组和 ACL。对于每个目录，`getfacl` 显示所有者、组和默认 ACL。只有目录包含默认 ACL。你可以在不支持 ACL 的文件系统上执行 `getfacl`。如果你没有指定选项，`getfacl` 将显示文件名、所有者、组以及默认 ACL（如果存在）。

## Options

- `-a` 显示文件名、所有者、组以及文件的 ACL。
- `-d` 显示文件名、所有者、组以及默认 ACL（如果存在）。

## Operands

`file` 普通文件、特殊文件或命名管道的路径。

## Output

ACL 输出的格式如下：

```
file:filename

owner: uid

group: gid

user::perm

user:uid::perm

group::perm

group:gid::perm

mask::perm

other::perm

default:user::perm

default:user:uid::perm

default:group::perm

default:group:gid::perm
```
