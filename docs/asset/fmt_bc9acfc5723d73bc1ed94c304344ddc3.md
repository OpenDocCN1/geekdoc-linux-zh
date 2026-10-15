
## 3.5 库版本控制

```
  global:

  fool;

  local:

);

LX_1.1 { }
```

命令 `readelf -V` 显示如下：

```
版本段 [.gnu.version] 包含 18 条目：
Addr: 00000000000002c6 Offset: 0x0002c6 Link: 2 (.dynym)
000: 0 (*local*) 0 (*local*) 0 (*local*) 0 (*local*)
004: 0 (*local*) 0 (*local*) 0 (*local*) 0 (*local*)
008: 0 (*local*) 0 (*local*) 2 (LX_1.1)
00c: 2 (LX_1.1) 2 (LX_1.1) 4 (GLIBC_2.0) 5 (GLIBC_2.1)
010: 0 (*local*) 0 (*local*)
```

注意，这一次 Version 定义部分显示的是弱版本（文本框）定义。

接下来，我们通过添加函数 `foo2` 来更新 `libfoo.so.1`：

```c
$cat foo.c

/* foo.c v 1.2 */

extern const char * _version = _message;

extern const char * _message2;

void foo1()

{

    (void) printf(_message);

}

void foo2()

{

    (void) printf(_message2);

}
```

更新 `message.c`：

```c
$cat message.c

/* message.c v1.2 */

const char * _version = "this is an updated string message 1\n";

const char * _message2 = "this is a string message 2\n";
```

更新脚本文件：

```c
LX_1.1 {
    global:
    foo1;
    local:
    *;
};

LX_1.1.1 { };

LX_1.2 {
    global:
    foo2;
};
```

构建库：

```bash
$gcc -fPIC -c foo.c message.c
$gcc -o libfoo.so.1 -shared libfoo.o -Wl,--version-script=scriptfile foo.o message
```

命令 `readelf -V libfoo.so.1` 显示如下：

```
Version symbols section .gnu.version 包含 20 个条目：
Addr: 0000000000000038 Offset: 0x000318 Link: 2 (.dynym)
000: 0 (*local) 0 (*local) 0 (*local) 0 (*local)
004: 0 (*local*) 0 (*local*) 0 (*local*) 0 (*local*)
008: 0 (*local*) 0 (*local*) 0 (*local*) 4 (LX_1.2)
00c: 3 (LX_1.1.1) 2 (LX_1.1) 5 (GLIBC_2.0)
010: 6 (GLIBC_2.1.3) 4 (LX_1.2) 0 (*local*) 0 (*local)

Version description section '.gnu.version_d' 包含 4 个条目：
Addr 0x00000000000340 Offset: 0x00340 Link: 3 (.dynstr)
00000: Rev: 1 Flags Base Index: 1 Cnt: 1 Name: libfoo.so
0001c: Rev: 1 Flags Index: 2 Cnt: 2 Name: LX_1.1
00038: Rev: 1 Flags WEAK Index: 3 Cnt: 1 Name: LX_1.1.1
00054: Rev: 1 Flags none: 4 Cnt: 2 Name: LX_1.2
00070: Parent 1: LX_1.1.1

Version needs section '.gnu.version_r' 包含 1 个条目：
Addr 0x000000000003b8 Offset: 0x0003b8 Link to section: 3 (.dynstr)
00000: Version: 1 File: libfoo.so.6 Cnt: 2
00010: Name: GLIBC_2.1.3 Flags none: 6
00020: Name: GLIBC_2.0 Flags none: 5
```

输出显示版本定义 `LX_1.2` 依赖于版本 `LX_1.1.1`。

更新 `main.c`：

```c
$cat main.c

/* main.c v1.2 */

main()

{

  foo1();

  foo2();

}
```

```bash
$ln -s libfoo.so.1 libfoo.so
$gcc -o main main.c -L. -lfoo
```

使用 `ldd -v` 命令检查 `main`：

```bash
$ ldd -v main
libfoo.so => ./libfoo.so (0xb7ffe000)
libfoo.so.6 => /lib/tls/i586/libfoo.so.6 (0x00b9c000)
/lib/ld-linux.so.2 (0x00b85000)
```

版本信息：

```
./main:
libfoo.so (LX 1.1) => ./libfoo.so
libfoo.so (LX 1.2) => ./libfoo.so
libfoo.so.6 (GLIBC_2.0) => /lib/tls/i586/libfoo.so.6
libfoo.so.6 (GLIBC_2.1.3) => /lib/tls/i586/libfoo.so.6
libfoo.so.6 (GLIBC_2.0) => /lib/tls/i586/libfoo.so.6
/lib/ld-linux.i586.so.2:
d-linux.so.2 (GLIBC_2.1) => /lib/ld-linux.so.2
ld-linux.so.2 (GLIBC_2.3) => /lib/ld-linux.so.2
ld-linux.so.2 (GLIBC_PRIVATE) => /lib/ld-linux.so.2
ld-linux.so.2 (GLIBC_2.0) => /lib/ld-linux.so.2
```

注意 `main` 执行文件引用了版本化库的 `LX_1.1` 和 `LX_1.2`，如框所示。

如果 `main.c` 如下：

```c
main()

{

  foo1();

}

gcc -o main main.c -L. -lfoo
```

生成的执行文件将链接到 `libfoo.so` 的版本 1.2，但如果检查，只会显示对版本 1.1 的引用，因为它只需要从库中解析符号：

```bash
$ ldd -v
libfoo.so => ./libfoo.so (0xb7ffe000)
libc.so.6 => /lib/tls/i586/libc.so.6 (0x00b9c000)
lib/ld-linux.so.2 (0x00b5000)
```

版本信息：

```
.main:
libfoo.so (LX 1.1) => ./libfoo.so
libc.so.6 (GLIBC_2.0) => /lib/tls/i586/libc.so.6
libfoo.so:
  libc.so.6 (GLIBC_2.1.3) => /lib/tls/i586/libc.so.6
  libc.so.6 (GLIBC_2.0) => /lib/tls/i586/libc.so.6
lib/tls/i586/libc.so:
  ld-linux.so.2 (GLIBC_2.1) => /lib/ld-linux.so.2
  ld-linux.so.2 (GLIBC_2.3) => /lib/ld-linux.so.2
  ld-linux.so.2 (GLIBC_PRIVATE) => /lib/ld-linux.so.2
  ld-linux.so.2 (GLIBC_2.0) => /lib/ld-linux.so.2
```
