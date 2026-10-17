
图 19.30. 访问类 1:2 的过滤器键。

# 19.13 使用 `ip` 命令设置 REALM 的 FIB 表输出

从图 19.34 中，我们首先找到 `fib_tables` 全局变量的地址，它被定义为 `fib_table` 结构体的数组。使用该行的 `fsym` 命令转储储 255 个值（32 位），以获取 `fib_table` 的地址，这是系统启动时的默认路由表。在转储输出的第 255 处，我们得到了第 118 行 `fib_table` 的地址。使用第 119 行的 `print` 命令，我们打印 `fib_table` 的内容。我们可以看到第 121 行的数据，然后可以看到第 124 行指向某个地址的插入函数；在这种情况下，它指向第 133–136 行的 `fn_hash_insert()` 函数。第 130 行 `fib_table` 结构体的数据指针是 FIB 数据库私有数据存放。该数据指针指向 FIB 数据库的 `fn_hash` 结构体，其中包含有关区域 (zones) 的信息。

使用 `fib_table` 的大小（0x24 字节），我们打印了第 139 行 `fn_hash` 结构的内容（`fib_table` 的数据字段）。在 19.35 中，`fn_hash` 结构体包含 `fn_zone` 结构体数组和 `fn_zone_list`。`fn_zones` 中的每个元素代表网络掩码（32 位）中的每一位。我们使用 32 位掩码添加 realm，因此 `fn_zones` 的第 32 个元素包含了第 174 行路由表条目的 `fn_zone` 结构体地址。

# TCP/IP 栈的链接与调试

```
627 >> sizeof tc_u_node.sel
628 Offset: 28 bytes.
629 >> base 28
--------------------------------------------
632 hex: 0x1c
633 decimal: 28
634 octal: 34
635 binary: 011100
--------------------------------------------
663 >> sizeof tc_u_32_sel
664 Size of "tc_u_32_sel": 16 bytes
665 >> base 16
--------------------------------------------
668 hex: 0x10
669 decimal: 16
670 octal: 20
--------------------------------------------
673 >> print -x (*tc_u_32_key*)(0xc5eddc + 0x1c + 0x10)
674 struct tc_u_32_key {
675     mask = 0xffffffff
676     val = 0x602a8c0 ipaddr
677     off = 0x00
678     offmask = 0x0
679 }
681 >> print -x (*tc_u_32_key*)(0xc5eddc + 0x1c + 0x10)
682 struct tc_u_32_key {
683     mask = 0xffffff
684     val = 0x17000 sport
685     off = 0x14
686     offmask = 0x0
687 }
```

图 19.31. 类 1:2 的过滤器键。

我们打印图 36 中第 179 行 `fn_zone` 结构的内容。`fn_zone` 结构包含指向第 182 行哈希表的指针、哈表的除因子、第 185 行哈表的索引掩码、第 186 行哈表的顺序以及第 187 行的区域掩码。

然后使用哈希表的指针，转储 16 个字（32 位），获取 `fib_node` 结构的地址，它包含表示路由表条目的 `fn_info` 结构。`fib_node` 数组已初始化并包含了数组第 12 和 15 处的 `fib_node`。

```
689 >> print-x (*tc_u_node *)0xc629070c)
690 struct tc_u_node {
691     next = 0x0
              ...
695     res = struct tcf_result {
696         class = 0xcf72fc0
697         classid = 0xc10003------------> class 1:3
698     }
700     sel = struct tc_u_32_sel {
703     nkeys = 0x2
              ...
709         keys = {
710             [0] struct tc_u_32_key (
715                 )
716         }
717     }
718 }
```

图 19.32. 类 1:3 的过滤器。

```
740 >> print-x (*tc_u_32_key*)(0xc91e04 + 0x1c + 0x10)
741 struct tc_u_32_key {
742     mask = 0xffffffff
743     val = 0x602a8c0 ipaddr
744     off = 0x10
745     offmask = 0x0
746 }
748 >> print-x (*tc_u_32_key*)(0xc91e04 + 0x1c + 0x10)
749 struct tc_u_32_key {
750     mask = 0xff00
751     val = 0xc5000 sport
752     off = 0x14
753     offmask = 0x0 }
```

图 19.33. 类 1:3 的过滤器键。

来自第 195 行的第一个 `fib_node`。`fib_node` 结构包含了第 198 行 `fn_info` 结构的地址。然后第 200 行是目标。我们还可以找到第 202–205 行的 `tos`、`type` 和 `state`。

# 748
# TCP/IP 栈的链接与调试

```
48 >> fsym fib_tables
49 ADDR OFFSET SECTION TYPE
50 ======================
51 0xc3096c0 GLOBAL_DATA fib_tables (unknown)
52 ======================
53 1 symbol found
54 >> dump 0xc3096c0: 00000000 00000000 00000000 :
58 0xc309ab0: 00000000 00000000 cee7974 ......
119 print -x(*fib_table*)cee7974
120 struct fib_table {
121     tb_id = 0xfe
124     tb_insert = 0xc0220c8
130     tb_data = ""
131 }
133 >> fsym 0xc0220c8
134 ADDR OFFSET SECTION TYPE
135 ======================
136 0xc0220c8 LOCAL_TEXT fn_hash_insert (unknown)
137 ======================
138 1 symbol found
```

图 19.34. `fib_tables`。

```
139 >> print-x(*fn_hash*)(0x79074 + 0x24)
140 struct fn_hash {
141     fn_zones = {
142         [0] 0xcced30fc...
150         [8] 0xc53ff2c...
158         [16] 0xc53ff54...
166         [24] 0xcced32d4...
174         [32] 0xc5e04bbc added realm 2 & 3
175     }
176     fn_zone_list = 0xc5e04bbc
177 }
```

图 19.35. 来自 `fib_table` 的 `fn_hash` 对象。

# 使用 `tc` 命令设置路由过滤器的输出

```
179 >> print -x (*fn_zone)*0xc5e04bbc

180 struct fn_zone {
181     fn_next = 0xc5d302d4
```
