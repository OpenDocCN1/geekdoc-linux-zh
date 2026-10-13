
`set no_exec_user = 1`

### 在 Solaris 2.6 中带有权限的栈页映射。如下转储如下：

```
/usr/proc/bin/pmap -x 256
256: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 256 256 256 256
```

### 在 Solaris 2.5 中带有权限的栈页映射。如下转储如下：

```
/usr/proc/bin/pmap -x 2564
2564: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 2564 2564 2564 2564
```

这是 Solaris 7 上 64 位可执行文件的 `pmap(1)` 转储，参数如下：

```
set no_exec_user = 1
```

这是 Solaris 7 上 64 位可执行文件的 `pmap(1)` 转储，由于 64 位，SPARC V9 应用程序接口将页面定义为只读，以阻止缓冲区溢出。

```
/usr/proc/bin/pmap -x 9964
9964: tp
地址 字节 共享 私有 权限 文件
0000000000000000 8 8 8 r-x mem
0000000000010000 8 8 8 rw-x mem
0000001000100010 1040 1032 1032 rw-x [ heap ]
FFFFFFFF 696 576 416 160 r-x libc.so.1
FFFFFFFF 64 64 64 rw-x libc.so.1
FFFFFFFF 112 112 112 r-x ld.so.1
FFFFFFFF 16 16 16 r-x libc_par.so.1
FFFFFFFF 8 8 8 r-x [ anon ]
FFFFFFFF 8 8 8 rw-x libbdl.so.1
FFFFFFFF 16 16 16 rw-x [ stack ]
总 字节 2000 1864 552 1312
```
