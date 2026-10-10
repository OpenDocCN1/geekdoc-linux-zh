
```
WORKSPACE 0x80008000 ;workspace in internal SRAM
FILE u-boot.bin
FORMAT BIN 0xFFFF00000
ERASE 0xFFF00000 ;erase a sector of flash
ERASE 0xFFF10000 ;erase a sector of flash
ERASE 0xFFF20000 ;erase a sector of flash
ERASE 0xFFF30000 ;erase a sector of flash
ERASE 0xFFF40000 ;erase a sector of flash

[REGS]
FILE $reg5200.def
```

## Index

Page numbers followed by $n$ indicate footnotes.

### Symbols

- `/arch` subdirectory, porting Linux, 422-424
- `@` (at sign), 333
- `/etc/exports` file, 230-231
- `/` (forward slash), 132
- `.` (period), 223
- `+` (plus sign), 333
- `/proc` file system, 234-238
  - cpuinfo entry, 238
  - init process, 236-237
  - maps entry, 237
  - mount dependency, 235
  - mounting, 235
- `$T` packet, 363
- `/workspace` directory, mounting, 231
- 32-bit, 38$n$
- 64-bit, 38$n$
- 855GM chipset, 41

### A

- AMCC PowerPC processors, 44-46
- AMD MIPS processors, 55
- apache package, 32
- applets, 286
- applications
  - debugging
    - attaching to running processes, 418
    - via serial ports, 418
  - Flash resident code, debugging, 417
  - with multiple processes, debugging, 411-414
  - multithreaded applications, debugging, 414-417
  - with shared libraries, debugging, 405-411
  - target applications
    - debugging, 400
    - debugging with gdbserver, 403-405
    - stripping, 400-403
- `/arch` subdirectory, porting Linux, 422-424
- architecture branches, porting Linux, 422-424
- architecture objects, composite kernel image, 104-105
- architectures
  - hardware architecture example (embedded systems), 12-13
  - initialization flow of control, 114
  - Linux-supported architectures, 60-61
- access rights, 26
- add-symbol-file command, 379
- addr2line, 346-347
- address breakpoints, 389
- address space, 25-26
- Advanced Telecommunications Computing Architecture (ATCA) platform, 61-62
- Alchemy processors, 55
- AltiVec hardware, 41
- ARM processors, 56, 60
  - Freescale ARM processors, 58–59
  - Intel ARM XScale processors, 59–60
  - TI ARM processors, 56–57
- at sign (@), 333
- ATCA platform, 61–62

### B

- backtrace command, 314
- BDI-2000 sample configuration file, 506–511. See also ITAG probes
- bd_info structure, 437
- Big Kernel Lock (BKL), 453
- bin directory, 132
- binary utilities, 340
  - addr2line, 346–347
  - ldd, 347–348
  - nm, 348
  - objcopy, 345–346
  - objdump, 344–345
  - prelink, 349
  - readelf, 340–344
  - strings, 347
  - strip, 346
- binutils, 340
- BIOS, bootloaders versus, 11–12
- bi_record structure, 437
- BKL (Big Kernel Lock), 453
- block devices, 192
- block sizes, 217
- board-specific information, porting Linux, 436–437
- board-specific initialization
  - MTD, 263–265
  - U-Boot porting example, 177–180
- boards. See hardware platforms; porting U-Boot
- boot block Flash chips, 20
- boot messages, 106–109
- booting. See also build system (kernel); initialization
  - debugging boot process, 417
  - dumping print log buffer, 394–396
  - serial debug output, 393–394
  - trapping crashes with KGDB, 396–397
- from disk with U-Boot, 171
- initrd, 146–149
- with KGDB enabled, 355–358

### bootloaders

- BIOS versus, 11–12
- booting kernel, 16–17
- boot strap loaders versus, 105
- DRAM controller setup, 159–160
- execution context, 163–164
- GRUB, 184, 186
- image compiling and linking, 160–163
- initialization flow of control, 109–110
  - architecture setup, 114
  - head.o module, 111–113
  - main.c module, 113
- initrd and, 146–149
- Lilo, 183–184
- memory addresses, 434
- nonvolatile storage versus RAM, 160
- porting Linux prerequisites, 426
- role of, 158–159
- selecting, 186
- starting target board, 15–16
- U-Boot, 164
- booting from disk, 171
- booting with KGDB enabled, 357
  - command sets, 167
  - configurable commands, 480
  - configuration, 164–166
  - debugging with ITAG probe, 390
