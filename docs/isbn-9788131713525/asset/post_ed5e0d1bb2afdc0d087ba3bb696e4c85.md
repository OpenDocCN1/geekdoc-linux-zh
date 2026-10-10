
gdb within both of these execution contexts. Listing 14-21 shows an example of such a debug session.

## Listing 14-21
U-Boot Debugging Using JTAG Probe

```
$ ppc-linux-gdb --silent u-boot
(gdb) target remote bdi2001
Remote debugging using bdi:2001
_start () at /home/chris/sandbox/u-boot-1.1.4/cpufmips5xxx/start.S:91
91 r21, BOOTFLAG_COLD /* Normal Power-On */
Current language: auto; currently asm

<< Debug a flash resident c code snippet >>
(gdb) mon break hard
(gdb) b board_init_f
Breakpoint 1 at 0xfff0457c: file board.c, line 366.
(gdb) c
Continuing.

Breakpoint 1, board_init_f (bootflag=0x7fc3afc) at board.c:366
366 gd = (gd_t *) (CFG_INIT_RAM_ADDR + CFG_GBL_DATA_OFFSET);
Current language: auto; currently c
(gdb) bt
#0 board_init_f (bootflag=0x1) at board.c:366
#1 0xfff0456c in board_init_f (bootflag=0x1) at board.c:353
(gdb) i frame
Stack level 0, frame at 0xf000bf50:
pc = 0xfff0457c in board_init_f (board.c:366); saved pc 0xfff0456c
called by frame at 0xf000bf78
Source language c.
Arglist at 0xf000bf50, args: bootflag=0x1
Locals at 0xf000bf50, Previous frame's sp is 0x0

<< Now debug a memory resident code snippet after relocation >>
(gdb) del 1
Discard symbol table from '/home/chris/sandbox/u-boot-1.1.4-powerdna/u-boot'?
(y or n) y
No symbol file now.
(gdb) add-symbol-file u-boot 0x7fa8000
add symbol table from file "u-boot" at
.text_addr = 0x7fa8000
(y or n) y
Reading symbols from u-boot...done.
(gdb) b board_init_r
Breakpoint 2 at 0x7fac6c0: file board.c, line 608.
(gdb) c
Continuing.

Breakpoint 2, board_init_r (id=0x7f85f84, dest_addr=0x7f85f94) at board.c:608
608 /* Initialize RAM version of global data */
(gdb) i frame
Stack level 0, frame at 0x7f85f38:
pc = 0x7fac6c0 in board_init_r (board.c:608); saved pc 0x7fac6b0
called by frame at 0x7f85f68
source language c.
Arglist at 0x7f85f38, args: id=0x7f85f84, dest_addr=0x7f85f84
Locals at 0x7f85f38, Previous frame's sp is 0x0
(gdb) mon break soft
(gdb)
```

Study this example carefully. Some subtleties are definitely worth taking the time to understand. First, we connect to the Abatron BDI-2000 using the target remote command. The IP address in this case is that of the Abatron unit, represented by the symbolic name bdi.[^10] The Abatron BDI-2000 uses port 2001 for its remote gdb protocol connection.

Next we issue a command to the BDI-2000 using the gdb mon command. The mon command tells gdb to pass the rest of the command directly to the remote hardware device. Therefore, mon break hard sets the BDI-2000 into hardware breakpoint mode.

We then set a hardware breakpoint at board_init_f. This is a routine that executes while still running out of Flash memory at address 0xffe10457c. After the breakpoint is defined, we issue the continue c command to resume execution. Immediately, the breakpoint at board_init_f is encountered, and we are free to do the usual debugging activities, including stepping through code and examining data. You can see that we have issued the bt command to examine the stack backtrace and the i frame command to examine the details of the current stack frame.

Now we continue execution again, but this time we know that U-Boot copies itself to RAM and resumes execution from its copy in RAM. So we need to change the debugging context while keeping the debugging session alive. To accomplish this, we discard the current symbol table (symbol-file command with no arguments) and load in the same symbol file again using the add-symbol-file command. This time, we instruct gdb to offset the symbol table to match where U-Boot has relocated itself to memory. This ensures that our source code and symbolic debugging information match the actual memory resident image.

After the new symbol table is loaded, we can add a breakpoint to a location that we know will reside in RAM when it is executed. This is where one of the subtle complications is exposed. Because we know that U-Boot is currently running in Flash but is about to move itself to RAM and jump to its RAM-based copy, we must still use a hardware breakpoint. Consider what happens at this point if we use a software breakpoint. gdb dutifully writes the breakpoint opcode into the specified memory location, but U-Boot overwrites it when it copies itself to RAM. The net result is that the breakpoint is never hit, and we begin to suspect that our tools are broken. After U-Boot has entered the RAM copy and our symbol table has been updated to reflect the RAM-based addresses, we are free to use RAM-based breakpoints. This is reflected by the last command in Listing 14-21 setting the Abatron unit back to soft breakpoint mode.

