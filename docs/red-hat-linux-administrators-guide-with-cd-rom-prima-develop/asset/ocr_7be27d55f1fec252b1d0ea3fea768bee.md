Because there is often more text than can fit in a single xterm or console window — it is a good idea to either review the initial text of the message by using the scroll bar or by parsing out the message by using the commands less and more. Either of these two commands allows the user to page through the remainder of the message by pressing the space bar or Enter key. Under a console window you can also review previous text within a text editor by selecting the Alt+PageUp and Alt+PageDown keys respectively to review or forward through text. Listing 2.1 is an example of a dmesg request and some sample output.

# Listing 2.1 A Sample dmesg Request on a Vanilla Red Hat 6.2 Install

```
1. [root@Backup /root]# dmesg | more
2. Linux version 2.2.24 - 5.0 (root@porky.devel.redhat.com) (gcc version egcs - 2.91 .66 19990314 / Linux (egcs - 1.1.2 release))
   #1 Tue Mar 7 21:07:39 EST 2000
3. relocating initrd image:
4.     initrd_start: 0xc00f960000    initrd_end: 0xc00ffff7b
5.     mem_start: 0xc0026c0000      mem_end: 0xc040f0000
6.     initrd_size: 0x00069f7b     dest: 0xc04095000
7. Detected 59860287 Hz processor.
8. Console: colour VGA + 80x25
9. Calibrating delay loop ... 596.38 BogoMIPS
10. Memory: 63161k/66556k available (1060k kernel code, 416k reserved, 976k data, 64k init, 0k bigmem)
11. Dentry hash table entries: 262144 (order 9, 2048k)
12. Buffer cache hash table entries: 65536 (order 6, 256k)
13. Page cache hash table entries: 16384 (order 4, 64k)
14. VFS: Disk quotas version dquot - 6.4.0 initialized
15. L1 I Cache: 64K L1 D Cache: 64K
16. L2 Cache: 512K
17. CPU: AMD AMD Athlon(tm) Processor stepping 01
18. Enabling extended fast FPU save and restore ... done.
19. Checking 386/387 coupling ... OK, FPU using exception 16 error reporting.
```