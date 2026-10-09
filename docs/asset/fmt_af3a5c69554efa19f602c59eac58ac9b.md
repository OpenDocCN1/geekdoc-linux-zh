
| :--- | :--- | :--- |
| OK | | `C:\ALDA2\x64\KSym` |

`*********** 符号加载错误 **********`

| 模块名称 | 错误 |
| :--- | :--- |
| `vmlinux` | 系统找不到指定的文件 |

你可以通过开启诊断 (`!noisy`) 并重复命令来排除相关问题。你还应该验证你的符号路径 (`sympath`) 是正确的。

-   3. 我们可以使用 `log` 命令查看日志并找到指向源码、堆栈指针和堆栈跟踪的 PC。请参考 GDB。

-   4. 我们可以从此转储获取异常跟踪：

```
0: kd-k8-SP

00 fffff800085aa3420 fffffffff00025f0
01 fffff800085aa3420 fffffffff00c3
02 fffff800085aa35a0 fffffffff002f98
03 fffff800085aa3600 fffffffff003c4
04 fffff800085aa3730 fffffffff004e1c
05 fffff800085aa3760 fffffffff00b1a1b
06 fffff800085aa3790 fffffffff001f5c4
07 fffff800085aa37f0 fffffffff004d34
08 fffff800085aa3800 fffffffff0015dc4
09 fffff800085aa3830 fffffffff001dd90
10 fffff800085aa3860 fffffffff0013114
11 fffff800085aa3870 fffffffff00e31c
12 fc fffff800085aa3c0 fffffffff001c160
13 fffff800085aa3440 fffffffff0018cad
14 fffff800085aa3480 fffffffff0013c68
15 fffff800085aa34a0 fffffffff001e1d0
16 fffff800085aa35c0 fffffffff0013cc0
17 fffff800085aa34e0 fffffffff0015d50
18 fffff800085aa37e0 fffffffff0015d928
19 fffff800085aa37f0 fffffffff0018dffc
20 fffff800085aa3810 fffffffff00011011
21 fffff800085aa3900 fffffffff00000000
```

调用点

```
vmlin!_crash_setup_regs+0xa0
vmlin!_crash_kacec+0x60
vmlin!_panic+0x350
vmlin!_die+0x208
vmlin!_die_kernel_fault+0x10c
vmlin!_kernel_fault+0x1bc
vmlin!_do_page_fault+0x220
vmlin!_do_translation+0x74
vmlin!_do_mem_alloc+0x4ca
vmlin!_lel1_abort+0x4c
vmlin!_lelh_64_sync_handler+0x178
vmlin!_lelh_64_sync+0x7c
mod_a+0x1c
vmlin!_init_module+0xa0
vmlin!_load_module+0x7c4
vmlin!_init_module_file+0x90
vmlin!_important_init_module+0x1d0
kernel_arm65_final_module+0x70
vmlin!_invoke_syscall_common+0x48
vmlin!_do_svc+0x228
vmlin!_lel5_64_sync_handler+0x15c
```

-   5. 我们可以在模块中看到问题：

```
0: kd> 1m
start
end\module name

ffff8000 7b870000 fffff8000 7b875000 aes_ce_ciph (deferred)
ffff8000 7b877000 fffff8000 7b88f000 aes_ke_blk (deferred)
ffff8000 7b881000 fffff8000 7b889000 aes_non_blk (deferred)
ffff8000 7b887000 fffff8000 7b88a000 aes_mem_bs (deferred)
ffff8000 7b930000 fffff8000 7b8a2000 x86_pi (deferred)
ffff8000 7b9d0000 fffff8000 7b8a2200 virtio_dma_buf (deferred)
ffff8000 7ba30000 fffff8000 7b8a3000 virtio (deferred)
ffff8000 7bbd0000 fffff8000 7b82c000 polyval_generic (deferred)
ffff8000 7bc03000 fffff8000 7b82d000 polyval_ce (no symbols)
ffff8000 7bc51000 fffff8000 7b82f000 x86_pi (deferred)
ffff8000 7b930000 fffff8000 7b905000 raid (no symbols)
ffff8000 7b9d0000 fffff8000 7b8d7000 sha1_ce (deferred)
ffff8000 7bde0000 fffff8000 7b8ec000 sm4 (no symbols)
ffff8000 7b200000 fffff8000 7b8e0000 sha256_arm64 (deferred)
ffff8000 7b851000 fffff8000 7b8f5000 sha62_ce (deferred)
ffff8000 7b860000 fffff8000 7b8f7000 gash_ce (deferred)
ffff8000 7b7d0000 fffff8000 7b92f000 crctli_of_def (deferred)
ffff8000 7b9b0000 fffff8000 7b928000 libcrc32 (no symbols)
ffff8000 7b9d0000 fffff8000 7b92e000 raid1 (deferred)
ffff8000 7b921000 fffff8000 7b92e000 xor (deferred)
ffff8000 7b929000 fffff8000 7b94c000 async_pcq (no symbols)
```

-   5. 搜索地址 `ffffff9b6000-ffffff9f0000` 在：

```
0: kd> 1lm
start
end\module name

ffffff9b6000 fffff9f000 vmlinux (service: DWARF Symbols)
c:\data\ksym

0: kd-q fffff9b6000 fffff9f000 fffff735-08beccc

ffffff9e20e218ffff735-088c000
```

-   6. 我们还可以搜索字符串和任何三个以上字符的 ASCII 片段（不要忘记小端序，低位在前）

```
0: kd-s-a fffff9b60000 fffff9f000 "bad"

ba9a07d16261485800 4c3b70 18 7548b.H.P.
9b19a2e06261480f41a0 01 98 00 66..i.
9b19f3a36261482141c1-f700 05p049d..I.
9ca01d256261485f769367616c6c0000
9ca509c86261485c63626300 72715fbadlock..
9caf7a466261485c63626300 7479badlock.nvdi
9caf70086261485c63626300 707561badblocks_population
9caf7a762261485c63626300-73badblocks..m

0: kd-dc fffff9b602a9 fffff9f0000

ffffff9b0019e "Zh1"
ffffff9b0019f "Job"
ffffff9b001ac "/"
9b0002a9 "Authu"
9b0002b1 "entiu"
9b0002b9 "cAMDu"
9b0002c7 "GenuE"
9b0002cf "Ineu.."
9b0002d7 "ntielus"

0: kd-dc fffff9b602a9 68745141 6ba116756974e659f810e75 Authent...
```
