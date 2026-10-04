```
.rodata:00BBAC4 kfqiv13 c 0 dd 6
; DATA XREF:.rodata:08019574
.rodata:00BBAC8 dd offset _2__STRING_5017_0
; "BANNER" dd 0
.rodata:00BBACC
.rodata:00BBAD0 dd offset _2__STRING_0_0
```

此可见，kfqiviw和kfqvip表的各项信息，我们可以获某某个固定视图都包含哪些可查询的字段。

基于上述分析结果，笔者编写了一个专门导出Linux Oracle数据系统表的程序——3]。它导出v$VERSION时，可得到如下所示的信息。

# 指令查询81.4 Result of oracle tables

```
kfqiv_element.viewname: [V$VERSION]: ?:0x03 0x43 0x1 0xffffc85
0x4
kfqvip_element.statement: [select inst_id, BANNER from GV$VERSION where
inst_id = USERENV('Instance')
kfqvip_element.params:
[BANNER]
```

# 指令查询81.5 Result of oracle tables

```
kfqiv_element.viewname: [GV$VERSION]: ?:0x03 0x26 0x2
0xffffc192 0x1
kfqvip_element.statement: [select inst_id, banner from
xversion
kfqvip_element.params:
[INST_ID] [BANNER]
```

固定视图GV$VERSION比V$VERSION多出了一个“instance”字段，除外两者相同。因此，我们只想专注研究数据表X$VERSION就可一反三地理解另一个。与许多名字以X$开头的数据表一样，这个表也没有资料可查。但是，我们可以直接对其进行检索:

```
SQL> select * from x$version;

ADDR                INDEX               INST_ID
BANNER--------------------------------------------------------------------------------
```