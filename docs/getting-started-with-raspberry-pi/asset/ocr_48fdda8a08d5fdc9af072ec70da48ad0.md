Kgdb ports are available for several architectures such as x86, ARM, and PowerPC. When you use kgdb to debug a target embedded device (instead of the PC shown in Figure 21.1), the gdb front-end that you run on your host system needs to be compiled to work with your target platform. For example, to debug a device driver developed for an ARM-based embedded device from your x86-based host development system, you have to use the appropriately generated gdb, often named arm-linux-gdb. The exact name depends on the distribution you use.

# GNU Debugger (gdb)

As mentioned earlier, you can use plain gdb to gather some kernel debug information. However, you can’t step through kernel code, set breakpoints, or modify kernel variables. Let’s use gdb to debug the kernel panic caused by the buggy function in Listing 21.1, but assume this time that trojan_function() is compiled as part of the kernel and not as a module, because you can’t easily peek inside modules using gdb.

This is part of the "oops" message generated when trojan_function() is executed:

```
```
Unable to handle kernel NULL pointer dereference at virtual address 000000ab
...
eax: f7571de0  ebx: ffffе000  ecx: f6c78000  edx: f98df870
...
Stack: c019d731 00000000
 bfffbe8 c0108fab
Call Trace:
 [<c019d731>] [<c013b8ac>] [<c0108fab>]
...```
```

Copy this cryptic "oops" message to oops.txt and use the ksymoops utility to obtain more verbose output. You might need to hand-copy the message if the system is hung:

```
```
bash> ksymoops oops.txt
Code; c019d710 <trojan_function+0/10>
00000000 <EIP>:
Code; c019d710 <trojan_function+0/10> <=====
 0: a1 ab 00 00 00  mov 0xab, %eax <=====
Code; c019d715 <trojan_function+5/10>
 5: c3  ret```
```

2.6 kernels emit "oops" output that can be used as is without the need of decoding using ksymoops if you enable CONFIG_KALLSYMS during kernel configuration.

Looking at the preceding dump, the "oops" has occurred inside trojan_function(). Let’s use gdb to obtain more information. In the following invocation, vmlinux is the uncompressed kernel image, and /proc/kcore is the kernel address space:

```
```bash> gdb vmlinux /proc/kcore```
```