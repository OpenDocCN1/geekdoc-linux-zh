如果我们在文件kqf.o里搜索文本 “select BANNER from
GV$VERSION where inst_id = USERENV('Instance')”,那么就会发
现它在kqvip表里。

# 指令清单81.2 kqf.o

```
.rodata:080185A0 kfqvip      dd offset _2__STRING_11126_0 ;
DATA XREF: kfgvcn+18
.rodata:080185A0                               ;
kfqvt+F
.rodata:080185A0                               ;
"select inst_id, decode(indx,1,'data ✓
  \u bloc ...
.rodata:080185A4      dd offset kfqv459_c_0
.rodata:080185A8      dd 0
.rodata:080185AC      dd 0

...
.rodata:08019570      dd offset _2__STRING_11378_0 ;
"select BANNER from GV$VERSION ✓
  \u where in "..."
.rodata:08019574      dd offset kfqv133_c_0
.rodata:08019578      dd 0
.rodata:0801957C      dd 0
.rodata:08019580      dd offset _2__STRING_11379_0 ;
"select inst_id, decode(bitand(✓
  \u cfflg,1),"..."
.rodata:08019584      dd offset kfqv403_c_0
.rodata:08019588      dd 0
.rodata:0801958C      dd 0
.rodata:08019590      dd offset _2__STRING_11380_0 ;
"select STATUS , NAME, ✓
  \u IS_RECOVERY_DEST..."
.rodata:08019594      dd offset kfqv199_c_0
```

这个每个元素由4个字段组成。而且它同样包含了1023元
素。第二个字段指向另一个表——就是与表名相对应的固定视
图。V$VERSION的表格只有两个元素，第一个是6（后字符符的长
度），第二个是BANNER字符串。此后是终止符——零字符和C语言字符
null。

# 指令清单81.3 kqf.o