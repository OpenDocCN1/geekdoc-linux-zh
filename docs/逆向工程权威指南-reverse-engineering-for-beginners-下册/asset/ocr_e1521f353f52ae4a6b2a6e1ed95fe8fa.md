这样一来，我们就可以看到它调用cygwin1.dll的哪些函数
虽然只会显示一次）以及调用指令的偏移量信息：

One-time INT3 breakpoint: cygwin1.dll!__main (called from
uptime.exe!OEP+0x6d (0x40106d))
One-time INT3 breakpoint: cygwin1.dll!_getuid32 (called from
uptime.exe!OEP+0xba3 (0x401ba3))
One-time INT3 breakpoint: cygwin1.dll!_getudid32 (called from
uptime.exe!OEP+0x8aa (0x4018aa))
One-time INT3 breakpoint: cygwin1.dll!_getgedid32 (called from
uptime.exe!OEP+0xcb7 (0x401cb7))
One-time INT3 breakpoint: cygwin1.dll!_getgid32 (called from
uptime.exe!OEP+0xce6 (0x401ce6))
One-time INT3 breakpoint: cygwin1.dll!_setsysconf (called from
uptime.exe!OEP+0x735 (0x401735))
One-time INT3 breakpoint: cygwin1.dll!_setlocale (called from
uptime.exe!OEP+0x7b2 (0x4017b2))
One-time INT3 breakpoint: cygwin1.dll!_open64 (called from
uptime.exe!OEP+0x994 (0x401994))
One-time INT3 breakpoint: cygwin1.dll!_lseek64 (called from
uptime.exe!OEP+0x7ea (0x4017ea))
One-time INT3 breakpoint: cygwin1.dll!_read (called from
uptime.exe!OEP+0x809 (0x401809))
One-time INT3 breakpoint: cygwin1.dll!_sscanf (called from
uptime.exe!OEP+0x839 (0x401839))
One-time INT3 breakpoint: cygwin1.dll!_uname (called from
uptime.exe!OEP+0x139 (0x401139))
One-time INT3 breakpoint: cygwin1.dll!_time (called from
uptime.exe!OEP+0x22e (0x40122e))
One-time INT3 breakpoint: cygwin1.dll!_localtime (called from
uptime.exe!OEP+0x236 (0x401236))
One-time INT3 breakpoint: cygwin1.dll!_sprintf (called from
uptime.exe!OEP+0x25a (0x40125a))
One-time INT3 breakpoint: cygwin1.dll!_setunset (called from
uptime.exe!OEP+0x3c5 (0x4013c5))
One-time INT3 breakpoint: cygwin1.dll!_getunset (called from
uptime.exe!OEP+0x3b1 (0x4013b1))
One-time INT3 breakpoint: cygwin1.dll!_endutenv (called from
nuptime.exe!OEP+0x3e6 (0x4013e6))
One-time INT3 breakpoint: cygwin1.dll!_puts (called from
uptime.exe!OEP+0x4c3 (0x4014c3))