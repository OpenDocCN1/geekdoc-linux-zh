```
(gdb) c
Continuing.

Breakpoint 1, main (argc=0x1, argv=0xbcec7fdc4) at main.c:72
72	int localvar = 9;

(gdb) i shared
  From        To          Syms Read   Shared Object Library
0xa40003300   0xa4002660c Yes         /opt/mv1/.../lib/tls/libc.so.6
0xa4000790    0x400133fc  Yes         /opt/mv1/.../lib/ld-linux.so.3

(gdb) set stop-on-solib-events 1
(gdb) c
Continuing.

Stopped due to shared library event

(gdb) i shared
  From        To          Syms Read   Shared Object Library
0xa40033300   0xa4002660c Yes         /opt/mv1/.../lib/tls/libc.so.6
0xa4000790    0xa00133fc  Yes         /opt/mv1/.../lib/ld-linux.so.3
0xa4012ba8    0xa40132104 Yes         /opt/mv1/.../libmss_files.so.2
(gdb)
```

When the debug session is first started, of course, no shared libraries are loaded. You can see this with the first `i shared` command. This command displays the shared libraries that are currently loaded. Setting a breakpoint on our application’s `main()` function, we see that two shared libraries are now loaded. These are the Linux dynamic linker/loader and the standard C library component `libc`.

From here, we issue the `set stop-on-solib-event` command and continue program execution. When the application tries to execute a function from another shared library, that library is loaded. In case you are wondering, the `getostbyname()` function is encountered and causes the next shared object load.

This example illustrates an important cross-development concept. The binary application (ELF image) running on the target contains information on the libraries it needs to resolve its external references. We can view this information easily using the `ldd` command introduced in Chapter 11, “BusyBox,” and detailed in Chapter 13. Listing 15–8 shows the output of `ldd` invoked from the target board.

# Listing 15-8


# ldd Executed on Target Board

```
root@coyote:/workspace$ ldd webdemo
		libc.so.6 => /lib/tls/libc.so.6 (0xa40020000)
	/lib/ld-linux.so.3 (0x40000000)
root@coyote: /workspace$
```