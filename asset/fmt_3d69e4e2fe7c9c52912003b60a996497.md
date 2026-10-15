
`ldd` 命令打印指定应用程序的共享库依赖。例如：

```
$ ldd test
librand.so => not found
libc.so.6 => /lib/tls/libc.so.6 (0x042000000)
/lib/ld-linux-x86-64.so.2 (0x00007ffff000)
```