- image format, 181-182
- initrd support, 147-149
- kernel, booting, 16-17
- network protocols, 167-170
- NFS root mount example, 304-306
- nonvolatile storage, 170-171
- porting, 172-181
- target board, starting, 15-16
- boom command, 17
- BOOTP (Bootstrap Protocol), U-Boot network operations, 167-170
- BOOTP server, hosting target boards, 298-300
- bootstrap loaders, 105-106
- bottom-half processing, 448
- breakpoints
  - hardware versus software breakpoints, 392
  - with KGDB, 358-360
  - remote debugging, 361-364
  - types of, 389
- Broadcom MIPS processors, 53-54
- browsing sysfs file system, 239-240
- build numbers, 109
- build output (kernel), 71-73
- build system (kernel), 79
  - composite kernel image, 100-102
  - architecture objects, 104-105
  - boot messages, 106-109
  - boot strap loaders, 105-106
  - Image object, 103
  - configuration editors, 82-85
  - dot-config file, 80-82
  - Kconfig files, 88-94
  - makefile targets, 85-88
  - makefiles, 94-95
- building
  - device drivers, 193-197
  - file systems, 242-243
    - cramfs, 228-229
    - JFFS2, 227-229
  - initrd image, 151-152
  - MTD (Memory Technology Devices)
    - services, 250-251
    - root file system, 135
- BusyBox, 274-275
  - commands, 286-287, 484
  - configuring, 275-277
  - cross-compiling, 277
  - defined, 133
  - example rcS initialization script, 283-284
  - executables, 280
  - init, 281-283
  - operations, 278-280
  - root file system, 281-284
  - target installation, 284-286
- busybox package, 32
- bzlImage target, 85

### C

- carrier grade Linux, standards for, 6
- cbrowser, 319-320
- CFI (Common Flash Interface) drivers, 256-257
- character devices, 192
- child processes, debugging, 413
- chipsnets, 41-43
- clocking SDRAM, 494-495
- command line, kernel command line, 114-121
- command sets, U-Boot, 167
- command-line partitioning (MTD), 259-260
- commands
  - backtrace, 314
  - BusyBox, 286-287, 484
  - configurable commands, U-Boot, 480
  - continue, 316
  - fs list, 255-256
  - gdb frame, 314
  - gdb print, 313
  - mkfs.jffs2, 227
  - user-defined commands
    - list of, 370-378
    - .gdbinit file, 369-370
- module_init(), 262
- commercial embedded Linux
  - distributions, 33
- Common Flash Interface (CFI) drivers, 256-257
- CompactFlash modules, 20
- CompactPCI platform, 61
- compilers, cross-development environment, 30-32
- compiling
  - bootloader images, 160-163
  - kernel, 71-73
  - optimization during, 353
- composite kernel image, 100-102
  - architecture objects, 104-105
  - boot messages, 106-109
  - bootstrapped, 105-106
  - Image object, 103
- .config file, 80-82. See also configuration files; configuration, of kernel
- MTD (Memory Technology Devices)
  - configuration, 248-249
  - configurable commands, U-Boot, 480
- configuration
  - BusyBox, 275-277
  - KGDB, 355
  - of kernel, Kconfig files, 88-94
  - MTD (Memory Technology Devices)
    - services, 248-250
    - subsystem, 253
  - U-Boot, 164-166
- configuration editors, 82-85
- configuration files
  - BDI-2000 sample configuration file, 506-511
  - JTAG probes, 387
- configuration rules, U-Boot porting example, 174
- CONFIG_MTD_CHAR element (MTD configuration), 249
- CONFIG_SERIAL_TEXT_DEBUG, 393-394
- connections
  - to KGDB, 358
  - JTAG probes, 386
- contexts. See execution contexts
- continue command, 316
  - remote debugging, 361
- controllers (SDRAM), setup, 495-500
- controllers boards. See hardware platforms
- converting
  - ext2 file system to ext3 file system, 222-223
  - spinlocks to mutexes, 455
- core dumps, debugging, 311-313
- Coreyote, board-specific MTD initialization, 264
- coryte_init() function, 264
- cPCI platform, 61
- cpuno entry (/proc file system), 238
- CPUs, porting U-Boot. See porting U-Boot
