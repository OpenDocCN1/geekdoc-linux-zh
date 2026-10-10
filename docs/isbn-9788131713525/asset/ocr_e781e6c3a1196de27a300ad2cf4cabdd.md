```
16 1907
ret = mod->init();
17 (gdb) 1mod
18 Address           Module
19 0xd102f9a0        loop
20 (gdb) set $m=(struct module *)0xd102f9a0.
21 (gdb) p $m->module_core
22 $1 = (void *) 0xd102000
23 (gdb) add-symbol-file ./drivers/block/loop.ko 0xd102000
24 add symbol table from file "./drivers/block/loop.ko" at
25    .text_addr = 0xd102000
26 (y or n) y
27 Reading symbols from /home/chris/sandbox/linux-2.6.13-amcc/
drivers/block/loop.ko... done.
```

Starting from line 2, we use the gdb user-defined macro connect created earlier in Listing 14-10 to connect to the target board and set our initial breakpoints. We then add the breakpoint in module.c, as shown in line 7, and we issue the continue command (c). Now the kernel completes the boot process and we establish a telnet session into the target and load the loop.ko module (not shown). When the loopback module is loaded, we immediately hit breakpoint #3. gdb then displays the information shown in lines 14 through 16.

At this point, we need to discover the address where the Linux kernel linked our module's .text section. Linux stores this address in the module information structure struct module in the module_core element. Using the 1mod macro we defined in Listing 14-16, we obtain the address of the struct module associated with our loop.ko module. This is shown in lines 17 through 19. Now we use this structure address to obtain the module's .text address from the module_core structure member. We pass this address to the gdb add-symbol-file command, and gdb uses this address to adjust its internal symbol table to match the actual addresses where the module was linked into the kernel. From there, we can proceed in the usual manner to set breakpoints in the module, step through code, examine data, and so on.

We conclude this section with a demonstration of placing a breakpoint in the loopback module's initialization function so that we can step through the module's initialization code. The complication here is that the kernel loads the module's initialization code into a separately allocated portion of memory so that it can be freed after use. Recall from Chapter 5, "Kernel Initializer Functions," our discussion of the __init macro. This macro expands into a compiler attribute that directs the linker to place the marked portion of code into a specially named ELF section. In essence,