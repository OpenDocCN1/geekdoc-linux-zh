
```bash
albino_lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo gdb ./trouble/trouble
GNU gdb (Ubuntu 7.11-1-0ubuntu16.04) 7.11
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GNU gdb version 3 or later <http://gnu.org/licenses/gpl.html>
This software is free to change and redistribute.
There is NO WARRANTY, to the extent permitted by law. Type "show copying" and "show warranty" for details.
This gdb was configured as "x86_64-linux-gnu". Type "show configuration" for configuration details.
For bug reporting instructions, please see:
http://www.gnu.org/software/gdb/bugs/gdb/.
Find the GDB manual and other documentation resources online at:
http://www.gnu.org/software/gdb/documentation/.
For help, type "help".
Type "apropos" word to search for commands related to "word"
Reading symbols from ./trouble/trouble...(no debugging symbols found)...done.
(gdb) start
Temporary breakpoint 1 at 0x403c5a
Starting program: /home/albino-lobster/antire_book/chap_6_debugger/dontpanic/build/trouble/trouble
[Inferior 1 (process 39299) exited normally]
(gdb)
```

`Trouble` 退出是因为 `gdb` 通过覆盖字节设置断点修改了 `main()`。当 `Trouble` 对 `main()` 计算校验和时，它将与存储的校验和不匹配，导致 `Trouble` 退出。
