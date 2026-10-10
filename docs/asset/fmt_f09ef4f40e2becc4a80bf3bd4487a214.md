
```assembly
$ ppc_44x-gdb --silent vmlinux
(gdb) target remote /dev/ttyS0
Remote debugging /dev/ttyS0
breakpoint () at arch/ppc/kernel/ppc-stub.c:825
825 )
(gdb) b panic
Breakpoint 1 at 0x00c16b18: file kernel/panic.c, line 74.
(gdb) b sys_sync
Breakpoint 2 at 0x00ca50a8c: file fs/buffer.c, line 296.
(gdb) b yosemite_setup_arch
Breakpoint 3 at 0x0c20f438: file arch/ppc/platforms/4xx/yosemite.c, line 116.
(gdb) c
Continuing.

Breakpoint 3, yosemite_setup_arch ()
at arch/ppc/platforms/4xx/yosemite.c:116
116     def = ocp_get_one_device(OCP_VENDER_IBM, OCP_FUNC_EMAC, 0);
(gdb) 1
111     struct ocp_def *def;
112     struct ocp_func_emac_data *emacdata;
113
114     /* Set mac_addr and phy mode for each EMAC */

116     def = ocp_get_one_device(OCP_VENDER_IBM, OCP_FUNC_EMAC, 0);
117     emacdata = def->additions;
118     memcpy(emacdata->mac_addr, __res.bi.enetaddr, 6);
119     emacdata->phy_mode = PHY_MODE_RMII;
120     )
(gdb) p yosemite_setup_arch
$1 = (void (void)) 0x0c20f41c <yosemite_setup_arch>
```

参考列表 14-7，函数 `yosemite_setup_arch()` 实际上位于 `yosemite.c` 文件的第 306 行。对比列表 14-10。我们命中了断点，但 GDB 返回的是文件 `yosemite.c` 第 116 行的断点。乍看之下，调试器与相应源代码之间的行号似乎不匹配。这是 GDB 的 bug 吗？首先，让我们确认编译器生成了调试信息。使用第 13 章描述的 `readelf` 工具^7，我们可以检查编译器生成的函数调试信息：

```bash
$ ppc_44x-readelf --debug-dump-info vmlinux | grep -u \yosemite_setup_arch : tail -n 7
DW_AT_name : (indirect string, offset: 0x9c04): yosemite_setup_arch
DW_AT_decl_file : 1
DW_AT_decl_line : 307
DW_AT_prototyped : 1
DW_AT_low_pc : 0xc020f41c
DW_AT_high_pc : 0xc020f794
DW_AT_frame_base : 1 byte block: 51 (DW_OP_reg1)
```

我们不需要精通阅读 DWARF 调试记录^8 就能看出该函数在我们的源文件中被报告为 307。我们可以使用第 13 章同样引入的 `addr2line` 工具来确认这一点。我们可以使用列表 14-10 中 GDB 得到的地址：

```bash
$ ppc_44x-addr2line -e vmlinux 0xc020f41c
arch/ppc/platforms/4xx/yosemite.c:307
```

此时，GDB 报告我们在 `yosemite.c` 文件第 116 行的断点。为了理解发生了什么，我们需要查看 GDB 报告的函数汇编输出。列表 14-11 是在对 `yosemite_setup_arch()` 函数执行 `disassemble` 命令后 GDB 的输出。

### 列表 14-11 disassemble yosemite_setup_arch

```assembly
(gdb) 0xc020f41c<yosemite_setup_arch:0>: mflr r0
0xc020f420<yosemite_setup_arch:4>: stwu r1,-48(r1)
0xc020f424<yosemite_setup_arch:8>: li r4,512
0xc020f428<yosemite_setup_arch:12>: li r5,0
0xc020f42c<yosemite_setup_arch:16>: li r3,4116
0xc020f430<yosemite_setup_arch:20>: stmw r25,20(r1)
0xc020f434<yosemite_setup_arch:24>: stw r0,52(r1)
0xc020f438<yosemite_setup_arch:28>: bl 0xc000d34 <ocp_get_device>
0xc020f43c<yosemite_setup_arch:32>: lwz r31,32(r3)
0xc020f440<yosemite_setup_arch:36>: lis r4,-16350
0xc020f444<yosemite_setup_arch:40>: li r28,2
0xc020f448<yosemite_setup_arch:44>: addi r4,4,2160
 (continued)
> ^7 对于 PowerPC 架构请使用交叉版本的 readelf，例如 `ppc_44x-readelf`。
> 8 DWARF 规范出现在本章末尾
```

### 列表 14-11 继续

```assembly

0xc020f44c<yosemite_setup_arch+48>: li r5,6

0xc020f450<yosemite_setup_arch+52>: lis r29,-16350

0xc020f454<yosemite_setup_arch+56>: addi r3,31,48

0xc020f458<yosemite_setup_arch+60>: lis r25,-16350

0xc020f45c<yosemite_setup_arch+64>: bl 0xc000c70 <memcpy>

0xc020f460<yosemite_setup_arch+68>: stw r28,44(r31)

0xc020f464<yosemite_setup_arch+72>: li r4,512

0xc020f468<yosemite_setup_arch+76>: lis r5,1

0xc020f46c<yosemite_setup_arch+80>: li r3,4116

0xc020f470<yosemite_setup_arch+84>: addi r26,25,1504

0xc020f474<yosemite_setup_arch+88>: bl 0xc000d344 <ocp_get_one_device>

0xc020f478<yosemite_setup_arch+92>: 

0xc020f47c<yosemite_setup_arch+96>: lwz r31,32(r3)

0xc020f480<yosemite_setup_arch+100>: addi r4,r4,2534

0xc020f484<yosemite_setup_arch+104>: li r5,6

0xc020f488<yosemite_setup_arch+108>: addi r3,31,48

0xc020f48c<yosemite_setup_arch+112>: bl 0xc000c70 <memcpy>

0xc020f490<yosemite_setup_arch+116>: li r4,1017

0xc020f494<yosemite_setup_arch+120>: lis r5,1618

0xc020f498<yosemite_setup_arch+124>: stw r28,44(r31)

0xc020f49c<yosemite_setup_arch+128>: ori r4,r4,16554

0xc020f4a0<yosemite_setup_arch+132>: ori r5,r5,4152

0xc020f4a4<yosemite_setup_arch+136>: addi r3,r29,-15380

0xc020f4a8<yosemite_setup_arch+140>: addi r29,r29,-15380
```