Why do we care about using hardware versus software breakpoints? If we had unlimited hardware breakpoint registers, we wouldn’t. But this is never the case. Here is what it looks like when you run out of processor-supported hardware breakpoint registers during a debug session:

```
(gdb) b flash_init
Breakpoint 3 at 0x7fbe01e: file flash.c, line 70.
(gdb) c
Continuing.
warning: Cannot insert breakpoint 3:
Error accessing memory address 0x7fbe0: Unknown error 4294967295.
```

Because we are debugging remotely, we aren’t told about the resource constraint until we try to resume after entering additional breakpoints. This is because of the way gdb handles breakpoints. When a breakpoint is hit, gdb restores all the breakpoints with the original opcodes for that particular memory location. When it resumes execution, it restores the breakpoint opcodes at the specified locations. You can observe this behavior by enabling gdb’s remote debug mode:

```
(gdb) set debug remote 1
```

## 14.5 When It Doesn’t Boot

One of the most frequently asked questions on the various mailing lists that serve embedded Linux goes something like this:

> I am trying to boot Linux on my board, and I get stuck after this message prints to my console:
>
> "Uncompressing Kernel Image . . . OK."

Thus starts the long and sometimes frustrating learning curve of embedded Linux! Many things that can go wrong could lead to this common failure. With some knowledge and a JTAG debugger, there are ways to determine what went awry.

### 14.5.1 Early Serial Debug Output

The first tool you might have available is CONFIG_SERIAL_TEXT_DEBUG. This Linux kernel-configuration option adds support for debug messages very early in the boot process. At the present time, this feature is limited to the PowerPC architecture, but nothing prevents you from duplicating the functionality in other architectures. Listing 14-22 provides an example of this feature in use on a PowerPC target using the U-Boot bootloader.

## Listing 14-22
Early Serial Text Debug

```
#! Booting image at 00200000 ...
Image Name: Linux-2.6.14
Created: 2005-12-19 22:24:03 UTC
Image Type: PowerPC Linux Kernel Image (gzip compressed)
Data Size: 607149 Bytes = 592.9 kB
Load Address: 00000000
Entry Point: 00000000
Verifying Checksum ... OK
Uncompressing Kernel Image ... OK
#mach(): Done <- = Start of messages enabled by
#hw:enter <- = CONFIG_SERIAL_TEXT_DEBUG
#hw:hwinit
#hw:mapin
#hw:setio
#hw:exit
setup_arch: enter
setup_arch: bootmem
arch: exit
arch: real exit
```

Using this feature, you can often tell where your board is getting stuck during the boot process. Of course, you can add your own early debug messages in other places in the kernel. Here is an example of its usage found in .../arch/ppc/mm/init.c:

```
/** Map in all of RAM starting at KERNELBASE **/
if (ppc_md.progress)
ppc_md.progress("#hw:mapin", 0x301);
mapin_ram();
```

The OMCC Yosemite platform is an excellent example of this infrastructure. Consult the following files in the Linux source tree[^11] for details of how this debugging system is implemented:

| File | Function | Purpose |
| --- | --- | --- |
| gen550_dbg.c | gen550_init | Serial port setup, called by yosemite.c platform-initialization |
| gen550_dbg.c | gen550_progress | Low-level serial output routine |
| ibm44x_common.c | ibm44x_platform_init | Binds platform-specific progress routine to generic ppc machine-dependent infrastructure |

### 14.5.2 Dumping the printk Log Buffer

When we discussed `printk` debugging in Section 14.3.6, we pointed out some of the limitations of this method. `printk` itself is a very robust implementation. One of its shortcomings is that you can't see any `printk` messages until later in the boot sequence when the console device has been initialized. Very often, when your board hangs on boot, quite a few messages are stuck in the `printk` buffer. If you know where to find them, you can often pinpoint the exact problem that is causing the boot to hang. Indeed, many times you will discover that the kernel has encountered an error that led to a call to `panic()`. The output from `panic()` has likely been dumped into the `printk` buffer, and you can often pinpoint the exact line of offending code.

This is best accomplished with a JTAG debugger, but it is still possible to use a bootloader and its memory dump capability to display the contents of the `printk` buffer after a reset. Some corruption of memory contents might occur as a result of the reset, but log buffer text is usually very readable.

The actual buffer where `printk` stores its message text is declared in the `printk` source file .../kernel/printk.c.

```
static char __log_buf[__LOG_BUF_LEN];
```

[^11]: All these filenames are unique, so they can be found without full pathname references.
